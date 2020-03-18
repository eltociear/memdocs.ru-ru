---
title: Очистка устройства с macOS
titleSuffix: Microsoft Intune
description: Сведения о том, как удалить все данные, в том числе операционную систему, на устройстве с macOS.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/27/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ab396092-907a-44b7-a157-aabee62176a9
ms.reviewer: coferro
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 650ba81c9e92ce03b67e90cf188435b7dc0800fb
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/13/2020
ms.locfileid: "79338218"
---
# <a name="erase-all-data-from-a-macos-device"></a>Очистка всех данных на устройстве с macOS

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Вы можете удалить на устройстве с macOS все данные, включая операционную систему. Устройство также будет удалено из системы управления Intune. Предупреждение для конечного пользователя отображаться не будет.

1. В [Центре администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) выберите **Устройства** > **Все устройства** и выберите устройство, которое требуется очистить.
2. Выберите пункты **Дополнительно** > **Очистить** и укажите шестизначный **ПИН-код восстановления**. Это ПИН-код, который должен указать пользователь для переустановки операционной системы на своем устройстве. Обязательно запомните или запишите этот ПИН-код, так как он не будет отображаться после завершения очистки.
![Снимок экрана](./media/device-erase/providepin.png)
3. Нажмите кнопку **ОК**, чтобы очистить устройство.
