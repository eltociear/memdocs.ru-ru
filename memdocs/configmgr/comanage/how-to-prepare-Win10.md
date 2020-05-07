---
title: Совместное управление для подключенных через Интернет устройств
titleSuffix: Configuration Manager
description: Сведения о подготовке подключенных через Интернет устройств Windows 10 к совместному управлению.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 04/24/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.assetid: 101de2ba-9b4d-4890-b087-5d518a4aa624
ms.openlocfilehash: 59ca1006d8700e52b3f3fb703f8896ce9fa8b9b7
ms.sourcegitcommit: 3ff33493c3f93bf06fdc942d30958a2a4ad03529
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/24/2020
ms.locfileid: "82137921"
---
# <a name="how-to-prepare-internet-based-devices-for-co-management"></a>Подготовка подключенных через Интернет устройств к совместному управлению

В этой статье описывается второй способ настройки совместного управления, предназначенный для новых устройств, подключенных через Интернет. Он применяется, когда у вас есть новые устройства Windows 10, которые присоединяются к Azure AD и автоматически регистрируются в Intune. Вам потребуется установить клиент Configuration Manager, чтобы достичь состояния совместного управления.  

## <a name="windows-autopilot"></a>Windows Autopilot

Для новых устройств Windows 10 можно использовать службу Autopilot, чтобы настроить состояние новых устройств. Этот процесс включает присоединение устройства к Azure AD и его регистрацию в Intune.  

Дополнительные сведения см. в статье [Обзор Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot).

