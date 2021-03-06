---
title: Настройка параметров киоска для Windows Holographic for Business в Microsoft Intune в Azure | Документация Майкрософт
description: Настройте устройства Windows Holographic for Business в качестве киосков с одним или несколькими приложениями, добавив приложения, отобразив панель задач, а также настроив меню "Пуск" и веб-браузер в Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3d54e02c7bb88354ec59a9a8ce780ff559377466
ms.sourcegitcommit: 169e279ba686c28d9a23bc0a54f0a2a0d20bdee4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2020
ms.locfileid: "83556104"
---
# <a name="windows-holographic-for-business-device-settings-to-run-as-a-kiosk-in-intune"></a>Настройка параметров устройств Windows Holographic for Business для запуска в качестве киоска в Intune

На устройствах Windows Holographic for Business можно настроить запуск в режиме киоска с одним или несколькими приложениями. Некоторые функции не поддерживаются в Windows Holographic for Business.

В этой статье перечислены и описаны различные параметры, которыми вы можете управлять на устройствах Windows Holographic for Business. В рамках решения в системе управления мобильными устройствами используйте эти параметры для управления устройствами Windows Holographic for Business в режиме киоска.

Администратор Intune может создавать и назначать эти параметры вашим устройствам.

См. дополнительные сведения о [настройке параметров киоска Windows в Intune](kiosk-settings.md).

## <a name="before-you-begin"></a>Подготовка к работе

