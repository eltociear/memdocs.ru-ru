---
title: Technical Preview 1804
titleSuffix: Configuration Manager
description: Сведения о новых возможностях, доступных в версии Technical Preview 1804 для Configuration Manager.
ms.date: 05/21/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8af43618-ec60-4c3e-a007-12399d1335b9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: b709d6ec0c0cda188502c314d945a70e8de71288
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/07/2020
ms.locfileid: "82905250"
---
# <a name="capabilities-in-technical-preview-1804-for-configuration-manager"></a>Возможности в Technical Preview 1804 для Configuration Manager

*Область применения: Configuration Manager (ветвь Technical Preview)*

Эта статья содержит сведения о функциях, доступных в версии 1804 Technical Preview для Configuration Manager. Эту версию можно установить для обновления и добавления новых возможностей в версию Technical Preview сайта. 

Перед установкой этого обновления ознакомьтесь со статьей, посвященной версии [Technical Preview](technical-preview.md). Там приведены общие требования и ограничения на использование ознакомительной технической версии, а также сведения о том, как выполнять обновления и оставлять отзывы.     


<!--  Known Issues Template   -->
## <a name="known-issues-in-this-technical-preview"></a>Известные проблемы в этой версии Technical Preview

### <a name="setup-link-to-download-updates-not-working"></a><a name="bkmk_ki-prereqs"></a> Ссылка в программе установки на скачивание обновлений не работает
<!--514334-->
При запуске программы установки с носителя на начальной странице отображается ссылка **Получить последние обновления Configuration Manager**, которая не работает в этом выпуске. По этой ссылке скачиваются файлы, необходимые для установки.

#### <a name="workaround"></a>Обходной путь
Чтобы скачать эти файлы, запустите мастер установки. На странице скачивания необходимых компонентов **скачайте требуемые файлы**. 


### <a name="the-application-catalog-web-service-point-cant-be-https-enabled"></a><a name="bkmk_appcathttps"></a> Точка веб-службы каталога приложений не поддерживает протокол HTTPS
<!--512637-->
Если точка веб-службы каталога приложений не поддерживает протокол HTTPS, тогда

- приложения, развернутые как доступные пользователям, больше не показываются в центре программного обеспечения.  

- В файле awebsctl.log отображается следующая ошибка:  

     `Call to HttpSendRequestSync failed for port 443 with status code 500, text: Internal Server Error`

#### <a name="workaround"></a>Обходной путь
Перенастройте точку веб-службы каталога приложений для связи с использованием протокола HTTP.  




</br>

**Ниже перечислены новые возможности, доступные в этой версии.**  


## <a name="configure-a-remote-content-library-for-the-site-server"></a>Настройка библиотеки удаленного содержимого на сервере сайта  
<!--1357525-->
Чтобы освободить место на жестком диске на первичном сервере сайта, переместите его [библиотеку содержимого](../plan-design/hierarchy/the-content-library.md) в другое место хранения. Можно переместить библиотеку содержимого на другой диск на сервере сайта, на отдельный сервер или отказоустойчивые диски в сети хранения данных (SAN). Рекомендуется использовать сеть SAN, поскольку она обеспечивает эластичное хранение, которое со временем растет или сжимается для удовлетворения ваших изменяющихся требований к содержимому. 

