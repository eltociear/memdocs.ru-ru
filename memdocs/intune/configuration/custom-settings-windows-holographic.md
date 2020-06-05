---
title: Пользовательские параметры Microsoft Intune для устройств Windows Holographic for Business | Документация Майкрософт
description: Добавьте или создайте настраиваемый профиль для использования параметров OMA-URI для устройств под управлением Windows Holographic for Business в Microsoft Intune, включая Microsoft Hololens. Можно задать параметры AllowFastReconnect, AllowVPN, AllowUpdateService, UpdateServiceURL, RequireUpdatesApproval, ApprovedUpdates и ApplicationLaunchRestrictions политики поставщика CSP.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.article: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.topic: reference
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: f37550bcfd8105b9cf5ea51c1bfa0d9305721348
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990075"
---
# <a name="use-custom-settings-for-windows-holographic-for-business-devices-in-intune"></a>Использование настраиваемых параметров для устройств Windows Holographic for Business в Intune

Microsoft Intune позволяет добавить или создать настраиваемые параметры для ваших устройств Windows Holographic for Business с помощью настраиваемых профилей. Настраиваемые профили являются компонентом Intune. Они предназначены для добавления параметров и функций устройств, которые не встроены в Intune.

В настраиваемых профилях Windows Holographic for Business используются параметры OMA-URI для настройки различных функций. Эти параметры обычно используются производителями мобильного устройства для управления функциями на устройстве.

