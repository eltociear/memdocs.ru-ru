---
title: Параметры устройства Windows Holographic for Business в Microsoft Intune в Azure | Документация Майкрософт
description: Изучите и настройте параметры ограничения для устройств с Windows Holographic for Business в Microsoft Intune. Управляйте отменой регистрации, геолокацией, паролями, установкой приложений из Магазина приложений, файлами cookie и всплывающими окнами в Microsoft Edge, Microsoft Defender, системой поиска, облаком и хранилищем, подключениями по Bluetooth, системным временем и данными об использовании.
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
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 301cdd9403b0bb3e2d64c8707782ecbc639dc044
ms.sourcegitcommit: 169e279ba686c28d9a23bc0a54f0a2a0d20bdee4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2020
ms.locfileid: "83556055"
---
# <a name="windows-holographic-for-business-device-settings-to-allow-or-restrict-features-using-intune"></a>Параметры устройства Windows Holographic for Business, разрешающие или ограничивающие функции с помощью Intune

В этой статье перечислены и описаны различные параметры, которыми вы можете управлять на устройствах Windows Holographic for Business, таких как Microsoft Hololens. Используйте эти параметры как часть решения управления мобильными устройствами (MDM), чтобы разрешать или отключать использование функций, управлять безопасностью и т. д.

Администратор Intune может создавать и назначать эти параметры вашим устройствам.

## <a name="before-you-begin"></a>Подготовка к работе

