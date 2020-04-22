---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 10/04/2019
ms.openlocfilehash: 5d65b2c250890c10c16214bcee385c39a4f58204
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697932"
---
### <a name="hardware-inventory-reports"></a><a name="ki_hinv"></a> Отчеты инвентаризации оборудования

<!--5468413-->
При попытке запустить отчет, использующий инвентаризацию оборудования, возвращается ошибка. Например, отчет BitLocker возвращает сообщение об ошибке примерно следующего вида:

```
Microsoft.Reporting.WinForms.ReportServerException
An error has occurred during report processing. (rsProcessingAborted)
```

Вы также можете увидеть следующую ошибку в файле **dataldr.log**:

`[42S22][207][Microsoft][SQL Server Native Client 11.0][SQL Server]Invalid column name 'FileTimeStamp00'. : pOFFICE_ADDIN_DATA`

Ошибка также может затрагивать панели мониторинга консоли, использующие инвентаризацию оборудования.

Эта проблема возникает, когда для определенных таблиц инвентаризации оборудования изменяется схема базы данных.

#### <a name="workaround"></a>Обходной путь

Обходное решение — удалить уже существующий атрибут из базы данных. Затем компонент загрузчика данных сайта может создать новый атрибут. Выполните на сервере базы данных сайта следующий скрипт SQL, чтобы исправить схему таблиц:

``` SQL
IF NOT EXISTS (SELECT * FROM SYS.columns WHERE name = 'FileTimestamp00' AND object_id = OBJECT_ID('OFFICE_ADDIN_DATA'))
BEGIN
       DELETE am
       FROM AttributeMap am
       INNER JOIN GroupMap gm ON am.GroupKey=gm.GroupKey
       WHERE gm.GroupClass='MICROSOFT|OFFICE_ADDIN|1.0'
       AND am.AttributeName='FileTimeStamp'

       PRINT 'Fix OFFICE_ADDIN_DATA schema'
END
```
