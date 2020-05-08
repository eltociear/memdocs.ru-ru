---
title: Поддерживаемые версии SQL Server
titleSuffix: Configuration Manager
description: Сведения о требованиях к версии и конфигурации SQL Server для размещения базы данных сайта Configuration Manager.
ms.date: 04/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 35e237b6-9f7b-4189-90e7-8eca92ae7d3d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3c52008089a6d23d5c4efe44f0970bb186eb334a
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/07/2020
ms.locfileid: "82904635"
---
# <a name="supported-sql-server-versions-for-configuration-manager"></a>Поддерживаемые версии SQL Server в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Каждому сайту Configuration Manager требуется поддерживаемая версия и конфигурация SQL Server для размещения базы данных сайта.  

## <a name="sql-server-instances-and-locations"></a><a name="bkmk_Instances"></a> Экземпляры SQL Server и расположения

### <a name="central-administration-site-and-primary-sites"></a>Сайт центра администрирования и первичные сайты

База данных сайта должна использовать установленную полную версию SQL Server.  

Возможные расположения SQL Server:  

- компьютер сервера сайта;  
- удаленный компьютер относительно сервера сайта.  

Поддерживаются следующие экземпляры:  

- экземпляр по умолчанию или именованный экземпляр SQL Server;  
- несколько конфигураций экземпляров;  
- кластер SQL Server; См. раздел [Использование кластера SQL Server для размещения базы данных сайта](../../servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database.md).
- группа доступности SQL Server AlwaysOn. Дополнительные сведения см. в статье [Подготовка к использованию групп доступности SQL Server AlwaysOn](../../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).

### <a name="secondary-sites"></a>Вторичные сайты

База данных сайта может использовать экземпляр по умолчанию установленной полной версии SQL Server или экспресс-выпуска SQL Server.  

SQL Server должен находиться на компьютере сервера сайта.  

### <a name="limitations-to-support"></a>Ограничения для поддержки

Не поддерживаются следующие конфигурации:

- кластер SQL Server в конфигурации кластера балансировки сетевой нагрузки (NLB);
- кластер SQL Server в общем томе кластера (CSV);
- технология зеркального отображения базы данных SQL Server и одноранговая репликация.

Репликация транзакций SQL Server поддерживается только для репликации объектов в точки управления, настроенные на использование [реплик базы данных](../../servers/deploy/configure/database-replicas-for-management-points.md).  

## <a name="supported-versions-of-sql-server"></a><a name="bkmk_SQLVersions"></a> Поддерживаемые версии SQL Server

В иерархии с несколькими сайтами разные сайты могут использовать разные версии SQL Server для размещения базы данных сайта только в следующих случаях:

