---
title: Средство Power Viewer
titleSuffix: Configuration Manager
description: Используйте средство Power Viewer, чтобы просмотреть состояние функции управления питанием в клиенте Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8143e3bf-d6bd-4c69-aec1-e6989cf2ecd9
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: bcab26abe2e2a9062eda5ff80ea958010e8a7f62
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707572"
---
# <a name="power-viewer-tool"></a>Средство Power Viewer

*Область применения: Configuration Manager (Current Branch)*

Power Viewer является одним из [средств Configuration Manager](tools.md). Используйте его, чтобы просмотреть состояние функции управления питанием в клиенте Configuration Manager.

Запустите **PowerVwr.exe** с правами администратора. При запуске средство отображает возможности электропитания и параметры питания локального компьютера на вкладке **Power Config** (Конфигурация питания). 

Чтобы просмотреть данные управления питанием удаленного компьютера, сделайте следующее:  

1. Перейдите в меню **Файл** и выберите пункт **Подключить**. 

2. Введите имя в поле **Компьютер**, а также **Имя пользователя** и **Пароль** при необходимости. 

В Power Viewer доступны три вкладки:  

- **Конфигурация питания** — просмотр возможностей и параметров электропитания на целевом компьютере.  

- **Ежедневная активность** — просмотр диаграмм ежедневных действий клиента, включая следующие сведения:  

    - **Компьютер включен**: состояние питания компьютера за один день. Спящий режим считается отключением питания.  

    - **Монитор включен**: включенное или отключенное состояние монитора за один день.  

    - **Активность пользователей**: данные об активности пользователей за один день.  

- **События управления питанием**: просмотр всех ежедневных событий питания. Клиент составляет сводку по этим событиям в 00:00. На основе этих сводных данных создается ежедневная диаграмма активности.  
