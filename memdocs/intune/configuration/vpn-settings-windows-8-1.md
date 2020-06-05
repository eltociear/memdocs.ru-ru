---
title: Настройка параметров VPN для устройств с Windows 8.1 в Microsoft Intune — Azure | Документация Майкрософт
description: В Microsoft Intune на устройствах под управлением Windows 8.1 добавьте или создайте профиль конфигурации виртуальной частной сети (VPN) с помощью параметров конфигурации, включая сведения о подключении, и параметров прокси-сервера, чтобы включить IP-адреса или полное доменное имя, а также TCP-порт.
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
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f0f242f336fadf9dd31641849462a5dd24c09e3f
ms.sourcegitcommit: 169e279ba686c28d9a23bc0a54f0a2a0d20bdee4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2020
ms.locfileid: "83556359"
---
# <a name="add-vpn-settings-on-windows-81-devices-in-microsoft-intune"></a>Добавление параметров VPN для устройств с ОС Windows 8.1 в Microsoft Intune

Сведения о параметрах Intune, используемых для настройки VPN-подключений на устройствах Windows 8.1.

В зависимости от выбранных параметров не все приведенные в следующем списке значения будут доступны для настройки.

## <a name="before-you-begin"></a>Подготовка к работе

[Создайте профиль конфигурации устройства VPN Windows 8.1](vpn-settings-configure.md).

## <a name="base-vpn-settings"></a>Основные параметры VPN

- **Имя подключения**. Введите имя подключения. Пользователи видят это имя при поиске устройства в списке доступных VPN-подключений. Например, введите `Contoso VPN`.
- **Серверы**: Добавьте VPN-серверы, к которым подключаются устройства. Добавляя новый сервер, вы вводите следующие сведения:
  - **Описание**. Укажите описательное имя сервера, например **VPN-сервер Contoso**.
  - **IP-адрес или полное доменное имя**. Укажите IP-адрес или полное доменное имя VPN-сервера, к которому подключаются устройства. Например, введите `192.168.1.1` или `vpn.contoso.com`.
  - **Сервер по умолчанию**. Значение **True** устанавливает данный сервер как сервер по умолчанию, который устройства используют для подключения. Установите только один сервер в качестве сервера по умолчанию.
  - **Импорт**. Укажите файл с разделителями-запятыми, который содержит список серверов в следующем формате: описание, IP-адрес или полное доменное имя, сервер по умолчанию. Щелкните **ОК**, чтобы импортировать эти серверы в список **Серверы**.
  - **Экспортировать**. Экспортирует список серверов в файл данных с разделителями-запятыми (CSV-файл).

- **Тип подключения**. Выберите тип VPN-подключения. Доступны следующие параметры:
  - **Check Point Capsule VPN**;
  - **SonicWall Mobile Connect**;
  - **F5 Edge Client**
  - **Pulse Secure**

<!--- **Fingerprint** (Check Point Capsule VPN only): Specify a string (for example, "Contoso Fingerprint Code") that will be used to verify that the VPN server can be trusted. A fingerprint can be sent to the client so it knows to trust any server that presents the same fingerprint when connecting. If the device doesn't already have the fingerprint, it will prompt the user to trust the VPN server that they are connecting to while showing the fingerprint. (The user manually verifies the fingerprint and chooses **trust** to connect.) --->

- **Группа входа или домен (только для SonicWall Mobile Connect)** . Введите имя группы входа или домена, к которому следует подключиться.

- **Роль** (только Pulse Secure). Введите имя роли пользователя, имеющей доступ к этому подключению. Роль пользователя определяет личные настройки и параметры, а также включает или отключает определенные функции доступа.

- **Область (только Pulse Secure)** . Введите имя области проверки подлинности, которую следует использовать. Область аутентификации — это группа ресурсов аутентификации, которая используется типом подключения Pulse Secure.

- **Настраиваемый XML**. Укажите пользовательские команды XML, настраивающие VPN-подключение.

  **Пример для Pulse Secure**.

  ```xml
  <pulse-schema><isSingleSignOnCredential>true</isSingleSignOnCredential></pulse-schema>
  ```

  **Пример для CheckPoint Mobile VPN**.

  ```xml
  <CheckPointVPN port="443" name="CheckPointSelfhost" sso="true" debug="3" />
  ```

  **Пример для SonicWall Mobile Connect**.

  ```xml
  <MobileConnect><Compression>false</Compression><debugLogging>True</debugLogging><packetCapture>False</packetCapture></MobileConnect>
  ```

  **Пример для F5 Edge Client**.

  ```xml
  <f5-vpn-conf><single-sign-on-credential /></f5-vpn-conf>
  ```

  Дополнительные сведения о написании пользовательских команд XML см. в документации по VPN каждого производителя.

- **Раздельное туннелирование**. Выберите значение **Включить**, чтобы разрешить устройствам выбирать нужное подключение в зависимости от трафика. Например, пользователь в отеле использует VPN-подключение для доступа к рабочим файлам, а стандартную сеть отеля — для обычного просмотра веб-страниц. Если требуется, чтобы весь трафик использовал VPN-туннель при активном VPN-подключении, выберите значение **Отключить**.

## <a name="proxy-settings"></a>Параметры прокси-сервера

- **Сценарий автоматической настройки**. Для настройки прокси-сервера будет использоваться файл. Введите **URL-адрес прокси-сервера**, содержащий файл конфигурации. Например, введите `http://proxy.contoso.com`.
- **Адрес**. Введите адрес прокси-сервера, например IP-адрес или `vpn.contoso.com`.
- **Номер порта**. Введите номер TCP-порта, используемого вашим прокси-сервером.
- **Автоматически определять параметры прокси-сервера**. Если вашему VPN-серверу требуется прокси-сервер для подключения, укажите, следует ли устройствам автоматически определять параметры подключения. Доступны следующие параметры:
  - **Не настроено** (по умолчанию). Intune не изменяет или не обновляет этот параметр.
  - **Включить**. Параметры подключения определяются автоматически.
  - **Отключить**: Параметры подключения не определяются автоматически.
- **Не использовать прокси-сервер для локальных адресов**. Выберите этот параметр, чтобы для локальных адресов выполнялся обход прокси-сервера. Доступны следующие параметры:
  - **Не настроено** (по умолчанию). Intune не изменяет или не обновляет этот параметр.
  - **Включить**. Не использовать прокси-сервер для локальных адресов.
  - **Отключить**: Использовать прокси-сервер для локальных адресов.

## <a name="next-steps"></a>Дальнейшие шаги

[Назначение профиля](device-profile-assign.md) и [отслеживание его состояния](device-profile-monitor.md).

Настройте параметры VPN на устройствах с [Android](vpn-settings-android.md), [Android Enterprise](vpn-settings-android-enterprise.md), [macOS](vpn-settings-macos.md) и [Windows 10](vpn-settings-windows-10.md).
