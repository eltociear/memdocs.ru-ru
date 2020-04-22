---
title: Создание последовательности задач для прочих развертываний (не ОС)
titleSuffix: Configuration Manager
description: Создание последовательностей задач, которые не предназначены для развертывания ОС, например для развертывания программного обеспечения или автоматизации задач
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 92aaec8a-8751-442a-b64b-62ab05b5bf50
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 583a90452fe077057b93150e9cb635fe9269de5a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709072"
---
# <a name="create-a-task-sequence-for-non-os-deployments"></a>Создание последовательности задач для прочих развертываний (не ОС)

*Область применения: Configuration Manager (Current Branch)*

Последовательности задач в Configuration Manager применяются для автоматизации любых задач в окружении. Эти задачи разрабатываются и тестируются главным образом для развертывания операционных систем. Configuration Manager имеет много других функций, которые следует рассматривать в первую очередь для следующих сценариев:

- [установка приложения](../../apps/understand/introduction-to-application-management.md);

    > [!NOTE]
    > Начиная с версии 2002, вы можете устанавливать сложные приложения в последовательностях задач с помощью модели приложения. Добавьте тип развертывания для приложения, которое представляет собой последовательность задач, для установки или удаления приложения. Дополнительные сведения см. в статье [Создание приложений Windows](../../apps/get-started/creating-windows-applications.md#bkmk_tsdt).<!-- 3555953 -->

- [установка обновлений программного обеспечения](../../sum/understand/software-updates-introduction.md);

- [настройка конфигурации](../../compliance/understand/ensure-device-compliance.md).

Вы можете применить и другие технологии автоматизации Microsoft System Center, такие как [Orchestrator](https://docs.microsoft.com/system-center/orchestrator/) и [Service Management Automation](https://docs.microsoft.com/system-center/sma/).  

Главным преимуществом последовательностей задач является их гибкость. Они позволяют настраивать параметры клиента, распространять программное обеспечение, обновлять драйверы, изменять состояния пользователей и выполнять другие задачи независимо от развертывания операционной системы. Можно создать настраиваемую последовательность задач, чтобы добавить любое количество задач. В Configuration Manager поддерживается использование пользовательских последовательностей задач для развертывания программного обеспечения, отличного от операционных систем. Но если выполнение последовательности задач приводит к нежелательным или несогласованным результатам, постарайтесь упростить эту операцию следующими способами:

- упростите шаги и действия;
- разнесите действия на несколько последовательностей задач;
- примените поэтапный подход к созданию и тестированию последовательности задач.

Следующие задачи можно выполнять в рамках пользовательской последовательности задач развертывания ПО, отличного от операционной системы:  

- [Проверить готовность](../understand/task-sequence-steps.md#BKMK_CheckReadiness)  

- [Подключить к сетевой папке](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder)  

- [Скачать содержимое пакета](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent)  

- [Установить приложение](../understand/task-sequence-steps.md#BKMK_InstallApplication)  

- [Установить пакет](../understand/task-sequence-steps.md#BKMK_InstallPackage)  

- [Установить обновления программного обеспечения](../understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  

- [Перезагрузить компьютер](../understand/task-sequence-steps.md#BKMK_RestartComputer)  

- [Выполнить из командной строки](../understand/task-sequence-steps.md#BKMK_RunCommandLine)  

- [Запустить сценарий PowerShell](../understand/task-sequence-steps.md#BKMK_RunPowerShellScript)  

- [Запуск последовательности задач](../understand/task-sequence-steps.md#child-task-sequence)  

- [Задать динамические переменные](../understand/task-sequence-steps.md#BKMK_SetDynamicVariables)  

- [Задать переменную последовательности задач](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable)  
