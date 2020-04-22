---
title: Использование параметров VPN для устройств Android в Microsoft Intune в Azure | Документация Майкрософт
description: 'Просмотрите все параметры для создания VPN-подключений на устройствах Android в Microsoft Intune. Введите имя подключения, IP-адрес или полное доменное имя VPN-сервера, выберите способ проверки подлинности пользователей и выберите один из типов подключения: Citrix, SonicWall, Check Point Capsule или Pulse Secure.'
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/19/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8b43b9671767a2d67bb98db6150799d266fe9fa6
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "80086563"
---
# <a name="android-device-settings-to-configure-vpn-in-intune"></a>Параметры устройства Android для настройки VPN в Intune

В этой статье перечислены и описаны различные параметры VPN-подключения, которыми можно управлять на устройствах Android. В рамках решения по управлению мобильными устройствами (MDM) используйте эти параметры для создания VPN-подключения, выбора способа проверки подлинности VPN, выбора типа VPN-сервера и т. д.

Администратор Intune может создавать и назначать параметры VPN устройствам Android. 

Дополнительные сведения о профилях VPN в Intune см. в [этой статье](vpn-settings-configure.md).

## <a name="before-you-begin"></a>Подготовка к работе

[Создайте профиль конфигурации устройства](vpn-settings-configure.md) и выберите **Android (администратор устройств)** .

## <a name="base-vpn"></a>Базовые настройки VPN

- **Имя подключения**. Введите имя подключения. Конечные пользователи увидят это имя при поиске устройства в списке доступных VPN-подключений. Например, введите `Contoso VPN`.
- **IP-адрес или полное доменное имя**. Укажите IP-адрес или полное доменное имя VPN-сервера, к которому подключаются устройства. Например, введите **192.168.1.1** или **vpn.contoso.com**.

  - **Метод проверки подлинности**. Укажите, как устройства будут проходить проверку подлинности на VPN-сервере. Доступны следующие параметры:

    - **Сертификаты**. Выберите существующий профиль сертификата SCEP или PKCS для проверки подлинности подключения. В разделе [Настройка сертификатов](../protect/certificates-configure.md) перечислены шаги для создания профиля сертификата.
    - **Имя пользователя и пароль**. При входе на VPN-сервер пользователям будет предложено ввести имя пользователя и пароль.

- **Тип подключения**. Выберите тип подключения VPN. Доступны следующие параметры:

  - **Check Point Capsule VPN**;
  - **Cisco AnyConnect**
  - **SonicWall Mobile Connect**;
  - **F5 Access**
  - **Pulse Secure**
  - **Citrix SSO**

- **Отпечаток** (только Check Point Capsule VPN). Укажите строку (например, **Contoso Fingerprint Code**), которая будет использоваться для проверки надежности VPN-сервера. Клиенту отправляется отпечаток пальца, чтобы клиент мог доверять любому серверу, имеющему такой же отпечаток. Если на устройстве еще нет отпечатка, пользователь получит запрос на подтверждение доверия к VPN-серверу с отображением отпечатка. Пользователь должен вручную проверить отпечаток и нажать кнопку "Доверять" для подключения.
- **Введите пары "ключ-значение" для атрибутов Citrix VPN** (только Citrix): введите пары "ключ-значение", предоставленные Citrix. Эти значения настраивают свойства VPN-подключения. 

  Можно также **импортировать** файл с разделителями-запятыми (CSV), содержащий пары ключей и значений. Проверьте, заданы ли свойства **Мои данные имеют заголовки** и **Ключ**.

  После добавления пар ключей и значений используйте функцию **Экспорт** для резервного копирования данных в CSV-файл.

## <a name="next-steps"></a>Дальнейшие действия

[Назначьте профиль](device-profile-assign.md) и [отслеживайте его состояние](device-profile-monitor.md).

Вы также можете создать профили VPN для устройств [Android Enterprise](vpn-settings-android-enterprise.md), [iOS и iPadOS](vpn-settings-ios.md), [macOS](vpn-settings-macos.md), [Windows 10 и более поздних версий](vpn-settings-windows-10.md), [Windows 8.1](vpn-settings-windows-8-1.md) и [Windows Phone 8.1](vpn-settings-windows-phone-8-1.md).
