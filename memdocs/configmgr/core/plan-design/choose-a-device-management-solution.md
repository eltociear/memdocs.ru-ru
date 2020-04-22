---
title: Выбор решения для управления устройствами
titleSuffix: Configuration Manager
description: Узнайте о решениях, предлагаемых корпорацией Майкрософт для управления компьютерами, серверами и устройствами.
ms.date: 01/24/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 24633725-791a-4df7-8dce-2c24c1a19a03
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d36e29f0f915c0f2a35070c667525853e5981564
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702272"
---
# <a name="choose-a-device-management-solution"></a>Выбор решения для управления устройствами

Корпорация Майкрософт предлагает разные решения для управления компьютерами, серверами и устройствами. Эти решения доступны в локальной среде и (или) облаке. Выберите решение, которое соответствует бизнес-требованиям вашей организации. Выбирайте решение в зависимости от платформ устройств, которыми необходимо управлять, и требуемых функций управления.

## <a name="overview"></a>Overview

Вы можете подобрать несколько решений Майкрософт для разных сценариев. Не обязательно останавливаться на чем-то одном.

- Для небольших организаций отличным вариантом будет такое средство, как Windows Admin Center.
- Около 75 % ИТ-организаций управляют устройствами с помощью Configuration Manager.
- В рамках инфраструктуры Azure Stack, которая в основном направлена на управление серверами, Microsoft Azure предоставляет различные решения для работы в облаке и локальной среде.
- Microsoft Intune обеспечивает управление клиентами в облаке.
- Вы можете объединить Configuration Manager и Intune с помощью функций совместного управления.

Эта таблица поможет сравнить эти технологии управления:

|  | Только облако | С возможностью подключения к облаку | Локально | отключен |
|---------|---------|---------|---------|---------|
| **Узел Hyper-V** | Не применяются | - Azure Stack<br/> - Windows Admin Center<br/> - Virtual Machine Manager | - Azure Stack<br/> - Windows Admin Center<br/> - Virtual Machine Manager | - Azure Stack<br/> - Windows Admin Center<br/> - Virtual Machine Manager |
| **Windows Server** | - Управление Azure<br/> - Configuration Manager | - Управление Azure<br/> - Configuration Manager | - Управление Azure<br/> - Configuration Manager | Configuration Manager |
| **Сервера Linux** | Управление Azure | Управление Azure | Управление Azure |  |
| **Windows 10** | - Intune<br/> - Configuration Manager | - Intune<br/> - Configuration Manager | - Intune<br/> - Configuration Manager | Configuration Manager |
| **Windows 7 или 8.1** | Configuration Manager | Configuration Manager | Configuration Manager | Configuration Manager |
| **Виртуальный рабочий стол Windows** | Configuration Manager | Не применяются | Не применяются | Не применяются |

Дополнительные сведения см. в следующих статьях:

