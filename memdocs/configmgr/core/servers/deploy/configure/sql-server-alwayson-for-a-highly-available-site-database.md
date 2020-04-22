---
title: SQL Server AlwaysOn
titleSuffix: Configuration Manager
description: Планирование использования групп доступности SQL Server AlwaysOn для Configuration Manager
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 58d52fdc-bd18-494d-9f3b-ccfc13ea3d35
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b9e2e4e85d9fb6a1ab34af8760e0ac61d6e4fab4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700892"
---
# <a name="prepare-to-use-sql-server-always-on-availability-groups-with-configuration-manager"></a>Подготовка к использованию групп доступности SQL Server AlwaysOn для Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Эта статья поможет вам подготовить Configuration Manager к использованию групп доступности SQL Server AlwaysOn. Эта функция предоставляет для базы данных сайта решение высокого уровня доступности и аварийного восстановления.  

Configuration Manager поддерживает использование групп доступности:

- для первичных сайтов и сайтов центра администрирования;
- в локальной среде или в Microsoft Azure.

В среде Microsoft Azure вы можете повысить уровень доступности базы данных сайта, используя *группы доступности Azure*. Дополнительные сведения о группах доступности Azure см. в статье [Управление доступностью виртуальных машин](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-manage-availability/).

> [!Important]
> Прежде чем продолжить, изучите инструкции по настройке SQL Server и групп доступности SQL Server. В этом руководстве предполагается, что вы знакомы с библиотекой документации и процедурами SQL Server.


## <a name="supported-scenarios"></a>Поддерживаемые сценарии

Ниже описаны поддерживаемые сценарии использования групп доступности с Configuration Manager. Дополнительные сведения и процедуры см. в статье о [настройке групп доступности для Configuration Manager](configure-aoag.md).

