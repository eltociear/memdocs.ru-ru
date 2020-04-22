---
title: Устаревшие компоненты для серверов сайта
titleSuffix: Configuration Manager
description: Сведения о продуктах и операционных системах, которые Configuration Manager больше не поддерживает для серверов сайта.
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d53ac075-438b-41da-ab85-42f33982da0c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2b6f9dfae2eaa4e7fac4cc9b059b608de3c1386a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702572"
---
# <a name="removed-and-deprecated-for-configuration-manager-site-servers"></a>Удаленные и устаревшие компоненты для серверов сайта Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Статья приводит продукты и операционные системы, поддержка которых для серверов сайта Configuration Manager прекращена или будет прекращена в будущем обновлении (нерекомендуемые продукты и системы). Позволяет заранее узнать о будущих изменениях, которые могут повлиять на использование Configuration Manager.  

Эта информация может измениться в будущем. Она может не включать все устаревшие функции, продукты или операционные системы.  

## <a name="server-os"></a>Серверная ОС  

|Операционные системы|Первое объявление об устаревании|Поддержка удалена|
|-|-|-|
|Windows Server 2008 R2 с пакетом обновления 1 (SP1)|10 июля 2015 г.| Версия 1702|
|Windows Server 2008 с пакетом обновления 2 (SP2)|10 июля 2015 г.|Версия 1511|

## <a name="sql-server"></a>SQL Server

|Версии SQL Server|Первое объявление об устаревании|Поддержка удалена|
|-|-|-|
|SQL Server 2008 R2|10 июля 2015 г.|Версия 1702|
|SQL Server 2008|10 июля 2015 г.|Версия 1511|

Если вы намерены обновить версию SQL Server, мы рекомендуем использовать перечисленные здесь методы от простых к более сложным.

1. [Обновите SQL Server на месте](../../../servers/manage/upgrade-on-premises-infrastructure.md#BKMK_SupConfigUpgradeDBSrv) (рекомендуется).  

2. Установите новую версию Windows на новом компьютере. Затем [воспользуйтесь функцией перемещения базы данных](../../../servers/manage/modify-your-infrastructure.md#bkmk_dbconfig) в установщике Configuration Manager, чтобы настроить новый SQL Server для сервера сайта.  

3. Используйте функции [резервного копирования и восстановления](../../../servers/manage/backup-and-recovery.md).  

## <a name="next-steps"></a>Дальнейшие шаги

Дополнительные сведения см. в следующих статьях:

- [Удаленные и устаревшие компоненты](removed-and-deprecated.md)  

- [Жизненный цикл службы поддержки Майкрософт](https://support.microsoft.com/lifecycle)  

- [Поддержка версий Configuration Manager (Current Branch)](../../../servers/manage/current-branch-versions-supported.md)  