Windows Holographic for Business открывает доступ ко множеству параметров поставщиков служб конфигурации (CSP). Обзор CSP см. в разделе [Введение в поставщики служб конфигурации (CSP) для ИТ-специалистов](https://technet.microsoft.com/itpro/windows/manage/how-it-pros-can-use-configuration-service-providers). Также см. [Поставщики служб конфигурации, поддерживаемые в Windows Holographic](https://docs.microsoft.com/windows/client-management/mdm/configuration-service-provider-reference#hololens).

Если вам нужен какой-то конкретный параметр, не забывайте, что [профиль ограничения устройств Windows Holographic for Business](device-restrictions-windows-holographic.md) содержит множество встроенных параметров. Поэтому вам может не потребоваться указывать настраиваемые значения.

Эта статья описывает создание настраиваемого профиля для устройств Windows Holographic for Business. Она также содержит список рекомендуемых параметров OMA-URI.

## <a name="before-you-begin"></a>Подготовка к работе

[Создайте настраиваемый профиль Windows 10](custom-settings-configure.md#create-the-profile).

## <a name="custom-oma-uri-settings"></a>Настраиваемые параметры OMA-URI

**Добавить**. Введите следующие параметры:

- **Имя** — Введите уникальное имя для параметра OMA-URI, чтобы его было проще найти в списке параметров.
- **Описание**. введите описание с общими сведениями о параметре и другой важной информацией.
- **OMA-URI** (с учетом регистра): введите код OMA-URI, для которого нужно указать параметр.
- **Тип данных**. Выберите тип данных для этого параметра OMA-URI. Доступны следующие параметры:

  - Строка
  - Строка (XML-файл)
  - Дата и время
  - Целое число
  - Число с плавающей запятой
  - Логическое значение
  - Base64 (файл)

- **Значение**: введите значение данных, которое нужно сопоставить с указанным OMA-URI. Значение зависит от выбранного типа данных. Например, если вы выбрали **Дата и время**, выберите значение из управляющего элемента выбора даты.

После добавления нескольких параметров можно выбрать **Экспорт**. Элемент **Экспорт** создает список всех добавленных значений в файле с разделителями-запятыми (CSV).

## <a name="recommended-custom-settings"></a>Рекомендованные пользовательские параметры

Следующие параметры также применимы к устройствам с Windows Holographic for Business.

### <a name="allowfastreconnect"></a>[AllowFastReconnect](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-authentication#authentication-allowfastreconnect)

> [!div class="mx-tableFixed"]
> |OMA-URI|Тип данных|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Authentication/AllowFastReconnect|Целое число<br/>0 — запрещено<br/>1 — разрешено (по умолчанию)|

### <a name="allowupdateservice"></a>[AllowUpdateService](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-allowupdateservice)

> [!div class="mx-tableFixed"]
> |OMA-URI|Тип данных|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Update/AllowUpdateService|Целое число<br/>0 — обновление службы запрещено <br/>1 — обновление службы разрешено (по умолчанию).|

### <a name="allowvpn"></a>[AllowVPN](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-settings#settings-allowvpn)

> [!div class="mx-tableFixed"]
> |OMA-URI|Тип данных|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Settings/AllowVPN|Целое число<br/>0 — запрещено<br/>1 — разрешено (по умолчанию)|

### <a name="requireupdateapproval"></a>[RequireUpdateApproval](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-requireupdateapproval)

> [!div class="mx-tableFixed"]
> |OMA-URI|Тип данных|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Update/RequireUpdateApproval|Этот параметр доступен в RS5 (сборка 17763) и более ранних версий. Начиная с 19H1 (сборка 18362), используйте [Центр обновления Windows для бизнеса](../protect/windows-update-for-business-configure.md).<br/><br/>Целое число<br/>0 — не настроено. Устройство устанавливает все доступные обновления.<br/>1 — устройство устанавливает только обновления, которые применимы и при этом находятся в списке разрешенных обновлений. Установите значение 1 для этой политики, если отдел ИТ хочет контролировать развертывание обновлений на устройствах, например, когда требуется предварительное тестирование.|

### <a name="scheduledinstalltime"></a>[ScheduledInstallTime](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-scheduledinstalltime)

> [!div class="mx-tableFixed"]
> |OMA-URI|Тип данных|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Update/ScheduledInstallTime|Целое число от 0 до 23, где 0 соответствует 00:00, а 23 — 23:00<br/>Значение по умолчанию — 3.|

### <a name="updateserviceurl"></a>[UpdateServiceURL](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-updateserviceurl)

> [!div class="mx-tableFixed"]
> |OMA-URI|Тип данных|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Update/UpdateServiceUrl|Этот параметр доступен в RS5 (сборка 17763) и более ранних версий. Начиная с 19H1 (сборка 18362), используйте [Центр обновления Windows для бизнеса](../protect/windows-update-for-business-configure.md).<br/><br/>Строка<br/>URL-адрес — устройство будет проверять наличие обновлений на сервере WSUS по указанному URL-адресу.<br/>Не настроено — устройство будет проверять наличие обновлений в центре обновления Майкрософт.|

### <a name="approvedupdates"></a>[ApprovedUpdates](https://docs.microsoft.com/windows/client-management/mdm/update-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|Тип данных|
> |---|---|
> |./Vendor/MSFT/Update/ApprovedUpdates/*GUID*<br/><br/>**Важно**<br/>Необходимо прочитать и принять лицензионные соглашения обновлений от имени конечных пользователей. Несоблюдение этого правила является нарушением юридических или договорных обязательств.|Узел для утверждения обновлений и принятия лицензионного соглашения от имени конечного пользователя.<br/><br/>Дополнительные сведения см. в статье [Update CSP](https://docs.microsoft.com/windows/client-management/mdm/update-csp) (Обновление поставщика службы шифрования).|

### <a name="applicationlaunchrestrictions"></a>[ApplicationLaunchRestrictions](https://docs.microsoft.com/windows/client-management/mdm/applocker-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|Тип данных|
> |----|---|
> |./Vendor/MSFT/AppLocker/ApplicationLaunchRestrictions/*Grouping*/*ApplicationType*/Policy<br/><br/>**Важно**<br/>В статье о поставщике служб конфигурации AppLocker содержатся примеры с экранированным языком XML. Для настройки этих параметров в пользовательских профилях Intune необходимо использовать обычный XML.|Строка<br/>Дополнительные сведения см. в статье [AppLocker CSP](https://docs.microsoft.com/windows/client-management/mdm/applocker-csp) (Поставщик служб конфигурации AppLocker).|

### <a name="deletionpolicy"></a>[DeletionPolicy](https://docs.microsoft.com/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|Тип данных|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/DeletionPolicy|Целое число<br/>0 — удалить немедленно, когда устройство возвращается в состояние без активных пользователей<br/>1 — удалить при достижении порога емкости хранилища (по умолчанию)<br/>2 — удалить при достижении порога емкости хранилища и порога бездействия профиля|

### <a name="enableprofilemanager"></a>[EnableProfileManager](https://docs.microsoft.com/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|Тип данных|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/EnableProfileManager|Логическое значение<br/>True — включить<br/>False — отключить (по умолчанию)|

### <a name="profileinactivitythreshold"></a>[ProfileInactivityThreshold](https://docs.microsoft.com/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|Тип данных|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/ProfileInactivityThreshold|Целое число<br/>Значение по умолчанию — 30.|

### <a name="storagecapacitystartdeletion"></a>[StorageCapacityStartDeletion](https://docs.microsoft.com/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|Тип данных|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/StorageCapacityStartDeletion|Целое число<br/>Значение по умолчанию — 25.|

### <a name="storagecapacitystopdeletion"></a>[StorageCapacityStopDeletion](https://docs.microsoft.com/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|Тип данных|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/StorageCapacityStopDeletion|Целое число<br/>Значение по умолчанию — 50.|

## <a name="find-the-policies-you-can-configure"></a>Поиск настраиваемых политик

Полный список поставщиков служб конфигурации (CSP), поддерживаемых Windows Holographic, приведен в разделе [Поставщики служб конфигурации, поддерживаемые в Windows Holographic](https://docs.microsoft.com/windows/client-management/mdm/configuration-service-provider-reference#hololens). Некоторые параметры не совместимы с некоторыми версиями Windows Holographic. В таблице в [CSP, поддерживаемые в Windows Holographic](https://docs.microsoft.com/windows/client-management/mdm/configuration-service-provider-reference#hololens) перечислены поддерживаемые версии для каждого поставщика служб конфигурации.

Кроме того, Intune поддерживает не все параметры, указанные в [этой таблице](https://docs.microsoft.com/windows/client-management/mdm/configuration-service-provider-reference#hololens). Чтобы узнать, поддерживает ли Intune необходимый параметр, откройте соответствующую статью для этого параметра. На странице каждого параметра отображаются сведения о поддерживаемой операции. Для работы с Intune параметр должен поддерживать операции **добавления** или **замены**.

## <a name="next-steps"></a>Дальнейшие шаги

[Назначение профиля](device-profile-assign.md) и [отслеживание его состояния](device-profile-monitor.md).

Создайте [настраиваемый профиль на устройствах с Windows 10](custom-settings-windows-10.md).

Узнайте больше о [настраиваемых профилях](custom-settings-configure.md) в Intune.
