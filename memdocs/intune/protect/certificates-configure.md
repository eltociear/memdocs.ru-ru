---
title: Создание профилей сертификатов в Microsoft Intune — Azure | Документы Майкрософт
description: Дополнительные сведения об использовании сертификатов и профилей сертификатов SCEP и PKCS с Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/21/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 5eccfa11-52ab-49eb-afef-a185b4dccde1
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4441fdaf8c3fb8bfb6613805df9eca27cc3ebf0c
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990380"
---
# <a name="use-certificates-for-authentication-in-microsoft-intune"></a>Использование сертификатов для проверки подлинности в Microsoft Intune

Используйте сертификаты с Intune для проверки подлинности пользователей в приложениях и корпоративных ресурсах через профили VPN, Wi-Fi или электронной почты. Если для проверки подлинности подключений используются сертификаты, конечным пользователям не нужно вводить имена пользователей и пароли, что позволяет сделать доступ прозрачным. Сертификаты также используются для подписывания и шифрования электронной почты с помощью S/MIME.

## <a name="intune-supported-certificates-and-usage"></a>Поддерживаемые сертификаты и использование Intune

| Type              | Проверка подлинности | Подписывание S/MIME | Шифрование S/MIME  |
|--|--|--|--|
| Импортированный сертификат PKCS |  | ![Поддерживается](./media/certificates-configure/green-check.png) | ![Поддерживается](./media/certificates-configure/green-check.png)|
| PKCS #12 (или PFX)    | ![Поддерживается](./media/certificates-configure/green-check.png) | ![Поддерживается](./media/certificates-configure/green-check.png) |  |
| Протокол SCEP  | ![Поддерживается](./media/certificates-configure/green-check.png) | ![Поддерживается](./media/certificates-configure/green-check.png) | |

Чтобы развернуть эти сертификаты, создайте и назначьте профили сертификатов для устройств.

Каждый отдельный профиль сертификата, созданный вами, поддерживает одну платформу. Например, если вы используете сертификаты PKCS, вы создадите профиль сертификата PKCS для Android и отдельный профиль сертификата PKCS для iOS/iPadOS. Если вы также используете сертификаты SCEP для этих двух платформ, вы создадите профиль сертификата SCEP для Android, а другой — для iOS/iPadOS.

### <a name="general-considerations-when-you-use-a-microsoft-certification-authority"></a>Общие рекомендации, которые следует учитывать при использовании центра сертификации Майкрософт

При использовании центра сертификации (ЦС) Майкрософт:

