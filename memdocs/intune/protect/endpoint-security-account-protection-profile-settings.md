---
title: Параметры политики защиты учетных записей для обеспечения безопасности конечных точек Intune | Документация Майкрософт
description: Политика защиты учетных записей для обеспечения безопасности конечных точек в Microsoft Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/17/2020
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
ms.openlocfilehash: f4e67c434af9eb7f88c3e7d3997ef7c7d829c860
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431999"
---
# <a name="account-protection-policy-settings-for-endpoint-security-in-intune"></a>Параметры политики защиты учетных записей для обеспечения безопасности конечных точек в Intune

Просмотрите параметры, которые можно настроить в профилях для политики *Защита учетных записей* в узле безопасности конечных точек в Intune в рамках[политики безопасности конечных точек](../protect/endpoint-security-policy.md).

Поддерживаемые платформы и профили

- **Windows 10 и более поздних версий**
  - Профиль: **Защита учетных записей** *(предварительная версия)*


## <a name="account-protection-profile"></a>Профиль защиты учетных записей

### <a name="account-protection"></a>Защита учетной записи

- **Блокирование Windows Hello для бизнеса**

  Windows Hello для бизнеса — это альтернативный метод входа в Windows путем замены паролей, смарт-карт и виртуальных смарт-карт.
  - **Не настроено** (*по умолчанию*) — устройства подготавливают Windows Hello для бизнеса.
  - **Отключено** — устройства подготавливают Windows Hello для бизнеса.
  - **Включено** — устройства не подготавливают Windows Hello для бизнеса ни для одного пользователя.
  
- **Включено для использования ключей безопасности для входа**

  Включение ключа безопасности Windows Hello в качестве учетных данных для входа на все компьютеры в клиенте.
  - **Не настроено** (*по умолчанию*)
  - **Да**

- **Включение Credential Guard**  
  [CSP []DeviceGuard](https://go.microsoft.com/fwlink/?linkid=872424)

  Credential Guard использует гипервизор Windows для обеспечения защиты. Credential Guard требуется поддержка оборудования для безопасной загрузки и защиты DMA. Этот параметр будет успешно применяться только на устройствах, отвечающих требованиям к оборудованию.
  - **Не настроено** (*по умолчанию*) — отключить использование Credential Guard, которое установлено в Windows по умолчанию.
  - **Включить с блокировкой UEFI** — включить Credential Guard и запретить его удаленное отключение, так как сохраненную конфигурацию UEFI необходимо очистить вручную.
  - **Включить без блокировки UEFI** — включить Credential Guard и разрешить его отключение без физического доступа к компьютеру.

## <a name="next-steps"></a>Дальнейшие шаги

[Политика безопасности конечной точки для защиты учетных записей](../protect/endpoint-security-account-protection-policy.md)
