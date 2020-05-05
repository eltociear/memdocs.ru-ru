---
title: Установка соединителя Exchange
titleSuffix: Configuration Manager
description: Установите и настройте соединитель Exchange для Configuration Manager для управления мобильными устройствами с помощью ActiveSync.
ms.date: 12/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: e179e30a-a1fc-461e-8087-ff3a55803450
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3d854e4b70a59a364b8611947feea89d4678e7e6
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724848"
---
# <a name="install-and-configure-the-exchange-connector"></a>Установка и Настройка соединителя Exchange

*Область применения: Configuration Manager (Current Branch)*

Используйте эту процедуру для установки и настройки коннектора Exchange Server для управления мобильными устройствами. Configuration Manager поддерживает только один коннектор в организации Exchange.

Перед установкой коннектора Exchange Server для Configuration Manager убедитесь, что у вас есть необходимые разрешения и версии. Дополнительные сведения см. в разделе [Управление устройствами с помощью Exchange и Configuration Manager](manage-mobile-devices-with-exchange-activesync.md#prerequisites).

## <a name="exchange-connection-account"></a>Учетная запись подключения Exchange

Выберите учетную запись, которая будет подключаться к серверу клиентского доступа Exchange для управления мобильными устройствами. Это может быть учетная запись компьютера сервера сайта или учетная запись пользователя Windows.

Затем настройте эту учетную запись в группе ролей Exchange для выполнения следующих командлетов Exchange Server:

- **Clear-ActiveSyncDevice**  

- **Get-ActiveSyncDevice;**  

- **Get-ActiveSyncDeviceAccessRule**  

- **Get-ActiveSyncDeviceStatistics;**  

- **Get-ActiveSyncMailboxPolicy**  

- **Get-ActiveSyncOrganizationSettings**  

- **Get-ExchangeServer;**  

- **Get-Mailbox**

- **Get-Recipient;**  

- **Set-ADServerSettings;**  

- **Set-ActiveSyncDeviceAccessRule**  

- **Set-ActiveSyncMailboxPolicy**  

- **Set-CASMailbox**  

- **New-ActiveSyncDeviceAccessRule**  

- **New-ActiveSyncMailboxPolicy**  

- **Remove-ActiveSyncDevice**  

- **Get-CasMailbox**  

- **Get-пользователь**  

- **Set-ActiveSyncOrganizationSettings**  

Эти командлеты включены в следующие роли управления Exchange Server:

- Управление получателями
- Управление организацией только для просмотра
- Управление сервером

См. Дополнительные сведения [о группах ролей управления](https://docs.microsoft.com/exchange/understanding-management-role-groups-exchange-2013-help) в документации по Exchange Server 2013.

> [!TIP]  
> Если вы попытаетесь установить или использовать коннектор Exchange Server без необходимых командлетов, в файле файле easdisc. log на компьютере сервера сайта появится следующая ошибка: `Invoking cmdlet <cmdlet> failed`.

## <a name="install-the-connector"></a>Установка соединителя

1. В консоли Configuration Manager перейдите в рабочую область **Администрирование** , разверните узел **Конфигурация иерархии**и выберите **коннекторы Exchange Server**.

1. На вкладке ленты **Главная** в группе **создать** выберите **Добавить Exchange Server**.

1. На странице **Общие** мастера добавления сервера Exchange Server выберите одну из сред Exchange Server.

    - **Локальный сервер Exchange Server**. Укажите один сервер или массив серверов клиентского доступа для каждого Active Directory сайта.

        Если сервер или массив находится вне сети, Configuration Manager пытается обнаружить сервер клиентского доступа для использования. В случае неудачи Configuration Manager использует сервер почтовых ящиков для установки подключения к серверу клиентского доступа. При попытке подключения она записывает в журнал следующие предупреждения в файле файле easdisc. log на компьютере сервера сайта: `Failed to open runspace for site <site_name>`.

    - **Размещенный сервер Exchange Server**. Укажите адрес сервера для среды Exchange Online.

    Затем выберите первичный сайт для запуска коннектора Exchange Server.

1. На странице **учетная запись** укажите учетную запись для подключения к серверу Exchange. Дополнительные сведения см. в разделе [учетная запись подключения Exchange](#exchange-connection-account).

1. На странице **Обнаружение** настройте расписание синхронизации и правила поиска устройств.

1. На странице **Параметры** настройте параметры мобильного устройства в следующих группах:

    - **Общие**
    - **Пароль**
    - **Управление электронной почтой**
    - **Безопасность**
    - **Приложение**

    Дополнительные сведения см. в разделе [параметры соединителя Exchange](manage-mobile-devices-with-exchange-activesync.md#policies).

    Если вы также регистрируете мобильные устройства с помощью Configuration Manager [ЛОКАЛЬНОГО MDM](../understand/manage-mobile-devices-with-on-premises-infrastructure.md), включите параметр **Разрешить внешнее управление мобильными устройствами**. Этот параметр позволяет этим мобильным устройствам продолжать получать электронную почту из Exchange после того, как Configuration Manager зарегистрирует их.

1. Завершите работу мастера.

## <a name="verify-and-monitor"></a>Проверка и мониторинг

Проверьте установку коннектора Exchange Server с сообщениями о состоянии и файлами журналов:

- Убедитесь, что диспетчер компонентов сайта успешно установил коннектор Exchange Server. Найдите в компоненте **SMS_EXCHANGE_CONNECTOR** сообщение с идентификатором Status **1015** .

    Установка может завершиться ошибкой, если указанный сервер клиентского доступа находится в автономном режиме. Если Configuration Manager не удается успешно установить соединитель, Configuration Manager повторяет установку каждые 60 минут. Повторная попытка будет повторяться до тех пор, пока установка не будет завершена или коннектор Exchange Server не будет удален.

- На компьютере сервера сайта проверьте **SiteComp. log** на наличие следующей записи: `Component SMS_EXCHANGE_CONNECTOR flagged for installation`. Затем он регистрирует успешную установку со следующим текстом: `STATMSG: ID=1015`.

После завершения установки Отслеживайте мобильные устройства, обнаруженные и управляемые соединителем. Просмотр коллекций мобильных устройств и использование отчетов для мобильных устройств.

> [!NOTE]  
> Configuration Manager создает имена для найденных мобильных устройств. В нем используется*тип устройства*формат *имя пользователя*_. Например, **jdoe_WindowsPhone**. Если у пользователя несколько мобильных устройств, имеющих один и тот же тип, Configuration Manager отображает для этих устройств одинаковое имя и в консоли, и в отчетах.  

## <a name="see-also"></a>См. также

- [Порты, используемые клиентами конфигурации и системами сайта](../../core/plan-design/hierarchy/ports.md#BKMK_PortsExchangeConnectorHosted)
- [Поддержка прокси-сервера](../../core/plan-design/network/proxy-server-support.md#site-system-roles-that-use-a-proxy)
- [Рекомендации по безопасности для мобильных устройств](../../core/clients/deploy/plan/security-and-privacy-for-clients.md#bkmk_mobile)
- [Сведения о конфиденциальности мобильных устройств, управляемых с помощью коннектора Exchange Server](../../core/clients/deploy/plan/security-and-privacy-for-clients.md#BKMK_Privacy_ExchangeConnector)
