---
title: Передача данных между сайтами
titleSuffix: Configuration Manager
description: Сведения о том, как Configuration Manager перемещает данные между сайтами и как можно управлять передачей данных по сети.
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: dc526e8d-fac3-4bb5-b206-03ad29b0ae11
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 6b6d4eab77d0543f9001cef2c1e2b618ba3e4328
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703622"
---
# <a name="data-transfers-between-sites"></a>Передача данных между сайтами

*Область применения: Configuration Manager (Current Branch)*

Configuration Manager использует *файловую репликацию* и *репликацию базы данных* для передачи разных типов данных между сайтами. Сведения о том, как Configuration Manager перемещает данные между сайтами и как можно управлять передачей данных по сети.  

## <a name="types-of-replication"></a>Типы репликации

### <a name="file-based-replication"></a><a name="bkmk_fileroute" /> Репликация на основе файлов

Configuration Manager использует файловую репликацию для передачи файловых данных между сайтами. Эти данные включают в себя приложения и пакеты, которые требуется развернуть в точках распространения на дочерних сайтах. Он также управляет необработанными записями данных обнаружения, передаваемых сайтом на родительский сайт, а затем обрабатывает их.  

Дополнительные сведения см. в разделе [Репликация на основе файлов](file-based-replication.md).

### <a name="database-replication"></a><a name="bkmk_dbrep" /> Репликация базы данных

Репликация базы данных Configuration Manager использует SQL Server для передачи данных. Он использует этот метод для объединения изменений в базе данных своего сайта с информацией из базы данных других сайтов в иерархии.

Дополнительные сведения см. в разделе [Репликация базы данных](database-replication.md).

Дополнительные сведения об устранении неполадок репликации SQL см. в разделе[Устранение неполадок репликации SQL](../../servers/manage/replication/overview.md).

## <a name="see-also"></a>См. также

[Монитор репликации](../../servers/manage/monitor-replication.md)
