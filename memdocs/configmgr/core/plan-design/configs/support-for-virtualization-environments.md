---
title: Поддержка виртуализации
titleSuffix: Configuration Manager
description: Требования для установки клиента и ролей системы сайта Configuration Manager в среде виртуализации.
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1098e8c5-9676-4c2b-841b-ec88bd04e495
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2e266373667efebccdb84fe743f66beeaa5a0e88
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688552"
---
# <a name="support-for-virtualization-environments-with-configuration-manager"></a>Поддержка сред виртуализации с использованием Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Configuration Manager поддерживает установку клиента и ролей системы сайта в поддерживаемых операционных системах, работающих как виртуальные машины в средах виртуализации, перечисленные в этой статье. Эта поддержка обеспечивается даже тогда, когда узел виртуальной машины (среда виртуализации) не поддерживается как клиент или сервер сайта.  

Например,вы используете Microsoft Hyper-V Server 2012 для размещения виртуальной машины, на которой работает Windows Server 2012. При этом вы можете установить клиент или роли системы сайта на виртуальной машине под управлением Windows Server 2012. Но вы не можете установить клиент на виртуальной машине под управлением Microsoft Hyper-V Server 2012.  

## <a name="virtualization-environments"></a>Среды виртуализации

- Windows Server 2019  
- Windows Server 2016 <sup>[Прим. 1](#bkmk_note1)</sup>  
- Microsoft Hyper-V Server 2016 <sup>[Прим. 1](#bkmk_note1)</sup>  
- Windows Server 2012 R2  
- Microsoft Hyper-V Server 2012  
- Windows Server 2012  

### <a name="note-1-nested-virtualization"></a><a name="bkmk_note1"></a> Примечание 1. Вложенная виртуализация

Configuration Manager не поддерживает [вложенную виртуализацию](https://docs.microsoft.com/windows-server/virtualization/hyper-v/What-s-new-in-Hyper-V-on-Windows#nested-virtualization-new), которая появилась в Windows Server 2016.

### <a name="virtualization-environment-support"></a>Поддержка сред виртуализации

Виртуальные машины должны соответствовать тем же требованиям к оборудованию и программному обеспечению, которые применялись бы для физического компьютера c Configuration Manager, или более строгим требованиям.  

Чтобы проверить поддержку среды виртуализации в Configuration Manager, воспользуйтесь программой проверки виртуализации серверов (SVVP). Она включает в себя сетевой мастер политики поддержки программы виртуализации. Дополнительные сведения см. на странице [о программе проверки виртуализации Windows Server](https://www.windowsservercatalog.com/svvp.aspx).  

> [!NOTE]  
> Configuration Manager не поддерживает гостевые операционные системы Virtual PC и Virtual Server, работающие на компьютерах Mac.  

Configuration Manager не может управлять виртуальными машинами, если они недоступны в Интернете. Образ отключенной виртуальной машины нельзя обновить; также нельзя собирать данные инвентаризации с помощью клиента Configuration Manager на основном компьютере.  

Виртуальные машины не обслуживаются особым образом. Например, Configuration Manager может не определить, нужно ли повторно применить к образу виртуальной машины обновление, если виртуальная машина, к которой применялось обновление, была остановлена и перезапущена без сохранения состояния.  

##  <a name="microsoft-azure-virtual-machines"></a><a name="bkmk_Azure"></a> Виртуальные машины Microsoft Azure  

Configuration Manager может выполняться на виртуальных машинах в Azure точно так же, как и локально в вашем центре обработки данных. Configuration Manager используется с виртуальными машинами Azure в следующих сценариях:  

- **Сценарий 1.** Запустите Configuration Manager на виртуальной машине Azure. Используйте его для управления клиентами, установленными на других виртуальных машинах Azure.  

- **Сценарий 2**. Запустите Configuration Manager на виртуальной машине Azure. Используйте его для управления клиентами, работающими за пределами Azure.  

- **Сценарий 3**. Запустите различные роли системы сайта Configuration Manager на виртуальных машинах Azure. Запустите другие роли в своем локальном центре обработки данных, который правильно подключен к Azure.  

При установке Configuration Manager на виртуальных машинах Azure применяются те же требования к сетям, поддерживаемым конфигурациям и оборудованию, что и при локальной установке.  

Дополнительные сведения см. в статье [Вопросы и ответы по использованию Configuration Manager в Azure](../../understand/configuration-manager-on-azure.md).

> [!IMPORTANT]  
> На сайты и клиенты Configuration Manager, работающие на виртуальных машинах Azure, распространяются те же требования к лицензиям, что и на локальные установки.  

## <a name="windows-virtual-desktop"></a>Виртуальный рабочий стол Windows

[Виртуальный рабочий стол Windows](https://docs.microsoft.com/azure/virtual-desktop/) входит в состав предварительной версии Microsoft Azure и Microsoft 365. Начиная с версии 1906 Configuration Manager можно использовать для управления этими виртуальными устройствами с Windows в Azure. Дополнительные сведения см. в статье о [поддерживаемых операционных системах для клиентов и устройств](supported-operating-systems-for-clients-and-devices.md).
