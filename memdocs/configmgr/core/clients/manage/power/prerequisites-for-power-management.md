---
title: Необходимые условия для управления питанием
titleSuffix: Configuration Manager
description: Ознакомьтесь с необходимыми условиями для управления питанием в Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 9c062f13-3c1f-4621-9cae-de0e322aa03f
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: a816d333d96dba6cb1c38f6499ccac78e2db8a3c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696522"
---
# <a name="prerequisites-for-power-management-in-configuration-manager"></a>Необходимые условия для управления питанием в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Функция управления питанием в Configuration Manager имеет внешние зависимости и зависимости в пределах продукта.  

## <a name="dependencies-external-to-configuration-manager"></a>Внешние зависимости Configuration Manager  
 Приведенная ниже таблица содержит список внешних зависимостей Configuration Manager для использования функций управления питанием.  

|Зависимость|Дополнительные сведения|  
|----------------|----------------------|  
|Клиентские компьютеры должны поддерживать требуемые режимы питания.|Чтобы использовать все возможности функций управления питанием, клиентские компьютеры должны поддерживать спящий режим, режим гибернации, выход из спящего режима и выход из режима гибернации. Соответствующие сведения о поддержке содержатся в отчете **Возможности электропитания** . Дополнительные сведения см. в подразделе [Отчет "Возможности электропитания"](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md#BKMK_Capabilites) раздела [Отслеживание и планирование управления питанием](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md).|  

## <a name="configuration-manager-dependencies"></a>Зависимости Configuration Manager  
 Приведенная ниже таблица содержит список зависимостей в Configuration Manager для использования функций управления питанием.  

|Зависимость|Дополнительные сведения|  
|----------------|----------------------|  
|Прежде чем можно будет создавать схемы управления питанием и отслеживать их выполнение, необходимо включить функцию управления питанием.|Сведения о включении и настройке управления питанием см. в разделе [Настройка функций управления питанием](../../../../core/clients/manage/power/configuring-power-management.md).|  
|Точка служб отчетов|Прежде чем можно будет просматривать отчеты управления питанием, необходимо настроить точку служб отчетов. Дополнительные сведения см. в разделе [Общие сведения об отчетах](../../../servers/manage/introduction-to-reporting.md).|  
