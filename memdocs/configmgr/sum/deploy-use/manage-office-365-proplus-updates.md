---
title: Управление обновлениями Office 365 профессиональный плюс
titleSuffix: Configuration Manager
description: Configuration Manager синхронизирует обновления клиента Office 365 в каталоге WSUS с сервером сайта, чтобы сделать их доступными для развертывания на клиентах.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 04/21/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: eac542eb-9aa1-4c63-b493-f80128e4e99b
ms.openlocfilehash: 4967b8b289d54a6355cb0a1e6454d5fac469a733
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110412"
---
# <a name="manage-office-365-proplus-with-configuration-manager"></a>Управление Office 365 профессиональный плюс с помощью Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

> [!Note]
> Начиная с 21 апреля 2020 г. Office 365 профессиональный плюс переименовывается в **Приложения Microsoft 365 для предприятия**. Дополнительные сведения см. в статье [Изменение названия Office 365 профессиональный плюс](https://docs.microsoft.com/deployoffice/name-change). Пока консоль Configuration Manager обновляется, в ней и в сопутствующей документации может встречаться старое название.

Configuration Manager позволяет управлять приложениями Office 365 профессиональный плюс. Доступны следующие варианты управления:

- [Развертывание приложений Office 365](#deploy-office-365-apps). Установщик Office 365 можно запустить с [панели управления клиентом Office 365](office-365-dashboard.md) для упрощения процесса первичной установки приложения Office 365. Мастер позволяет настроить параметры установки Office 365, скачать файлы из сети доставки содержимого (CDN), создать и развернуть приложение сценария на основе содержимого.

- [Развертывание обновлений Office 365](#deploy-office-365-updates). Можно управлять обновлениями клиента Office 365 с помощью рабочего процесса управления обновлениями программного обеспечения. Когда корпорация Майкрософт публикует новое обновление клиента Office 365 в сети доставки содержимого сети (CDN) Office, она также публикует пакет обновления для служб Windows Server Update Services (WSUS). После того как Configuration Manager синхронизирует обновление клиента Office 365 в каталоге WSUS с сервером сайта, оно будет доступно для развертывания на клиентах.

   > [!NOTE]
   > Начиная с версии Configuration Manager 2002, можно импортировать обновления для Office 365 в отключенные среды. Дополнительные сведения см. в статье [Синхронизация обновлений Office 365 из отключенной точки обновления программного обеспечения](../get-started/synchronize-office-updates-disconnected.md).   

- [Добавление поддержки языков для скачивания обновлений Office 365](#bkmk_o365_lang). В Configuration Manager можно добавить поддержку скачивания обновлений для любых языков, поддерживаемых Office 365. При этом не имеет значения, поддерживаются ли они в Configuration Manager. До версии Configuration Manager 1610 необходимо скачать и развернуть обновления для всех языков, настроенных в клиентах Office 365.

- [Изменение канала обновления](#bkmk_channel). Чтобы изменить канал обновления, можно распространить изменение раздела реестра в клиентах Office 365 с помощью групповой политики.

На [панели мониторинга для управления клиентами Office 365](office-365-dashboard.md) можно просмотреть сведения о клиенте Office 365 и запустить некоторые из действий управления Office 365.

## <a name="deploy-office-365-apps"></a>Развертывание приложений Office 365  
Запустите установщик Office 365 с панели управления клиентом Office 365 для первичной установки приложения Office 365. Мастер позволяет настроить параметры установки Office 365, скачать файлы из сети доставки содержимого (CDN), создать и развернуть приложение сценария для работы с файлами. Обновления Office 365 не применяются, пока служба Office 365 не будет установлена на клиентах и не будет запущена [задача автоматического обновления Office](https://docs.microsoft.com/deployoffice/overview-of-the-update-process-for-office-365-proplus). В целях тестирования задачу обновления можно запустить вручную.

Чтобы в первый раз установить приложения Office 365 на клиентах с предыдущими версиями Configuration Manager, выполните следующие действия.
- Скачайте средство развертывания Office 365.
- Скачайте исходные файлы установки Office 365, в том числе необходимые языковые пакеты.
- Создайте файл Configuration.xml, содержащий правильную версию Office и канала.
- Создайте и разверните пакет или приложение сценария, чтобы установить приложения Office 365 на клиенты.

### <a name="requirements"></a>Requirements (Требования)
- Компьютер, на котором выполняется установщик Office 365, должен иметь доступ к Интернету.  
- Пользователь, запускающий установщик Office 365, должен иметь права на **чтение** и **запись** для общей папки расположения содержимого, которая указана в мастере.
- Если при скачивании появляется ошибка 404, скопируйте следующие файлы в папку %temp% для текущего пользователя:
  - [releasehistory.xml](https://officecdn.microsoft.com/pr/wsus/releasehistory.cab)
  - [o365client_32bit.xml](https://officecdn.microsoft.com/pr/wsus/ofl.cab)  

### <a name="deploy-office-365-apps-using-configuration-manager-version-1806-or-higher"></a>Развертывание приложений Office 365 с помощью Configuration Manager версии 1806 или более поздней: 
Начиная с версии Configuration Manager 1806 центр развертывания Office интегрирован с установщиком Office 365 в консоли Configuration Manager. При создании развертывания для Office 365 вы можете динамически настроить последние параметры управления Office. <!--1358149-->

1. В консоли Configuration Manager последовательно выберите **Библиотека программного обеспечения** > **Обзор** > **Управление клиентом Office 365**.
2. В верхней правой части окна щелкните **Установщик Office 365**. Откроется мастер установки клиента Office 365.
3. На странице **Параметры приложения** укажите имя и описание приложения, введите расположение загрузки для файлов и нажмите кнопку **Далее**. Расположение должно быть таким: &#92;&#92;*сервер*&#92;*общая папка*.
4. На странице **Параметры Office** щелкните **Перейти в центр развертывания Office**. Откроется [средство настройки Office для технологии "нажми и работай"](https://config.office.com).
5. Настройте нужные параметры для установки Office 365. По завершении настройки в правом верхнем углу страницы щелкните **Отправить**. 
6. На странице **Развертывание** решите, нужно ли выполнить развертывание сейчас или позже. Если вы решили развернуть приложение позже, его можно будет найти на странице **Библиотека программного обеспечения** > **Управление приложениями** > **Приложения**.  
7. На странице **Сводка** подтвердите параметры. 
8. Нажмите кнопку **Далее**, а затем нажмите кнопку **Закрыть**, когда мастер установки клиента Office 365 завершит работу. 

### <a name="deploy-office-365-apps-using-configuration-manager-version-1802-and-prior"></a>Развертывание приложений Office 365 с помощью Configuration Manager версии 1802 или более ранней:

1. В консоли Configuration Manager последовательно выберите **Библиотека программного обеспечения** > **Обзор** > **Управление клиентом Office 365**.
2. В верхней правой части окна щелкните **Установщик Office 365**. Откроется мастер установки клиента Office 365.
3. На странице **Параметры приложения** укажите имя и описание приложения, введите расположение загрузки для файлов и нажмите кнопку **Далее**. Расположение должно быть таким: &#92;&#92;*сервер*&#92;*общая папка*.
4. На странице **Импорт параметров клиента** укажите, требуется ли импортировать параметры клиента Office 365 из существующего XML-файла конфигурации, или задайте параметры вручную. Завершив настройку, нажмите кнопку **Далее**.  

    При наличии существующего файла конфигурации введите путь к файлу и перейдите к шагу 7. Укажите расположение в виде &#92;&#92;*сервер*&#92;*общая папка*&#92;*имя_файла*.XML.
    > [!IMPORTANT]    
    > XML-файл конфигурации должен содержать только [языки, поддерживаемые клиентом Office 365 ProPlus](https://docs.microsoft.com/deployoffice/office2016/language-identifiers-and-optionstate-id-values-in-office-2016).

5. На странице **Клиентские продукты** выберите набор Office 365, который вы используете. Выберите приложения, которые хотите включить. Выберите дополнительные продукты Office, которые требуется включить, а затем нажмите кнопку **Далее**.
6. На странице **Параметры клиента** выберите параметры, которые будут включены, а затем нажмите кнопку **Далее**.
7. На странице **Развертывания** укажите необходимость развертывания приложения, а затем нажмите кнопку **Далее**. <br/>Если вы решили не развертывать пакет в мастере, перейдите к шагу 9.
8. Настройте параметры в остальной части мастера, как для обычного развертывания приложения. Подробные сведения см. в разделе [Создание и развертывание приложения](../../apps/get-started/create-and-deploy-an-application.md).
9. Завершите работу мастера.
10. Чтобы развернуть или изменить приложение, откройте последовательно элементы **Библиотека программного обеспечения** > **Обзор** > **Управление приложениями** > **Приложения**.    

Когда вы создаете и развертываете приложения Office 365 с помощью установщика Office 365, по умолчанию Configuration Manager не берет на себя управление обновлениями Office. Чтобы клиенты Office 365 получали обновления через Configuration Manager, выполните инструкции из статьи [Развертывание обновлений Office 365 с помощью Configuration Manager](#deploy-office-365-updates).

После развертывания приложений Office 365 можно создать правила автоматического развертывания для обслуживания приложений. Чтобы создать правило автоматического развертывания для приложений Office 365, щелкните действие **Создать ADR** на [панели мониторинга для управления клиентами Office 365](office-365-dashboard.md). Щелкните **Клиент Office 365** при выборе продукта. Дополнительные сведения см. в статье [Автоматическое развертывание обновлений программного обеспечения](automatically-deploy-software-updates.md).


## <a name="drill-through-required-office-365-updates"></a>Детализация необходимых обновлений Office 365
<!--4224414-->
*(Представлено в версии 1906)*

Статистика по соответствию поддерживает детализацию, позволяющую определить, на каких устройствах требуется конкретное обновление программного обеспечения Office 365. Чтобы просмотреть список устройств, требуется разрешение на просмотр обновлений и коллекций, к которым относятся устройства. Чтобы детализировать список устройств, сделайте следующее.

1. Выберите **Библиотека программного обеспечения** > **Управление клиентами Office 365** > **Обновления Office 365**.
1. Выберите любое обновление, которое требуется по крайней мере на одном устройстве.
1. Перейдите на вкладку **Сводка** и найдите круговую диаграмму в разделе **Статистика**.
1. Для детализации по списку устройств щелкните гиперссылку **Просмотреть обязательные** рядом с круговой диаграммой.
1. В результате откроется временный узел в разделе **Устройства**, в котором представлены устройства, требующие обновления. В узле также можно выполнить такие действия, как создание коллекции на основе списка.


## <a name="deploy-office-365-updates"></a>Развертывание обновлений Office 365

Используйте следующие процедуры для развертывания обновлений Office 365 с помощью Configuration Manager.

1. [Проверьте требования](/DeployOffice/manage-updates-to-office-365-proplus-with-system-center-configuration-manager#requirements-for-using-configuration-manager-to-manage-office-365-client-updates) для использования Configuration Manager для управления обновлениями клиента Office 365 в разделе **Требования к использованию Configuration Manager для управления обновлениями клиента Office 365** этой статьи.  

2. [Настройте точки обновления программного обеспечения](../get-started/configure-classifications-and-products.md) для синхронизации обновлений клиента Office 365. Настройте классификацию **Обновления** и выберите **Клиент Office 365** в качестве продукта. Настроив точки обновления программного обеспечения, синхронизируйте обновления для использования классификации **Обновления**.
3. Разрешите клиентам Office 365 получать обновления из Configuration Manager. Для включения клиента используйте параметры клиента Configuration Manager или групповую политику.

    **Способ 1**. Начиная с версии 1606 Configuration Manager для управления агентом клиента Office 365, можно использовать параметр клиента Configuration Manager. После настройки этого параметра и развертывания обновлений Office 365 агент клиента Configuration Manager взаимодействует с агентом клиента Office 365 для скачивания обновлений из точки распространения и их установки. Configuration Manager принимает данные инвентаризации параметра агента клиента Office 365 профессиональный плюс.    

      1. В консоли Configuration Manager щелкните **Администрирование** > **Обзор** > **Параметры клиента**.  

      2. Откройте соответствующие параметры устройства, чтобы включить агент клиента. Дополнительные сведения о параметрах клиента по умолчанию и настраиваемых параметрах см. в разделе [Настройка параметров клиента](../../core/clients/deploy/configure-client-settings.md).  

      3. Щелкните **Обновления программного обеспечения** и выберите **Да** для параметра **Включить управление агентом клиента Office 365**.  

    **Способ 2**.  [Включение получения обновлений для клиентов Office 365](/DeployOffice/manage-updates-to-office-365-proplus-with-system-center-configuration-manager#BKMK_EnableClient) в Configuration Manager с помощью групповой политики или средства развертывания Office.  

4. [Разверните обновления Office 365](deploy-software-updates.md) на клиентах.

> [!Important]
> - Начиная с версии 1706 Configuration Manager, обновления клиента Office 365 перемещены на узел **Управление клиентами Office 365** >**Обновления Office 365**. Это перемещение не повлияет на вашу текущую конфигурацию ADR. 
> - До версии Configuration Manager 1610 необходимо скачать и развернуть обновления для всех языков, настроенных в клиентах Office 365. Предположим, у вас есть клиент Office 365 с языками en-us и de-de. На сервере сайта вы скачиваете и развертываете актуальное обновление Office 365 только для языка en-us. Когда пользователь запускает установку из центра программного обеспечения для этого обновления, оно зависает на этапе скачивания содержимого для языков de-de. 

> [!NOTE]  
>
> Если, вы недавно установили Office 365 профессиональный плюс, возможно, канал обновления еще не настроен. Это также может зависеть от способа установки. В этом случае развернутые обновления будут определяться как неприменимые. При установке Office 365 профессиональный плюс создается [запланированная задача автоматического обновления](https://docs.microsoft.com/deployoffice/overview-of-the-update-process-for-office-365-proplus). В этом случае задачу нужно выполнить хотя бы один раз, чтобы настроить канал обновления для набора и чтобы обновления определялись как применимые.
>
> Если вы недавно установили Office 365 профессиональный плюс, и развернутые обновления не обнаружены, для проверки можно вручную запустить задачу автоматического обновления Office и затем на клиенте запустить [цикл оценки развертывания обновлений программного обеспечения](../understand/software-updates-introduction.md#scan-for-software-updates-compliance-process). Инструкции по выполнению этого обновления в последовательности задач см. в статье [Управление Office 365 профессиональный плюс с помощью Configuration Manager](manage-office-365-proplus-updates.md#updating-office-365-proplus-in-a-task-sequence).

## <a name="restart-behavior-and-client-notifications-for-office-365-updates"></a>Перезапуск и клиентские уведомления об обновлениях Office 365
При развертывании обновления для клиента Office 365 перезапуск и отправка клиентских уведомлений происходят по-разному в зависимости от используемой версии Configuration Manager. Следующая таблица содержит сведения об изменениях в пользовательском интерфейсе во время получения клиентом обновлений Office 365:

|Версия Configuration Manager |Взаимодействие с конечным пользователем|  
|----------------|---------------------|
|1706, 1710|Перед установкой обновления клиент получает всплывающее уведомление и уведомление в приложении, а также открывается диалоговое окно с обратным отсчетом.|
|1802| Перед установкой обновления клиент получает всплывающее уведомление и уведомление в приложении, а также открывается диалоговое окно с обратным отсчетом. </br>Если во время применения обновления клиента Office 365 выполняются какие-либо приложения Office 365, их невозможно принудительно закрыть. Установка обновления будет требовать перезапуска системы. <!--510006-->|


> [!Important]
>
>В Configuration Manager версии 1706 обратите внимание на следующее:
>
>- Для необходимых приложений, у которых крайний срок наступает в течение следующих 48 часов, а содержимое обновления скачано, в области уведомлений на панели задач отображается значок уведомления. 
>- Для необходимых приложений, у которых крайний срок наступает в течение следующих 7,5 часов, а обновление скачано, отображается диалоговое окно обратного отсчета. До наступления крайнего срока пользователь может до трех раз закрыть это диалоговое окно, отложив обратный отчет. Если операция отложена, обратный отсчет отображается снова через два часа. Если операция не отложена, выполняется 30-минутный обратный отсчет, по завершении которого устанавливается обновление.
>- Всплывающее уведомление может не отображаться, пока пользователь не щелкнет значок в области уведомлений. Кроме того, если область уведомлений имеет минимальный размер, значок может не отображаться, пока пользователь не откроет или не развернет эту область. 
>- Пока пользователь не работает на устройстве, выводится уведомление с диалоговым окном обратного отсчета. Например, если устройство заблокировано на ночь, возможно, что запущенные на устройстве приложения Office могут быть принудительно закрыты, чтобы установить обновление. Перед закрытием приложения система Office сохраняет его данные, чтобы предотвратить их потерю. 
>- Если крайний срок уже прошел или для него настроено минимально возможное значение, запущенные приложения Office могут быть закрыты без уведомления. 
>- Если пользователь устанавливает обновление Office до наступления крайнего срока, Configuration Manager подтверждает его установку при достижении крайнего срока. Если обновление на устройстве не обнаружено, оно устанавливается. 
>- Панель уведомления в приложении не отображается в приложении Office, выполняемом перед скачиванием обновления. После скачивания обновления уведомление в приложении отображается только для вновь открытых приложений.
>- При установке обновлений Microsoft Office, активируемых в период обслуживания или запланированных на нерабочее время, приложения Office могут быть закрыты без уведомления. 
>- Дополнительные сведения см. в статье [Уведомления об обновлениях для конечных пользователей в Office 365](https://docs.microsoft.com/deployoffice/end-user-update-notifications-for-office-365-proplus).


## <a name="add-languages-for-office-365-update-downloads"></a><a name="bkmk_o365_lang"></a> Скачивание обновлений для поддержки добавления языков для Office 365
В Configuration Manager можно добавить поддержку скачивания обновлений для любых языков, поддерживаемых Office 365.

### <a name="download-updates-for-additional-languages-in-version-1902"></a>Скачивание обновлений для поддержки дополнительных языков в версии 1902
<!--3555955-->

Начиная с Configuration Manager версии 1902 рабочий процесс обновления отделяет 38 языков для **Центра обновления Windows** от большого количества дополнительных языков для **обновления клиента Office 365**.

Выбрать нужные языки можно на странице **Выбор языка** в следующих расположениях.
- Мастер создания правил автоматического развертывания
- Мастер развертывания обновлений программного обеспечения
- Мастер скачивания обновлений программного обеспечения
- Свойства правил автоматического развертывания

На странице **Выбор языка** выберите раздел **обновления клиента Office 365** и щелкните **Изменить**. Добавьте необходимые языки для Office 365, а затем нажмите кнопку **ОК**.

![Снимок экрана: добавление языков для Office 365](media/office-update-languages-selection.png)

### <a name="to-add-support-to-download-updates-for-additional-languages-in-version-1810-and-earlier"></a>Добавление поддержки скачивания обновлений для дополнительных языков в версии 1810 и ниже

Выполните описанную ниже процедуру на точке обновления программного обеспечения на сайте центра администрирования или автономном первичном сайте.

> [!IMPORTANT]  
> Настройка дополнительных языков для обновлений Office 365 действует в пределах всего сайта. Когда вы добавите языки с помощью описанной ниже процедуры, все обновления Office 365 будут скачиваться на этих языках, а также на языках, выбранных на странице **Выбор языка** в мастере скачивания обновлений программного обеспечения или мастере развертывания обновлений программного обеспечения.

1. В командной строке выполните команду *wbemtest* с правами администратора, чтобы открыть тестер инструментария управления Windows.
2. Щелкните **Подключиться** и введите *root\sms\site_&lt;код_сайта&gt;* .
3. Щелкните **Запрос** и выполните следующий запрос: *select &#42; from SMS_SCI_Component where componentname ="SMS_WSUS_CONFIGURATION_MANAGER"*  
   ![Запрос WMI](../media/1-wmiquery.png)
4. В области результатов дважды щелкните объект с кодом сайта для сайта центра администрирования или автономного первичного сайта.
5. Выберите свойство **Props**, щелкните **Изменить свойство**, а затем щелкните **Встроенные**.
   ![Редактор свойств](../media/2-propeditor.png)
6. Начиная с первого результата запроса откройте каждый объект, пока не найдете тот, свойство **PropertyName** которого имеет значение **AdditionalUpdateLanguagesForO365**.
7. Выберите **Value2** и щелкните **Изменить свойство**.  
   ![Изменение свойства Value2](../media/3-queryresult.png)
8. Добавьте дополнительные языки в свойство **Value2** и щелкните **Сохранить свойство**. <br/> Например, добавьте pt-pt (португальский — Португалия), af-za (африкаанс — ЮАР), nn-no (норвежский (нюнорск) — Норвегия) и т. д. Для этих языков введите `pt-pt,af-za,nn-no`. Не используйте пробелы между названиями языков.
 
   ![Добавление языков в редакторе свойств](../media/4-props.png)  
9. Нажмите кнопку **Закрыть**, нажмите кнопку **Закрыть**, щелкните **Сохранить свойство**, а затем — **Сохранить объект** (если здесь нажать кнопку **Закрыть**, значения удаляются). Нажмите кнопку **Закрыть**, а затем — **Выйти**, чтобы закрыть тестер инструментария управления Windows.
10. В консоли Configuration Manager последовательно выберите **Библиотека программного обеспечения** > **Обзор** > **Управление клиентом Office 365** > **Обновления Office 365**.
11. Теперь обновления Office 365 будут скачиваться на языке, выбранном в мастере, и языках, настроенных с помощью этой процедуры. Чтобы убедиться в том, что обновления скачиваются на нужных языках, перейдите к источнику пакета обновления и найдите файлы с кодом языка в имени.  
    ![Имена файлов для дополнительных языков](../media/5-verification.png)

## <a name="updating-office-365-proplus-in-a-task-sequence"></a>Обновление Office 365 профессиональный плюс в последовательности задач
При использовании шага последовательности задач по [установке обновления программного обеспечения](../../osd/understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates) Office 365 развернутые обновления могут определяться как неприменимые.  Это может произойти, если запланированная задача автоматического обновления Office еще ни разу не запускалась (см. примечание в разделе [Развертывание обновлений Office 365](manage-office-365-proplus-updates.md#deploy-office-365-updates)), например, если вы установили Office 365 профессиональный плюс непосредственно перед выполнением этого шага.

Чтобы настроить канал обновления для правильного определения развернутых обновлений, используйте один из следующих способов:

**Способ 1**.
1. На компьютере с той же версией Office 365 профессиональный плюс откройте планировщик задач (taskschd.msc) и найдите задачу автоматического обновления Office 365. Как правило, она находится в разделе **Библиотека планировщика заданий** >**Microsoft**>**Office**.
2. Щелкните правой кнопкой мыши задачу автоматического обновления и выберите пункт **Свойства**.
3. Перейдите на вкладку **Действия** и щелкните **Изменить**. Скопируйте команду и все ее аргументы. 
4. Измените последовательность задач в консоли Configuration Manager.
5. Добавьте новый шаг **Выполнить из командной строки** перед шагом **Установить обновления программного обеспечения** в последовательности задач. Если Office 365 профессиональный плюс устанавливается как часть той же последовательности задач, убедитесь, что этот шаг выполняется после установки Office.
6. Вставьте команду и аргументы, которые были скопированы из запланированной задачи автоматического обновления Office. 
7. Нажмите кнопку **ОК**. 

**Способ 2**.
1. На компьютере с той же версией Office 365 профессиональный плюс откройте планировщик задач (taskschd.msc) и найдите задачу автоматического обновления Office 365. Как правило, она находится в разделе **Библиотека планировщика заданий** >**Microsoft**>**Office**.
2. Измените последовательность задач в консоли Configuration Manager.
3. Добавьте новый шаг **Выполнить из командной строки** перед шагом **Установить обновления программного обеспечения** в последовательности задач. Если Office 365 профессиональный плюс устанавливается как часть той же последовательности задач, убедитесь, что этот шаг выполняется после установки Office.
4. В поле командной строки введите командную строку, которая будет выполнять запланированную задачу. Просмотрите пример ниже и убедитесь, что в строке в кавычках указаны те же путь и имя задачи, которые были определены на шаге 1.  

    Пример: `schtasks /run /tn "\Microsoft\Office\Office Automatic Updates 2.0"`
5. Нажмите кнопку **ОК**. 

## <a name="change-the-update-channel-after-you-enable-office-365-clients-to-receive-updates-from-configuration-manager"></a><a name="bkmk_channel"></a> Изменение канала обновления после предоставления клиентам Office 365 разрешения на получение обновлений из Configuration Manager

После развертывания Office 365 профессиональный плюс можно изменить канал обновления с помощью групповой политики или средства развертывания Office (ODT). Например, можно переместить устройство из Semi-Annual Channel в Semi-Annual Channel (Targeted). При изменении канала Office обновляется автоматически без необходимости переустановки или загрузки полной версии. Дополнительные сведения см. в разделе [Изменение канала обновления Office 365 профессиональный плюс для устройств в организации](https://docs.microsoft.com//deployoffice/change-update-channels).


## <a name="next-steps"></a>Дальнейшие шаги

На панели мониторинга для управления клиентами Office 365 в Configuration Manager можно просматривать сведения о клиенте Office 365 и развертывать приложения Office 365. Дополнительные сведения см. в руководстве по [панели мониторинга для управления клиентами Office 365](office-365-dashboard.md).