---
title: Устранение неполадок репликации SQL
titleSuffix: Configuration Manager
description: Используйте эти схемы, чтобы понять и устранить неполадки репликации SQL между сайтами Configuration Manager
ms.date: 02/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 71d7430e-c5aa-485b-8dc0-c80fd8f29f17
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 202a3360b5e04d66ada0d3b47ddd4638c2197167
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703992"
---
# <a name="troubleshoot-sql-replication"></a>Устранение неполадок репликации SQL

В иерархии с несколькими сайтами Configuration Manager использует репликацию SQL для обмена данными между сайтами. Дополнительные сведения см. в разделе [Репликация базы данных](../../../plan-design/hierarchy/database-replication.md).

Чтобы лучше понять и помочь в устранении неполадок, связанных с репликацией SQL, используйте эти схемы.

- [Репликация SQL](sql-replication.md)
- [Конфигурация SQL](sql-configuration.md)
- [Производительность SQL](sql-performance.md)
- [Повторная инициализация репликации SQL](sql-replication-reinit.md)
- [Повторная инициализация глобальных данных](global-data-reinit.md)
- [Повторная инициализация данных сайта](site-data-reinit.md)
- [Повторная инициализация отсутствующего сообщения](reinit-missing-message.md)

Эти схемы устранения неполадок взаимосвязаны. Используйте следующую схему, чтобы понять их связи:

![Обзор схемы процесса устранения неполадок при репликации SQL](media/overview.png)

<!-- PNG used instead of SVG because of weird blankspace in the SVG. The SVG file exists in the same location. -->

Дополнительные сведения см. в следующих сериях блогов Службы поддержки Майкрософт:

- [Внутренние компоненты синхронизации Configuration Manager DRS](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-drs-synchronization-internals/ba-p/1154317)
- [Служба репликации данных Configuration Manager 2012 (DRS) Unleashed](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-2012-data-replication-service-drs-unleashed/ba-p/339916)
- [Configuration Manager 2012 DRS — Часто задаваемые вопросы по устранению неполадок](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-2012-drs-troubleshooting-faqs/ba-p/339934)
- [Внутренние компоненты инициализации Configuration Manager 2012 DRS](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-2012-drs-initialization-internals/ba-p/339948)
- [Configuration Manager 2012: Проблемы с сертификатами Service Broker DRS и SQL](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-2012-drs-and-sql-service-broker-certificate-issues/ba-p/339910)
