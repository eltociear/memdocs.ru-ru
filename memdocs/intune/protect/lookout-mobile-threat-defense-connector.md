---
title: Соединитель Lookout MTD в Microsoft Intune
titleSuffix: Microsoft Intune
description: Сведения об интеграции Intune с Lookout Mobile Threat Defense (MTD) для управления доступом к корпоративным ресурсам с мобильных устройств.
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
ms.assetid: 3a730a5d-2a90-42b0-aa28-aadfc7a18788
ms.reviewer: davera
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7c3ca25ce4bf4f6520e7ef5f7e3aaaff958060a2
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990804"
---
# <a name="lookout-mobile-endpoint-security-connector-with-intune"></a>Соединитель Lookout Mobile Endpoint Security с Intune

Вы можете управлять доступом к корпоративным ресурсам с мобильных устройств на основании оценки рисков, проведенной Lookout, решением для защиты от угроз на мобильных устройствах, интегрированным с Microsoft Intune. Оценка рисков основана на данных телеметрии, собранных с устройств службой Lookout и включающих в себя следующее:
- Уязвимости операционной системы
- Установленные вредоносные приложения
- Вредоносные сетевые профили

Вы можете настроить политики условного доступа на основе оценки рисков Lookout, реализуемой с помощью политик соответствия Intune для зарегистрированных устройств. Эти политики также позволяют разрешать или блокировать доступ к корпоративным ресурсам с устройств, не соответствующих требованиям в зависимости от обнаруженных угроз. Для незарегистрированных устройств можно использовать политики защиты приложений для принудительного применения блокировки или выборочной очистки на основе обнаруженных угроз.

## <a name="how-do-intune-and-lookout-mobile-endpoint-security-help-protect-company-resources"></a>Как Intune и Lookout Mobile Endpoint Security помогают защитить ресурсы организации?

Приложение **Lookout for work** устанавливается и выполняется на мобильных устройствах. Оно регистрирует сведения о файловой системе и сетевом стеке, а также данные телеметрии устройства и приложений (при наличии) и отправляет их в облачную службу защиты от угроз на устройстве Lookout для вычисления риска в отношении угроз для мобильного устройства. Вы можете изменить классификации уровней риска для угроз в консоли Lookout, исходя из своих потребностей.

- **Поддержка зарегистрированных устройств**. Политика соответствия устройств Intune содержит правило для Mobile Threat Defense (MTD), которое может использовать сведения об оценке рисков из Lookout for work. При включении этого правила Intune оценивает соответствие устройства заданной политике. Если устройство определяется как несоответствующее, его доступ к таким ресурсам, как Exchange Online и SharePoint Online, блокируется. Пользователи также получают от приложения Lookout for work, установленного на устройстве, рекомендации по устранению проблемы и восстановлению доступа к корпоративным ресурсам. Чтобы включить поддержку использования Lookout for work зарегистрированными устройствами, выполните следующие действия.
  - [Добавьте приложения MTD на устройства](../protect/mtd-apps-ios-app-configuration-policy-add-assign.md)
  - [Создайте политику соответствия устройств, которая поддерживает MTD](../protect/mtd-device-compliance-policy-create.md)
  - [Включите соединитель MTD в Intune](../protect/mtd-connector-enable.md)

- **Поддержка незарегистрированных устройств**. Intune может использовать данные оценки рисков из приложения Lookout for work на незарегистрированных устройствах при использовании политик защиты приложений Intune. Администраторы могут применять эти сведения для защиты корпоративных данных в [защищенных Microsoft Intune приложениях](../apps/apps-supported-intune-apps.md), а также применять блокировку или выборочную очистку корпоративных данных на этих незарегистрированных устройствах. Чтобы включить поддержку использования Lookout for work незарегистрированными устройствами, выполните следующие действия.
  - [Добавьте приложение MTD на незарегистрированные устройства](../protect/mtd-add-apps-unenrolled-devices.md)
  - [Создайте политику защиты приложений Mobile Threat Defense](../protect/mtd-app-protection-policy.md)
  - [Включите соединитель MTD в Intune для незарегистрированных устройств](../protect/mtd-enable-unenrolled-devices.md)

## <a name="supported-platforms"></a>Поддерживаемые платформы

При регистрации в Intune для Lookout поддерживаются следующие платформы:

- **Android 4.1 и более поздней версии**.  
- **iOS 8 и более поздние версии**  

