---
title: Technical Preview 1709
titleSuffix: Configuration Manager
description: Сведения о функциях, доступных в Technical Preview для Configuration Manager, версия 1709.
ms.date: 09/28/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a3ef6bdc-a204-4c4c-a02f-2bd03f35183e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: bedb515c8446e13189fb84644bc0ce7563cc1574
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078776"
---
# <a name="capabilities-in-technical-preview-1709-for-configuration-manager"></a>Возможности в Technical Preview 1709 для Configuration Manager

*Область применения: Configuration Manager (ветвь Technical Preview)*

В этой статье содержатся сведения о функциях, доступных в технической версии 1709 для Configuration Manager. Этот выпуск можно установить для обновления и добавления новых возможностей в ознакомительную техническую версию сайта Configuration Manager. Перед установкой этой версии прочтите статью [Technical Preview для Configuration Manager](../../core/get-started/technical-preview.md). В ней приведены общие требования и ограничения на использование ознакомительной технической версии, а также сведения о том, как выполнять обновления и оставлять отзывы о функциях этого выпуска.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Известные проблемы в этой версии Technical Preview:**
- **Если сервер сайта находится в пассивном режиме, происходит сбой обновления до предварительной версии 1709**. Если вы запустили предварительную версию 1706, 1707 или 1708 и [сервер первичного сайта находится в пассивном режиме](capabilities-in-technical-preview-1706.md#site-server-role-high-availability), удалите сервер сайта в пассивном режиме, чтобы обновить сайт предварительной версии до версии 1709. Вы можете повторно установить сервер сайта в пассивном режиме, после того как на сайте заработает версия 1709.

  Удаление сервера сайта в пассивном режиме
  1. Откройте консоль и выберите **Администрирование** > **Обзор** > **Конфигурация сайта** > **Серверы и роли системы сайта**. Затем выберите сервер сайта в пассивном режиме.
  2. На панели **Системные роли сайта** щелкните правой кнопкой мыши роль **Сервер сайта** и нажмите кнопку **Удалить роль**.
  3. Щелкните правой кнопкой мыши сервер сайта в пассивном режиме, а затем выберите **Удалить**.
  4. Удалив сервер сайта на активном сервере первичного сайта, перезапустите службу **CONFIGURATION_MANAGER_UPDATE**.


**Ниже перечислены новые возможности, доступные в этой версии.**  

## <a name="improved-vpn-profile-experience-in-configuration-manager-console"></a>Улучшенный интерфейс профиля VPN в консоли Configuration Manager
<!-- 1313282 -->
В этом выпуске мы обновили мастер профилей VPN и страницы свойств для отображения параметров для выбранной платформы. В частности, внесены следующие изменения.

- Каждая платформа имеет собственный рабочий процесс. Это значит, что новые профили VPN содержат только параметры, поддерживаемые платформой.
- Теперь страницы **Поддерживаемые платформы** отображаются после страницы **Общие**.  Платформа выбирается перед заданием значений свойств.
- Если в качестве платформы выбраны **Android**, **Android for Work** или **Windows Phone 8.1**, страница **Поддерживаемые платформы** не требуется и не отображается.
- Рабочий процесс на основе клиента Configuration Manager объединен с рабочими процессами Windows 10 на основе клиента гибридного развертывания MDM. Они поддерживают те же параметры.
- Каждый рабочий процесс платформы включает в себя только параметры для этого рабочего процесса.  Например, рабочий процесс Android содержит параметры, соответствующие Android. Параметры, соответствующие iOS или Windows 10 Mobile больше не отображаются в рабочем процессе Android.
- Параметры, управляемые Configuration Manager, для устройств Windows 8.1 имеют четкое обозначение.
- Страница "Автоподключение VPN" устарела и была удалена.

Эти изменения применяются к новым профилям VPN.  

Чтобы свести к минимуму риск совместимости, существующие профили VPN оставлены без изменений.  При редактировании существующего профиля параметры отображаются так же, как и при создании профиля.  

### <a name="try-it-out"></a>Попробуйте!

Создайте профиль VPN с помощью обычного процесса. Обратите внимание, что изменилась первая страница в мастере параметров профилей VPN.

1. Последовательно выберите пункты **Активы и соответствие** > **Обзор** > **Параметры соответствия** > **Доступ к ресурсам компании**  > **Профили VPN** и выберите **Создать профиль VPN**.
2. Введите имя на странице **Общие** и в разделе **Укажите тип профиля VPN, который требуется создать** выберите один из следующих вариантов.

    - быть под управлением ОС Windows 10;  
    - Windows 8.1  
    - Windows Phone 8.1  
    - iOS и macOS  
    - Android  
    - Android for Work  

3. При выборе **Windows 8.1** вы также можете **создать профиль** или **импортировать данные из файла**.
4. Завершите работу мастера, чтобы закончить создание профиля.

Выбирая различные платформы, обратите внимание, что отображаются только параметры, относящиеся к указываемой платформе.

## <a name="co-management-for-windows-10-devices"></a>Совместное управление для устройств Windows 10    
<!-- 1350871 -->
Многие клиенты хотят управлять устройствами Windows 10 таким же образом, как и мобильными устройствами с помощью упрощенного, экономичного облачного решения. Но переход с традиционной системы управления на современную может быть сложной задачей. Начиная с Windows 10 версии 1607 (также называется юбилейным обновлением) устройства с Windows 10 можно одновременно присоединить к Active Directory (AD) в локальной среде и Azure AD в облачной среде (гибридная служба Azure AD). Это улучшение открывает новые возможности для совместного управления, позволяя работать с устройствами Windows 10 одновременно при помощи Configuration Manager и Intune. Решение обеспечивает поэтапный переход с традиционной системы управления на современную. 

### <a name="prerequisites"></a>Предварительные условия
Перед включением совместного управления необходимо выполнить следующие предварительные требования. Существуют общие предварительные требования и различные условия для существующих клиентов Configuration Manager и устройств, которые не являются клиентами.

### <a name="known-issues"></a>Известные проблемы
Созданную политику совместного управления невозможно изменить. Чтобы изменить политику, удалите ее и создайте ее повторно с необходимыми параметрами. 

#### <a name="general-prerequisites"></a>Основные обязательные требования
Ниже приведены общие требования для включения совместного управления.  

- Technical Preview для System Center Configuration Manager, версия 1709
- Azure AD 
- Лицензии EMS или Intune для всех пользователей
- Подписка Intune (выберите **Intune** в качестве центра MDM)

   > [!Note]  
   > Совместное управление невозможно включить при наличии гибридной среды MDM (службы Intune, интегрированной с Configuration Manager).

#### <a name="additional-prerequisites-for-existing-configuration-manager-clients"></a>Дополнительные требования для существующих клиентов Configuration Manager
- Windows 10, версия 1709 (Fall Creators Update) и более поздние версии
- Присоединение к гибридному развертыванию Azure AD (присоединение к AD и Azure AD)

#### <a name="additional-prerequisites-for-new-windows-10-devices"></a>Дополнительные требования для новых устройств Windows 10
- Windows 10, версия 1709 (Fall Creators Update) и более поздние версии
- [Шлюз управления облачными клиентами](../clients/manage/manage-clients-internet.md#cloud-management-gateway) в Configuration Manager

### <a name="workloads-you-can-switch-to-intune"></a>Рабочие нагрузки, которые можно перенести в Intune
После включения совместного управления Configuration Manager продолжит управлять всеми рабочими нагрузками. Когда все будет готово, вы можете предоставить Intune возможность управления доступными рабочими нагрузками. В этом выпуске Intune поддерживает управление следующими рабочими нагрузками.   

#### <a name="compliance-policies"></a>Политики соответствия требованиям
Политики соответствия требованиям определяют правила и параметры, которым должно соответствовать устройство, чтобы политики условного доступа расценивали его как совместимое. Политики соответствия также можно использовать для отслеживания и устранения проблем совместимости у устройств, независимо от условного доступа.

#### <a name="windows-update-for-business-policies"></a>Политики Центра обновления Windows для бизнеса
Политики Цента обновления Windows для бизнеса позволяют настраивать политики отсрочки обновлений компонентов Windows 10 или исправлений для устройств Windows 10, управляемых непосредственно с помощью Центра обновления Windows для бизнеса. Дополнительные сведения см. в статье [Настройка политик отсрочки Центра обновления Windows для бизнеса](https://docs.microsoft.com/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10#configure-windows-update-for-business-deferral-policies).  

### <a name="remote-actions-available-in-intune-on-azure-for-co-managed-devices"></a>Удаленные действия, доступные в Intune в Azure для совместно управляемых устройств
Если устройство Windows 10 включено для совместного управления, вам доступны следующие удаленные действия из Intune в Azure.  
- [Сброс параметров](https://docs.microsoft.com/intune/devices-wipe#wipe)
- [Выборочная очистка](https://docs.microsoft.com/intune/apps-selective-wipe)
- [Удаление устройств](https://docs.microsoft.com/intune/devices-wipe#delete-devices-from-the-azure-active-directory-portal)
- [Перезапуск устройства](https://docs.microsoft.com/intune/device-restart)
- [Новый запуск](https://docs.microsoft.com/intune/device-fresh-start)

### <a name="prepare-intune-for-co-management"></a>Подготовка Intune для совместного управления
Перед переключением рабочих нагрузок с Configuration Manager на Intune создайте профили и политики, необходимые в Intune для продолжения защиты устройств.
В Intune можно создать объекты на основе существующих объектов в Configuration Manager. Или, если текущая стратегия основана на устаревших или традиционных принципах управления, может потребоваться пересмотреть, какие политики и профили нужны для современной системы управления. Следующие ресурсы помогут создать политики и профили.    
<!-- - [Device compliance policies](https://docs.microsoft.com/intune/compliance-policy-create-windows)  -->
- [Политики Центра обновления Windows для бизнеса](https://docs.microsoft.com/intune/windows-update-for-business-configure)  
- [Профили конфигурации устройств](https://docs.microsoft.com/intune/device-profile-create)  

### <a name="architectural-overview-for-co-management"></a>Обзор архитектуры совместного управления
На следующей схеме представлен обзор архитектуры совместного управления и его соответствие существующим инфраструктурам Configuration Manager и Intune.

![Архитектурная схема совместного управления](./media/co-management-arch-cm1709tp.svg)

### <a name="scenarios-to-enable-co-management"></a>Сценарии включения совместного управления  
Совместное управление можно включить для устройств Windows 10, зарегистрированных в Microsoft Intune, и существующих клиентов Windows 10 Configuration Manager. В итоге устройства Windows 10 будут одновременно управляться с помощью Configuration Manager и Intune, а также входить в состав AD и Azure AD.  

#### <a name="devices-enrolled-in-intune"></a>Устройства, зарегистрированные в Intune  
Если устройства Windows 10 зарегистрированы в Intune, вы установите клиент Configuration Manager на устройства (с помощью определенного аргумента командной строки), чтобы подготовить клиенты для совместного управления. Затем включите совместное управление из консоли Configuration Manager, чтобы начать перемещение конкретных рабочих нагрузок в Intune для конкретных устройств Windows 10.  

Для устройств Windows 10, которые еще не зарегистрированы в Intune, можно использовать автоматическую регистрацию в Azure. Для новых устройств Windows 10 можно использовать Windows AutoPilot, чтобы настроить запуск при первом включении, предполагающий автоматическую регистрацию устройств в Intune.  

#### <a name="configuration-manager-clients"></a>Клиенты Configuration Manager
При наличии устройств Windows 10, являющихся клиентами Configuration Manager, можно зарегистрировать эти устройства и включить совместное управление из консоли Configuration Manager. Configuration Manager запускает автоматическую регистрацию в Intune в зависимости от сведений клиента Azure AD.  

### <a name="prepare-windows-10-devices-for-co-management"></a>Подготовка устройств Windows 10 для совместного управления
Можно включить совместное управление на устройствах Windows 10, присоединенных к AD и Azure AD и зарегистрированных в Intune, и клиенте в Configuration Manager. На новых устройствах Windows 10 и устройствах, которые уже зарегистрированы в Intune, установите клиент Configuration Manager, после чего они будут поддерживать совместное управление. Устройства Windows 10, которые уже являются клиентами Configuration Manager, можно зарегистрировать в Intune и включить совместное управление в консоли Configuration Manager.

#### <a name="command-line-to-install-configuration-manager-client"></a>Командная строка для установки клиента Configuration Manager
В Intune создайте приложение для устройств Windows 10 устройств, которые еще не являются клиентами Configuration Manager. При создании приложения в следующих разделах используйте приведенную ниже командную строку:

ccmsetup.msi CCMSETUPCMD="/mp:&#60;*URL-адрес конечной точки для взаимной проверки подлинности шлюза управления облачными клиентами*&#62;/ CCMHOSTNAME=&#60;*URL-адрес конечной точки для взаимной проверки подлинности шлюза управления облачными клиентами*&#62; SMSSiteCode=&#60;*Код сайта*&#62; SMSMP=https:&#47;/&#60;*Полное доменное имя точки управления*&#62; AADTENANTID=&#60;*ИД клиента AAD*&#62; AADTENANTNAME=&#60;*Имя клиента*&#62; AADCLIENTAPPID=&#60;*ИД приложения сервера для интеграции AAD*&#62; AADRESOURCEURI=https:&#47;/&#60;*ИД ресурса*&#62;"

Например, если у вас есть следующие значения.

- **URL-адрес конечной точки для взаимной проверки подлинности шлюза управления облачными клиентами**: https:/&#47;contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100    

   >[!Note]    
   >Используйте значение **MutualAuthPath** в представлении SQL **vProxy_Roles** в качестве значения **URL-адреса конечной точки для взаимной проверки подлинности шлюза управления облачными клиентами**.

- **Полное доменное имя точки управления (MP)** : sccmmp.corp.contoso.com    
- **Код сайта**: PS1    
- **Идентификатор клиента Azure AD**: 72F988BF-86F1-41AF-91AB-2D7CD011XXXX    
- **Имя клиента Azure AD**: contoso    
- **ИД приложения клиента Azure AD**: bef323b3-042f-41a6-907a-f9faf0d1XXXX     
- **Универсальный код ресурса (URI) идентификатора ресурса AAD**: ConfigMgrServer    

  > [!Note]    
  > Используйте значение **IdentifierUri** в представлении SQL **vSMS_AAD_Application_Ex** в качестве значения **URI ИД ресурса AAD**.

Можно использовать следующую командную строку:

ccmsetup.msi CCMSETUPCMD="/mp:https:/&#47;contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100    CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100 SMSSiteCode=PS1 SMSMP=https:/&#47;sccmmp.corp.contoso.com AADTENANTID=72F988BF-86F1-41AF-91AB-2D7CD011XXXX AADTENANTNAME=contoso  AADCLIENTAPPID=bef323b3-042f-41a6-907a-f9faf0d1XXXX AADRESOURCEURI=https:/&#47;ConfigMgrServer"

> [!Tip]
>Параметры командной строки для веб-сайта можно найти, выполнив следующие действия.     
> 1. В консоли Configuration Manager последовательно выберите **Администрирование** > **Обзор** > **Облачные службы** > **Совместное управление**.  
> 2. На вкладке "Главная" в группе "Управление" выберите команду **Настроить совместное управление**, чтобы открыть мастер подключения совместного управления.    
> 3. На странице "Подписка" щелкните **Войти**, войдите в свой клиент Intune и нажмите кнопку **Далее**.    
> 4. На странице "Включение" в разделе **Устройства, зарегистрированные в Intune** щелкните **Копировать**, чтобы скопировать командную строку в буфер обмена, а затем сохраните командную строку для использования в процедуре создания приложения.  
> 5. Чтобы завершить работу мастера, нажмите кнопку **Отмена**.

#### <a name="new-windows-10-devices"></a>Новые устройства Windows 10
На новых устройствах Windows 10 используйте службу Autopilot, чтобы настроить запуск при первом включении, предполагающий присоединение устройства к AD и Azure AD, а также регистрацию устройства в Intune. Затем создайте приложение в Intune для развертывания клиента Configuration Manager.  
1. Включите AutoPilot для новых устройств Windows 10. Дополнительные сведения см. в статье [Обзор AutoPilot](https://docs.microsoft.com/windows/deployment/windows-10-auto-pilot).  
2. Настройте автоматическую регистрацию в Azure AD для автоматической регистрации устройств в Intune. Дополнительные сведения см. в статье  [Регистрация устройств Windows](https://docs.microsoft.com/intune/windows-enroll).
3. В Intune создайте приложение с пакетом клиента Configuration Manager и разверните приложения на устройствах Windows 10, для которых нужно включить совместное управление. При выполнении действий по [установке клиентов из Интернета с помощью Azure AD](https://docs.microsoft.com/sccm/core/clients/deploy/deploy-clients-cmg-azure) используйте [командную строку для установки клиента Configuration Manager](#command-line-to-install-configuration-manager-client).   

#### <a name="windows-10-devices-not-enrolled-in-intune-or-a-configuration-manager-client"></a>Устройств Windows 10, незарегистрированные в Intune или имеющие клиент Configuration Manager
Чтобы зарегистрировать в Intune устройства Windows 10, которые не зарегистрированы в Intune или имеют клиент Configuration Manager, можно использовать автоматическую регистрацию. Затем создайте приложение в Intune для развертывания клиента Configuration Manager.
1. Настройте автоматическую регистрацию в Azure AD для автоматической регистрации устройств в Intune. Дополнительные сведения см. в статье  [Регистрация устройств Windows](https://docs.microsoft.com/intune/windows-enroll).  
2. В Intune создайте приложение с пакетом клиента Configuration Manager и разверните приложения на устройствах Windows 10, для которых нужно включить совместное управление. При выполнении действий по [установке клиентов из Интернета с помощью Azure AD](https://docs.microsoft.com/sccm/core/clients/deploy/deploy-clients-cmg-azure) используйте [командную строку для установки клиента Configuration Manager](#command-line-to-install-configuration-manager-client).

#### <a name="windows-10-devices-enrolled-in-intune"></a>Устройства Windows 10, зарегистрированные в Intune
Для устройств Windows 10, которые уже зарегистрированы в Intune, создайте приложение в Intune для развертывания клиента Configuration Manager. При выполнении действий по [установке клиентов из Интернета с помощью Azure AD](https://docs.microsoft.com/sccm/core/clients/deploy/deploy-clients-cmg-azure) используйте [командную строку для установки клиента Configuration Manager](#command-line-to-install-configuration-manager-client).  

### <a name="switch-configuration-manager-workloads-to-intune"></a>Переключение рабочих нагрузок Configuration Manager на Intune
В предыдущем разделе вы подготовили устройства Windows 10 для совместного управления. Теперь эти устройства присоединены к AD и Azure AD, зарегистрированы в Intune и имеют клиент Configuration Manager. Скорее всего, у вас останутся устройства Windows 10, присоединенные к AD и имеющие клиент Configuration Manager, но не присоединенные к Azure AD или не зарегистрированные в Intune. Следующая процедура предназначена для включения совместного управления, подготовки оставшихся устройствами Windows 10 (клиентов Configuration Manager без регистрации в Intune) для совместного управления и для переключения определенных рабочих нагрузок Configuration Manager на Intune.

1. В консоли Configuration Manager последовательно выберите **Администрирование** > **Обзор** > **Облачные службы** > **Совместное управление**.    
2. На вкладке "Главная" в группе "Управление" выберите команду **Настроить совместное управление**, чтобы открыть мастер подключения совместного управления.    
3. На странице "Подписка" щелкните **Войти**, войдите в свой клиент Intune и нажмите кнопку **Далее**.   
4. На странице "Промежуточное хранение" укажите следующие сведения, а затем нажмите кнопку **Далее**.
    - **Пилотная группа**. Пилотная группа содержит одну или несколько коллекций для выбора. Используйте эту группу в ходе поэтапного развертывания совместного управления. Можно начать с небольшой тестовой коллекции и затем по мере развертывания совместного управления для нескольких пользователей и устройств добавлять в пилотную группы дополнительные коллекции. Коллекции в пилотной группе можно изменить в любое время в окне свойств совместного управления.
    - **Production**: При выборе этого параметра все поддерживаемые устройства Windows 10 включаются для совместного управления. Настройте **Группу исключения** с одной коллекцией или несколькими. Устройства, являющиеся членами любой коллекции в этой группе, исключаются из совместного управления. 
5. На странице "Включение" выберите **Пилотный проект** или **Все** (в зависимости от параметров, настроенных на странице промежуточного этапа), чтобы включить автоматическую регистрацию в Intune, и нажмите кнопку **Далее**. При выборе варианта **Пилотный проект** автоматически регистрируются в Intune только клиенты Configuration Manager, являющихся членами пилотной группы. Это позволяет включить совместное управление в подмножестве клиентов для первоначального тестирования совместного управления и развертывания совместного управления с помощью поэтапного подхода. 
6. На странице "Рабочие нагрузки" выберите, следует ли управлять рабочими нагрузками Configuration Manager в Intune, а затем нажмите кнопку **Далее**. С помощью ползунков укажите, следует ли переключать рабочую нагрузку в пилотную группу или для всех клиентов Windows 10 (в зависимости от параметров, настроенных на странице промежуточного этапа). 
7. Чтобы включить совместное управление, завершите работу мастера.  

<!--### Modify your co-management settings
After you enable co-management using the wizard, you can modify your target group and change the workloads that are managed by Configuration Manager and Intune.  
- In the Configuration Manager console, go to **Administration** > **Overview** > **Cloud Services** > **Co-management**.  
Select the co-management object, and then on the Home tab, click **Properties**. -->   

<!--### Monitor co-management
After you have enabled co-management, you can monitor which devices are managed by Configuration Manager and which are managed by Intune. You can also see which Configuration Manager workloads are managed by which product.-->

## <a name="see-also"></a>См. также
Сведения об установке или обновлении ветви Technical Preview см. в статье [Technical Preview для Configuration Manager](technical-preview.md). 
