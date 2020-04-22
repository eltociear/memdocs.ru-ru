---
title: Управление коллекциями
titleSuffix: Configuration Manager
description: Выполнение типичных задач управления в System Center Configuration Manager.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e102fd1a-76df-4d8e-b1b0-10ee18318f67
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2fc8347ae766cbd16075ef4170efa2f8042371f8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695312"
---
# <a name="how-to-manage-collections-in-configuration-manager"></a>Управление коллекциями в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

В этой статье содержатся обзорные сведения о задачах управления для коллекций в Configuration Manager.  

> [!NOTE]  
>  Сведения о создании коллекций Configuration Manager вы найдете в [этой статье](create-collections.md).



## <a name="how-to-manage-device-collections"></a><a name="bkmk_device"></a> Управление коллекциями устройств  

В рабочей области **Активы и соответствие** выберите **Коллекции устройств**, выберите нужную коллекцию, затем выберите задачу управления.  


#### <a name="show-members"></a>Показать участников
Отображение всех ресурсов, которые входят в выбранную коллекцию, во временном узле, включенном в узел **Устройства** .


#### <a name="add-selected-items"></a>Добавить выбранные элементы
Позволяет создавать различные элементы при помощи следующих команд. 

- **Добавление выбранных элементов в существующую коллекцию устройств**. Открытие диалогового окна **Выбор коллекции** . Выберите коллекцию, в которую вы хотите добавить члены выбранной коллекции. Выбранная коллекция включается в эту коллекцию с помощью правила членства **Включить коллекции** .  

- **Добавление выбранных элементов в новую коллекцию устройств**. Открывается **мастер создания коллекций устройств**, где можно создать новую коллекцию. Выбранная коллекция включается в эту коллекцию с помощью правила членства **Включить коллекции** .  


Дополнительные сведения см. в статье [Создание коллекций](create-collections.md).


#### <a name="install-client"></a>Установить клиент
Открывается **мастер установки клиента**. Этот мастер использует принудительную установку клиента, чтобы установить клиент Configuration Manager на всех компьютерах в выбранной коллекции. Дополнительные сведения см. в разделе [Принудительная установка клиента](../../deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).


#### <a name="run-script"></a>Запуск скрипта
Открывается мастер **запуска скрипта**, чтобы выполнить скрипт PowerShell на всех клиентах в коллекции. Дополнительные сведения см. в статье [Создание и запуск скриптов PowerShell из консоли Configuration Manager](../../../../apps/deploy-use/create-deploy-scripts.md).


#### <a name="manage-affinity-requests"></a>Управление запросами на сопоставление
Открывается диалоговое окно **Управление запросами на сопоставление пользователей и устройств**. Утвердите или отклоните ожидающие утверждения запросы на сопоставление пользователей и устройств для устройств в выбранной коллекции. Дополнительные сведения см. в статье [Связывание пользователей и устройств с помощью сопоставления пользователей и устройств в System Center Configuration Manager](../../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).


#### <a name="clear-required-pxe-deployments"></a>Очистить необходимые развертывания PXE
Очистка необходимых развертываний загрузки PXE на всех членах выбранной коллекции. Дополнительные сведения см. в статье [Использование PXE для развертывания Windows по сети](../../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md).


#### <a name="update-membership"></a>Обновить членство
Оценка членства для выбранной коллекции. Для коллекций с большим числом членов обновление данных может занять некоторое время. Чтобы обновить список членов коллекции после завершения обновления данных, используйте действие **Обновить** .


#### <a name="add-resources"></a>Добавить ресурсы
Открывается диалоговое окно **Добавить ресурсы в коллекцию**. Найдите новые ресурсы и добавьте их в выбранную коллекцию. Во время обновления для значка выбранной коллекции отображается символ песочных часов.


#### <a name="client-notification"></a>Уведомление клиента
Дополнительные сведения см. в разделе [Уведомление клиента](../client-notification.md).


#### <a name="endpoint-protection"></a>Endpoint Protection
Дополнительные сведения см. в разделе [Уведомление клиента](../client-notification.md).


#### <a name="export"></a>Экспортировать
Открывается **мастер экспорта коллекции**, который позволяет экспортировать коллекцию в MOF-файл. Этот файл можно архивировать или импортировать на другой сайт Configuration Manager. При экспорте коллекции не экспортируются коллекции, на которую в ней есть ссылки. Ссылки на другие коллекции обозначаются правилами **Включить** или **Исключить**.


#### <a name="copy"></a>Копировать
Создание копии выбранной коллекции. Новая коллекция использует выбранную коллекцию в качестве ограничивающей коллекции.


