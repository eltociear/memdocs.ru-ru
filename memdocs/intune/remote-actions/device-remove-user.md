---
title: Удаление пользователя с устройства iOS или iPadOS с помощью Microsoft Intune
titleSuffix: ''
description: Узнайте, как удалить пользователя с устройства iOS или iPadOS с помощью Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/22/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 2ea5941c-a69b-4e1c-b42c-a1fc0c3a7de7
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 08a6ccb30d4397ce5d06483556579c32f3eb2819
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/13/2020
ms.locfileid: "79348982"
---
# <a name="remove-a-user-from-a-shared-iosipados-device"></a>Удаление пользователя с общего устройства iOS или iPadOS


[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Действие **Удалить пользователя** удаляет выбранного пользователя из локального кэша на общем устройстве iOS. Устройство iPad нужно настроить для управления приложением Classroom для iOS или iPadOS с помощью [профиля образования iOS или iPadOS](../fundamentals/education-settings-configure-ios.md). 

## <a name="supported-platforms"></a>Поддерживаемые платформы

- Windows — не поддерживается
- Windows Phone — не поддерживается
- iOS или iPadOS — поддерживается в iOS или iPadOS версии 9.3 и выше (только общие устройства iPad)
- macOS — не поддерживается
- Android — не поддерживается

## <a name="remove-a-user"></a>Удаление пользователя

1. Войдите в [Центр администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Выберите **Устройства** > **Все устройства**.
3. Выберите нужное устройство iOS или iPadOS в списке управляемых устройств.
4. В области для устройства выберите **Пользователи**.
5. В списке щелкните имя удаляемого пользователя правой кнопкой мыши и выберите пункт **Удалить пользователя**.

## <a name="next-steps"></a>Дальнейшие шаги

- Чтобы отобразились сведения о состоянии действия **Удалить пользователя**, выберите **Устройства** > **Действия устройства**.
