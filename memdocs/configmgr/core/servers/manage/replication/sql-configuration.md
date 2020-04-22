---
title: Конфигурация SQL
titleSuffix: Configuration Manager
description: Используйте эту схему, чтобы начать устранение неполадок в конфигурации SQL для Configuration Manager
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 95ab8cbd-0807-4422-823a-f5f9314ba623
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b909d992dc16b6e786c62143347ed420d913dbc5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707622"
---
# <a name="sql-configuration"></a>Конфигурация SQL

В иерархии с несколькими сайтами Configuration Manager использует репликацию SQL для обмена данными между сайтами. Дополнительные сведения см. в разделе [Репликация базы данных](../../../plan-design/hierarchy/database-replication.md).

Используйте следующую схему, чтобы начать устранение неполадок конфигурации SQL, связанной с SQL Service Broker:

![Схема для устранения неполадок конфигурации SQL](media/sql-configuration.svg)

## <a name="queries"></a>Запросы

Эта схема содержит следующие запросы и действия:

### <a name="check-if-sql-can-deliver-ssb-messages"></a>проверка, может ли SQL доставлять SSB-сообщения;

```sql
SELECT transmission_status, *
FROM sys.transmission_queue
ORDER BY enqueue_time DESC
```

## <a name="remediation-actions"></a>Действия по исправлению

### <a name="remediate-the-issues-reported-from-transmission_status"></a>устранение неполадок, обнаруженных в результате передачи данных_статуса.

Распространенные проблемы:

- Настройка брандмауэра
- Сетевая конфигурация
- Сертификат SSB неправильно настроен

### <a name="run-sql-profiler-to-trace-ssb-events"></a>Запустите SQL Profiler для отслеживания событий SSB

Запустите SQL Profiler для базы данных CAS и основного сайта, чтобы отследить события, связанные с компонентом SQL Service Broker:

- **Вход в систему Audit Broker**
- **Беседа Audit Broker**
- События в категории**Брокер**
