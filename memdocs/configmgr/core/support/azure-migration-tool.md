---
title: Расширение и миграция локального сайта в Microsoft Azure
titleSuffix: Configuration Manager
description: Сведения об использовании средства миграции, чтобы программно создавать виртуальные машины Azure для Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1c975c5e-efd1-4d47-a315-39ccb32633dc
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 00f07e20c24ea9bb7d06b18f300e0206696c5e20
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707942"
---
# <a name="extend-and-migrate-on-premises-site-to-microsoft-azure"></a>Расширение и миграция локального сайта в Microsoft Azure

*Область применения: Configuration Manager (Current Branch)*


Это средство, появившееся в версии 1910, позволяет программно создавать виртуальные машины Azure для Configuration Manager. <!--3556022--> Оно может выполнять установку с использованием параметров по умолчанию роли сайта, таких как пассивный сервер сайта, точки управления и точки распространения. После проверки новых ролей используйте их в качестве дополнительных систем сайта для обеспечения высокой доступности. Вы также можете удалить локальную роль системы сайта и оставить только роль виртуальной машины Azure.

## <a name="prerequisites"></a>Предварительные условия

- Подписка Azure.

- Виртуальная сеть Azure со шлюзом ExpressRoute.

<!-- - A standalone primary site. A hierarchy with a central administration site isn't currently supported. can comment this out because TP only supports a standalone primary!-->

- Учетная запись пользователя должна иметь роль полного администратора **Configuration Manager** и права администратора на сервере первичного сайта.

