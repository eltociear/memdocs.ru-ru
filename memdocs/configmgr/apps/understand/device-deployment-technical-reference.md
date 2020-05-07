---
title: Технический справочник по развертыванию приложений в коллекциях устройств
titleSuffix: Configuration Manager
description: Технический справочник по устранению неполадок развертывания приложений в коллекциях устройств в Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: 4e62b04d-fe56-42ed-87dc-e673cf061d52
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1965029a1933793057dc5768bacb391afd645404
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688792"
---
# <a name="application-deployment-for-device-collections"></a>Развертывание приложений в коллекции устройств

*Область применения: Configuration Manager (Current Branch)*

При развертывании приложения в коллекции устройств политика нацеливается на все устройства в коллекции независимо от цели развертывания. В этой статье описываются процессы скачивания политики и развертывания приложений на клиенте.

> [!TIP]
> Все сведения, необходимые для просмотра журналов клиента, можно получить, выполнив запрос SQL, указанный в разделе [Перед началом работы](app-deployment-technical-reference.md#before-you-begin).

## <a name="policy-download"></a>Скачивание политики

После того как политика развертывания приложения будет нацелена на клиент, клиент скачает политику в следующем цикле ее опроса. При скачивании политики, помимо политики развертывания, клиент скачивает связанные политики. В их число входят политика для приложения, тип развертывания, глобальные условия и т. д. Действие по скачиванию политики можно отследить в файле **PolicyAgent.log** на клиенте с помощью уникального идентификатора приложения или назначения.

<pre><code class="lang-text">Download of policy CCM_Policy_Policy5.PolicyID="{<b>3AC57DFE-3F87-4C59-930B-B9F57CB41B91</b>}",PolicySource="SMS:PS1",PolicyVersion="1.00" completed (DTS Job ID: {AE88E639-0E59-40D7-AAA9-4403AAE6EE82})
Policy state for [CCM_Policy_Policy5.PolicyID="{<b>3AC57DFE-3F87-4C59-930B-B9F57CB41B91</b>}",PolicySource="SMS:PS1",PolicyVersion="1.00"] is currently [Active]
</code></pre>

После того как политики будут скачаны на клиенте, компонент планировщика создаст расписания для активации и применения развертывания.

## <a name="deployment-activation"></a>Активация развертывания

Оценка приложения инициируется при активации развертывания. Компонент планировщика создает расписание для активации назначения в доступное время, настроенное в развертывании. Это действие можно отследить в файле **Scheduler.log** на клиенте, используя уникальный идентификатор назначения приложения.

- Для **обязательных** развертываний создается расписание активации, но во избежание конфликтов ресурсов на серверах сайта и точках распространения в нем предусмотрена задержка до двух часов. Задержка помогает избежать конфликтов, так как если приложение считается применимым согласно правилам требований, его содержимое может быть скачано во время оценки.

    <pre><code class="lang-text">SMSTrigger '15AF8C4000080000' for scheduler '<b>Machine/{5F2FA409-C9B2-4100-8BC8-051820311DE1}</b>' will fire at 08/15/2019 01:44:00 PM with randomization.
    </code></pre>

- Для **доступных** развертываний создается расписание для запуска активации в доступное время, настроенное в развертывании.

    <pre><code class="lang-text">SMSTrigger '1E4F8C4000080001' for scheduler '<b>Machine/{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}</b>' will fire at 08/15/2019 01:13:33 PM without randomization.
    </code></pre>

Когда наступает указанное время, компонент планировщика отправляет сообщение об активации агенту DCM для выполнения оценки приложения.

<pre><code class="lang-text">Sending message for schedule '<b>Machine/{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}</b>' (Target: 'direct:DCMAgent', Name: '')
</code></pre>

Агент DCM получает это сообщение и создает задание для оценки приложения.

```text
CDCMAgent::HandleMessage - Message received for machine: '<?xml version='1.0' ?><CIAssignmentMessage MessageType='Activation'><AssignmentID>{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}</AssignmentID></CIAssignmentMessage>'
```

## <a name="deployment-enforcement"></a>Принудительное применение развертывания

Установка приложения инициируется при применении развертывания.

- Для **обязательных** развертываний после скачивания политики планировщик создает расписание с крайним сроком, чтобы выполнить развертывание приложения при наступлении этого момента. По умолчанию расписание крайнего срока не задается случайным образом. Поведение случайного выбора для активации можно контролировать с помощью параметра клиента [Запретить случайный выбор срока](../../core/clients/deploy/about-client-settings.md#disable-deadline-randomization).

    <pre><code class="lang-text">SMSTrigger '15EF8C4000080000' for scheduler '<b>Machine/DEADLINE:{5F2FA409-C9B2-4100-8BC8-051820311DE1}</b>' will fire at 08/15/2019 03:05:00 PM without randomization.
    </code></pre>

    При достижении крайнего срока компонент планировщика отправляет сообщение с указанием крайнего срока в агент DCM. 

    <pre><code class="lang-text">Sending message for schedule '<b>Machine/DEADLINE:{5F2FA409-C9B2-4100-8BC8-051820311DE1}</b>' (Target: 'direct:DCMAgent', Name: '')
    </code></pre>

    Агент DCM получает это сообщение и создает задание для принудительного применения приложения.
  
    ```text
    CDCMAgent::HandleMessage - Message received for machine: '<?xml version='1.0' ?><CIAssignmentMessage MessageType='EnforcementDeadline'><AssignmentID>{5F2FA409-C9B2-4100-8BC8-051820311DE1}</AssignmentID></CIAssignmentMessage>'
    ```

    > [!NOTE]
    > Для развертываний с крайним сроком в прошлом приложение активируется и развертывается немедленно с помощью одного и того же задания агента DCM, которое выполняет действия по оценке, скачиванию и установке.

- Для **доступных** развертываний расписание крайнего срока отсутствует, поскольку принудительное развертывание выполняется при инициации установки приложения пользователем из центра программного обеспечения. Когда пользователь запускает установку, создается задание агента DCM для выполнения оценки, скачивания и установки приложения. Это действие можно отследить в файле **DCMAgent.log** на клиенте.

## <a name="next-steps"></a>Дальнейшие шаги

- [Основные сведения о клиентских компонентах развертывания приложений](client-components-technical-reference.md)
