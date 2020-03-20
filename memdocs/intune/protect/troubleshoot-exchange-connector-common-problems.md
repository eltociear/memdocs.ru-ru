---
title: Устранение распространенных проблем с соединителем Intune с Exchange
titleSuffix: Microsoft Intune
description: Диагностика и устранение распространенных неполадок с локальным соединителем Microsoft Intune с Exchange.
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/26/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 55f51f94cf26aa2486ef390d5fbb668eaf013e10
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/13/2020
ms.locfileid: "79350633"
---
# <a name="resolve-common-problems-with-the-intune-exchange-connector"></a>Устранение распространенных проблем с соединителем Intune с Exchange
 
Сведения в этой статье помогут администратору службы Intune в устранении распространенных ошибок в работе соединителя Intune с Exchange.

Прежде чем начать устранение неполадок, ознакомьтесь со статьей [Устранение неполадок локального соединителя Exchange](troubleshoot-exchange-connector.md), чтобы получить основные сведения о соединителе. Также ознакомьтесь с общими проблемами настройки соединителя.

## <a name="an-exchange-activesync-device-isnt-discovered-from-exchange"></a>Устройство Exchange ActiveSync не обнаруживается из Exchange

Если устройство Exchange ActiveSync не обнаруживается из Exchange, [отслеживайте активность соединителя Exchange](exchange-connector-install.md#on-premises-intune-exchange-connector-high-availability-support), чтобы узнать, выполняется ли синхронизация соединителя Exchange с сервером Exchange. Если синхронизация не выполнялась с момента присоединения устройства, соберите журналы синхронизации и вложите их в свой запрос на поддержку. При успешном выполнении полной синхронизации или быстрой синхронизации с момента соединения устройства проверьте наличие следующих проблем.

- Убедитесь, что у пользователей есть лицензия Intune. В противном случае соединитель Exchange не обнаружит их устройства.

- Если основной SMTP-адрес пользователя отличается от его имени субъекта-пользователя в Azure Active Directory (Azure AD), то соединитель Exchange не сможет обнаружить устройства для этого пользователя. Для устранения проблемы исправьте основной SMTP-адрес.

- Если в вашей среде используются серверы почтовых ящиков Exchange 2010 и Exchange 2013, рекомендуется нацелить соединитель Exchange на сервер клиентского доступа Exchange 2013 (CAS). Если соединитель Exchange настроен для взаимодействия с сервером клиентского доступа Exchange 2010, соединитель Exchange не сможет обнаружить устройства пользователей в Exchange 2013.

- Для сред Exchange (цен. категория "Выделенный") нужно изначально настроить соединитель Exchange таким образом, чтобы он указывал на сервер клиентского доступа Exchange 2013 (а не Exchange 2010) в выделенной среде. При выполнении командлетов PowerShell соединитель будет обмениваться данными только с центрами сертификации Exchange 2013.

## <a name="problems-with-the-notification-email-message"></a>Проблемы с сообщением электронной почты с уведомлением

Чтобы обеспечить условный доступ для локальных почтовых ящиков на устройствах, которые не работают под управлением Android Knox, убедитесь, что регистрация Intune начинается с сообщения электронной почты о начале работы, которое отправляет соединитель Intune Exchange. Запуск регистрации из сообщения гарантирует, что устройство получает уникальный идентификатор ActiveSyncID на всех платформах (Exchange, Azure AD, Intune).

Пользователь может не получить уведомление по электронной почте по следующим причинам.

- Учетная запись уведомления настроена неправильно.
- Произошел сбой автообнаружения для учетной записи уведомления.
- Сбой запроса веб-служб Exchange (EWS) на отправку сообщения электронной почты.

Ознакомьтесь со следующими разделами, чтобы устранить неполадки с уведомлениями по электронной почте.

### <a name="check-the-notification-account-that-retrieves-autodiscover-settings"></a>Проверьте учетную запись уведомления, которая используется для получения параметров автообнаружения

1. Убедитесь, что служба автоматического обнаружения и веб-службы Exchange настроены в службах клиентского доступа Exchange. Дополнительные сведения см. в разделе [Службы клиентского доступа](https://docs.microsoft.com/Exchange/architecture/client-access/client-access) и [Служба автообнаружения в Exchange Server](https://docs.microsoft.com/Exchange/architecture/client-access/autodiscover?view=exchserver-2019).

2. Убедитесь, что ваша учетная запись уведомления соответствует следующим требованиям.

   - Учетная запись имеет активный почтовый ящик, размещенный на локальном сервере Exchange.

   - Имя субъекта-пользователя учетной записи совпадает с адресом SMTP.

3. Для автообнаружения требуется DNS-сервер с записью DNS для **Autodiscover.SMTPdomain.com** (например, Autodiscover.contoso.com), указывающей на сервер клиентского доступа Exchange. Чтобы проверить запись, укажите полное доменное имя вместо *Autodiscover.SMTPdomain.com* и выполните следующие действия.

   1. В командной строке введите *nslookup*.

   2. Введите *Autodiscover.SMTPdomain.com*. Результат выполнения должен быть аналогичен следующему: ![Результаты nslookup](./media/troubleshoot-exchange-connector-common-problems/nslookup-results.png
      )

   Службу автообнаружения можно также протестировать из Интернета по адресу https://testconnectivity.microsoft.com. Ее также можно протестировать из локального домена с помощью анализатора подключений Майкрософт. Дополнительные сведения см. в статье [Анализатор подключений Майкрософт](https://docs.microsoft.com/previous-versions/office/exchange-remote-connectivity/jj851141(v=exchg.80)).


### <a name="check-autodiscovery"></a>Проверка автообнаружения

Если не удается выполнить автообнаружение, попробуйте выполнить следующие действия.

1. [Настройте допустимую запись DNS автообнаружения](https://docs.microsoft.com/previous-versions/exchange-server/exchange-150/mt473798(v=exchg.150)).

2. В явном виде укажите URL-адрес EWS в файле конфигурации соединителя Intune Exchange:

   1. определите URL-адрес EWS. URL-адрес EWS по умолчанию для Exchange — `https://<mailServerFQDN>/ews/exchange.asmx`, но ваш URL-адрес может отличаться. Обратитесь к администратору Exchange, чтобы уточнить правильный URL-адрес вашей среды.

   2. Откройте для редактирования файл *OnPremisesExchangeConnectorServiceConfiguration.xml*. По умолчанию файл расположен в папке *%ProgramData%\Microsoft\Windows Intune Exchange Connector* на компьютере, на котором работает соединитель Exchange. Откройте файл в текстовом редакторе, а затем измените следующую строку в соответствии с URL-адресом EWS для вашей среды: `<ExchangeWebServiceURL> https://<YourExchangeHOST>/EWS/Exchange.asmx</ExchangeWebServiceURL>`

3. Сохраните файл, а затем перезагрузите компьютер или перезапустите службу соединителя Exchange Microsoft Intune.

>[!NOTE]
> В этой конфигурации соединитель Intune Exchange перестает использовать автообнаружение и подключается напрямую к URL-адресу EWS.

## <a name="next-steps"></a>Дальнейшие шаги

Чтобы получить справку по конкретным ошибкам, попробуйте [устранить распространенные ошибки соединителя Intune Exchange](troubleshoot-exchange-connector-common-errors.md).

Чтобы получить поддержку из сообщества Intune:

- Обратитесь к разделу [Поддержка](../fundamentals/get-support.md), чтобы использовать консоль Intune для устранения неполадок или для обращения в службу поддержки Майкрософт.
- Опубликуйте свой вопрос на [форумах Microsoft Intune](https://social.technet.microsoft.com/Forums/home?forum=microsoftintuneprod).