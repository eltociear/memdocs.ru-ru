---
title: Соединитель MTD Zimperium в Intune
titleSuffix: Intune on Azure
description: Здесь приведены сведения об интеграции Intune с Zimperium Mobile Threat Defense для управления доступом к корпоративным ресурсам с мобильных устройств.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/09/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 975d8d84-792a-41ad-925a-4a7f1ae4dcaf
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b443f922b31523ec6f27971648ba1ea9c5123867
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989399"
---
# <a name="zimperium-mobile-threat-defense-connector-with-intune"></a>Соединитель Mobile Threat Defense Zimperium с Intune

Вы можете управлять доступом к корпоративным ресурсам с мобильных устройств посредством условного доступа на основании оценки рисков, проведенной Zimperium, — решением для защиты от угроз на мобильных устройствах, интегрированным с Microsoft Intune. Оценка рисков основана на данных телеметрии, собранных с устройств, на которых выполняется приложение Zimperium.

Вы можете настроить политики условного доступа на основе оценки рисков Zimperium, реализуемой с помощью политик соответствия устройств Intune для зарегистрированных устройств. Эти политики также позволяют разрешать или блокировать доступ к корпоративным ресурсам с устройств, не соответствующих требованиям в зависимости от обнаруженных угроз. Для незарегистрированных устройств можно использовать политики защиты приложений для принудительного применения блокировки или выборочной очистки на основе обнаруженных угроз.

## <a name="supported-platforms"></a>Поддерживаемые платформы

- **Android 4.1 и более поздней версии**.

- **iOS 8 и более поздние версии**

## <a name="prerequisites"></a>Предварительные условия

- Azure Active Directory Premium

- Подписка Microsoft Intune

