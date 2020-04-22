---
title: Рабочий процесс проверки подлинности Azure AD
titleSuffix: Configuration Manager
description: Сведения о процессе установки клиента Configuration Manager на устройстве c Windows 10 с проверкой подлинности Azure Active Directory
ms.date: 07/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 9aaf466a-3f40-4468-b3cd-f0010f21f05a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9215688104b1a929cad7c172126387961851760b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695002"
---
# <a name="azure-ad-authentication-workflow"></a>Рабочий процесс проверки подлинности Azure AD

*Область применения: Configuration Manager (Current Branch)*

Эта статья содержит справочные сведения о процессе установки клиента Configuration Manager на устройстве с Windows 10, присоединенном к Azure Active Directory (Azure AD). Здесь подробно рассматривается рабочий процесс проверки подлинности устройства и установки клиента.  
 

## <a name="azure-ad-token-request-workflow"></a>Рабочий процесс запроса маркера безопасности Azure AD

![Схема рабочего процесса Azure AD CCMSetup](media/azure-ad-install-workflow.png)  

### <a name="1-azure-ad-token-request"></a>1. Запрос маркера безопасности Azure AD

Клиент Windows 10, присоединенный к домену Azure AD, использует параметры Azure AD для запроса маркера безопасности. В **ccmsetup.log** регистрируются приведенные ниже записи.

- Запрос маркера безопасности Azure AD для устройства:

    ``` Log
    Getting AAD (device) token with: ClientId = 22ed38d9-XXXX-4036-XXXX-a98452fda4fc, ResourceUrl = https://ConfigMgrService, AccountId = https://login.microsoftonline.com/common/oauth2/token
    ```

- Если маркер безопасности для устройства получить не удалось, запрашивается маркер безопасности Azure AD для пользователя:

    ``` Log
    Getting AAD (user) token with: ClientId = f1f9b14e-XXXX-4f17-XXXX-2593f6eee91e, ResourceUrl = https://ConfigMgrService, AccountId = X49FC29A-ECE3-XXX-A3C1-XXXXXXF035A6E
    ```

> [!NOTE]
> Клиент должен получить сертификат подключения к рабочему месту (WPJ) при присоединении к Azure AD. Если сертификат подключения к рабочему месту не найден, клиент не пытается создать запрос с помощью коммуникационного канала службы токенов безопасности (CCM_STS). Такое поведение обусловлено тем, что клиент не может добавить к запросу маркер безопасности Azure AD. У устройства обычно нет этого сертификата, если клиент неправильно присоединен к Azure AD.
>
> Кроме того, если маркер безопасности является недопустимым, шлюз управления облачными клиентами (CMG) не перенаправляет запрос к ролям внутреннего узла. Маркер безопасности может быть недействительным, если клиент не зарегистрирован как служба управления облачными клиентами в Configuration Manager.


### <a name="2-configuration-manager-client-token-request"></a>2. Запрос маркера безопасности клиента Configuration Manager

Как только клиент получает маркер безопасности Azure AD, он запрашивает маркер безопасности клиента Configuration Manager (CCM).

В **ccmsetup.log** на виртуальной машине CMG регистрируются следующие записи:

``` Log
Getting CCM Token from STS server 'CloudManagementGateway.cloudapp.net/CCM_PROXY_MUTUALAUTH/XXXXXX037938216'
Getting CCM Token from https://CloudManagementGateway.cloudapp.net/CCM_PROXY_MUTUALAUTH/XXXXXX037938216/CCM_STS
```

#### <a name="21-cmg-gets-request"></a>2.1 Получение запроса шлюзом управления облачными клиентами

В **IIS.log** регистрируются следующие записи:

``` Log
RD0003FF74XX2 10.0.0.4 GET /CCM_STS - 443 - HTTP/1.1 python-requests/2.20.0 - - 13.95.234.44 404 0 2 1477 154 15
```

#### <a name="22-cmg-forwards-request-to-cmg-connection-point"></a>2.2 Перенаправление запроса шлюзом CMG в точку подключения шлюза управления облачными клиентами

В **CMGService.log** регистрируются следующие записи:

``` Log
RequestUri: /CCM_PROXY_SERVERAUTH/XXXXXX037938216/CCM_STS  RequestCount: 769  RequestSize: 1081595 Bytes  ResponseCount: 769     ResponseSize: 36143 Bytes  AverageElapsedTime: 3945 ms
```