Эта библиотека удаленного контента является новым предварительным условием для [роли сервера сайта высокой доступности](capabilities-in-technical-preview-1706.md#site-server-role-high-availability). 

> [!Note]  
> Это действие перемещает на сервер сайта только библиотеку содержимого. Это не влияет на расположение библиотеки содержимого в точках распространения. 

### <a name="prerequisites"></a>Предварительные условия  
- Учетной записи компьютера сервера сайта необходимы разрешения сетевого пути, к которому перемещается библиотека содержимого, на **чтение** и **запись**. В удаленной системе компоненты не установлены. 

### <a name="try-it-out"></a>Попробуйте!
 Попробуйте выполнить следующие задачи, Затем отправьте [отзыв](#bkmk_feedback) с уведомлением о полученном результате.

1. В консоли Configuration Manager перейдите в рабочую область **Администрирование**. Разверните узлы **Конфигурация сайта** и выберите **Сайты**. На вкладке **Сводка** в нижней части области сведений обратите внимание на новый столбец для **библиотеки содержимого**.  

2. Нажмите кнопку **Управление библиотекой контента** на ленте.  

3. Выберите **в общей сетевой папке** и введите допустимый сетевой путь. Этот путь — это место, куда сайт перемещает библиотеку содержимого. Нажмите кнопку **ОК**.  

4. Обратите внимание на свойство **Состояние** в столбце библиотеки содержимого на панели сведений. Оно обновляется, показывая процесс перемещения библиотеки содержимого сайта. В процессе выполнения отображается процент завершения. При возникновении состояния ошибки отображается ошибка. К распространенным ошибкам относится `access denied` или `disk full`. По завершении работы отображается `OK`. Подробные сведения см. в файле **distmgr.log**. Дополнительные сведения см. в разделе [Журналы сервера сайта и сервера системы сайта](../plan-design/hierarchy/log-files.md#BKMK_SiteSiteServerLog).  

Если нужно переместить библиотеку содержимого обратно на сервер сайта, повторите этот процесс, но выберите вариант **Локальный сервер сайта**.  

> [!Tip]  
> Чтобы переместить содержимое на другой диск на сервере сайта, используйте средство **переноса библиотеки содержимого**. Дополнительные сведения см. в разделе [Набор инструментов Configuration Manager](#configuration-manager-toolkit).  



## <a name="submit-feedback-from-the-configuration-manager-console"></a><a name="bkmk_feedback"></a> Отправка отзывов из консоли Configuration Manager  
<!--1357542-->

Отправьте смайлик! Теперь можно напрямую сообщить команде Configuration Manager о полученном опыте работы. Из консоли Configuration Manager несложно отправлять отзывы. Команда разработчиков будет рада услышать все ваши отзывы: похвалы, проблемы и предложения.  

### <a name="try-it-out"></a>Попробуйте!
 Попробуйте выполнить следующие задачи, Затем отправьте **отзыв** с уведомлением о полученном результате.  

1. В консоли Configuration Manager нажмите кнопку смайлика в верхнем правом углу над лентой.  

2. В раскрывающемся списке выберите один из доступных вариантов:  

   - **Отправить смайлик**: если вам действительно что-нибудь понравилось! Для этого параметра введите подробности вашего отзыва. Затем при желании добавьте снимок экрана и адрес электронной почты.  

   - **Отправить нахмуренный смайлик**: если произошла ошибка в консоли или что-то не работает должным образом. Для этого параметра введите сведения о потенциальных неполадках. Затем при желании добавьте снимок экрана, адрес электронной почты и диагностические данные.  

   - **Отправить предложение**: если у вас есть идея, как изменить и улучшить Configuration Manager. Этот параметр открывает сайт [UserVoice](https://configurationmanager.uservoice.com) в вашем веб-браузере.  

Эти отзывы переходят непосредственно к команде разработчиков Майкрософт для Configuration Manager. Хотя центр обратной связи Windows 10 по-прежнему поддерживается, настоятельно рекомендуется использовать механизм передачи отзывов в консоли.  

Следующая анонимная информация всегда включена в содержимое отзыва:  

- Версия и язык консоли Configuration Manager  

- Версия сайта Configuration Manager  

- Идентификатор для службы поддержки, также известный как идентификатор иерархии  

- Версия ОС и язык для системы, на которой работает консоль  

- Точное расположение в консоли, из которой была нажата кнопка смайлик  

Эти данные соответствуют набору наших данных диагностики и использования. Дополнительные сведения см. в статье [Данные о диагностике и использовании](../plan-design/diagnostics/diagnostics-and-usage-data.md).

### <a name="known-issues"></a>Известные проблемы

При попытке отправить отзыв с устройства, которое не может получить доступ в Интернет, приложение может неожиданно закрыться. Для отправки одобрения или неодобрения убедитесь, что устройство имеет доступ к сайту petrol.office.microsoft.com.



## <a name="support-center"></a>Центр поддержки
<!--1357489-->

Используйте Центр поддержки для устранения неполадок клиента, просмотра журнала в режиме реального времени или записи состояния компьютера клиента Configuration Manager для последующего анализа. Центр поддержки — это единый инструмент, консолидирующий многие инструменты администратора для устранения неполадок. Предварительный просмотр последней версии Центра поддержки с исправлениями ошибок, улучшениями и предварительным просмотром нашего нового средства просмотра журналов доступен в техническом предпросмотре. Установщик Центра поддержки находится на сервере сайта в папке **cd.latest\SMSSETUP\Tools\SupportCenter**.


### <a name="new-support-center-features"></a>Новые компоненты Центра поддержки  

- Новое средство просмотра журналов OneTrace. Оно работает аналогично CMTrace и включает усовершенствования, такие как представление с вкладками и закрепляемые окна.  

- Новая функция сборщика данных собирает журналы диагностики из локального или удаленного клиента Configuration Manager. Она предоставляет в реальном времени диагностику инвентаря (заменяет Client Spy), политики (заменяет Policy Spy) и кэша клиента.  



## <a name="configuration-manager-toolkit"></a>Набор инструментов Configuration Manager
<!--1357145-->

Сервер и средства клиента Configuration Manager теперь включены в Technical Preview. Найдите их на сервере сайта в папке **cd.latest\SMSSETUP\Tools**. Больше никакой установки не требуется.

#### <a name="server-tools"></a>Серверные инструменты  

- **Диспетчер заданий точки распространения**: устраняет неполадки с заданием распространения содержимого в точках распространения  

- **Средство просмотра оценки коллекции**: просмотр сведений об оценке коллекции  

- **Проводник библиотеки содержимого**: просмотр содержимого хранилища отдельных экземпляров библиотеки содержимого  

- **Перенос содержимого библиотеки**: перенос содержимого библиотеки между дисками  

- **Средство владения содержимым**: изменение права собственности на потерянные пакеты. Эти пакеты существуют на сайте без собственного сервера сайта.  

- **Средство ролевого администрирования и аудита**: помогает администраторам настроить роли для аудита  

#### <a name="client-tools"></a>Клиентские инструменты

- **CMTrace**: просмотр журналов  

- **Средство наблюдения за развертыванием**: устранение неполадок с приложениями, обновлениями и развертываниями базовых шаблонов  

- **Средство Policy Spy**: просмотр назначений политик  

- **Средство Power Viewer**: просмотр состояния функции управления питанием  

- **Средство для работы с расписанием отправок**: создание расписаний триггеров и оценок базовых показателей управления требуемой конфигурацией  

> [!Important]  
> [Центр поддержки](#support-center) рекомендуется для использования в большинстве случаев, поскольку он включает в себя те же или улучшенные функции для следующих инструментов.  
> - Client Spy
> - CMTrace<sup>1</sup> 
> - Средство наблюдения за развертыванием
> - Policy Spy
> - Средство расписания отправок
> 
> <sup>1</sup> CMTrace не зависит от .NET или Windows Presentation Foundation (WPF), поэтому оно по-прежнему используется в загрузочных образах Windows PE.

### <a name="known-issues"></a>Известные проблемы
Во время запуска некоторые клиентские и серверные средства могут неожиданно завершить работу. Данная проблема вызвана отсутствующим файлом на носителе. Чтобы обойти ее, скопируйте файл **Microsoft.Diagnostics.Tracing.EventSource.dll** из каталога AdminConsole\bin в каталоги SMSSETUP\Tools\ClientTools и ServerTools. Этот файл должен иметь ту же версию, которую использует консоль Configuration Manager. Другие версии могут не работать. <!--513977-->



## <a name="uninstall-application-on-approval-revocation"></a>Удаление приложения при отзыве одобрения
<!--1357891-->

При отмене одобрения приложения реакция на событие изменилась. Теперь, когда вы отклоняете запрос для приложения, клиент удаляет приложение с устройства пользователя. 

### <a name="prerequisites"></a>Предварительные условия
- Включить функцию **Утверждение запросов приложений для пользователей на каждом устройстве**.

### <a name="try-it-out"></a>Попробуйте!
 Попробуйте выполнить следующие задачи, Затем отправьте [отзыв](#bkmk_feedback) с уведомлением о полученном результате.

1. В консоли Configuration Manager разверните приложение, требующее утверждения пользователя. На вкладке **Параметры развертывания** включите параметр: **Администратор должен утвердить запрос для этого приложения на устройстве**.  

2. В центре программного обеспечения клиента Configuration Manager пользователь запрашивает разрешение на установку приложения.  

3. В консоли Configuration Manager утвердите запрос для этого пользователя установить приложение на устройстве. Запросы на утверждение приложений отображаются в рабочей области **Библиотека программного обеспечения** в разделе **Управление приложениями** в узле **Запросы утверждения**.  

4. В центре программного обеспечения на стороне клиента пользователь устанавливает приложение.  

5. В консоли Configuration Manager отклоните запрос пользователя для приложения на устройстве.  

### <a name="known-issues"></a>Известные проблемы
- После установки приложения на стороне клиента обновите политику пользователя. В центре программного обеспечения переключитесь на вкладку **Параметры**, раскройте окно **Обслуживание компьютера** и нажмите кнопку **Политика синхронизации**.<!--480609-->  

- Точка веб-службы каталога приложений должна быть HTTP. Дополнительные сведения см. в разделе [Известные проблемы в этой версии Technical Preview](#bkmk_appcathttps).<!--512637-->  



## <a name="exclude-active-directory-containers-from-discovery"></a>Исключение контейнеров Active Directory из обнаружения
<!--1358143-->
Чтобы сократить количество обнаруженных объектов, теперь можно исключать определенные контейнеры из обнаружения систем Active Directory. Эта функция является результатом [отзывов с UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8414520-exclude-virtual-cluster-and-ou-from-discovery).

### <a name="try-it-out"></a>Попробуйте!
 Попробуйте выполнить следующие задачи, Затем отправьте [отзыв](#bkmk_feedback) с уведомлением о полученном результате.

1. В консоли Configuration Manager перейдите к рабочей области **Администрирование**. Разверните **Конфигурацию иерархии** и выберите **Методы обнаружения**. Выберите **Обнаружение систем Active Directory** и нажмите кнопку **Свойства** на ленте.  

2. Щелкните значок "Создать", чтобы задать новый контейнер Active Directory.   

3. В диалоговом окне "Контейнер Active Directory" для запуска обнаружения найдите или введите **путь** в разделе "Расположение".  

4. В разделе "Параметры поиска" включите параметр для **выполнения рекурсивного поиска дочерних контейнеров Active Directory**. Затем нажмите кнопку **Добавить**, чтобы выбрать подконтейнеры, которые будут исключены из этого обнаружения.  

5. В диалоговом окне "Выберите новый контейнер" выберите дочерний контейнер для исключения. Нажмите кнопку **ОК**, чтобы закрыть диалоговое окно "Выберите новый контейнер".  

6. Нажмите кнопку **ОК**, чтобы закрыть диалоговое окно "Контейнер Active Directory".  

7. В окне "Свойства обнаружения систем Active Directory" посмотрите путь к контейнеру Active Directory, с которого начинается обнаружение. В столбце **Рекурсивный** отображается **Да**, и в новом столбце **Имеет исключения** также отображается **Да**. Нажмите кнопку **ОК**, чтобы закрыть окно "Свойства обнаружения систем Active Directory".  



## <a name="specify-the-visibility-of-the-application-catalog-website-link-in-software-center"></a>Указание видимости ссылки на веб-сайт каталога приложений в центре программного обеспечения
<!--1358214-->

Теперь можно управлять тем, будет ли ссылка **Откройте веб-сайт каталога приложений** отображаться в узле **Состояние установки** Центра программного обеспечения.  

> [!Note]  
> Поддержка веб-сайта пользователей каталога приложений завершится после первого обновления, которое будет выпущено после 1 июня 2018 года. Дополнительные сведения см. в разделе [Удаленные и устаревшие компоненты](../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).  

### <a name="try-it-out"></a>Попробуйте!
 Попробуйте выполнить следующие задачи, Затем отправьте [отзыв](#bkmk_feedback) с уведомлением о полученном результате.

1. В консоли Configuration Manager на узле **Параметры клиентов** в рабочей области **Администрирование** создайте пользовательскую политику клиентского устройства.  

2. Выберите группу **Центр программного обеспечения**.  

3. В разделе **Параметры центра программного обеспечения** нажмите кнопку **Настроить**.  

4. Включите параметр **Скрыть ссылку на веб-сайт каталога приложений в центре программного обеспечения**.   

Дополнительные сведения о параметрах клиентов см. в разделе [Настройка параметров клиентов](../clients/deploy/configure-client-settings.md).




## <a name="filter-automatic-deployment-rules-by-software-update-architecture"></a>Фильтрация правил автоматического развертывания с помощью архитектуры обновления программного обеспечения
 <!--1322266-->
Теперь можно фильтровать правила автоматического развертывания, чтобы исключить архитектуры Itanium и ARM64.

### <a name="try-it-out"></a>Попробуйте!
Попробуйте выполнить следующие задачи, Затем отправьте [отзыв](#bkmk_feedback) с уведомлением о полученном результате.

1. В консоли Configuration Manager перейдите к рабочей области **Библиотеки программного обеспечения**. Разверните **Обновления программного обеспечения** и выберите **Правила автоматического развертывания**. На ленте выберите **Создать правило автоматического развертывания**.  

2. Заполните соответствующие параметры для вкладок **Общие** и **Параметры развертывания**.  

3. Во вкладке **Обновления программного обеспечения** выберите **Архитектура** и затем нажмите **Элементы для поиска** в разделе **Условия поиска**.  

4. Выберите архитектуры, которые необходимо включить в правило автоматического развертывания.  

5. Нажмите кнопку **Далее** и приступите к созданию правила автоматического развертывания.  

> [!IMPORTANT]  
> Помните, что существуют 32-разрядные (x86) приложения и компоненты, работающие в 64-разрядных (x64) системах. Если вы не уверены, что поддержка x86-приложений не нужна, то включите ее, как и при выборе x64-приложений.  

### <a name="known-issues"></a>Известные проблемы
После добавления критериев архитектуры на странице свойств правила автоматического развертывания в критериях поиска отображается **Название**. Правило автоматического развертывания по-прежнему работает должным образом и выбирает правильные обновления программного обеспечения. Тем не менее нельзя включать оба критерия, **Архитектура** и **Название**, в данный момент. <!--512634,512632-->



## <a name="improvements-to-os-deployment"></a>Улучшение развертывания операционной системы
Мы улучшили процедуру развертывания операционной системы, приняв во внимание ваши отзывы, отправленные через систему User Voice.  

- [Маскировка конфиденциальных данных, хранимых в переменных последовательности задач](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/15282795-secret-task-sequence-variable-value-exposed): на шаге [Задать переменную последовательности задач](../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) выберите новый параметр **Не показывать это значение**. Например, при указании пароля.<!--1358330--> При включении этого параметра применяются следующие варианты поведения.
  - Значение переменной не отображается в smsts.log.
  - Консоль Configuration Manager и поставщик SMS обрабатывают это значение так же, как и другие секретные данные, такие как пароли.
  - Значение не включается при экспорте последовательности задач.
  - Редактор последовательности задач не считывает это значение при редактировании шага. Для внесения изменений повторно введите все значения.

  > [!Important]  
  > Переменные и их значения сохраняются с последовательностью задач как файл XML и маскируются в базе данных. Когда клиент запрашивает политику последовательности задач из точки управления, она зашифровывается в пути и хранится на стороне клиента. Однако все значения переменных являются обычным текстом в среде последовательности задач в памяти во время выполнения на стороне клиента. Если последовательность задач включает шаг для вывода значения переменной, этот вывод данных находится в виде простого текста. Это поведение требует явного действия администратора для включения такого шага в последовательность задач. 


- [Маскировка имени программы во время шага "Выполнить команду" последовательности задач](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/15282795-secret-task-sequence-variable-value-exposed): чтобы предотвратить отображение или регистрацию потенциально конфиденциальных данных, присвойте переменной последовательности задач **OSDDoNotLogCommand** значение `TRUE`. Эта переменная маскирует имя программы в файл smsts.log во время [выполнения из командной строки](../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine) шага последовательности задач. <!--1358493-->  



## <a name="improvements-to-the-configuration-manager-console"></a>Усовершенствования в консоли Configuration Manager
- Основная информация о пользователе теперь отображается при просмотре элементов коллекции в разделах **Ресурсы и соответствие**, **Коллекции устройств**.<!--510252-->  



## <a name="next-steps"></a>Дальнейшие шаги
Сведения об установке или обновлении ветви Technical Preview см. в статье [Technical Preview для Configuration Manager](technical-preview.md).    
