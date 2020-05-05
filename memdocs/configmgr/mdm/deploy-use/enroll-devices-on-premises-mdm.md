---
title: Регистрация устройств для локального управления мобильными устройствами
titleSuffix: Configuration Manager
description: Узнайте о методах регистрации устройств для локального управления мобильными устройствами (MDM) в Configuration Manager.
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: b58472e3-31a5-4305-8eb6-2522befebe02
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1ca7f792bb6b419dd1d20d495bdb53bc7c2be506
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724608"
---
# <a name="enroll-devices-for-on-premises-mdm-in-configuration-manager"></a>Регистрация устройств для локальной среды MDM в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Чтобы управлять устройствами с помощью Configuration Manager локального управления мобильными устройствами (MDM), сначала необходимо зарегистрировать их. Затем Configuration Manager может взаимодействовать с устройствами для задач управления. Configuration Manager предоставляет два метода регистрации устройств:

- **Регистрация пользователя**. пользователи начинают процесс регистрации на своем устройстве. Чтобы регистрация пользователя была выполнена, установите доверенный корневой сертификат на устройстве и подготавливает пользователя к регистрации в параметрах клиента. Чтобы зарегистрировать устройство, пользователю нужно ввести только свои учетные данные.

    Дополнительные сведения см. в статье [как пользователи регистрируют устройства](user-enroll-devices-on-premises-mdm.md).

- **Массовые регистрация**. пользователь устройства не начинает регистрацию. Пакет групповой регистрации создается в Configuration Manager. При открытии на устройстве пакет предоставляет сведения, необходимые для регистрации устройства.

    Дополнительные сведения см. [в статье как выполнить автоматическую регистрацию устройств](bulk-enroll-devices-on-premises-mdm.md).

Дополнительные сведения о версиях ОС, которые Configuration Manager поддерживаются для регистрации устройств в локальной системе MDM, см. в разделе [Поддерживаемые конфигурации](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_OnpremOS).
