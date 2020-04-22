---
title: Управление запросами
titleSuffix: Configuration Manager
description: Сведения об управлении запросами. Содержит подробную справочную таблицу.
ms.date: 04/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e562e2a0-8df8-4952-952f-e8c38461c612
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 37050a3a96b732df3f56269592e049077008ab2b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694472"
---
# <a name="how-to-manage-queries-in-configuration-manager"></a>Управление запросами в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

В статье описано, как управлять запросами в Configuration Manager.  

 Сведения о том, как создавать запросы, см. в разделе [Создание запросов](../../../core/servers/manage/create-queries.md).  

## <a name="manage-queries"></a>Управление запросами
 В рабочей области **Мониторинг** последовательно выберите **Запросы**, запрос для управления и задачу управления.  

 В следующей таблице приведены сведения об этих задачах управления.  

|Задача управления|Сведения| 
|---------------------|-------------|
|**Выполнить**|Выполнение выбранного запроса и отображение результатов на консоли Configuration Manager.|
|**Установить клиент**|Открытие компонента **Мастер установки клиента**, который позволяет установить клиент Configuration Manager на компьютерах, определенных при выполнении выбранного запроса.<br /><br /> Этот параметр недоступен для запросов, определяющих мобильные устройства, пользователей или группы пользователей. <br /><br /> Дополнительные сведения об установке клиентов Configuration Manager с помощью принудительной установки см. в статье [Развертывание клиентов на компьютерах Windows](../../clients/deploy/deploy-clients-to-windows-computers.md).| 
|**Экспортировать**|Открытие **мастера экспорта объектов**. Экспорт запроса в MOF-файл, который затем можно импортировать на другой сайт.
|**Переместить**|Открытие диалогового окна **Перемещение выбранных элементов**. В этом диалоговом окне можно переместить выбранный запрос в папку, созданную в узле **Запросы**.|

## <a name="next-steps"></a>Дальнейшие шаги 
 [Создание запросов](../../../core/servers/manage/create-queries.md)
