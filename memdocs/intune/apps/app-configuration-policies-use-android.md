---
title: Добавление политик конфигурации приложений для управляемых устройств Android Enterprise
titleSuffix: Microsoft Intune
description: Используйте политики конфигурации приложений в Microsoft Intune для предоставления параметров, когда пользователи запускают приложение управляемого Google Play.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/15/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: d0b6f3fe-2bd4-4518-a6fe-b9fd115ed5e0
ms.reviewer: chrisbal
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: eb376e9574dcbbbefca3c089dc4180356b1d5a89
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988758"
---
# <a name="add-app-configuration-policies-for-managed-android-enterprise-devices"></a>Добавление политик конфигурации приложений для управляемых устройств Android Enterprise

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Политики конфигурации приложений в Microsoft Intune предоставляют параметры для управляемых приложений Google Play на управляемых устройствах Android Enterprise. Разработчик приложения предоставляет параметры конфигурации приложения под управлением Android. Intune использует эти предоставленные параметры, чтобы предоставить администратору возможность настраивать функции для приложения. Политика конфигурации приложения назначается группам пользователей. Параметры политики используются каждый раз, когда приложение проверяет их значения (как правило, при первом запуске).

> [!NOTE]  
> Конфигурацию приложений поддерживают не все приложения. Обратитесь к разработчику приложения, чтобы узнать, поддерживает ли его приложение политики конфигурации приложения.

