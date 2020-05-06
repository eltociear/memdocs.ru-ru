---
title: Технический справочник по установке приложения
titleSuffix: Configuration Manager
description: Технический справочник по устранению неполадок установки приложений в Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: 2af4f9c3-16b8-4691-a59d-aea6241d288e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 13c96e9ad4f0608084d87bed3973221730cb2d5f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688822"
---
# <a name="application-installation"></a>Установка приложения

*Область применения: Configuration Manager (Current Branch)*

Прежде чем продолжить, ознакомьтесь с [клиентскими компонентами для развертывания приложений](client-components-technical-reference.md), чтобы понять обработку заданий агентами DCM и CI.

Установка приложения выполняется компонентами агента DCM и агента CI при принудительном применении развертывания. Время принудительного применения отличается для доступных и обязательных развертываний. Сведения о принудительном применении назначения см. в статьях [Развертывание приложения в коллекции устройств](device-deployment-technical-reference.md) или [Развертывание приложения в коллекции пользователей](user-deployment-technical-reference.md).

## <a name="enforcement-initiation"></a>Инициация принудительного применения

Установка приложения инициируется компонентом агента CI на клиенте на этапе **StateEnforcingCIs**. Этот процесс выполняется одинаково независимо от того, где развернуто приложение: в коллекции устройств или коллекции пользователей.

- Для **доступных** развертываний приложение устанавливается, когда пользователь инициирует его установку из центра программного обеспечения.
- Для **обязательных** развертываний приложение устанавливается при наступлении крайнего срока развертывания. Однако пользователь может запустить установку из центра программного обеспечения до наступления крайнего срока.

Когда агент CI инициирует установку приложения, он создает задачу, которая обрабатывается компонентом диспетчера задач CI. Затем диспетчер задач CI инициирует установку. Это действие можно отследить в файле **CITaskMgr.log** с использованием уникального идентификатора типа развертывания.

<pre><code class="lang-text"><b>Initiating task Enforce</b> for CI ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44.2 (ConfigMgr Toolkit - Windows Installer (*.msi file)) for target: , consumer: {9BC3154A-98F1-4595-A967-173D536A3F94}
Initiated application enforcement. : CITask(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44.2..Install.Enforce)
</code></pre>

## <a name="application-enforcement"></a>Принудительное применение приложения

После инициации принудительного применения приложения клиент снова выполняет обнаружение приложений, чтобы убедиться, что приложение еще не установлено. Как только будет определено, что приложение не установлено, инициируется установка приложения. Это действие можно отследить в файле **AppEnforce.log** с использованием уникального идентификатора типа развертывания.

```text
+++ Starting Install enforcement for App DT "ConfigMgr Toolkit - Windows Installer (*.msi file)" ApplicationDeliveryType - ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, Revision - 2, ContentPath - C:\WINDOWS\ccmcache\2, Execution Context - System
    Executing Command line: "C:\WINDOWS\system32\msiexec.exe" /i "ConfigMgrTools.msi" /q /qn with user context
    Process 7292 terminated with exitcode: 0
Status is switching to Success
```

## <a name="installation-verification"></a>Проверка установки

После установки приложения снова применяется метод обнаружения приложений для обнаружения приложения как установленного.

<pre><code class="lang-text">Performing detection of app deployment type ConfigMgr Toolkit - Windows Installer (*.msi file)(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, revision 2) for system.
+++ <b>Discovered MSI application</b> [AppDT Id: ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, Revision: 2, MSI Product code: {4FFF7ECC-CCF7-4530-B938-E7812BB91186}, MSI Product version: ]
++++++ <b>App enforcement completed</b> (3 seconds) for App DT "ConfigMgr Toolkit - Windows Installer (*.msi file)" [ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44], Revision: 2, User SID: ] ++++++
</code></pre>

Наконец, после завершения принудительного применения агент CI получает уведомление о завершении задачи, а задание агента CI переходит к следующему этапу.

<pre><code class="lang-text">CIAgentJob({2BF84225-C9E8-49A6-A308-A160C4B799D3}): CAgentJob::HandleEvent(<b>Event=CITaskComplete, CurrentState=StateEnforcingCIs</b>)
</code></pre>

## <a name="next-steps"></a>Дальнейшие шаги

[Устранение неполадок, связанных с развертываниями приложений](../deploy-use/troubleshoot-application-deployment.md)
