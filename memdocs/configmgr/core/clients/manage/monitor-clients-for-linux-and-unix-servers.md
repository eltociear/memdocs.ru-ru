---
title: Мониторинг клиентов Linux и UNIX
titleSuffix: Configuration Manager
description: Мониторинг клиентов для серверов Linux и UNIX в Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: d827cf91-b18f-4ee7-b538-24ba6f003ab9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d2ea3a0b630e1710aeaf74a4349f202806d45039
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696772"
---
# <a name="how-to-monitor-clients-for-linux-and-unix-servers-in-configuration-manager"></a>Мониторинг клиентов для серверов Linux и UNIX в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

> [!Important]  
> Начиная с версии 1902, Configuration Manager не поддерживает клиенты Linux и UNIX. 
> 
> Вы можете управлять серверами Linux с помощью портала управления Microsoft Azure. Решения Azure располагают расширенной поддержкой Linux, которая в большинстве случаев превышает функциональные возможности Configuration Manager, включая полное управление исправлениями для Linux.

Для просмотра сведений с серверов Linux и UNIX в консоли Configuration Manager используются те же методы, что и для просмотра сведений с клиентских компьютеров под управлением Windows.  

 Для просмотра доступны следующие данные.  

- Сведения о состоянии клиентов на панелях мониторинга консоли Configuration Manager  

- Сведения о клиентах в отчетах Configuration Manager по умолчанию  

- Сведения об инвентаризации в обозревателе ресурсов  

  В следующих разделах описывается, как получить эти сведения из обозревателя ресурсов и отчетов.  

##  <a name="use-resource-explorer-to-view-inventory-for-linux-and-unix-servers"></a><a name="BKMK_UseResourceExpforLnU"></a> Использование обозревателя ресурсов для просмотра данных инвентаризации для серверов Linux и UNIX  

 После того как клиент Configuration Manager отправит данные инвентаризации оборудования на сайт Configuration Manager, эти сведения вы можете просмотреть с помощью обозревателя ресурсов. Клиент Configuration Manager для Linux и UNIX не добавляет в обозреватель ресурсов новые классы или представления для инвентаризации. Данные инвентаризации Linux и UNIX сопоставляются с существующими WMI-классами. С помощью обозревателя ресурсов вы можете просмотреть сведения об инвентаризации для серверов Linux и UNIX в классификациях на основе Windows.  

 Например, вы можете составить список всех изначально установленных программ, обнаруженных на серверах Linux и UNIX. Примерами изначально установленных программ являются **.rpms** в Linux или **.pkgs** в Solaris. После того как клиент Linux или UNIX отправит данные инвентаризации, в обозревателе ресурсов в консоли Configuration Manager вы можете просмотреть список всех изначально установленных программ UNIX или Linux.  

 Сведения об использовании обозревателя ресурсов см. в статье [Использование обозревателя ресурсов для просмотра данных инвентаризации оборудования](../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md).  

##  <a name="how-to-use-reports-to-view-information-for-linux-and-unix-servers"></a><a name="BKMK_UseReportsforLnU"></a> Использование отчетов для просмотра сведений для серверов Linux и UNIX  
 Отчеты для Configuration Manager содержат сведения с серверов Linux и UNIX, а также сведения с компьютеров под управлением Windows. Для интеграции данных в отчетах Linux и UNIX выполнять дополнительные настройки не требуется.  

 Например, при выполнении отчета с именем «Количество версий операционной системы» в нем отображается список других операционных систем и количество клиентов, работающих под управлением каждой операционной системы. Отчет основан на данных инвентаризации оборудования, которые были отправлены различными клиентами Configuration Manager, работающими в разных операционных системах.  

 Кроме того, вы можете создать настраиваемые отчеты, связанные с данными серверов Linux и UNIX. Свойство **Caption** класса инвентаризации оборудования **Operating System** является полезным атрибутом, который вы можете использовать для идентификации конкретных операционных систем в запросе отчета.  

 Дополнительные сведения об отчетах в Configuration Manager см. в разделе [Общие сведения об отчетах](../../servers/manage/introduction-to-reporting.md).  