- [Создайте профиль конфигурации устройства киоска Windows 10](kiosk-settings.md#create-the-profile).

  При создании профиля конфигурации устройства киоска Windows 10 используется больше параметров, чем указано в этой статье. Параметры, описанные в этой статье, поддерживаются на устройствах Windows Holographic for Business.

- Этот профиль киоска непосредственно связан с профилем ограничений устройства, который создается с помощью [параметров киоска Microsoft Edge](device-restrictions-windows-holographic.md#microsoft-edge-browser). Подведение итогов.

  1. Создайте профиль киоска для работы в полноэкранном режиме.
  2. Создайте [профиль ограничений устройства](device-restrictions-windows-holographic.md#microsoft-edge-browser) и настройте разрешенные параметры и функции в Microsoft Edge.

> [!IMPORTANT]
> Не забудьте назначить этот профиль киоска тем же устройствам, которым назначен ваш [профиль Microsoft Edge](device-restrictions-windows-holographic.md#microsoft-edge-browser).

## <a name="single-app-full-screen-kiosk"></a>Киоск с одним приложением в полноэкранном режиме

Выполняется только одно приложение на устройстве. Определенное приложение запускается при входе пользователя в систему. Этот режим также не позволяет открывать новые приложения или изменять выполняющиеся.

- **Тип входа пользователя**. Выберите тип учетной записи, которая запускает приложение. Доступны следующие параметры:

  - **Автоматический вход (Windows 10 версии 1803 и выше)** . Не поддерживается в Windows Holographic for Business.
  - **Учетная запись локального пользователя**. Введите данные локальной (для этого устройства) учетной записи. Или введите учетную запись Майкрософт (MSA), связанную с приложением киоска. Указанная здесь учетная запись используется для входа в киоск.

    Для киосков в общедоступных средах следует использовать тип пользователя с минимальными правами.

- **Тип приложения**. Выберите **Добавить приложение магазина**.

  - **Приложение для работы в режиме киоска**. Выберите приложение в списке.

    В списке нет ни одного приложения? Добавьте нужные, используя инструкции из статьи о [клиентских приложениях](../apps/apps-add.md).

## <a name="multi-app-kiosk"></a>Киоск с несколькими приложениями

В этом режиме приложения доступны через меню "Пуск". Пользователь может открывать только эти приложения. Если приложение имеет зависимость от другого приложения, оба должны быть включены в список разрешенных приложений.

- **Целевая Windows 10 на устройствах в режиме S**. Выберите **Нет**. Режим S не поддерживается в Windows Holographic for Business.

- **Тип входа пользователя**. Добавьте учетные записи пользователей, которые могут использовать добавляемые вами приложения. Доступны следующие параметры:

  - **Автоматический вход (Windows 10 версии 1803 и выше)** . Не поддерживается в Windows Holographic for Business.
  - **Учетные записи локальных пользователей**. **Добавьте** данные локальной (для этого устройства) учетной записи. Указанная здесь учетная запись используется для входа в киоск.
  - **Пользователь или группа Azure AD (Windows 10 версии 1803 и более поздние версии)** . Требуются учетные данные пользователя для входа в устройство. Выберите **Добавить**, чтобы выбрать в списке пользователей или группы Azure AD. Вы можете выбрать несколько пользователей и (или) групп. Нажмите кнопку **ОК**, чтобы сохранить изменения.
  - **Посетитель HoloLens**. Учетная запись посетителя является гостевой, и для нее не требуются какие-либо учетные данные пользователя или проверка подлинности, как описано в разделе [Суть режима общего ПК](https://docs.microsoft.com/windows/configuration/set-up-shared-or-guest-pc#shared-pc-mode-concepts).

- **Браузеры и приложения**. Добавьте приложения, которые будут выполняться на устройстве киоска. Как вы помните, здесь можно добавить несколько приложений.

  - **Браузеры**
    - **Добавить Microsoft Edge**: Microsoft Edge добавляется в сетку приложений, и на таком терминале могут выполняться любые приложения. Выберите тип режима киоска Microsoft Edge.

      - **Обычный режим (полная версия Microsoft Edge)** . Запускает полнофункциональную версию Microsoft Edge со всеми функциями просмотра. Пользовательские данные и состояние сохраняются между сеансами.
      - **Открытый просмотр (InPrivate)** : выполняется версия Microsoft Edge InPrivate с несколькими вкладками с использованием специального интерфейса для киосков, которые работают в полноэкранном режиме.

      Дополнительные сведения об этих параметрах см. в разделе [Развертывание полноэкранного режима Microsoft Edge](https://docs.microsoft.com/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy#supported-configuration-types).

      > [!NOTE]
      > Этот параметр включает браузер Microsoft Edge на устройстве. Чтобы настроить параметры, относящиеся к Microsoft Edge, создайте профиль ограничений устройства (**Устройства** > **Профили конфигурации** > **Создать профиль** > **Windows 10** в качестве платформы > **Ограничения устройств** > **Браузер Microsoft Edge**). В разделе [Браузер Microsoft Edge](device-restrictions-windows-holographic.md#microsoft-edge-browser) указаны и описаны доступные параметры Holographic for Business.

    - **Добавить браузер киоска**. Не поддерживается в Windows Holographic for Business.

  - **Приложения**
    - **Добавить приложение магазина**. Выберите существующее приложение, добавленное или развернутое в Intune в качестве [клиентского приложения](../apps/apps-add.md), включая бизнес-приложения. Если у вас нет приложений, Intune поддерживает многие [типы приложений](../apps/apps-add.md), которые можно [добавить в Intune](../apps/store-apps-windows.md).
    - **Добавить приложение Win32**. Не поддерживается в Windows Holographic for Business.
    - **Добавить по AUMID**. Этот вариант позволяет добавить стандартные приложения Windows, например Блокнот или Калькулятор. Укажите следующие свойства.

      - **Имя приложения**. Обязательно. Введите имя приложения.
      - **Идентификатор модели пользователя приложения (AUMID)** . Обязательно. Введите идентификатор пользовательской модели приложения (AUMID) для приложения Windows. Чтобы получить этот идентификатор, выполните инструкции из статьи [Find the Application User Model ID of an installed app](https://docs.microsoft.com/windows-hardware/customize/enterprise/find-the-application-user-model-id-of-an-installed-app) (Поиск идентификатора модели пользователя для установленного приложения).

    - **Автозапуск**. Необязательный параметр. После добавления приложений и браузера выберите одно приложение или браузер, которые будут открываться автоматически при входе пользователя в систему. В автозапуск можно добавить только одно приложение или браузер.
    - **Размер плитки**. Обязательно. После добавления приложений выберите размер плитки: маленькая, средняя, широкая или большая.

- **Использовать альтернативный макет меню "Пуск"** . Выберите **Да**, чтобы задать XML-файл, описывающий, как приложения отображаются в меню "Пуск", включая их очередность. Используйте этот параметр, если вам нужны определенные настройки меню "Пуск". [Настройка и экспорт макета начального экрана](https://docs.microsoft.com/hololens/hololens-kiosk#start-layout-for-hololens). Содержатся некоторые рекомендации и XML-файл для устройств Windows Holographic for Business.

- **Панель задач Windows**. Не поддерживается в Windows Holographic for Business.
- **Разрешить доступ к папке загрузок**: Не поддерживается в Windows Holographic for Business.
- **Укажите период обслуживания для перезапуска приложений**. Не поддерживается в Windows Holographic for Business.

## <a name="next-steps"></a>Дальнейшие шаги

[Назначьте профиль](device-profile-assign.md) и [отслеживайте его состояние](device-profile-monitor.md).

Вы также можете создать профили киоска для устройств [Android](device-restrictions-android.md#kiosk), [Android Enterprise](device-restrictions-android-for-work.md#dedicated-devices) и [Windows 10 (и более поздних версий)](kiosk-settings-windows.md).
