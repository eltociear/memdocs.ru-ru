---
title: Развертывание и обновление Microsoft Edge версии 77 и более поздних версий
titleSuffix: Configuration Manager
description: Развертывание и обновление Microsoft Edge версии 77 и более поздней с Configuration Manager
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 73b420be-5d6a-483a-be66-c4d274437508
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2c3a542355dfa01e5f4f5be12f7b1bac10f30250
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689522"
---
# <a name="microsoft-edge-management"></a>Управление Microsoft Edge

*Область применения: Configuration Manager (Current Branch)*

Кардинально обновленный Microsoft Edge готов для использования в корпоративной среде. Начиная с версии Configuration Manager 1910 вы можете развернуть [Microsoft Edge версии 77 и более поздней](https://docs.microsoft.com/deployedge/) для пользователей. С помощью PowerShell устанавливается выбранная сборка Edge. Кроме того, скрипт отключает автоматические обновления для Microsoft Edge, чтобы ими можно было управлять с помощью Configuration Manager.

## <a name="deploy-microsoft-edge"></a><a name="bkmk_Microsoft_Edge"></a> Развертывание Microsoft Edge
<!--4561024-->
Администраторы могут выбрать канал Beta, Dev или стабильный канал, а также версию клиента Microsoft Edge для развертывания. Каждый выпуск содержит нововведения и улучшения, основанные на отзывах наших клиентов и сообщества.

### <a name="prerequisites-for-deploying"></a>Необходимые условия для развертывания

Для клиентов, нацеленных на развертывание Microsoft Edge:

- По умолчанию [Политика выполнения](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_execution_policies) в PowerShell не может быть ограниченной.
  - PowerShell запускается для выполнения установки.

Устройству, на котором запущена консоль Configuration Manager, требуется доступ к следующим конечным точкам:

|Расположение|Используйте|
|---|---|
|`https://edgeupdates.microsoft.com/api/products?view=enterprise`|Сведения о выпусках Microsoft Edge|
|`http://dl.delivery.mp.microsoft.com`|Содержимое для выпусков Microsoft Edge|

### <a name="verify-microsoft-edge-update-policies"></a><a name="bkmk_autoupdate"></a> Проверка политик обновления Microsoft Edge

#### <a name="configuration-manager-version-1910"></a>Configuration Manager версии 1910

В версии 1910 при развертывании Microsoft Edge сценарий установки отключает автоматические обновления для Microsoft Edge, что позволяет управлять ими с помощью Configuration Manager. Это поведение можно изменить с помощью групповой политики. Дополнительные сведения см. в разделе [Планирование развертывания Microsoft Edge](https://docs.microsoft.com/deployedge/deploy-edge-plan-deployment#define-and-configure-policies) и [Политики обновления Microsoft Edge](https://docs.microsoft.com/DeployEdge/microsoft-edge-update-policies).

#### <a name="configuration-manager-version-2002-and-later"></a>Configuration Manager версии 2002 и более поздних
<!--4561024-->
Начиная с версии 2002, можно создать приложение Microsoft Edge, которое настроено на получение автоматических обновлений, а не на их отключение. Это изменение позволяет выбрать управление обновлениями для Microsoft Edge с помощью Configuration Manager или разрешить для Microsoft Edge автоматическое обновление. При создании приложения выберите **Allow Microsoft Edge to automatically update the version of the client on the end user's device** (Разрешить Microsoft Edge автоматически обновлять версию клиента на устройстве пользователя) на странице **параметров Microsoft Edge**. Если вы ранее использовали групповую политику для изменения этого поведения, групповая политика перезапишет параметр, созданный Configuration Manager во время установки Microsoft Edge.

[![Параметр автоматического обновления Microsoft Edge](./media/4561024-autoupdate-edge.png)](./media/4561024-autoupdate-edge.png#lightbox)

### <a name="create-a-deployment"></a>Создание развертывания

Создайте приложение Microsoft Edge с помощью встроенного интерфейса, который упрощает управление Microsoft Edge:

1. В разделе **Библиотека программного обеспечения** консоли есть новый узел **Управление Microsoft Edge**.
1. Выберите **Создать приложение Microsoft Edge** на ленте, либо щелкнув правой кнопкой мыши узел **Управление Microsoft Edge**.

   ![Действие при правом щелчке узла "Управление Microsoft Edge"](./media/4561024-create-microsoft-edge-application.png)

1. На странице **Параметры приложения** мастера укажите имя, описание и расположение содержимого для приложения. Убедитесь, что указанная папка расположения содержимого пуста.
1. На странице **Параметры Microsoft Edge** выберите:
   - канал для развертывания;
   - версию для развертывания.
   - Если вы хотите **Разрешить Microsoft Edge автоматически обновлять версию клиента на устройстве пользователя** (добавлено в версии 2002)
1. На странице **Развертывание** укажите, требуется ли развернуть приложение. Если выбрать **Да**, можно указать параметры развертывания для приложения. Дополнительные сведения о параметрах развертывания см. в разделе [Развертывание приложений](deploy-applications.md#bkmk_deploy-general).
1. В **центре программного обеспечения** на клиентском устройстве пользователь может просмотреть и установить приложение.

   ![Страница "Параметры Microsoft Edge" в мастере развертывания](./media/4561024-software-center-install-edge.png)

### <a name="log-files-for-deployment"></a>Файлы журналов для развертывания

|Расположение|Журнал|Используйте|
|---|---|---|
| Сервер сайтов|SMSProv.log|Отображает сведения при сбое создания приложения или развертывания.|
| [Различается](../../core/plan-design/hierarchy/log-files.md)|PatchDownloader.log| Отображает сведения при сбое скачивания содержимого.|
| Клиент|  AppEnforce.log|Отображает сведения об установке.|

## <a name="update-microsoft-edge"></a>Обновление Microsoft Edge
<!--4831871-->

Начиная с версии Configuration Manager 1910 вы увидите узел с именем **Все обновления Microsoft Edge** в разделе **Управление Microsoft Edge**. Этот узел помогает управлять обновлениями для всех каналов Microsoft Edge.<!--initial edge updates released Jan 15,2020-->

1. Чтобы получить обновления для Microsoft Edge, убедитесь, что у вас установлена классификация **Обновления** и продукт **Microsoft Edge**, [выбранный для синхронизации](../../sum/get-started/configure-classifications-and-products.md).

   [![Выбор Microsoft Edge в качестве продукта в свойствах точки обновления программного обеспечения](./media/4831871-microsoft-edge-product-sup.png)](./media/4831871-microsoft-edge-product-sup.png#lightbox)

1. В рабочей области **Библиотека программного обеспечения** разверните узел **Управление Microsoft Edge** и щелкните узел **Все обновления Microsoft Edge**.

1. При необходимости щелкните **Синхронизировать обновления программного обеспечения** на ленте, чтобы начать синхронизацию. Дополнительные сведения см. в статье [Synchronize software updates](../../sum/get-started/synchronize-software-updates.md) (Синхронизация обновлений программного обеспечения).

   ![Узел "Все обновления Microsoft Edge"](./media/4831871-all-microsoft-edge-updates.png)

1. Управляйте обновлениями Microsoft Edge и развертывайте их, как любые другие обновления, например добавляя их в [правило автоматического развертывания](../../sum/deploy-use/automatically-deploy-software-updates.md). Некоторые из общих задач обновления, которые можно выполнить из узла **Все обновления Microsoft Edge**, включают:

   - [Создание поэтапного развертывания](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md)
   - [Развертывание обновлений программного обеспечения вручную](../../sum/deploy-use/manually-deploy-software-updates.md)
   - [Скачивание обновлений программного обеспечения](../../sum/deploy-use/download-software-updates.md)

## <a name="microsoft-edge-management-dashboard"></a><a name="bkmk_edge-dash"></a> Панель мониторинга "Управление Microsoft Edge"
<!--3871913-->
*(Представлено в версии 2002)*

Начиная с Configuration Manager 2002, панель мониторинга "Управление Microsoft Edge" предоставляет подробные сведения об использовании Microsoft Edge и других браузеров. На этой панели мониторинга вы можете:

- увидеть, на каком количестве устройств установлен Microsoft Edge;
- увидеть, на каком количестве клиентов установлены разные версии Microsoft Edge.
   - Эта диаграмма не включает канал канареечного развертывания;
- просмотреть установленные браузеры на разных устройствах.
- просмотреть предпочтительный браузер по устройству. <!--5907383-->
   - В настоящее время для выпуска 2002 эта диаграмма будет пустой.

### <a name="prerequisites-for-the-dashboard"></a>Необходимые условия для панели мониторинга

Включите следующие свойства в классы [инвентаризации оборудования](../../core/clients/manage/inventory/extend-hardware-inventory.md) для панели мониторинга "Управление Microsoft Edge".

- **Установленное программное обеспечение — аналитика активов (SMS_InstalledSoftware)**
   - Код программного обеспечения
   - Название продукта
   - Версия продукта

- **Браузер по умолчанию (SMS_DefaultBrowser)**
   - Идентификатор программы браузера

- **SMS_BrowserUsage (SMS_BrowserUsage)**
   - BrowserName
   - UsagePercentage

### <a name="view-the-dashboard"></a>Просмотр панели мониторинга

В рабочей области **Библиотека программного обеспечения** щелкните **Управление Microsoft Edge**, чтобы открыть панель мониторинга. Измените коллекцию для данных графа, нажав кнопку **Обзор** и выбрав другую коллекцию. По умолчанию в раскрывающемся списке отображается пять самых крупных коллекций. При выборе коллекции, которая отсутствует в списке, вновь выбранная коллекция будет находиться в нижней части раскрывающегося списка.

[![Панель мониторинга "Управление Microsoft Edge"](./media/3871913-microsoft-edge-dashboard.png)](./media/3871913-microsoft-edge-dashboard.png#lightbox)

## <a name="next-steps"></a>Дальнейшие шаги

[Мониторинг приложений](monitor-applications-from-the-console.md)

[Мониторинг обновлений программного обеспечения](../../sum/deploy-use/monitor-software-updates.md)

[Мониторинг поэтапных развертываний и управление ими](../../osd/deploy-use/manage-monitor-phased-deployments.md)