- Configuration Manager поддерживает используемые версии SQL Server.
- Используемые версии SQL Server поддерживаются корпорацией Майкрософт.
- SQL Server поддерживает репликацию между двумя версиями SQL Server. Дополнительные сведения см. в статье [Обратная совместимость репликации](https://docs.microsoft.com/sql/relational-databases/replication/replication-backward-compatibility).

В SQL Server 2016 и более ранних версиях поддержка каждой версии SQL и пакета обновления предоставляется в соответствии с [политикой жизненного цикла Майкрософт](https://aka.ms/sqllifecycle). Поддержка конкретного пакета обновления SQL Server включает накопительные пакеты обновления, если только они не нарушают обратную совместимость с базовой версией пакета обновления. Начиная с SQL Server 2017, пакеты обновления не будут выпускаться, так как к ним применяется [современная модель обслуживания](https://docs.microsoft.com/archive/blogs/sqlreleaseservices/announcing-the-modern-servicing-model-for-sql-server). Команда SQL Server рекомендует регулярно [в упреждающем режиме устанавливать накопительные пакеты обновления](https://docs.microsoft.com/archive/blogs/sqlreleaseservices/announcing-updates-to-the-sql-server-incremental-servicing-model-ism), как только они становятся доступными.

Если не указано иное, следующие версии SQL Server поддерживаются всеми актуальными версиями Configuration Manager. Если добавляется поддержка новой версии SQL Server, будет указана версия Configuration Manager, в которой появилась эта поддержка. Аналогично, если поддержка прекращается, будут предоставлены сведения о затронутых версиях Configuration Manager.

> [!IMPORTANT]  
> При использовании SQL Server Standard для базы данных сайта центра администрирования вы ограничиваете общее число клиентов, поддерживаемых иерархией. См. раздел [Данные по размерам и масштабированию](size-and-scale-numbers.md).

### <a name="sql-server-2019-standard-enterprise"></a>SQL Server 2019: Standard и Enterprise.

Начиная с версии Configuration Manager 1910, вы можете использовать эту версию SQL Server с любым накопительным обновлением, если версия накопительного обновления поддерживается жизненным циклом SQL.

Эту версию SQL можно использовать для следующих сайтов:

- сайт центра администрирования
- первичный сайт;
- вторичный сайт.

#### <a name="known-issue-with-sql-server-2019"></a>Известная проблема с SQL Server 2019

Существует известная проблема<!--6436234--> с новой функцией [встраивания скалярных определяемых пользователем функций](https://docs.microsoft.com/sql/relational-databases/user-defined-functions/scalar-udf-inlining) в SQL 2019. Чтобы решить эту проблему и отключить встраивание определяемых пользователем функций, выполните следующий скрипт в SQL Server 2019:

```sql
ALTER DATABASE SCOPED CONFIGURATION SET TSQL_SCALAR_UDF_INLINING = OFF  
```

После выполнения этого скрипта может потребоваться перезапустить SQL Server, хотя это не всегда обязательно. См. сведения об [отключении встраивания скалярных определяемых пользователем функций без изменения уровня совместимости](https://docs.microsoft.com/sql/relational-databases/user-defined-functions/scalar-udf-inlining?view=sql-server-ver15#disabling-scalar-udf-inlining-without-changing-the-compatibility-level).

Вы можете отключить эту функцию SQL для сервера базы данных сайта, так как в Configuration Manager она не используется.

Если не отключить эту функцию в SQL Server 2019, на сервере сайта время от времени будет происходить сбой при отправке запроса к базе данных. Например, в журнале **hman.log** будут отображаться следующие ошибки:

```hman.log
*** [HY000][0][Microsoft][SQL Server Native Client 11.0]Unspecified error occurred on SQL Server. Connection may have been terminated by the server.
*** select dbo.fnGetSiteMode(dbo.fnGetSiteCode())
*** [HY000][596][Microsoft][SQL Server Native Client 11.0][SQL Server]Cannot continue the execution because the session is in the kill state.
Failed to execute SQL command select dbo.fnGetSiteMode(dbo.fnGetSiteCode())
```

Похожие ошибки могут появиться и в других журналах, например **SmsAdminUI.log**.

В SQL Server версии 2019 регистрируется следующая ошибка:

`Microsoft SQL Server reported SQL message 596, severity 21: [HY000][596][Microsoft][SQL Server Native Client 11.0][SQL Server]Cannot continue the execution because the session is in the kill state.`

Вы также увидите аварийные дампы (файлы `.mdump`) в SQL в каталоге журналов (по умолчанию `C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\Log`).

### <a name="sql-server-2017-standard-enterprise"></a>SQL Server 2017: Standard и Enterprise.

Эту версию можно использовать с [накопительным обновлением 2](https://support.microsoft.com/help/4052574) или более поздней версии, если версия накопительного обновления поддерживается жизненным циклом SQL. Эту версию SQL можно использовать для следующих сайтов:

- сайт центра администрирования  
- первичный сайт;  
- вторичный сайт.  
  <!--SMS.498506-->

### <a name="sql-server-2016-standard-enterprise"></a>SQL Server 2016: Standard и Enterprise.  
<!--514985-->
Эту версию можно использовать с минимальным пакетом обновления и накопительным обновлением, поддерживаемыми жизненным циклом SQL. Эту версию SQL можно использовать для следующих сайтов:

- сайт центра администрирования  
- первичный сайт;  
- вторичный сайт.  

### <a name="sql-server-2014-standard-enterprise"></a>SQL Server 2014: Standard и Enterprise.

Эту версию можно использовать с минимальным пакетом обновления и накопительным обновлением, поддерживаемыми жизненным циклом SQL. Эту версию SQL можно использовать для следующих сайтов:

- сайт центра администрирования  
- первичный сайт;  
- вторичный сайт.

### <a name="sql-server-2012-standard-enterprise"></a>SQL Server 2012: Standard и Enterprise.

Эту версию можно использовать с минимальным пакетом обновления и накопительным обновлением, поддерживаемыми жизненным циклом SQL. Эту версию SQL можно использовать для следующих сайтов:

- сайт центра администрирования  
- первичный сайт;  
- вторичный сайт.  

### <a name="sql-server-2017-express"></a>SQL Server 2017 Express

Эту версию можно использовать с [накопительным обновлением 2](https://support.microsoft.com/help/4052574) или более поздней версии, если версия накопительного обновления поддерживается жизненным циклом SQL. Эту версию SQL можно использовать для следующих сайтов:

- вторичный сайт.
<!--SMS.498506-->

### <a name="sql-server-2016-express"></a>SQL Server 2016, экспресс-выпуск

Эту версию можно использовать с минимальным пакетом обновления и накопительным обновлением, поддерживаемыми жизненным циклом SQL. Эту версию SQL можно использовать для следующих сайтов:

- вторичный сайт.

### <a name="sql-server-2014-express"></a>SQL Server 2014 Express

Эту версию можно использовать с минимальным пакетом обновления и накопительным обновлением, поддерживаемыми жизненным циклом SQL. Эту версию SQL можно использовать для следующих сайтов:

- вторичный сайт.  

### <a name="sql-server-2012-express"></a>SQL Server 2012 Express

Эту версию можно использовать с минимальным пакетом обновления и накопительным обновлением, поддерживаемыми жизненным циклом SQL. Эту версию SQL можно использовать для следующих сайтов:

- вторичный сайт.  

## <a name="required-configurations-for-sql-server"></a><a name="bkmk_SQLConfig"></a> Обязательные конфигурации для SQL Server

Ниже перечислены необходимые конфигурации для всех устанавливаемых версий SQL Server, используемых для базы данных сайта (включая экспресс-выпуск SQL Server). Если Configuration Manager устанавливает выпуск SQL Server Express в процессе установки вторичного сайта, эти конфигурации создаются автоматически.  

### <a name="sql-server-architecture-version"></a>Версия архитектуры SQL Server

Для работы Configuration Manager требуется 64-разрядная версия SQL Server для размещения базы данных сайта.  

### <a name="database-collation"></a>Параметры сортировки баз данных

На всех сайтах экземпляр SQL Server, используемый для сайта, и база данных сайта должны использовать следующие параметры сортировки: **SQL_Latin1_General_CP1_CI_AS**.  

Configuration Manager поддерживает два исключения из этих параметров сортировки для стандарта China GB18030. См. дополнительные сведения о [поддержке в разных странах](../hierarchy/international-support.md).  

### <a name="database-compatibility-level"></a>Уровень совместимости базы данных

Configuration Manager требует, чтобы уровень совместимости базы данных сайта был не ниже минимальной версии SQL Server, поддерживаемой вашей версией Configuration Manager. Например, начиная с версии 1702 требуется [уровень совместимости базы данных](https://docs.microsoft.com/sql/relational-databases/databases/view-or-change-the-compatibility-level-of-a-database) не ниже 110. <!-- SMS.506266-->

### <a name="sql-server-features"></a>Компоненты SQL Server

Для каждого сервера сайта требуются только **службы компонента Database Engine** .  

Для репликации баз данных Configuration Manager не требуется компонент **Репликация SQL Server**. Но эта конфигурация SQL Server необходима при использовании [реплик базы данных для точек управления](../../servers/deploy/configure/database-replicas-for-management-points.md).  

### <a name="windows-authentication"></a>Проверка подлинности Windows

Configuration Manager требуется компонент **проверки подлинности Windows** для проверки подключений к базе данных.  

### <a name="sql-server-instance"></a>Экземпляр SQL Server

Для каждого сайта необходимо использовать выделенный экземпляр SQL Server. Это может быть **именованный экземпляр** или **экземпляр по умолчанию**.  

### <a name="sql-server-memory"></a>Память SQL Server

Зарезервируйте память для SQL Server с помощью SQL Server Management Studio. Установите параметр **Минимальный объем памяти сервера** в разделе **Параметры памяти сервера**. См. дополнительные сведения о [параметрах конфигурации сервера памяти SQL Server](https://docs.microsoft.com/sql/database-engine/configure-windows/server-memory-server-configuration-options).  

- **Сервер базы данных, который установлен на том же компьютере, что и сервер сайта**: Предельный объем памяти, выделяемой для SQL Server, должен составлять 50–80 % общего объема памяти системы.  

- **Выделенный сервер базы данных, удаленный от сервера сайта**: Предельный объем памяти, выделяемой для SQL Server, должен составлять 80–90 % общего объема памяти системы.  

- **Резерв памяти для буферного пула каждого используемого экземпляра SQL Server**.  

  - Сайт центра администрирования: установите не менее 8 ГБ.  
  - Основной сайт: установите не менее 8 ГБ.  
  - Дополнительный сайт: установите не менее 4 ГБ.  

### <a name="sql-nested-triggers"></a>Вложенные триггеры SQL

Вложенные триггеры SQL должны быть включены. См. дополнительные сведения о [настройке параметра конфигурации сервера вложенных триггеров](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-the-nested-triggers-server-configuration-option).

### <a name="sql-server-clr-integration"></a>Интеграция со средой CLR для SQL Server

Для работы базы данных сайта требуется среда CLR для SQL Server. Этот параметр включается автоматически при установке Configuration Manager. Дополнительные сведения о среде CLR см. в разделе [Введение в интеграцию SQL Server со средой CLR](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/introduction-to-sql-server-clr-integration).  

### <a name="sql-server-service-broker-ssb"></a>SQL Server Service Broker (SSB)

SQL Server Service Broker является обязательным как для межсайтовой репликации, так и для одного первичного сайта.

### <a name="trustworthy-setting"></a>Параметр TRUSTWORTHY

Configuration Manager автоматически включает свойство базы данных SQL [TRUSTWORTHY](https://docs.microsoft.com/sql/relational-databases/security/trustworthy-database-property). Для Configuration Manager требуется **включить** это свойство.

## <a name="optional-configurations-for-sql-server"></a><a name="bkmk_optional"></a> Дополнительные конфигурации для SQL Server

Следующие конфигурации являются необязательными для каждой базы данных, использующей полную установку SQL Server.  

### <a name="sql-server-service"></a>Служба SQL Server

Вы можете настроить службу SQL Server на выполнение с использованием следующих средств.  

- Учетная запись *пользователя домена с ограниченными правами*:  

  - Мы рекомендуем использовать этот параметр. При этом может потребоваться вручную зарегистрировать имя субъекта-службы (SPN) для учетной записи.  

- Учетная запись **локальной системы** компьютера, на котором выполняется SQL Server:  

  - Используйте учетную запись локальной системы для упрощения процесса настройки.  
  - Если используется учетная запись локальной системы, Configuration Manager автоматически регистрирует имя субъекта-службы для службы SQL Server.  
  - Использовать учетную запись локальной системы для службы SQL Server не рекомендуется.  

Когда компьютер SQL Server не использует учетную запись локальной системы для запуска служб SQL Server, необходимо настроить имя SPN учетной записи, которая используется для запуска службы SQL Server в доменных службах Active Directory. (При использовании системной учетной записи имя субъекта-службы регистрируется автоматически.)

См. дополнительные сведения об [управлении именами субъектов-служб для сервера базы данных сайта](../../servers/manage/modify-your-infrastructure.md#bkmk_SPN).  

См. дополнительные сведения об [изменении стартовой учетной записи службы для SQL Server в службах диспетчера служб](https://docs.microsoft.com/sql/database-engine/configure-windows/scm-services-change-the-service-startup-account).  

### <a name="sql-server-reporting-services"></a>Службы SQL Server Reporting Services

Службы SQL Server Reporting Services необходимы для установки точки служб отчетов, позволяющей создавать отчеты. Configuration Manager поддерживает те же версии SQL Server для создания отчетов, что и для базы данных сайта.

См. сведения о [необходимых условиях для создания отчетов в Configuration Manager](../../servers/manage/prerequisites-for-reporting.md).

> [!IMPORTANT]  
> После обновления SQL Server предыдущей версии может возникнуть следующая ошибка: *Построитель отчетов не существует*.  
> Для устранения этой ошибки необходимо переустановить роль системы сайта "Точка служб отчетов".  

### <a name="data-warehouse-service-point"></a>Точка обслуживания хранилища данных

Для хранилища данных используется отдельная база данных. Ее можно разместить на сервере базы данных сайта или в отдельном экземпляре SQL Server. См. сведения о [точке обслуживания хранилища данных для Configuration Manager](../../servers/manage/data-warehouse.md).

### <a name="sql-server-ports"></a>Порты SQL Server

Для обмена данными с компонентом SQL Server Database Engine, а также для межсайтовой репликации можно использовать конфигурацию портов SQL Server по умолчанию или указать другие порты.  

- Для **межсайтового обмена данными** применяется компонент SQL Server Service Broker, который по умолчанию использует TCP-порт 4022.  
- **Для внутрисайтового обмена данными** между системой базы данных SQL Server и различными ролями системы сайта Configuration Manager по умолчанию используется порт TCP 1433. Следующие роли систем сайта соединяются напрямую с базой данных SQL Server.  

  - Точка управления  
  - Компьютер поставщика SMS  
  - Точка служб отчетов  
  - Сервер сайтов  

Если на сервере SQL Server размещены базы данных нескольких сайтов, каждая база данных должна использовать отдельный экземпляр SQL Server. Кроме того, для каждого экземпляра должен быть настроен уникальный набор портов.  

> [!WARNING]  
> Configuration Manager не поддерживает динамические порты. Именованные экземпляры SQL Server по умолчанию используют динамические порты для подключения к компоненту Database Engine, поэтому при использовании именнованного экземпляра необходимо вручную настроить статический порт для внутрисайтовой передачи данных.  

Если на компьютере с SQL Server включен брандмауэр, убедитесь, что в нем открыты порты, используемые для развертывания. Также эти порты должны быть открыты во всех расположениях в сети между компьютерами, которые обмениваются данными с сервером SQL Server.  

См. дополнительные сведения о [настройке сервера SQL Server для прослушивания определенного TCP-порта](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port).  

## <a name="upgrade-options-for-sql-server"></a>Параметры обновления для SQL Server

Если вам нужно обновить версию SQL Server, используйте перечисленные здесь методы от простых к более сложным:  

- [Обновите SQL Server на месте](../../servers/manage/upgrade-on-premises-infrastructure.md#to-upgrade-sql-server-on-the-site-database-server) (рекомендуется).  

- Установите новую версию SQL Server на новом компьютере, а затем [воспользуйтесь функцией перемещения базы данных](../../servers/manage/modify-your-infrastructure.md#bkmk_dbconfig) в установщике Configuration Manager, чтобы сервер сайта мог обращаться к новому серверу SQL Server.  

- Используйте функции [резервного копирования и восстановления](../../servers/manage/backup-and-recovery.md). Поддерживается использование резервного копирования и восстановления сценария обновления SQL. При просмотре [рекомендаций перед восстановлением сайта](../../servers/manage/recover-sites.md#considerations-before-recovering-a-site) требование к управлению версиями SQL можно проигнорировать.
