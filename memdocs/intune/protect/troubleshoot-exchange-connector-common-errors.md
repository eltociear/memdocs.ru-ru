---
title: Устранение распространенных неполадок с соединителем Intune с Exchange
titleSuffix: Microsoft Intune
description: Диагностика и устранение распространенных неполадок с локальным соединителем Microsoft Intune с Exchange
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/02/2019
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
ms.openlocfilehash: cb35fdc400c89c64b689f4695a48d201e50fc617
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/13/2020
ms.locfileid: "79350659"
---
# <a name="resolve-common-errors-for-the-intune-exchange-connector"></a>Устранение распространенных ошибок с соединителем Intune с Exchange

Сведения в этой статье помогут администратору службы Intune в устранении определенных неполадок и сообщений об ошибках в работе соединителя Intune с Exchange.  

## <a name="configuration-failed-and-returned-error-code-0x0000001"></a>Сбой настройки с кодом ошибки 0x0000001

**Проблема**.  
При попытке настроить соединитель Microsoft Intune с Exchange появляется следующее сообщение об ошибке:

```
   The Microsoft Intune Exchange Connector cannot connect to the Microsoft Exchange server.  
   The following Microsoft Exchange Server address could not be reached <Exchange server Name FQDN>  
   Verify that the FQDN of the exchange server address and credentials that you entered is correct and the server is running. The Microsoft Intune Exchange Connector does not support Exchange server arrays.  
   Error code: 0x0000001  
```

Эта проблема может возникать, если параметры прокси-сервера Интернета настроены неправильно.

**Решение**.  
Настройка параметров прокси-сервера:
1. Обратитесь к администратору локальной сети, чтобы убедиться, что параметры прокси-сервера настроены правильно. 
2. Используйте команду **Netsh winhttp**, чтобы настроить прокси-сервер и добавить необходимый список исключений. Пример.  

   ```
   Netsh winhttp set proxy proxy-server="http=proxy.corp.domain.com" bypass-list"34*.*;134.132.*.*;10.*.*;localhost;*.corp.domain.com;*.staging.domain.com"
   ```

## <a name="configuration-failed-and-returned-error-code-0x000000b"></a>Сбой настройки с кодом ошибки 0x000000b   

**Проблема**.  
При попытке настроить соединитель Microsoft Intune с Exchange появляется следующее сообщение об ошибке:  

```
   The Microsoft Intune Exchange Connector experienced an error:  
   CertEnroll::CX509PrivateKey::Create: The system cannot find the file specified. 0x80070002 (WIN32: 2  
   ERROR_FILE_NOT_FOUND  
   Error code: 0x000000b  
```
Эта проблема может возникать, если учетная запись, используемая для входа в Intune, не является учетной записью глобального администратора Intune.

**Решение**.  
Войдите в Intune с помощью учетной записи глобального администратора или добавьте свою учетную запись в группу глобальных администраторов. Дополнительные сведения см. в разделе [Управление доступом на основе ролей (RBAC) с помощью Microsoft Intune](../fundamentals/role-based-access-control.md).

## <a name="configuration-failed-and-returned-error-code-0x0000006"></a>Сбой настройки с кодом ошибки 0x0000006

**Проблема**.  
При попытке настроить соединитель Microsoft Intune с Exchange появляется следующее сообщение об ошибке:  

```  
   The Microsoft Intune Exchange Connector cannot connect to Microsoft Intune  
   Verify that you are connected to the Internet, check the Microsoft Intune Service Status, and try to connect again.  
   Error code: 0x00000006  
```  
Эта ошибка может возникать, если для подключения к Интернету используется прокси-сервер, который блокирует трафик к службе Intune. Чтобы определить, используется ли прокси-сервер, выберите **Панель управления** > **Свойства браузера**, перейдите на вкладку **Подключение** и нажмите **Параметры сети**.

**Решение**.  

- **Вариант 1** — удалите параметры прокси-сервера, чтобы разрешить компьютеру подключаться к Интернету, минуя прокси-сервер.  

- **Вариант 2** — настройте прокси-сервер, чтобы разрешить взаимодействие со службой Intune, как описано в статье [Требования к соединителю Exchange для Intune](exchange-connector-install.md#intune-exchange-connector-requirements).



## <a name="event-7000-or-7041-microsoft-intune-exchange-connector-service-wont-start"></a>Событие 7000 или 7041: не удается запустить службу соединителя Microsoft Intune с Exchange.

**Проблема**.  
Устройство iOS не регистрируется в Intune и создает одно из следующих сообщений об ошибке:  

```  
   Log Name:      System
   Source:            Service Control Manager
   Date:               <time>
   Task Category: None
   Level:               Error
   Keywords:        Classic
   User:                N/A
   Computer:      <computer>
   Description:
   The Microsoft Intune Exchange Connector Service service failed to start because of the following error:  
   The service did not start because of a logon failure.
```  

```  
   Log Name:      System
   Source:            Service Control Manager
   Date:               <time>
   Event ID:          7041
   Task Category: None
   Level:               Error   
   Keywords:        Classic
   User:                N/A
   Computer:       <computer>
   Description:
   The WIEC service was unable to log on as .\WIEC_USER with the currently configured password because of the following error:
   Logon failure: the user has not been granted the requested logon type at this computer.
   Service: WIEC
   Domain and account: .\WIEC_USER
   This service account does not have the required user right "Log on as a service."  
```
Эта проблема может возникать, если в локальной политике учетной записи **WIEC_User** не предоставлено право **Вход в качестве службы**.

**Решение**.  
На компьютере, на котором работает соединитель Intune с Exchange, назначьте учетной записи службы **WIEC_User** право **Вход в качестве службы**. Если компьютер является узлом кластера, обязательно назначьте учетной записи службы кластера право *Вход в качестве службы* на всех узлах кластера.  

Чтобы назначить учетной записи службы **WIEC_User** на компьютере право **Вход в качестве службы**, выполните следующие действия.

1. Войдите в систему с учетной записью администратора или члена группы "Администраторы".
2. Выполните **secpol.msc**, чтобы открыть локальную политику безопасности.
3. Выберите **Настройки безопасности** > **Локальные политики**, а затем выберите **Назначение прав пользователя**.
4. На правой панели дважды щелкните **Вход в качестве службы**.
5. Выберите **Добавить пользователя или группу**, добавьте в политику учетную запись **WIEC_USER**, а затем последовательно нажмите кнопку **ОК** два раза.

Если учетной записи **WIEC_User** уже было назначено право **Вход в качестве службы**, но впоследствии оно было удалено, обратитесь к администратору домена, чтобы определить, не перезаписывает ли его параметр групповой политики.  

## <a name="next-steps"></a>Дальнейшие шаги  

Сведения в следующих статьях помогут устранить определенные ошибки.
- [Устранение распространенных проблем с соединителем Intune с Exchange](troubleshoot-exchange-connector-common-problems.md).git 

Обратитесь за помощью в службу поддержки или в сообщество Intune.
- Обратитесь к разделу [Поддержка](../fundamentals/get-support.md), чтобы использовать консоль Intune для устранения неполадок или для обращения в службу поддержки Майкрософт. 
- Опубликуйте свой вопрос на форумах [Microsoft Intune](https://social.technet.microsoft.com/Forums/en-US/home?forum=microsoftintuneprod).  
