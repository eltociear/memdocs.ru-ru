---
title: Планирование миграции
titleSuffix: Configuration Manager
description: Узнайте подробнее о сайтах и иерархиях перед переносом данных в иерархию назначения Configuration Manager (Current Branch).
ms.date: 01/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b2bf493e-1e10-496f-a139-2646522703ed
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b514e2bb0843801cfa6f0f307af8a5013fc3f9e6
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702832"
---
# <a name="plan-for-migration-to-configuration-manager-current-branch"></a>Планирование миграции на Configuration Manager (Current Branch)

*Область применения: Configuration Manager (Current Branch)*

Прежде чем переносить данные в конечную иерархию Configuration Manager (Current Branch), убедитесь в том, что вы знакомы с сайтами и иерархиями в Configuration Manager. Дополнительные сведения о сайтах и иерархиях см. в разделе [Основные сведения о Configuration Manager](../../core/understand/fundamentals.md).  

Установите иерархию Configuration Manager (Current Branch) в качестве конечной иерархии, чтобы можно было перенести данные из поддерживаемой исходной иерархии.  

После установки конечной иерархии нужно настроить компоненты и функции управления, которые требуется использовать в вашей конечной иерархии перед началом переноса данных.  

Кроме того, может потребоваться спланировать перекрытие между исходной иерархией и конечной иерархией. Например, исходная иерархия может быть настроена для использования тех же сетевых расположений или границ, что и конечная иерархия, а затем в конечной иерархии устанавливаются новые клиенты и используется автоматическое назначение сайта. В этом сценарии, так как вновь установленный клиент Configuration Manager может выбрать сайт для присоединения из любой иерархии, клиент может быть неправильно назначен исходной иерархии. Поэтому следует назначать все новые клиенты в конечной иерархии в конкретные сайты в данной иерархии, а не использовать автоматическое назначение.  

Дополнительные сведения о назначении сайта см. в подразделе [Рекомендации по назначению сайта клиента](../../core/plan-design/hierarchy/interoperability-between-different-versions.md#BKMK_SupConfigSiteAssignment) раздела [Взаимодействие различных версий Configuration Manager](../../core/plan-design/hierarchy/interoperability-between-different-versions.md).  

В следующих разделах содержатся справочные сведения о планировании миграции поддерживаемой исходной иерархии в конечную иерархию Configuration Manager:

-   [Необходимые условия для миграции](../../core/migration/prerequisites-for-migration.md)  

-   [Контрольные списки администратора по планированию миграции](../../core/migration/administrator-checklists-for-migration-planning.md)  

-   [Определение необходимости миграции данных в Configuration Manager (Current Branch)](../../core/migration/determine-whether-to-migrate-data.md)  

-   [Планирование стратегии для исходных иерархий](../../core/migration/planning-a-source-hierarchy-strategy.md)  

-   [Контрольные списки администратора по планированию миграции](../../core/migration/administrator-checklists-for-migration-planning.md)  

-   [Планирование стратегии миграции клиентов](../../core/migration/planning-a-client-migration-strategy.md)  

-   [Планирование стратегии миграции для развертывания содержимого](../../core/migration/planning-a-content-deployment-migration-strategy.md)  

-   [Планирование миграции объектов Configuration Manager в Configuration Manager (Current Branch)](../../core/migration/planning-for-the-migration-of-objects.md)  

-   [Планирование отслеживания действий миграции](../../core/migration/planning-to-monitor-migration-activity.md)  

-   [Планирование завершения миграции](../../core/migration/planning-to-complete-migration.md)  
