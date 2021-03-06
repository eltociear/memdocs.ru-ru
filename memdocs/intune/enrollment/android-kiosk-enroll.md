---
title: Настройка регистрации в Intune для выделенных устройств с Android для бизнеса
titleSuffix: Microsoft Intune
description: Узнайте, как зарегистрировать выделенные устройства с Android для бизнеса в Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 1/15/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 544db0c11894967eca71a5b8c2e107e0fab47ef5
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989004"
---
# <a name="set-up-intune-enrollment-of-android-enterprise-dedicated-devices"></a>Настройка регистрации в Intune выделенных устройств с Android для бизнеса

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Android для бизнеса поддерживает корпоративные однофункциональные устройства за счет набора решений для выделенных устройств. Такие устройства используются для одной цели, например для цифровой подписи, печати билетов, управления запасами и т. д. Администраторы ограничивают работу устройства, разрешая использовать ограниченный набор приложений и веб-ссылок. Пользователи не могут добавлять другие приложения или выполнять другие операции на устройстве.

Intune помогает развертывать приложения и параметры на выделенных устройствах с Android для бизнеса. Дополнительные сведения об Android для бизнеса см. в статье [Android's enterprise requirements](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012) (Требования Android для бизнеса).

Устройства, которыми вы управляете таким образом, регистрируются в Intune без учетной записи пользователя и не привязаны к конечному пользователю. Они не предназначены для персональных приложений или приложений, где требуются данные конкретного пользователя, например Outlook или Gmail.

## <a name="device-requirements"></a>Требования к устройствам

Устройства должны удовлетворять следующим требованиям, чтобы ими можно было управлять как корпоративными выделенными устройствами с Android:

- ОС Android версии 6.0 и более поздних.
- Устройства должны иметь версию Android с подключением к Google Mobile Services (GMS). Устройства должны иметь доступ к GMS и возможность подключиться к GMS.

## <a name="set-up-android-enterprise-dedicated-device-management"></a>Настройка управления выделенными устройствами с Android для бизнеса

Чтобы настроить управление выделенными устройствами с Android для бизнеса, сделайте следующее:

1. Чтобы подготовиться к управлению мобильными устройствами, нужно [установить **Microsoft Intune** в качестве службы управления мобильными устройствами (MDM)](../fundamentals/mdm-authority-set.md) для получения инструкций. Этот параметр указывается только один раз при первой настройке Intune для управления мобильными устройствами.
2. [Подключите учетную запись клиента Intune к учетной записи управляемого Google Play](connect-intune-android-enterprise.md).
3. [Создание профиля регистрации.](#create-an-enrollment-profile)
4. [Создание группы устройств](#create-a-device-group).
5. [Регистрация выделенных устройств](#enroll-the-dedicated-devices).

### <a name="create-an-enrollment-profile"></a>Создание профиля регистрации

> [!NOTE]
> Если срок действия маркера истек, связанный с ним профиль не будет отображаться в разделе **Регистрация устройства** > **Регистрация Android** > **Выделенные корпоративные устройства**. Чтобы просмотреть все профили, связанные с активными и неактивными маркерами, щелкните **Фильтр** и установите флажки для состояний политики "Активно" и "Не активно". 

Необходимо создать профиль регистрации, чтобы зарегистрировать выделенные устройства. При создании профиля вы получаете токен регистрации (случайная строка) и QR-код. В зависимости от версии Android и устройства вы можете использовать токен или QR-код для [регистрации выделенного устройства](#enroll-the-dedicated-devices).

1. Войдите в [Центр администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) и выберите **Устройства** > **Android** > **Регистрация Android** > **Выделенные корпоративные устройства**.
2. Выберите **Создать** и заполните обязательные поля.
    - **Имя**. Введите имя, которое будет использоваться при назначении профиля динамической группе устройств.
    - **Срок действия токена**. Дата, когда истекает срок действия токена. По требованию Google этот период составляет не более 90 дней.
3. Выберите **Создать**, чтобы сохранить профиль.

### <a name="create-a-device-group"></a>Создание группы устройств

Вы можете выбирать приложения и политики для назначенных или динамических групп устройств. Вы можете настроить динамические группы устройств AAD на автоматическое добавление устройств, зарегистрированных с определенным профилем регистрации, выполнив следующие действия:

1. Войдите в [Центр администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) и выберите **Группы** > **Все группы** > **Новая группа**.
2. В колонке **Группа** заполните обязательные поля следующим образом:
    - **Тип группы**: безопасность
    - **Имя группы**: введите интуитивно понятное имя (например, "Устройства фабрики 1")
    - **Тип членства**: динамическое устройство
3. Выберите **Добавить динамический запрос**.
4. В колонке **Правила динамического членства** заполните поля следующим образом:
    - **Добавить правило динамического членства**: простое правило
    - **Место добавления устройств**: enrollmentProfileName
    - В среднем поле выберите **Равно**.
    - В последнем поле введите имя профиля регистрации, который был создан ранее.
    Дополнительные сведения о правилах динамического членства см. в статье [Правила динамического членства в группах для Azure Active Directory](https://docs.microsoft.com/azure/active-directory/users-groups-roles/groups-dynamic-membership). 
5. Выберите **Добавить запрос** > **Создать**.

### <a name="replace-or-remove-tokens"></a>Замена или удаление токенов

- **Заменить токен**. Вы можете создать новый токен или QR-код, когда срок действия почти истек, с помощью опции "Заменить токен".
- **Отменить токен**. Вы можете незамедлительно прекратить действие токена или QR-кода. С этого момента токен или QR-код будут недействительны. Эту опцию можно использовать, если вы:
  - случайно предоставили токен или QR-код постороннему лицу;
  - завершили все регистрации и вам не нужен токен или QR код.

Замена или отмена токена или QR-кода не повлияет на уже зарегистрированные устройства.

1. Войдите в [Центр администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) и выберите **Устройства** > **Android** > **Регистрация Android** > **Выделенные корпоративные устройства**.
2. Выберите нужный профиль.
3. Выберите **Токен**.
4. Чтобы заменить токен, нажмите **Заменить токен**.
5. Чтобы отменить токен, нажмите **Отменить токен**.

## <a name="enroll-the-dedicated-devices"></a>Регистрация выделенных устройств

Теперь вы можете [зарегистрировать выделенные устройства](android-dedicated-devices-fully-managed-enroll.md).

> [!NOTE]
> Приложение **Microsoft Intune** автоматически установится во время регистрации выделенного устройства.  Это приложение является обязательным для регистрации. Его нельзя удалить. 

## <a name="managing-apps-on-android-enterprise-dedicated-devices"></a>Управление приложениями на выделенных устройствах с Android для бизнеса

На выделенных устройствах с Android для бизнеса можно устанавливать только приложения с типом назначения [Обязательно](../apps/apps-deploy.md#assign-an-app). Приложения устанавливаются из управляемого Google Play Маркета так же, как на устройствах с рабочим профилем Android для бизнеса.

Приложения обновляются автоматически на управляемых устройствах, когда разработчик приложения публикует обновление в Google Play.

Чтобы удалить приложение с выделенного устройства с Android для бизнеса, выполните одно из следующих действий:
- Удалите развертывание обязательного приложения.
- Создайте развертывание удаления для приложения.

## <a name="next-steps"></a>Дальнейшие действия
- [Развертывание приложений Android](../apps/apps-deploy.md)
- [Добавление политик конфигурации Android](../configuration/device-profiles.md)
