---
title: Особые примечания о миграции
titleSuffix: Microsoft Intune
description: В этой статье рассказывается о том, какие моменты необходимо учесть, прежде чем начинать миграцию в Microsoft Intune.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 01/02/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: f29d2894-e98b-4f2c-b444-a8ccc1b7efdd
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5a954732b2df5824d7116dc10e035b10290c0290
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/13/2020
ms.locfileid: "79358329"
---
# <a name="special-migration-considerations"></a>Особые примечания о миграции

В зависимости от имеющейся среды поставщика MDM к миграции могут применяться особые требования.

## <a name="wipe-for-apples-device-enrollment-program-dep"></a>Очистка для программы регистрации устройств (DEP) Apple

В рамках программы регистрации устройств (DEP) Apple задаются конфигурации устройств, которые пользователь не сможет удалить. Чтобы сохранить расширенные функции управления DEP, устройства нужно переключить в исходное состояние путем очистки для регистрации в Intune.

Чтобы продолжить использовать программу DEP для управления устройствами в Intune, [настройте регистрацию устройств iOS/iPadOS с помощью программы регистрации устройств](../enrollment/device-enrollment-program-enroll-ios.md).

## <a name="next-steps"></a>Дальнейшие шаги

[Этап 2. Кампания по миграции](migration-guide-campaign.md)