Дополнительные сведения о поддержке платформы и языка см. на [веб-сайте Lookout](https://personal.support.lookout.com/hc/articles/114094140253).  

## <a name="prerequisites"></a>Предварительные условия

- Корпоративная подписка на Lookout Mobile Endpoint Security  
- Подписка Microsoft Intune
- Azure Active Directory Premium
- Enterprise Mobility and Security (EMS) E3 или E5 с лицензиями, назначенными пользователям.  

Дополнительные сведения см. на странице [Lookout Mobile Endpoint Security](https://www.lookout.com/products/mobile-endpoint-security).

## <a name="sample-scenarios"></a>Примеры сценариев

Ниже приведены распространенные сценарии при использовании службы Mobile Endpoint Security с Intune.

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Управление доступом на основании оценки угроз от вредоносных приложений

При обнаружении на устройствах вредоносного ПО можно заблокировать следующие возможности до устранения угрозы:

- Подключение к корпоративной электронной почте
- Синхронизация корпоративных файлов с помощью приложения OneDrive для работы
- Доступ к приложениям организации

*Блокировка при обнаружении вредоносных программ:*

> [!div class="mx-imgBorder"]
> ![Схематическое изображение блокирования доступа политикой из-за вредоносных приложений](./media/lookout-mobile-threat-defense-connector/malicious-apps-blocked.png)

*Доступ предоставлен после устранения угрозы:*

> [!div class="mx-imgBorder"]
> ![Схематическое изображение предоставления доступа к устройствам после устранения угрозы](./media/lookout-mobile-threat-defense-connector/malicious-apps-unblocked.png)

### <a name="control-access-based-on-threat-to-network"></a>Управление доступом на основе угроз для сети

Обнаружение угроз для вашей сети, таких как атаки "злоумышленник в середине", и защита доступа к сети Wi-Fi на основе рисков, связанных с устройствами.

*Блокировка доступа к сети через Wi-Fi:*

> [!div class="mx-imgBorder"]
> ![Изображение блокирования доступа к Wi-Fi из-за угроз для сети](./media/lookout-mobile-threat-defense-connector/network-wifi-blocked.png)

*Доступ предоставлен после устранения угрозы:*

> [!div class="mx-imgBorder"]
> ![Схематическое изображение предоставления доступа политикой условного доступа после устранения угрозы](./media/lookout-mobile-threat-defense-connector/network-wifi-unblocked.png)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Управление доступом к SharePoint Online на основании оценки угрозы для сети

Обнаруживайте угрозы для сети, такие как атаки типа "злоумышленник в середине", и запрещайте синхронизацию корпоративных файлов на основе риска устройства.

*Блокирование SharePoint Online при обнаружении сетевых угроз:*

> [!div class="mx-imgBorder"]
> ![Схематическое изображение блокирования доступа к SharePoint Online](./media/lookout-mobile-threat-defense-connector/network-spo-blocked.png)

*Доступ предоставлен после устранения угрозы:*

> [!div class="mx-imgBorder"]
> ![Схематическое изображение предоставления доступа после устранения сетевой угрозы](./media/lookout-mobile-threat-defense-connector/network-spo-unblocked.png)

### <a name="control-access-on-unenrolled-devices-based-on-threats-from-malicious-apps"></a>Управление доступом на незарегистрированных устройствах на основании оценки угроз от вредоносных приложений

Когда решение Lookout Mobile Threat Defense считает, что устройство заражено:
> [!div class="mx-imgBorder"]
> ![Политика защиты приложений блокируется из-за обнаруженных вредоносных программ](./media/lookout-mobile-threat-defense-connector/lookout-app-policy-block.png)

Доступ предоставляется после устранения угрозы:

> [!div class="mx-imgBorder"]
> ![Доступ предоставляется после устранения угрозы для политики защиты приложений](./media/lookout-mobile-threat-defense-connector/lookout-app-policy-remediated.png)

## <a name="next-steps"></a>Дальнейшие действия

Вот основные шаги по реализации этого решения:

- [Настройка интеграции с Lookout](lookout-mtd-connector-integration.md)
- [Включение Mobile Endpoint Security в Intune](mtd-connector-enable.md)
- [Добавление и назначение приложения Lookout for Work](mtd-apps-ios-app-configuration-policy-add-assign.md)
- [Настройка политики соответствия устройств Lookout](mtd-device-compliance-policy-create.md)
- [Создание политики защиты приложений MTD](mtd-app-protection-policy.md)
