---
title: Устранение неполадок с устройствами Android для бизнеса в Microsoft Intune
description: Рекомендации по устранению распространенных проблем с регистрацией устройств с Android в Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/25/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: mghadial
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: bcc524a69d0fb41da84a2e882b81a205fe7192cc
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "79363334"
---
# <a name="troubleshoot-android-enterprise-device-problems-in-microsoft-intune"></a>Устранение неполадок с устройствами Android для бизнеса в Microsoft Intune

С помощью сведений, приведенных в этой статье, администраторы Intune смогут понять и устранить проблемы, возникающие при регистрации устройств с Android для бизнеса в Intune.

## <a name="apps-on-android-enterprise-devices"></a>Приложения на устройствах Android для бизнеса

### <a name="managed-google-play-apps-that-arent-deployed-through-intune-are-displayed-in-the-work-profile"></a>Управляемые приложения Google Play, не развернутые с помощью Intune, отображаются в рабочем профиле.
Системные приложения могут быть включены в рабочем профиле изготовителем устройства при создании рабочего профиля. Этот процесс не контролируется поставщиком MDM.

Для устранения проблем выполните следующие действия.

  1. Соберите журналы Корпоративного портала.
  2. Обратите внимание на приложения, которые отображаются в рабочем профиле неожиданно.
  3. Отмените регистрацию устройства в Intune и удалите Корпоративный портал.
  4. Установите приложение [Test DPC](https://play.google.com/store/apps/details?id=com.afwsamples.testdpc), которое позволяет создать рабочий профиль без EMM для тестирования.
  5. Следуйте инструкциям в приложении [Test DPC](https://play.google.com/store/apps/details?id=com.afwsamples.testdpc), чтобы создать рабочий профиль на устройстве.
  6. Проверьте приложения, которые отображаются в рабочем профиле. 
  7. Если в приложении Test DPC отображаются те же приложения, изготовитель ожидает их наличия на устройстве.

### <a name="unapproved-managed-google-play-for-work-store-apps-arent-being-removed-from-the-client-apps-page-in-intune"></a>Неутвержденные управляемые приложения Google Play для работы не удаляются со страницы клиентских приложений в Intune
Это нормальная ситуация.

### <a name="managed-google-play-apps-arent-being-reported-under-the-discovered-apps-blade-in-the-intune-portal"></a>Управляемые приложения Google Play не отображаются в колонке "Обнаруженные приложения" на портале Intune
Это нормальная ситуация. Только системные приложения, установленные в рабочем профиле, включаются в колонку "Обнаруженные приложения". Чтобы просмотреть установленные управляемые приложения Google Play, перейдите в колонку **Управляемые приложения**.

### <a name="are-web-applications-supported-for-work-profile-enrolled-devices"></a>Поддерживаются ли веб-приложения для зарегистрированных устройств с рабочим профилем?
Да. Дополнительные сведения см. в статье [Веб-ссылки в управляемом Google Play](../apps/apps-add-android-for-work.md#managed-google-play-web-links)

## <a name="device-management"></a>Управление устройствами

### <a name="file-path-internal-storageandroiddatacommicrosoftwindowsintunecompanyportalfiles-missing-on-work-profile-enrolled-devices"></a>Путь к файлу Internal storage/Android/Data.com.microsoft.windowsintune.companyportal/files отсутствует на зарегистрированных устройствах с рабочим профилем

  **Ответ**. Это нормальная ситуация. Этот путь создается только для сценария "Администратор устройства" (устаревшая регистрация Android).

  Чтобы получить журналы Корпоративного портала, выполните следующие действия.

  1. В приложении Корпоративного портала со значком коснитесь **Меню** > **Справка** > **Поддержка по электронной почте**, а затем коснитесь **Отправить сообщение электронной почты и передать журналы**. 
  2. При появлении запроса **Отправить запрос на поддержку с помощью** выберите одно из почтовых приложений.
  3. Для ИТ-администратора создается сообщение электронной почты с идентификатором инцидента, который может быть предоставлен службе технической поддержки Майкрософт.

### <a name="managed-google-play-last-sync-time--hasnt-been-updated-in-days"></a>Последняя синхронизация управляемого Google Play выполнена давно
Это нормальная ситуация. Синхронизация происходит только тогда, когда вы выполняете ее вручную.

### <a name="encryption-is-required-when-a-device-is-enrolled-can-it-be-turned-off"></a>При регистрации устройства требуется шифрование. Можно ли его отключить?
Нет. Google требует, чтобы устройство было зашифровано для создания рабочего профиля. 

### <a name="samsung-devices-are-blocking-the-use-of-third-party-keyboards-like-swiftkey"></a>Устройства Samsung блокируют использование клавиатур сторонних производителей, таких как SwiftKey
Samsung применяет это ограничение начиная с устройств Android 8.0. Корпорация Майкрософт в настоящее время пытается решить этот вопрос с Samsung и опубликует новые сведения, когда они появятся.

## <a name="remote-actions"></a>Удаленные действия

### <a name="wipe-factory-reset-option-isnt-available-for-work-profile-enrolled-device"></a>Параметр очистки (сброс заводских настроек) недоступен для зарегистрированного устройства с рабочим профилем
Это нормальная ситуация. При наличии рабочего профиля поставщик MDM не имеет полного контроля над устройством. Единственный доступный вариант — "Прекратить использование" (Удаление корпоративных данных). Он удаляет весь рабочий профиль и все его содержимое.

### <a name="is-device-passcode-reset-supported"></a>Сброс секретного кода устройства поддерживается?
Для зарегистрированных устройств с рабочим профилем можно сбросить секретный код рабочего профиля на устройствах Android 8.0 или более поздней версии только в следующих случаях:
- секретный код рабочего профиля является управляемым;
- конечный пользователь разрешил вам сбросить его.

Для выделенных устройств (COSU) и полностью управляемых устройств сброс секретного кода устройства поддерживается.


## <a name="next-steps"></a>Дальнейшие шаги

- [Устранение проблем при регистрации устройств в Intune](troubleshoot-device-enrollment-in-intune.md)
- [Задайте вопрос на форуме Intune](https://social.technet.microsoft.com/Forums/%7Blang-locale%7D/home?category=microsoftintune&filter=alltypes&sort=lastpostdesc)
- [См. блог группы поддержки Microsoft Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/bg-p/IntuneCustomerSuccess)
- [См. блог разработчиков Microsoft Enterprise Mobility + Security](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-Identity/Announcing-the-public-preview-of-Azure-AD-group-based-license/ba-p/245210)