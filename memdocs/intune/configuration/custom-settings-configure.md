---
title: Использование настраиваемых параметров устройств в Microsoft Intune — Azure | Документы Майкрософт
description: Добавьте или создайте профиль, чтобы использовать настраиваемые параметры для устройств Windows Phone, Windows 8.1, Windows 10 и более поздних версий, администратора устройства с Android, Android для бизнеса, macOS и iOS/iPadOS с помощью Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/18/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6122f4624cc40152184c1c460afa6a7a39976063
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/21/2020
ms.locfileid: "80083985"
---
# <a name="create-a-profile-with-custom-settings-in-intune"></a>Создайте профиль с настраиваемыми параметрами в Intune

Microsoft Intune включает множество встроенных параметров для управления различными функциями на устройстве. Кроме того, вы можете создавать настраиваемые профили, которые создаются аналогично встроенным профилям. Они очень удобны, когда нужно использовать параметры и функции устройств, которые не встроены в Intune. Эти профили включают в себя функции и параметры, которыми вы можете управлять на устройствах в своей организации. Например, можно создать настраиваемый профиль, который задает одну и ту же функцию для каждого устройства iOS/iPadOS.

Пользовательские параметры настраиваются по-разному для каждой платформы. Например, для управления функциями на устройствах Android и Windows можно указать значения универсального кода ресурсов Open Mobile Alliance (OMA-URI). На устройства Apple можно импортировать файл, созданный с помощью [Apple Configurator](https://itunes.apple.com/us/app/apple-configurator-2/id1037126344?mt=12) или [Apple Profile Manager](https://support.apple.com/profile-manager).

Дополнительные сведения о профилях конфигурации см. в разделе [Что такое профили устройств в Microsoft Intune?](device-profiles.md).

В этой статье показано, как создать настраиваемый профиль для администратора устройства Android, Android для бизнеса, iOS/iPadOS, macOS и Windows. Также можно увидеть все доступные настройки для разных платформ.

## <a name="create-the-profile"></a>Создание профиля

1. Войдите в [Центр администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Выберите **Устройства** > **Профили конфигурации** > **Создать профиль**.
3. Укажите следующие свойства.

    - **Имя** — Введите описательное имя для политики. Назначьте имена политикам, чтобы их можно было легко найти в последствии. Например, хорошее имя политики — **Windows 10: настраиваемый профиль, который включает настраиваемые параметры OMA-URI AllowVPNOverCellular**.
    - **Описание**. Введите описание профиля. Этот параметр является необязательным, но мы рекомендуем его использовать.
    - **Платформа**. Выберите платформу устройств. Доступны следующие параметры:

      - **Администратор устройства с Android**
      - **Android Enterprise**
      - **iOS/iPadOS**
      - **macOS**
      - **Windows 10 и более поздних версий**.
      - **Windows 8.1 и более поздние версии**

    - **Тип профиля**: Выберите **Пользовательский**.

4. Параметры для каждой платформы различаются. Чтобы просмотреть параметры для конкретной платформы, выберите свою платформу:

    - [Администратор устройства с Android](custom-settings-android.md)
    - [Android Enterprise](custom-settings-android-for-work.md)
    - [iOS/iPadOS](custom-settings-ios.md)
    - [macOS](custom-settings-macos.md)
    - [Windows 10](custom-settings-windows-10.md)
    - [Windows Holographic for Business](custom-settings-windows-holographic.md)
    - [Windows Phone 8.1](custom-settings-windows-phone-8-1.md)

5. Когда все будет готово, выберите **Создать профиль** > **Создать**.

Созданный профиль отобразится в списке профилей (**Конфигурация устройства** > **Профили**).

## <a name="next-steps"></a>Дальнейшие шаги

Созданный профиль готов к назначению. Далее [назначьте профиль](device-profile-assign.md) и [отслеживайте его состояние](device-profile-monitor.md).
