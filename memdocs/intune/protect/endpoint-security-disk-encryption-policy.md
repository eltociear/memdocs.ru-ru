---
title: Управление шифрованием дисков с помощью политик безопасности конечных точек в Microsoft Intune | Документация Майкрософт
description: Настраивайте и разворачивайте политики для устройств, которыми вы управляете, с помощью политики шифрования дисков для обеспечения безопасности конечных точек в Microsoft Endpoint Manager.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: b988e4ddeb306c7da290c87e8a32fa0571627257
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431674"
---
# <a name="disk-encryption-policy-for-endpoint-security-in-intune"></a>Политика шифрования дисков для обеспечения безопасности конечных точек в Intune

Профили шифрования дисков безопасности конечных точек касаются только тех параметров, которые связаны со встроенными методами шифрования устройств, например FileVault или BitLocker. Благодаря этому администраторы систем безопасности могут легко управлять только необходимыми параметрами шифрования дисков.

Несмотря на то что настроить параметры устройств можно и в профилях *Endpoint Protection*, профили конфигурации устройств включают дополнительные категории параметров. Эти параметры не связаны с шифрованием дисков и могут усложнить настройку именно шифрования дисков.

Политики безопасности конечных точек можно найти в разделе *Управление* в узле **Безопасность конечной точки** [центра администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

## <a name="prerequisites-for-disk-encryption-policy"></a>Необходимые условия для использования политики шифрования дисков

- **macOS**: macOS 10.13 или более поздней версии
- **Windows**: Windows 10 или более поздней версии

## <a name="disk-encryption-profiles"></a>Профили шифрования дисков

**Профили macOS**.

- **FileVault** ― FileVault предлагает встроенное полное шифрование диска для устройств macOS.

  Управление [параметрами FileVault](../protect/endpoint-security-disk-encryption-profile-settings.md#filevault) для macOS.

  Сведения о создании профиля FileVault см. в разделе [Использование шифрования дисков FileVault для macOS](../protect/encrypt-devices-filevault.md).

**Профили Windows 10**.

- **BitLocker**. Шифрование диска BitLocker — это функция защиты данных, которая интегрируется с операционной системой и устраняет угрозу кражи или нарушения безопасности данных на потерянных, украденных или неправильно выведенных из эксплуатации компьютерах.

  Управление [параметрами BitLocker](../protect/endpoint-security-disk-encryption-profile-settings.md#bitlocker) для Windows 10.

  Сведения о создании профиля BitLocker см. в разделе [Использование шифрования дисков BitLocker для Windows 10](../protect/encrypt-devices.md).

## <a name="manage-device-encryption"></a>Управление шифрованием устройств

После развертывания политики для шифрования диска устройства ознакомьтесь со следующими статьями, чтобы получить сведения об управлении шифрованием.

- [Управление BitLocker](../protect/encrypt-devices.md#manage-bitlocker)
- [Управление FileVault](../protect/encrypt-devices-filevault.md#manage-filevault)
- [Мониторинг шифрования устройств](../protect/encryption-monitor.md)

## <a name="next-steps"></a>Дальнейшие шаги

- [Как создать профиль FileVault](../protect/encrypt-devices-filevault.md#create-an-endpoint-security-policy-for-filevault)
- [Как создать профиль BitLocker](../protect/encrypt-devices.md#create-an-endpoint-security-policy-for-bitlocker)
