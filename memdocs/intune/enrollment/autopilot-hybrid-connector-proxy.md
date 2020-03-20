---
title: Настройка параметров прокси-сервера для соединителя Intune для Active Directory
description: В этой статье описывается настройка соединителя Intune для Active Directory для работы с имеющимися локальными прокси-серверами.
keywords: ''
author: master11218
ms.author: erikje
manager: dougeby
ms.date: 4/16/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: tanvira
ms.suite: ems
search.appverid: ''
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: 227ed78b593ce10d47b9a1cdcc14dfbd58acdd93
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/13/2020
ms.locfileid: "79339518"
---
# <a name="work-with-existing-on-premises-proxy-servers"></a>Работа с имеющимися локальными прокси-серверами

В этой статье описывается, как настроить соединитель Intune для Active Directory для работы с исходящими прокси-серверами. Она предназначена для клиентов, имеющих в своей сетевой среде прокси-серверы.

По умолчанию соединитель Intune для Active Directory попытается автоматически обнаружить прокси-сервер в сети, используя автоматическое обнаружение веб-прокси (WPAD). Если он настроен в сети, дополнительная настройка может не потребоваться.  Если требуются изменения, в следующих разделах описано, как переопределить параметры по умолчанию, используя [стандартные возможности .NET Framework для настройки параметров прокси-сервера](https://docs.microsoft.com/dotnet/framework/configure-apps/file-schema/network/defaultproxy-element-network-settings).  Дополнительные параметры описаны в этой документации.

Дополнительные сведения о работе соединителей см. в разделе [Сведения о соединителях Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy-connectors).

## <a name="completely-bypass-outbound-proxies"></a>Полный обход исходящих прокси-серверов

Можно настроить соединитель для обхода вашего локального прокси-сервера, чтобы убедиться, что он использует прямое подключение к службам Azure. Это рекомендуемый подход в случае, если это допускает ваша сетевая политика, поскольку это сократит количество настроек, которые необходимо поддерживать.

Чтобы отключить в соединителе использование исходящего прокси-сервера, измените файл :\Program Files\Microsoft Intune\ODJConnector\ODJConnectorUI\ODJConnectorUI.exe.config и добавьте адрес и порт прокси-сервера в раздел, показанный в следующем примере кода:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <system.net>  
        <defaultProxy>   
            <defaultProxy enabled="False" /> 
        </defaultProxy>  
    </system.net>
    <runtime>
        <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
            <dependentAssembly>
                <assemblyIdentity name="mscorlib" publicKeyToken="b77a5c561934e089" culture="neutral"/>
                <bindingRedirect oldVersion="0.0.0.0-2.0.0.0" newVersion="4.6.0.0" />
            </dependentAssembly>
        </assemblyBinding>
    </runtime>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6" />
    </startup>
    <appSettings>
        <add key="SignInURL" value="https://portal.manage.microsoft.com/Home/ClientLogon"/>
        <add key="LocationServiceEndpoint" value="RestUserAuthLocationService/RestUserAuthLocationService/ServiceAddresses"/>
    </appSettings>
</configuration>
```

Для того чтобы служба средства обновления соединителей также обходила прокси-сервер, сделайте аналогичные изменения в файле C:\Program Files\Microsoft Intune\ODJConnector\ODJConnectorSvc\ODJConnectorSvc.exe.config.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <system.net>  
        <defaultProxy>
            <defaultProxy enabled="False" /> 
        </defaultProxy>  
    </system.net>
    <startup>
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6" />
    </startup>
    <appSettings>
        <add key="BaseServiceAddress" value="https://manage.microsoft.com/" />
    </appSettings>
</configuration>
```

Обязательно сделайте копии исходных файлов на случай, если вам понадобится вернуться к файлам конфигурации по умолчанию.

После внесения изменений в файл конфигурации необходимо перезапустить службу соединителя Intune. 

1. Откройте **services.msc**.
2. Найдите и выберите **Служба соединителя ODJ Intune**.
3. Выберите **Перезапуск**.

![Снимок экрана: перезапуск службы](./media/autopilot-hybrid-connector-proxy/service-restart.png)


## <a name="specifying-an-alternative-proxy-server"></a>Указание альтернативного прокси-сервера

Если с соединителем Intune для Active Directory следует использовать другой прокси-сервер (например, для обхода проверки подлинности), его можно указать аналогичным образом. Для этого измените файл :\Program Files\Microsoft Intune\ODJConnector\ODJConnectorUI\ODJConnectorUI.exe.config и добавьте адрес и порт прокси-сервера в раздел, показанный в следующем примере кода:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <system.net>  
        <defaultProxy>   
            <proxy proxyaddress="<PROXY ADDRESS HERE>:<PORT HERE>" bypassonlocal="True" usesystemdefault="True"/>   
        </defaultProxy>  
    </system.net>
    <runtime>
        <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
            <dependentAssembly>
                <assemblyIdentity name="mscorlib" publicKeyToken="b77a5c561934e089" culture="neutral"/>
                <bindingRedirect oldVersion="0.0.0.0-2.0.0.0" newVersion="4.6.0.0" />
            </dependentAssembly>
        </assemblyBinding>
    </runtime>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6" />
    </startup>
    <appSettings>
        <add key="SignInURL" value="https://portal.manage.microsoft.com/Home/ClientLogon"/>
        <add key="LocationServiceEndpoint" value="RestUserAuthLocationService/RestUserAuthLocationService/ServiceAddresses"/>
    </appSettings>
</configuration>
```

Для того чтобы служба средства обновления соединителей также обходила прокси-сервер, сделайте аналогичные изменения в файле C:\Program Files\Microsoft Intune\ODJConnector\ODJConnectorSvc\ODJConnectorSvc.exe.config.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <system.net>  
        <defaultProxy>   
            <proxy proxyaddress="<PROXY ADDRESS HERE>:<PORT HERE>" bypassonlocal="True" usesystemdefault="True"/>   
        </defaultProxy>  
    </system.net>
    <startup>
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6" />
    </startup>
    <appSettings>
        <add key="BaseServiceAddress" value="https://manage.microsoft.com/" />
    </appSettings>
</configuration>
```

Обязательно сделайте копии исходных файлов на случай, если вам понадобится вернуться к файлам конфигурации по умолчанию.

После внесения изменений в файл конфигурации необходимо перезапустить службу соединителя Intune. 

1. Откройте **services.msc**.
2. Найдите и выберите **Служба соединителя ODJ Intune**.
3. Выберите **Перезапуск**.

![Снимок экрана: перезапуск службы](./media/autopilot-hybrid-connector-proxy/service-restart.png)


## <a name="next-steps"></a>Дальнейшие шаги

[Управление вашими устройствами](../remote-actions/device-management.md)
