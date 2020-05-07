---
title: Технический справочник по загрузке приложений
titleSuffix: Configuration Manager
description: Технический справочник по устранению неполадок в Configuration Manager при загрузке приложений.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: 41c29a07-9bf6-4ec4-b3f2-1c05e001eff7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: effa8115a5023a8e0611f6bc4245a101b3a47e38
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688862"
---
# <a name="application-download-in-configuration-manager"></a>Загрузка приложения в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Прежде чем продолжить, ознакомьтесь с [клиентскими компонентами для развертывания приложений](client-components-technical-reference.md), чтобы понять обработку заданий агентами DCM и CI.

## <a name="download-initiation"></a>Инициация загрузки

Загрузка содержимого приложения инициируется компонентом агента CI на клиенте на этапе **StateDownloadingContents**. Этот процесс выполняется одинаково независимо от того, где развернуто приложение: в коллекции устройств или коллекции пользователей.

- Для **доступных** развертываний содержимое приложения загружается, когда пользователь инициирует его установку из центра программного обеспечения.
- Для **обязательных** развертываний содержимое приложения загружается при активации назначения и после того, как приложение будет признано применимым. Сведения об активации назначения см. в статьях [Развертывание приложения в коллекции устройств](device-deployment-technical-reference.md) или [Развертывание приложения в коллекции пользователей](user-deployment-technical-reference.md).

Когда агент CI инициирует загрузку содержимого, он создает задачу, которая обрабатывается компонентом диспетчера задач CI. Затем диспетчер задач CI инициирует загрузку содержимого. Это действие можно отследить в файле **CITaskMgr.log** с использованием уникального идентификатора типа развертывания.

<pre><code class="lang-text"><b>Initiating task ContentDownload</b> for CI ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44.2 (ConfigMgr Toolkit - Windows Installer (*.msi file)) for target: , consumer: {53EA65C2-D596-4215-83E4-F7007B78E18C}
</code></pre>

## <a name="distribution-point-location"></a>Расположение точки распространения

Все задачи загрузки обрабатываются компонентом доступа к содержимому, который отвечает за управление кэшем клиента. После того как задача скачивания будет создана, компонент доступа к содержимому проверяет, доступно ли содержимое в кэше клиента. Если содержимое недоступно, оно создает запрос распространения для получения списка точек распространения, из которых можно получить содержимое. Это действие можно отследить в файлах **CAS.log** и **LocationServices.log** на клиенте с помощью уникального идентификатора содержимого.

```text
Requesting locations synchronously for content Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1 with priority Foreground
ContentLocationRequest : <Request XML Body>
Reply Message Body : <Reply XML Body>
```

> [!IMPORTANT]
> Несмотря на то, что компонент служб определения местоположения обрабатывает запросы на размещение, он не запрашивает расположения из точки управления напрямую. Все запросы к точке управления обычно проходят через компонент обмена сообщениями CCM, который записывает журнал в файл **CcmMessaging.log**.

XML-файл ответа с расположением содержит список точек распространения на основе группы границ клиента. Этот список анализируется и сохраняется в WMI на клиенте в соответствии с [приоритетом источника содержимого](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#content-source-priority). Это действие можно отследить в файле **ContentTransferManager.log**с помощью уникального идентификатора содержимого и поискового запроса `Persisted location`. 

Если XML-файл ответа расположения не содержит точек распространения, в файле **ContentTransferManager.log** появится сообщение `Received empty location update` и при скачивании приложения клиент может зависнуть на 0 %. Обычно такой ответ может возникать из-за проблем с конфигурацией группы границ. Дополнительные сведения см. в разделе [Сбои загрузки](../deploy-use/troubleshoot-application-deployment.md#download-failures).

## <a name="content-download"></a>Загрузка содержимого

После получения расположения точек распространения компонент доступа к содержимому создает задание передачи содержимого. Это действие можно отследить в файле **CAS.log** с помощью уникального идентификатора содержимого.

<pre><code class="lang-text">Submitted CTM job <b>{6D0EA720-EB4E-4893-8395-8B27470A6CFB}</b> to download Content <b>Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1</b> under context System
</code></pre>

Затем диспетчер распространения содержимого создает задание службы передачи данных для загрузки содержимого. Это действие можно отследить в файле **ContentTransferManager.log** на клиенте с помощью уникального идентификатора содержимого.

<pre><code class="lang-text">CTM job <b>{6D0EA720-EB4E-4893-8395-8B27470A6CFB}</b> (corresponding DTS job <b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b>) started download from '<Distribution Point URL>/<b>Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1</b>' for full content download.
</code></pre>

> [!NOTE]
> Эта запись журнала может использоваться для обнаружения идентификаторов заданий диспетчера распространения содержимого и службы передачи данных, которые можно использовать для отслеживания передачи содержимого в файлах **ContentTransferManager.log** и **DataTransferService.log** соответственно.

Служба передачи данных выполняет загрузку содержимого приложения, создавая задание фоновой интеллектуальной службы передачи (BITS), и ожидает завершения загрузки. Это действие можно отследить в файле **DataTransferService.log** на клиенте с помощью идентификатора задания диспетчера распространения содержимого, полученного из файла **ContentTransferService.log**.

<pre><code class="lang-text">Starting BITS job '{40263E01-2EDD-462F-ABBA-A5E892CB9229}' for DTS job '<b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b>' under user 'S-1-5-18'.
DTSJob <b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b> in state 'DownloadingData'.
DTS job <b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b> has completed
</code></pre>

По завершении загрузки будет отправлено уведомление компоненту доступа к содержимому. Компонент доступа к содержимому затем проверяет скачанное содержимое, чтобы убедиться, что содержимое не было изменено во время загрузки. Это действие можно отследить в файле **CAS.log** с помощью уникального идентификатора содержимого.

```text
Hash verification succeeded for content Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1 downloaded under context System
```

Наконец, после проверки содержимого агент CI получает уведомление о завершении задачи, а задание агента CI переходит к следующему этапу.

<pre><code class="lang-text">CIAgentJob({2BF84225-C9E8-49A6-A308-A160C4B799D3}): CAgentJob::HandleEvent(<b>Event=CITaskComplete, CurrentState=StateDownloadingContents</b>)
</code></pre>

## <a name="next-steps"></a>Дальнейшие шаги

- [Установка приложения](deployment-install-technical-reference.md)
