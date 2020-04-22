---
title: Включение TLS 1.2 на серверах сайта и удаленных системах сайта
titleSuffix: Configuration Manager
description: В этой статье описано, как включить TLS 1.2 для серверов сайта Configuration Manager.
ms.date: 12/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0ce9b428-cb0f-46f3-bf69-c465e6623d6f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 15377520b76b9b3a3813e6ad4253548f29e011db
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704102"
---
# <a name="how-to-enable-tls-12-on-the-site-servers-and-remote-site-systems"></a>Включение TLS 1.2 на серверах сайта и удаленных системах сайта

*Область применения: Configuration Manager (Current Branch)*

При включении TLS 1.2 для среды Configuration Manager начните с [включения TLS 1.2 для клиентов](enable-tls-1-2-client.md). Затем включите TLS 1.2 на серверах сайта и удаленных системах сайта. Наконец, следует протестировать связь клиента с системой сайта, прежде чем потенциально отключить старые протоколы на стороне сервера. Для включения TLS 1.2 на серверах сайта и удаленных системах сайта выполните следующие задачи:

- Убедитесь, что TLS 1.2 включен в качестве протокола для SChannel на уровне операционной системы
- Обновите и настройте .NET Framework для поддержки TLS 1.2
- Обновление SQL Server и клиентских компонентов
- Обновление служб Windows Server Update Services (WSUS)

Дополнительные сведения о зависимостях для конкретных компонентов и сценариев Configuration Manager см. в разделе [о включении TLS 1.2](enable-tls-1-2.md). 

## <a name="ensure-that-tls-12-is-enabled-as-a-protocol-for-schannel-at-the-operating-system-level"></a><a name="bkmk_protocol"></a> Убедитесь, что TLS 1.2 включен в качестве протокола для SChannel на уровне операционной системы

[!INCLUDE [Enable TLS 1.2 protocol as a security provider](includes/enable-tls-1-2-protocol-security-provider.md)]

## <a name="update-and-configure-the-net-framework-to-support-tls-12"></a><a name="bkmk_net"></a> Обновите и настройте .NET Framework для поддержки TLS 1.2

[!INCLUDE [Update and configure the .NET framework to support TLS 1.2](includes/update-net-framework-to-support-tls-1-2.md)]


## <a name="update-sql-server-and-client-components"></a><a name="bkmk_sql"></a> Обновите SQL Server и клиентские компоненты

Microsoft SQL Server 2016 и более поздних версий поддерживает TLS 1.1 и TLS 1.2. Более ранние версии и зависимые библиотеки могут потребовать обновления. Подробные сведения см. в статье базы знаний KB3135244 [TLS 1.2 support for Microsoft SQL Server](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server) (Поддержка TLS 1.2 для MIcrosoft SQL Server).

Серверы вторичных сайтов должны использовать версию не ниже SQL Server 2016 Express с пакетом обновления 2 (13.2.50.26).

### <a name="sql-server-native-client"></a><a name="bkmk_sql-client"></a> Собственный клиент SQL Server

> [!NOTE]
> В [статье базы знаний 3135244](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server) также описаны требования для клиентских компонентов SQL Server.

Кроме того, обязательно обновите SQL Server Native Client до версии не менее SQL 2012 с пакетом обновления 4 (11.*.7001.0). Начиная с версии 1810 для этого требования выполняется [проверка готовности (с предупреждением)](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).

Configuration Manager использует SQL Server Native Client в следующих ролях системы сайта:

- Сервер базы данных сайтов
- Сервер сайта: сайт центра администрирования, первичный сайт или вторичный сайт
- Точка управления
- Точка управления устройством
- точка миграции состояния,
- Поставщик SMS
- Точка обновления программного обеспечения
- Точка распространения с поддержкой многоадресной рассылки
- Точка службы обновления аналитики активов
- Точка служб отчетов
- веб-служба каталога приложений;
- Точка регистрации
- Точка Endpoint Protection
- Точка подключения службы
- Точка регистрации сертификатов
- Точка обслуживания хранилища данных


## <a name="update-windows-server-update-services-wsus"></a><a name="bkmk_wsus"></a> Обновление служб Windows Server Update Services (WSUS)

Для поддержки TLS 1.2 в более ранних версиях WSUS установите следующее обновление на сервере WSUS:

- На сервере WSUS с Windows Server 2012 установите [обновление 4022721](https://support.microsoft.com/help/4022721) или более позднее.
- На сервере WSUS с Windows Server 2012 R2 установите [обновление 4022720](https://support.microsoft.com/help/4022720) или более позднее.

Начиная с Windows Server 2016 протокол TLS 1.2 поддерживается по умолчанию для служб WSUS.  Обновления TLS 1.2 необходимы только на серверах WSUS Windows Server 2012 и Windows Server 2012 R2.

## <a name="next-steps"></a>Дальнейшие шаги

- [Распространенные проблемы при включении TLS 1.2](enable-tls-1-2-troubleshoot.md)
