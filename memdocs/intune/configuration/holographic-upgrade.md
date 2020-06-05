---
title: Обновление до Windows Holographic for Business в Microsoft Intune в Azure | Документация Майкрософт
description: Обновление до Windows 10 Holographic for Business с помощью профиля конфигурации устройства в Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: d561d2682cf90d5d7075640c260d8f21c8b891b1
ms.sourcegitcommit: 169e279ba686c28d9a23bc0a54f0a2a0d20bdee4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2020
ms.locfileid: "83556121"
---
# <a name="upgrade-devices-running-windows-holographic-to-windows-holographic-for-business"></a>Обновление устройств с Windows Holographic до Windows Holographic for Business

Microsoft Intune включает множество параметров для управления и защиты устройств. В этой статье перечислены и описаны параметры, которые можно использовать, чтобы обновить устройства Windows Holographic до Windows Holographic for Business.

В рамках решения в системе управления мобильными устройствами используйте эти параметры для обновления ваших устройств Windows Holographic. Для получения нужной лицензии на обновление Microsoft HoloLens вы можете приобрести пакет Commercial Suite. Дополнительные сведения: [Разблокировка функций Windows Holographic for Business](https://docs.microsoft.com/hololens/hololens1-upgrade-enterprise).

Администратор Intune может создавать и назначать эти параметры вашим устройствам.

Дополнительные сведения об этой функции см. в разделе [Обновление Windows 10 или выход из S-режима в Intune с помощью профиля конфигурации](edition-upgrade-configure-windows-10.md).

## <a name="before-you-begin"></a>Подготовка к работе

[Создайте профиль конфигурации устройства для переключения режима и обновления выпуска Windows 10](edition-upgrade-configure-windows-10.md#create-the-profile).

При создании профиля конфигурации устройства для переключения режима и обновления выпуска Windows 10 используется больше параметров, чем указано в этой статье. Параметры, описанные в этой статье, поддерживаются на устройствах Windows Holographic for Business.

## <a name="edition-upgrade"></a>Обновление выпусков

- **Выпуск, до которого необходимо обновить**: выберите **Windows 10 Holographic для бизнеса**.
- **Файл лицензии**: перейдите и выберите полученный вами файл лицензии XML.

  :::image type="content" source="./media/holographic-upgrade/Holographic-edition-upgrade.png" alt-text="Введите в Intune имя файла XML, которое включает информацию о лицензии Holographic for Business.":::

## <a name="next-steps"></a>Дальнейшие шаги

[Назначение профиля](device-profile-assign.md) и [отслеживание его состояния](device-profile-monitor.md).

Вы можете также создать профили обновления выпусков для устройств [Параметры устройства Windows 10 (и более поздних) для обновления выпусков или включения S-режима в Intune](edition-upgrade-windows-settings.md).
