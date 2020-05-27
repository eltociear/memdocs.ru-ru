---
title: Использование Sophos Mobile с Intune
titleSuffix: Intune on Azure
description: Как использовать Sophos Mobile в Microsoft Intune для управления доступом к корпоративным ресурсам с мобильных устройств.
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
ms.assetid: ''
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: be5cf3d0ba83fe1027dcec9dcde50257e30b7c47
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988216"
---
# <a name="sophos-mobile-threat-defense-connector-with-intune"></a>Соединитель Sophos Mobile Threat Defense в Intune
Вы можете управлять доступом с мобильных устройств к корпоративным ресурсам, используя условный доступ на основе оценки рисков. Такую возможность дает вам Sophos Mobile — решение Mobile Threat Defense (MTD), интегрируемое с Microsoft Intune. Оценка рисков основана на телеметрии, собираемой с устройств с запущенным приложением Sophos Mobile.
Вы можете настроить политики условного доступа на основе оценки рисков Sophos Mobile, реализуемой с помощью политик соответствия устройств Intune. Эти политики также позволяют разрешать или блокировать доступ к корпоративным ресурсам с устройств, не соответствующих требованиям в зависимости от обнаруженных угроз.

> [!NOTE]
> Этот поставщик защиты от мобильных угроз не поддерживается для незарегистрированных устройств.

## <a name="supported-platforms"></a>Поддерживаемые платформы

- Android 5.0 и более поздние версии
- iOS 11.0 и более поздние версии

## <a name="prerequisites"></a>Предварительные условия

- Azure Active Directory Premium
- Подписка Microsoft Intune
- Подписка на Sophos Mobile Threat Defense

Дополнительные сведения см. на [веб-сайте Sophos](https://www.sophos.com/products/mobile-control.aspx).

## <a name="how-do-intune-and-sophos-mobile-help-protect-your-company-resources"></a>Как Intune и Sophos Mobile помогают защитить ресурсы вашей организации?

Приложение Sophos Mobile для Android или iOS/iPadOS регистрирует сведения о файловой системе и сетевом стеке, а также данные телеметрии устройств и приложений (при наличии), и отправляет их в облачную службу Sophos Mobile для оценки риска в отношении угроз для мобильного устройства.

Политика соответствия устройств Intune включает правило Sophos Mobile Threat Defense, основанное на оценке рисков Sophos Mobile. При включении этого правила Intune оценивает соответствие устройства заданной политике. Если устройство определяется как несоответствующее, его доступ к таким ресурсам, как Exchange Online и SharePoint Online, блокируется. Пользователи также получают от приложения Sophos Mobile, установленного на устройстве, рекомендации по устранению проблемы и восстановлению доступа к корпоративным ресурсам.  

## <a name="sample-scenarios"></a>Примеры сценариев

Далее приведены некоторые распространенные сценарии.

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Управление доступом на основании оценки угроз от вредоносных приложений

При обнаружении на устройствах вредоносного ПО можно заблокировать следующие действия до устранения угрозы:

- Подключение к корпоративной электронной почте
- Синхронизация корпоративных файлов с помощью приложения OneDrive для работы
- Доступ к приложениям организации

*Блокировка при обнаружении вредоносных программ*:

![Схематическое изображение обнаруженных вредоносных приложений](./media/sophos-mtd-connector/sophos-malicious-apps-blocked.png)  

*Доступ предоставляется после устранения угрозы*:  
![Схематическое изображение предоставления доступа после устранения угрозы](./media/sophos-mtd-connector/sophos-malicious-apps-unblocked.png)

### <a name="control-access-based-on-threat-to-network"></a>Управление доступом на основе угроз для сети

Обнаружение угроз для вашей сети, таких как атаки злоумышленник в середине, и защита доступа к сети Wi-Fi на основе рисков, связанных с устройствами.  

*Блокировка доступа к сети через Wi-Fi*:  
![Блокировка доступа к сети через Wi-Fi](./media/sophos-mtd-connector/sophos-network-wifi-blocked.png)

*Доступ предоставляется после устранения угрозы*:   
![Доступ предоставляется после устранения угрозы](./media/sophos-mtd-connector/sophos-network-wifi-unblocked.png)  

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Управление доступом к SharePoint Online на основании оценки угрозы для сети

Обнаружение угроз для вашей сети, таких как атаки злоумышленник в середине, и блокирование синхронизации корпоративных файлов на основании риска для устройства.  

*Блокировка SharePoint Online при обнаружении сетевых угроз*:

![Блокировка SharePoint Online при обнаружении сетевых угроз](./media/sophos-mtd-connector/sophos-network-spo-blocked.png)  

*Доступ предоставляется после устранения угрозы*:

![Пример предоставления доступа к Sharepoint после устранения угрозы](./media/sophos-mtd-connector/sophos-network-spo-unblocked.png)  

<!-- 
### Control access on unenrolled devices based on threats from malicious apps

When the Sophos Mobile Threat Defense solution considers a device to be infected:

![App protection policy blocks due to detected malware](./media/sophos-mtd-connector/sophos-mobile-app-policy-block.png)

Access is granted on remediation:

![Access is granted on remediation for App protection policy](./media/sophos-mtd-connector/sophos-mobile-app-policy-remediated.png)
-->

## <a name="next-steps"></a>Дальнейшие действия

- [Интеграция Sophos с Intune](sophos-mtd-connector-integration.md)
- [Настройка приложений Sophos](mtd-apps-ios-app-configuration-policy-add-assign.md)
- [Создание политики соответствия устройств Sophos](mtd-device-compliance-policy-create.md)
- [Включение соединителя Sophos MTD](mtd-connector-enable.md)
