---
title: Технический справочник по оценке приложения
titleSuffix: Configuration Manager
description: Технический справочник по устранению неполадок, связанных с оценкой приложения, в Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: a7035223-d7bd-47b4-896f-08de3416a4eb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fdeec54489adfc0d2a5cceb99c7e7587ce1a41ab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688842"
---
# <a name="application-deployment-evaluation"></a>Оценка развертывания приложений

*Область применения: Configuration Manager (Current Branch)*

Прежде чем продолжить, ознакомьтесь с [клиентскими компонентами для развертывания приложений](client-components-technical-reference.md), чтобы понять обработку заданий агентами DCM и CI.

Оценка приложения выполняется компонентами агента DCM и агента CI при активации развертывания. Сведения об активации назначения см. в статьях [Развертывание приложения в коллекции устройств](device-deployment-technical-reference.md) или [Развертывание приложения в коллекции пользователей](user-deployment-technical-reference.md).

## <a name="application-detection-and-evaluation"></a>Обнаружение и оценка приложения

Оценка приложения выполняется на этапе **InvokingSdmMethod** задания агента CI. На этом этапе клиент оценивает метод обнаружения, заданный для приложения, чтобы определить, установлено ли приложение на устройстве. Это действие можно отследить в файле **AppDiscovery.log** с использованием уникального идентификатора типа развертывания или имени типа развертывания.

```text
Performing detection of app deployment type ConfigMgr Toolkit - Windows Installer (*.msi file)(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, revision 2) for system.
+++ Did not detect app deployment type ConfigMgr Toolkit - Windows Installer (*.msi file)(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, revision 2) for system.
```

> [!NOTE]
> В приведенном выше примере показано обнаружение приложения MSI, которое выполняется путем проверки наличия на устройстве кода продукта MSI. Для приложений, использующих альтернативные методы обнаружения, для проверки установки приложения применяется соответствующий метод обнаружения.

Далее клиент оценивает требуемое состояние приложения на основе цели развертывания. Этот шаг также предполагает определение наличия зависимостей или правил замены, которые должны учитываться для приложения. Это действие можно отследить в файле **AppIntentEval.log** с использованием приложения и уникального идентификатора типа развертывания.

<pre><code class="lang-text"># Available Application Deployment

[Application or DT Unique ID] :- <b>Current State = NotInstalled, Applicability = Applicable, ResolvedState = Available</b>, ConfigureState = NotNeeded, Title = [Application or DT Name]

# Required Application Deployment

[Application or DT Unique ID] :- <b>Current State = NotInstalled, Applicability = Applicable, ResolvedState = Installed</b>, ConfigureState = NotNeeded, Title = [Application or DT Name]

# Requirement Rules Not Met

[Application or DT Unique ID] :- <b>Current State = NotInstalled, Applicability = NotApplicable, ResolvedState = None</b>, ConfigureState = NotNeeded, Title = [Application or DT Name]
</code></pre>

В приведенной выше записи журнала **текущее состояние** указывает, установлено ли приложение на устройстве в настоящее время. **Применимость** указывает, применимо ли приложение на основе определенных правил требований. **ResolvedState** указывает требуемое состояние приложения на основе цели развертывания.

> [!TIP]
> Используйте [средство мониторинга развертывания](../../core/support/deployment-monitoring-tool.md) для просмотра состояния приложения, состояния применимости и нарушений требований.

## <a name="next-steps"></a>Дальнейшие шаги

- [Скачивание приложения](deployment-download-technical-reference.md)