#### <a name="refresh"></a>Обновление
Обновление представления.


#### <a name="delete"></a>Удалить
Удаление выбранной коллекции. Кроме того, можно удалить все ресурсы в коллекции из базы данных сайта. 

Коллекции, встроенные в Configuration Manager, удалить нельзя. Список встроенных коллекций см. в разделе [Встроенные коллекции](introduction-to-collections.md#built-in-collections).


#### <a name="simulate-deployment"></a>Имитировать развертывание
Запуск **мастера имитации развертывания приложения**. Этот мастер позволяет проверить результаты развертывания приложения, не устанавливая и не удаляя приложение. Дополнительные сведения см. в статье [Имитация развертываний приложений в System Center Configuration Manager](../../../../apps/deploy-use/simulate-application-deployments.md).


#### <a name="deploy"></a>Развернуть
Отображается список, включающий следующие элементы.  

- **Приложение**. Открывается **мастер развертывания программного обеспечения**. Выберите и настройте развертывание приложения в выбранную коллекцию. Дополнительные сведения см. в статье [Развертывание приложений с помощью Configuration Manager](../../../../apps/deploy-use/deploy-applications.md).  

- **Программа**. Открывается **мастер развертывания программного обеспечения**. Выберите и настройте развертывание пакета и программы в выбранную коллекцию. Дополнительные сведения см. в разделе [Пакеты и программы](../../../../apps/deploy-use/packages-and-programs.md).  

- **Шаблон базовой конфигурации**. Открывается диалоговое окно **Развертывание шаблона базовых конфигураций**. Настройте развертывание одной или нескольких конфигурационных баз в выбранной коллекции. Дополнительные сведения см. в разделе [Развертывание конфигурационных баз](../../../../compliance/deploy-use/deploy-configuration-baselines.md).  

- **Последовательность задач**. Открывается **мастер развертывания программного обеспечения**. Выберите и настройте развертывание последовательности задач в выбранную коллекцию. Дополнительные сведения см. в разделе [Управление последовательностями задач для их автоматизации](../../../../osd/deploy-use/deploy-a-task-sequence.md).  

- **Обновления программного обеспечения**. Открывается **мастер развертывания обновлений программного обеспечения**. Настройте развертывание обновлений программного обеспечения для ресурсов в выбранной коллекции. Дополнительные сведения см. в статье об [управлении обновлениями программного обеспечения](../../../../sum/understand/software-updates-introduction.md).  


#### <a name="clear-server-group-deployment-locks"></a>Снятие блокировки развертывания для группы серверов
Вручную снимите все блокировки развертываний для группы серверов в коллекции. Дополнительные сведения см. в статье [Обслуживание группы серверов](../../../../sum/deploy-use/service-a-server-group.md).


#### <a name="move"></a>Переместить
Перемещение выбранной коллекции в другую папку в узле **Коллекции устройств**. 


#### <a name="properties"></a>Элемент Property
Дополнительные сведения см. в разделе [Свойства коллекции](#BKMK_CollProp).  


## <a name="how-to-manage-user-collections"></a><a name="bkmk_user"></a> Управление коллекциями пользователей  

В рабочей области **Активы и соответствие** выберите **Коллекции пользователей**, выберите нужную коллекцию, затем выберите задачу управления.  

> [!Note]  
> Для коллекций пользователей поддерживаются приведенные ниже действия, поведение которых совпадает с поведением для коллекций устройств. Отличие лишь в том, что действия применяются к коллекции пользователей и включенным в нее пользователям. Дополнительные сведения см. в описании соответствующего действия в разделе [Управление коллекциями устройств](#bkmk_device).  

- **Показать участников**  
- **Добавить выбранные элементы**  
    - **Добавление выбранных элементов в существующую коллекцию пользователей**  
    - **Добавление выбранных элементов в новую коллекцию пользователей**  
- **Управление запросами на сопоставление**  
- **Обновить членство**  
- **Добавить ресурсы**  
- **Экспортировать**  
- **Копировать**  
- **Обновление**  
- **Удалить**  
- **Имитировать развертывание**  
- **Развертывание**  
    - **Приложение**  
    - **Программа**  
    - **Шаблон базовой конфигурации**
- **Переместить**  
- **Свойства**


##  <a name="collection-properties"></a><a name="BKMK_CollProp"></a> Свойства коллекции  

В диалоговом окне **Свойства** для выбранной коллекции можно просмотреть и настроить следующие свойства.  

#### <a name="general"></a>Общие
Просмотр и указание общих сведений о выбранной коллекции, включая имя коллекции и ограничивающую коллекцию.

#### <a name="membership-rules"></a>Правила членства в коллекции
Настройка правил членства в коллекции, которые определяют состав коллекции. Дополнительные сведения см. в статье [Создание коллекций](create-collections.md).  

#### <a name="power-management"></a>Управление питанием
Настройка схем управления питанием, назначаемых компьютерам в выбранной коллекции. Дополнительные сведения см. в статье [Общие сведения об управлении питанием](../power/introduction-to-power-management.md).  

#### <a name="deployments"></a>развертывания,
Отображение списка программ, развернутых на устройствах-членах выбранной коллекции.  

#### <a name="maintenance-windows"></a>Периоды обслуживания
Просмотр и настройка периодов обслуживания, применяемых к членам выбранной коллекции. Дополнительные сведения см. в разделе [Использование периодов обслуживания](use-maintenance-windows.md).

#### <a name="collection-variables"></a>Переменные коллекции
Настройка переменных, которые будут применяться к этой коллекции и использоваться последовательностями задач. Дополнительные сведения см. в разделе [How to set variables](../../../../osd/understand/using-task-sequence-variables.md#bkmk_set) (Как задать переменные).  

#### <a name="distribution-point-groups"></a>Группы точек распространения
Привязка одной или нескольких групп точек распространения к членам выбранной коллекции. Дополнительные сведения см. в разделе [Управление содержимым и инфраструктурой содержимого](../../../servers/deploy/configure/manage-content-and-content-infrastructure.md).

#### <a name="aad-group-sync"></a>Синхронизация группы AAD
Синхронизация результатов членства в коллекции с группами Azure Active Directory Эта синхронизация является [функцией предварительной версии](../../../servers/manage/pre-release-features.md), начиная с версии 1906. Дополнительные сведения см. в статье [Создание коллекций](create-collections.md#bkmk_aadcollsync).

#### <a name="security"></a>Безопасность
Отображение пользователей, которым назначены разрешения для выбранной коллекции в рамках связанных ролей и областей безопасности. Дополнительные сведения см. в разделе [Основы ролевого администрирования](../../../understand/fundamentals-of-role-based-administration.md).  

#### <a name="alerts"></a>Предупреждения 
Настройка условий создания оповещений для функции статуса клиента и Endpoint Protection. Дополнительные сведения см. в статьях [Настройка состояния клиента в System Center Configuration Manager](../../deploy/configure-client-status.md) и [Мониторинг состояния Endpoint Protection](../../../../protect/deploy-use/monitor-endpoint-protection.md).  
## <a name="using-powershell"></a><a name="bkmk_powershell"></a> Использование PowerShell

PowerShell можно использовать для управления коллекциями.  Дополнительные сведения см. на странице

* [Get-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollection)
* [Set-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmcollection)
* [New-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmcollection)
* [Copy-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/copy-cmcollection)
* [Remove-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollection)
* [Import-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/import-cmcollection)
* [Export-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/export-cmcollection)
* [Get-CMCollectionMember](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectionmember)
* [Get-CMCollectionSetting](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectionsetting)
* [Invoke-CMCollectionUpdate](https://docs.microsoft.com/powershell/module/configurationmanager/invoke-cmcollectionupdate)
* [Add-CMCollectionMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/add-cmcollectionmembershiprule)
* [Set-CMCollectionPowerManagement](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmcollectionpowermanagement)
* [Get-CMCollectionMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectionmembershiprule)
* [Remove-CMCollectionMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollectionmembershiprule)
* [Get-CMCollectionDirectMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectiondirectmembershiprule)
* [Get-CMCollectionQueryMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectionquerymembershiprule)
* [Get-CMCollectionIncludeMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectionincludemembershiprule)
* [Add-CMCollectionToAdministrativeUser](https://docs.microsoft.com/powershell/module/configurationmanager/add-cmcollectiontoadministrativeuser)
* [Remove-CMCollectionQueryMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollectionquerymembershiprule)
* [Remove-CMCollectionDirectMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollectiondirectmembershiprule)
* [Get-CMCollectionExcludeMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectionexcludemembershiprule)
* [Add-CMCollectionToDistributionPointGroup](https://docs.microsoft.com/powershell/module/configurationmanager/add-cmcollectiontodistributionpointgroup)
* [Remove-CMCollectionIncludeMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollectionincludemembershiprule)
* [Remove-CMCollectionExcludeMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollectionexcludemembershiprule)
* [Remove-CMCollectionFromAdministrativeUser](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollectionfromadministrativeuser)
