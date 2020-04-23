---
title: Установка облачных точек распространения
titleSuffix: Configuration Manager
description: Выполните эти инструкции, чтобы настроить облачную точку распространения в Configuration Manager.
ms.date: 09/06/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bb83ac87-9914-4a35-b633-ad070031aa6e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 30cd61240b09f821d8b18c37e6accc7450f35817
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701672"
---
# <a name="install-a-cloud-distribution-point-for-configuration-manager"></a>Установка облачной точки распространения для Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

> [!Important]  
> Реализация предоставления общего доступа к содержимому в Azure изменилась. Используйте облачный шлюз управления с включенной возможностью обслуживания содержимого. Для этого включите параметр **Allow CMG to function as a cloud distribution point and serve content from Azure storage** (Разрешить CMG работать как точка распространения и обслуживать содержимое из хранилища Azure). Дополнительные сведения см. в разделе [Изменение CMG](../../../clients/manage/cmg/setup-cloud-management-gateway.md#modify-a-cmg).
>
> В дальнейшем нельзя будет создавать традиционные облачные точки распространения. Дополнительные сведения см. в разделе [Удаленные и устаревшие компоненты](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).

В этой статье приводятся инструкции по установке облачной точки распространения Configuration Manager в Microsoft Azure. Она включает следующие разделы:

- [Подготовка к работе](#bkmk_before)
- [Установка](#bkmk_setup)
- [Настройка DNS](#bkmk_dns)
- [Настройка прокси-сервера сайта](#bkmk_proxy)
- [Распространение содержимого и настройка клиентов](#bkmk_client)
- [Управление и мониторинг](#bkmk_monitor)
- [Изменение](#bkmk_modify)
- [Расширенное устранение неполадок](#bkmk_tshoot)


## <a name="before-you-begin"></a><a name="bkmk_before"></a> Подготовка к работе

Прежде всего ознакомьтесь со статьей [Использование облачной точки распространения](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md). Она поможет вам спланировать и спроектировать облачные точки распространения.

Используйте следующий контрольный список, чтобы убедиться в наличии всех необходимых сведений и компонентов для создания облачной точки распространения:  

- Сервер сайта может подключиться к Azure. Если в сети используется прокси-сервер, [настройте роль системы сайта](#bkmk_proxy).  

- **Среда Azure**, которую необходимо использовать. Например, общедоступное облако Azure или облако Azure для государственных организаций США.  

- Начиная с версии 1806 и выше *рекомендуется* использовать **развертывания Azure Resource Manager**. Действуют следующие требования:<!--1322209-->  

    - Интеграция с [Azure Active Directory](azure-services-wizard.md) для службы **Управление облачными клиентами**. Обнаружение пользователей Azure AD не требуется.  

    - **Идентификатор подписки** Azure.  

    - **Группа ресурсов** Azure.  

    - **Администратор подписки** должен войти в свою учетную запись во время работы мастера.  

- **Сертификат проверки подлинности сервера**, экспортированный как PFX-файл.  

- Глобальное уникальное **имя службы** для облачной точки распространения.  

    > [!TIP]  
    > Прежде чем запросить сертификат проверки подлинности сервера, в котором применяется имя службы, убедитесь в том, что для домена Azure используется уникальное имя. Пример: *WallaceFalls.CloudApp.Net*.
    >
    > 1. Войдите на [портал Azure](https://portal.azure.com).
    > 1. Щелкните **Все ресурсы**, а затем нажмите кнопку **Добавить**.
    > 1. Выполните поиск по запросу **Облачная служба**. Щелкните **Создать**.
    > 1. В поле **DNS-имя** введите нужный префикс, например *WallaceFalls*. В интерфейсе будет указано, доступен ли домен или он уже используется другой службой.
    >
    > Не создавайте службу на портале. Просто воспользуйтесь этим процессом для проверки доступности имени.

- **Регион** Azure для этого развертывания.  

- Если вам все еще нужно использовать **классическое развертывание службы Azure** в Configuration Manager версии 1810 или более ранней, вам необходимо выполнить следующие требования:  

    > [!Important]  
    > Начиная с версии 1810 классическое развертывание службы в Azure не рекомендуется использовать в Configuration Manager. Перейдите на использование развертываний Azure Resource Manager для облачной точки распространения. Дополнительные сведения см. в статье об [Azure Resource Manager](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#azure-resource-manager).  
    >
    > Начиная с версии Configuration Manager 1902, Azure Resource Manager — единственный механизм развертывания для новых экземпляров облачной точки распространения.<!-- 3605704 -->

    - **Идентификатор подписки** Azure.  

    - **Сертификат управления** Azure, экспортированный в CER-файл и в PFX-файл. Администратору подписки Azure необходимо добавить сертификат управления CER в подписку на [портале Azure](https://portal.azure.com).  

### <a name="branchcache"></a>BranchCache

Чтобы разрешить облачной точке распространения использовать Windows BranchCache, установите функцию BranchCache на сервере сайта.<!-- SCCMDocs-pr#4054 -->

- Если сервер сайта имеет роль системы сайта локальной точки распространения, настройте параметр в свойствах этой роли, чтобы **включить и настроить BranchCache**. Дополнительные сведения см. в разделе [Настройка точки распространения](install-and-configure-distribution-points.md#bkmk_config-general).

- Если у сервера сайта нет роли точки распространения, установите функцию BranchCache в Windows. Дополнительные сведения см. в разделе [Установка функции BranchCache](https://docs.microsoft.com/windows-server/networking/branchcache/deploy/install-the-branchcache-feature).

Если вы уже распространяли содержимое в облачную точку распространения, а затем решили включить BranchCache, сначала установите этот компонент. Затем повторно распространите содержимое в облачную точку распространения.

> [!NOTE]  
> В Configuration Manager версии 1810 и более ранних версиях при наличии нескольких облачных точек распространения необходимо вручную задать парольную фразу ключа BranchCache. Дополнительные сведения см. в [статье базы знаний 4458143 на веб-сайте технической поддержки Майкрософт](https://support.microsoft.com/help/4458143).

## <a name="set-up"></a><a name="bkmk_setup"></a> Установка  

Выполните приведенную ниже процедуру на сайте для размещения облачной точки распространения в соответствии с [проектом](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#bkmk_topology).  

1. В консоли Configuration Manager в рабочей области **Администрирование** разверните узел **Облачные службы** и щелкните **Облачные точки распространения**. На ленте щелкните **Создать облачную точку распространения**.  

2. На странице **Общие** мастера создания облачных точек распространения настройте указанные ниже параметры.  

    1. Сначала укажите **окружение Azure**.  

    2. Начиная с версии 1806 и выше *рекомендуется* использовать **метод развертывания Azure Resource Manager**. Щелкните **Войти**, чтобы выполнить проверку подлинности с учетной записью администратора подписки Azure. Мастер автоматически заполняет оставшиеся поля данными, сохраненными в качестве предварительных требований интеграции Azure AD. Если вы владеете несколькими подписками, выберите нужный **код подписки**.  

    > [!Note]  
    > Начиная с версии 1810 классическое развертывание службы в Azure не рекомендуется использовать в Configuration Manager.
    >
    > Если вам нужно использовать классическое развертывание службы, выберите соответствующий параметр на этой странице. Сначала введите **идентификатор подписки Azure**. Нажмите кнопку **Обзор** и выберите PFX-файл для сертификата управления Azure.  

3. Выберите **Далее**. Дождитесь завершения проверки сайтом подключения к Azure.  

4. На странице **Параметры** укажите следующие параметры, а затем нажмите кнопку **Далее**:  

    - **Регион**. Выберите регион Azure, где нужно создать облачную точку распространения.  

    - **Группа ресурсов** (только для метода развертывания с помощью Azure Resource Manager)  

        - **Использовать существующую**. Выберите существующую группу ресурсов из раскрывающегося списка.  

        - **Создать новую**. Введите имя группы ресурсов, которую нужно создать в подписке Azure.  

    - **Основной сайт**. Выберите первичный сайт, который будет передавать содержимое в эту точку распространения.

    - **Файл сертификата**. Нажмите кнопку **Обзор** и выберите PFX-файл для сертификата проверки подлинности сервера, связанного с этой облачной точкой распространения. Общее имя из этого сертификата передается в обязательные поля **Полное доменное имя службы** и **Имя службы**.  

        > [!NOTE]  
        > Сертификат проверки подлинности сервера для облачной точки распространения поддерживает подстановочные знаки. Если используется сертификат с подстановочным знаком, замените звездочку (`*`) в поле **Полное доменное имя службы** нужным именем узла для службы.  

5. На странице **Предупреждения** настройте квоты хранилища, квоты передачи данных и процент квот, для которого требуется получать предупреждения Configuration Manager. Нажмите кнопку **Далее**.  

6. Завершите работу мастера.  

### <a name="monitor-installation"></a>Мониторинг установки  

Сайт начинает создавать размещенную службу для облачной точки распространения. После закрытия мастера можно следить за ходом установки облачной точки распространения в консоли Configuration Manager. Кроме того, можно отслеживать файл **CloudMgr.log** на сервере первичного сайта. При необходимости подготовку облачной службы можно отслеживать на портале Azure.  

> [!NOTE]  
> Инициализация новой точки распространения в Azure может занять до 30 минут. Следующее сообщение повторяется в файле **CloudMgr.log** до подготовки учетной записи хранения:  
> `Waiting for check if container exists. Will check again in 10 seconds`  
> После подготовки учетной записи хранения служба будет создана и настроена.  

### <a name="verify-installation"></a>Проверка установки

Убедитесь в завершении установки облачной точки распространения одним из описанных ниже способов.  

- В консоли Configuration Manager перейдите к рабочей области **Администрирование**. Разверните узел **Облачные службы** и выберите узел **Облачные точки распространения**. Найдите новую облачную точку распространения в списке. В столбце "Состояние" должно содержаться значение **Готово**.  

- В консоли Configuration Manager перейдите в рабочую область **Мониторинг**. Разверните узел **Состояние системы** и выберите узел **Состояние компонента**. Отобразите все сообщения от компонента **SMS_CLOUD_SERVICES_MANAGER** и найдите сообщение о состоянии с идентификатором **9409**.  

- При необходимости перейдите на портал Azure. В области **Развертывание** облачной точки распространения будет отображаться состояние **Готово**.  


## <a name="configure-dns"></a><a name="bkmk_dns"></a> Настройка DNS  

Перед тем как клиенты смогут использовать облачную точку распространения, они должны иметь возможность разрешать имя облачной точки распространения в IP-адрес, находящийся под управлением Azure. Точка управления предоставляет **полное доменное имя службы** для облачной точки распространения. Облачная точка распространения существует в Azure в виде **имени службы**. Просмотрите значения на вкладке **Параметры** свойств облачной точки распространения.

> [!Note]  
> В узле **Облачные точки распространения** консоли есть столбец с именем **Имя службы**, однако в нем фактически приводятся **полные доменные имена служб**. Чтобы увидеть оба значения, откройте окно **Свойства** для облачной точки распространения и перейдите на вкладку **Параметры**.  

<!-- Remove based on feedback from RoYork
If you issue the server authentication certificate from your PKI, you may directly specify the Azure **Service name**. For example, `WallaceFalls.cloudapp.net`. When you specify this certificate in the Create Cloud Distribution Point Wizard, both the **Service FQDN** and **Service name** properties are the same. In this scenario, you don't need to configure DNS. The name that clients receive from the management point is the same name as the service in Azure.  
-->

Общее имя сертификата проверки подлинности сервера должно включать в себя доменное имя. Это имя требуется, когда вы приобретаете сертификат у общедоступного поставщика. Оно рекомендуется, если сертификат выпускается из инфраструктуры открытых ключей (PKI). Например, `WallaceFalls.contoso.com`. Если этот сертификат указывается в мастере создания облачных точек распространения, общее имя задается в свойстве **Домен. имя службы** (`WallaceFalls.contoso.com`). В **имени службы** берется то же имя узла (`WallaceFalls`) и добавляется к доменному имени Azure, `cloudapp.net`. В этом сценарии клиентам необходимо разрешать **полное доменное имя службы** домена (`WallaceFalls.contoso.com`) в **имя службы** Azure (`WallaceFalls.cloudapp.net`). Создайте псевдоним CNAME для сопоставления этих имен.

### <a name="create-cname-alias"></a>Создание псевдонима CNAME

Создайте запись канонического имени (CNAME) в общедоступной службе DNS организации с выходом в Интернет. Эта запись создает псевдоним для получаемого клиентами свойства **Домен. имя службы** облачной точки распространения в **имени службы** Azure. Например, создайте запись CNAME для `WallaceFalls.contoso.com` в `WallaceFalls.cloudapp.net`.  

### <a name="client-name-resolution-process"></a>Процесс разрешения имени клиента

Ниже описывается, как клиент разрешает имя облачной точки распространения.  

1. Клиент получает **полное доменное имя службы** для облачной точки распространения в списке источников содержимого. Например, `WallaceFalls.contoso.com`.  

2. Он выполняет запрос к службе DNS, которая разрешает полное доменное имя службы с помощью псевдонима CNAME для **имени службы** Azure. Например, `WallaceFalls.cloudapp.net`.  

3. Он снова выполняет запрос к службе DNS, которая разрешает имя службы Azure в общедоступный IP-адрес.  

4. Клиент использует этот IP-адрес для запуска обмена данными с облачной точкой распространения.  

5. Облачная точка распространения представляет сертификат проверки подлинности сервера клиенту. Клиент использует цепь доверия проверяемого сертификата.  


## <a name="set-up-site-server-proxy"></a><a name="bkmk_proxy"></a> Настройка прокси-сервера сайта  

Серверу первичного сайта, который управляет облачной точкой распространения, требуется связь с Azure. Если в организации для управления доступом к Интернету применяется прокси-сервер, настройте его использование на сервере первичного сайта.  

Дополнительные сведения см. в статье [Поддержка прокси-сервера](../../../plan-design/network/proxy-server-support.md).  


## <a name="distribute-content-and-configure-clients"></a><a name="bkmk_client"></a> Распространение содержимого и настройка клиентов

Содержимое передается в облачную точку распространения точно так же, как в локальную. Точка управления не включает облачную точку распространения в список расположений содержимого, если в ней нет содержимого, запрашиваемого клиентами. Дополнительные сведения см. в разделе [Распространение содержимого и управление им](deploy-and-manage-content.md).

Управление облачной точкой распространения осуществляется точно так же, как локальной. Действия включают в себя назначение облачной точки распространения группе точек распространения и управление пакетами содержимого. Дополнительные сведения см. в разделе [Установка и настройка точек распространения](install-and-configure-distribution-points.md).

Параметры клиента по умолчанию позволяют ему использовать облачные точки распространения. Вы управляете доступом ко всем облачным точкам распространения в иерархии с помощью указанных ниже параметров клиента.  

- В группе **Настройки облака** измените параметр **Разрешить доступ к облачным точкам распространения**.  

    - По умолчанию для него установлено значение **Да**.  

    - Измените и разверните этот параметр для пользователей и устройств.  


## <a name="manage-and-monitor"></a><a name="bkmk_monitor"></a> Управление и мониторинг  

Содержимое, передаваемое в облачную точку распространения, отслеживается точно так же, как передаваемое в локальную. Дополнительные сведения см. в разделе [Мониторинг содержимого](monitor-content-you-have-distributed.md).

### <a name="alerts"></a><a name="bkmk_alerts"></a> Предупреждения  

Configuration Manager периодически проверяет службу Azure. Если служба неактивна или возникли проблемы с сертификатом или подпиской, Configuration Manager создает оповещение.

Настройте пороговые значения для объема данных, который нужно хранить в облачной точке распространения, и для объема данных, который клиенты скачивают из точки распространения. Оповещения о достижении этих пороговых значений позволяют определить, когда следует остановить или удалить облачную службу, изменить содержимое, которое хранится в облачной точке распространения, или изменить клиенты, которые могут использовать службу.

- **Порог оповещений хранилища**. Задает верхний предел (в ГБ) объема данных или содержимого, который должен храниться в облачной точке распространения. По умолчанию этот предел составляет 2000 ГБ. Configuration Manager создает предупреждения и критические оповещения, когда свободное место достигает заданных уровней. По умолчанию оповещения создаются при достижении 50 % и 90 % от порогового значения.  

- **Месячный порог оповещений передачи**. Это значение помогает отслеживать объем содержимого, передаваемый из точки распространения клиентам в течение 30 дней. По умолчанию этот порог составляет 10 000 ГБ. Сайт создает предупреждение и критические оповещения, если объем переданных данных достигает заданных значений. По умолчанию оповещения создаются при достижении 50 % и 90 % от порогового значения.  

    > [!IMPORTANT]  
    > Configuration Manager отслеживает передачу данных, но не останавливает передачу после достижения указанного порога оповещений передачи.  

Задайте пороговые значения для каждой облачной точки распространения в процессе установки или используйте вкладку **Оповещения** в окне свойств облачной точки распространения.  

> [!NOTE]  
> Оповещения для облачной точки распространения зависят от статистики использования, полученной от Azure, и для их появления может потребоваться до 24 часов. Дополнительные сведения об аналитике службы хранилища Azure см. в статье [Аналитика хранилища](https://docs.microsoft.com/rest/api/storageservices/storage-analytics).  

В почасовом цикле первичный сайт, отслеживающий облачную точку распространения, скачивает данные транзакций из Azure. Эти данные сохраняются в файле `CloudDP-<ServiceName>.log` на сервере сайта. Configuration Manager оценивает эти сведения в отношении квот хранилища и передачи для каждой облачной точки распространения. Если объем передаваемых данных достигает или превышает указанный объем для предупреждений или критических оповещений, Configuration Manager формирует соответствующее оповещение.  

> [!WARNING]  
> Так как сайт скачивает сведения о передаче данных из Azure каждый час, объем данных может превысить порог предупреждения или критического оповещения, прежде чем Configuration Manager сможет получить доступ к данным и вызвать оповещение.  


## <a name="modify"></a><a name="bkmk_modify"></a> Изменение

Вы можете просмотреть обобщенные сведения о точке распространения в узле **Облачные точки распространения** в разделе **Облачные службы** в рабочей области **Администрирование** консоли Configuration Manager. Выберите точку распространения и щелкните **Свойства**, чтобы просмотреть дополнительные сведения.  

При изменении свойств облачной точки распространения для изменения доступны параметры на перечисленных ниже вкладках.  

#### <a name="settings"></a>"Настройки"

- **Описание**  

- **Файл сертификата**. Прежде чем истечет срок действия сертификата проверки подлинности сервера, выдайте новый сертификат с тем же общим именем. Затем добавьте новый сертификат здесь, чтобы служба начала использовать его. Если срок действия сертификата истек, клиенты не доверяют службе и не используют ее.  

#### <a name="alerts"></a>Предупреждения

Настройте пороговые значения данных для хранилища и оповещений о ежемесячной передаче данных.  

#### <a name="content"></a>Content

Управляйте содержимым по аналогии с локальной точкой распространения.  

### <a name="redeploy-the-service"></a>Повторное развертывание службы

Более значительные изменения, например следующие настройки, требуют повторного развертывания службы:

- Замена классической модели развертывания моделью Azure Resource Manager
- Подписка
- Имя службы
- Замена закрытых ключей открытыми (PKI)
- Регион Azure

Начиная с версии 1806 при наличии существующей облачной точки распространения в классической модели развертывания необходимо развернуть новую облачную точку распространения для использования метода развертывания Azure Resource Manager. Существует два варианта.

- Если вы хотите повторно использовать то же имя службы, выполните следующие действия.  

    1. Сначала удалите классическую облачную точку распространения. Если другой облачной точки распространения нет, клиенты, возможно, не смогут получить содержимое.  

    2. Создайте облачную точку распространения с помощью модели развертывания Azure Resource Manager. Используйте тот же сертификат проверки подлинности сервера.  

    3. Передайте необходимое содержимое пакетов ПО в новую облачную точку распространения.  

- Если вы хотите использовать новое имя службы, выполните следующие действия.  

    1. Создайте облачную точку распространения с помощью модели развертывания Azure Resource Manager. Используйте новый сертификат проверки подлинности сервера.  

    2. Передайте необходимое содержимое пакетов ПО в новую облачную точку распространения.  

    3. Удалите классическую облачную точку распространения.

> [!Tip]  
> Чтобы определить текущую модель развертывания облачной точки распространения, выполните указанные ниже действия.<!--SCCMDocs issue #611-->  
>
> 1. В консоли Configuration Manager в рабочей области **Администрирование** разверните узел **Облачные службы** и выберите узел **Облачные точки распространения**.  
> 2. Добавьте атрибут **Модель развертывания** в качестве столбца в представление списка. Для развертывания с помощью Resource Manager этот атрибут имеет значение **Azure Resource Manager**.  

### <a name="stop-or-start-the-cloud-service-on-demand"></a>Остановка или запуск облачной службы по требованию

Вы можете остановить облачную точку распространения в консоли Configuration Manager в любой момент. При этом вы немедленно запрещаете клиентам скачивать дополнительное содержимое из службы. Перезапустите облачную службу в консоли Configuration Manager, чтобы восстановить доступ для клиентов. Например, можно остановить облачную службу при достижении порогового значения для данных.  

При остановке облачной точки распространения облачная служба не удаляет содержимое из учетной записи хранения. Кроме того, это действие не запрещает серверу сайта передавать дополнительное содержимое в облачную точку распространения. Точка управления по-прежнему возвращает облачную точку распространения клиентам в качестве допустимого источника содержимого.

Чтобы остановить облачную точку распространения, используйте описанную ниже процедуру.  

1. В консоли Configuration Manager перейдите к рабочей области **Администрирование**. Разверните узел **Облачные службы** и выберите узел **Облачные точки распространения**.  

2. Выберите облачную точку распространения. Чтобы остановить службу, которая работает в Azure, нажмите на ленте кнопку **Остановить службу**.  

3. Чтобы перезапустить облачную точку распространения, щелкните **Запустить службу**.  

### <a name="delete-a-cloud-distribution-point"></a>Удаление облачной точки распространения

Чтобы удалить облачную точку распространения, выберите ее в консоли Configuration Manager и нажмите кнопку **Удалить**.  

При удалении облачной точки распространения из иерархии Configuration Manager удаляет содержимое из облачной службы в Azure.

Удаление всех компонентов в Azure вручную приведет к несогласованности системы. В этом случае остаются потерянные данные и может возникнуть непредвиденное поведение.


## <a name="advanced-troubleshooting"></a><a name="bkmk_tshoot"></a> Расширенное устранение неполадок

Если необходимо собирать диагностические данные журнала из виртуальных машин Azure с целью устранения неполадок облачной точки распространения, используйте следующий образец скрипта PowerShell, чтобы включить расширение диагностики службы для подписки:<!--514275-->  

``` PowerShell
# Change these variables for your Azure environment. The current values are provided as examples. You can find the values for these from the Azure portal.
$storage_name="4780E38368358502‬‭23C071" # The name of the storage account that goes with the CloudDP
$key="3jSyvMssuTyAyj5jWHKtf2bV5JF^aDN%z%2g*RImGK8R4vcu3PE07!P7CKTbZhT1Sxd3l^t69R8Cpsdl1xhlhZtl" # The storage access key from the Storage Account view
$service_name="4780E38368358502‬‭23C071" # The name of the cloud service for the CloudDP, which for a Cloud DP is the same as the storage name
$azureSubscriptionName="8ba1cb83-84a2-457e-bd37-f78d2dd371ee" # The subscription name the tenant is using
$subscriptionId="8ba1cb83-84a2-457e-bd37-f78d2dd371ee" # The subscription ID the tenant is using

# This variable is the path to the config file on the local computer.
$public_config="F:\PowerShellDiagFile\diagnostics.wadcfgx"

# These variables are for the Azure management certificate. Install it in the Current User certificate store on the system running this script.
$thumbprint="dac9024f54d8f6df94935fb1732638ca6ad77c13" # The thumbprint of the Azure management certificate
$mycert = Get-Item cert:\\CurrentUser\My\$thumbprint

Set-AzureSubscription -SubscriptionName $azureSubscriptionName -SubscriptionId $subscriptionId -Certificate $mycert

Select-AzureSubscription $azureSubscriptionName

Set-AzureServiceDiagnosticsExtension -StorageAccountName $storage_name -StorageAccountKey $key -DiagnosticsConfigurationPath $public_config –ServiceName $service_name -Slot 'Production' -Verbose
```

Ниже приведен пример файла **diagnostics.wadcfgx**, указанного в переменной **public_config** в приведенном выше скрипте PowerShell. Дополнительные сведения см. в статье [Схема конфигурации расширения системы диагностики Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/azure-diagnostics-schema).  

``` XML
<?xml version="1.0" encoding="utf-8"?>
<PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <WadCfg>
    <DiagnosticMonitorConfiguration overallQuotaInMB="4096">
      <Directories scheduledTransferPeriod="PT1M">
        <IISLogs containerName ="wad-iis-logfiles" />
        <FailedRequestLogs containerName ="wad-failedrequestlogs" />
      </Directories>
      <WindowsEventLog scheduledTransferPeriod="PT1M">
        <DataSource name="Application!*" />
      </WindowsEventLog>
      <Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Information" />
      <CrashDumps dumpType="Full">
        <CrashDumpConfiguration processName="WaAppAgent.exe" />
        <CrashDumpConfiguration processName="WaIISHost.exe" />
        <CrashDumpConfiguration processName="WindowsAzureGuestAgent.exe" />
        <CrashDumpConfiguration processName="WaWorkerHost.exe" />
        <CrashDumpConfiguration processName="DiagnosticsAgent.exe" />
        <CrashDumpConfiguration processName="w3wp.exe" />
      </CrashDumps>
      <PerformanceCounters scheduledTransferPeriod="PT1M">
        <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Requests/Sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Errors Total/Sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Queued" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Rejected" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
      </PerformanceCounters>
    </DiagnosticMonitorConfiguration>
  </WadCfg>
</PublicConfig>
```