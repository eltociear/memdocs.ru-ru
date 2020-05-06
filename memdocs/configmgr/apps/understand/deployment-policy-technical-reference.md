---
title: Технический справочник по политике развертывания приложений
titleSuffix: Configuration Manager
description: Технический справочник по устранению неполадок, связанных с политиками развертывания приложений, в Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: bf24fb83-521f-4a41-ab8e-df70a6c10e78
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 51d260ede4ed275c401c3b9f9e131134c62ae74e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688832"
---
# <a name="application-deployment-policy"></a>Политика развертывания приложений

*Область применения: Configuration Manager (Current Branch)*

## <a name="policy-creation"></a>Создание политики

При развертывании приложения создается экземпляр класса [SMS_ApplicationAssignment](../../develop/reference/apps/sms_applicationassignment-server-wmi-class.md), который представляет назначение приложения коллекции. Это действие можно отследить в файле **SMSProv.log**.

<pre><code class="lang-text">SMS Provider    PutInstanceAsync <b>SMS_ApplicationAssignment</b>~
SMS Provider    Auditing: User CONTOSO\Admin created an instance of class SMS_ApplicationAssignment.~
</code></pre>

В базе данных Configuration Manager эти сведения хранятся в таблице `CI_CIAssignments`, где `AssignmentType` 2 представляет развертывание приложения. При создании назначения компонент "Монитор базы данных SMS" обнаруживает изменение в таблице, а затем сообщает диспетчеру репликации объектов о необходимости обработать политику назначения CI (CIA). Затем компонент "Диспетчер репликации объектов" создает политику для назначения приложения в базе данных, которая сохраняется в таблице `Policy` базы данных. Идентификатор политики основан на уникальном идентификаторе приложения. Это действие можно отследить в файле **objreplmgr.log** по уникальному идентификатору назначения, который можно получить с помощью SQL-запроса, указанного в разделе [Перед началом работы](app-deployment-technical-reference.md#before-you-begin).

<pre><code class="lang-text">***** Processing Application Assignment {<b>3AC57DFE-3F87-4C59-930B-B9F57CB41B91</b>} *****
</code></pre>

Политику для назначения приложения можно просмотреть в базе данных с помощью представленного ниже SQL-запроса.

```sql
SELECT P.PolicyID, PA.PolicyAssignmentID, PA.PADBID, PA.IsTombstoned, PA.LastUpdateTime FROM Policy P
JOIN PolicyAssignment PA ON P.PolicyID = PA.PolicyID
WHERE P.PolicyID = '{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}' -- Replace Assignment Unique ID
```

## <a name="policy-targeting"></a>Целевой объект политики

После создания политики компонент "Поставщик политики" назначает ее ресурсам в коллекции, для которой предназначено развертывание приложения. Сведения об области применения политики хранятся в таблице `ResPolicyMap` базы данных. Для отслеживания этого действия в файле **policypv.log** можно использовать идентификатор PADBID, возвращенный приведенным выше запросом. Однако идентификатор PADBID, записанный в журнале, может не всегда соответствовать PADBID, возвращенному этим запросом, если несколько политик обрабатываются одновременно.

<pre><code class="lang-text">~Policy or Policy Target Change Event triggered.
~Completed batch with beginning <b>PADBID = 16778403 ending PADBID = 16778403</b>.
</code></pre>

> [!NOTE]
> Таблица `ResPolicyMap` не содержит сведений об области применения для приложений, которые развертываются как **доступные** в коллекциях пользователей. Центр программного обеспечения запрашивает список этих приложений из точки управления, а сведения об области применения политики для этих приложений создаются динамически, когда пользователь запрашивает приложение из центра программного обеспечения.

## <a name="next-steps"></a>Дальнейшие шаги

- [Развертывание приложений в коллекциях устройств](device-deployment-technical-reference.md)
- [Развертывание приложений в коллекциях пользователей](user-deployment-technical-reference.md)
