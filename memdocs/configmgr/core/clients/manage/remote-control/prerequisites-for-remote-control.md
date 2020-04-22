---
title: Предварительные требования для удаленного управления
titleSuffix: Configuration Manager
description: Сведения о предварительных требованиях для удаленного управления в Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: c1b2057e-b74f-43fa-a293-763a8f866d3d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f19f8799dd90fc61c0bfeeee1dc60125ba491fef
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696422"
---
# <a name="prerequisites-for-remote-control-in-configuration-manager"></a>Предварительные требования для удаленного управления в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Функция удаленного управления в Configuration Manager имеет внешние зависимости и зависимости в пределах продукта.  

## <a name="dependencies-external-to-configuration-manager"></a>Внешние зависимости Configuration Manager  

|Зависимость|Дополнительные сведения|  
|----------------|----------------------|  
|Драйвер видеоадаптера компьютера|Чтобы обеспечить оптимальную работу функции удаленного управления, на клиентских компьютерах должны быть установлены последние версии драйверов.|  

 Устройства, работающие под управлением Windows Embedded, Windows Embedded for Point of Service (POS) и Windows Fundamentals for Legacy PCs, не поддерживают средство просмотра удаленного управления, однако поддерживают клиент удаленного управления.  

 Функцию удаленного управления Configuration Manager нельзя использовать для удаленного администрирования клиентских компьютеров, где выполняется Systems Management Server 2003 или Configuration Manager 2007.  

> [!NOTE]  
>  Службы Windows не требуются в качестве внешней зависимости для удаленного управления.  

### <a name="supported-operating-systems-for-the-remote-control-viewer"></a>Поддерживаемые операционные системы для средства просмотра удаленного управления  
Средство просмотра удаленного управления поддерживается во всех операционных системах, которые поддерживает консоль Configuration Manager. Дополнительные сведения см. в статье [Поддерживаемые конфигурации консолей Configuration Manager](../../../../core/plan-design/configs/supported-operating-systems-consoles.md).   

## <a name="configuration-manager-dependencies"></a>Зависимости Configuration Manager  

|Зависимость|Дополнительные сведения|  
|----------------|----------------------|  
|Функция удаленного управления должна быть включена для клиентов|Функция удаленного управления не включается по умолчанию при установке Configuration Manager. Сведения о включении и настройке удаленного управления см. в разделе [Настройка удаленного управления](../../../../core/clients/manage/remote-control/configuring-remote-control.md).|  
|Точка служб отчетов|Чтобы настроить создание отчетов по удаленному управлению, необходимо установить роль системы сайта "точка служб отчетов". Дополнительные сведения см. в разделе [Общие сведения об отчетах](../../../servers/manage/introduction-to-reporting.md).|  
|Разрешения безопасности для управления функцией удаленного управления|Для получения доступа к ресурсам коллекции и запуска сеанса удаленного управления из консоли Configuration Manager: права **Чтение**, **Чтение ресурса** и **Удаленное управление** для объекта **Коллекция**.<br /><br /> Роль безопасности **Оператор средств удаленного управления** включает все разрешения, необходимые для управления этой функцией в Configuration Manager.<br /><br /> Дополнительные сведения см. в разделе [Настройка администрирования на основе ролей для Configuration Manager](../../../../core/servers/deploy/configure/configure-role-based-administration.md).<br /><br /> Кроме того, разрешенным средствам просмотра необходимо предоставить разрешение на использование удаленного управления. Для этого добавьте этих пользователей в список **Пользователи средств удаленного управления и удаленного помощника** в параметрах **удаленных средств** клиента.
