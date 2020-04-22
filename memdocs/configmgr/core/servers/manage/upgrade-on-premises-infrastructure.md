---
title: Обновление локальной инфраструктуры
titleSuffix: Configuration Manager
description: Узнайте, как обновить инфраструктуру, например SQL Server и ОС для систем сайта.
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8ca970dd-e71c-404f-9435-d36e773a0db2
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 033c5de1a85ce2fa8b11fe7a187fcc4d5c023931
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704302"
---
# <a name="upgrade-on-premises-infrastructure-that-supports-configuration-manager"></a>Обновление локальной инфраструктуры для Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Используйте приведенные в этой статье сведения, чтобы обновить инфраструктуру, работающую на базе Configuration Manager.  

- Если вы хотите *обновить* предыдущую версию до текущей ветви Configuration Manager, см. [Обновление до Configuration Manager](../deploy/install/upgrade-to-configuration-manager.md).  

- Если вы хотите *обновить* свою инфраструктуру текущей ветви Configuration Manager до новой версии, см. [Обновления для Configuration Manager](updates.md).  


## <a name="upgrade-the-os-of-site-systems"></a><a name="BKMK_SupConfigUpgradeSiteSrv"></a> Обновление ОС для систем сайта  

Configuration Manager поддерживает обновление на месте для серверных ОС, размещающих сервер сайта и любую роль системы сайта, в следующих ситуациях:  

- Если конечная версия пакета обновления Windows все еще поддерживается Configuration Manager, будет также поддерживаться обновление на месте до более поздней версии пакета обновления Windows Server.  

- Обновление на месте:  

    - Windows Server 2016 до Windows Server 2019  

    - Windows Server 2012 R2 до Windows Server 2019  

    - Windows Server 2012 R2 до Windows Server 2016  

    - Windows Server 2012 до Windows Server 2016  

    - Windows Server 2012 до Windows Server 2012 R2  

    - Windows Server 2008 R2 до Windows Server 2012 R2  

При обновлении сервера используйте процедуры обновления для соответствующей ОС. Дополнительные сведения см. в следующих статьях:  

