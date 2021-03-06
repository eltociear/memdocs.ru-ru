---
title: Настройка обнаружения
titleSuffix: Configuration Manager
description: Настройте методы обнаружения, чтобы найти ресурсы для управления из сети, Active Directory и Azure Active Directory.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 49505eb1-d44d-4121-8712-e0f3d8b15bf5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3bd03cb15ae1633d8ddfc8c2f26a741d2679b083
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704752"
---
# <a name="configure-discovery-methods-for-configuration-manager"></a>Настройка методов обнаружения для Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Настройте методы обнаружения, чтобы найти ресурсы для управления из сети, Active Directory и Azure Active Directory (Azure AD). Сначала включите, а затем настройте каждый метод, используемый для поиска в среде. Процесс включения и отключения метода аналогичен. Единственное исключение — методы Heartbeat-обнаружения и обнаружения сервера.  

- По умолчанию **Heartbeat-обнаружение** уже включено во время установки первичного сайта Configuration Manager. Оно настраивается для запуска по основному расписанию. Метод Heartbeat-обнаружения должен быть постоянно включен. Он обеспечивает актуальность записей данных обнаружения (DDR) для устройств. Дополнительные сведения о Heartbeat-обнаружении см. в [этом разделе](about-discovery-methods.md#bkmk_aboutHeartbeat).  

- **Обнаружение сервера** — это метод автоматического обнаружения. Он находит компьютеры, которые используются в качестве системы сайта. Вы не можете настроить или отключить этот метод.  


## <a name="active-directory-forest-discovery"></a><a name="BKMK_ConfigADForestDisc"></a> Обнаружение в лесах Active Directory  

Чтобы завершить настройку метода обнаружения в лесах Active Directory, необходимо настроить параметры расположения в консоли Configuration Manager.  

- В узле **Методы обнаружения** нужно:

  - включить этот метод обнаружения;  

  - задать расписание опроса;  

  - выбрать, будут ли в процессе обнаружения автоматически создаваться границы для найденных сайтов и подсетей Active Directory;  

- В узле **Леса Active Directory** нужно:

  - добавить леса, которые требуется найти;  

  - включить обнаружение сайтов и подсетей Active Directory в этом лесу;  

  - настроить параметры, позволяющие сайтам Configuration Manager публиковать данные сайта в лесу;  

  - назначить каждому лесу учетную запись, используемую в качестве учетной записи леса Active Directory.  

Используйте приведенные ниже действия, чтобы включить обнаружение в лесах Active Directory и настроить отдельные леса, используемые с этим методом.  

### <a name="configure-active-directory-forest-discovery"></a>Настройка обнаружения в лесах Active Directory  

1. В рабочей области **Администрирование** консоли Configuration Manager разверните узел **Конфигурация иерархии** и щелкните узел **Методы обнаружения**.  

2. Выберите метод "Обнаружение в лесах Active Directory" для сайта, на котором нужно настроить обнаружение.  

3. На вкладке **Рабочий стол** на ленте выберите команду **Свойства**.  

4. На панели свойств **Общие** настройте следующие параметры:  

    - Включите метод обнаружения.

    - Укажите параметры для границ сайта для обнаруженных расположений.  

    - Задайте расписание выполнения обнаружения.  

5. Нажмите кнопку **ОК** , чтобы сохранить настройки.  

### <a name="configure-a-forest-for-active-directory-forest-discovery"></a>Настройка леса для метода обнаружения в лесах Active Directory  

1. В рабочей области **Администрирование** разверните узел **Конфигурация иерархии**, а затем выберите узел **Леса Active Directory**. Если метод обнаружения в лесах Active Directory был запущен ранее, все обнаруженные леса будут отображены в области результатов. При использовании этого метода обнаружения обнаруживается локальный лес и все надежные леса. Добавьте вручную ненадежные леса.  

    - Чтобы настроить ранее обнаруженный лес, выберите его в области результатов. На ленте выберите **Свойства**, чтобы открыть свойства леса.

    - Чтобы настроить новый лес, который отсутствует в списке, на вкладке ленты **Главная** в группе **Создать** выберите **Добавить лес**. Это действие открывает диалоговое окно **Add Forests** (Добавление лесов).

2. На вкладке **Общие** завершите настройку леса, который необходимо обнаружить, и укажите **учетную запись леса Active Directory**. Дополнительные сведения об этой учетной записи см. в разделе [Accounts](../../../plan-design/hierarchy/accounts.md#active-directory-forest-account) (Учетные записи).  

    > [!NOTE]  
    > Для обнаружения и публикации в лесах, не имеющих доверия, методу обнаружения в лесах Active Directory требуется глобальная учетная запись. Если учетная запись компьютера сервера сайта не используется, можно выбрать только глобальную учетную запись.  

3. Если вы планируете разрешить сайтам публиковать данные сайта в этом лесу, откройте вкладку **Публикация** и завершите настройку публикации в этом лесу.  

    > [!NOTE]  
    > При включении публикации данных сайта в лес расширьте схему Active Directory этого леса для Configuration Manager. Учетная запись леса Active Directory должна иметь разрешения на полный доступ к контейнеру System в этом лесу.  

4. Нажмите кнопку **ОК** , чтобы сохранить настройки.  


## <a name="active-directory-discovery-for-computers-users-or-groups"></a><a name="BKMK_ConfigADDiscGeneral"></a> Обнаружение Active Directory для компьютеров, пользователей или групп  

Для настройки обнаружения компьютеров, пользователей или групп начните с общих шагов, описанных далее.

1. В рабочей области **Администрирование** консоли Configuration Manager разверните узел **Конфигурация иерархии** и щелкните узел **Методы обнаружения**.  

2. Выберите метод обнаружения для сайта, на котором нужно настроить обнаружение.  

3. На вкладке **Рабочий стол** на ленте выберите команду **Свойства**.  

4. На вкладке свойств **Общие** установите флажок, чтобы разрешить обнаружение. Или настройте обнаружение сейчас, а включите позже.  

Затем используйте информацию из следующих разделов, чтобы настроить конкретные методы обнаружения.  

- [Обнаружение групп Active Directory](#bkmk_config-adgd)  

- [Обнаружение систем Active Directory](#bkmk_config-adgd)  

- [Обнаружение пользователей Active Directory](#bkmk_config-adud)  

> [!NOTE]  
> Сведения в этом разделе не применяются к методу обнаружения в лесах Active Directory.  

Хотя все эти методы обнаружения не зависят друг от друга, у них есть общие параметры. Дополнительные сведения об этих параметрах конфигурации см. в статье [Общие параметры для обнаружения групп, систем и пользователей](about-discovery-methods.md#bkmk_shared).  

> [!WARNING]  
> Опрос каждого из этих методов обнаружения Active Directory может существенно увеличить нагрузку на сеть. Поэтому выполнение каждого метода обнаружения рекомендуется запланировать на такие периоды, когда этот сетевой трафик не сможет оказать негативное влияние на использование сети.  

### <a name="configure-active-directory-group-discovery"></a><a name="bkmk_config-adgd"></a> Настройка обнаружения групп Active Directory  

1. На вкладке **Общие** окна свойств обнаружения групп Active Directory выберите **Добавить**, чтобы настроить область обнаружения. Выберите **Группы** или **Расположение**. Затем выполните следующие настройки в диалоговых окнах **Добавить группы** или **Добавить расположение Active Directory**.  

    1. Укажите **Имя** для этой области обнаружения.  

    2. Укажите **Домен Active Directory** или **Расположение** для поиска.  

        - Если выбран параметр **Группы**, укажите одну или несколько групп Active Directory, которые требуется обнаружить.  

        - Если выбран параметр **Расположение**, в качестве расположения для поиска укажите контейнер Active Directory. Для этого расположения можно также включить рекурсивный поиск дочерних контейнеров Active Directory.  

    3. Укажите **учетную запись обнаружения групп Active Directory**, которая будет использоваться сайтом для поиска в этой области обнаружения. Дополнительные сведения см. в разделе об [учетных записях](../../../plan-design/hierarchy/accounts.md#active-directory-group-discovery-account).  

    4. Чтобы сохранить параметры области обнаружения, нажмите **OK**.  

2. Повторите предыдущие шаги для каждой дополнительной области обнаружения, которую требуется определить.  

3. На вкладке **Расписание опроса** настройте расписание опроса полного обнаружения и обнаружения изменений.

4. На вкладке **Параметры** можно настроить параметры фильтрации или удаления устаревших записей компьютеров из обнаружения. Также можно настроить обнаружение членства в группах распространения.  

    > [!NOTE]  
    > По умолчанию метод обнаружения групп Active Directory находит только членство в группах безопасности.  

5. Нажмите кнопку **ОК** , чтобы сохранить настройки.  

### <a name="configure-active-directory-system-discovery"></a><a name="bkmk_config-adsd"></a> Настройка обнаружения систем Active Directory  

1. На вкладке **Общие** окна свойств обнаружения систем Active Directory выберите значок **Создать**![значок Создать](media/Disc_new_Icon.gif), чтобы указать новый контейнер Active Directory. В диалоговом окне **Контейнер Active Directory** выполните следующие настройки:  

    1. Введите или выберите **путь**. Это значение является допустимым путем LDAP в контейнере или подразделении (OU). Сайт запрашивает этот путь к ресурсам. Например, `LDAP://CN=Computers,DC=contoso,DC=com`  

    2. Укажите параметры, изменяющие способ поиска.  

        - **Обнаруживать объекты в группах Active Directory**: сайт также учитывает членство в группах по этому пути.  

        - **Выполнять рекурсивный поиск в дочерних контейнерах Active Directory**: если этот параметр включен, сайт выполняет поиск любых дополнительных контейнеров или подразделений по указанному выше пути. Если вы отключите этот параметр, сайт будет искать ресурсы только по определенному пути.  

          В версии 1806 и выше выберите подконтейнеры для исключения из этого рекурсивного поиска. Этот параметр позволяет сократить число обнаруженных объектов. Выберите **Добавить**, чтобы выбрать контейнеры в указанном выше пути. В диалоговом окне "Выберите новый контейнер" выберите дочерний контейнер для исключения. Нажмите **OK**, чтобы закрыть диалоговое окно "Выберите новый контейнер".<!--1358143-->

          > [!Tip]  
          > Список контейнеров Active Directory в окне свойств обнаружения системы Active Directory содержит столбец **Имеет исключения**. При выборе контейнеров для исключения это значение приравнивается к **Да**.  

    3. Для каждого расположения укажите учетную запись, которая будет использоваться в качестве **учетной записи обнаружения Active Directory**. Дополнительные сведения см. в разделе об [учетных записях](../../../plan-design/hierarchy/accounts.md#active-directory-system-discovery-account).  

        > [!TIP]  
        > Для каждого заданного расположения можно настроить ряд параметров обнаружения и уникальную учетную запись обнаружения Active Directory.  

    4. Нажмите **OK**, чтобы сохранить конфигурацию контейнера Active Directory.  

2. На вкладке **Расписание опроса** настройте расписание опроса полного обнаружения и обнаружения изменений.  

3. На вкладке **Атрибуты Active Directory** настройте дополнительные атрибуты для компьютеров, которые нужно найти. На этой вкладке также указаны атрибуты объектов по умолчанию.  

    > [!Tip]  
    > Например, ваша организация использует атрибут **Description** для учетной записи компьютера в Active Directory. Щелкните элемент **Настраиваемые** и добавьте `Description` в качестве настраиваемого атрибута. После выполнения этого метода обнаружения этот атрибут появится на вкладке "Свойства" устройства в консоли Configuration Manager.<!--513948-->  

4. На вкладке **Параметры** можно настроить параметры фильтрации или удаления устаревших записей компьютеров из обнаружения.  

5. Нажмите кнопку **ОК** , чтобы сохранить настройки.  

### <a name="configure-active-directory-user-discovery"></a><a name="bkmk_config-adud"></a> Настройка обнаружения пользователей Active Directory  

1. На вкладке **Общие** окна свойств обнаружения пользователей Active Directory выберите значок **Создать**![значок Создать](media/Disc_new_Icon.gif), чтобы указать новый контейнер Active Directory. В диалоговом окне **Контейнер Active Directory** выполните следующие настройки:  

    1. Укажите одно или несколько расположений для поиска.  

    2. Для каждого расположения укажите параметры, изменяющие способ поиска.  

    3. Для каждого расположения укажите учетную запись, которая будет использоваться в качестве **учетной записи обнаружения Active Directory**. Дополнительные сведения см. в разделе об [учетных записях](../../../plan-design/hierarchy/accounts.md#active-directory-user-discovery-account).  

        > [!NOTE]  
        > Для каждого заданного расположения можно настроить уникальный ряд параметров обнаружения и уникальную учетную запись обнаружения Active Directory.  

    4. Нажмите **OK**, чтобы сохранить конфигурацию контейнера Active Directory.  

2. На вкладке **Расписание опроса** настройте расписание опроса полного обнаружения и обнаружения изменений.  

3. На вкладке **Атрибуты Active Directory** настройте дополнительные атрибуты для компьютеров, которые нужно найти. На этой вкладке также указаны атрибуты объектов по умолчанию.  

4. Нажмите кнопку **ОК** , чтобы сохранить настройки.  


## <a name="azure-ad-user-discovery"></a><a name="azureaadisc"></a> Обнаружение пользователей Azure AD

Обнаружение пользователей Azure AD включается и настраивается не так, как другие методы обнаружения. Настройте этот метод при настройке сайта Configuration Manager в Azure AD.

Дополнительные сведения см. в статье [Обнаружение пользователей Azure AD](about-discovery-methods.md#azureaddisc).

### <a name="prerequisites"></a>Предварительные условия

Для активации и настройки этого метода обнаружения выполните [настройку служб Azure](azure-services-wizard.md) для **облачного управления**.

Если для *создания* приложения Azure используется Configuration Manager, он настраивает приложение с необходимыми правами доступа.

Если вы сначала создаете приложение в Azure, а затем *импортируете* его в Configuration Manager, вам необходимо вручную настроить приложение. Настройки включают в себя предоставление серверному приложению разрешения на чтение данных каталога.

1. Войдите на [Портал Azure](https://portal.azure.com) в качестве пользователя с правами *глобального администратора*. Перейдите в раздел **Azure Active Directory** и выберите **Регистрация приложений**. При необходимости переключитесь на вкладку **Все приложения**.

1. Выберите необходимое приложение.

1. В меню **Управление** выберите **Разрешения API**.  

    1. На панели **Разрешения API** выберите **Добавить разрешение**.  

    2. На панели **Запрос разрешений API** переключитесь на **Интерфейсы API, используемые моей организацией**.  

    3. Найдите и выберите API-интерфейс **Microsoft Graph**.  

        > [!Tip]
        > В версии 1810 и более ранних версиях используйте API **Azure Active Directory Graph**.

    4. Выберите группу **Разрешения приложения**. Разверните **Каталог** и выберите **Directory.Read.All**.  

    5. Выберите **Добавить разрешения**.  

1. На панели **Разрешения API** в разделе **Предоставление согласия** выберите **Предоставление согласия администратора...** . Выберите **Да**.  

### <a name="configure-azure-ad-user-discovery"></a>Настройка обнаружения пользователей Azure AD

При настройке **облачного управления** службы Azure:

- В мастере на странице **Обнаружение** щелкните **Включить обнаружение пользователей Azure Active Directory**.
- Выберите **Параметры**.
- В диалоговом окне "Параметры обнаружения пользователей Azure AD" настройте расписание для обнаружения. Также можно включить обнаружение изменений, при котором проверяется только наличие новых или измененных учетных записей в Azure AD.

> [!Note]  
> Если пользователь имеет федеративное или синхронизированное удостоверение, необходимо использовать [обнаружение пользователей Active Directory](about-discovery-methods.md#bkmk_aboutUser) в Configuration Manager, а также обнаружение пользователей Azure AD. Дополнительные сведения о гибридных удостоверениях см. в разделе [Определение стратегии внедрения гибридной идентификации](/azure/active-directory/active-directory-hybrid-identity-design-considerations-identity-adoption-strategy).<!--497750-->


## <a name="azure-ad-user-group-discovery"></a><a name="bkmk_azuregroupdisco"></a> Обнаружение группы пользователей Azure AD

<!--3611956-->
> [!Tip]  
> Эта функция появилась в версии 1906 [на стадии предварительного выпуска](../../manage/pre-release-features.md). Начиная с версии 2002, эта функция больше не считается функцией предварительной версии.  

Вы можете обнаруживать группы пользователей и членов этих групп в Azure AD. Когда сайт находит пользователей в группах Azure AD, которые ранее не были обнаружены, он добавляет их в качестве новых ресурсов пользователя в Configuration Manager. Запись ресурса-группы пользователей создается в том случае, если группа является группой безопасности.

### <a name="prerequisites"></a>Предварительные условия

- Управление облаком [службы Azure](azure-services-wizard.md)
- Разрешение на чтение и поиск в группах Azure AD

### <a name="limitations"></a>Ограничения

Обнаружение изменений для обнаружения группы пользователей Azure Active Directory сейчас отключено.

### <a name="log-files"></a>Файлы журнала

Используйте файл SMS_AZUREAD_DISCOVERY_AGENT.log для устранения неполадок. Этот журнал данных также используется для обнаружения пользователей Azure AD. Дополнительные сведения см. в [файлах журнала](../../../plan-design/hierarchy/log-files.md#BKMK_ServerLogs).

### <a name="enable-azure-ad-user-group-discovery"></a>Включение обнаружения групп пользователей в Azure AD

Чтобы включить обнаружение в существующей службе Azure **Управление облачными клиентами**:

1. Перейдите в рабочее пространство **Администрирование**, разверните **Облачные службы**, а затем выберите узел **Службы Azure**.
1. Выберите одну из служб Azure, а затем выберите меню **Свойства** в ленте.
1. На вкладке **Обнаружение** установите флажок **Включить обнаружение групп Azure Active Directory**, а затем выберите **Параметры**.
1. Нажмите кнопку **Добавить** на вкладке **Области обнаружения**.
    - Вы можете изменить **Расписание опроса** на другой вкладке.
1. Выберите одну группу пользователей или несколько. Вы можете использовать **Поиск** по имени и выбрать, хотите ли вы просмотреть **только группы безопасности**.
    - Вам будет предложено войти в Azure, когда вы щелкнете **Поиск** в первый раз.
1. По завершении выбора групп нажмите кнопку **OK**.
1. После обнаружения группы пользователей Azure AD можно видеть в узле **Пользователи**.

Чтобы включить обнаружение при настройке новой службы Azure **Управление облачными клиентами** выполните следующее:

- В мастере на странице **Обнаружение** щелкните **Включить обнаружение групп Azure Active Directory**.
- Выберите **Параметры**.
- В диалоговом окне "Параметры обнаружения групп Azure AD" настройте области обнаружения и его график ее проведения обнаружения.


## <a name="heartbeat-discovery"></a><a name="BKMK_ConfigHBDisc"></a> Heartbeat-обнаружение

Configuration Manager включает метод Heartbeat-обнаружения при установке основного сайта. Для использования расписания по умолчанию, по которому обнаружение будет проводиться каждые семь дней, дополнительные настройки не требуются. В ином случае необходимо настроить только периодичность отправки данных записей Heartbeat-обнаружения клиентами в точку управления.  

> [!NOTE]  
> Если на одном сайте наряду с принудительной установкой клиента включена задача обслуживания **Сброс флага установки**, установите для расписания Heartbeat-обнаружения значение, меньшее чем значение параметра **Период повторного обнаружения клиента** задачи обслуживания **Сброс флага установки**. Дополнительные сведения о задачах обслуживания сайта см. в статье [Задачи обслуживания](../../manage/maintenance-tasks.md).  

### <a name="configure-the-heartbeat-discovery-schedule"></a>Настройка расписания Heartbeat-обнаружения  

1. В рабочей области **Администрирование** консоли Configuration Manager разверните узел **Конфигурация иерархии** и щелкните узел **Методы обнаружения**.  

2. Выберите метод **Heartbeat-обнаружение** для сайта, на котором его нужно настроить.  

3. На вкладке **Рабочий стол** на ленте выберите команду **Свойства**.  

4. Настройте частоту, с которой клиенты отправляют запись данных Heartbeat-обнаружения. Чтобы сохранить настройки, нажмите **OK**.  


<a name="BKMK_AboutConfigNetworkDisc"></a>

## <a name="network-discovery"></a><a name="BKMK_ConfigNetworkDisc"></a> Обнаружение сети  

Прежде чем настроить обнаружение сетевых ресурсов, примите к сведению следующие данные.  

- Доступные уровни обнаружения сетевых ресурсов  

- Доступные параметры обнаружения сетевых ресурсов  

- Ограничение обнаружения сетевых ресурсов в сети  

Дополнительные сведения см. в разделе [Обнаружение сети](about-discovery-methods.md#bkmk_aboutNetwork).  

Следующие разделы содержат сведения об общих конфигурациях обнаружения сетевых ресурсов. Можно настроить одну или несколько конфигураций, которые будут использоваться во время выполнения одного и того же процесса обнаружения. При работе с несколькими конфигурациями учтите взаимодействия, которые могут повлиять на результаты обнаружения.  

Например, вы обнаружили все устройства SNMP-протокола, использующие конкретное имя сообщества SNMP. В том же процессе обнаружения вы отключили выполнение обнаружения в определенной подсети. Таким образом, запущенный метод обнаружения сетевых ресурсов не будет искать устройства SNMP с указанным именем сообщества в отключенной подсети.  

### <a name="determine-your-network-topology"></a><a name="BKMK_DetermineNetTopology"></a> Определение топологии сети  

Для сопоставления сети можно использовать обнаружение только топологии. В этом случае поиск потенциальных клиентов не выполняется. Для реализации метода обнаружения сетевых ресурсов с поиском только топологии используется протокол SNMP.  

При сопоставлении топологии сети задайте параметр **Максимальное число прыжков** на вкладке **SNMP** диалогового окна **Свойства обнаружения сети**. Если указать небольшое максимальное число прыжков, это поможет ограничить использование пропускной способности сети в процессе обнаружения. По мере дальнейшего обнаружения сетевых ресурсов увеличьте число прыжков, чтобы получить лучшее представление о топологии сети.  

После изучения топологии сети можно настроить дополнительные параметры для обнаружения сетевых ресурсов. Эти свойства позволяют найти потенциальных клиентов и их операционные системы. Также можно настроить обнаружение сетевых ресурсов для ограничения сегментов сети для поиска.  

Дополнительные сведения см. в разделе [Определение топологии сети](#bkmk_proc-top).

### <a name="network-discovery-search-options"></a>Параметры поиска обнаружения сетевых ресурсов

В Configuration Manager поддерживаются перечисленные ниже методы поиска сети.

- [Ограничение поиска заданными подсетями](#BKMK_LimitBySubnet)
- [Поиск в определенном домене](#BKMK_SearchByDomain)
- [Ограничение поиска с помощью имен SNMP-сообществ](#BKMK_LimitBySNMPname)
- [Поиск конкретного DHCP-сервера](#BKMK_SearchByDHCP)

#### <a name="limit-searches-by-using-subnets"></a><a name="BKMK_LimitBySubnet"></a> Ограничение поиска заданными подсетями  

Обнаружение сетевых ресурсов можно настроить для поиска в конкретных подсетях. По умолчанию при обнаружении сетевых ресурсов поиск производится в подсети сервера, выполняющего обнаружение. Все другие настроенные и включенные подсети применяются только в вариантах поиска с использованием протоколов SNMP и DHCP. При обнаружении сетевых ресурсов в доменах ограничения по подсетям не действуют.  

Если задать одну или несколько подсетей на вкладке **Подсети** диалогового окна **Свойства обнаружения сети**, поиск будет производиться только в тех подсетях, для которых установлен флажок **Включено**.  

Если отключить подсеть, в ней не будет производиться обнаружение, но будут выполняться следующие условия:  

- SNMP-запросы не будут выполняться в этой подсети;  

- DHCP-серверы в ответ на запрос не будут возвращать список ресурсов, расположенных в этой подсети;  

- с помощью запросов к доменам можно будет обнаруживать ресурсы, расположенные в данной подсети.  

#### <a name="search-a-specific-domain"></a><a name="BKMK_SearchByDomain"></a> Поиск в определенном домене  

Обнаружение сетевых ресурсов можно настроить для поиска в определенном домене или множестве доменов. По умолчанию при обнаружении сетевых ресурсов поиск производится в локальном домене сервера, выполняющего обнаружение.  

Если задать один или несколько доменов на вкладке **Домены** диалогового окна **Свойства обнаружения сети**, поиск будет производиться только в тех доменах, для которых установлен флажок **Включено**.  

Если отключить домен, в нем не будет производиться обнаружение, но будут выполняться следующие условия:  

- при обнаружении сетевых ресурсов запросы к контроллерам этого домена отправляться не будут;  

- SNMP-запросы по-прежнему будут выполняться в подсетях этого домена;  

- DHCP-серверы по-прежнему будут возвращать список ресурсов, расположенных в этом домене.  

#### <a name="limit-searches-by-using-snmp-community-names"></a><a name="BKMK_LimitBySNMPname"></a> Ограничение поиска с помощью имен SNMP-сообществ  

Обнаружение сетевых ресурсов можно настроить для поиска в определенном SNMP-сообществе или наборе таких сообществ. По умолчанию метод настраивает **общедоступное** имя сообщества.  

При обнаружении сетевых ресурсов имена сообществ используются для получения доступа к маршрутизаторам, которые являются SNMP-устройствами. Маршрутизатор может возвращать в процессе обнаружения сетевых ресурсов информацию о других маршрутизаторах и подсетях, связанных с ним.  

> [!NOTE]  
> Имена SNMP-сообществ напоминают пароли. При обнаружении сетевых ресурсов получать информацию можно только от тех SNMP-устройств, для которых указано имя сообщества. У каждого SNMP-устройства может быть собственное имя сообщества, но зачастую для нескольких устройств используется общее имя сообщества. Кроме того, большинству SNMP-устройств по умолчанию присвоено имя сообщества **public**. Но некоторые организации удаляют на своих устройствах имя сообщества **public** из соображений безопасности.  

Если на вкладке **SNMP** диалогового окна **Свойства обнаружения сети** отображается несколько SNMP-сообществ, поиск в них при обнаружении сетевых ресурсов будет производиться в том порядке, в котором они перечислены. Убедитесь, что часто используемые имена находятся в верхней части списка. Эта конфигурация помогает свести к минимуму сетевой трафик, создаваемый сайтом при попытке обратиться к устройству, используя разные имена.

> [!NOTE]  
> Кроме имени SNMP-сообщества вы можете указать IP-адрес или разрешаемое имя конкретного SNMP-устройства. Это можно сделать на вкладке **SNMP-устройства** диалогового окна **Свойства обнаружения сети**.  

#### <a name="search-a-specific-dhcp-server"></a><a name="BKMK_SearchByDHCP"></a> Поиск конкретного DHCP-сервера  

Обнаружение сетевых ресурсов можно настроить для поиска DHCP-клиентов с использованием определенного DHCP-сервера или нескольких серверов.  

Поиск будет вестись на каждом DHCP-сервере, указанном на вкладке **DHCP** диалогового окна **Свойства обнаружения сети** . Если сервер, выполняющий обнаружение, получает свой IP-адрес от DHCP-сервера, можно настроить обнаружение для поиска на данном DHCP-сервере. Включите этот режим с помощью параметра **Добавить DHCP-сервер, на использование которого настроен сервер сайта**.  

> [!NOTE]  
> Чтобы успешно настроить обнаружение сетевых ресурсов для использования DHCP-сервера, среда должна поддерживать протокол IPv4. Обнаружение сетевых ресурсов не может быть настроено для использования DHCP-сервера в среде на базе протокола IPv6.  

### <a name="how-to-configure-network-discovery"></a><a name="BKMK_HowToConfigNetDisc"></a> Настройка обнаружения сетевых ресурсов  

Следуйте описанным ниже процедурам, в соответствии с которыми сначала определяется только топология сети, а затем настраивается обнаружение сетевых ресурсов для поиска потенциальных клиентов с использованием одного или нескольких предусмотренных вариантов.  

#### <a name="how-to-determine-your-network-topology"></a><a name="bkmk_proc-top"></a> Определение топологии сети  

1. В рабочей области **Администрирование** консоли Configuration Manager разверните узел **Конфигурация иерархии** и щелкните узел **Методы обнаружения**.  

2. Выберите метод **Обнаружение сети**, на котором нужно включить обнаружение.  

3. На вкладке **Рабочий стол** на ленте выберите команду **Свойства**.  

    - На вкладке **Общие** установите опцию **Включить обнаружение сетевых ресурсов**. Затем выберите **Топология** из параметра **Тип обнаружения**.  

    - На вкладке **Подсети** выберите параметр **Поиск в локальных подсетях**.  

      > [!TIP]  
      > Если вы знаете, из каких конкретно подсетей состоит данная сеть, снимите флажок **Поиск в локальных подсетях**. Затем нажмите на значок **Создать**![значок Создать](media/Disc_new_Icon.gif), чтобы добавить конкретные подсети, в которых требуется выполнить поиск. Для крупных сетей выполняйте поиск не более чем в одной-двух подсетях за один раз, чтобы свести к минимуму использование пропускной способности.  

    - На вкладке **Домены** установите флажок **Поиск в локальном домене**.  

    - На вкладке **SNMP** выберите один вариант из раскрывающегося списка **Максимальное число прыжков**. Этот параметр указывает, сколько прыжков между маршрутизаторами обнаружение сети может обнаружить при сопоставлении топологии.  

      > [!TIP]  
      > Впервые определяя топологию сети, следует указать небольшое максимальное число прыжков — это поможет ограничить использование пропускной способности сети.  

4. На вкладке **Расписание** выберите значок **Создать**![значок Создать](media/Disc_new_Icon.gif), чтобы задать расписание обнаружения сетевых ресурсов.  

    > [!NOTE]  
    > Возможность задания различных конфигураций обнаружения для разных расписаний сетевого обнаружения не предусмотрена. Каждый раз, когда выполняется обнаружение сетевых ресурсов, используется текущая конфигурация обнаружения.  

5. Чтобы принять заданные конфигурации, нажмите **OK**. Обнаружение сети будет выполняться в назначенное время.  

#### <a name="how-to-configure-network-discovery"></a><a name="bkmk_proc-config"></a> Настройка обнаружения сетевых ресурсов  

1. В рабочей области **Администрирование** консоли Configuration Manager разверните узел **Конфигурация иерархии** и щелкните узел **Методы обнаружения**.  

2. Выберите метод **Обнаружение сети**, на котором нужно включить обнаружение.  

3. На вкладке **Рабочий стол** на ленте выберите команду **Свойства**.  

4. На вкладке **Общие** установите опцию **Включить обнаружение сетевых ресурсов**.  

    - Выберите один из **типов обнаружения**, который хотите запустить.  

    - Включите параметр **Медленная сеть** для Configuration Manager для автоматической корректировки низкой пропускной способности сети.  

5. Чтобы настроить обнаружение на поиск в подсетях, переключитесь на вкладку **Подсети**. Затем настройте один или несколько из следующих параметров.  

    - Чтобы обнаружение производилось в локальных подсетях компьютера, который выполняет обнаружение, установите флажок **Поиск в локальных подсетях**.  

    - Чтобы выполнить поиск в конкретной подсети, добавьте ее в список **Subnets to search** (Искать в подсетях), а для параметра **Поиск** задайте значение **Включено**:  

      1. Если подсеть отсутствует в списке, выберите значок **Создать**![значок Создать](media/Disc_new_Icon.gif). В диалоговом окне **Новое назначение подсети** введите значения параметров **Подсеть** и **Маска**, а затем нажмите **OK**. По умолчанию поиск в новой подсети включен.  

      2. Чтобы изменить значение **поиска** для подсети из списка, выберите ее в списке. Затем выберите значок **Переключить** для переключения между значениями **Отключено** и **Включено**.  

6. Чтобы настроить обнаружение на поиск в доменах, перейдите к вкладке **Домены**. Затем настройте один или несколько из следующих параметров.  

    - Чтобы обнаружение производилось на домене компьютера, выполняющего обнаружение, установите флажок **Поиск в локальном домене**.  

    - Чтобы выполнить поиск в конкретном домене, добавьте его в список **Домены**, а для параметра **Поиск** задайте значение **Включено**:  

      1. Если домен отсутствует в списке, выберите значок **Создать**![значок Создать](media/Disc_new_Icon.gif). В диалоговом окне **Свойства домена** введите сведения о **домене** и нажмите **OK**. По умолчанию поиск в новом домене включен.  

      2. Чтобы изменить значение **поиска** для домена из списка, выберите его в списке. Затем выберите значок **Переключить** для переключения между значениями **Отключено** и **Включено**.  

7. Чтобы настроить обнаружение для поиска определенных имен SNMP-сообществ для SNMP-устройств, перейдите на вкладку **SNMP**. Затем настройте один или несколько из следующих параметров.  

    - Чтобы добавить имя SNMP-сообщества в список **Имена SNMP-сообществ**, щелкните значок **Создать**![значок Создать](media/Disc_new_Icon.gif). В диалоговом окне **Новое имя SNMP-сообщества** укажите **имя** сообщества и нажмите **OK**.  

    - Чтобы удалить имя SNMP-сообщества из списка, выделите это имя и щелкните значок **Удалить**![значок "Удалить"](media/Disc_delete_Icon.gif).  

    - Чтобы изменить порядок поиска в именованных SNMP-сообществах, выделите имя сообщества из списка. Затем выберите значок **Переместить элемент вверх**![значок "Переместить вверх"](media/Disc_moveUp_Icon.gif) или значок **Переместить элемент вниз**![значок "Переместить вниз"](media/Disc_moveDown_Icon.gif). При обнаружении поиск в сообществах будет производиться сверху вниз в порядке следования имен. 

    - Чтобы задать максимально разрешенное количество прыжков между маршрутизаторами при SNMP-поиске, выберите нужное значение из раскрывающегося списка **Максимальное число прыжков**.  

8. Чтобы настроить SNMP-устройство, перейдите на вкладку **SNMP-устройства**. Если устройство отсутствует в списке, выберите значок **Создать**![значок Создать](media/Disc_new_Icon.gif). В диалоговом окне **Новое SNMP-устройство** укажите IP-адрес или имя SNMP-устройства, а затем нажмите **OK**.  

    > [!NOTE]  
    > Если указано имя устройства, система Configuration Manager должна быть в состоянии разрешить NetBIOS-имя в IP-адрес.  

9. Чтобы настроить обнаружение для запроса определенных DHCP-серверов, перейдите на вкладку **DHCP**. Затем настройте один или несколько из следующих параметров.  

    - Чтобы отправлять запросы к DHCP-серверу на компьютере, выполняющем обнаружение, включите параметр **Всегда использовать DHCP-сервер сайта**.  

      > [!NOTE]  
      > Для использования этого параметра сервер должен получать свой IP-адрес от DHCP-сервера и не должен иметь статический IP-адрес.  

    - Чтобы при обнаружении отправлялись запросы к определенному DHCP-серверу, щелкните значок **Создать**![значок Создать](media/Disc_new_Icon.gif). В диалоговом окне **Новый DHCP-сервер** введите IP-адрес или имя DHCP-сервера, а затем нажмите **OK**.  

      > [!NOTE]  
      > Если указано имя сервера, система Configuration Manager должна быть в состоянии разрешить NetBIOS-имя в IP-адрес.  

10. Для настройки времени выполнения обнаружения перейдите на вкладку **Расписание**. Щелкните значок **Создать**![значок Создать](media/Disc_new_Icon.gif), чтобы задать расписание обнаружения сетевых ресурсов. Вы можете задать несколько повторяющихся расписаний и несколько расписаний без повторения.  

    > [!NOTE]  
    > Если на вкладке **Расписание** отображается несколько расписаний одновременно, процедура обнаружения сетевых ресурсов будет запущена для каждого расписания в указанное в нем время. Это также справедливо и для повторяющихся расписаний.  

11. Чтобы сохранить конфигурации, нажмите **OK**.  

### <a name="how-to-verify-that-network-discovery-has-finished"></a><a name="BKMK_HowToVerifyNetDisc"></a> Проверка завершения обнаружения сетевых ресурсов  

Время, необходимое для того, чтобы завершить обнаружение сетевых ресурсов, зависит от различных факторов, в том числе:  

- размер сети;  

- топология сети;  

- максимальное число прыжков, заданное для поиска маршрутизаторов в данной сети;  

- тип выполняемого обнаружения.  

Обнаружение сетевых ресурсов не оповещает о своем завершении. Чтобы удостовериться, что обнаружение завершено, используйте следующую процедуру.  

1. В консоли Configuration Manager перейдите в рабочую область **Мониторинг**. Разверните **Состояние системы**, а затем выберите узел **Запросы сообщения о состоянии**.  

2. Выберите запрос **Все сообщения об изменении состояния**.  

3. На вкладке ленты **Главная** в группе **Запросы сообщения о состоянии** щелкните **Показать сообщения**.  

4. В окне Все сообщения об изменении состояния выберите значение из раскрывающегося списка **Выбрать дату и время**, содержащего момент запуска обнаружения. Затем выберите **ОК**, чтобы открыть **Средство просмотра сообщений о состоянии Configuration Manager**.  

    > [!TIP]  
    > Можно также использовать раскрывающийся список **Выбрать дату и время** для указания конкретных даты и времени, когда выполнялось обнаружение. Этот вариант полезен, если пользователь выполнял обнаружение сетевых ресурсов в определенную дату и желает получить сообщения только за эту дату.  

5. Чтобы проверить, завершилось ли обнаружение сетевых ресурсов, попытайтесь найти сообщение о состоянии следующего вида:  

    - Идентификатор сообщения: **502**  

    - Компонент: **SMS_NETWORK_DISCOVERY**  

    - Описание: **Компонент остановлен**  

    Если такое сообщение отсутствует, обнаружение сетевых ресурсов еще не завершено.  

6. Чтобы определить, когда было запущено обнаружение сетевых ресурсов, попытайтесь найти сообщение о состоянии следующего вида:  

    - Идентификатор сообщения: **500**  

    - Компонент: **SMS_NETWORK_DISCOVERY**  

    - Описание: **Компонент запущен**  

    Эта информация подтверждает, что обнаружение сетевых ресурсов запущено. Если эта информация отсутствует, заново запланируйте обнаружение сетевых ресурсов.  
