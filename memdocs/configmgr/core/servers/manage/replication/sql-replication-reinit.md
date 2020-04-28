---
title: Повторная инициализация репликации SQL
titleSuffix: Configuration Manager
description: Используйте эту схему, чтобы начать поиск неисправностей при повторной инициализации репликации SQL между сайтами Configuration Manager
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ce4a1ca8-6433-4447-819f-19dd5faa6f46
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f6207ed4eeeef892de38c85096d2cc80189214d1
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078568"
---
# <a name="sql-replication-reinit"></a>Повторная инициализация репликации SQL

В иерархии с несколькими сайтами Configuration Manager использует репликацию SQL для обмена данными между сайтами. Дополнительные сведения см. в разделе [Репликация базы данных](../../../plan-design/hierarchy/database-replication.md).

Используйте следующую схему, чтобы начать устранение неполадок при повторной инициализации репликации SQL (reinit):

![Схема устранения неисправностей при повторной репликации SQL](media/sql-replication-reinit.svg)

## <a name="queries"></a>Запросы

Эта схема использует следующие запросы:

### <a name="check-if-site-is-in-maintenance-mode"></a>проверка, работает ли сайт в режиме обслуживания;

```sql
SELECT * FROM ServerData
WHERE Status = 120
```

### <a name="check-which-replication-group-hasnt-completed-reinit"></a>проверка, какая группа репликации не завершила повторную инициализацию;

```sql
SELECT * FROM RCM_DrsInitializationTracking
WHERE InitializationStatus NOT IN (6,7)
```

### <a name="check-global-data"></a>проверка глобальных данных;

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N'GLOBAL'
```

### <a name="check-site-data"></a>проверка данных сайта.

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N'Site'
```

## <a name="next-steps"></a>Дальнейшие шаги

- [Повторная инициализация глобальных данных](global-data-reinit.md)
- [Повторная инициализация данных сайта](site-data-reinit.md)
- [Конфигурация SQL](sql-configuration.md)
