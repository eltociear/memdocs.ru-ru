---
title: Заявление о конфиденциальности для командлетов
titleSuffix: Configuration Manager
description: Узнайте, как корпорация Майкрософт собирает и использует данные, связанные с командлетами Configuration Manager
ms.date: 01/3/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bec00fb4-1ac0-4e49-b330-0871b3722459
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 551a8086894f877d07c57fbe2848c2befacfc5b5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695752"
---
# <a name="configuration-manager-cmdlet-library-privacy-statement"></a>Заявление о конфиденциальности — библиотека командлетов Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

В настоящем заявлении о конфиденциальности описаны функции библиотеки командлетов Configuration Manager.  

## <a name="usage-data"></a>Данные об использовании  

#### <a name="what-this-feature-does"></a>Назначение этой функции

Библиотека командлетов Configuration Manager позволяет управлять иерархией Configuration Manager с помощью командлетов и скриптов Windows PowerShell. Библиотека командлетов собирает сведения об использовании командлетов в библиотеке, чтобы определить тенденции и шаблоны использования. Библиотека командлетов также собирает сведения о типах и количестве ошибок, возникших при использовании командлетов.  

#### <a name="information-collected-processed-or-transmitted"></a>Собираемые, обрабатываемые и передаваемые сведения
   
Собираемые данные об использовании включают сведения о запуске, остановке и завершении командлетов, запуске нерекомендуемых командлетов и метриках действий для операций поставщика SMS, связанных с командлетами. Эти сведения не позволяют установить вашу личность. Собранные сведения об ошибках содержат ошибки, возвращенные командлетами, и сведения об ошибках для исключений Некоторые подробные отчеты об ошибках могут непреднамеренно содержать отдельные идентификаторы, например серийный номер устройства, подключенного к компьютеру. Библиотека командлетов фильтрует и анонимизирует сведения, содержащиеся в отчетах об ошибках, чтобы удалить отдельные идентификаторы перед их отправкой в Майкрософт.  

#### <a name="use-of-information"></a>Использование сведений
   
Корпорация Майкрософт использует эти сведения для повышения качества, безопасности и целостности предлагаемых продуктов и служб.  

#### <a name="choicecontrol"></a>Выбор/управление   

эта функция данных об использовании включена по умолчанию. Библиотека командлетов Configuration Manager имеет два раздела реестра для управления этой функцией.  

 Чтобы полностью отказаться от использования, задайте следующие два значения разделов реестра. Они соответствуют каждому из поставщиков трассировки событий для Windows (ETW):  

- HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Provider:CeipLevel=0 (отказ от сбора данных об использовании для поставщика драйверов)  

- HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Cmdlets:CeipLevel=0 (отказ от сбора данных об использовании для командлетов)  

  Изменения параметров сбора данных об использовании зависят от компьютера, на котором они были выполнены.  


## <a name="next-steps"></a>Дальнейшие шаги

[Документация по библиотеке командлетов Configuration Manager](https://docs.microsoft.com/powershell/sccm/configurationmanager/).   