- Чтобы использовать профили сертификатов SCEP, необходимо [настроить сервер службы регистрации сертификатов для сетевых устройств (NDES)](certificates-scep-configure.md#set-up-ndes) для Intune.
- Чтобы использовать следующие типы профилей сертификатов, необходимо [установить соединитель сертификатов Microsoft Intune](certificates-scep-configure.md#install-the-intune-certificate-connector):
  - профиль сертификата SCEP;
  - Профиль сертификата PKCS

- Чтобы использовать импортированные сертификаты PKCS, сделайте следующее:
  - [Установите соединитель сертификатов PFX для Microsoft Intune](certificates-imported-pfx-configure.md#download-install-and-configure-the-pfx-certificate-connector-for-microsoft-intune).
  - Экспортируйте сертификаты из центра сертификации, а затем импортируйте их в Microsoft Intune. См. [проект PFXImport PowerShell](https://github.com/Microsoft/Intune-Resource-Access/tree/develop/src/PFXImportPowershell).

- Разверните сертификаты с помощью следующих механизмов:
  - [профили доверенных сертификатов](certificates-configure.md#create-trusted-certificate-profiles) для развертывания доверенного корневого сертификата ЦС из корневого или промежуточного (выдающего) ЦС на устройствах;
  - Профили сертификатов SCEP
  - Профили сертификатов PKCS
  - профили импортированных сертификатов PKCS.

### <a name="general-considerations-when-you-use-a-third-party-certification-authority"></a>Общие рекомендации, которые следует учитывать при использовании стороннего центра сертификации

При использовании стороннего центра сертификации (не Майкрософт):

- Чтобы использовать профили сертификатов SCEP, сделайте следующее:
  - Настройте интеграцию со сторонним ЦС от [одного из наших поддерживаемых партнеров](certificate-authority-add-scep-overview.md#third-party-certification-authority-partners). Для настройки необходимо выполнить инструкции из стороннего центра сертификации, чтобы интегрировать его с Intune.
  - [Создайте приложение в Azure AD](certificate-authority-add-scep-overview.md#set-up-third-party-ca-integration), которое делегирует Intune права для проверки запроса на сертификат SCEP.

- Для использования импортированных сертификатов PKCS требуется [установить соединитель сертификатов PFX для Microsoft Intune](certificates-imported-pfx-configure.md#download-install-and-configure-the-pfx-certificate-connector-for-microsoft-intune).

- Разверните сертификаты с помощью следующих механизмов:
  - [профили доверенных сертификатов](certificates-configure.md#create-trusted-certificate-profiles) для развертывания доверенного корневого сертификата ЦС из корневого или промежуточного (выдающего) ЦС на устройствах;
  - Профили сертификатов SCEP
  - профили сертификатов PKCS *(поддерживаются только [платформой Digicert PKI](certificates-digicert-configure.md))* ;
  - профили импортированных сертификатов PKCS.

## <a name="supported-platforms-and-certificate-profiles"></a>Поддерживаемые платформы и профили сертификатов

| Платформа              | Профиль доверенного сертификата | Профиль сертификата PKCS | Профиль сертификата SCEP | Профиль импортированного сертификата PKCS  |
|--|--|--|--|---|
| Администратор устройства с Android | ![Поддерживается](./media/certificates-configure/green-check.png) | ![Поддерживается](./media/certificates-configure/green-check.png) | ![Поддерживается](./media/certificates-configure/green-check.png)|  ![Поддерживается](./media/certificates-configure/green-check.png) |
| Android для бизнеса <br> Полностью управляемые устройства (владелец устройства)   | ![Поддерживается](./media/certificates-configure/green-check.png) |   | ![Поддерживается](./media/certificates-configure/green-check.png) |   |
| Android для бизнеса <br> Выделенное устройство (владелец устройства)   | ![Поддерживается](./media/certificates-configure/green-check.png)  |   | ![Поддерживается](./media/certificates-configure/green-check.png)  |   |
| Android для бизнеса <br> — Рабочий профиль    | ![Поддерживается](./media/certificates-configure/green-check.png) | ![Поддерживается](./media/certificates-configure/green-check.png) | ![Поддерживается](./media/certificates-configure/green-check.png) | ![Поддерживается](./media/certificates-configure/green-check.png) |
| iOS/iPadOS                   | ![Поддерживается](./media/certificates-configure/green-check.png) | ![Поддерживается](./media/certificates-configure/green-check.png) | ![Поддерживается](./media/certificates-configure/green-check.png) | ![Поддерживается](./media/certificates-configure/green-check.png) |
| MacOS                 | ![Поддерживается](./media/certificates-configure/green-check.png) |  ![Поддерживается](./media/certificates-configure/green-check.png) |![Поддерживается](./media/certificates-configure/green-check.png)|![Поддерживается](./media/certificates-configure/green-check.png)|
| Windows Phone 8.1     |![Поддерживается](./media/certificates-configure/green-check.png)  |  | ![Поддерживается](./media/certificates-configure/green-check.png)| ![Поддерживается](./media/certificates-configure/green-check.png) |
| Windows 8.1 и более поздние версии |![Поддерживается](./media/certificates-configure/green-check.png)  |  |![Поддерживается](./media/certificates-configure/green-check.png) |   |
| Windows 10 и более поздней версии  | ![Поддерживается](./media/certificates-configure/green-check.png) | ![Поддерживается](./media/certificates-configure/green-check.png) | ![Поддерживается](./media/certificates-configure/green-check.png) | ![Поддерживается](./media/certificates-configure/green-check.png) |

## <a name="export-the-trusted-root-ca-certificate"></a>Экспорт доверенного корневого сертификата ЦС

Чтобы использовать импортированные сертификаты PKCS, SCEP и PKCS, устройства должны доверять корневому центру сертификации. Чтобы установить доверие, экспортируйте доверенный корневой сертификат ЦС, а также все промежуточные или выдаваемые сертификаты центра сертификации в качестве общедоступного сертификата (CER-файла). Эти сертификаты можно получить из выдающего ЦС или с любого устройства, которое доверяет выдающему ЦС.

Чтобы экспортировать сертификат, обратитесь к документации по своему центру сертификации. Вам потребуется экспортировать открытый сертификат в виде CER-файла.  Не экспортируйте закрытый ключ (PFX).

Этот CER-файл будет использоваться при [создании профилей доверенных сертификатов](#create-trusted-certificate-profiles) для развертывания этого сертификата на устройствах.

## <a name="create-trusted-certificate-profiles"></a>Создание профилей доверенных сертификатов

Перед созданием профиля сертификата SCEP, PKCS или импортированного сертификата PKCS создайте и разверните профиль доверенного сертификата. Развертывание профиля доверенного сертификата в тех же группах, которые получают другие типы профилей сертификатов, гарантирует, что каждое устройство сможет распознать подлинность вашего ЦС. Сюда входят такие профили, как профили для VPN, Wi-Fi и электронной почты.

Профили сертификатов SCEP непосредственно ссылаются на профиль доверенного сертификата. Профили сертификатов PKCS не ссылаются напрямую на профиль доверенного сертификата, но напрямую ссылаются на сервер, на котором размещен ваш ЦС. Профили импортированных сертификатов PKCS не ссылаются напрямую на профиль доверенного сертификата, но могут использовать его на устройстве. Развертывание профиля доверенного сертификата на устройствах гарантирует, что доверие будет установлено. Если устройство не доверяет корневому ЦС, политика профиля сертификата SCEP или PKCS сообщит об ошибке.

Создайте отдельный профиль доверенного сертификата для каждой платформы устройства, которую вы хотите поддерживать, точно так же, как это делается для профилей сертификатов SCEP, PKCS или импортированного сертификата PKCS.

### <a name="to-create-a-trusted-certificate-profile"></a>Создание профиля доверенного сертификата

1. Войдите в [Центр администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Выберите **Устройства** > **Профили конфигурации** > **Создать профиль**.

   ![Перейдите к Intune и создайте профиль для доверенного сертификата](./media/certificates-configure/certificates-configure-profile-new.png)

3. Укажите следующие свойства.
   - **Платформа**. Выберите платформу устройств, которые будут принимать этот профиль.
   - **Профиль**. Выберите **Доверенный сертификат**.
  
4. Щелкните **Создать**.

5. В разделе **Основные** укажите следующие свойства.
   - **Имя** — Введите описательное имя для нового профиля. Назначьте имена профилям, чтобы позже их можно было легко найти. Например, хорошее имя профиля — *Профиль для доверенного сертификата для всей компании*.
   - **Описание**. Введите описание профиля. Этот параметр является необязательным, но мы рекомендуем его использовать.

6. Выберите **Далее**.

7. В **Параметрах конфигурации** укажите CER-файл ранее экспортированного доверенного сертификата корневого ЦС. 

   Только для устройств Windows 8.1 и Windows 10 выберите **Конечное хранилище** для доверенного сертификата из следующих расположений:

   - **хранилище сертификатов на компьютере — корневое**;
   - **хранилище сертификатов на компьютере — промежуточное**;
   - **хранилище сертификатов пользователей — промежуточное**.

   ![Создайте профиль и отправьте доверенный сертификат](./media/certificates-configure/certificates-configure-profile-fill.png)

8. Выберите **Далее**.

9. В поле **Теги области** (необязательно) назначьте тег для фильтрации профиля по конкретным ИТ-группам, например `US-NC IT Team` или `JohnGlenn_ITDepartment`. Дополнительные сведения о тегах области см. в разделе [Использование RBAC и тегов области для распределенных ИТ-групп](../fundamentals/scope-tags.md).

   Выберите **Далее**.

10. В разделе **Назначения** выберите пользователей или группы, которые будут принимать ваш профиль. Дополнительные сведения о назначении профилей см. в статье [Назначение профилей пользователей и устройств](../configuration/device-profile-assign.md).

    Выберите **Далее**.

11. (*Применимо только к Windows 10*) В разделе **Правила применимости** укажите правила применимости, чтобы уточнить назначение этого профиля. Вы можете как назначить, так и не назначать профиль на основе выпуска ОС или версии устройства.

  Сведения о [правилах применимости](../configuration/device-profile-create.md#applicability-rules) см. в руководстве по *созданию профиля устройства в Microsoft Intune*.

12. В окне **Проверка и создание** проверьте параметры. При выборе "Создать" внесенные изменения сохраняются и назначается профиль. Политика также отображается в списке профилей.

## <a name="additional-resources"></a>Дополнительные ресурсы

- [Назначение профилей устройств](../configuration/device-profile-assign.md)  
- [Использование S/MIME для подписывания и шифрования сообщений электронной почты](certificates-s-mime-encryption-sign.md)  
- [Использование сторонних центров сертификации](certificate-authority-add-scep-overview.md)  

## <a name="next-steps"></a>Дальнейшие шаги

Создайте профили сертификатов SCEP, PKCS или импортированных сертификатов PKCS для каждой платформы, которую хотите использовать. Дополнительные сведения см. в следующих статьях:

- [Настройка инфраструктуры для поддержки сертификатов SCEP с помощью Intune](certificates-scep-configure.md)  
- [Настройка инфраструктуры сертификатов Microsoft Intune для PKCS](certficates-pfx-configure.md)  
- [Создание профиля импортированного сертификата PKCS](certificates-imported-pfx-configure.md#create-a-pkcs-imported-certificate-profile)
