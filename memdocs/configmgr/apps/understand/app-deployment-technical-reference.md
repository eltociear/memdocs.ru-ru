---
title: Технический справочник по устранению неполадок с развертыванием приложений
titleSuffix: Configuration Manager
description: Технический справочник по устранению неполадок развертывания приложений в Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: a4eb09c8-e570-4369-9adb-ded9c8ad3400
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5b3513131b73ac2b63cf18f31b1e39e15ee97420
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688872"
---
# <a name="technical-reference-for-application-deployment-in-configuration-manager"></a>Технический справочник по развертыванию приложений в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

В этой статье вы узнаете, как работают развертывания приложений.

## <a name="before-you-begin"></a>Перед началом работы

При просмотре журналов клиентов в процессе устранения неполадок в развертываниях приложений могут оказаться полезными несколько элементов. Эти элементы включают:

- Идентификатор CI приложения
- Уникальный идентификатор приложения
- Уникальный идентификатор типа развертывания
- Уникальный идентификатор развертывания приложения (он же уникальный идентификатор назначения)
- Цель развертывания приложений
- Уникальный идентификатор содержимого
- Идентификатор и имя коллекции
- Тип коллекции

Чтобы упростить устранение неполадок, можно выполнить SQL-запрос, аналогичный приведенному ниже, к базе данных Configuration Manager, чтобы получить указанные выше сведения.

```sql
SELECT APP.CI_ID [App CI ID], APP.CI_UniqueID [App Unique ID], APP.DisplayName [App Name],
DT.CI_UniqueID [DT Unique ID], DT.ContentId [DT Content ID],
CIA.Assignment_UniqueID [Assignment ID], CIA.CollectionID, CIA.CollectionName,
CASE CIA.OfferTypeID WHEN 0 THEN 'Required' WHEN 2 THEN 'Available' WHEN 3 THEN 'Simulate' ELSE 'Unknown' END AS [Deployment Purpose],
CASE C.CollectionType WHEN 1 THEN 'User Collection' WHEN 2 THEN 'Device Collection' ELSE 'Unknown' END AS [Collection Type],
DT.Technology, DT.DisplayName [DT Name]
FROM fn_ListApplicationCIs(1033) APP
JOIN fn_ListDeploymentTypeCIs(1033) DT ON DT.AppModelName = APP.ModelName AND DT.IsLatest = 1
LEFT JOIN v_CIAssignmentToCI CIACI ON CIACI.CI_ID = APP.CI_ID
LEFT JOIN v_CIAssignment CIA ON CIACI.AssignmentID = CIA.AssignmentID
LEFT JOIN v_Collection C ON C.CollectionID = CIA.CollectionID
WHERE APP.IsLatest = 1 AND APP.DisplayName = 'Application Name' -- Replace Application Name
```

> [!IMPORTANT]
> При выполнении этого запроса **необходимо** использовать имя приложения, указанное на вкладке "Общие сведения" в окне свойств приложения, а не локализованное имя приложения, указанное на вкладке "Центр программного обеспечения" в окне свойств приложения.

## <a name="next-steps"></a>Дальнейшие шаги

- [Политика развертывания приложений](deployment-policy-technical-reference.md)
