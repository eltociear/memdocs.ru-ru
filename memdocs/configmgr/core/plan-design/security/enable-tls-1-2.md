---
title: Обзор включения TLS 1.2
titleSuffix: Configuration Manager
description: Общие сведения о том, как включить TLS 1.2 для Configuration Manager.
ms.date: 12/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 31de47c9-891b-4de7-8d5e-fbbc1bff7c60
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5d9d7cea7e5653b338a3eb4adb01d9fded99035e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704062"
---
# <a name="how-to-enable-tls-12"></a>Как включить TLS 1.2

*Область применения: Configuration Manager (Current Branch)*

Протокол TLS, например, SSL, является протоколом шифрования, предназначенным для обеспечения безопасности данных при передаче по сети. В этих статьях описывается, как обеспечить безопасный обмен данными по протоколу TLS 1.2 в Configuration Manager. Кроме того, в них приводятся требования к обновлению для часто используемых компонентов и рекомендации по устранению распространенных проблем.

## <a name="enabling-tls-12"></a>Включение TLS 1.2

Configuration Manager обеспечивает безопасный обмен данными с помощью множества различных компонентов. Протокол, который используется для конкретного подключения, зависит от возможностей всех соответствующих компонентов на стороне клиента и сервера. Если один из компонентов устарел или настроен неправильно, при обмене данными может использоваться старая, менее безопасная версия протокола. Чтобы корректно включить поддержку TLS 1.2 для всех безопасных подключений в Configuration Manager, вам нужно сделать это для всех необходимых компонентов. Необходимые компоненты зависят от вашей среды и используемых функций Configuration Manager.

> [!IMPORTANT]
> Начните с клиентов, особенно если используются предыдущие версии Windows. Прежде чем включить TLS 1.2 и отключить старые протоколы на серверах Configuration Manager, убедитесь, что все клиенты поддерживают этот протокол. В противном случае клиенты не смогут обмениваться данными с серверами и могут быть потеряны.


## <a name="tasks-for-configuration-manager-clients-site-servers-and-remote-site-systems"></a>Задачи для клиентов Configuration Manager, серверов сайта и удаленных систем сайта

Чтобы включить TLS 1.2 для компонентов, от которых зависит Configuration Manager для защищенного обмена данными, необходимо выполнить несколько задач на стороне клиентов и серверов сайта.

### <a name="enable-tls-12-for-configuration-manager-clients"></a>Включение TLS 1.2 для клиентов Configuration Manager

