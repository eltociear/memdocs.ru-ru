---
title: Поддерживаемые конфигурации
titleSuffix: Configuration Manager
description: Ознакомьтесь с основными конфигурациями и требованиями для планирования, развертывания и обслуживания правильно работающей среды Configuration Manager.
ms.date: 10/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 45a10878-ff48-4318-9c6d-c014b38a4039
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 09618acc1c0950c3eaae79cca59fcf71dc7ef61e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688522"
---
# <a name="supported-configurations-for-configuration-manager"></a>Поддерживаемые конфигурации для Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Локальное решение Configuration Manager использует ваши серверы, клиенты, сетевые конфигурации и дополнительные продукты, такие как Microsoft Intune, SQL Server и Azure.

Информация в этом и последующих разделах необходима для понимания основных конфигураций, требований и ограничений с целью планирования, развертывания и обслуживания правильно работающей среды Configuration Manager.  Эта информация относится к инфраструктуре сайтов, иерархий и управляемых устройств Configuration Manager.

Если функция или возможность Configuration Manager требует более конкретной настройки, соответствующую информацию можно найти в документации по этой функции. Эта информация дополняет общие сведения о конфигурации.  

 Продукты и технологии, описываемые в следующих разделах, поддерживаются в Configuration Manager. Однако их указание здесь не подразумевает расширения поддержки этих продуктов за пределы их индивидуальных жизненных циклов поддержки. Configuration Manager не позволяет работать с продуктами, жизненный цикл поддержки которых уже завершен, в том числе с теми, для которых действует программа [расширенных обновлений безопасности (ESU)](https://support.microsoft.com/help/4497181/lifecycle-faq-extended-security-updates). Дополнительные сведения о жизненных циклах поддержки Майкрософт см. на веб-сайте [Правила по срокам поддержки продуктов Майкрософт](https://go.microsoft.com/fwlink/p/?LinkId=208270). Дополнительные сведения о расширенных обновлениях безопасности в Configuration Manager см. в статье [Поддерживаемые версии операционных систем для клиентов и устройств под управлением Configuration Manager](supported-operating-systems-for-clients-and-devices.md#bkmk_ESU).

> [!NOTE]  
>  Сведения о политике сроков поддержки продуктов корпорации Майкрософт см. на веб-сайте [Вопросы и ответы о правилах по срокам поддержки продуктов корпорации Майкрософт](https://go.microsoft.com/fwlink/p/?LinkId=31976).  

 Кроме того, продукты и версии продуктов, которые не указаны в следующих разделах, не поддерживаются в Configuration Manager, если только иное не указано в [блоге рабочей группы по корпоративной мобильности и безопасности](https://blogs.technet.microsoft.com/enterprisemobility/).  Иногда содержимое в этом блоге может обновляться раньше, чем текст данного документа.


-  [Данные по размерам и масштабированию](../../../core/plan-design/configs/size-and-scale-numbers.md)  
Сведения о количестве сайтов, ролей системы сайта на каждый сайт, а также клиентов или устройств, поддерживаемом в различных типах иерархии Configuration Manager.

-  [Предварительные требования к сайтам и системе сайта](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)  
Сведения о конфигурациях, необходимых для поддержки различных типов сайтов и ролей системы сайта на сервере Windows Server.

-  [Поддерживаемые операционные системы для серверов системы сайта](../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)  
Узнайте, какие операционные системы можно использовать в качестве сервера сайта или сервера системы сайта.

-  [Поддерживаемые операционные системы для клиентов и устройств](../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md)  
Узнайте, какими операционными системами можно управлять с помощью Configuration Manager, включая Windows, Windows Embedded, Linux и UNIX, Mac и операционные системы мобильных устройств.

-  [Поддерживаемые операционные системы для консоли](../../../core/plan-design/configs/supported-operating-systems-consoles.md)  
Узнайте, в каких операционных системах может размещаться консоль Configuration Manager, которая служит точкой доступа для управления развертыванием.  

-  [Поддержка версий SQL Server](../../../core/plan-design/configs/support-for-sql-server-versions.md)  
Сведения о версиях SQL Server, в которых могут размещаться база данных сайта и база данных отчетов, а также об обязательных и необязательных конфигурациях, которые можно использовать.

-  [Параметры высокой доступности](../../servers/deploy/configure/high-availability-options.md)  
Сведения о вариантах, которые можно реализовать при разработке среды, чтобы обеспечить высокий уровень доступности служб для развертывания Configuration Manager.

-  [Рекомендуемое оборудование](../../../core/plan-design/configs/recommended-hardware.md)  
Рекомендации, которые помогут вам определить соответствующее оборудование и конфигурации для размещения сайтов Configuration Manager и основных служб.

-  [Поддержка доменов Active Directory](../../../core/plan-design/configs/support-for-active-directory-domains.md)  
Сведения о поддерживаемых конфигурациях домена Active Directory, которые необходимы для Configuration Manager.

-  [Поддержка функций и сетей Windows](../../../core/plan-design/configs/support-for-windows-features-and-networks.md)  
Сведения о поддерживаемых технологиях Windows (например, BranchCache и дедупликации данных) и ограничениях на их использование с Configuration Manager.

-  [Поддержка сред виртуализации](../../../core/plan-design/configs/support-for-virtualization-environments.md)  
Дополнительные сведения о поддерживаемых технологиях виртуальных машин.
