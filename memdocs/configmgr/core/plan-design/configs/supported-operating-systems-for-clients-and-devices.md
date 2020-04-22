---
title: Поддерживаемые клиенты и устройства
titleSuffix: Configuration Manager
description: Сведения о версиях операционных систем, которые Configuration Manager поддерживает для клиентов и устройств.
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 87f4e041-67df-4c61-aa98-7444faffe565
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8e3f375fb515808c1df39d1fdd786abb8f89a0a2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81691372"
---
# <a name="supported-os-versions-for-clients-and-devices-for-configuration-manager"></a>Поддерживаемые версии операционных систем для клиентов и устройств под управлением Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Configuration Manager поддерживает установку клиентского программного обеспечения на компьютерах Windows и macOS.  

## <a name="general-requirements-and-limitations"></a>Общие требования и ограничения

Ознакомьтесь со следующими требованиями и ограничениями для всех клиентов.

- Не поддерживается изменение параметров типа запуска и **Вход от имени** для любой службы Configuration Manager. Такие изменения могут привести к неправильной работе основных служб.

## <a name="windows-computers"></a>Компьютеры Windows  

Для управления указанными ниже версиями ОС Windows используйте клиент, предоставляемый с Configuration Manager. Дополнительные сведения см. в статье [Развертывание клиентов на компьютерах Windows в Configuration Manager](../../clients/deploy/deploy-clients-to-windows-computers.md).  

### <a name="supported-client-os-versions"></a>Поддерживаемые версии клиентских ОС

- **Windows 10**  

    Дополнительные сведения о поддержке Windows 10 см. [здесь](support-for-windows-10.md).  

- **Windows 8.1** (x86, x64): Professional и Enterprise

#### <a name="windows-virtual-desktop"></a>Виртуальный рабочий стол Windows

