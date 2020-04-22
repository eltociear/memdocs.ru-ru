---
title: Предварительные требования для сайта
titleSuffix: Configuration Manager
description: Узнайте, как настроить компьютер Windows в качестве сервера системы сайта Configuration Manager.
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1392797b-76cb-46b4-a3e4-8f349ccaa078
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d4fb94d0ab64cb7c3dc3128c982b0c2b162b22b7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702162"
---
# <a name="site-and-site-system-prerequisites-for-configuration-manager"></a>Предварительные требования к сайту и системе сайта для Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Компьютерам с ОС Windows требуется особая конфигурация, чтобы их можно было использовать в качестве серверов системы сайта Configuration Manager.

Для некоторых продуктов, таких как службы Windows Server Update Services (WSUS) для точки обновления программного обеспечения, необходимо обратиться к документации, чтобы ознакомиться с дополнительными требованиями и ограничениями. Здесь приводятся конфигурации, которые непосредственно касаются использования Configuration Manager.

Для получения дополнительной информации о .NET Framework см. статью [Вопросы и ответы: жизненный цикл .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework).


## <a name="general-requirements-and-limitations"></a><a name="bkmk_generalprerewq"></a> Общие требования и ограничения

Перечисленные ниже требования относятся ко всем серверам системы сайта.

- Каждый сервер системы сайта должен работать под управлением 64-разрядной ОС. Единственным исключением является роль системы сайта точки распространения, которую можно установить в некоторых 32-разрядных операционных системах.  

- Системы сайта не поддерживаются в установках основных серверных компонентов в любой операционной системе. Исключением является то, что установки основных серверных компонентов поддерживаются для роли системы сайта "Точка распространения". Дополнительные сведения см. в статье [Поддерживаемые операционные системы для серверов системы сайта Configuration Manager](supported-operating-systems-for-site-system-servers.md).  

- Не допускается изменение следующих параметров после установки сервера системы сайта.  

    - Имя домена, в котором находится компьютер системы сайта (**переименование домена**)  

    - Членство компьютера в домене  

    - Имя компьютера.  

    Если нужно изменить какие-либо из этих элементов, сначала удалите роль системы сайта с компьютера. Затем заново установите ее после внесения изменений. Если изменения влияют на сервер сайта, сначала удалите сайт. Затем заново установите его после внесения изменений.  

- Роли системы сайта не поддерживаются в экземпляре кластера Windows Server. Единственным исключением является сервер базы данных сайта. Дополнительные сведения см. в статье [Использование кластера SQL Server для базы данных сайта Configuration Manager](../../servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database.md).  

    Начиная с версии 1810 процесс установки Configuration Manager более не блокирует установку роли сервера сайта на компьютере с ролью Windows для отказоустойчивой кластеризации. Эта роль требуется для SQL Always On, в связи с чем ранее было невозможно размещать базу данных сайта на сервере сайта. Благодаря этому изменению вы можете создать сайт с высоким уровнем доступности с меньшим количеством серверов за счет использования SQL Always On и сервера сайта в пассивном режиме. Дополнительные сведения см. в статье [Способы обеспечения высокой доступности](../../servers/deploy/configure/high-availability-options.md). <!--3607761, fka 1359132-->  

- Не поддерживается изменение параметров "Тип запуска" и "Вход от имени" для любой службы Configuration Manager. Это может привести к неправильной работе ключевых служб.  

### <a name="prerequisites-for-windows-server-2012-and-later-operating-systems"></a><a name="bkmk_2012Prereq"></a> Необходимые компоненты для Windows Server 2012 и более поздних операционных систем  

Предварительные требования для определенных серверов и ролей системы сайта в Windows Server 2012 и более поздних версий см. в основных разделах этой статьи:

- [Серверы сайта центра администрирования и первичного сайта](#bkmk_2012sspreq)
- [Сервер вторичного сайта](#bkmk_2012secpreq)
- [Сервер базы данных](#bkmk_2012dbpreq)
- [Сервер поставщика SMS](#bkmk_2012smsprovpreq)
- [Точка веб-сайта каталога приложений](#bkmk_2012acwspreq)
- [Точка веб-службы каталога приложений](#bkmk_2012ACwsitepreq)
- [Точка синхронизации каталога аналитики активов](#bkmk_2012AIpreq)
- [Точка регистрации сертификатов](#bkmk_2012crppreq)
- [Точка распространения](#bkmk_2012dppreq)
- [Точка Endpoint Protection](#bkmk_2012EPPpreq)
- [Точка регистрации](#bkmk_2012Enrollpreq)
- [Прокси-точка регистрации](#bkmk_2012EnrollProxpreq)
- [Резервная точка состояния](#bkmk_2012FSPpreq)
- [Точка управления](#bkmk_2012MPpreq)
- [Точка служб отчетов](#bkmk_2012RSpoint)
- [Точка подключения службы](#bkmk_SCPpreq)
- [Точка обновления программного обеспечения](#bkmk_2012SUPpreq)
- [Точка миграции состояния](#bkmk_2012SMPpreq)

## <a name="central-administration-site-and-primary-site-servers"></a><a name="bkmk_2012sspreq"></a> Серверы сайта центра администрирования и первичного сайта

### <a name="windows-server-roles-and-features"></a>Роли и компоненты Windows Server

- .NET Framework 3.5

- Протокол удаленного разностного сжатия  

- При использовании точки обновления программного обеспечения на сервере, отличном от сервера сайта, установите консоль администрирования WSUS на сервере сайта.

### <a name="net-framework"></a>.NET Framework

Включите компонент Windows для .NET Framework 3.5.

Также установите поддерживаемую версию .NET Framework 4.5 или более позднюю. Начиная с версии 1906, Configuration Manager поддерживает .NET Framework 4.8.

Дополнительные сведения о версиях .NET Framework см. в следующих статьях:

- [Версии и зависимости платформы .NET Framework](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Вопросы и ответы: жизненный цикл .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="windows-adk"></a>Windows ADK  

- Перед установкой или обновлением сайта центра администрирования или первичного сайта установите версию комплекта средств для развертывания и оценки Windows (Windows ADK), которая требуется для устанавливаемой или обновляемой версии Configuration Manager. Дополнительные сведения см. на странице [Windows 10 ADK](support-for-windows-10.md#windows-10-adk).  

- Дополнительные сведения об этом требовании см. в статье [Требования к инфраструктуре для развертывания ОС](../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md).  

### <a name="visual-c-redistributable"></a>Распространяемый компонент Visual C++  

- Configuration Manager устанавливает распространяемый пакет Microsoft Visual C++ 2013 на каждый компьютер, на который устанавливается сервер сайта.  

- Сайты центра администрирования и первичные сайты требуют 32- и 64-разрядных версий применимого файла распространяемого компонента.  

### <a name="sql-server-native-client"></a>Собственный клиент SQL Server

При установке нового сайта Configuration Manager автоматически устанавливает SQL Server Native Client в качестве распространяемого компонента. После установки сайта Configuration Manager не обновляет SQL Server Native Client. Убедитесь, что компонент обновлен. Дополнительные сведения см. в разделе [Проверки готовности – SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="secondary-site-server"></a><a name="bkmk_2012secpreq"></a> Сервер вторичного сайта

### <a name="windows-server-roles-and-features"></a>Роли и компоненты Windows Server

- .NET Framework 3.5

- Протокол удаленного разностного сжатия  

### <a name="net-framework"></a>.NET Framework

Включите компонент Windows для .NET Framework 3.5.

Также установите поддерживаемую версию .NET Framework 4.5 или более позднюю. Начиная с версии 1906, Configuration Manager поддерживает .NET Framework 4.8.

Дополнительные сведения о версиях .NET Framework см. в следующих статьях:

- [Версии и зависимости платформы .NET Framework](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Вопросы и ответы: жизненный цикл .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="visual-c-redistributable"></a>Распространяемый компонент Visual C++

- Configuration Manager устанавливает распространяемый пакет Microsoft Visual C++ 2013 на каждый компьютер, на который устанавливается сервер сайта.  

- Вторичные сайты требуют только 64-разрядных версий.  

### <a name="default-site-system-roles"></a>Роли системы сайта по умолчанию  

- По умолчанию вторичный сайт устанавливает **точку управления** и **точку распространения**.  

- Убедитесь в том, что сервер вторичного сайта соответствует необходимым условиям для этих ролей системы сайта.  

### <a name="sql-server-native-client"></a>Собственный клиент SQL Server

При установке нового сайта Configuration Manager автоматически устанавливает SQL Server Native Client в качестве распространяемого компонента. После установки сайта Configuration Manager не обновляет SQL Server Native Client. Убедитесь, что компонент обновлен. Дополнительные сведения см. в разделе [Проверки готовности – SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="database-server"></a><a name="bkmk_2012dbpreq"></a> Сервер базы данных  

### <a name="remote-registry-service"></a>Служба удаленного реестра  

- Во время установки сайта Configuration Manager включите службу **удаленного реестра** на компьютере, на котором будет размещена база данных сайта.  

### <a name="sql-server"></a>SQL Server  

- Прежде чем устанавливать сайт центра администрирования или первичный сайт, установите поддерживаемую версию SQL Server для размещения базы данных сайта. Дополнительные сведения см. в разделе [Поддерживаемые версии SQL Server](support-for-sql-server-versions.md).  

- Перед установкой вторичного сайта можно установить поддерживаемую версию SQL Server.  

- Если вы хотите, чтобы Configuration Manager установил экспресс-выпуск SQL Server в рамках установки вторичного сайта, то компьютер должен соответствовать требованиям для запуска экспресс-выпуска SQL Server.  

### <a name="sql-server-native-client"></a>Собственный клиент SQL Server

При установке нового сайта Configuration Manager автоматически устанавливает SQL Server Native Client в качестве распространяемого компонента. После установки сайта Configuration Manager не обновляет SQL Server Native Client. Убедитесь, что компонент обновлен. Дополнительные сведения см. в разделе [Проверки готовности – SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="sms-provider-server"></a><a name="bkmk_2012smsprovpreq"></a> Сервер поставщика SMS  

### <a name="windows-adk"></a>Windows ADK

- На компьютере, на котором устанавливается экземпляр поставщика SMS, должна быть установлена версия Windows ADK, которая требуется для устанавливаемой или обновляемой версии Configuration Manager. Дополнительные сведения см. на странице [Windows 10 ADK](support-for-windows-10.md#windows-10-adk).  

- Дополнительные сведения об этом требовании см. в статье [Требования к инфраструктуре для развертывания операционной системы в System Center Configuration Manager](../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md).  

### <a name="windows-server-roles-and-features"></a>Роли и компоненты Windows Server

- Если вы используете [службу администрирования](../../../develop/adminservice/overview.md), серверу, на котором размещена роль поставщика SMS, требуется .NET 4.5 или более поздних версий.  <!-- SCCMDocs issue #1203 -->

    > [!NOTE]
    > Configuration Manager версии 1810 требует .NET 4.5.2 или более поздней версии.

- Веб-сервер (IIS): Каждый поставщик пытается установить [службу администрирования](../../../develop/adminservice/overview.md). Эта служба зависит от IIS для привязки сертификата к HTTPS-порту 443. Configuration Manager использует IIS API для проверки этой конфигурации сертификата. При настройке сайта для [улучшенного протокола HTTP](../hierarchy/enhanced-http.md) Configuration Manager использует IIS API для привязки сгенерированного сайтом сертификата. Начиная с версии 2002, сайт автоматически использует самозаверяющий сертификат сайта.

### <a name="sql-server-native-client"></a>Собственный клиент SQL Server

При установке нового сайта Configuration Manager автоматически устанавливает SQL Server Native Client в качестве распространяемого компонента. После установки сайта Configuration Manager не обновляет SQL Server Native Client. Убедитесь, что компонент обновлен. Дополнительные сведения см. в разделе [Проверки готовности – SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="application-catalog-website-point"></a><a name="bkmk_2012acwspreq"></a> Точка веб-сайта каталога приложений  

> [!Important]  
> Пользовательский интерфейс Silverlight каталога приложений не поддерживается в текущей ветви версии 1806. Начиная с версии 1906, обновленные клиенты автоматически используют точку управления для развертываний приложений, доступных пользователю. Но вы не можете устанавливать новые роли каталога приложений. Поддержка ролей каталога приложений прекращена в версии 1910.  
>
> Дополнительные сведения см. в следующих статьях:
>
> - [Настройка центра программного обеспечения](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Удаленные и устаревшие компоненты](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

### <a name="windows-server-roles-and-features"></a>Роли и компоненты Windows Server

- .NET Framework 3.5

- ASP.NET 4.5  

### <a name="net-framework"></a>.NET Framework

Включите компонент Windows для .NET Framework 3.5.

Также установите поддерживаемую версию .NET Framework 4.5 или более позднюю.

Дополнительные сведения о версиях .NET Framework см. в следующих статьях:

- [Версии и зависимости платформы .NET Framework](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Вопросы и ответы: жизненный цикл .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>Конфигурация служб IIS  

- Общие компоненты HTTP:  

    - Документ по умолчанию  

    - Статическое содержимое  

- Разработка приложения.  

    - ASP.NET 3.5 (и автоматически выбранные параметры)  

    - ASP.NET 4.5 (и автоматически выбранные параметры)  

    - Расширяемость .NET 3.5  

    - Расширяемость .NET 4.5  

- Безопасность:  

    - Проверка подлинности Windows  

- Совместимость управления IIS 6.  

    - Совместимость метабазы IIS 6  


## <a name="application-catalog-web-service-point"></a><a name="bkmk_2012ACwsitepreq"></a> Точка веб-службы каталога приложений  

> [!Important]  
> Пользовательский интерфейс Silverlight каталога приложений не поддерживается в текущей ветви версии 1806. Начиная с версии 1906, обновленные клиенты автоматически используют точку управления для развертываний приложений, доступных пользователю. Но вы не можете устанавливать новые роли каталога приложений. Поддержка ролей каталога приложений прекращена в версии 1910.  
>
> Дополнительные сведения см. в следующих статьях:
>
> - [Настройка центра программного обеспечения](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Удаленные и устаревшие компоненты](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

### <a name="windows-server-roles-and-features"></a>Роли и компоненты Windows Server

- .NET Framework 3.5

- ASP.NET 4.5:  

    - Активация HTTP (и автоматически выбранные параметры)  

### <a name="net-framework"></a>.NET Framework

Включите компонент Windows для .NET Framework 3.5.

Также установите поддерживаемую версию .NET Framework 4.5 или более позднюю.

Дополнительные сведения о версиях .NET Framework см. в следующих статьях:

- [Версии и зависимости платформы .NET Framework](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Вопросы и ответы: жизненный цикл .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>Конфигурация служб IIS

- Общие компоненты HTTP:  

    - Документ по умолчанию  

- Совместимость управления IIS 6.  

    - Совместимость метабазы IIS 6  

- Разработка приложений:  

    - ASP.NET 3.5 (и автоматически выбранные параметры)  

    - Расширяемость .NET 3.5  

    - ASP.NET 4.5 (и автоматически выбранные параметры)  

    - Расширяемость .NET 4.5  

### <a name="computer-memory"></a>Объем памяти компьютера  

- На компьютере, на котором размещена эта роль системы сайта, должно быть свободно не менее 5 % доступной памяти для того, чтобы роль системы сайта могла обрабатывать запросы.  

- Если эта роль системы сайта расположена на том же компьютере, что и другая роль системы сайта с таким же требованием к памяти, общее требование к памяти на компьютере не увеличивается, а остается таким же — минимум 5 %.  

### <a name="sql-server-native-client"></a>Собственный клиент SQL Server

При установке нового сайта Configuration Manager автоматически устанавливает SQL Server Native Client в качестве распространяемого компонента. После установки сайта Configuration Manager не обновляет SQL Server Native Client. Убедитесь, что компонент обновлен. Дополнительные сведения см. в разделе [Проверки готовности – SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="asset-intelligence-synchronization-point"></a><a name="bkmk_2012AIpreq"></a> Точка синхронизации каталога аналитики активов  

### <a name="net-framework"></a>.NET Framework

Установите поддерживаемую версию .NET Framework 4.5 или более позднюю. Начиная с версии 1906, Configuration Manager поддерживает .NET Framework 4.8.

Дополнительные сведения о версиях .NET Framework см. в следующих статьях:

- [Версии и зависимости платформы .NET Framework](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Вопросы и ответы: жизненный цикл .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="sql-server-native-client"></a>Собственный клиент SQL Server

При установке нового сайта Configuration Manager автоматически устанавливает SQL Server Native Client в качестве распространяемого компонента. После установки сайта Configuration Manager не обновляет SQL Server Native Client. Убедитесь, что компонент обновлен. Дополнительные сведения см. в разделе [Проверки готовности – SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="certificate-registration-point"></a><a name="bkmk_2012crppreq"></a> Точка регистрации сертификатов  

### <a name="windows-server-roles-and-features"></a>Роли и компоненты Windows Server

- .NET Framework

    - Активация по протоколам HTTP  

### <a name="net-framework"></a>.NET Framework

Установите поддерживаемую версию .NET Framework 4.5 или более позднюю. Начиная с версии 1906, Configuration Manager поддерживает .NET Framework 4.8.

Дополнительные сведения о версиях .NET Framework см. в следующих статьях:

- [Версии и зависимости платформы .NET Framework](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Вопросы и ответы: жизненный цикл .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>Конфигурация служб IIS

- Разработка приложений:  

    - ASP.NET 3.5 (и автоматически выбранные параметры)  

    - ASP.NET 4.5 (и автоматически выбранные параметры)  

- Совместимость управления IIS 6.  

    - Совместимость метабазы IIS 6  

    - Совместимость с WMI IIS 6  

### <a name="sql-server-native-client"></a>Собственный клиент SQL Server

При установке нового сайта Configuration Manager автоматически устанавливает SQL Server Native Client в качестве распространяемого компонента. После установки сайта Configuration Manager не обновляет SQL Server Native Client. Убедитесь, что компонент обновлен. Дополнительные сведения см. в разделе [Проверки готовности – SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="distribution-point"></a><a name="bkmk_2012dppreq"></a> Точка распространения  

### <a name="windows-server-roles-and-features"></a>Роли и компоненты Windows Server

- Протокол удаленного разностного сжатия  

#### <a name="iis-configuration"></a>Конфигурация служб IIS

- Разработка приложений:  

    - Расширения ISAPI  

- Безопасность:  

    - Проверка подлинности Windows  

- Совместимость управления IIS 6.  

    - Совместимость метабазы IIS 6  

    - Совместимость с WMI IIS 6  

### <a name="powershell"></a>PowerShell  

- До установки точки распространения на сервере Windows Server 2012 или более поздней версии требуется PowerShell 3.0 или 4.0.  

### <a name="visual-c-redistributable"></a>Распространяемый компонент Visual C++

- Configuration Manager устанавливает распространяемый пакет Microsoft Visual C++ 2013 на каждый компьютер, на котором размещается точка распространения.  

- Устанавливаемая версия зависит от платформы компьютера (x86 или x64).  

### <a name="microsoft-azure"></a>Microsoft Azure  

- Для размещения точки распространения можно воспользоваться облачной службой Microsoft Azure.  

### <a name="to-support-pxe-or-multicast"></a>Поддержка PXE или многоадресной рассылки  

- Включите ответчик PXE в точке распространения без службы развертывания Windows.  

- Установите и настройте роль Windows Server "Службы развертывания Windows (WDS)".  

    > [!NOTE]  
    > Службы развертывания Windows устанавливаются и настраиваются автоматически при настройке точки распространения для поддержки PXE или многоадресной рассылки на сервере Windows Server 2012 или более поздней версии.  

- Убедитесь, что установлен и актуализирован клиент SQL Server Native Client для точки распространения с поддержкой многоадресной рассылки. Дополнительные сведения см. в разделе [Проверки готовности – SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).

Дополнительные сведения см. в разделе [Установка и настройка точек распространения](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe).

<!--sms.503672 -Clarified BITS use-->
> [!NOTE]  
> Точка распространения передает содержимое с помощью **фоновой интеллектуальной службы передачи** (BITS), встроенной в Windows. Роль точки распространения не требует устанавливать дополнительный компонент расширения сервера IIS BITS, так как клиент не передает сведения в него.  


## <a name="endpoint-protection-point"></a><a name="bkmk_2012EPPpreq"></a> Точка Endpoint Protection  

### <a name="windows-server-roles-and-features"></a>Роли и компоненты Windows Server  

- .NET Framework 3.5

- Компоненты Защитника Windows (Windows Server 2016 или более поздней версии)  

### <a name="sql-server-native-client"></a>Собственный клиент SQL Server

При установке нового сайта Configuration Manager автоматически устанавливает SQL Server Native Client в качестве распространяемого компонента. После установки сайта Configuration Manager не обновляет SQL Server Native Client. Убедитесь, что компонент обновлен. Дополнительные сведения см. в разделе [Проверки готовности – SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="enrollment-point"></a><a name="bkmk_2012Enrollpreq"></a> Точка регистрации  

### <a name="windows-server-roles-and-features"></a>Роли и компоненты Windows Server

- .NET Framework 3.5

    - Активация HTTP (и автоматически выбранные параметры)  

    - ASP.NET 4.5  

    - Службы Windows Communication Foundation<!-- SCCMDocs issue #1168 -->  

### <a name="net-framework"></a>.NET Framework

Включите компонент Windows для .NET Framework 3.5.

Также установите поддерживаемую версию .NET Framework 4.5 или более позднюю. Начиная с версии 1906, Configuration Manager поддерживает .NET Framework 4.8.

> [!Note]
> При установке этой роли системы сайта Configuration Manager автоматически устанавливает платформу .NET Framework 4.5.2. Эта установка может перевести сервер в состояние ожидания перезагрузки. Если ожидается перезагрузка для .NET Framework, то приложения .NET могут завершаться сбоем, пока сервер не выполнит перезагрузку и не завершит установку.  

Дополнительные сведения о версиях .NET Framework см. в следующих статьях:

- [Версии и зависимости платформы .NET Framework](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Вопросы и ответы: жизненный цикл .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>Конфигурация служб IIS

- Общие компоненты HTTP:  

    - Документ по умолчанию  

- Разработка приложений:  

    - ASP.NET 3.5 (и автоматически выбранные параметры)  

    - Расширяемость .NET 3.5  

    - ASP.NET 4.5 (и автоматически выбранные параметры)  

    - Расширяемость .NET 4.5  

- Совместимость управления IIS 6.  

    - Совместимость метабазы IIS 6  

### <a name="computer-memory"></a>Объем памяти компьютера

- На компьютере, на котором размещена эта роль системы сайта, должно быть свободно не менее 5 % доступной памяти для того, чтобы роль системы сайта могла обрабатывать запросы.  

- Если эта роль системы сайта расположена на том же компьютере, что и другая роль системы сайта с таким же требованием к памяти, общее требование к памяти на компьютере не увеличивается, а остается таким же — минимум 5 %.  

### <a name="sql-server-native-client"></a>Собственный клиент SQL Server

При установке нового сайта Configuration Manager автоматически устанавливает SQL Server Native Client в качестве распространяемого компонента. После установки сайта Configuration Manager не обновляет SQL Server Native Client. Убедитесь, что компонент обновлен. Дополнительные сведения см. в разделе [Проверки готовности – SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="enrollment-proxy-point"></a><a name="bkmk_2012EnrollProxpreq"></a> Прокси-точка регистрации  

### <a name="windows-server-roles-and-features"></a>Роли и компоненты Windows Server

- .NET Framework 3.5

### <a name="net-framework"></a>.NET Framework

Включите компонент Windows для .NET Framework 3.5.

Также установите поддерживаемую версию .NET Framework 4.5 или более позднюю. Начиная с версии 1906, Configuration Manager поддерживает .NET Framework 4.8.

> [!Note]
> При установке этой роли системы сайта Configuration Manager автоматически устанавливает платформу .NET Framework 4.5.2. Эта установка может перевести сервер в состояние ожидания перезагрузки. Если ожидается перезагрузка для .NET Framework, то приложения .NET могут завершаться сбоем, пока сервер не выполнит перезагрузку и не завершит установку.  

Дополнительные сведения о версиях .NET Framework см. в следующих статьях:

- [Версии и зависимости платформы .NET Framework](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Вопросы и ответы: жизненный цикл .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>Конфигурация служб IIS

- Общие компоненты HTTP:  

    - Документ по умолчанию  

    - Статическое содержимое  

- Разработка приложения.  

    - ASP.NET 3.5 (и автоматически выбранные параметры)  

    - ASP.NET 4.5 (и автоматически выбранные параметры)  

    - Расширяемость .NET 3.5  

    - Расширяемость .NET 4.5  

- Безопасность:  

    - Проверка подлинности Windows  

- Совместимость управления IIS 6.  

    - Совместимость метабазы IIS 6  

### <a name="computer-memory"></a>Объем памяти компьютера

- На компьютере, на котором размещена эта роль системы сайта, должно быть свободно не менее 5 % доступной памяти для того, чтобы роль системы сайта могла обрабатывать запросы.  

- Если эта роль системы сайта расположена на том же компьютере, что и другая роль системы сайта с таким же требованием к памяти, общее требование к памяти на компьютере не увеличивается, а остается таким же — минимум 5 %.  


## <a name="fallback-status-point"></a><a name="bkmk_2012FSPpreq"></a> Резервная точка состояния

### <a name="windows-server-roles-and-features"></a>Роли и компоненты Windows Server

- Серверные расширения BITS (и автоматически выбранные параметры) или фоновые интеллектуальные службы передачи (BITS) (и автоматически выбранные параметры)

#### <a name="iis-configuration"></a>Конфигурация служб IIS

Требуется конфигурация IIS по умолчанию со следующими дополнениями:  

- Совместимость управления IIS 6.  

    - Совместимость метабазы IIS 6  


## <a name="management-point"></a><a name="bkmk_2012MPpreq"></a> Точка управления  

### <a name="windows-server-roles-and-features"></a>Роли и компоненты Windows Server

- Серверные расширения BITS (и автоматически выбранные параметры) или фоновые интеллектуальные службы передачи (BITS) (и автоматически выбранные параметры)  

### <a name="net-framework"></a>.NET Framework

Установите поддерживаемую версию .NET Framework 4.5 или более позднюю. Начиная с версии 1906, Configuration Manager поддерживает .NET Framework 4.8.

Дополнительные сведения о версиях .NET Framework см. в следующих статьях:

- [Версии и зависимости платформы .NET Framework](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Вопросы и ответы: жизненный цикл .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>Конфигурация служб IIS

- Разработка приложений:  

    - Расширения ISAPI  

- Безопасность:  

    - Проверка подлинности Windows  

- Совместимость управления IIS 6.  

    - Совместимость метабазы IIS 6  

    - Совместимость с WMI IIS 6  

### <a name="sql-server-native-client"></a>Собственный клиент SQL Server

При установке нового сайта Configuration Manager автоматически устанавливает SQL Server Native Client в качестве распространяемого компонента. После установки сайта Configuration Manager не обновляет SQL Server Native Client. Убедитесь, что компонент обновлен. Дополнительные сведения см. в разделе [Проверки готовности – SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="reporting-services-point"></a><a name="bkmk_2012RSpoint"></a> Точка служб отчетов  

### <a name="net-framework"></a>.NET Framework

Установите поддерживаемую версию .NET Framework 4.5 или более позднюю. Начиная с версии 1906, Configuration Manager поддерживает .NET Framework 4.8.

Дополнительные сведения о версиях .NET Framework см. в следующих статьях:

- [Версии и зависимости платформы .NET Framework](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Вопросы и ответы: жизненный цикл .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="sql-server-reporting-services"></a>Службы SQL Server Reporting Services  

- Перед установкой точки формирования отчетов установите и настройте по крайней мере один экземпляр SQL Server для поддержки служб SQL Server Reporting Services.  

- Для служб SQL Server Reporting Services можно использовать тот же самый экземпляр, что и для базы данных сайта.  

- Кроме того, применяемый экземпляр можно использовать совместно с другими продуктами System Center при условии, что они не имеют ограничений на совместное использование экземпляра SQL Server.  

### <a name="sql-server-native-client"></a>Собственный клиент SQL Server

При установке нового сайта Configuration Manager автоматически устанавливает SQL Server Native Client в качестве распространяемого компонента. После установки сайта Configuration Manager не обновляет SQL Server Native Client. Убедитесь, что компонент обновлен. Дополнительные сведения см. в разделе [Проверки готовности – SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="service-connection-point"></a><a name="bkmk_SCPpreq"></a> Точка подключения службы  

### <a name="net-framework"></a>.NET Framework

Включите компонент Windows для .NET Framework 3.5.

Также установите поддерживаемую версию .NET Framework 4.5 или более позднюю. Начиная с версии 1906, Configuration Manager поддерживает .NET Framework 4.8.

> [!Note]
> При установке этой роли системы сайта Configuration Manager автоматически устанавливает платформу .NET Framework 4.5.2. Эта установка может перевести сервер в состояние ожидания перезагрузки. Если ожидается перезагрузка для .NET Framework, то приложения .NET могут завершаться сбоем, пока сервер не выполнит перезагрузку и не завершит установку.  

Дополнительные сведения о версиях .NET Framework см. в следующих статьях:

- [Версии и зависимости платформы .NET Framework](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Вопросы и ответы: жизненный цикл .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="visual-c-redistributable"></a>Распространяемый компонент Visual C++

- Configuration Manager устанавливает распространяемый пакет Microsoft Visual C++ 2013 на каждый компьютер, на котором размещается точка распространения.  

- Для роли системы сайта требуется версия x64.  

### <a name="sql-server-native-client"></a>Собственный клиент SQL Server

При установке нового сайта Configuration Manager автоматически устанавливает SQL Server Native Client в качестве распространяемого компонента. После установки сайта Configuration Manager не обновляет SQL Server Native Client. Убедитесь, что компонент обновлен. Дополнительные сведения см. в разделе [Проверки готовности – SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="software-update-point"></a><a name="bkmk_2012SUPpreq"></a> Точка обновления программного обеспечения  

### <a name="windows-server-roles-and-features"></a>Роли и компоненты Windows Server

- .NET Framework 3.5

Требуется конфигурация IIS по умолчанию.

### <a name="net-framework"></a>.NET Framework

Включите компонент Windows для .NET Framework 3.5.

Также установите поддерживаемую версию .NET Framework 4.5 или более позднюю. Начиная с версии 1906, Configuration Manager поддерживает .NET Framework 4.8.

Дополнительные сведения о версиях .NET Framework см. в следующих статьях:

- [Версии и зависимости платформы .NET Framework](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Вопросы и ответы: жизненный цикл .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="windows-server-update-services"></a>Службы WSUS  

- Перед установкой точки обновления программного обеспечения установите роль Windows Server "Windows Server Update Services".  

- Дополнительные сведения см. в статье [Планирование обновлений программного обеспечения](../../../sum/plan-design/plan-for-software-updates.md).  

> [!NOTE]  
> При использовании точки обновления программного обеспечения на сервере, отличном от сервера сайта, необходимо установить консоль администрирования WSUS на сервере сайта.

### <a name="sql-server-native-client"></a>Собственный клиент SQL Server

При установке нового сайта Configuration Manager автоматически устанавливает SQL Server Native Client в качестве распространяемого компонента. После установки сайта Configuration Manager не обновляет SQL Server Native Client. Убедитесь, что компонент обновлен. Дополнительные сведения см. в разделе [Проверки готовности – SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="state-migration-point"></a><a name="bkmk_2012SMPpreq"></a> Точка миграции среды

<!--SCCMDocs issue 645-->
### <a name="windows-server-roles-and-features"></a>Роли и компоненты Windows Server

- .NET Framework 3.5

    - Активация HTTP (и автоматически выбранные параметры)  

    - ASP.NET 4.5  

### <a name="net-framework"></a>.NET Framework

Включите компонент Windows для .NET Framework 3.5.

Также установите поддерживаемую версию .NET Framework 4.5 или более позднюю. Начиная с версии 1906, Configuration Manager поддерживает .NET Framework 4.8.

> [!Note]
> При установке этой роли системы сайта Configuration Manager автоматически устанавливает платформу .NET Framework 4.5.2. Эта установка может перевести сервер в состояние ожидания перезагрузки. Если ожидается перезагрузка для .NET Framework, то приложения .NET могут завершаться сбоем, пока сервер не выполнит перезагрузку и не завершит установку.  

Дополнительные сведения о версиях .NET Framework см. в следующих статьях:

- [Версии и зависимости платформы .NET Framework](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Вопросы и ответы: жизненный цикл .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>Конфигурация служб IIS

- Общие компоненты HTTP:  

    - Документ по умолчанию  

- Разработка приложений:  

    - ASP.NET 3.5 (и автоматически выбранные параметры)  

    - Расширяемость .NET 3.5  

    - ASP.NET 4.5 (и автоматически выбранные параметры)  

    - Расширяемость .NET 4.5  

- Совместимость управления IIS 6.  

    - Совместимость метабазы IIS 6  

### <a name="sql-server-native-client"></a>Собственный клиент SQL Server

При установке нового сайта Configuration Manager автоматически устанавливает SQL Server Native Client в качестве распространяемого компонента. После установки сайта Configuration Manager не обновляет SQL Server Native Client. Убедитесь, что компонент обновлен. Дополнительные сведения см. в разделе [Проверки готовности – SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).