- Чтобы добавить пассивный сервер, первичный сайт должен соответствовать требованиям к высокой доступности для [сервера сайта](../servers/deploy/configure/site-server-high-availability.md#prerequisites). Например, требуется использование [удаленной библиотеки содержимого](../plan-design/hierarchy/the-content-library.md#bkmk_remote).

### <a name="required-azure-permissions"></a>Требуемые разрешения Azure

Для запуска средства вам потребуются следующие разрешения в Azure:
<!--5789222-->
Microsoft.Resources/subscriptions/resourceGroups/read <br>
Microsoft.Resources/subscriptions/resourceGroups/write <br>
Microsoft.Resources/deployments/read <br>
Microsoft.Resources/deployments/write <br>
Microsoft.Resources/deployments/validate/action <br>
Microsoft.Compute/virtualMachines/extensions/read <br>
Microsoft.Compute/virtualMachines/extensions/write <br>
Microsoft.Compute/virtualMachines/read <br>
Microsoft.Compute/virtualMachines/write <br>
Microsoft.Network/virtualNetworks/read <br>
Microsoft.Network/virtualNetworks/subnets/read <br>
Microsoft.Network/virtualNetworks/subnets/join/action <br>
Microsoft.Network/networkInterfaces/read <br>
Microsoft.Network/networkInterfaces/write <br>
Microsoft.Network/networkInterfaces/join/action <br>
Microsoft.Network/networkSecurityGroups/write <br>
Microsoft.Network/networkSecurityGroups/read <br>
Microsoft.Network/networkSecurityGroups/join/action <br>
Microsoft.Storage/storageAccounts/write <br>
Microsoft.Storage/storageAccounts/read <br>
Microsoft.Storage/storageAccounts/listkeys/action <br>
Microsoft.Storage/storageAccounts/listServiceSas/action <br>
Microsoft.Storage/storageAccounts/blobServices/containers/write <br>
Microsoft.Storage/storageAccounts/blobServices/containers/read <br>
Microsoft.KeyVault/vaults/deploy/action <br>
Microsoft.KeyVault/vaults/read <br>


Дополнительные сведения о разрешениях и назначении ролей см. в статье [Управление доступом к ресурсам Azure с помощью RBAC](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal).

## <a name="run-the-tool"></a>Запуск программы

1. Войдите на сервер первичного сайта и запустите следующее средство в каталоге установки Configuration Manager: `Cd.Latest\SMSSETUP\TOOLS\ExtendMigrateToAzure\ExtendMigrateToAzure.exe`

1. Просмотрите сведения на вкладке **Общие**, а затем перейдите на вкладку **Azure Information**.

1. На вкладке **Azure Information** выберите **среду Azure**, а затем **выполните вход**.

    > [!TIP]
    > Чтобы правильно выполнить вход, может потребоваться добавить `https://*.microsoft.com` в список надежных веб-сайтов.

    [ ![Вкладка сведений Azure в средстве расширения и миграции](./media/3556022-azure-information-tab.png)](./media/3556022-azure-information-tab.png#lightbox)

1. После входа выберите свой **идентификатор подписки** и **виртуальную сеть**. Средство отображает только сети со шлюзом ExpressRoute.

## <a name="site-server-high-availability"></a>Высокая доступность сервера сайта

1. На вкладке **Высокая доступность сервера сайта** выберите **Проверить**, чтобы оценить готовность сайта.

    Если какая-либо из проверок не пройдена, выберите **More detail** (Подробности), чтобы определить, как устранить проблему. Дополнительные сведения о предварительных сведениях см. в [этом разделе](../servers/deploy/configure/site-server-high-availability.md#prerequisites).

2. Если вы хотите расширить или перенести сервер сайта в Azure, щелкните **Create a site server in Azure** (Создать сервер сайта в Azure). Затем заполните следующие поля:

    |Имя|Описание:|
    |---|---|
    |**Подписка**|Только чтение. Отображает имя и идентификатор подписки.|
    |**Группа ресурсов**| Выводит список доступных групп ресурсов. Если необходимо создать группу ресурсов, используйте [портал Azure](https://portal.azure.com), а затем запустите это средство повторно.|
    |**Расположение**| Только чтение. Определяется расположением виртуальной сети|
    |**Размер виртуальной машины**|Выберите размер в соответствии с рабочей нагрузкой. Корпорация Майкрософт рекомендует **Standard_DS3_v2**.|
    |**Операционная система**|Только чтение. Средство использует Windows Server 2019.|
    |**Тип диска**|Только чтение. Для лучшей производительности средство использует SSD (цен. категория "Премиум").|
    |**Виртуальная сеть**|Только чтение.|
    |**Подсеть**|Выберите подсеть для использования. Если необходимо создать подсеть, используйте [портал Azure](https://portal.azure.com).|
    |**Имя компьютера**|Введите имя виртуальной машины пассивного сервера сайта в Azure. Это то же имя, которое отображается на [портале Azure](https://portal.azure.com).|
    |**Local admin username** (Имя пользователя локального администратора)|Введите имя локального пользователя с правами администратора, созданное виртуальной машиной Azure перед присоединением к домену.|
    |**Local admin password** (Пароль локального администратора)|Пароль локального пользователя с правами администратора. Чтобы защитить пароль во время развертывания Azure, сохраните его в качестве секрета в [Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-overview). Затем используйте ссылку. При необходимости создайте пароль на [портале Azure](https://portal.azure.com).|
    |**Domain FQDN** (Полное доменное имя)|Полное доменное имя для присоединяемого домена Active Directory. По умолчанию средство получает это значение от текущего компьютера.|
    |**Имя пользователя домена**|Имя пользователя домена, которому разрешено присоединиться к домену. По умолчанию средство использует имя пользователя, выполнившего вход.|
    |**Пароль домена**|Пароль пользователя домена, которому разрешено присоединиться к домену. Средство проверяет его после нажатия кнопки **Запуск**. Чтобы защитить пароль во время развертывания Azure, сохраните его в качестве секрета в [Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-overview). Затем используйте ссылку. При необходимости создайте пароль на [портале Azure](https://portal.azure.com).|
    |**Domain DNS IP** (IP-адрес DNS домена)|Используется для присоединения к домену. По умолчанию средство использует DNS от текущего компьютера.|
    |**Тип**|Только чтение. В нем отображается тип *Пассивный сервер сайта*.|

    > [!IMPORTANT]
    > По умолчанию для виртуальных машин пункт **Использовать существующую лицензию Windows Server** настроен на значение **Нет**. Если вы хотите использовать локальные лицензии Windows Server с подпиской Software Assurance, настройте этот параметр на [портале Azure](https://portal.azure.com) после подготовки виртуальных машин. Дополнительные сведения см. в статье [Преимущество гибридного использования Azure для Windows Server](https://docs.microsoft.com/windows-server/get-started/azure-hybrid-benefit).

1. Чтобы начать подготовку виртуальной машины Azure, нажмите кнопку **Запуск**. Чтобы отслеживать состояние развертывания, перейдите на вкладку **Deployments in Azure** (Развертывания в Azure). Чтобы получить последнее состояние, щелкните **Refresh deployment status** (Обновить состояние развертывания).

    > [!TIP]
    > Для проверки состояния, поиска ошибок и определения возможных исправлений можно также использовать [портал Azure](https://portal.azure.com).

1. После завершения развертывания перейдите к серверам SQL и предоставьте разрешения для новой виртуальной машины Azure. Дополнительные сведения о предварительных требованиях для высокой доступности сервера сайта см. в [этой статье](../servers/deploy/configure/site-server-high-availability.md#prerequisites).

1. Чтобы добавить виртуальную машину Azure в качестве сервера сайта в пассивном режиме, выберите **Add site server in passive mode** (Добавить сервер сайта в пассивном режиме).

1. Когда на сайте будет добавлен сервер сайта в пассивном режиме, на вкладке **Высокая доступность сервера сайта** появится состояние.

   [![Пассивный сервер сайта добавлен на вкладку "Высокая доступность сервера сайта"](./media/3556022-site-server-passive-mode.png)](./media/3556022-site-server-passive-mode.png#lightbox)

1. Затем перейдите на вкладку [Deployments in Azure](#bkmk_deploy-azure) (Развертывания в Azure), чтобы завершить развертывание.

## <a name="site-database"></a>База данных сайта

В настоящее время у этого средства нет задач для миграции базы данных из локальной среды в Azure. Вы можете переместить базу данных с локального сервера SQL Server на виртуальную машину Azure SQL Server. Это средство содержит следующие статьи на вкладке **База данных сайта**, которые помогут выполнить следующие действия:

- [Архивация сайта Configuration Manager](../servers/manage/backup-and-recovery.md)
- [Изменения, относящиеся к резервному копированию сайта](../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md#changes-for-site-backup)
- [Migrate a SQL Server database to SQL Server in an Azure VM](/azure/virtual-machines/windows/sql/virtual-machines-windows-migrate-sql) (Перенос базы данных SQL Server на SQL Server на виртуальной машине Azure)

## <a name="site-system-roles"></a>Роли систем сайта

1. Перейдите на вкладку **Системные роли сайта**. Чтобы назначить новую роль системы сайта с параметрами по умолчанию, нажмите кнопку **Создать**. Сейчас поддерживаются роли точки управления, точки распространения и точки обновления программного обеспечения. В настоящее время в средстве доступны не все роли.

    [![Вкладка "Системные роли сайта" в средстве расширения и миграции](./media/3556022-site-system-roles-tab.png)](./media/3556022-site-system-roles-tab.png#lightbox)

1. В окне подготовки заполните поля, чтобы подготовить виртуальную машину роли сайта в Azure. Эти сведения похожи на приведенный выше список для сервера сайта.

1. Чтобы начать подготовку виртуальной машины Azure, нажмите кнопку **Запуск**. Чтобы отслеживать состояние развертывания, перейдите на вкладку **Deployments in Azure** (Развертывания в Azure). Чтобы получить последнее состояние, щелкните **Refresh deployment status** (Обновить состояние развертывания).

    > [!TIP]
    > Для проверки состояния, поиска ошибок и определения возможных исправлений можно также использовать [портал Azure](https://portal.azure.com).

1. Повторите эту процедуру для добавления других ролей системы сайта.

1. Затем перейдите на вкладку [Deployments in Azure](#bkmk_deploy-azure) (Развертывания в Azure), чтобы завершить развертывание.

1. После завершения развертывания перейдите в консоль Configuration Manager, чтобы внести дополнительные изменения в роль сайта.

## <a name="deployments-in-azure"></a><a name="bkmk_deploy-azure"></a> Развертывания в Azure

1. Когда Azure создаст виртуальную машину, перейдите на вкладку **Deployments in Azure** (Развертывания в Azure) в средстве. Щелкните **Развернуть**, чтобы настроить роль с параметрами по умолчанию.

1. Нажмите кнопку **Запустить**, чтобы запустить скрипт PowerShell.

    [![Развертывание ролей сайта с помощью выполнения созданного сценария PowerShell](./media/3556022-run-powershell-script-deployment.png)](./media/3556022-run-powershell-script-deployment.png#lightbox)

1. Повторите эти действия для настройки других ролей.

## <a name="add-site-roles-to-an-existing-virtual-machine-deployment"></a><a name="bkmk_add_role"></a> Добавление ролей сайта в существующее развертывание виртуальной машины
<!--5665775, 6307931-->
Начиная с Configuration Manager версии 2002, инструмент расширения и миграции локального сайта в Microsoft Azure поддерживает подготовку нескольких ролей системы сайта на одной виртуальной машине Azure. Вы можете добавить роли системы сайта после завершения первоначального развертывания виртуальной машины Azure. Чтобы добавить новую роль в существующую виртуальную машину, выполните следующие действия:
1. На вкладке **Развертывания в Azure** щелкните развертывание виртуальной машины с состоянием **Выполнено**.
1. Нажмите кнопку **Создать**, чтобы добавить дополнительную роль в виртуальную машину.


## <a name="next-steps"></a>Дальнейшие шаги

Просмотр изменений на [портале Azure](https://portal.azure.com)
