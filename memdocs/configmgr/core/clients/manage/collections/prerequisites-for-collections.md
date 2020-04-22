---
title: Предварительные требования для коллекций
titleSuffix: Configuration Manager
description: Сведения о предварительных требованиях для коллекций в Configuration Manager.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a53e4cf1-518a-4210-9c16-022c4261d2fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 313c3183cd6401390d743575ba513026a3e3f607
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695542"
---
# <a name="prerequisites-for-collections-in-configuration-manager"></a>Предварительные требования для коллекций в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Коллекции в Configuration Manager содержат только зависимости в пределах продукта.  

## <a name="configuration-manager-dependencies"></a>Зависимости Configuration Manager  

|Зависимость|Дополнительные сведения|  
|----------------|----------------------|  
|Точка служб отчетов|Чтобы создавать отчеты по коллекциям, необходимо установить роль системы сайта "точка служб отчетов". Дополнительные сведения см. в разделе [Общие сведения об отчетах](../../../servers/manage/introduction-to-reporting.md).|  
|Для управления коллекциями должны быть предоставлены определенные разрешения системы безопасности|Для работы с параметрами соответствия необходимо иметь следующие разрешения.<br /><br /> — Для создания коллекций и управления ими: **Создать**, **Удалить**, **Изменить**, **Изменить папку**, **Переместить объект**, **Чтение** и **Чтение ресурса** для объекта **Коллекция**.<br /><br /> — Для управления параметрами коллекции: **Изменить параметр коллекции** для объекта **Коллекция**.<br /><br /> Разрешение **Изменить папку** требуется для всех папок коллекции, включая корневую папку.|  