#### <a name="23-cmg-connection-point-transforms-cmg-client-request-to-management-point-client-request"></a>2.3 Точка подключения шлюза управления облачными клиентами преобразует запрос клиента CMG в запрос точки управления клиентом

В **SMS_CLOUD_PROXYCONNECTOR.log** регистрируются следующие записи:

``` Log
MessageID: 3087bd34-b82c-4950-b972-e82bb0fb8385 RequestURI: https://MP.MYCORP.COM/CCM_STS EndpointName: CCM_STS ResponseHeader: HTTP/1.1 200 OK ~~ ResponseBodySize: 0 ElapsedTime: 2 ms
```

#### <a name="24-management-point-verifies-user-token-in-site-database"></a>2.4 Проверка точкой управления маркера безопасности пользователя в базе данных сайта

В **CCM_STS.log** регистрируются следующие записи:

``` Log
Validated AAD token. TokenType: Device TenantId: XXXXe388-XXXX-485c-XXXX-e8e4eb41XXXX UserId: 00000000-0000-0000-0000-000000000000 DeviceId: 0XXXXX80-77XX-4XXa-X63X-67XXXXX64bb7 OnPrem_UserSid:  OnPrem_DeviceSid:

Return token to client, token type: UDA, hierarchyId: XXXX4f9c-XXXX-46a5-XXXX-7612c324XXXX, userId: 00000000-0000-0000-0000-000000000000, deviceId: GUID:XXXXaee9-cXXc-4ccd-XXXX-f1417d81XXX
```


## <a name="content-location-request"></a>Запрос о расположении содержимого

Когда клиент получает ответ с маркером безопасности CCM, он кэширует его и использует для запроса сведений о сайте и расположении содержимого через шлюз управления облачными клиентами. В **ccmsetup.log** регистрируются приведенные ниже записи.

``` Log
Cached encrypted token for 'S-1-5-18'. Will expire at '00/99/2999 00:00:00'
Sending location request to 'CloudManagementGateway.cloudapp.net/CCM_PROXY_MUTUALAUTH/XXXXXX037938216' with payload '< Request >
Appending CCM Token to the header.
```


## <a name="client-installation"></a>Установка клиента

Содержимое клиента скачивается на устройство и начинается установка.

### <a name="communication-validation"></a>Проверка связи

- CMG проверяет маркер безопасности клиента с помощью шлюза управления облачными клиентами, точки подключения и протокола и HTTP(S) этого шлюза, а также запроса базы данных точки управления.
- Клиент проверяет сертификат управления или сертификат службы шлюза управления облачными клиентами.
- PKI для сертификата службы шлюза управления облачными клиентами: в локальном хранилище клиента должен присутствовать сертификат шлюза управления облачными клиентами корневого центра сертификации (ЦС).
- Сертификат сторонней службы шлюза управления облачными клиентами: клиенты автоматически проверяют сертификат с помощью корневого ЦС, опубликованного в Интернете.


## <a name="common-issues"></a>Распространенные проблемы

- Отсутствует корневой ЦС
- Проверка CRL включена: опубликуйте CRL в Интернете или используйте параметр **usepkicert/nocrlcheck** в командной строке.
- Не удалось найти сертификат WPJ: клиент зарегистрирован в Azure AD, но не присоединен к Azure AD.

Использование /NoCRLCheck работает только при начальной загрузке ccmsetup. Для полноценной работы клиентов необходимо опубликовать CRL в Интернете. В качестве решения можно отключить проверку CRL в настройках связи сайта клиента. В противном случае, когда служба расположения обновит параметры безопасности, связь клиентов с сервером будет прекращена.


## <a name="client-registration"></a>Регистрация клиента

![Схема рабочего процесса регистрации Azure AD](media/azure-ad-registration-workflow.png)  

### <a name="1-configuration-manager-client-request-registration"></a>1. Регистрация запроса к клиентам Configuration Manager

В файле **ClientIDManagerStartup.log** регистрируются следующие записи:

``` Log
[RegTask] - Client is not registered. Sending registration request for GUID:1XXXXXEF-5XX8-4XX3-XEDX-XXXFBFF78XXX ...
Registering client using AAD auth.
```