- [Обновите Windows и WinHTTP в Windows 8.0, Windows Server 2012 (не R2) и более ранних версий](enable-tls-1-2-client.md#bkmk_winhttp)
- [Убедитесь, что TLS 1.2 включен в качестве протокола для SChannel на уровне операционной системы](enable-tls-1-2-client.md#bkmk_protocol)
- [Обновите и настройте .NET Framework для поддержки TLS 1.2](enable-tls-1-2-client.md#bkmk_net)


### <a name="enable-tls-12-for-configuration-manager-site-servers-and-remote-site-systems"></a>Включите TLS 1.2 для серверов сайта Configuration Manager и удаленных систем сайта

- [Убедитесь, что TLS 1.2 включен в качестве протокола для SChannel на уровне операционной системы](enable-tls-1-2-server.md#bkmk_protocol)
- [Обновите и настройте .NET Framework для поддержки TLS 1.2](enable-tls-1-2-server.md#bkmk_net)
- [Обновите SQL Server и SQL Native Client](enable-tls-1-2-server.md#bkmk_sql)
- [Обновить службы Windows Server Update Services (WSUS).](enable-tls-1-2-server.md#bkmk_wsus)


## <a name="features-and-scenario-dependencies"></a>Компоненты и зависимости сценариев

В этом разделе описаны зависимости для определенных функций и сценариев Configuration Manager. Чтобы определить дальнейшие действия, найдите элементы, которые имеют отношение к вашей среде.

|Возможность или сценарий|Обновление задач|
|--- |--- |
|Серверы сайтов (центральные, серверы-источники или серверы-получатели)| - [Обновите .NET Framework](enable-tls-1-2-server.md#bkmk_net)<br/> – Проверьте параметры криптостойкости|
|Сервер базы данных сайтов|[Обновите SQL Server и его клиентские компоненты](enable-tls-1-2-server.md#bkmk_sql)|
|Сервер вторичного сайта|[Обновите SQL Server и его клиентские компоненты](enable-tls-1-2-server.md#bkmk_sql) до совместимой версии SQL Express|
|Роли систем сайта| - [Обновите .NET Framework](enable-tls-1-2-server.md#bkmk_net) и проверьте параметры стойкости шифрования <br/> - [Обновите SQL Server и его клиентские компоненты](enable-tls-1-2-server.md#bkmk_sql) для ролей, которые требуют этого, в том числе для [SQL Server Native Client](enable-tls-1-2-server.md#bkmk_sql-client)|
|Точка служб отчетов|- [Обновите .NET Framework](enable-tls-1-2-server.md#bkmk_net) на сервере сайта, серверах SQL Reporting Services и всех компьютерах с консолью<br/> – При необходимости перезапустите службу SMS_Executive|
|Точка обновления программного обеспечения|[Обновите службы WSUS](enable-tls-1-2-server.md#bkmk_wsus)|
|Шлюз управления облаком|[Принудительное применение TLS 1.2](../../clients/manage/cmg/security-and-privacy-for-cloud-management-gateway.md#bkmk_tls)|
|Консоль Configuration Manager| - [Обновите .NET Framework](enable-tls-1-2-client.md#bkmk_net)<br/> – Проверьте параметры криптостойкости|
|Клиент Configuration Manager с ролями системы сайта HTTPS|[Обновите Windows для поддержки TLS 1.2 для обмена данными между клиентом и сервером через WinHTTP](enable-tls-1-2-client.md#bkmk_winhttp)|
|Центр программного обеспечения| - [Обновите .NET Framework](enable-tls-1-2-client.md#bkmk_net)<br/> – Проверьте параметры криптостойкости|
|Клиенты Windows 7| *Прежде чем* включать TLS 1.2 на каких-либо серверных компонентах, [обновите Windows для поддержки TLS 1.2 для обмена данными между клиентом и сервером через WinHTTP](enable-tls-1-2-client.md#bkmk_winhttp). Если сначала включить TLS 1.2 на серверных компонентах, ранние версии клиентов могут быть потеряны.|

## <a name="frequently-asked-questions"></a>Часто задаваемые вопросы

### <a name="why-use-tls-12-with-configuration-manager"></a>Зачем использовать TLS 1.2 с Configuration Manager?

TLS 1.2 более безопасен, чем предыдущие криптографические протоколы, такие как SSL 2.0, SSL 3.0, TLS 1.0 и TLS 1.1. По сути, TLS 1.2 обеспечивает безопасность передачи данных по сети.

### <a name="where-does-configuration-manager-use-encryption-protocols-like-tls-12"></a>Где Configuration Manager использует протоколы шифрования, например TLS 1.2?

Существует пять основных задач, для которых Configuration Manager использует протоколы шифрования, такие как TLS 1.2:

- Взаимодействие клиента с ролями сервера сайта на основе IIS, если роль настроена для использования протокола HTTPS. Примерами таких ролей являются точки распространения, точки обновления программного обеспечения и точки управления.
- Обмен данными между точкой управления, службой SMS Executive и поставщиком SMS с помощью SQL. Configuration Manager всегда шифрует обмен данными с SQL.
- Обмен данными между сервером сайта и службами WSUS, если служба WSUS настроена для использования протокола HTTPS.
- Консоль Configuration Manager для служб SQL Reporting Services (SSRS), если службы SSRS настроены для использования протокола HTTPS.
- Любые подключения к интернет-службам. Например, шлюз управления облачными службами (CMG), синхронизация точки подключения службы и синхронизация метаданных обновления из Центра обновления Майкрософт.

### <a name="what-determines-which-encryption-protocol-is-used"></a>Как определить, какой протокол шифрования использовать?

Протокол HTTPS всегда будет требовать наивысшую версию протокола, поддерживаемую как клиентом, так и сервером, в зашифрованном обмене данных. При установлении соединения клиент отправляет на сервер сообщение с наивысшим доступным протоколом. Если сервер поддерживает ту же версию, он отправляет сообщение, используя эту версию. Эта согласованная версия и используется для соединения. Если сервер не поддерживает версию, представленную клиентом, то в сообщении сервера будет указана самая высокая версия, которую он может использовать. Дополнительные сведения о протоколе подтверждения TLS см. в разделе [Установка защищенного сеанса с помощью TLS](https://docs.microsoft.com/windows/win32/secauthn/tls-handshake-protocol#establishing-a-secure-session-by-using-tls).

### <a name="what-determines-which-protocol-version-the-client-and-server-can-use"></a>Что определяет версию протокола, которую может использовать клиент и сервер?

Как правило, следующие элементы могут определить используемую версию протокола:

- Приложение может определять, какие версии протоколов следует согласовать.
  - Рекомендуется избегать использования строго установленных версий протоколов на уровне приложения и соблюдать конфигурацию, определенную на уровне протокола компонента и операционной системы.
  - Configuration Manager следует этим рекомендациям.
- Для приложений, написанных с использованием .NET Framework, версии протокола по умолчанию зависят от версии платформы, на которой они были скомпилированы.  
  - Версии .NET до 4.6.3 не включали TLS 1.1 и 1.2 в списке протоколов для согласования по умолчанию.
- Приложения, использующие WinHTTP для соединений по протоколу HTTPS, например клиент Configuration Manager, зависят от версии операционной системы, уровня обновления и конфигурации для поддержки версии протокола.


## <a name="additional-resources"></a>Дополнительные ресурсы

- [Технический справочник по элементам управления шифрования](cryptographic-controls-technical-reference.md)
- [Рекомендации по использованию протокола TLS с .NET Framework](https://docs.microsoft.com/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry)
- [Статья базы знаний 3135244. Поддержка TLS 1.2 для Microsoft SQL Server](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server)

## <a name="next-steps"></a>Дальнейшие шаги

- [Включение TLS 1.2 на клиентах](enable-tls-1-2-client.md)
- [Включение TLS 1.2 на серверах сайта](enable-tls-1-2-server.md)
