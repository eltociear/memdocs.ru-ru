---
title: Повторная инициализация глобальных данных
titleSuffix: Configuration Manager
description: Используйте эту схему, чтобы начать устранение неполадок повторной инициализации репликации SQL для глобальных данных в иерархии Configuration Manager
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d36622c0-776c-493b-971a-4a586fc394d4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9fed8a5b257591aa95fcd53b4e12a82249fce762
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694302"
---
# <a name="troubleshoot-global-data-reinit"></a>Устранение неполадок при инициализации глобальных данных

В иерархии с несколькими сайтами Configuration Manager использует репликацию SQL для обмена данными между сайтами. Дополнительные сведения см. в разделе [Репликация базы данных](../../../plan-design/hierarchy/database-replication.md).

Используйте следующую схему, чтобы начать устранение неполадок повторной инициализации репликации SQL (reinit) для глобальных данных в иерархии Configuration Manager:

![Схема устранения неполадок при инициализации глобальных данных](media/global-data-reinit.svg)

## <a name="queries"></a>Запросы

Эта схема использует следующие запросы:

### <a name="check-if-site-replication-hasnt-finished-reinit"></a>проверка, не завершилась ли повторная инициализация репликации сайта;

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N`Global'
```

### <a name="get-the-trackingguid--status-from-the-primary-site"></a>получение руководства по отслеживанию и статуса с основного сайта;

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N`Global'
```

### <a name="get-the-trackingguid--status-from-the-cas"></a>получение руководства по отслеживанию и статуса из CAS;

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
WHERE RequestTrackingGUID=@trackingGuid
```

### <a name="check-request-status-for-the-tracking-id"></a>проверка статуса запроса для идентификатора отслеживания.

```sql
SELECT Status FROM RCM_InitPackageRequest
WHERE RequestTrackingGUID=@trackGuid
```

## <a name="next-steps"></a>Дальнейшие действия

- [Повторная инициализация отсутствующего сообщения](reinit-missing-message.md)
