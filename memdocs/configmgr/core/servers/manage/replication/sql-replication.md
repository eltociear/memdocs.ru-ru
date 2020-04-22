---
title: Репликация SQL
titleSuffix: Configuration Manager
description: Используйте эту схему, чтобы начать поиск неисправностей при повторной инициализации репликации SQL между сайтами Configuration Manager
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: adb198c4-da3c-49c3-8fbd-6d1361272869
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a25218e53313b7a8c3192959b54b65d2a32fae7d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81699862"
---
# <a name="sql-replication"></a>Репликация SQL

В иерархии с несколькими сайтами Configuration Manager использует репликацию SQL для обмена данными между сайтами. Дополнительные сведения см. в разделе [Репликация базы данных](../../../plan-design/hierarchy/database-replication.md).

Используйте следующую схему, чтобы начать устранение неполадок репликации SQL при сбое связи:

![Схема устранения неполадок при репликации SQL](media/sql-replication.svg)

## <a name="queries"></a>Запросы

Эта схема использует следующие запросы:

### <a name="check-if-the-replication-group-link-is-in-degraded-or-failed-state"></a>проверка, не находится ли ссылка на группу репликации в неработоспособном или неисправном состоянии;

```sql
SELECT * FROM RCM_ReplicationLinkStatus
WHERE Status IN (8, 9)
```

### <a name="check-if-replication-group-link-is-recently-calculated"></a>проверка, была ли ссылка на группу репликации недавно рассчитана;

```sql
DECLARE @cutoffTime DATETIME
SELECT @cutoffTime = DATEADD(minute, -30, GETUTCDATE())
SELECT * FROM RCM_ReplicationLinkStatus
WHERE UpdateTime >@cutoffTime
```

### <a name="check-sql-maintenance-mode"></a>проверка режима обслуживания SQL.

```sql
SELECT * FROM ServerData
WHERE Status = 120
```

## <a name="next-steps"></a>Дальнейшие действия

- [Повторная инициализация репликации SQL](sql-replication-reinit.md)
- [Производительность SQL](sql-performance.md)
- [Конфигурация SQL](sql-configuration.md)