Чтобы настроить автоматическую регистрацию устройств в Intune при присоединении к Azure AD, ознакомьтесь со статьей  [Настройка регистрации для устройств Windows](https://docs.microsoft.com/intune/windows-enroll).  

### <a name="gather-information-from-configuration-manager"></a>Сбор информации из Configuration Manager

Используйте Configuration Manager для сбора сведений об устройствах и создания отчетов на основе полученной информации. Эти данные требуются для Intune. Эти сведения включают серийный номер устройства, идентификатор продукта Windows и идентификатор оборудования. Они используются для регистрации устройства в Intune с целью поддержки Windows Autopilot.

1. В консоли Configuration Manager перейдите к рабочей области **Мониторинг**, разверните узлы **Отчетность** и **Отчеты** и выберите узел **Оборудование — общее**.  

2. Запустите новый отчет **Сведения об устройстве для Windows Autopilot** и просмотрите результаты.  

3. В средстве просмотра отчетов щелкните значок **Экспорт** и выберите вариант **CSV (разделитель — запятая)** .  

4. После сохранения файла отправьте данные в Intune.  

Дополнительные сведения см. в разделе [Добавление устройств](https://docs.microsoft.com/intune/enrollment-autopilot#add-devices).

### <a name="autopilot-for-existing-devices"></a>Autopilot для существующих устройств
<!--1358333-->

[Windows Autopilot для существующих устройств](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430) предоставляется в Windows 10, начиная с версии 1809. Эта функция позволяет пересоздать образ и подготовить устройство Windows 7 к [режиму Windows Autopilot под управлением пользователя](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven) с помощью одной встроенной последовательности задач Configuration Manager.

Дополнительные сведения см. в статье [с описанием последовательности задач Windows Autopilot для существующих устройств](../osd/deploy-use/windows-autopilot-for-existing-devices.md).

## <a name="install-the-configuration-manager-client"></a>Установка клиента Configuration Manager

Чтобы применить второй способ для подключенных через Интернет устройств, потребуется создать приложение в Intune. Разверните это приложение на устройствах Windows 10, которые еще не являются клиентами Configuration Manager.

> [!NOTE]
> Прежде чем назначать это приложение на устройствах в Intune, убедитесь, что устройства доверяют сертификату проверки подлинности сервера шлюза CMG. Дополнительные сведения см. в разделе [Доверенный корневой сертификат шлюза CMG для клиентов](../core/clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_cmgroot). Если устройство не доверяет сертификату проверки подлинности сервера шлюза CMG, в файле ccmsetup.log на клиентском устройстве отобразится ошибка WINHTTP_CALLBACK_STATUS_FLAG_INVALID_CA.

### <a name="get-the-command-line-from-configuration-manager"></a>Получение командной строки из Configuration Manager

1. В консоли Configuration Manager перейдите в рабочую область **Администрирование**, разверните **Облачные службы** и выберите узел **Совместное управление**.  

2. Выберите объект для совместного управления и выберите на ленте элемент **Свойства**.  

3. На вкладке **Включение** скопируйте командную строку. Вставьте ее в Блокнот, чтобы сохранить для следующего процесса.  

Ниже представлен пример командной строки: `CCMSETUPCMD="CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500 SMSSITECODE=ABC"`

<!--1358215-->
Определите, какие свойства командной строки требуются для вашей среды.  

- Обязательными во всех сценариях являются следующие свойства командной строки:  
  - CCMHOSTNAME  
  - SMSSITECODE  

- Следующие свойства обязательны при использовании Azure AD для проверки подлинности клиента вместо сертификатов проверки подлинности клиента на основе PKI:  
  - AADCLIENTAPPID  
  - AADRESOURCEURI  

- Если клиент будет перемещаться обратно в интрасеть, следующее свойство является обязательным:  
  - SMSMP  

- Если вы используете собственный сертификат PKI и список отзыва не публикуется в Интернете, следующий параметр является обязательным:  
  - /noCRLCheck  

    Дополнительные сведения см. в статье [Планирование списков отзыва сертификатов](../core/plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs).

- Начиная с версии 2002, используйте следующее свойство для начальной загрузки последовательности задач сразу после регистрации клиента:
  - PROVISIONTS

    Дополнительные сведения см. в разделе [о свойствах установки клиентов — PROVISIONTS](../core/clients/deploy/about-client-installation-properties.md#provisionts).

Сайт публикует дополнительные сведения, связанные с Azure AD, в шлюзе управления облачными клиентами. Присоединенный к домену AD клиент Azure получает эти сведения из шлюза управления облачными клиентами во время процесса ccmsetup, используя тот же клиент, к которому он присоединен. Такое поведение дополнительно упрощает регистрацию устройств для совместного управления в среде с несколькими клиентами Azure AD. Нужны только два свойства ccmsetup: **CCMHOSTNAME** и **SMSSITECODE**.<!--3607731-->

> [!NOTE]
> Если вы уже развертываете клиент Configuration Manager из Intune, дополните для приложение Intune новой командной строкой и новым MSI. <!-- SCCMDocs-pr issue 3084 -->

В следующем примере показаны все эти свойства.

`CCMSETUPCMD="CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSITECODE=ABC AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver SMSMP=https://mp1.contoso.com PROVISIONTS=PRI20001"`

Дополнительные сведения см. в статье [Свойства установки клиента](../core/clients/deploy/about-client-installation-properties.md).

### <a name="create-the-app-in-intune"></a>Создание приложения в Intune

1. Перейдите к [порталу Azure](https://portal.azure.com) и откройте страницу Intune.  

2. Щелкните **Клиентские приложения** > **Приложения** > **Добавить**.  

3. В разделе **Другие** выберите **Бизнес-приложение**.  

4. Отправьте файл пакета приложения **ccmsetup.msi**. Этот файл находится на сервере сайта Configuration Manager в папке `<ConfigMgr installation directory>\bin\i386`.  

    > [!Tip]  
    > Когда вы обновляете сайт, не забудьте обновить и это приложение в Intune.  

5. После обновления приложения настройте его, используя командную строку, которую вы скопировали из Configuration Manager.  

> [!IMPORTANT]
> Если вы измените эту командную строку, соблюдайте ограничение по длине в 1024 символа. Если командная строка будет длиннее 1024 символов, установка клиента завершится сбоем.