### <a name="2-configuration-manager-request-azure-ad-token-to-register-client"></a>2. Маркер запроса Azure AD Configuration Manager для регистрации клиента

В файле **ADALOperationProvider.log** регистрируются следующие записи:

``` Log
Getting AAD (user) token with: ClientId = f1f9b14e-XXXX-4f17-XXXX-2593f6eee91e, ResourceUrl = https://ConfigMgrService, AccountId = X49FC29A-ECE3-XXX-A3C1-XXXXXXF035A6E
Retrieved AAD token for AAD user '00000000-0000-0000-0000-000000000000'
```

#### <a name="21-configuration-manager-client-is-registered"></a>2.1 Клиент Configuration Manager зарегистрирован  

В файле **ClientIDManagerStartup.log** регистрируются следующие записи:

``` Log
[RegTask] - Client is registered. Server assigned ClientID is GUID:1XXXXXEF-5XX8-4XX3-XEDX-XXXFBFF78XXX. Approval status 3
```

> [!NOTE]  
> Во время регистрации клиента всегда выполняется проверка сертификата. Этот процесс происходит, даже если вы используете для регистрации клиента метод аутентификации Azure AD.


### <a name="3-configuration-manager-client-token-request"></a>3. Запрос маркера безопасности клиента Configuration Manager

Когда клиент будет зарегистрирован на сайте, он запросит маркер CCM. Маркер CCM шифруется для локальной системной учетной записи (S-1-5-18) и кэшируется каждые восемь часов. Через восемь часов срок действия маркера истекает, и клиент запрашивает обновление маркеров.

В файле **ClientIDManagerStartup.log** регистрируются следующие записи:

``` Log
Getting CCM Token from STS server 'MP.MYCORP.COM'
Getting CCM Token from https://MP.MYCORP.COM/CCM_STS
...
Cached encrypted token for 'S-1-5-18'. Will expire at 'XX/XX/XX XX:XX:XX'
```

#### <a name="31-cmg-gets-request"></a>3.1 Шлюз управления облачными клиентами получает запрос

В **IIS.log** регистрируются следующие записи:

``` Log
RD0003FF74XX2 10.0.0.4 GET /CCM_STS - 443 - HTTP/1.1 python-requests/2.20.0 - - 13.95.234.44 404 0 2 1477 154 15
```

#### <a name="32-cmg-forwards-request-to-cmg-connection-point"></a>3.2 Шлюз управления облачными клиентами перенаправляет запрос в точку подключения шлюза

В **CMGService.log** регистрируются следующие записи:

``` Log
RequestUri: /CCM_PROXY_SERVERAUTH/XXXXXX037938216/CCM_STS  RequestCount: 769  RequestSize: 1081595 Bytes  ResponseCount: 769     ResponseSize: 36143 Bytes  AverageElapsedTime: 3945 ms
```

#### <a name="33-cmg-connection-point-transforms-cmg-client-request-to-management-point-client-request"></a>3.3 Точка подключения шлюза управления облачными клиентами преобразует запрос клиента в запрос точки управления клиентом

В **SMS_CLOUD_PROXYCONNECTOR.log** регистрируются следующие записи:

``` Log
MessageID: 3087bd34-b82c-4950-b972-e82bb0fb8385 RequestURI: https://MP.MYCORP.COM/CCM_STS EndpointName: CCM_STS ResponseHeader: HTTP/1.1 200 OK ~~ ResponseBodySize: 0 ElapsedTime: 2 ms
```

#### <a name="34-management-point-verifies-user-token-in-site-database"></a>3.4 Точка управления проверяет маркер пользователя в базе данных сайта

В **CCM_STS.log** регистрируются следующие записи:

``` Log
Validated AAD token. TokenType: Device TenantId: XXXXe388-XXXX-485c-XXXX-e8e4eb41XXXX UserId: 00000000-0000-0000-0000-000000000000 DeviceId: 0XXXXX80-77XX-4XXa-X63X-67XXXXX64bb7 OnPrem_UserSid:  OnPrem_DeviceSid:

Return token to client, token type: UDA, hierarchyId: XXXX4f9c-XXXX-46a5-XXXX-7612c324XXXX, userId: 00000000-0000-0000-0000-000000000000, deviceId: GUID:XXXXaee9-cXXc-4ccd-XXXX-f1417d81XXX
```
