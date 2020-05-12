---
title: 'Поддерживаемые конфигурации для LTSB '
titleSuffix: Configuration Manager
description: Сведения об операционных системах и зависимых продуктах, которые работают с System Center Configuration Manager (Long-Term Servicing Branch).
ms.date: 05/10/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f0f818d4-7f45-402f-8758-dc88bc024953
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7de7d562131f97ac21d1c394b176d3b7f4ce7747
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906441"
---
# <a name="supported-configurations-for-the-long-term-servicing-branch-of-system-center-configuration-manager"></a>Поддерживаемые конфигурации для System Center Configuration Manager (Long-Term Servicing Branch)

*Область применения: System Center Configuration Manager: Long-Term Servicing Branch*

Сведения в этом разделе помогут вам понять, какие операционные системы и зависимые продукты поддерживаются версией Long-Term Servicing Branch (LTSB) Configuration Manager.
Если в этих разделах, посвященных LTSB, не указано иное, для LTSB действуют те же конфигурации и ограничения, что и для Current Branch версии 1606.  При возникновении противоречий используйте сведения, относящиеся к применяемому выпуску. Как правило, версия LTSB более ограничена по сравнению с Current Branch.

## <a name="general-statement-of-support"></a>Общее заявление о поддержке
Эта ветвь Configuration Manager поддерживает следующие продукты и технологии. Учтите, что их перечисление здесь не означает расширение поддержки этих продуктов или версий за пределами индивидуальных жизненных циклов поддержки. Продукты, жизненный цикл поддержки которых уже истек, не поддерживаются в Configuration Manager. Дополнительные сведения см. на веб-сайте [Политика жизненного цикла поддержки Майкрософт](https://support.microsoft.com/lifecycle) и в разделе часто задаваемых вопросов об этой политике.

Кроме того, продукты и версии продуктов, которые не указаны в следующих разделах, не поддерживаются, если только иное не указано в [блоге рабочей группы по корпоративной мобильности и безопасности](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/bg-p/enterprisemobilityandsecurity).

**Ограничения в отношении поддержки будущих продуктов**. В LTSB ограничена поддержка будущих серверных и клиентских операционных систем, а также зависимых продуктов. Список платформ для LTSB является фиксированным в течение жизненного цикла выпуска.

**Windows:**
- Поддерживаются только исправления и обновления для системы безопасности Windows.
- Отсутствует поддержка версий Current Branch (CB), Current Branch for Business (CBB) и LTSB Windows 10.
- Отсутствует поддержка новых основных версий Windows Server.

**SQL Server:**
- Для SQL Server поддерживаются только исправления, обновления для системы безопасности и промежуточные обновления, такие как пакеты обновления.
- Отсутствует поддержка новых основных версий SQL Server.  

## <a name="site-systems-and-servers"></a>Системы сайта и серверы
LTSB поддерживает использование следующих операционных систем Windows в качестве систем сайта.  Для каждой операционной системы действуют требования и ограничения, указанные в соответствующем месте в разделе [Поддерживаемые операционные системы для серверов системы сайта](../plan-design/configs/supported-operating-systems-for-site-system-servers.md).  Например, установка основных серверных компонентов Windows 2012 R2 должна быть 64-разрядной, она поддерживает размещение только точки распространения и не поддерживает PXE и многоадресную рассылку.

**Поддерживаемые операционные системы:**
- Windows Server 2016
- Windows Server 2012 R2 (x64): Standard, Datacenter
- Windows Server 2012 (x64): Standard, Datacenter
- Windows 10 Корпоративная 2015 LTSB (x86, x64)
- Windows 10 Корпоративная 2016 LTSB (x86, x64)
- Windows 8.1 (x86, x64): Professional и Enterprise
- Windows Server 2012, вариант установки основных серверных компонентов
- Windows Server 2012 R2, вариант установки основных серверных компонентов

## <a name="client-management"></a>Управление клиентами
В следующих разделах описываются клиентские операционные системы, которыми можно управлять с помощью LTSB. LTSB не поддерживает добавление новых операционных систем в качестве поддерживаемых клиентов.

### <a name="windows-computers"></a>Компьютеры Windows
LTSB можно использовать для управления перечисленными ниже операционными системами Windows с клиентским программным обеспечением Configuration Manager, которое входит в состав Configuration Manager. Дополнительные сведения см. в статье [Развертывание клиентов на компьютерах Windows в Configuration Manager](../clients/deploy/deploy-clients-to-windows-computers.md).

**Поддерживаемые операционные системы:**
- Windows Server 2016
- Windows Server 2012 R2 (x64): Standard, Datacenter (примечание 1)
- Windows Server 2012 (x64): Standard, Datacenter (примечание 1)
- Windows Storage Server 2012 R2 (x64)
- Windows Storage Server 2012 (x64)
- Windows 10 Корпоративная 2015 LTSB (x86, x64)
- Windows 10 Корпоративная 2016 LTSB (x86, x64)
- Windows 8.1 (x86, x64): Professional и Enterprise
- Windows Server 2012 R2, вариант установки основных серверных компонентов (x64) (примечание 2)
- Windows Server 2012, вариант установки основных серверных компонентов (x64) (примечание 2)

**Примечание 1.** Выпуски Datacenter поддерживаются, но не сертифицированы для Configuration Manager.  
**Примечание 2.** Чтобы поддерживать принудительную установку клиента, на компьютере под управлением этой версии операционной системы должна быть запущена служба роли файлового сервера для ролей файлового сервера и сервера служб хранилища. Сведения об установке компонентов Windows на компьютере основных серверных компонентов см. в разделе [Установка ролей и компонентов сервера на компьютере основных серверных компонентов](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj574158(v=ws.11)).

### <a name="windows-embedded"></a>Windows Embedded
С помощью LTSB можно управлять перечисленными ниже устройствами Windows Embedded, установив на устройстве клиентское программное обеспечение.  Дополнительные сведения см. в статье [Планирование развертывания клиентов на устройствах Windows Embedded в System Center Configuration Manager](../clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).

**Требования и ограничения**  

-   На поддерживаемых системах Windows Embedded, для которых не включены фильтры записи, поддерживаются все клиентские компоненты.  

-   Клиенты, использующие один из следующих типов фильтров, поддерживаются для всех компонентов, кроме управления питанием:  

    -   Расширенный фильтр записи (EWF)    

    -   Файловый фильтр записи (FBWF) ОЗУ    

    -   Объединенный фильтр записи (UWF)  

-   Каталог приложений не поддерживается ни одним устройством Windows Embedded.  

-   Чтобы иметь возможность отслеживать обнаруженные вредоносные программы на устройствах Windows Embedded на базе Windows XP, необходимо установить пакет сценариев Microsoft Windows WMI на встроенное устройство. Для установки данного пакета используйте конструктор Windows Embedded Target Designer. Чтобы обеспечить формирование отчетов об обнаруженных вредоносных программах, необходимы файлы *WBEMDISP.DLL* и *WBEMDISP.TLB*, которые следует зарегистрировать в папке %windir%\System32\WBEM на устройстве Windows Embedded.  

**Поддерживаемые операционные системы:**  
-   Windows 10 Корпоративная 2016 LTSB (x86, x64)  
-   Windows 10 Корпоративная 2015 LTSB (x86, x64)  
-   Windows Embedded 8.1 Industry (x86, x64)    
-   Windows Thin PC (x86, x64)    
-   Windows Embedded POSReady 7 (x86, x64)    
-   Windows Embedded Standard 7 с пакетом обновления 1 (SP1) (x86, x64)    
-   Windows Embedded POSReady 2009 (x86)   
-   Windows Embedded Standard 2009 (x86)  

### <a name="windows-ce"></a>Windows CE  
 Можно управлять устройствами Windows CE с устаревшим клиентом Configuration Manager для мобильных устройств, который входит в состав Configuration Manager.  

**Требования и ограничения**  

-   Клиенту мобильного устройства требуется 0,78 МБ дискового пространства для установки клиента. Для входа в систему на мобильном устройстве может потребоваться до 256 КБ дополнительного пространства.    

-   Возможности таких мобильных устройств зависят от платформы и типа клиента. Сведения о функциях управления Configuration Manager, поддерживаемых для устаревшего клиента для мобильных устройств, см. в разделе [Выбор решения для управления устройствами Configuration Manager](../plan-design/choose-a-device-management-solution.md).  

**Поддерживаемые операционные системы:**  

-   Windows CE 7.0 (процессоры ARM и x86)  

**Поддерживаемые языки:**  
-   Китайский (упрощенное и традиционное письмо)    
-   Английский (США)    
-   Французский (Франция)    
-   Немецкий    
-   Итальянский    
-   Японский  
-   Корейский  
-   Португальский (Бразилия)  
-   Русский  
-   Испанский (Испания)  

### <a name="mac-computers"></a>Компьютеры Mac  
 С помощью LTSB можно управлять компьютерами Mac OS X с использованием клиента Configuration Manager для Mac.

Пакет установки клиента Mac не поставляется с носителем Configuration Manager. Можно скачать его вместе с компонентом "Клиенты для дополнительных операционных систем" из [Центра загрузки Майкрософт](https://www.microsoft.com/download/details.aspx?id=47719).  

Поддержка операционных систем Mac ограничена перечисленными в этом разделе. Она не охватывает дополнительные операционные системы, которые могут поддерживаться в будущем обновлении установочных пакетов клиента Mac для Current Branch.

Дополнительные сведения см. в статье [How to deploy clients to Macs](../clients/deploy/deploy-clients-to-macs.md) (Развертывание клиентов на компьютерах Mac).

**Поддерживаемые версии:**  
-   Mac OS X 10.9 (Mavericks)  
-   Mac OS X 10.10 (Yosemite)  
-   Mac OS X 10.11 (El Capitan)  

## <a name="linux-and-unix-servers"></a>Серверы Linux и UNIX
С помощью LTSB вы можете управлять серверами Linux и UNIX с использованием клиента Configuration Manager для Linux и UNIX.

Пакеты установки клиента Linux и UNIX не поставляются с носителем Configuration Manager. Можно скачать их вместе с компонентом "Клиенты для дополнительных операционных систем" из [Центра загрузки Майкрософт](https://www.microsoft.com/download/details.aspx?id=47719). Помимо пакетов установки клиента скачиваемые файлы содержат сценарий установки, который управляет установкой клиента на каждом компьютере.

Поддержка операционных систем Linux и UNIX ограничена описанными в этом разделе. Она не охватывает дополнительные операционные системы, которые могут поддерживаться в будущем обновлении установочных пакетов клиента Linux и UNIX для Current Branch.

**Требования и ограничения**  

-   Сведения о зависимостях файла операционной системы для клиента Linux и UNIX можно найти в разделе [Необходимые условия для развертывания клиентов на серверах Linux и UNIX](../clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_ClientDeployPrereqforLnU).  
-   Обзор возможностей управления, поддерживаемых для компьютеров UNIX или Linux, см. в разделе [Развертывание клиентов на серверах UNIX и Linux](../clients/deploy/deploy-clients-to-unix-and-linux-servers.md).  
-   Для поддерживаемых версий Linux и UNIX список версий включает в себя все последующие промежуточные версии. Например, если указана поддержка CentOS версии 6, это означает, что поддерживаются также все последующие промежуточные версии CentOS 6, например CentOS 6.3. Аналогично если указана поддержка операционной системы, у которой есть пакеты обновления, например SUSE Linux Enterprise Server 11 с пакетом обновления 1 (SP1), то поддерживаются также последующие пакеты обновления для этой операционной системы.
-   Сведения о пакетах установки клиента и универсальном агенте см. в статье [Развертывание клиентов на серверах UNIX и Linux в System Center Configuration Manager](../clients/deploy/deploy-clients-to-unix-and-linux-servers.md).


**Поддерживаемые версии:**    
Перечисленные ниже версии поддерживаются с помощью указанного TAR-файла.  
### <a name="aix"></a>AIX  

|Версия|Файл|  
|-|-|  
|Версия 5.3 (Power)|ccm-Aix53ppc.&lt;сборка\>.tar|  
|Версия 6.1 (Power)|ccm-Aix61ppc.&lt;сборка\>.tar|  
|Версия 7.1 (Power)|ccm-Aix71ppc.&lt;сборка\>.tar|  

### <a name="centos"></a>CentOS  

|Версия|Файл|  
|-|-|  
|Версия 5 x86|ccm-Universalx86.&lt;сборка\>.tar|  
|Версия 5 x64|ccm-Universalx64.&lt;сборка\>.tar|  
|Версия 6 x86|ccm-Universalx86.&lt;сборка\>.tar|  
|Версия 6 x64|ccm-Universalx64.&lt;сборка\>.tar|  
|Версия 7 x64|ccm-Universalx64.&lt;сборка\>.tar|  

### <a name="debian"></a>Debian  

|Версия|Файл|    
|-|-|  
|Версия 5 x86|ccm-Universalx86.&lt;сборка\>.tar|  
|Версия 5 x64|ccm-Universalx64.&lt;сборка\>.tar|  
|Версия 6x86|ccm-Universalx86.&lt;сборка\>.tar|  
|Версия 6 x64|ccm-Universalx64.&lt;сборка\>.tar|  
|Версия 7 x86|ccm-Universalx86.&lt;сборка\>.tar|  
|Версия 7 x64|ccm-Universalx64.&lt;сборка\>.tar|  
|Версия 8 x86|ccm-Universalx86.&lt;сборка\>.tar|  
|Версия 8 x64|ccm-Universalx64.&lt;сборка\>.tar|  

### <a name="hp-ux"></a>HP-UX  

|Версия|Файл|  
|-|-|  
|Версия 11iv2 IA64|ccm-HpuxB.11.23i64.&lt;сборка\>.tar|  
|Версия 11iv2 PA-RISC|ccm-HpuxB.11.23PA.&lt;сборка\>.tar|  
|Версия 11iv3 IA64|ccm-HpuxB.11.31i64.&lt;сборка\>.tar|  
|Версия 11iv3 PA-RISC|ccm-HpuxB.11.31PA.&lt;сборка\>.tar|  

### <a name="oracle-linux"></a>Oracle Linux  

|Версия|Файл|    
|-|-|  
|Версия 5 x86|ccm-Universalx86.&lt;сборка\>.tar|  
|Версия 5 x64|ccm-Universalx64.&lt;сборка\>.tar|  
|Версия 6 x86|ccm-Universalx86.&lt;сборка\>.tar|  
|Версия 6 x64|ccm-Universalx64.&lt;сборка\>.tar|  
|Версия 7 x64|ccm-Universalx64.&lt;сборка\>.tar|  

### <a name="red-hat-enterprise-linux-rhel"></a>Red Hat Enterprise Linux (RHEL)  

|Версия|Файл|  
|-|-|  
|Версия 4 x86|ccm-RHEL4x86.&lt;сборка\>.tar|  
|Версия 4 x64|ccm-RHEL4x64.&lt;сборка\>.tar|  
|Версия 5 x86|ccm-Universalx86.&lt;сборка\>.tar|  
|Версия 5 x64|ccm-Universalx64.&lt;сборка\>.tar|  
|Версия 6 x86|ccm-Universalx86.&lt;сборка\>.tar|  
|Версия 6 x64|ccm-Universalx64.&lt;сборка\>.tar|  
|Версия 7 x64|ccm-Universalx64.&lt;сборка\>.tar|  

### <a name="solaris"></a>Solaris  

|Версия|Файл|   
|-|-|  
|Версия 9 SPARC|ccm-Sol9sparc.&lt;сборка\>.tar|  
|Версия 10 x86|ccm-Sol10x86.&lt;сборка\>.tar|  
|Версия 10 SPARC|ccm-Sol10sparc.&lt;сборка\>.tar|  
|Версия 11 x86|ccm-Sol11x86.&lt;сборка\>.tar|  
|Версия 11 SPARC|ccm-Sol11sparc.&lt;сборка\>.tar|  

### <a name="suse-linux-enterprise-server-sles"></a>SUSE Linux Enterprise Server (SLES)  

|Версия|Файл|  
|-|-|  
|Версия 9 x86|ccm-SLES9x86.&lt;сборка\>.tar|  
|Версия 10 с пакетом обновления 1 (SP1) x86|ccm-Universalx86.&lt;сборка\>.tar|  
|Версия 10 с пакетом обновления 1 (SP1) x64|ccm-Universalx64.&lt;сборка\>.tar|  
|Версия 11 с пакетом обновления 1 (SP1) x86|ccm-Universalx86.&lt;сборка\>.tar|  
|Версия 11 с пакетом обновления 1 (SP1) x64|ccm-Universalx64.&lt;сборка\>.tar|  
|Версия 12 x64|ccm-Universalx64.&lt;сборка\>.tar|  

### <a name="ubuntu"></a>Ubuntu  

|Версия|Файл|    
|-|-|  
|Версия 10.04 LTS x86|ccm-Universalx86.&lt;сборка\>.tar|  
|Версия 10.04 LTS x64|ccm-Universalx64.&lt;сборка\>.tar|  
|Версия 12.04 LTS x86|ccm-Universalx86.&lt;сборка\>.tar|  
|Версия 12.04 LTS x64|ccm-Universalx64.&lt;сборка\>.tar|  
|Версия 14.04 LTS x86|ccm-Universalx86.&lt;сборка\>.tar|  
|Версия 14.04 LTS x64|ccm-Universalx64.&lt;сборка\>.tar|  

### <a name="exchange-server-connector"></a>Соединитель Exchange Server
 LTSB поддерживает ограниченное управление устройствами, которые подключаются к экземпляру сервера Exchange Server, без установки клиентского программного обеспечения. Дополнительные сведения см. в статье [Управление мобильными устройствами с помощью System Center Configuration Manager и Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).

 **Требования и ограничения**  

-   Configuration Manager предлагает ограниченные возможности управления мобильными устройствами. Ограниченные возможности управления доступны при использовании коннектора Exchange Server с устройствами, поддерживающими функцию Exchange Active Sync (EAS), которые подключаются к серверу с Exchange Server или Exchange Online.  

-   Дополнительные сведения о функциях управления, поддерживаемых Configuration Manager для мобильных устройств, управляемых с использованием коннектора Exchange Server, см. в разделе [Выбор решения для управления устройствами в Configuration Manager](../plan-design/choose-a-device-management-solution.md).  

**Поддерживаемые версии Exchange Server:**  
-   Exchange Server 2010 с пакетом обновления 1 (SP1)  
-   Exchange Server 2010 с пакетом обновления 2 (SP2)  
-   Exchange Server 2013;  

> [!NOTE]
> LTSB не поддерживает управление устройствами, которые подключаются через веб-службу, например Exchange Online (Office 365).


## <a name="configuration-manager-console"></a>Консоль Configuration Manager
LTSB поддерживает перечисленные ниже операционные системы для запуска консоли Configuration Manager. На каждом компьютере, на котором размещается консоль, должна быть платформа .NET Framework версии 4.5.2 или более поздней за исключением ОС Windows 10, для которой требуется платформа .NET Framework 4.6 или более поздней версии.

**Поддерживаемые операционные системы:**
- Windows Server 2016
- Windows Server 2012 R2 (x64): Standard, Datacenter
- Windows Server 2012 (x64): Standard, Datacenter
- Windows 10 Корпоративная 2016 LTSB (x86, x64)
- Windows 10 Корпоративная 2015 LTSB (x86, x64)
- Windows 8.1 (x86, x64): Professional и Enterprise


## <a name="sql-server-versions-supported-for-the-site-database-and-reporting-point"></a>Версии SQL Server, поддерживаемые для базы данных сайта и точки формирования отчетов
LTSB поддерживает перечисленные ниже версии SQL Server для размещения базы данных сайта и точки формирования отчетов. Для каждой поддерживаемой версии действуют те же требования к конфигурации и ограничения, что и для Current Branch, как указано в разделе [Поддержка версий SQL Server](../plan-design/configs/support-for-sql-server-versions.md).  К ним относятся использование кластера SQL Server или групп доступности SQL Server AlwaysOn.  

**Поддерживаемые версии:**

- SQL Server 2016: Standard и Enterprise.
- SQL Server 2014 с пакетом обновления 2 (SP2): Standard и Enterprise.
- SQL Server 2014 с пакетом обновления 1 (SP1): Standard и Enterprise.
- SQL Server 2012 с пакетом обновления 3 (SP3): Standard и Enterprise.
- SQL Server 2008 R2 с пакетом обновления 3 (SP3): Standard, Enterprise и Datacenter.
- SQL Server 2016, экспресс-выпуск
- SQL Server 2014 Express с пакетом обновления 2 (SP2)
- SQL Server 2014 Express с пакетом обновления 1 (SP1)
- SQL Server 2012 Express с пакетом обновления 3 (SP3)

## <a name="support-for-active-directory-domains"></a>Поддержка доменов Active Directory
Все системы сайта LTSB должны быть членами поддерживаемого домена Windows Active Directory. В отношении поддержки доменов Active Directory действуют требования и ограничения, указанные в разделе [Поддержка доменов Active Directory](../plan-design/configs/support-for-active-directory-domains.md), однако она ограничена следующими режимами работы домена:

**Поддерживаемые режимы:**
- Windows Server 2008
- Windows Server 2008 R2
- Windows Server 2012
- Windows Server 2012 R2

## <a name="additional-support-topics-that-apply-to-the-long-term-servicing-branch"></a>Дополнительные разделы о поддержке, относящиеся к Long-Term Servicing Branch
Сведения в следующих разделах, посвященных Current Branch, также относятся к LTSB:
- [Данные по размерам и масштабированию](../plan-design/configs/size-and-scale-numbers.md)
- [Предварительные требования к сайтам и системе сайта](../plan-design/configs/site-and-site-system-prerequisites.md)
- [Способы обеспечения высокой доступности](../servers/deploy/configure/high-availability-options.md)
- [Рекомендуемое оборудование](../plan-design/configs/recommended-hardware.md)
- [Поддержка функций и сетей Windows](../plan-design/configs/support-for-windows-features-and-networks.md)
- [Поддержка сред виртуализации](../plan-design/configs/support-for-virtualization-environments.md)
