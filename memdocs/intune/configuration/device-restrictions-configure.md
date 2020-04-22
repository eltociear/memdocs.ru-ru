---
title: Ограничение возможностей устройств с помощью политики в Microsoft Intune — Azure | Документация Майкрософт
description: Добавление профиля устройства для ограничения функций на устройствах с администратором устройств Android, Android для бизнеса, Android, macOS, iOS, iPadOS, Windows Phone и Windows 10 в Microsoft Intune.
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
ms.openlocfilehash: 716925f077b7433eab06a6ea2f557c7653d0b03d
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "80551412"
---
# <a name="configure-device-restriction-settings-in-microsoft-intune"></a>Настройка параметров ограничений устройств в Microsoft Intune

Intune включает политики ограничения устройств, которые помогают администраторам контролировать устройства Android, iOS/iPadOS, macOS и Windows. Эти ограничения позволяют контролировать широкий спектр параметров и функций для защиты ресурсов организации. Например, администраторы могут:

- Разрешает или запрещает использование камеры устройства.
- управлять доступом к Google Play, магазинам приложений, просмотру документов и играм;
- блокировать встроенные приложения или создавать список разрешенных или запрещенных приложений;
- разрешать или запрещать резервное копирование файлов в облачные учетные записи и учетные записи хранения;
- устанавливать минимальную длину пароля и блокировать простые пароли.

Эти функции настраиваются администратором и доступны в Intune. Intune использует "профили конфигурации" для создания и настройки этих параметров для вашей организации. После добавления этих компонентов в профиль вы сможете отправлять или развертывать профиль в устройства в своей организации.

В этой статье описано, как создать профиль ограничения для устройств. Также можно увидеть все доступные настройки для разных платформ.

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
        - **Windows 8.1 и более поздние версии**
        - **Windows Phone 8.1**

    - **Профиль**. Выберите **Ограничения устройств**.

        Если вы хотите создать профиль ограничений для устройств Windows 10 для совместной работы, например Surface Hub, выберите **Ограничения для устройств (Windows 10 для совместной работы)** .

4. Щелкните **Создать**.
5. В разделе **Основные** укажите следующие свойства.

    - **Имя** — Введите описательное имя для политики. Назначьте имена политикам, чтобы их можно было легко найти в последствии. Например, хорошее имя политики — **iOS/iPadOS: Блокировать камеру на устройствах**.
    - **Описание**. Введите описание политики. Этот параметр является необязательным, но мы рекомендуем его использовать.

6. Выберите **Далее**.

7. В разделе **Параметры конфигурации** доступные для настройки параметры будут отличаться в зависимости от выбранной платформы. Выберите платформу для настройки дополнительных параметров:

    - [Администратор устройства с Android](device-restrictions-android.md)
    - [Android Enterprise](device-restrictions-android-for-work.md)
    - [iOS/iPadOS](device-restrictions-ios.md)
    - [macOS](device-restrictions-macos.md)
    - [Windows Phone 8.1](device-restrictions-windows-phone-8-1.md)
    - [Windows 8.1](device-restrictions-windows-8-1.md)
    - [Windows 10 и более поздние версии](device-restrictions-windows-10.md)
    - [Windows 10 для совместной работы](device-restrictions-windows-10-teams.md)
    - [Windows Holographic for Business](device-restrictions-windows-holographic.md)

8. Выберите **Далее**.
9. В поле **Теги области** (необязательно) назначьте тег для фильтрации профиля по конкретным ИТ-группам, например `US-NC IT Team` или `JohnGlenn_ITDepartment`. Дополнительные сведения о тегах области см. в разделе [Использование RBAC и тегов области для распределенных ИТ-групп](../fundamentals/scope-tags.md).

    Выберите **Далее**.

10. В поле **Назначения** выберите пользователей или группы, которые будет принимать ваш профиль. Дополнительные сведения о назначении профилей см. в статье [Назначение профилей пользователей и устройств](device-profile-assign.md).

    Выберите **Далее**.

11. В окне **Проверка и создание** проверьте параметры. При выборе **Создать** внесенные изменения сохраняются и назначается профиль. Политика также отображается в списке профилей.

## <a name="next-steps"></a>Дальнейшие шаги

Созданный профиль готов к назначению. Далее [назначьте профиль](device-profile-assign.md) и [отслеживайте его состояние](device-profile-monitor.md).

<!--  Removing image as part of design review; retaining source until we known the disposition.

## Example of device restriction settings

In this high-level example, you'll create a device restriction policy that blocks the use of the built-in camera app on Android devices.

![How to disable the camera on Android devices](./media/device-restrictions-configure/disable-android-camera.png)

-->
