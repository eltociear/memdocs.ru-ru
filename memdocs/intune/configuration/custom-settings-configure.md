---
title: Использование настраиваемых параметров устройств в Microsoft Intune — Azure | Документы Майкрософт
description: Добавьте или создайте профиль, чтобы использовать настраиваемые параметры для устройств Windows Phone, Windows 8.1, Windows 10 и более поздних версий, администратора устройства с Android, Android для бизнеса, macOS и iOS/iPadOS с помощью Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/24/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: feb211b1de15aa0400e9ff71b428e2db02ef4b03
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "80551362"
---
# <a name="create-a-profile-with-custom-settings-in-intune"></a>Создайте профиль с настраиваемыми параметрами в Intune

Microsoft Intune включает множество встроенных параметров для управления различными функциями на устройстве. Кроме того, вы можете создавать настраиваемые профили, которые создаются аналогично встроенным профилям. Они очень удобны, когда нужно использовать параметры и функции устройств, которые не встроены в Intune. Эти профили включают в себя функции и параметры, которыми вы можете управлять на устройствах в своей организации. Например, можно создать настраиваемый профиль, который задает одну и ту же функцию для каждого устройства iOS/iPadOS.

Пользовательские параметры настраиваются по-разному для каждой платформы. Например, для управления функциями на устройствах Android и Windows можно указать значения универсального кода ресурсов Open Mobile Alliance (OMA-URI). На устройства Apple можно импортировать файл, созданный с помощью [Apple Configurator](https://itunes.apple.com/us/app/apple-configurator-2/id1037126344?mt=12) или [Apple Profile Manager](https://support.apple.com/profile-manager).

Дополнительные сведения о профилях конфигурации см. в разделе [Что такое профили устройств в Microsoft Intune?](device-profiles.md).

В этой статье показано, как создать настраиваемый профиль для администратора устройства Android, Android для бизнеса, iOS/iPadOS, macOS и Windows. Также можно увидеть все доступные настройки для разных платформ.

> [!NOTE]
> В течение нескольких недель пользовательский интерфейс Intune получит обновление и сможет работать в полноэкранном режиме. В текущей версии процесс создания или изменении параметров может несколько отличаться от описанного в этой статье.

## <a name="create-the-profile"></a>Создание профиля

1. Войдите в [Центр администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Выберите **Устройства** > **Профили конфигурации** > **Создать профиль**.
3. Укажите следующие свойства.

    - **Платформа**. Выберите платформу устройств. Доступны следующие параметры:  

        - **Администратор устройства с Android**
        - **Android Enterprise**
        - **iOS/iPadOS**
        - **macOS**
        - **Windows 10 и более поздних версий**.
        - **Windows Phone 8.1**

    - **Профиль**. Выберите **Пользовательский**.

4. Щелкните **Создать**.
5. В разделе **Основные** укажите следующие свойства.

    - **Имя** — Введите описательное имя для политики. Назначьте имена политикам, чтобы их можно было легко найти в последствии. Например, хорошее имя политики — **Windows 10: настраиваемый профиль, который включает настраиваемые параметры OMA-URI AllowVPNOverCellular**.
    - **Описание**. Введите описание политики. Этот параметр является необязательным, но мы рекомендуем его использовать.

6. Выберите **Далее**.

7. В разделе **Параметры конфигурации** доступные для настройки параметры будут отличаться в зависимости от выбранной платформы. Выберите платформу для настройки дополнительных параметров:

    - [Администратор устройства с Android](custom-settings-android.md)
    - [Android Enterprise](custom-settings-android-for-work.md)
    - [iOS/iPadOS](custom-settings-ios.md)
    - [macOS](custom-settings-macos.md)
    - [Windows 10](custom-settings-windows-10.md)
    - [Windows Holographic for Business](custom-settings-windows-holographic.md)
    - [Windows Phone 8.1](custom-settings-windows-phone-8-1.md)

8. Выберите **Далее**.
9. В поле **Теги области** (необязательно) назначьте тег для фильтрации профиля по конкретным ИТ-группам, например `US-NC IT Team` или `JohnGlenn_ITDepartment`. Дополнительные сведения о тегах области см. в разделе [Использование RBAC и тегов области для распределенных ИТ-групп](../fundamentals/scope-tags.md).

    Выберите **Далее**.

10. В поле **Назначения** выберите пользователей или группы, которые будет принимать ваш профиль. Дополнительные сведения о назначении профилей см. в статье [Назначение профилей пользователей и устройств](device-profile-assign.md).

    Выберите **Далее**.

11. В окне **Проверка и создание** проверьте параметры. При выборе **Создать** внесенные изменения сохраняются и назначается профиль. Политика также отображается в списке профилей.

## <a name="example"></a>Пример

В примере ниже параметр **Connectivity/AllowVPNOverCellular** включен. Он позволяет устройству с Windows 10 открыть VPN-подключение по сети мобильной связи.

> [!div class="mx-imgBorder"]
> ![Пример настраиваемой политики, содержащий параметры VPN, в Intune и Endpoint Manager](./media/custom-settings-configure/custom-policy-example.png)

## <a name="next-steps"></a>Дальнейшие шаги

Профиль создан, но пока в нем ничего нельзя делать. Далее [назначьте профиль](device-profile-assign.md) и [отслеживайте его состояние](device-profile-monitor.md).