- [Центр обновления Windows Server](https://aka.ms/upgradecenter)  

- [Варианты обновления и преобразования для Windows Server 2016](https://docs.microsoft.com/windows-server/get-started/supported-upgrade-paths)  

- [Варианты обновления для Windows Server 2012 R2](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn303416(v=ws.11))  

### <a name="upgrade-to-windows-server-2016-or-2019"></a><a name="bkmk_2016-2019"></a> Обновление до Windows Server 2016 или 2019

Выполните указания этого раздела в следующих сценариях обновления:  

- Обновление Windows Server 2012 R2 или Windows Server 2016 до Windows Server 2019  

- Обновление Windows Server 2012 или Windows Server 2012 R2 до Windows Server 2016  

#### <a name="before-upgrade"></a>Действия перед обновлением

- (Windows Server 2012 или Windows Server 2012 R2): Удалите клиент System Center Endpoint Protection (SCEP). В Windows Server теперь встроен Защитник Windows, который заменяет клиент SCEP. Наличие клиента SCEP может помешать обновлению Windows Server.  

- Если на сервере установлена роль Windows Server Update Services (WSUS), удалите ее. Вы можете сохранить базу данных SUSDB и повторно подключить ее после переустановки служб WSUS.  

- Если вы обновляете ОС сервера сайта, убедитесь, что [репликация на основе файлов](../../plan-design/hierarchy/file-based-replication.md) является для сайта работоспособной. Проверьте все почтовые ящики на наличие невыполненных работ как на отправляющем сайте, так и на получающем. При наличии большого количества задержанных или ожидающих заданий репликации, дождитесь их завершения.<!-- SCCMDocs#1792 -->
    - На отправляющем сайте проверьте **sender.log**.
    - На принимающем сайте проверьте **despooler.log**.

#### <a name="after-upgrade"></a>Действия после обновления

- Защитник Windows должен работать и быть настроенным на автоматический запуск.  

- Проверьте, что запущены следующие службы Configuration Manager:  

    - SMS_EXECUTIVE  

    - SMS_SITE_COMPONENT_MANAGER  

- **Служба активации Windows** и службы **WWW/W3svc** должны быть включены и настроены на автоматический запуск. Процесс обновления отключает эти службы, поэтому проверьте, что они запущены для следующих ролей системы сайта:  

    - Сервер сайтов  

    - Точка управления  

    - Тточка веб-службы каталога приложений  

    - Точка веб-сайта каталога приложений  

- Обеспечьте соответствие всех серверов с ролью системы сайта всем необходимым [требованиям](../../plan-design/configs/site-and-site-system-prerequisites.md). Например, может потребоваться переустановить BITS, WSUS или настроить некоторые параметры служб IIS.  

- Обеспечив соответствие требованиям, вновь перезагрузите сервер и проверьте работу служб.  

- При обновлении сервера первичного сайта необходимо [выполнить сброс сайта](modify-your-infrastructure.md#bkmk_reset).  

#### <a name="known-issue-for-remote-configuration-manager-consoles"></a>Известные проблемы с удаленными консолями Configuration Manager

После обновления сервера сайта или экземпляра поставщика SMS вы не сможете подключаться с помощью консоли Configuration Manager. В качестве обходного решения восстановите разрешения для группы **Администраторы SMS** в WMI вручную. Разрешения должны быть заданы на сервере сайта и на каждом удаленном сайте, на котором размещается экземпляр поставщика SMS.

1. На соответствующих серверах откройте консоль управления (MMC), добавьте оснастку **Управляющий элемент WMI** и выберите **Локальный компьютер**.  

2. В консоли управления (MMC) откройте окно **Свойства** оснастки **Элемент управления WMI (локальный)** и перейдите на вкладку **Безопасность**.  

3. Разверните дерево под элементом "Корень", выберите узел **SMS**, а затем щелкните **Безопасность**.  У группы **Администраторы SMS** должны быть следующие разрешения:  

    - Включить учетную запись  

    - Включить удаленно  

4. На вкладке **Безопасность** под узлом **SMS** выберите узел **site_&lt;код сайта**> узел, а затем — **Безопасность**. У группы **Администраторы SMS** должны быть следующие разрешения:  

    - Выполнение методов  

    - Запись поставщика  

    - Включить учетную запись  

    - Включить удаленно  

5. Сохраните разрешения, чтобы восстановить доступ к консоли Configuration Manager.  

#### <a name="known-issue-for-remote-site-systems"></a>Известная проблема для удаленных систем сайтов

После обновления сервера, на котором размещена роль системы сайта, значение `Software\Microsoft\SMS` может отсутствовать в следующем разделе реестра: `HKLM\SYSTEM\CurrentControlSet\Control\SecurePipeServers\Winreg\AllowedPaths`

Если это значение отсутствует после обновления Windows на сервере, добавьте его вручную. В противном случае отправка ролями системы сайта файлов во входящие папки сервера сайта может завершиться сбоем.

### <a name="upgrade-to-windows-server-2012-r2"></a><a name="bkmk_2012r2"></a> Обновление до Windows Server 2012 R2

При обновлении Windows Server 2008 R2 или Windows Server 2012 до Windows Server 2012 R2 необходимо сделать следующее.

#### <a name="before-upgrade"></a>Действия перед обновлением

- Windows Server 2012: Если на сервере установлена роль Windows Server Update Services (WSUS), удалите ее. Вы можете сохранить базу данных SUSDB и повторно подключить ее после переустановки служб WSUS.  

- Windows Server 2008 R2: Перед обновлением до Windows Server 2012 R2 необходимо удалить службы WSUS 3.2 с сервера. Вы можете сохранить базу данных SUSDB и повторно подключить ее после переустановки служб WSUS. См. дополнительные сведения о [службах Windows Server Update Services](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh852345(v=ws.11)#new-and-changed-functionality).  

- Если вы обновляете ОС сервера сайта, убедитесь, что [репликация на основе файлов](../../plan-design/hierarchy/file-based-replication.md) является для сайта работоспособной. Проверьте все почтовые ящики на наличие невыполненных работ как на отправляющем сайте, так и на получающем. При наличии большого количества задержанных или ожидающих заданий репликации, дождитесь их завершения.<!-- SCCMDocs#1792 -->
    - На отправляющем сайте проверьте **sender.log**.
    - На принимающем сайте проверьте **despooler.log**.

#### <a name="after-upgrade"></a>Действия после обновления

- Процесс обновления отключает службы развертывания Windows. Проверьте, что эта служба запущена для следующих ролей системы сайта:  

    - Сервер сайтов  

    - Точка управления  

    - Тточка веб-службы каталога приложений  

    - Точка веб-сайта каталога приложений  

- **Служба активации Windows** и службы **WWW/W3svc** должны быть включены и настроены на автоматический запуск. Процесс обновления отключает эти службы, поэтому проверьте, что они запущены для следующих ролей системы сайта:  

    - Сервер сайтов  

    - Точка управления  

    - Тточка веб-службы каталога приложений  

    - Точка веб-сайта каталога приложений  

- Обеспечьте соответствие всех серверов с ролью системы сайта всем необходимым [требованиям](../../plan-design/configs/site-and-site-system-prerequisites.md). Например, может потребоваться переустановить BITS, WSUS или настроить некоторые параметры служб IIS.  

    Обеспечив соответствие требованиям, вновь перезагрузите сервер и проверьте работу служб.  

### <a name="unsupported-upgrade-scenarios"></a>Неподдерживаемые сценарии обновления

Следующие варианты обновления Windows Server часто запрашиваются, но не поддерживаются в Configuration Manager:  

- Windows Server 2008 до Windows Server 2012 или более поздней версии;  

- Windows Server 2008 R2 до Windows Server 2012.  


## <a name="upgrade-the-os-of-clients"></a><a name="BKMK_SupConfigUpgradeClient"></a> Обновление ОС клиентов  

Configuration Manager поддерживает обновление ОС клиентов Configuration Manager на месте в следующих ситуациях.  

- Если конечная версия пакета обновления поддерживается Configuration Manager, будет также поддерживаться обновление на месте до более поздней версии пакета обновления Windows.  

- Обновление на месте Windows из поддерживаемой версии Windows 10. Дополнительные сведения см. в статье [Обновление Windows до последней версии](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md).  

- Технические обновления между выпуском сборок Windows 10. Дополнительные сведения см. в разделе [Управление Windows как службой](../../../osd/deploy-use/manage-windows-as-a-service.md).  


## <a name="upgrade-sql-server"></a><a name="BKMK_SupConfigUpgradeDBSrv"></a> Обновление SQL Server  

Configuration Manager поддерживает обновление на месте для SQL Server на сервере базы данных сайта.

См. дополнительные сведения: [Поддержка версий SQL Server](../../plan-design/configs/support-for-sql-server-versions.md) в Configuration Manager.  

### <a name="upgrade-the-service-pack-version-of-sql-server"></a>Обновление версии пакета обновления для SQL Server

Если конечная версия пакета обновления SQL Server все еще поддерживается Configuration Manager, будет также поддерживаться обновление на месте до более поздней версии пакета обновления для SQL Server.

Если в вашей иерархии несколько сайтов Configuration Manager, разные сайты могут использовать разные версии пакетов обновления SQL Server. Порядок обновления версий пакетов обновления SQL Server для разных сайтов может быть любым.

### <a name="upgrade-to-a-new-version-of-sql-server"></a>Обновление до новой версии SQL Server

Configuration Manager поддерживает обновление SQL Server на месте до следующих версий:

- SQL Server 2017  

- SQL Server 2016  

- SQL Server 2014  

Сюда входит обновление SQL Server Express до более новой версии на вторичных сайтах.

При обновлении версии SQL Server, где размещена база данных сайта, необходимо обновлять используемые на сайтах версии SQL Server в следующем порядке.

1. Сначала обновите SQL Server на сайте центра администрирования.  

2. Обновите вторичные сайты, прежде чем обновлять их родительский первичный сайт.  

3. И наконец, обновите родительские первичные сайты. Сюда входят оба дочерних первичных сайта, отправляющих отчеты на сайт центра администрирования, и автономные первичные сайты, являющиеся сайтом верхнего уровня в иерархии.  

### <a name="sql-server-cardinality-estimation-level"></a>Уровень оценки кратности SQL Server

При обновлении базы данных сайта с более ранней версии SQL Server она сохраняет текущий уровень оценки кратности SQL, если он не ниже минимального допустимого уровня для данного экземпляра SQL Server. Если уровень совместимости обновляемой базы данных SQL Server ниже допустимого, для базы данных задается минимальный допустимый уровень совместимости для SQL Server.

В таблице ниже приведены рекомендуемые уровни совместимости для баз данных сайтов Configuration Manager.

|Версия SQL Server | Поддерживаемые уровни совместимости | Рекомендуемый уровень |
|----------------|--------------------|--------|
| SQL Server 2017 | 140, 130, 120, 110  | 140 |
| SQL Server 2016 | 130, 120, 110  | 130 |
| SQL Server 2014 | 120, 110      | 110 |

Чтобы определить уровень совместимости оценки кратности SQL Server для вашей базы данных сайта, выполните на сервере базы данных сайта следующий SQL-запрос:  

```SQL
SELECT name, compatibility_level FROM sys.databases
```

Дополнительные сведения об уровнях совместимости оценки кратности SQL и их задании см. в статье [Уровень совместимости инструкции ALTER DATABASE (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level?view=sql-server-2017).

Дополнительные сведения об обновлении SQL Server см. в следующих статьях:  

- [Обновление до SQL Server 2017](https://docs.microsoft.com/sql/database-engine/install-windows/supported-version-and-edition-upgrades-2017)  

- [Обновление до SQL Server 2016](https://docs.microsoft.com/sql/database-engine/install-windows/supported-version-and-edition-upgrades?view=sql-server-2016)  

- [Обновление до SQL Server 2014](https://docs.microsoft.com/sql/database-engine/install-windows/supported-version-and-edition-upgrades?view=sql-server-2014)  

### <a name="to-upgrade-sql-server-on-the-site-database-server"></a>Порядок обновления SQL Server на сервере базы данных сайта  

1. Остановите все службы Configuration Manager на сайте.  

2. Обновите SQL Server до поддерживаемой версии.  

3. Перезапустите службы Configuration Manager.  

> [!NOTE]  
> При изменении выпуска SQL Server, используемого на сайте центра администрирования, с версии Standard на выпуск Datacenter или Enterprise секционирование баз данных не меняется. Оно ограничивает число клиентов, поддерживаемых иерархией.  
