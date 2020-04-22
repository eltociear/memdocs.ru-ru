---
title: Обновление Long-Term Servicing Branch до Current Branch
titleSuffix: Configuration Manager
description: Узнайте, как преобразовать сайт Long-Term Servicing Branch в сайт Current Branch.
ms.date: 02/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ec5b54cf-62b7-4ed1-9bb3-e8c63b9641c8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b9f79eae1eee29fee33a9a841a303aae55686c55
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707232"
---
# <a name="upgrade-the-long-term-servicing-branch-to-the-current-branch"></a>Обновление Long-Term Servicing Branch до Current Branch

*Область применения: System Center Configuration Manager: Long-Term Servicing Branch*

В этом разделе вы узнаете, как обновить (преобразовать) сайт и иерархию версии Long-Term Servicing Branch (LTSB) Configuration Manager до версии Current Branch.

Если у вас есть действующее соглашение Software Assurance (или аналогичные лицензионные права), предоставляющее права на использование версии Current Branch, вы можете преобразовать установку LTSB в Current Branch.  Такое преобразование является односторонним, так как сайт Current Branch нельзя преобразовать в LTSB.

Если у вас несколько сайтов, преобразовать необходимо только сайт верхнего уровня в иерархии. После преобразования сайта верхнего уровня:
- Подчиненные первичные сайты преобразуются автоматически.
- Вторичные сайты необходимо обновить вручную с помощью консоли Configuration Manager.

## <a name="run-setup-to-convert-the-long-term-servicing-branch"></a>Запуск программы установки для преобразования Long-Term Servicing Branch
На сайте верхнего уровня в иерархии можно запустить программу установки Configuration Manager с соответствующего базового носителя и выбрать пункт **Обслуживание сайта**.  Когда появится страница лицензирования, выберите вариант Current Branch и следуйте указаниям мастера.

После преобразования сайта в Current Branch можно будет использовать ранее недоступные функции и возможности.

> [!NOTE]  
> Соответствующий базовый носитель — это носитель с версией не ниже версии установки LTSB.

Так как версия LTSB основана на версии 1606, для ее преобразования в Current Branch нельзя использовать базовый носитель с версией 1511. Вместо этого запустите программу установки с того же базового носителя с версией 1606, который вы использовали для установки сайта LTSB, и выберите вариант лицензирования для Current Branch.  Кроме того, если была выпущена более новая базовая версия Current Branch, можно запустить программу установки с ее базового носителя.

Список базовых версий см. в подразделе **Базовые и обновленные версии** раздела [Обновления для Configuration Manager](../servers/manage/updates.md).

## <a name="use-the-configuration-manager-console-to-convert-the-long-term-servicing-branch"></a>Использование консоли Configuration Manager для преобразования ветви Long-Term Servicing Branch
Если сайт работает под управлением версии LTSB, вы можете преобразовать его в версию Current Branch в консоли Configuration Manager, выполнив указанные ниже действия.

 1. В консоли перейдите к узлу **Администрирование** > **Конфигурация сайта** > **Сайты** и откройте раздел **Параметры иерархии**.  

 2. Щелкните **Параметры иерархии** и перейдите на вкладку **Лицензирование**. Выберите параметр **Преобразование в Current Branch** и щелкните **Применить**.  

После преобразования сайта в Current Branch можно будет использовать ранее недоступные функции и возможности.
