---
title: Распространенные проблемы при включении протокола TLS 1.2
titleSuffix: Configuration Manager
description: Описание распространенных проблем при включении протокола TLS 1.2
ms.date: 12/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 15083f28-8ff2-4e23-9f5e-b5dbd0859839
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7c07b0af1b3063619ac5f71965d96f611aefafd9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704072"
---
# <a name="common-issues-when-enabling-tls-12"></a>Распространенные проблемы при включении TLS 1.2

В этом разделе представлены рекомендации по устранению распространенных проблем, которые возникают при включении поддержки TLS 1.2 в Configuration Manager.

## <a name="unsupported-platforms"></a>Неподдерживаемые платформы

Следующие клиентские платформы поддерживаются Configuration Manager, но не поддерживаются в среде TLS 1.2:

- Windows CE
- Apple OS X;
- устройства Windows 10, управляемые с помощью локального решения MDM.

## <a name="reports-dont-show-in-the-console"></a>Отчеты не отображаются в консоли

Если отчеты не отображаются в консоли Configuration Manager, установите обновления на компьютере, на котором работает консоль. [Обновите .NET Framework](enable-tls-1-2-client.md#bkmk_net) и включите криптостойкость.

## <a name="fips-security-policy-enabled"></a>Включена политика безопасности FIPS

Если включен параметр политики безопасности FIPS для сервера или клиента, в ходе согласования безопасного канала (Schannel) может быть выбран протокол TLS 1.0. Это происходит даже в том случае, если вы отключили этот протокол в реестре.

Чтобы определить причину проблемы, включите ведение журнала событий для канала безопасности, а затем просмотрите события Schannel в системном журнале. Подробные сведения см. в статье [How to restrict the use of certain cryptographic algorithms and protocols in Schannel.dll](https://support.microsoft.com/help/245030/how-to-restrict-the-use-of-certain-cryptographic-algorithms-and-protoc) (Как ограничить использование определенных алгоритмов шифрования и протоколов в Schannel.dll).

## <a name="sql-server-communication-failure"></a>Сбой связи SQL Server

Если при связи с SQL Server возникает ошибка **SslSecurityError**, сделайте следующее:

- [Обновите .NET Framework](enable-tls-1-2-server.md#bkmk_net) и включите криптостойкость на каждом компьютере.
- [Обновите SQL Server](enable-tls-1-2-server.md#bkmk_sql) на сервере узла.
- [Обновите клиентские компоненты SQL](enable-tls-1-2-server.md#bkmk_sql-client) во всех системах, которые обмениваются данными с SQL (например, на серверах сайтов, в поставщике SMS и на серверах ролей сайтов).

## <a name="configuration-manager-client-communication-failures"></a>Сбои связи клиента Configuration Manager

Если клиент Configuration Manager не взаимодействует с ролями сайтов, убедитесь, что вы [обновили Windows](enable-tls-1-2-client.md#bkmk_winhttp) для поддержки TLS 1.2 для обмена данными между клиентом и сервером через WinHTTP. Типичные роли сайта включают точки распространения, точки управления и точки миграции состояния.

## <a name="reporting-services-point-fails-and-returns-an-expected-error"></a>Сбой точки служб отчетов с возвращением ожидаемой ошибки

Если для точки служб отчетов не настроены отчеты, проверьте наличие указанной ниже записи в журнале **SRSRP.log**:

`The underlying connection was closed:`
`An expected error occurred on a receive.`

Для устранения этой проблемы выполните следующие действия:

1. [Обновите .NET Framework](enable-tls-1-2-client.md#bkmk_net) и включите криптостойкость на всех нужных компьютерах.

1. После установки обновлений перезапустите службу SMS_Executive.

## <a name="application-catalog-doesnt-initialize"></a>Каталог приложений не инициализируется

> [!Important]  
> Поддержка ролей каталога приложений прекращена в версии 1910. Дополнительные сведения см. в разделе [Удаленные и устаревшие компоненты](../changes/deprecated/removed-and-deprecated-cmfeatures.md).

Если каталог приложений не инициализируется, проверьте наличие указанной ниже записи в файле **ServicePortalWebSite.svclog**:

`SOAP security negotiation failed. The client and server can't communicate because they don't share a common algorithm.`

Для устранения этой проблемы выполните следующие действия:

1. [Обновите .NET Framework](enable-tls-1-2-client.md#bkmk_net) и включите криптостойкость на всех нужных компьютерах.

1. В папке `%WinDir%\System32\InetSrv` на сервере каталога приложений создайте файл **W2SP.exe.config** с таким содержимым:

    ``` XML
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <runtime>
      <AppContextSwitchOverrides value="Switch.System.ServiceModel.DisableUsingServicePointManagerSecurityProtocols=false;Switch.System.Net.DontEnableSchUseStrongCrypto=false" />
      </runtime>
    </configuration>
    ```

    > [!NOTE]
    > Это файл по умолчанию, который создается в процессе сборки приложения с помощью .NET Framework 4.6.3.

1. Используйте защиту транспорта HTTPS для ролей каталога приложений.

    > [!Important]
    > Если вы применяете защиту сообщений HTTP для ролей каталога приложений, WCF может использовать только SSL 3.0 и TLS 1.0. Протокол TLS 1.2 в таком случае недоступен.

1. Если вы внесли изменения, перезагрузите компьютер.

## <a name="software-center-or-browser-doesnt-communicate-with-the-application-catalog"></a>Центр программного обеспечения или браузер не взаимодействуют с каталогом приложений

> [!Important]  
> Поддержка ролей каталога приложений прекращена в версии 1910. Дополнительные сведения см. в разделе [Удаленные и устаревшие компоненты](../changes/deprecated/removed-and-deprecated-cmfeatures.md).

Чтобы обеспечить беспроблемную работу центра программного обеспечения с доступными пользователям приложениями на сайте с включенным протоколом TLS 1.2, удалите роль каталога приложений. Затем разрешите центру программного обеспечения напрямую обмениваться данными с точкой управления. Дополнительные сведения см. в разделе [Удаление каталога приложений](../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat).

Если вам нужно устранить ошибки связи между каталогом приложений и центром программного обеспечения, сделайте следующее:

- [Обновите .NET Framework](enable-tls-1-2-client.md#bkmk_net) и включите криптостойкость на каждом компьютере.

- После внесения изменений перезагрузите все обновленные компьютеры.

<!-- - Configure the browser is configured to support TLS 1. Prior to Windows 10, this option was disabled by default. removing, Silverlight experience is out of support-->

## <a name="service-connection-point-upload-failures"></a>Сбои отправки на точке подключения службы

Если точка подключения службы не отправляет данные в службу SCCMConnectedService, [обновите .NET Framework](enable-tls-1-2-server.md#bkmk_net) и включите криптостойкость на каждом компьютере. После внесения изменений обязательно перезагрузите компьютеры.

## <a name="configuration-manager-console-displays-intune-onboarding-dialog-box"></a>Консоль Configuration Manager отображает диалоговое окно подключения Intune

Если при попытке консоли подключиться к порталу Intune отображается диалоговое окно подключения Intune, [обновите .NET Framework](enable-tls-1-2-client.md#bkmk_net) и включите криптостойкость на каждом компьютере. После внесения изменений обязательно перезагрузите компьютеры.

## <a name="configuration-manager-console-displays-failure-to-sign-in-to-azure"></a>Консоль Configuration Manager отображает ошибку при входе в Azure

Если при попытке создать приложения в Azure Active Directory (Azure AD) в диалоговом окне подключения служб Azure отображается ошибку сразу же, как только вы выбираете **Войти**, [обновите .NET Framework](enable-tls-1-2-server.md#bkmk_net) и включите криптостойкость. После внесения изменений обязательно перезагрузите компьютеры.

## <a name="configuration-manager-cloud-services-and-tls-12"></a>Облачные службы Configuration Manager и TLS 1.2

Виртуальные машины Azure, используемые шлюзом управления облачными клиентами и облачными точками распространения, поддерживают TLS 1.2. Поддерживаемые версии клиентов автоматически используют TLS 1.2.

**SMSAdminui.log** может содержать сообщение об ошибке, подобное приведенному ниже:

``` Log
Microsoft.ConfigurationManager.CloudBase.AAD.AADAuthenticationException
Service returned error. Check InnerException for more details
at Microsoft.ConfigurationManager.CloudBase.AAD.AADAuthenticationContext.GetAADAuthResultObject
...
Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException
Service returned error. Check InnerException for more details
at Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext.RunAsyncTask
...
System.Net.WebException
The underlying connection was closed: An unexpected error occurred on a receive.
at System.Net.HttpWebRequest.GetResponse
```

В журнале системных событий для EventID 36874 SChannel может быть записано следующее описание: `An TLS 1.2 connection request was received from a remote client application, but none of the cipher suites supported by the client application are supported by the server. The TLS connection request has failed.`
<!--SCCMDocs issue #1608-->

## <a name="additional-resources"></a>Дополнительные ресурсы

- [Рекомендации по использованию протокола TLS с .NET Framework](https://docs.microsoft.com/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry)
- [Статья базы знаний 3135244. Поддержка TLS 1.2 для Microsoft SQL Server](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server)
- [Технический справочник по элементам управления шифрования](cryptographic-controls-technical-reference.md)

## <a name="next-steps"></a>Дальнейшие шаги

- [Включение TLS 1.2 на клиентах](enable-tls-1-2-client.md)
- [Включение TLS 1.2 на серверах сайта и удаленных системах сайта](enable-tls-1-2-server.md)

