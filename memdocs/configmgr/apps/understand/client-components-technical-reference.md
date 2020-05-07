---
title: Технический справочник по клиентским компонентам для развертывания приложений
titleSuffix: Configuration Manager
description: Клиентские компоненты, которые используются для устранения неполадок, связанных с развертыванием приложений в Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: 701a3456-9dd6-4aaa-9c5a-37c1e1773216
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 35b54bd5868197d607a15ab1d4759d03968b9892
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688852"
---
# <a name="understanding-application-deployment-client-components"></a>Основные сведения о клиентских компонентах развертывания приложений

*Область применения: Configuration Manager (Current Branch)*

Операции применения и оценки развертывания приложений выполняются компонентами агента DCM и агента CI в клиенте. В этой статье описывается, как выполняется типичное задание агентов DCM и CI.

## <a name="dcm-agent"></a>Агент DCM

Агент DCM — это высокоуровневый клиентский компонент, отвечающий за оценку элементов конфигурации, включая приложения. При активации или применении развертывания создается задание агента DCM, которое считывает политику назначения и определяет действия, требующие выполнения. Это действие можно отследить в файле **DCMAgent.log** в клиенте по идентификатору задания агента DCM, который можно определить по уникальному идентификатору приложения.

### <a name="device-deployments"></a>Развертывания на устройствах

- Для **обязательных** развертываний в файле DCMAgent.log приводятся соответствующие действия. Они могут различаться в зависимости от того, прошел ли уже крайний срок развертывания.

    ```text
    # Evaluation Job example:
    DCMAgentJob({A9E850E2-91B0-4122-94FD-D14EDF925AF7}): CDCMAgentJob::PopulateCIsFromAssignment - CI policy Id:ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/RequiredApplication_fc76ef0a-3ab0-4110-8cce-1addc36d0225 version:3 with actions: Evaluation, Content Download

    # Enforcement Job example:
    DCMAgentJob({4C8A9F6E-390B-450E-B505-B5698DB68EDD}): CDCMAgentJob::PopulateCIsFromAssignment - CI policy Id:ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/RequiredApplication_fc76ef0a-3ab0-4110-8cce-1addc36d0225 version:3 with actions: Evaluation, Install, Uninstall, Update, Look-ahead Install, Look-ahead Uninstall, Look-ahead Update
    ```

- Для **доступных** развертываний в файле DCMAgent.log показано, что развертывание `is not mandatory`. Для таких развертываний выполняется оценка приложения, но принудительное применение пропускается, если только пользователь не инициировал установку.

    ```text
    # Evaluation Job example:
    DCMAgentJob({E353BF94-D7ED-4ADD-AF0F-9273F6A67FC1}): CDCMAgentJob::PopulateCIsFromAssignment - [SCAN] CI policy Id :ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/RequiredApplication_fc76ef0a-3ab0-4110-8cce-1addc36d0225 version:3 - Assignment:{3AC57DFE-3F87-4C59-930B-B9F57CB41B91} is not mandatory.

    # Enforcement Job (user initiated) example:
    Request to enforce application ConfigMgr Toolkit(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/Application_fc76ef0a-3ab0-4110-8cce-1addc36d0225.3) immediately for target: machine with action(s): Evaluation, Install, Update
    CDCMAgentJobMgr::CreateInteractiveJob - Queuing new job: {D331249E-F7DE-481B-A497-8E8B5E7B91C3}

    ```

### <a name="user-deployments"></a>Развертывания для пользователей

- Для **обязательных** развертываний в файле DCMAgent.log приводятся соответствующие действия. Они могут различаться в зависимости от того, прошел ли уже крайний срок развертывания.

    ```text
    # Evaluation Job example:
    DCMAgentJob({65D9688D-1781-4DA3-B07A-193D481251C6}): CDCMAgentJob::PopulateCIsFromAssignment - CI policy Id:ScopeId_C8F7EAE6-DBA8-4970-B3FF-47ED706868DE/RequiredApplication_6b39398b-fd20-47ca-bd68-074274509f98 version:2 with actions: Evaluation, Content Download

    # Enforcement Job example:
    DCMAgentJob({2B0DA272-FC65-4F31-9557-C4D840D650F1}): CDCMAgentJob::PopulateCIsFromAssignment - CI policy Id:ScopeId_C8F7EAE6-DBA8-4970-B3FF-47ED706868DE/RequiredApplication_6b39398b-fd20-47ca-bd68-074274509f98 version:2 with actions: Evaluation, Install, Uninstall, Update, Look-ahead Install, Look-ahead Uninstall, Look-ahead Update
    ```