[Создайте профиль конфигурации ограничений на устройстве с Windows 10](device-restrictions-configure.md#create-the-profile).

При создании профиля конфигурации ограничений на устройстве с Windows 10 используется больше параметров, чем указано в этой статье. Параметры, описанные в этой статье, поддерживаются на устройствах Windows Holographic for Business.

## <a name="app-store"></a>Магазин App Store

- **Автообновление приложений из Магазина**. **Блокировать** — запрещает автоматически обновлять приложения, установленные из Microsoft Store. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить автоматически обновлять приложения, установленные из Microsoft Store.

  [ApplicationManagement/AllowAppStoreAutoUpdate CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowappstoreautoupdate)

- **Установка доверенного приложения**. Выберите, можно ли устанавливать приложения не из Microsoft Store (способ, также известный как загрузка неопубликованных приложений). В ходе загрузки неопубликованных приложений производится установка, запуск и тестирование приложения, не сертифицированного Microsoft Store. Например, приложение, которое является внутренним и нужно только для вашей компании. Доступны следующие параметры:
  - **Не настроено** (по умолчанию). Intune не изменяет или не обновляет этот параметр.
  - **Блокировать**: предотвращает загрузку неопубликованных приложений. Невозможно установить приложения не из Microsoft Store.
  - **Разрешить**: разрешает загрузку неопубликованных приложений. Можно устанавливать приложения не из Microsoft Store.

  [ApplicationManagement/AllowAllTrustedApps CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowalltrustedapps)

- **Разблокировка для разработчиков**. Разрешает использовать параметры разработчика Windows, например изменение пользователем неопубликованных приложений. Доступны следующие параметры:
  - **Не настроено** (по умолчанию). Intune не изменяет или не обновляет этот параметр.
  - **Блокировать**: предотвращает режим разработчика и загрузку неопубликованных приложений.
  - **Разрешить**: разрешает режим разработчика и загрузку неопубликованных приложений.

  [CSP ApplicationManagement/AllowDeveloperUnlock](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowdeveloperunlock)

## <a name="cellular-and-connectivity"></a>Сотовая сеть и подключение

- **Bluetooth**. Значение **Блокировать** запрещает пользователю включать Bluetooth. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить использовать Bluetooth на устройстве.

  [CSP Connectivity/AllowBluetooth](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-connectivity#connectivity-allowbluetooth)

- **Возможность обнаружения Bluetooth**. Значение **Блокировать** запрещает обнаружение устройства другими устройствами, поддерживающими Bluetooth. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить другим устройствам с поддержкой Bluetooth, например гарнитуре, обнаруживать устройство.

  [CSP Bluetooth/AllowDiscoverableMode](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowdiscoverablemode)

- **Реклама Bluetooth**. Значение **Блокировать** предотвращает отправку рекламы через Bluetooth с устройства. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить устройству отправлять рекламу через Bluetooth.

  [CSP Bluetooth/AllowAdvertising](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowadvertising)

## <a name="cloud-and-storage"></a>Облако и хранилище

- **Учетная запись Майкрософт**. Значение **Блокировать** запрещает пользователям связывание учетных записей Майкрософт с устройством. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить добавление и использование учетной записи Майкрософт.

  [CSP Accounts/AllowMicrosoftAccountConnection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-accounts#accounts-allowmicrosoftaccountconnection)

## <a name="control-panel-and-settings"></a>Панель управления и параметры

- **Изменение системного времени**. Значение **Блокировать** запрещает пользователям изменять на устройстве параметры даты и времени. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить пользователям изменять эти параметры.

  [CSP Settings/AllowDateTime](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-settings#settings-allowdatetime)

## <a name="general"></a>Общие

- **Регистрация вручную**. Значение **Блокировать** запрещает пользователям удалять рабочую учетную запись с помощью панели управления рабочей областью на устройстве. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр.

  [CSP Experience/AllowManualMDMUnenrollment](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowmanualmdmunenrollment)

- **Географическое положение**. Значение **Блокировать** запрещает пользователям включать на устройстве службы определения местоположения. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр.

  [CSP Experience/AllowFindMyDevice](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowfindmydevice)

- **Кортана**. Значение **Блокировать** отключает на устройстве голосовой помощник — Кортану. Если Cortana выключена, пользователи могут по-прежнему использовать поиск элементов на устройстве. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить использовать Кортану.

  [CSP Experience/AllowCortana](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowcortana)

## <a name="microsoft-edge-browser"></a>Браузер Microsoft Edge

- **Начало работы** > **Разрешить всплывающие окна**. Значение **Да** (по умолчанию) разрешает отображение всплывающих окон в веб-браузере. Значение **Нет** блокирует всплывающие окна в браузере.

  [CSP Browser/AllowPopups](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowpopups)

- **Избранное и поиск** > **Показать предложения поиска**. Значение **Да** (по умолчанию) разрешает поисковой системе предлагать сайты по мере ввода фраз в строке поиска. Если выбрать **Нет**, это будет запрещено.

  [CSP Browser/AllowSearchSuggestionsinAddressBar](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar)

- **Конфиденциальность и безопасность** > **Разрешить использовать диспетчер паролей**. Значение **Да** (по умолчанию) разрешает Microsoft Edge автоматически использовать диспетчер паролей, который позволяет пользователям управлять паролями на устройстве. **Нет** запрещает использовать диспетчер паролей Microsoft Edge.

  [CSP Browser/AllowPasswordManager](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager)

- **Конфиденциальность и безопасность** > **Файлы cookie**. Выберите режим применения файлов cookie в веб-браузере. Доступны следующие параметры:
  - **Разрешить**: Файлы cookie сохраняются на устройстве.
  - **Блокировать все файлы cookie**. Файлы cookie не сохраняются на устройстве.
  - **Блокировать только сторонние файлы cookie**. Файлы cookie сторонних производителей и партнеров не сохраняются на устройстве.

  [CSP Browser/AllowCookies](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowcookies)

- **Конфиденциальность и безопасность** > **Отправить заголовки do-not-track**. Значение **Да** требует, чтобы устройства отправляли заголовки Do Not Track на веб-сайты, запрашивающие сведения для отслеживания (рекомендуется). Значение **Нет** (по умолчанию) не отправляет заголовки, что позволяет веб-сайтам отслеживать пользователя. Пользователи могут настроить этот параметр.

  [CSP Browser/AllowDoNotTrack](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack)

## <a name="microsoft-defender-smartscreen"></a>Фильтр SmartScreen в Microsoft Defender

- **SmartScreen для Microsoft Edge**. **Требовать** — компонент SmartScreen в Microsoft Defender будет отключен и пользователи не смогут включить его. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может включить компонент SmartScreen и разрешить пользователям включать и отключать его.

  [CSP Browser/AllowSmartScreen](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)

## <a name="password"></a>Пароль

- **Пароль**. Если задано значение **Требовать**, пользователи должны вводить пароль для доступа к устройству. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить доступ к устройствам без ввода пароля. Применяется только к локальным учетным записям. Пароли учетных записей домена по-прежнему настраиваются Active Directory (AD) и Azure AD.

  [CSP DeviceLock/DevicePasswordEnabled](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-devicepasswordenabled)

- **Требовать пароль при выходе устройства из состояния простоя**. Если задано значение **Требовать**, пользователи должны вводить пароль для разблокировки устройства после простоя. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может не требовать ввода ПИН-кода или пароля после простоя.

  [CSP DeviceLock/AllowIdleReturnWithoutPassword](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-allowidlereturnwithoutpassword)

## <a name="reporting-and-telemetry"></a>Отчетность и телеметрия

- **Публикация данных об использовании**. Выберите уровень предоставляемых диагностических данных. Доступны следующие параметры:

  - **Не настроено** (по умолчанию). Intune не изменяет или не обновляет этот параметр. Принудительный параметр отсутствует. Пользователи выбирают уровень предоставляемых данных. По умолчанию ОС может не предоставлять общий доступ к данным.
  - **Безопасность**. Сведения, необходимые для обеспечения повышенной безопасности, включая данные о настройке компонентов интерфейса для подключенных пользователей и телеметрии, средства удаления вредоносных программ и Microsoft Defender в Windows.
  - **Основные**. Основные сведения об устройстве, включая связанные с качеством данные, совместимость приложений, данные об использовании приложений и данные с уровня безопасности.
  - **Расширенные**. Дополнительные сведения, в том числе использование Windows, Windows Server, System Center и приложений, то, как они работают, расширенные данные о надежности, а также данные с основного уровня и уровня безопасности.
  - **Полные**. Все данные, необходимые для выявления и устранения проблем, а также данные с уровня безопасности, базового и расширенного уровней.

  [CSP System/AllowTelemetry](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-system#system-allowtelemetry)

## <a name="search"></a>Система поиска

- **Поиск местоположения**. Значение **Блокировать** запрещает службе Windows Search использовать местоположение. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить эту функцию.

  [CSP Search/AllowSearchToUseLocation](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-search#search-allowsearchtouselocation)

## <a name="next-steps"></a>Дальнейшие шаги

[Назначение профиля](device-profile-assign.md) и [отслеживание его состояния](device-profile-monitor.md).
