---
title: Необходимые условия для ведения отчетов
titleSuffix: Configuration Manager
description: Сведения о различных зависимостях, которые влияют на использование отчетов в Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9cc508a5-5023-4833-b776-ae9a6971138f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e08833a5ef560a0f958fe68b4ade0d4717dffc73
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703522"
---
# <a name="prerequisites-for-reporting-in-configuration-manager"></a>Необходимые условия для создания отчетов в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Инструмент отчетов в Configuration Manager имеет следующие зависимости.

- Службы SQL Server Reporting Services
- Точка служб отчетов
- Сервер отчетов Power BI (необязательно, начиная с версии 2002)

## <a name="sql-server-reporting-services"></a>Службы SQL Server Reporting Services

Перед использованием отчетов в Configuration Manager необходимо установить и настроить службы SQL Server Reporting Services.

Дополнительные сведения о планировании и развертывании Reporting Services см. в статье [Установка SQL Server Reporting Services](https://docs.microsoft.com/sql/reporting-services/install-windows/install-reporting-services).

Установите базу данных Reporting Services на экземпляре по умолчанию или на именованном экземпляре 64-разрядной версии SQL Server. Экземпляр SQL Server может размещаться на одном компьютере с сервером системы сайта или на удаленном компьютере.

Configuration Manager поддерживает те же версии SQL Server для создания отчетов, что и для базы данных сайта. Дополнительные сведения см. в разделе [Поддерживаемые версии SQL Server](../../plan-design/configs/support-for-sql-server-versions.md#bkmk_SQLVersions).

## <a name="reporting-services-point"></a>Точка служб отчетов

Чтобы создавать отчеты в Configuration Manager, необходимо настроить роль системы сайта "Точка служб отчетов".

Дополнительные сведения см. в разделе [Необходимые компоненты для сайта и системы сайта](../../plan-design/configs/site-and-site-system-prerequisites.md#bkmk_2012RSpoint).

## <a name="power-bi-report-server"></a>Сервер отчетов Power BI

Начиная с версии 2002, можно интегрировать отчеты с сервером отчетов Power BI. Дополнительные сведения, включая предварительные требования, см. в статье [Интеграция с сервером отчетов Power BI](powerbi-report-server.md).

## <a name="next-steps"></a>Дальнейшие шаги

[Настройка отчетов](configuring-reporting.md)
