---
title: Просмотр данных диагностики
titleSuffix: Configuration Manager
description: Просмотр данных о диагностике и использовании, чтобы убедиться в отсутствии конфиденциальных сведений в иерархии Configuration Manager.
ms.date: 12/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 594eb284-0d93-4c5d-9ae6-f0f71203682a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 993a3549ddca4c2b5ae1dbbfc0346f28b9c3083e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692742"
---
# <a name="how-to-view-diagnostics-and-usage-data-for-configuration-manager"></a>Просмотр данных о диагностике и использовании для Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Вы можете просмотреть данные о диагностике и использовании, полученные из иерархии Configuration Manager, чтобы убедиться в отсутствии конфиденциальных сведений или личных данных. Сайт сводит и сохраняет свои диагностические данные в таблице **TEL_TelemetryResults** базы данных сайта. Он форматирует данные эффективным способом, пригодным для программного использования.

Сведения в этой статье помогут вам просмотреть точные данные, отправляемые в корпорацию Майкрософт. Они не предназначены для использования в других целях, таких как анализ данных.  

## <a name="view-data-in-database"></a>Просмотр данных в базе данных

Следующую команду SQL можно использовать для просмотра содержимого этой таблицы — непосредственно отправляемых данных:  

``` SQL
SELECT * FROM TEL_TelemetryResults
```

## <a name="export-the-data"></a>Экспорт данных

Когда точка подключения службы находится в автономном режиме, вы можете применять средство подключения службы для экспорта текущих данных в файл с разделителями-запятыми (CSV). Запустите инструмент подключения службы на точке подключения службы с параметром **-Export**.

Дополнительные сведения см. в статье [Использование инструмента подключения службы](../../servers/manage/use-the-service-connection-tool.md).

## <a name="one-way-hashes"></a><a name="bkmk_hashes"></a> Односторонние хэши

Некоторые данные состоят из строк случайных буквенно-цифровых символов. Configuration Manager использует алгоритм SHA-256 для создания односторонних хэшей. Этот процесс гарантирует, что корпорация Майкрософт не получит потенциально конфиденциальные данные. Хэшированные данные по-прежнему можно использовать для корреляции и сравнения.

Например, вместо сбора имен таблиц в базе данных сайта для каждого из них записывается односторонний хэш. Такое поведение гарантирует, что имена пользовательских таблиц не будут видны. Затем корпорация Майкрософт выполняет тот же односторонний хэш-процесс имен таблиц SQL по умолчанию. Сравнение результатов двух запросов определяет отклонение схемы базы данных от значения по умолчанию для продукта. Затем эти сведения используются для улучшения обновлений, требующих внесения изменений в схему SQL.  

При просмотре необработанных данных в каждой строке данных будет отображаться общее хэшированное значение. Этот хэш — идентификатор иерархии. Он используется для корреляции данных с соответствующей иерархией, не идентифицируя клиент или источник.

### <a name="how-the-one-way-hash-works"></a>Как работает односторонний хэш

1. Получите идентификатор иерархии, выполнив следующий запрос SQL в SQL Management Studio для базы данных Configuration Manager:

    ``` SQL
    select [dbo].[fnGetHierarchyID]()
    ```

2. Используйте приведенный ниже скрипт Windows PowerShell для одностороннего хэширования идентификатора иерархии.  

    ``` PowerShell
    Param( [Parameter(Mandatory=$True)] [string]$value )  
      $guid = [System.Guid]::NewGuid()  
      if( [System.Guid]::TryParse($value,[ref] $guid) -eq $true ) {  
      #many of the values we hash are Guids  
      $bytesToHash = $guid.ToByteArray()  
    } else {  
      #otherwise hash as string (unicode)  
      $ue = New-Object System.Text.UnicodeEncoding  
      $bytesToHash = $ue.GetBytes($value)
    }  
      # Load Hash Provider (https://en.wikipedia.org/wiki/SHA-2)
    $hashAlgorithm = [System.Security.Cryptography.SHA256Cng]::Create()
    # Hash the input
    $hashedBytes = $hashAlgorithm.ComputeHash($bytesToHash)
    # Base64 encode the result for transport
    $result = [Convert]::ToBase64String($hashedBytes)
    return $result
    ```

3. Сравните выходные данные скрипта с идентификатором GUID в необработанных данных. Этот процесс показывает, как скрываются данные.

## <a name="next-steps"></a>Дальнейшие шаги

> [!div class="nextstepaction"]
> [Уровни данных о диагностике и использовании](levels-overview.md)