- [Создание группы доступности для использования с Configuration Manager](configure-aoag.md#bkmk_create).  
- [Настройка сайта для использования группы доступности](configure-aoag.md#bkmk_configure)  
- [Добавление членов синхронной реплики в группу доступности с размещенной базой данных сайта или их удаление из группы](configure-aoag.md#bkmk_sync).  
- [Настройка и восстановление сайта из реплик асинхронной фиксации](configure-aoag.md#bkmk_async)  
- [Перемещение базы данных сайта из группы доступности в именованный экземпляр или экземпляр изолированного сервера SQL Server по умолчанию](configure-aoag.md#bkmk_stop).  


## <a name="prerequisites"></a>Предварительные условия

На все сценарии распространяются указанные ниже требования. Если к определенному сценарию применимы дополнительные условия, они подробно описаны вместе со сценарием.

### <a name="configuration-manager-accounts-and-permissions"></a>Учетные записи и разрешения Configuration Manager

#### <a name="installation-account"></a>Учетная запись для установки

Учетная запись, используемая для запуска установки Configuration Manager, должна быть:

- членом локальной группы **Администраторы** на каждом компьютере из группы доступности;
- **системного администратора** для каждого экземпляра SQL Server с базой данных сайта.

#### <a name="site-server-to-replica-member-access"></a>Доступ сервера сайта к членам реплики

Учетная запись компьютера сервера сайта должна входить в группу локальных **Администраторов** на каждом компьютере, входящем в группу доступности.

### <a name="sql-server"></a>SQL Server

#### <a name="version"></a>Версия

Каждая реплика в группе доступности должна запускать версию SQL Server, поддерживаемую используемой версией Configuration Manager. На разных узлах группы доступности могут работать разные версии SQL Server, если такая возможность поддерживается SQL Server. Дополнительные сведения см. в статье [Поддерживаемые версии SQL Server в Configuration Manager](../../../plan-design/configs/support-for-sql-server-versions.md).<!--SCCMDocs issue 656-->

#### <a name="edition"></a>выпуск

Используйте выпуск *Enterprise* платформы SQL Server.

#### <a name="account"></a>Учетная запись

Каждый экземпляр SQL Server может работать под учетной записью пользователя домена (**учетной записью службы**) или под учетной записью, не входящей в домен. Все реплики в группе могут иметь разную конфигурацию.

- Используйте учетную запись с минимально необходимым уровнем разрешений. Дополнительные сведения см. в статье [Вопросы безопасности при установке SQL Server](https://docs.microsoft.com/sql/sql-server/install/security-considerations-for-a-sql-server-installation).  

- Для SQL Server опубликовано подробное руководство по [настройке учетных записей службы Windows и разрешений](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-windows-service-accounts-and-permissions).  

- Чтобы использовать учетную запись, не входящую в домен, необходимо применить сертификаты. Дополнительные сведения см. в статье [Использование сертификатов для конечной точки зеркального отображения базы данных (Transact-SQL)](https://docs.microsoft.com/sql/database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql).  

- Дополнительные сведения см. в разделе [Создание конечной точки зеркального отображения базы данных для групп доступности Always On](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/database-mirroring-always-on-availability-groups-powershell).  


### <a name="database"></a>База данных

#### <a name="configure-the-database-on-a-new-replica"></a>Настройка базы данных на новой реплике

Настройте для базы данных на каждой реплике следующие параметры:  

- Включите **интеграцию со средой CLR**:

    ``` SQL
    sp_configure 'show advanced options', 1;  
    GO  
    RECONFIGURE;  
    GO  
    sp_configure 'clr enabled', 1;  
    GO  
    RECONFIGURE;  
    GO
    ```

    Дополнительные сведения см. в разделе [Интеграция с CLR](https://docs.microsoft.com/sql/relational-databases/clr-integration/clr-integration-enabling).  

- Задайте для параметра **Max text repl size** (Максимальный размер текста ответа) значение `2147483647`:  

    ``` SQL
    EXECUTE sp_configure 'max text repl size (B)', 2147483647
    ```

- В качестве владельца базы данных укажите *учетную запись SA*. Вам не нужно включать эту учетную запись.

- Установите значение **ВКЛЮЧИТЬ** для параметра **НАДЕЖНОСТЬ**:

    ``` SQL
    ALTER DATABASE [CM_xxx] SET TRUSTWORTHY ON;
    ```

    Дополнительные сведения см. в описании [свойства базы данных TRUSTWORTHY](https://docs.microsoft.com/sql/relational-databases/security/trustworthy-database-property).

- Включите компонент **Service Broker**:  

    ``` SQL
    ALTER DATABASE [CM_xxx] SET ENABLE_BROKER
    ```

    > [!Note]  
    > Параметр компонента Service Broker нельзя включить для базы данных, которая уже входит в группу доступности. Необходимо включить этот параметр, прежде чем добавлять его в группу доступности.<!-- SCCMDocs#1432 -->

- Настройка приоритета компонента Service Broker:

    ``` SQL
    ALTER DATABASE [CM_xxx] SET HONOR_BROKER_PRIORITY ON;
    ALTER DATABASE [CM_xxx] SET ENABLE_BROKER WITH ROLLBACK IMMEDIATE

    ```

Эти настройки следует указывать только на первичной реплике. Чтобы настроить вторичную реплику, сначала выполните отработку отказа с первичной реплики на вторичную. Это действие сделает бывшую вторичную реплику первичной.

#### <a name="database-verification-script"></a>Скрипт проверки базы данных

Выполните следующий скрипт SQL, чтобы проверить конфигурацию базы данных на первичной и вторичной репликах. Прежде чем устранять проблемы на вторичной реплике, сделайте ее первичной.

``` SQL
    SET NOCOUNT ON

    DECLARE @dbname NVARCHAR(128)

    SELECT @dbname = sd.name FROM sys.sysdatabases sd WHERE sd.dbid = DB_ID()

    IF (@dbname = N'master' OR @dbname = N'model' OR @dbname = N'msdb' OR @dbname = N'tempdb' OR @dbname = N'distribution' ) BEGIN
    RAISERROR(N'ERROR: Script is targeting a system database.  It should be targeting the DB you created instead.', 0, 1)
    GOTO Branch_Exit;
    END ELSE
    PRINT N'INFO: Targeted database is ' + @dbname + N'.'

    PRINT N'INFO: Running verifications....'

    IF NOT EXISTS (SELECT * FROM sys.configurations c WHERE c.name = 'clr enabled' AND c.value_in_use = 1)
    PRINT N'ERROR: CLR is not enabled!'
    ELSE
    PRINT N'PASS: CLR is enabled.'

    DECLARE @repltable TABLE (
    name nvarchar(max),
    minimum int,
    maximum int,
    config_value int,
    run_value int )

    INSERT INTO @repltable
    EXEC sp_configure 'max text repl size (B)'

    IF NOT EXISTS(SELECT * from @repltable where config_value = 2147483647 and run_value = 2147483647 )
    PRINT N'ERROR: Max text repl size is not correct!'
    ELSE
    PRINT N'PASS: Max text repl size is correct.'

    IF NOT EXISTS (SELECT db.owner_sid FROM sys.databases db WHERE db.database_id = DB_ID() AND db.owner_sid = 0x01)
    PRINT N'ERROR: Database owner is not sa account!'
    ELSE
    PRINT N'PASS: Database owner is sa account.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_trustworthy_on = 1 )
    PRINT N'ERROR: Trustworthy bit is not on!'
    ELSE
    PRINT N'PASS: Trustworthy bit is on.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_broker_enabled = 1 )
    PRINT N'ERROR: Service broker is not enabled!'
    ELSE
    PRINT N'PASS: Service broker is enabled.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_honor_broker_priority_on = 1 )
    PRINT N'ERROR: Service broker priority is not set!'
    ELSE
    PRINT N'PASS: Service broker priority is set.'

    PRINT N'Done!'

    Branch_Exit:
```


### <a name="availability-group-configurations"></a>Конфигурации групп доступности

#### <a name="replica-members"></a>Члены реплик

- Группа доступности должна иметь по меньшей мере одну конечную точку.  

- Число и тип реплик в группе доступности должны поддерживаться в используемой версии SQL Server.

- Вы можете использовать реплику с асинхронной фиксацией для восстановления синхронных реплик. Дополнительные сведения см. в статье о [вариантах восстановления для базы данных сайта](../../manage/recover-sites.md#site-database-recovery-options).  

    > [!Warning]  
    > Configuration Manager не поддерживает использование реплики с асинхронной фиксацией в качестве базы данных сайта при *отработке отказа*. Дополнительные сведения см. в статье об [отработке отказа и доступных режимах для групп доступности AlwaysOn](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups).  

Configuration Manager не проверяет состояние и актуальность реплики с асинхронной фиксацией. Использование реплики с асинхронной фиксацией в качестве базы данных сайта может нарушить целостность сайта и данных. Эта реплика может быть не синхронизирована умышленно. Дополнительные сведения см. в статье [Обзор групп доступности SQL Server Always On](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server).

Каждый член реплики должен иметь следующие настройки:

- используйте *экземпляр по умолчанию* или *именованный экземпляр*;  

- для параметра **Соединения в первичной роли** установите значение **Разрешить все соединения**;  

- для параметра **Вторичная реплика для чтения** установите значение **Да**;  

- включите функцию **Отработка отказа вручную**.

    > [!Note]
    > В версии 1902 и более ранних необходимо настроить все группы доступности на SQL Server для автоматической обработки отказа. Такая конфигурация необходима, даже если она не размещает базу данных сайта.
    >
    > Начиная с версии 1906, Configuration Manager поддерживает использование синхронных реплик группы доступности, если настроена **автоматическая отработка отказа**. Функцию **Отработка отказа вручную** следует использовать в следующих ситуациях:
    >
    > - Чтобы указать использование базы данных сайта в группе доступности, запустите программу установки Configuration Manager.  
    > - если вы установили любое обновление Configuration Manager. (Речь идет не только об обновлениях, которые затрагивают базу данных сайта.)  

- Все члены должны иметь одинаковый [режим заполнения](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/automatic-seeding-secondary-replicas).<!-- SCCMDocs-pr#3899 --> Установка Configuration Manager включает в себя проверку предварительных условий для проверки этой конфигурации при создании базы данных путем установки или восстановления.

    > [!Note]  
    > Когда программа установки создает базу данных и вы настраиваете **автоматическое** заполнение начальных значений, группа доступности должна иметь разрешения на создание базы данных. Это требование относится как к новой базе данных, так и к восстановленной. Дополнительные сведения см. в разделе [Автоматическое заполнение для вторичной реплики](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/automatic-seeding-secondary-replicas#security).<!-- SCCMDocs-pr#3900 -->

#### <a name="replica-member-location"></a>Расположение члена реплики

Все реплики в группе доступности следует размещать в одном расположении: локально или в Microsoft Azure. Не поддерживается создание групп, включающих одновременно локальные и облачные (Azure) члены.

Установка Configuration Manager должна иметь доступ к каждой реплике. Если вы настраиваете группу доступности в Azure за внутренней или внешней подсистемой балансировки нагрузки, откройте перечисленные ниже порты по умолчанию:

- Сопоставитель конечных точек RPC — **TCP 135**

- SQL Server Service Broker: **TCP 4022**  

- SQL через TCP: **TCP 1433**

После завершения установки следующие порты должны оставаться открытыми для Configuration Manager:  

- SQL Server Service Broker: **TCP 4022**  

- SQL через TCP: **TCP 1433**  

Для этих конфигураций можно использовать настраиваемые порты. Необходимо использовать одинаковые настраиваемые порты на конечной точке и на всех репликах в группе доступности.

#### <a name="listener"></a>Прослушиватель

Группа доступности должна иметь минимум один *прослушиватель группы доступности*. Виртуальное имя этого прослушивателя применяется при настройке Configuration Manager для использования базы данных сайта в группе доступности. Хотя группа доступности может содержать несколько прослушивателей, Configuration Manager может использовать только один. См. дополнительные сведения о [создании или настройке прослушивателя группы доступности (SQL Server)](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server).

#### <a name="file-paths"></a>Пути к файлам

При запуске программы установки Configuration Manager для настройки сайта для использования базы данных в группе доступности, каждый вторичный сервер реплики должен иметь путь к файлу SQL Server, идентичный пути к файлам базы данных сайта в текущей первичной реплике. Если идентичного пути не существует, программе установки не удастся добавить экземпляр для группы доступности в качестве нового расположения базы данных сайта.  

Локальной учетной записи службы SQL Server требуется разрешение **Полный доступ** для этой папки.

Вторичным серверам реплики требуется только этот путь к файлу в рамках использования установки Configuration Manager для выбора экземпляра базы данных в группе доступности. Когда эта программа закончит настройку базы данных сайта в группе доступности, вы можете удалить неиспользуемый путь с серверов вторичной реплики.

Например, рассмотрим следующий сценарий.

- Вы создали группу доступности, которая использует три сервера SQL Server.  

- Сервер первичной реплики является новой установкой SQL Server 2014. По умолчанию он хранит MDF- и LDF-файлы базы данных в папке `C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA`.  

- Оба сервера вторичной реплики обновлены из предыдущих версий до SQL Server 2014. При этом обновлении серверы сохраняют исходный путь для хранения файлов базы данных: `C:\Program Files\Microsoft SQL Server\MSSQL10.MSSQLSERVER\MSSQL\DATA`.  

- Прежде чем перемещать базу данных сайта в эту группу доступности, создайте на каждом сервере вторичной реплики следующий путь файла: `C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA`. Это точная копия пути, указанного на первичной реплике. Возможно, вторичные реплики не будут использовать это расположение файла.  

- Теперь на каждом сервере вторичной реплики предоставьте учетной записи службы SQL Server полный доступ к только что созданному расположению.  

- Теперь вы можете успешно запустить установку Configuration Manager, чтобы настроить сайт на использование базы данных сайта в группе доступности.  

#### <a name="multi-subnet-failover"></a>Отработка отказа с несколькими подсетями

<!-- SCCMDocs-pr#3734 -->
Начиная с версии 1906 можно включить [ключевое слово "MultiSubnetFailover" строки подключения](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server#MultiSubnetFailover) в SQL Server. Также необходимо вручную добавить следующие значения в реестр Windows на сервере сайта:

``` Registry
HKLM:\SOFTWARE\Microsoft\SMS\Identification
HKLM:\SOFTWARE\Microsoft\SMS\SQL Server

MSF Enabled : 1 (DWORD)
```

> [!Warning]  
> Использование [высокой доступности сервера сайта](site-server-high-availability.md) и SQL Server Always On с аварийным переключением между несколькими подсетями не обеспечивает полных возможностей автоматического аварийного переключения для сценариев аварийного восстановления.

Если необходимо создать группу доступности с членом в удаленном расположении, следует установить приоритет на основе наименьшей задержки сети. Высокая задержка в сети может привести к сбоям репликации.<!-- SCCMDocs#1381 -->


## <a name="limitations-and-known-issues"></a>Ограничения и известные проблемы

На все сценарии распространяются указанные ниже ограничения.

### <a name="unsupported-sql-server-options-and-configurations"></a>Не поддерживаемые параметры и конфигурации SQL Server

- **Базовые группы доступности**. Представленные SQL Server 2016 Standard Edition, базовые группы доступности не поддерживают доступ на чтение ко вторичным репликам. Этот доступ нужен для конфигурации. Дополнительные сведения см. в статье [Базовые группы доступности (группы доступности AlwaysOn)](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups?view=sql-server-2017).  

- **Экземпляр отказоустойчивого кластера**. Экземпляры отказоустойчивого кластера не поддерживаются для реплики, используемой с Configuration Manager. Дополнительные сведения см. в статье [Экземпляры отказоустойчивого кластера AlwaysOn (SQL Server)](https://docs.microsoft.com/sql/sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server).  

- **MultiSubnetFailover**. В версии 1902 и более ранних, не поддерживается использование группы доступности с Configuration Manager в конфигурации с несколькими подсетями. Также нельзя использовать ключевое слово [MutliSubnetFailover](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server#MultiSubnetFailover) в строке подключения.

    Для поддержки этой конфигурации обновите Configuration Manager до версии 1906 или более поздней. Дополнительные сведения см. в разделе с предварительными требованиями для [отработки отказа с несколькими подсетями](sql-server-alwayson-for-a-highly-available-site-database.md#multi-subnet-failover).

### <a name="sql-servers-that-host-additional-availability-groups"></a>Серверы SQL, на которых размещаются дополнительные группы доступности

<!--SCCMDocs issue 649-->
Когда SQL Server содержит одну или несколько групп доступности в дополнение к группе, которая используется для установки Configuration Manager, ему требуются особые настройки во время запуска установки Configuration Manager. Эти же параметры нужны для установки обновлений Configuration Manager. Каждая реплика в каждой группе доступности должна иметь следующие настройки:

- отработка отказа вручную;  
- разрешение любого подключения только для чтения.  

> [!Note]
> В версии 1902 и более ранних необходимо настроить все группы доступности на SQL Server для автоматической обработки отказа. Такая конфигурация необходима, даже если она не размещает базу данных сайта.
>
> Начиная с версии 1906, Configuration Manager поддерживает использование синхронных реплик группы доступности, если настроена **автоматическая отработка отказа**. Функцию **Отработка отказа вручную** следует использовать в следующих ситуациях:
>
> - Чтобы указать использование базы данных сайта в группе доступности, запустите программу установки Configuration Manager.  
> - если вы установили любое обновление Configuration Manager. (Речь идет не только об обновлениях, которые затрагивают базу данных сайта.)  

### <a name="unsupported-database-use"></a>Неподдерживаемое использование базы данных

#### <a name="configuration-manager-supports-only-the-site-database-in-an-availability-group"></a>Configuration Manager поддерживает только сайт базы данных в группе доступности

Следующие базы данных не поддерживаются Configuration Manager в группе доступности SQL Server Always On:  

- база данных отчетов;  
- база данных WSUS.  

#### <a name="pre-existing-database"></a>Существующая база данных

Нельзя использовать новую базу данных, созданную в реплике. При настройке группы доступности следует восстановить на первичной реплике копию существующей базы данных Configuration Manager.  

#### <a name="distributed-views"></a>Распределенные представления

<!-- SCCMDocs-pr#3792 -->
В версии 1902 и более ранних, если база данных сайта размещена в группе доступности SQL Server Always on, нельзя включить [распределенные представления](../../../plan-design/hierarchy/data-transfers-between-sites.md#bkmk_dbrep) для репликации базы данных. Для поддержки этой конфигурации обновите ее до версии 1906 или более поздней.


### <a name="setup-errors-in-configmgrsetuplog"></a>Ошибки установки в файле ConfigMgrSetup.log

При запуске программы установки Configuration Manager для перемещения базы данных сайта в группу доступности, программа пытается обработать роли базы данных на вторичных репликах группы доступности. При этом в файл **ConfigMgrSetup.log** сохраняется следующая ошибка:  

`ERROR: SQL Server error: [25000][3906][Microsoft][SQL Server Native Client 11.0][SQL Server]Failed to update database "CM_AAA" because the database is read-only. Configuration Manager Setup 1/21/2016 4:54:59 PM 7344 (0x1CB0)`  

Эти ошибки можно спокойно игнорировать.

### <a name="site-expansion"></a>Расширение сайта

<!--SCCMDocs issue 568-->
Если вы настраиваете использование SQL Always On для базы данных автономного первичного сайта, этот сайт нельзя расширить путем добавления сайта центра администрирования. Такой процесс завершится сбоем. Чтобы расширить этот сайт, временно удалите первичную базу данных сайта из группы доступности.

При добавлении вторичного сайта вносить изменения в конфигурацию не требуется.


## <a name="changes-for-site-backup"></a>Изменения, относящиеся к резервному копированию сайта

### <a name="backup-database-files"></a>Резервное копирование файлов базы данных
  
Если база данных сайта использует группу доступности, запустите встроенную задачу обслуживания **Резервное копирование сайта**, которая создает резервные копии основных параметров и файлов Configuration Manager. Не используйте файлы с расширением .mdf или .ldf, созданные этой задачей резервного копирования. Вместо этого создавайте прямые резервные копии базы данных сайта средствами SQL Server.

### <a name="transaction-log"></a>Журнал транзакций  

Настройте для базы данных модель **полного** восстановления. Эта конфигурация является обязательной для работы Configuration Manager в группе доступности. Создайте систему мониторинга и корректировки размера для журнала транзакций базы данных сайта. В модели полного восстановления транзакции не защищены, пока не создана полная резервная копия базы данных или журнала транзакций. Дополнительные сведения см. в разделе [Резервное копирование и восстановление баз данных SQL Server](https://docs.microsoft.com/sql/relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases).


## <a name="changes-for-site-recovery"></a>Изменения, относящиеся к восстановлению сайта

Если функционирует хотя бы один узел группы доступности, для восстановления сайта можно использовать вариант **Пропустить восстановление базы данных (используйте этот параметр, если база данных сайта не затронута)** .

Начиная с версии 1906, восстановление сайта может повторно создать базу данных в группе SQL Always On. Этот процесс работает как с автоматическим заполнением, так и с заполнением вручную.<!-- SCCMDocs-pr#3846 -->

В версии 1902 или более ранней, если утрачены все узлы группы доступности, перед восстановлением сайта необходимо повторно создать группу доступности. Configuration Manager не может самостоятельно создавать или восстанавливать узлы доступности. Создайте группу, восстановите резервную копию и настройте параметры SQL. После этого выполните восстановление с параметром **Пропустить восстановление базы данных (используйте этот параметр, если база данных сайта не затронута)** .

Дополнительные сведения см. в статье [Резервное копирование и восстановление](../../manage/backup-and-recovery.md).


## <a name="changes-for-reporting"></a>Изменения, относящиеся к отчетам

### <a name="install-the-reporting-service-point"></a>Установка точки служб отчетов

Точка служб отчетов не поддерживает использование виртуального имени прослушивателя группы доступности. Также она не может размещать базу данных в группе доступности SQL Server Always On.  

- По умолчанию при установке точки служб отчетов для параметра **Имя сервера базы данных сайта** указывается виртуальное имя, присвоенное прослушивателю. Измените это значение, чтобы указать имя компьютера и экземпляр реплики в группе доступности.  

- Чтобы снизить нагрузку, связанную с отчетами, и повысить доступность узла реплики в автономном режиме, мы рекомендуем установить дополнительные точки служб отчетов на каждом узле реплики. Настройте каждую точку служб отчетов так, чтобы она использовала собственное имя компьютера. Если вы установите точку служб отчетов на каждой реплике в группе доступности, служба отчетов всегда сможет связаться с активным сервером точки служб отчетов.  

### <a name="switch-the-reporting-services-point-used-by-the-console"></a>Изменение точки служб отчетов, используемой для консоли

1. В консоли Configuration Manager перейдите к рабочей области **Наблюдение**, разверните пункт **Отчеты**, и выберите узел **Отчеты**.

1. На ленте выберите **Параметры отчета**.  

1. В диалоговом окне параметров отчета выберите нужную точку служб отчетов.  


## <a name="next-steps"></a>Дальнейшие шаги

В этой статье описаны предварительные требования, ограничения и изменения для выполнения стандартных задач, которые требуются Configuration Manager при использовании групп доступности. Процедуры установки и настройки групп доступности для сайта см. в статье [Настройка групп доступности SQL Server AlwaysOn для Configuration Manager](configure-aoag.md).
