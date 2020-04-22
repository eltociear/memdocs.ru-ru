---
title: Данные о диагностике и использовании
titleSuffix: Configuration Manager
description: Дополнительные сведения о данных о диагностике и использовании, собираемых Configuration Manager для собственных компонентов.
ms.date: 12/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 88ac4e55-d47b-4c94-b9c3-704c6a48b845
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6fff68eaad52f753d27971562a4bbfaa47a6cf6e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81691352"
---
# <a name="diagnostics-and-usage-data-for-configuration-manager"></a>Данные о диагностике и использовании для Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Configuration Manager собирает собственные данные о диагностике и использовании, которые корпорация Майкрософт использует для улучшения процесса установки, качества и безопасности будущих выпусков.  

Каждая иерархия Configuration Manager включает данные о диагностике и использовании. Они составляются посредством запросов SQL Server, выполняемых еженедельно на каждом первичном сайте и сайте центра администрирования (CAS). Если иерархия использует (CAS), дочерние первичные сайты реплицируют свои данные на этот (CAS). На верхнем сайте иерархии [точка подключения службы](../../servers/deploy/configure/about-the-service-connection-point.md) отправляет эти сведения при выполнении проверки на наличие обновлений. Если точка подключения службы находится в автономном режиме, сведения передаются с помощью [средства подключения службы](../../servers/manage/use-the-service-connection-tool.md).

> [!NOTE]  
> Configuration Manager собирает данные только из базы данных SQL Server сайта, не получая их непосредственно от клиентов или серверов сайта.  

Дополнительные сведения см. в [Заявлении о конфиденциальности корпорации Майкрософт](https://go.microsoft.com/fwlink/?LinkID=626527).  

> [!div class="nextstepaction"]
> [Обработка данных о диагностике и использовании корпорацией Майкрософт](how-diagnostics-and-usage-data-is-used.md)