- Подписка на службу Mobile Threat Defense Zimperium

  - Дополнительные сведения см. на [веб-сайте Zimperium](https://www.zimperium.com/zips-mobile-ips).

## <a name="how-do-intune-and-zimperium-help-protect-your-company-resources"></a>Как Intune и Zimperium помогают защитить ресурсы вашей организации?

Мобильное приложение Zimperium для Android или iOS/iPadOS регистрирует сведения о файловой системе и сетевом стеке, а также данные телеметрии устройств и приложений (при наличии), и отправляет их в облачную службу Zimperium для оценки риска в отношении угроз для мобильного устройства.

- **Поддержка зарегистрированных устройств**. Политика соответствия устройств Intune содержит правило для Mobile Threat Defense (MTD), которое может использовать сведения об оценке рисков из Zimperium. При включении этого правила Intune оценивает соответствие устройства заданной политике. Если устройство определяется как несоответствующее, его доступ к таким ресурсам, как Exchange Online и SharePoint Online, блокируется. Пользователи заблокированных устройств получают от мобильного приложения Zimperium рекомендации по устранению проблемы и восстановлению доступа к корпоративным ресурсам. Для поддержки использования Zimperium на зарегистрированных устройствах выполните следующие действия.
  - [Добавьте приложения MTD на устройства](../protect/mtd-apps-ios-app-configuration-policy-add-assign.md)
  - [Создайте политику соответствия устройств, которая поддерживает MTD](../protect/mtd-device-compliance-policy-create.md)
  - [Включите соединитель MTD в Intune](../protect/mtd-connector-enable.md)

- **Поддержка незарегистрированных устройств**. Intune может использовать данные оценки рисков из приложения Zimperium на незарегистрированных устройствах при использовании политик защиты приложений Intune. Администраторы могут применять эти сведения для защиты корпоративных данных в [защищенных Microsoft Intune приложениях](../apps/apps-supported-intune-apps.md), а также применять блокировку или выборочную очистку корпоративных данных на этих незарегистрированных устройствах. Для поддержки использования Zimperium на незарегистрированных устройствах выполните следующие действия.
  - [Добавьте приложение MTD на незарегистрированные устройства](../protect/mtd-add-apps-unenrolled-devices.md)
  - [Создайте политику защиты приложений Mobile Threat Defense](../protect/mtd-app-protection-policy.md)
  - [Включите соединитель MTD в Intune для незарегистрированных устройств](../protect/mtd-enable-unenrolled-devices.md)
  
## <a name="sample-scenarios"></a>Примеры сценариев

Ниже приведены некоторые сценарии интеграции Zimperium с Intune.

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Управление доступом на основании оценки угроз от вредоносных приложений

При обнаружении на устройствах вредоносного ПО можно заблокировать до устранения угрозы следующие функции.

- Подключение к корпоративной электронной почте

- Синхронизация корпоративных файлов с помощью приложения OneDrive для работы

- Доступ к приложениям организации

*Блокировка при обнаружении вредоносных программ:*

> [!div class="mx-imgBorder"]
> ![Схематическое изображение обнаруженных вредоносных приложений](./media/zimperium-mobile-threat-defense-connector/Maliciousapps-blocked-zimperium.png)

*Доступ предоставлен после устранения угрозы:*

> [!div class="mx-imgBorder"]
> ![Схематическое изображение предоставления доступа после устранения угрозы](./media/zimperium-mobile-threat-defense-connector/maliciousapps-unblocked-zimperium.png)

### <a name="control-access-based-on-threat-to-network"></a>Управление доступом на основе угроз для сети

Обнаружение угроз типа **злоумышленник в середине** и защита доступа к сетям Wi-Fi на основе рисков для устройств.

*Блокировка доступа к сети через Wi-Fi:*

> [!div class="mx-imgBorder"]
> ![Блокировка доступа к сети через Wi-Fi](./media/zimperium-mobile-threat-defense-connector/network-wifi-blocked-zimperium.png)

*Доступ предоставлен после устранения угрозы:*

> [!div class="mx-imgBorder"]
> ![Доступ предоставляется после устранения угрозы](./media/zimperium-mobile-threat-defense-connector/network-wifi-unblocked-zimperium.png)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Управление доступом к SharePoint Online на основании оценки угрозы для сети

Обнаружение угроз типа **злоумышленник в середине** и предотвращение синхронизации корпоративных файлов на основе риска для устройств.

*Блокирование SharePoint Online при обнаружении сетевых угроз:*

> [!div class="mx-imgBorder"]
> ![Блокировка SharePoint Online при обнаружении сетевых угроз](./media/zimperium-mobile-threat-defense-connector/network-spo-blocked-zimperium.png)

*Доступ предоставлен после устранения угрозы:*

> [!div class="mx-imgBorder"]
> ![Пример предоставления доступа к Sharepoint после устранения угрозы](./media/zimperium-mobile-threat-defense-connector/network-spo-unblocked-zimperium.png)

### <a name="control-access-on-unenrolled-devices-based-on-threats-from-malicious-apps"></a>Управление доступом на незарегистрированных устройствах на основании оценки угроз от вредоносных приложений

Когда решение Zimperium Mobile Threat Defense считает, что устройство заражено

> [!div class="mx-imgBorder"]
> ![Политика защиты приложений блокируется из-за обнаруженных вредоносных программ](./media/zimperium-mobile-threat-defense-connector/zimperium-mobile-app-policy-block.png)

Доступ предоставляется после устранения угрозы:

> [!div class="mx-imgBorder"]
> ![Доступ предоставляется после устранения угрозы для политики защиты приложений](./media/zimperium-mobile-threat-defense-connector/zimperium-mobile-app-policy-remediated.png)

## <a name="next-steps"></a>Дальнейшие действия

- [Интеграция Zimperium с Intune](zimperium-mtd-connector-integration.md)

- [Настройка приложений Zimperium](mtd-apps-ios-app-configuration-policy-add-assign.md)

- [Создание политики соответствия устройств Zimperium](mtd-device-compliance-policy-create.md)

- [Включение соединителя MTD Zimperium](mtd-connector-enable.md)

- [Создание политики защиты приложений MTD](../protect/mtd-app-protection-policy.md)
