---
title: Сбор данных диагностики
titleSuffix: Configuration Manager
description: Узнайте, как Configuration Manager собирает собственные данные диагностики и сведения об использовании.
ms.date: 12/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: becfa825-b19f-448c-ab82-bb929255e4ae
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ca40891c840e954f2828833c179f01bcbc6e7448
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688472"
---
# <a name="how-configuration-manager-collects-diagnostics-and-usage-data"></a>Как Configuration Manager собирает данные диагностики и сведения об использовании

*Область применения: Configuration Manager (Current Branch)*

Для сбора данных диагностики и сведений об использовании для Configuration Manager каждый первичный сайт еженедельно выполняет запросы SQL Server. В иерархии с несколькими сайтами данные реплицируются на сайт центра администрирования.  

На верхнем сайте иерархии точка подключения службы отправляет эти сведения при выполнении проверки на наличие обновлений. Режим точки подключения службы определяет способ передачи данных.

- **Сетевое**. Один раз в неделю данные о диагностике и использовании автоматически отправляются из точки подключения службы в облачную службу.

- **Автономное**. Данные о диагностике и использовании передаются вручную с помощью [инструмента подключения службы](../../servers/manage/use-the-service-connection-tool.md).

Дополнительные сведения см. в статье [Точки подключения службы](../../servers/deploy/configure/about-the-service-connection-point.md).

> [!div class="nextstepaction"]
> [Как просмотреть данные о диагностике и использовании](view-diagnostics-and-usage-data.md)