<!--3556025-->
[Виртуальный рабочий стол Windows](https://docs.microsoft.com/azure/virtual-desktop/) — это служба виртуализации для настольных систем и приложений, которая работает на Microsoft Azure. Начиная с версии 1906 Configuration Manager можно использовать для управления этими виртуальными устройствами с Windows в Azure.

Как и в случае сервера терминалов, некоторые из этих виртуальных устройств позволяют запускать несколько одновременных активных сеансов пользователей. Для решения проблем с производительностью клиентов Configuration Manager теперь отключает политики пользователя на любом устройстве, которое допускает эти несколько сеансов пользователя. Даже при включении политик пользователя клиент по умолчанию отключает их на этих устройствах, в том числе для многосеансового режима Windows 10 Корпоративная и серверов терминалов.

Клиент отключает политику пользователя лишь при обнаружении таких устройств во время новой установки. Для существующих клиентов такого типа, обновляемых до этой версии, сохраняется прежнее поведение. На существующем устройстве он настраивает параметр политики пользователя, даже если обнаруживает, что устройство разрешает несколько сеансов пользователя.

Если в этом сценарии требуется политика пользователя и допустимо любое возможное снижение производительности, используйте один из следующих методов, чтобы включить политику пользователя:

- В версии 1910 и более поздних используйте [параметры клиента](../../clients/deploy/configure-client-settings.md). В группе **Политика клиента** настройте следующий параметр: **Включите политику пользователя для нескольких пользовательских сеансов**.<!-- 4737447 -->

- В версии 1906 используйте пакет SDK Configuration Manager с [серверным классом WMI SMS_PolicyAgentConfig](../../../develop/reference/core/clients/config/sms_policyagentconfig-server-wmi-class.md). Задайте для нового свойства `PolicyEnableUserPolicyOnTS` значение `true`.

> [!Note]  
> Совместное управление нельзя использовать с клиентом, работающим в Windows 10 Корпоративная в многосеансовом режиме. <!-- SCCMDocs-pr#3950 -->

### <a name="supported-server-os-versions"></a>Поддерживаемые версии серверных ОС

- **Windows Server 2019**: Standard и Datacenter <sup>[Примечание 1](#bkmk_note1)</sup>  
    (начиная с Configuration Manager версии 1806)

- **Windows Server 2016**: Standard и Datacenter <sup>[Примечание 1](#bkmk_note1)</sup>  

- **Windows Storage Server 2016**: Workgroup и Standard  

- **Windows Server 2012 R2** (x64): Standard и Datacenter <sup>[Примечание 1](#bkmk_note1)</sup>

- **Windows Storage Server 2012 R2** (x64)

- **Windows Server 2012** (x64): Standard и Datacenter <sup>[Примечание 1](#bkmk_note1)</sup>

- **Windows Storage Server 2012** (x64)

#### <a name="server-core"></a>Основные серверные компоненты

Следующие версии относятся к устанавливаемому основному серверному компоненту для ОС. <sup>[Примечание 3](#bkmk_note3)</sup>  

Выпуски Windows Server, выпускаемые в рамках Semi-Annual Channel, устанавливаются вместе с основными серверными компонентами, такими как Windows Server версии 1809. Так как эти компоненты являются клиентами Configuration Manager, они поддерживаются так же, как и соответствующая версия Windows 10, выпускаемая в рамках программы Semi-Annual Channel. Дополнительные сведения о поддержке Windows 10 см. [здесь](support-for-windows-10.md).

- **Windows Server 2019** (x64) <sup>[Примечание 2](#bkmk_note2)</sup>

- **Windows Server 2016** (x64) <sup>[Примечание 2](#bkmk_note2)</sup>

- **Windows Server 2012 R2** (x64) <sup>[Примечание 2](#bkmk_note2)</sup>

- **Windows Server 2012** (x64) <sup>[Примечание 2](#bkmk_note2)</sup>

#### <a name="note-1"></a><a name="bkmk_note1"></a> Примечание 1

Средство Configuration Manager проверяет и поддерживает версии Windows Server Datacenter, но оно не сертифицировано официально для использования с Windows Server. Поддержка исправлений в Configuration Manager не касается проблем, которые наблюдаются только в Windows Server Datacenter Edition. Дополнительные сведения о программе сертификации Windows Server см. на сайте [Windows Server Catalog](https://www.windowsservercatalog.com/).

#### <a name="note-2"></a><a name="bkmk_note2"></a> Примечание 2

Для поддержки [принудительной установки клиента ](../../clients/deploy/plan/client-installation-methods.md#client-push-installation) добавьте службу файлового сервера из серверной роли "Файловые службы и службы хранилища". Сведения об установке компонентов Windows на компьютере основных серверных компонентов см. в разделе [Install roles, role services, and features by using Windows PowerShell cmdlets](https://docs.microsoft.com/windows-server/administration/server-manager/install-or-uninstall-roles-role-services-or-features#install-roles-role-services-and-features-by-using-windows-powershell-cmdlets) (Установка ролей, служб ролей и компонентов с помощью командлетов Windows PowerShell).  

#### <a name="note-3"></a><a name="bkmk_note3"></a> Примечание 3

Новое приложение центра программного обеспечения не поддерживается ни в одной версии Windows Server Core.<!--SCCMDocs issue 683-->

## <a name="windows-embedded-computers"></a>Компьютеры Windows Embedded  

Устройствами Windows Embedded можно управлять, установив на устройстве клиент Configuration Manager. Дополнительные сведения см. в статье [Планирование развертывания клиентов на устройствах Windows Embedded в System Center Configuration Manager](../../clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).  

### <a name="requirements-and-limitations"></a>Требования и ограничения

- В системах Windows Embedded, для которых не включены фильтры записи, поддерживаются все клиентские компоненты.  

- Клиенты, использующие один из следующих типов фильтров, поддерживаются для всех компонентов, кроме управления питанием:  

  - Расширенный фильтр записи (EWF)

  - Файловый фильтр записи (FBWF) ОЗУ

  - Объединенный фильтр записи (UWF)  

- Каталог приложений не поддерживается ни одним устройством Windows Embedded.  

### <a name="supported-os-versions"></a>Поддерживаемые версии ОС  

- **Windows 10 Корпоративная** (x86, x64)  

- **Windows 10 IoT Корпоративная** (x86, x64)  
    Эта версия включает канал долгосрочного обслуживания (LTSC). Дополнительные сведения см. в статье [An overview of Windows 10 IoT Enterprise](https://docs.microsoft.com/windows/iot-core/windows-iot-enterprise) (Обзор версии Windows 10 IoT Корпоративная).<!--SCCMDocs issue 560-->  

- **Windows Embedded 8.1 Industry** (x86, x64)

- **Windows Embedded 8 Standard** (x86, x64)

- **Windows Thin PC** (x86, x64)

- **Windows Embedded POSReady 7** (x86, x64)

- **Windows Embedded Standard 7 с пакетом обновления 1 (SP1)** (x86, x64)

## <a name="windows-ce-computers"></a>Компьютеры Windows CE

Устройствами Windows CE можно управлять с помощью устаревшего клиента Configuration Manager для мобильных устройств, который входит в состав Configuration Manager.  

### <a name="requirements-and-limitations"></a>Требования и ограничения

- Клиенту мобильного устройства требуется для установки 0,78 МБ дискового пространства. Для входа в систему может потребоваться до 256 КБ дополнительного пространства.

- Возможности таких мобильных устройств зависят от платформы и типа клиента. Сведения о поддерживаемых функциях управления см. в статье [Выбор решения для управления устройствами в System Center Configuration Manager](../choose-a-device-management-solution.md).  

### <a name="supported-os-versions"></a>Поддерживаемые версии ОС

- Windows CE 7.0 (процессоры ARM и x86)  

    > [!Note]
    > Поддержка Windows CE 7.0 в Configuration Manager прекращена. Дополнительные сведения см. в статье [Удаленные и устаревшие компоненты клиентов Configuration Manager](../changes/deprecated/removed-and-deprecated-client.md).

#### <a name="supported-languages-include"></a>Поддерживаемые языки

- Китайский (упрощенное и традиционное письмо)

- Английский (США)

- Французский (Франция)

- Немецкий

- Итальянский

- Японский  

- Корейский  

- Португальский (Бразилия)  

- Русский  

- Испанский (Испания)  

## <a name="extended-security-updates-and-configuration-manager"></a><a name="bkmk_ESU"></a> Расширенные обновления безопасности и Configuration Manager

Программа [расширенных обновлений безопасности (ESU)](https://support.microsoft.com/help/4497181/lifecycle-faq-extended-security-updates) — это исключительный вариант для клиентов, которым необходимо использовать определенные устаревшие продукты Майкрософт после окончания их поддержки. Например, Windows 7. Она позволяет получать важные и критически важные обновления безопасности (как определено в [Центре Майкрософт по реагированию на угрозы (MSRC)](https://www.microsoft.com/msrc)) в течение максимум трех лет после окончания срока расширенной поддержки продукта.

Configuration Manager не позволяет работать с продуктами, жизненный цикл поддержки которых уже завершен. Сюда входят все продукты, для которых действует программа ESU. Обновления для системы безопасности по программе ESU будут публиковаться в Windows Server Update Services (WSUS). Эти обновления будут появляться в консоли Configuration Manager. Хотя Configuration Manager больше не позволяет использовать продукты, охватываемые программой ESU, [последняя выпущенная версия Configuration Manager (Current Branch)](../../servers/manage/updates.md#version-details) поддерживает развертывание и установку обновлений для системы безопасности Windows, выпускаемых в рамках этой программы. Последнюю выпущенную версию также можно использовать для развертывания Windows 10 на устройствах под управлением Windows 7.

Что касается функций управления клиентами, не связанных с развертыванием ОС и обновлением программного обеспечения Windows, эти функции больше не будут тестироваться на операционных системах, охватываемых программой ESU, и их дальнейшая работа не гарантируется. Для получения поддержки по управлению клиентами настоятельно рекомендуем как можно скорее перейти на текущую версию этих операционных систем.

## <a name="mac-computers"></a>Компьютеры Mac  

Компьютерами Apple Mac можно управлять с помощью клиента Configuration Manager для macOS.  

Пакет установки клиента для macOS не поставляется на носителе Configuration Manager. Скачайте [клиент Microsoft Endpoint Configuration Manager для macOS (64-разрядная версия)](https://www.microsoft.com/download/details.aspx?id=100850) в Центре загрузки Майкрософт.  

Дополнительные сведения см. в статье [How to deploy clients to Macs](../../clients/deploy/deploy-clients-to-macs.md) (Развертывание клиентов на компьютерах Mac).  

### <a name="requirements-and-limitations"></a>Требования и ограничения

- Не поддерживается установка и работа клиента Configuration Manager для macOS на компьютерах с учетной записью, отличной от привилегированной. Это может привести к неправильной работе ключевых служб.  

### <a name="supported-versions"></a>Поддерживаемые версии

- **macOS Catalina (10.15)** (требуется сайт Configuration Manager версии 1910 или более поздней и клиент Configuration Manager для macOS версии 5.0.8742.1000 или более поздней)

- **macOS Mojave (10.14)**

- **macOS High Sierra (10.13)**

## <a name="linux-and-unix-servers"></a>Серверы Linux и UNIX  

> [!Important]  
> Configuration Manager версии 1902 не поддерживает Linux и UNIX в качестве клиента. О прекращении поддержки было объявлено с выходом [версии 1802](../changes/whats-new-in-version-1802.md#deprecation-announcement-for-linux-and-unix-client-support). Вы можете управлять серверами Linux с помощью портала управления Microsoft Azure. Решения Azure располагают расширенной поддержкой Linux, которая в большинстве случаев превышает функциональные возможности Configuration Manager, включая полное управление исправлениями для Linux.

Пакеты установки клиента для Linux и UNIX не поставляются на носителе Configuration Manager. Скачайте **Клиенты для дополнительных операционных систем** из [Центра загрузки Майкрософт](https://go.microsoft.com/fwlink/?LinkID=525184). Помимо пакетов установки клиента скачиваемые файлы содержат скрипт, который управляет установкой клиента на каждом компьютере.  

### <a name="requirements-and-limitations"></a>Требования и ограничения

- Сведения о зависимостях файла операционной системы для клиента Linux и UNIX можно найти в разделе [Необходимые условия для развертывания клиентов на серверах Linux и UNIX](../../clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_ClientDeployPrereqforLnU).  

- Обзор возможностей управления, поддерживаемых для UNIX или Linux, см. в статье [Развертывание клиентов на серверах UNIX и Linux в System Center Configuration Manager](../../clients/deploy/deploy-clients-to-unix-and-linux-servers.md).  

- Для поддерживаемых версий Linux и UNIX список версий включает в себя все последующие промежуточные версии. Например, CentOS версии 6 включает CentOS 6.3. Аналогично, поддержка операционной системы, у которой есть пакеты обновления (например, SUSE Linux Enterprise Server 11 с пакетом обновления 1 (SP1)), включает поддержку всех последующих пакетов обновления для этой операционной системы.  

- Сведения о пакетах установки клиента и универсальном агенте см. в статье [Развертывание клиентов на серверах UNIX и Linux в System Center Configuration Manager](../../clients/deploy/deploy-clients-to-unix-and-linux-servers.md).  

### <a name="supported-versions"></a>Поддерживаемые версии

Перечисленные ниже версии поддерживаются с помощью указанного TAR-файла.  

#### <a name="aix"></a>AIX  

|Версия|TAR-файл|  
|-|-|  
|Версия 6.1 (Power)|ccm-Aix61ppc.&lt;сборка\>.tar|  
|Версия 7.1 (Power)|ccm-Aix71ppc.&lt;сборка\>.tar|  

#### <a name="centos"></a>CentOS  

|Версия|TAR-файл|  
|-|-|  
|Версия 5 x86|ccm-Universalx86.&lt;сборка\>.tar|  
|Версия 5 x64|ccm-Universalx64.&lt;сборка\>.tar|  
|Версия 6 x86|ccm-Universalx86.&lt;сборка\>.tar|  
|Версия 6 x64|ccm-Universalx64.&lt;сборка\>.tar|  
|Версия 7 x64|ccm-Universalx64.&lt;сборка\>.tar|  

#### <a name="debian"></a>Debian  

|Версия|TAR-файл|  
|-|-|  
|Версия 5 x86|ccm-Universalx86.&lt;сборка\>.tar|  
|Версия 5 x64|ccm-Universalx64.&lt;сборка\>.tar|  
|Версия 6 x86|ccm-Universalx86.&lt;сборка\>.tar|  
|Версия 6 x64|ccm-Universalx64.&lt;сборка\>.tar|  
|Версия 7 x86|ccm-Universalx86.&lt;сборка\>.tar|  
|Версия 7 x64|ccm-Universalx64.&lt;сборка\>.tar|  
|Версия 8 x86|ccm-Universalx86.&lt;сборка\>.tar|  
|Версия 8 x64|ccm-Universalx64.&lt;сборка\>.tar|  

#### <a name="hp-ux"></a>HP-UX  

|Версия|TAR-файл|  
|-|-|  
|Версия 11iv3 IA64|ccm-HpuxB.11.31i64.&lt;сборка\>.tar|  

#### <a name="oracle-linux"></a>Oracle Linux  

|Версия|TAR-файл|  
|-|-|  
|Версия 5 x86|ccm-Universalx86.&lt;сборка\>.tar|  
|Версия 5 x64|ccm-Universalx64.&lt;сборка\>.tar|  
|Версия 6 x86|ccm-Universalx86.&lt;сборка\>.tar|  
|Версия 6 x64|ccm-Universalx64.&lt;сборка\>.tar|  
|Версия 7 x64|ccm-Universalx64.&lt;сборка\>.tar|  

#### <a name="red-hat-enterprise-linux-rhel"></a>Red Hat Enterprise Linux (RHEL)  

|Версия|TAR-файл|  
|-|-|  
|Версия 5 x86|ccm-Universalx86.&lt;сборка\>.tar|  
|Версия 5 x64|ccm-Universalx64.&lt;сборка\>.tar|  
|Версия 6 x86|ccm-Universalx86.&lt;сборка\>.tar|  
|Версия 6 x64|ccm-Universalx64.&lt;сборка\>.tar|  
|Версия 7 x64|ccm-Universalx64.&lt;сборка\>.tar|  

#### <a name="solaris"></a>Solaris  

|Версия|TAR-файл|  
|-|-|  
|Версия 10 x86|ccm-Sol10x86.&lt;сборка\>.tar|  
|Версия 10 SPARC|ccm-Sol10sparc.&lt;сборка\>.tar|  
|Версия 11 x86|ccm-Sol11x86.&lt;сборка\>.tar|  
|Версия 11 SPARC|ccm-Sol11sparc.&lt;сборка\>.tar|  

#### <a name="suse-linux-enterprise-server-sles"></a>SUSE Linux Enterprise Server (SLES)  

|Версия|TAR-файл|  
|-|-|  
|Версия 10 с пакетом обновления 1 (SP1) x86|ccm-Universalx86.&lt;сборка\>.tar|  
|Версия 10 с пакетом обновления 1 (SP1) x64|ccm-Universalx64.&lt;сборка\>.tar|  
|Версия 11 с пакетом обновления 1 (SP1) x86|ccm-Universalx86.&lt;сборка\>.tar|  
|Версия 11 с пакетом обновления 1 (SP1) x64|ccm-Universalx64.&lt;сборка\>.tar|  
|Версия 12 x64|ccm-Universalx64.&lt;сборка\>.tar|  

#### <a name="ubuntu"></a>Ubuntu  

|Версия|TAR-файл|  
|-|-|  
|Версия 10.04 LTS x86|ccm-Universalx86.&lt;сборка\>.tar|  
|Версия 10.04 LTS x64|ccm-Universalx64.&lt;сборка\>.tar|  
|Версия 12.04 LTS x86|ccm-Universalx86.&lt;сборка\>.tar|  
|Версия 12.04 LTS x64|ccm-Universalx64.&lt;сборка\>.tar|  
|Версия 14.04 LTS x86|ccm-Universalx86.&lt;сборка\>.tar|  
|Версия 14.04 LTS x64|ccm-Universalx64.&lt;сборка\>.tar|  
|Версия 16.04 LTS x86|ccm-Universalx86.&lt;сборка\>.tar|  
|Версия 16.04 LTS x64|ccm-Universalx64.&lt;сборка\>.tar|  


## <a name="on-premises-mdm"></a><a name="bkmk_OnpremOS"></a> Локальное управление мобильными устройствами (MDM)

В Configuration Manager предусмотрены встроенные возможности для управления мобильными устройствами, которые являются локальными, без установки клиентского программного обеспечения. Дополнительные сведения см. в статье об [управлении мобильными устройствами с помощью локальной инфраструктуры](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

### <a name="supported-operating-systems"></a>Поддерживаемые операционные системы

- **Windows 10 Pro** (x86, x64)  

- **Windows 10 Pro Корпоративная** (x86, x64)  

- **Windows 10 IoT Корпоративная** (x86, x64)  
    Эта версия включает канал долгосрочного обслуживания (LTSC). Дополнительные сведения см. в статье [An overview of Windows 10 IoT Enterprise](https://docs.microsoft.com/windows/iot-core/windows-iot-enterprise) (Обзор версии Windows 10 IoT Корпоративная).<!--SCCMDocs issue 560-->  

- **Windows 10 IoT Mobile Корпоративная**  

- **Windows 10 для совместной работы для Surface Hub**  

- **Windows 10 Mobile**  

- **Windows 10 Mobile Корпоративная**  

    > [!Note]
    > Поддержка Windows 10 Mobile и Windows 10 Mobile Корпоративная в Configuration Manager прекращена. Дополнительные сведения см. в статье [Удаленные и устаревшие компоненты клиентов Configuration Manager](../changes/deprecated/removed-and-deprecated-client.md).


## <a name="exchange-server-connector"></a><a name="bkmk_ExSrvConOS"></a> Коннектор Exchange Server  

Configuration Manager поддерживает ограниченное управление устройствами, которые подключаются к серверу Exchange Server, без установки клиента Configuration Manager. Дополнительные сведения см. в статье [Управление мобильными устройствами с помощью System Center Configuration Manager и Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

### <a name="supported-versions-of-exchange-server"></a>Поддерживаемые версии Exchange Server

- **Exchange Online (Office 365)** : эта версия включает Business Productivity Online Standard Suite  

- **Exchange Server 2016**  

- **Exchange Server 2013**  

- **Exchange Server 2010 с пакетом обновления 1 (SP1)** или **Exchange Server 2010 с пакетом обновления 2 (SP2)**
