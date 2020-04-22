---
title: Проверка готовности к обновлению
titleSuffix: Configuration Manager
description: Интегрируйте решение "Проверка готовности к обновлению" с Configuration Manager, чтобы получить доступ к данным совместимости обновления до Windows 10, а также к целевым устройствам для обновления или исправления.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 01/31/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 68407ab8-c205-44ed-9deb-ff5714451624
ms.openlocfilehash: 18d8b66a7b9f5ad889645cbc8e48ebcbfe6550a9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696322"
---
# <a name="integrate-upgrade-readiness-with-configuration-manager"></a>Интеграция решения "Проверка готовности к обновлению" с Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

> [!Important]  
> Поддержка службы Windows Analytics прекращена 31 января 2020 г. Дополнительные сведения см. в статье базы знаний [KB 4521815 о прекращении поддержки Windows Analytics с 31 января 2020 г.](https://support.microsoft.com/help/4521815/windows-analytics-retirement)
>
> Ее преемницей станет служба "Аналитика компьютеров". Дополнительные сведения см. в статье [Что такое Аналитика компьютеров](../../../desktop-analytics/overview.md).

Если сайт Configuration Manager был подключен к решению "Проверка готовности к обновлению", необходимо удалить его и заново настроить клиенты.

## <a name="remove-upgrade-readiness-connection"></a><a name="bkmk_remove"></a> Удаление подключения к решению "Проверка готовности к обновлению"

1. Откройте консоль Configuration Manager от имени пользователя с ролью **Полный администратор**.

1. Перейдите в рабочую область **Администрирование**, разверните узел **Облачные службы**, а затем выберите узел **Службы Azure**.

1. Удалите службу Windows Analytics.

## <a name="reconfigure-clients"></a>Повторная настройка клиентов

### <a name="unenroll-devices"></a>Отмена регистрации устройств

Во-первых, проверьте параметры сайта по умолчанию или любые настраиваемые параметры клиентского устройства в группе **Windows Analytics**. Например, отключите следующий параметр: **Управление параметрами телеметрии Windows с помощью Configuration Manager**.

> [!IMPORTANT]
> Если вы планируете использовать Аналитику компьютеров, будут настроены параметры диагностических данных Windows на клиентах. Используйте мастер подключения к службам Azure, чтобы настроить эти параметры для использования с Аналитикой компьютеров. Дополнительные сведения см. в статье [How to connect Configuration Manager with Desktop Analytics](../../../desktop-analytics/connect-configmgr.md) (Подключение Configuration Manager к Аналитике компьютеров).

На зарегистрированных устройствах удалите значение CommercialID из следующих разделов реестра Windows:

- `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`
- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

### <a name="windows-diagnostic-data-configuration"></a>Конфигурация диагностических данных Windows

Если вы не хотите, чтобы устройства продолжали отправлять диагностические данные:

- Windows 10: установите уровень диагностических данных **Безопасность**.
- Windows 7 с пакетом обновления 1 (SP1) или Windows 8.1: отключите **ключ согласия на сбор коммерческих данных**.

Задайте эти значения с помощью одного из следующих методов:

- Групповая политика (**Конфигурация компьютера** > **Административные шаблоны** > **Компоненты Windows** > **Сборки для сбора данных и предварительные сборки**).
- Управление мобильным устройством (MDM), например [Microsoft Intune](https://docs.microsoft.com/intune/device-restrictions-windows-10#reporting-and-telemetry).

Дополнительные сведения см. в статье [Настройка диагностических сведений Windows в вашей организации](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization).

> [!NOTE]  
> После применения этих изменений устройства немедленно прекращают отправлять диагностические данные. На остановку обработки аналитических сведений для рабочей области может уйти 24–48 часов. Корпорация Майкрософт удаляет эти данные из своих облачных служб в течение 30 дней или менее.

<!--
Upgrade Readiness is a part of [Windows Analytics](https://docs.microsoft.com/windows/deployment/upgrade/manage-windows-upgrades-with-upgrade-readiness). It allows you to assess and analyze the readiness of devices in your environment for an upgrade to Windows 10. Integrate Upgrade Readiness with Configuration Manager to access client upgrade compatibility data in the Configuration Manager console. Then use this data to create collections, and target devices for upgrade or remediation.



## Configure clients

Upgrade Readiness relies on Windows Analytics data. In order for Upgrade Readiness to receive sufficient data, configure the following prerequisites:

- Configure all clients with a *commercial ID key*  

- Configure Windows 10 clients for Windows Analytics to report at least basic level data  

- For clients running Windows 7 or 8.1:  

    - Install the updates as described in [Get started with Upgrade Readiness](https://docs.microsoft.com/windows/deployment/upgrade/upgrade-readiness-get-started)  

    - Enable Windows Analytics client settings  

Configure these settings using Configuration Manager client settings. For more information, see [Use Windows Analytics](monitor-windows-analytics.md).

> [!NOTE]  
> Deploying the correct prerequisite updates and configuring client settings should be sufficient in most environments. If you encounter issues with Upgrade Readiness not receiving data from devices in your environment, then some of these issues may be addressed by using the [Upgrade Readiness deployment script](https://docs.microsoft.com/windows/deployment/upgrade/upgrade-readiness-deployment-script). 



## Connect Configuration Manager to Upgrade Readiness

Use the [Azure services wizard](../../servers/deploy/configure/azure-services-wizard.md) to simplify the process of configuring Azure services you use with Configuration Manager. To connect Configuration Manager with Upgrade Readiness, create an Azure Active Directory (Azure AD) app registration of type *Web app / API* in the [Azure portal](https://portal.azure.com). For more information about how to create an app registration, see [Register your application with your Azure AD tenant](/azure/active-directory/active-directory-app-registration). 

In the Azure portal, give following permissions to your newly registered web app:
- *Reader* permissions to the resource group that contains the Log Analytics workspace with your Upgrade Readiness data
- *Contributor* permissions to the Log Analytics workspace that hosts your Upgrade Readiness data

The Azure services wizard uses this app registration to allow Configuration Manager to communicate securely with Azure AD and connect your infrastructure to your Upgrade Readiness data.

> [!IMPORTANT]  
> Grant permissions to the app itself, not to an Azure AD user identity. It's the registered app that accesses the data on behalf of your Configuration Manager infrastructure. To grant the permissions, search for the name of the app registration in the **Add users** area when assigning the permission. 
> 
> This process is the same as when providing Configuration Manager with permissions to Log Analytics. These steps must be completed before the app registration is imported into Configuration Manager with the *Azure services wizard*.
> 
> For more information, see [Connect Configuration Manager to Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm).


### Use the Azure Wizard to create the connection

Follow the instructions in [Configure Azure services](../../servers/deploy/configure/azure-services-wizard.md) to create a connection to Upgrade Readiness by importing the web app registration you created above. 

If the web app import was successful and the correct permissions are assigned in the Azure portal, the *Configuration* page pre-populates the following values:   
-  Azure subscriptions  
-  Azure resource group  
-  Windows Analytics workspace  

More than one resource group or workspace is available in the following circumstances: 
- If the registered Azure AD web app has *Contributor* permissions on more than one resource group   
- If the selected resource group has more than one Log Analytics workspace  



## View and use Upgrade Readiness information in Configuration Manager

After you've integrated Upgrade Readiness with Configuration Manager, you can view the analysis of your clients' upgrade readiness.

1. In the Configuration Manager console, go to the **Monitoring** workspace, and select the **Upgrade Readiness** node.  

2. Review the data. For example:  
    - The upgrade readiness state  
    - The percent of Windows devices that are reporting data  

3. Filter the dashboard to view data for devices in specific collections.  

4. View the devices in a particular readiness state, and then create a dynamic collection for those devices. Then use that collection to upgrade those devices, or take action to remediate devices that are in a blocked state.  

> [!Note]  
> The site synchronizes data with Upgrade Readiness once a week. To manually trigger synchronization:
> 1. In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select the **Azure Services** node.  
> 2. Select the Upgrade Readiness connection from the list.  
> 3. In the ribbon, select the option to synchronize.  



## Next steps

- [Upgrade Windows to the latest version](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md)  
- [Create a task sequence to upgrade an OS](../../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md)  
- [Create phased deployments](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md)  