- [Что такое Azure Stack?](https://docs.microsoft.com/azure-stack/operator/azure-stack-overview)
- [Что такое Windows Admin Center?](https://docs.microsoft.com/windows-server/manage/windows-admin-center/understand/what-is)
- [Что такое Virtual Machine Manager?](https://docs.microsoft.com/system-center/vmm/overview)
- [Продукты управления Azure](https://docs.microsoft.com/azure/)
- [Что такое Виртуальный рабочий стол Windows?](https://docs.microsoft.com/azure/virtual-desktop/overview)

Дополнительные сведения о решениях Configuration Manager и Intune содержатся в следующем разделе.

## <a name="client-management"></a>Управление клиентами

В этом разделе сравниваются четыре следующих решения для управления клиентами:

- [клиент Configuration Manager](#bkmk_sccm);
- [локальное управление мобильными устройствами (MDM) в Configuration Manager](#bkmk_opmdm);
- [совместное управление с Microsoft Intune](#bkmk_comanage);
- [Microsoft Exchange](#bkmk_opmdm)

Вы можете использовать эти решения как по отдельности, так и в сочетании друг с другом. Например, для компьютеров и серверов в организации можно использовать подход к управлению на основе клиентов, а для ноутбуков — функцию совместного управления через Интернет. Объединив эти подходы, вы сможете выполнять все необходимые задачи, связанные с управлением устройствами.  

Кроме того, здесь есть две таблицы, в которых решения по управлению сравниваются по следующим аспектам:

- [по поддерживаемым платформам](#bkmk_comp1);
- [по функциям управления](#bkmk_comp2).

### <a name="configuration-manager-client"></a><a name="bkmk_sccm"></a> Клиент Configuration Manager  

Для этого варианта требуется установить клиент Configuration Manager на устройствах. Этот вариант предоставляет больше всего функций для управления компьютерами, серверами и другими устройствами в вашей среде.

Дополнительные сведения см. в статье [Методы установки клиента в System Center Configuration Manager](../clients/deploy/plan/client-installation-methods.md).  

### <a name="on-premises-mdm"></a><a name="bkmk_opmdm"></a> Локальное управление мобильными устройствами (MDM)  

При использовании этого варианта применяются возможности управления устройствами, встроенные в Windows 10. Хотя локальное управление MDM пока нельзя назвать таким же полнофункциональным, как управление на основе клиентов, это более простое решение. При таком подходе к управлению устройствами используются локальные ресурсы Configuration Manager.  

Дополнительные сведения см. в статье об [управлении мобильными устройствами с помощью локальной инфраструктуры](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

### <a name="co-management-with-microsoft-intune"></a><a name="bkmk_comanage"></a> Совместное управление с Microsoft Intune

Совместное управление — один из основных способов подключения развернутого клиента Configuration Manager к облаку Microsoft 365. Такой способ позволяет параллельно управлять устройствами Windows 10 с помощью Configuration Manager и Microsoft Intune. Совместное управление позволяет подключить к облаку приобретенное ПО Configuration Manager, добавив новые функции.

Дополнительные сведения см. в статье [What is co-management?](../../comanage/overview.md) (Что такое совместное управление?).  

### <a name="microsoft-exchange"></a><a name="bkmk_exchange"></a> Microsoft Exchange  

В этом варианте используется соединитель Exchange Server, который подключает несколько серверов Exchange к Configuration Manager. Оно позволяет централизованно управлять устройствами, которые могут подключаться к Exchange ActiveSync. Можно настроить функции управления мобильными устройствами Exchange из консоли Configuration Manager. Например, можно настроить удаленную очистку устройств и управление параметрами для нескольких серверов Exchange.

Дополнительные сведения см. в статье [Управление мобильными устройствами с помощью System Center Configuration Manager и Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

### <a name="compare-solutions-by-supported-platforms"></a><a name="bkmk_comp1"></a> Сравнение решений по поддерживаемым платформам  

|Платформа|Клиент Configuration Manager|локальное управление мобильными устройствами (MDM).|Configuration Manager с Exchange| Intune |
|--------|----------------------------|---------------|-----------------------------------|--------|
|Android| | |да| да |
|iOS| | |да| да |
|Mac OS X|да| |да| да |
|Windows 10|да|да|да| да |
|Windows 10 Mobile| |да|да| да |
|Windows (предыдущие версии)|да| |да|  |
|Windows Server|да| |да|  |
|Windows Embedded|да| | |  |

Полный список поддерживаемых платформ см. в следующих статьях:

- [Поддерживаемые операционные системы для клиентов и устройств в Configuration Manager](configs/supported-operating-systems-for-clients-and-devices.md)
- [Поддерживаемые конфигурации Intune](https://docs.microsoft.com/intune/supported-devices-browsers)

Для управления мобильными устройствами Android, iOS и Windows 10 корпорация Майкрософт рекомендует использовать Intune. Дополнительные сведения см. в статье о [Microsoft Intune](https://docs.microsoft.com/intune/what-is-intune).

### <a name="compare-solutions-by-management-functionality"></a><a name="bkmk_comp2"></a> Сравнение решений по функциям управления  

|Функция управления|Клиент Configuration Manager|локальное управление мобильными устройствами (MDM).|Configuration Manager с Exchange|  
|--------|----------------------------|---------------|-----------------------------------|  
|Взаимная проверка подлинности на основе сертификатов|да|да| |
|Установка клиента|да| | |
|Поддержка через Интернет|да| | |
|Обнаружение|да| |да|
|Инвентаризация оборудования|да|да|да|
|Инвентаризация программного обеспечения|да| |да|
|Параметры|да|да|да|
|Развертывание программного обеспечения|да|да| |
|Управление обновлением программного обеспечения|да| | |
|Развертывание операционной системы|да| | |
|Блокировка из Configuration Manager|да|да| |
|Карантин и блокировка из Exchange Server (и Configuration Manager)| | |да|
|Удаленная очистка| |да|да|