1. Войдите в [Центр администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Выберите **Приложения** > **Политики конфигурации приложений** > **Добавить** > **Управляемые устройства**. Обратите внимание, что вы можете выбрать между пунктами **Управляемые устройства** и **Управляемые приложения**. Дополнительные сведения см. в разделе [Приложения, поддерживающие конфигурацию приложений](app-configuration-policies-overview.md#apps-that-support-app-configuration).
3. На странице **Основные** добавьте следующие сведения.
    - **Имя**. Имя профиля, которое отображается на портале Azure.
    - **Описание**. Описание профиля, которое отображается на портале Azure.
    - **Тип регистрации устройства** — этот параметр имеет значение **Управляемые устройства**.
4. В качестве **платформы** выберите **Android для бизнеса**.
5. Щелкните **Выбрать приложение** рядом с пунктом **Целевое приложение**. Откроется панель **Связанное приложение**. 
6. В области **Связанное приложение** выберите управляемое приложение, которое нужно связать с политикой конфигурации, и нажмите кнопку **ОК**.
7. Нажмите кнопку **Далее**, чтобы отобразить страницу **Параметры**.
8. Щелкните **Добавить**, чтобы отобразить область **Добавление разрешений**.
9. Щелкните разрешения, которые нужно переопределить. Предоставляемые разрешения переопределят политику "Разрешения приложения по умолчанию" для выбранных приложений.
10. Задайте **Состояние разрешения** для каждого разрешения. Вы можете выбрать между **Запрашивать**, **Разрешать автоматически**или **Запрещать автоматически**. Дополнительные сведения см. [Android Enterprise settings to mark devices as compliant or not compliant using Intune](../protect/compliance-policy-create-android-for-work.md) (Параметры Android для бизнеса, позволяющие пометить устройства как соответствующие или не соответствующие политике с помощью Intune).
11. Если управляемое приложение поддерживает параметры конфигурации, в раскрывающемся списке отображается пункт **Формат параметров конфигурации**. Выберите один из следующих методов, чтобы добавить сведения о конфигурации:
    - **Использовать конструктор конфигурации**
    - **Использование редактора JSON**<br><br>
    Дополнительные сведения об использовании конструктора конфигураций см. в разделе [Использование конструктора конфигураций](#use-the-configuration-designer). Дополнительные сведения о вводе XML-данных см. в разделе [Использование редактора JSON](#enter-json-data).
12. Нажмите кнопку **Далее**, чтобы перейти на страницу **Назначения**.
13. В раскрывающемся списке рядом с **Кому назначить** выберите либо **Выбранные группы**, **Все пользователи**, **Все устройства** или **All users and all devies** (Все пользователи и все устройства), чтобы назначить политику конфигурации приложений.

    ![Снимок экрана: вкладка "Включить" на странице назначений политик](./media/app-configuration-policies-use-ios/app-config-policy01.png)

14. Выберите **Все пользователи** из раскрывающегося списка.

    ![Снимок экрана: раскрывающийся список "Назначения политик — все пользователи"](./media/app-configuration-policies-use-ios/app-config-policy02.png)

15. Щелкните **Выбрать группы для исключения**, чтобы открыть соответствующую панель.

    ![Снимок экрана: панель "Назначения политик" и "Выбрать группы для исключения"](./media/app-configuration-policies-use-ios/app-config-policy03.png)

16. Выберите группы, которые требуется исключить, и щелкните **Выбрать**.

    >[!NOTE]
    >Если при добавлении группы какая-то другая группа уже включена с выбранным типом назначения, этот тип станет для нее фиксированным, и выбрать для нее какой-то другой тип назначения будет невозможно. Поэтому вы не сможете исключить эту уже используемую группу.

17. Выберите **Далее**, чтобы перейти на страницу **Просмотр и создание**.
18. Щелкните **Создать**, чтобы добавить политику конфигурации приложений в Intune.

## <a name="use-the-configuration-designer"></a>Использование конструктора конфигурации

Если приложение поддерживает параметры конфигурации, для управляемых приложений Google Play можно использовать конструктор конфигурации. Конфигурация применяется к устройствам, зарегистрированным в Intune. Конструктор позволяет настраивать конкретные значения конфигурации для параметров, предоставляемых приложением.

1. Нажмите кнопку **Добавить**. Выберите список параметров конфигурации, которые необходимо ввести для приложения.

    Если для своего почтового приложения вы используете GMail или Nine Work, см. раздел [Настройки устройства Android Enterprise для конфигурации электронной почты](../configuration/email-settings-android-enterprise.md) для получения дополнительных сведений об этих настройках.

2. Для каждого ключа и значения в конфигурации задайте следующие параметры.

    - **Тип значения**: Тип данных значения конфигурации. В качестве типов значений String можно при необходимости выбрать переменную или профиль сертификата.
    - **Значение конфигурации**: Значение для конфигурации. Если в качестве **типа значения** задается переменная или сертификат, можно воспользоваться списком переменных или профилей сертификатов. При выборе сертификата псевдоним сертификата, развернутого на устройстве, заполняется во время выполнения.

### <a name="supported-variables-for-configuration-values"></a>Поддерживаемые переменные для значений конфигурации

Если в качестве типа значения вы останавливаетесь на переменной, можно выбрать следующие параметры.

| Параметр | Пример |
|----|----|
| Идентификатор устройства AAD | dc0dc142-11d8-4b12-bfea-cae2a8514c82 |
| Идентификатор учетной записи | fc0dc142-71d8-4b12-bbea-bae2a8514c81 |
| Идентификатор устройства Intune | b9841cd9-9843-405f-be28-b2265c59ef97 |
| Домен | contoso.com |
| Mail | john@contoso.com |
| Частичное имя участника-пользователя | john |
| ИД пользователя | 3ec2c00f-b125-4519-acf0-302ac3761822 |
| Имя пользователя | John Doe |
| Имя субъекта-пользователя | john@contoso.com |

### <a name="allow-only-configured-organization-accounts-in-multi-identity-apps"></a>Разрешение использовать только настроенные учетные записи организации в приложениях с несколькими удостоверениями 

Администраторы Microsoft Intune могут контролировать добавление учетных записей в приложения Microsoft на управляемых устройствах. Вы можете ограничивать доступ только для учетных записей разрешенных организаций и блокировать личные учетные записи на зарегистрированных устройствах. Для устройств Android используйте следующие пары "ключ-значение":

| **Key** | com.microsoft.intune.mam.AllowedAccountUPNs |
|---|---|
| **Значения** | <ul><li>Одно или несколько имен участников-пользователей, разделенных <code>;</code>.</li><li>Разрешены только управляемые учетные записи разрешено, определяемые этим ключом.</li><li> Для устройств, зарегистрированных в Intune, маркер <code>{{userprincipalname}}</code> может использоваться для представления учетной записи зарегистрированного пользователя.</li></ul> |

   > [!NOTE]
   > Следующие приложения обрабатывают описанную выше конфигурацию приложения и разрешают только учетные записи организации:
   > - Edge для Android (42.0.4.4048 и более поздней версии)
   > - Office, Word, Excel, PowerPoint для Android (16.0.9327.1000 и более поздней версии)
   > - OneDrive для Android (5.28 и более поздней версии)
   > - Outlook для Android (2.2.222 и более поздней версии)

## <a name="enter-json-data"></a>Использование редактора JSON

Некоторые параметры конфигурации в приложениях (например, приложения с типами пакетов) нельзя настроить с помощью конструктора конфигураций. Для работы с такими значениями используйте редактор JSON. Параметры передаются в приложение автоматически при его установке.

1. В разделе **Формат параметров конфигурации** выберите **Использовать редактор JSON**.
2. В редакторе вы можете определить значения JSON для параметров конфигурации. Вы можете скачать образец файла конфигурации с помощью команды **Скачать шаблон JSON**.
3. Нажмите кнопку **ОК**, а затем выберите **Добавить**.

Созданная вами политика отображается в списке.

Назначенное приложение запускается на устройстве с параметрами, настроенными в политике конфигурации приложений.

## <a name="preconfigure-the-permissions-grant-state-for-apps"></a>Предварительная настройка состояния предоставления разрешений для приложений

Можно также предварительно настроить разрешения на доступ к возможностям устройства Android для приложения. По умолчанию приложения Android, которым требуются права доступа к устройству, например доступ к данным о расположении или камере устройства, предлагают пользователям разрешить или запретить доступ.

Например, приложение использует микрофон устройства. Пользователю предлагается предоставить приложению разрешение на использование микрофона.

1. В [Центре администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) выберите **Приложения** > **Политики конфигурации приложений** >  **Добавить** > **Управляемые устройства**.
2. Добавьте следующие свойства:

    - **Имя** — Введите описательное имя для политики. Назначьте имена политикам, чтобы их можно было легко найти в последствии. Например, правильное имя политики: **Политика приложения Android Enterprise разрешений для приглашений для всей компании**.
    - **Описание**. Введите описание профиля. Этот параметр является необязательным, но мы рекомендуем его использовать.
    - **Тип регистрации устройства**: этот параметр имеет значение **Управляемые устройства**.
    - **Платформа**. Выберите **Android**.

3. Выберите **Связанное приложение**. Выберите приложение, для которого требуется определить политику конфигурации. Для выбора используйте список приложений в рабочем профиле Android, которые были утверждены и синхронизированы в Intune.
4. Выберите **Разрешения** > **Добавить**. В списке выберите доступные разрешения приложения > **OK**.
5. Для каждого разрешения настройте его предоставление в рамках этой политики:
    - **Командная строка**. запрос на разрешение или запрет доступа.
    - **Разрешать автоматически**. Автоматическое разрешение без уведомления пользователя.
    - **Запрещать автоматически**. Автоматическое отклонение без уведомления пользователя.
6. Чтобы назначить политику конфигурации приложения, выберите "Политика конфигурации приложения" > **Назначение** > **Выбрать группы**. Выберите группы пользователей для назначения > **Выбрать**.
7. Нажмите **Сохранить**, чтобы назначить политику.

## <a name="additional-information"></a>Дополнительные сведения

- [Назначение управляемых приложений Google Play для устройств Android Enterprise](apps-add-android-for-work.md#assigning-a-managed-google-play-app-to-android-enterprise-work-profile-devices)
- [Развертывание параметров конфигурации приложения Outlook для iOS, iPadOS и Android](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune)

## <a name="next-steps"></a>Дальнейшие шаги

Продолжайте [назначать](apps-deploy.md) и [отслеживать](apps-monitor.md) приложение как обычно.
