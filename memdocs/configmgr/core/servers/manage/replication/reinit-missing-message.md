---
title: Повторная инициализация отсутствующего сообщения
titleSuffix: Configuration Manager
description: Используйте эту схему, чтобы начать устранение неполадок с отсутствующим сообщением с помощью повторной инициализации репликации SQL в Configuration Manager
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 39a3001e-2df5-4b36-bd83-4f1d21dda335
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1e640c3dd756d96a58e8b54d6056d2adbb7bb99c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703982"
---
# <a name="reinit-missing-message"></a>Повторная инициализация отсутствующего сообщения

В иерархии с несколькими сайтами Configuration Manager использует репликацию SQL для обмена данными между сайтами. Дополнительные сведения см. в разделе [Репликация базы данных](../../../plan-design/hierarchy/database-replication.md).

Используйте следующую схему, чтобы начать устранение неполадок с отсутствующим сообщением с помощью повторной инициализации репликации SQL (reinit):

![Схема устранения неполадок с отсутствующим сообщением во время инициализации](media/reinit-missing-message.svg)

## <a name="queries"></a>Запросы

Эта схема использует следующие запросы:

### <a name="check-if-site-replication-hasnt-finished-reinit"></a>проверка, не завершилась ли повторная инициализация репликации сайта;

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
```

### <a name="get-the-trackingguid--status-from-subscriber-site"></a>получение руководства по отслеживанию и статуса с сайта абонента;

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
```

### <a name="get-the-trackingguid--status-from-the-publishing-site"></a>получение руководства по отслеживанию и статуса с сайта публикации.

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
WHERE RequestTrackingGUID=@trackingGuid
```

## <a name="remediation-actions"></a>Действия по исправлению

### <a name="version-1902-and-later"></a>версия 1902 и более поздние версии

Чтобы обнаружить ошибку и выполнить повторную инициализацию, запустите [Replication Link Analyzer](../monitor-replication.md#BKMK_RLA).

### <a name="version-1810-and-earlier"></a>версия 1810 и более ранние версии

Запустите следующий SQL-запрос, чтобы получить `ReplicationGroupID`:

```sql
SELECT rd.ID AS ReplicationGroupID from ReplicationData rd
INNER JOIN RCM_DrsInitializationTracking it ON rd.ReplicationGroup = it.ReplicationGroup
WHERE it.RequestTrackingGUID=@trackingGuid
```

Затем используйте `InitializeData` метод для `SMS_ReplicationGroup` класса WMI со следующими значениями:

- ReplicationGroupID: из SQL-запроса выше
- SiteCode1: родительский сайт
- SiteCode2: дочерний сайт

Дополнительные сведения см. в разделе [Метод InitializeData в классе SMS_ReplicationGroup](../../../../develop/reference/core/servers/configure/initializedata-method-in-class-sms_replicationgroup.md).

#### <a name="example"></a>Пример

```PowerShell
Invoke-WmiMethod –Namespace "root\sms\site_CAS" -Class SMS_ReplicationGroup –Name InitializeData -ArgumentList "20", "CAS", "PR1"
```

## <a name="next-steps"></a>Дальнейшие действия

- [Повторная инициализация репликации SQL](sql-replication-reinit.md)
