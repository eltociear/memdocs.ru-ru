---
title: Соединитель Better Mobile Threat Defense в Intune
titleSuffix: Intune on Azure
description: Настройте соединитель Better Mobile Threat Defense в Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/09/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 05dec05cdc5a16078328d736d2f622cea1b2aa00
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "79353987"
---
# <a name="better-mobile-threat-defense-connector-with-intune"></a>Соединитель Better Mobile Threat Defense в Intune

Вы можете управлять доступом с мобильных устройств к корпоративным ресурсам, используя условный доступ на основе оценки рисков. Такую возможность дает вам Better Mobile — решение Mobile Threat Defense (MTD), интегрируемое с Microsoft Intune. Оценка рисков основана на телеметрии, собираемой с устройств с запущенным приложением Better Mobile.

Вы можете настроить политики условного доступа на основе оценки рисков Better Mobile, реализуемой с помощью политик соответствия устройств Intune для зарегистрированных устройств. Эти политики также позволяют разрешать или блокировать доступ к корпоративным ресурсам с устройств, не соответствующих требованиям в зависимости от обнаруженных угроз. Для незарегистрированных устройств можно использовать политики защиты приложений для принудительного применения блокировки или выборочной очистки на основе обнаруженных угроз.

## <a name="how-do-intune-and-better-mobile-help-protect-your-company-resources"></a>Каким образом Intune и Better Mobile помогают защитить ресурсы вашей организации?

Приложение Better Mobile устанавливается и запускается на мобильных устройствах. Оно собирает данные телеметрии по файловой системе, сетевому стеку, устройствам и приложениям (при наличии) и отправляет эти данные в облачную службу Better Mobile для оценки на устройстве риска мобильных угроз.

- **Поддержка зарегистрированных устройств**. Политика соответствия устройств Intune содержит правило для Mobile Threat Defense (MTD), которое может использовать сведения об оценке рисков из Better Mobile. При включении этого правила Intune оценивает соответствие устройства заданной политике. Если устройство определяется как несоответствующее, его доступ к таким ресурсам, как Exchange Online и SharePoint Online, блокируется. Пользователи также получают от приложения Better Mobile, установленного на устройстве, рекомендации по устранению проблемы и восстановлению доступа к корпоративным ресурсам. Для поддержки использования Better Mobile на зарегистрированных устройствах выполните следующие действия.
  - [Добавьте приложения MTD на устройства](../protect/mtd-apps-ios-app-configuration-policy-add-assign.md)
  - [Создайте политику соответствия устройств, которая поддерживает MTD](../protect/mtd-device-compliance-policy-create.md)
  - [Включите соединитель MTD в Intune](../protect/mtd-connector-enable.md)

- **Поддержка незарегистрированных устройств**. Intune может использовать данные оценки рисков из приложения Better Mobile на незарегистрированных устройствах при использовании политик защиты приложений Intune. Администраторы могут применять эти сведения для защиты корпоративных данных в [защищенных Microsoft Intune приложениях](../apps/apps-supported-intune-apps.md), а также применять блокировку или выборочную очистку корпоративных данных на этих незарегистрированных устройствах. Для поддержки использования Better Mobile на незарегистрированных устройствах выполните следующие действия.
  - [Добавьте приложение MTD на незарегистрированные устройства](../protect/mtd-add-apps-unenrolled-devices.md)
  - [Создайте политику защиты приложений Mobile Threat Defense](../protect/mtd-app-protection-policy.md)
  - [Включите соединитель MTD в Intune для незарегистрированных устройств](../protect/mtd-enable-unenrolled-devices.md)

## <a name="supported-platforms"></a>Поддерживаемые платформы

- **Android 4.1 и более поздней версии**.

- **Устройства iOS 8.0 и более поздних версий**

## <a name="prerequisites"></a>Предварительные условия

- Azure Active Directory Premium

- Подписка на Microsoft Intune

- Подписка на Better Mobile Threat Defense

  - Дополнительные сведения см. на [веб-сайте Better Mobile](https://www.better.mobi/).

## <a name="sample-scenarios"></a>Примеры сценариев

Далее приведены некоторые распространенные сценарии.

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Управление доступом на основании оценки угроз от вредоносных приложений

При обнаружении на устройствах вредоносного ПО можно заблокировать следующие действия до устранения угрозы:

- Подключение к корпоративной электронной почте

- Синхронизация корпоративных файлов с помощью приложения OneDrive для работы

- Доступ к приложениям организации

Блокировка при обнаружении вредоносных программ:

![Изображение обнаруженных вредоносных приложений](./media/better-mobile-threat-defense-connector/better-mobile-maliciousapps-blocked.png)

Доступ предоставляется после устранения угрозы:

![Обнаружены вредоносные приложения, доступ предоставлен](./media/better-mobile-threat-defense-connector/better-mobile-maliciousapps-unblocked.png)

### <a name="control-access-based-on-threat-to-network"></a>Управление доступом на основе угроз для сети

Обнаружение угроз для вашей сети, таких как атаки **злоумышленник в середине**, и защита доступа к сети Wi-Fi на основе рисков, связанных с устройствами.

Блокировка доступа к сети через Wi-Fi:

![Блокировка доступа к сети через Wi-Fi](./media/better-mobile-threat-defense-connector/better-mobile-network-wifi-blocked.png)

Доступ предоставляется после устранения угрозы:

![Изображение предоставления доступа после устранения угрозы](./media/better-mobile-threat-defense-connector/better-mobile-network-wifi-unblocked.png)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Управление доступом к SharePoint Online на основе оценки угроз для сети

Обнаружение угроз для вашей сети, таких как атаки **злоумышленник в середине**, и блокирование синхронизации корпоративных файлов на основании риска для устройства.

Блокировка SharePoint Online при обнаружении сетевых угроз:

![Блокировка SharePoint Online при обнаружении сетевых угроз](./media/better-mobile-threat-defense-connector/better-mobile-network-spo-blocked.png)

Доступ предоставлен после устранения угрозы:

![Пример предоставления доступа к Sharepoint после устранения угрозы](./media/better-mobile-threat-defense-connector/better-mobile-network-spo-unblocked.png)

### <a name="control--access-on-unenrolled-devices-based-on-threats-from-malicious-apps"></a>Управление доступом на незарегистрированных устройствах на основании оценки угроз от вредоносных приложений

Когда решение BETTER Mobile Threat Defense считает, что устройство заражено: ![Политика защиты приложений блокируется из-за обнаруженных вредоносных программ](./media/better-mobile-threat-defense-connector/better-mobile-app-policy-block.png)

Доступ предоставляется после устранения угрозы:

![Доступ предоставляется после устранения угрозы для политики защиты приложений](./media/better-mobile-threat-defense-connector/better-mobile-app-policy-remediated.png)

## <a name="next-steps"></a>Дальнейшие шаги

- [Интеграция Better Mobile с Intune](better-mobile-mtd-connector-integration.md)

- [Настройка приложений Better Mobile](mtd-apps-ios-app-configuration-policy-add-assign.md)

- [Создание политики соответствия устройств Better Mobile](mtd-device-compliance-policy-create.md)

- [Включение MTD-соединителя Better Mobile](mtd-connector-enable.md)

- [Создание политики защиты приложений MTD](mtd-app-protection-policy.md) 
