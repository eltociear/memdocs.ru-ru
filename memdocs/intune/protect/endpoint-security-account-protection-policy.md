---
title: Управление параметрами защиты учетных записей с помощью политик безопасности конечных точек в Microsoft Intune | Документация Майкрософт
description: Настраивайте и разворачивайте политики для устройств, которыми вы управляете, с помощью параметров политики защиты учетных записей для обеспечения безопасности конечных точек в Microsoft Endpoint Manager.
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
ms.openlocfilehash: 6fb5702b7c809c7810004a53d084f19fa94dea9e
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431856"
---
# <a name="account-protection-policy-for-endpoint-security-in-intune"></a>Политика защиты учетных записей для обеспечения безопасности конечных точек в Intune

Используйте политики безопасности конечной точки Intune для защиты учетных записей, чтобы защищать удостоверения и учетные записи пользователей. Политика защиты учетных записей работает с параметрами для Windows Hello и Credential Guard, которые являются частью системы управления удостоверениями и доступом Windows.

- *Windows Hello для бизнеса* вместо паролей применяет надежную двухфакторную проверку подлинности на ПК и мобильных устройствах.
- *Credential Guard* помогает защитить учетные данные и секреты, используемые на устройствах.

Дополнительные сведения см. в разделе [Управление удостоверениями и доступом](https://docs.microsoft.com/windows/security/identity-protection/) в документации по управлению удостоверениями и доступом Windows.

Политики безопасности конечных точек для защиты учетных записей можно найти в разделе *Управление* в узле **Безопасность конечной точки** [центра администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

Просмотрите [параметры для профилей защиты учетных записей](../protect/endpoint-security-asr-profile-settings.md).

## <a name="prerequisites-for-account-protection-profiles"></a>Предварительные требования для профилей защиты учетных записей

- Windows 10 или более поздней версии

## <a name="account-protection-profiles"></a>Профили защиты учетных записей

*Профили защиты учетных записей существуют в предварительной версии*.

**Профили Windows 10**.

- **Защита учетной записи** *(предварительная версия)*  — параметры политик защиты учетных записей помогают защитить учетные данные пользователя.

## <a name="next-steps"></a>Дальнейшие шаги

[Настройка политик безопасности конечных точек](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)