- Для **доступных** развертываний задания агента DCM для оценки и применения создаются при инициации установки приложения пользователем.

    ```text
    # Evaluation Job example:
    DCMAgentJob({FBB44C84-DB06-41F7-8DC1-D9BA368F0C20}): CDCMAgentJob::PopulateCIsFromAssignment - [SCAN] CI policy Id :ScopeId_C8F7EAE6-DBA8-4970-B3FF-47ED706868DE/RequiredApplication_6b39398b-fd20-47ca-bd68-074274509f98 version:2 - Assignment:{7EA17128-EB4F-448A-88A7-B865E7DA228C} is not mandatory.

    # Enforcement Job example:
    CAppMgmtSDK::EnforceAppPolicy ScopeId_C8F7EAE6-DBA8-4970-B3FF-47ED706868DE/RequiredApplication_6b39398b-fd20-47ca-bd68-074274509f98.
    CDCMAgentJobMgr::CreateInteractiveJob - Queuing new job: {7936D7F3-24B0-401D-BADD-59EB5B49C2C2}
    ```

## <a name="ci-agent"></a>Агент CI

Агент CI — это клиентский компонент, отвечающий за оценку и исправление элементов конфигурации. Агент DCM считывает политику назначения и создает задание, чтобы компонент агента CI выполнил запрошенные действия. В файле **DCMAgent.log** записывается идентификатор задания агента CI, по которому можно отследить действие агента CI в файле **CIAgent.log** в клиенте.

<pre><code class="lang-text">DCMAgentJob({E353BF94-D7ED-4ADD-AF0F-9273F6A67FC1}): CDCMAgent::InitiateCIAgentJob - <b>Starting CI Agent Job</b> {57AF6FA1-3482-4469-9881-A63F41D18406} for target: machine. Refer to this CI agent job ID in ciagent.log for more details
</code></pre>

Типичное задание агента CI состоит из нескольких этапов, которые можно определить, отфильтровав файл **CIAgent.log** по идентификатору задания агента CI и выполнив поиск по `TransitionState`. Ниже приведены некоторые ключевые этапы для задания развертывания приложения, выполняемого агентом CI.

- **DownloadingCIs**
  - На этом этапе скачиваются метаданные приложения, необходимые для его оценки. К ним относятся метод обнаружения, правила требований, глобальные условия и т. д. Это действие можно отследить в файлах **CIDownloader.log** и **DataTransferService.log**. Для **доступных** развертываний этот процесс происходит во время первой оценки приложения. Однако для **обязательных** развертываний этот процесс происходит сразу же после скачивания политики.

- **InvokingSdmMethod**
  - На этом этапе метод обнаружения приложений используется для проверки установки приложения и определения требуемого состояния. Это действие можно отследить в файлах **AppDiscovery.log** и **AppIntentEval.log**. Дополнительные сведения об этом этапе см. в статье [Оценка приложения](deployment-evaluation-technical-reference.md).

- **StateDownloadingContents**
  - На этом этапе при необходимости скачивается содержимое приложения. Это действие можно отследить в файлах **CAS.log**, **ContentTransferManager.log**, **LocationServices.log** и **DataTransferService.log**. Дополнительные сведения об этом этапе см. в статье [Скачивание приложения](deployment-download-technical-reference.md).

- **StateEnforcingCIs**
  - На этом этапе запускается установка приложения. Это действие можно отследить в файле **AppEnforce.log**. Дополнительные сведения об этом этапе см. в статье [Установка приложения](deployment-install-technical-reference.md).

- **StateEnforcementReporting**
  - На этом этапе записывается состояние установки приложения для передачи в точку управления. Это действие можно отследить в файле **StateMessage.log**.

Хотя задание агента CI проходит все этапы, необязательные этапы пропускаются. Например, для **доступных** развертываний пропускаются этапы StateDownloadingContents и StateEnforcingCIs, пока пользователь не попытается установить приложение из центра программного обеспечения. Однако для **обязательных** развертываний на этапе StateDownloadingContents скачивается необходимое содержимое приложения при активации назначения, но этап StateEnforcingCIs пропускается, если крайний срок находится в будущем. Этот процесс можно наблюдать в файле CIAgent.log, выполнив фильтрацию по идентификатору задания агента CI, а затем выполнив поиск по `Skipping policy`.

```text
{57AF6FA1-3482-4469-9881-A63F41D18406} - Skipping policy CI <CI Unique ID> and all dependents for ContentDownload task since CI action was not requested.
{57AF6FA1-3482-4469-9881-A63F41D18406} - Skipping policy CI <CI Unique ID> and all dependents for Enforce task since CI action was not requested.
```

## <a name="next-steps"></a>Дальнейшие шаги

- [Оценка приложения](deployment-evaluation-technical-reference.md)
- [Скачивание приложения](deployment-download-technical-reference.md)
- [Установка приложения](deployment-install-technical-reference.md)
