---
title: Отслеживание применения приложений с помощью функции контроля использования программных продуктов
titleSuffix: Configuration Manager
description: Сведения об операциях, доступных в контроле использования программных продуктов Configuration Manager.
ms.date: 09/20/2017
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: b1fdaee2-2816-4447-94cd-609f6948f215
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 13d8cce1811c4a27f6a3e7485eea4d65132c2888
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689252"
---
# <a name="software-metering-in-configuration-manager"></a>Контроль использования программных продуктов в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Этот раздел содержит справочные сведения о всех операциях, которые вы можете выполнять при работе с контролем использования программных продуктов в Configuration Manager.

> [!IMPORTANT]
>  Контроль использования программных продуктов применяется для отслеживания классических приложений Windows с расширением **EXE**. Контроль использования программных продуктов не отслеживает современные приложения Windows (например, те, которые используются операционной системой Windows 8).

##  <a name="prerequisites-for-software-metering"></a>Необходимые условия для контроля использования программных продуктов
Контроль использования программных продуктов не имеет внешних зависимостей — только зависимости внутри продукта.

|Зависимость|Дополнительные сведения|
|----------------|----------------------|
|Параметры клиентов для контроля использования программных продуктов.|Для применения функции контроля использования программных продуктов параметр клиента **Включить отслеживание использования программного обеспечения для клиентов** должен быть включен и развернут на компьютеры. Вы можете назначить параметры контроля использования программных продуктов всем компьютерам в иерархии или развернуть настраиваемые параметры в отдельные группы компьютеров. См. подраздел **Настройка отслеживания использования программного обеспечения** в этом разделе.|
|Точка служб отчетов.|Прежде чем можно будет просматривать отчеты по отслеживанию использования программного обеспечения, необходимо настроить точку служб отчетов. Дополнительные сведения см. в разделе [Общие сведения об отчетах](../../core/servers/manage/introduction-to-reporting.md).|

##  <a name="configure-software-metering"></a>Настройка контроля использования программных продуктов
 В ходе этой процедуры выполняется настройка стандартных параметров клиента для контроля использования программных продуктов и их применение ко всем компьютерам в иерархии. Если эти параметры требуется применить только к некоторым компьютерам, создайте настраиваемые параметры клиентского устройства и разверните их в коллекции, которая содержит необходимые компьютеры. Дополнительные сведения о создании настраиваемых параметров устройства см. в разделе [Настройка параметров клиента](../../core/clients/deploy/configure-client-settings.md).

1. В консоли Configuration Manager последовательно выберите **Администрирование** > **Параметры клиента** > **Параметры клиента по умолчанию**.

2. На вкладке **Главная** в группе **Свойства** нажмите кнопку **Свойства**.

3. В диалоговом окне **Параметры по умолчанию** щелкните **Отслеживание использования программного обеспечения**.

4. В списке **Параметры устройства** настройте следующие параметры.

   -   **Включить отслеживание использования программного обеспечения для клиентов**. Выберите **True**, чтобы включить отслеживание использования ПО.

   -   **Расписание сбора данных**. Настройте периодичность сбора данных для контроля использования ПО с клиентских компьютеров. Используйте значение по умолчанию ( **7 дней** ) или нажмите кнопку **Расписание** , чтобы настроить собственное расписание.

5. Нажмите кнопку **ОК** , чтобы закрыть диалоговое окно **Параметры по умолчанию** .

   Заданные параметры будут применены к клиентским компьютерам при следующем скачивании политики клиента. Сведения об инициации получения политик для отдельного клиента см. в разделе [Управление клиентами](../../core/clients/manage/manage-clients.md).

##  <a name="create-software-metering-rules"></a>Создание правил контроля использования программных продуктов
 Используйте мастер создания правила отслеживания использования программного обеспечения, чтобы создать правило контроля использования программных продуктов для сайта Configuration Manager.

1.  В консоли Configuration Manager выберите элемент **Активы и соответствие** > **Отслеживание использования программного обеспечения**.

3.  На вкладке **Домашняя страница** в группе **Создать** щелкните **Создать правило отслеживания использования программного обеспечения**.

4.  На странице **Общие** мастера создания правила отслеживания использования программного обеспечения укажите перечисленные ниже сведения.

    -   **Имя** — имя правила отслеживания использования программного обеспечения. Оно должно быть уникальным и описательным.

        > [!NOTE]
        >  Правила отслеживания использования программного обеспечения могут иметь одно и то же имя, если имя файла, который они содержат, отличается.

    -   **Имя файла** — имя файла программы, использование которой требуется контролировать. Можно нажать кнопку **Обзор** для отображения диалогового окна **Открыть** , в котором можно выбрать файл программы для использования.

        > [!NOTE]
        >  Если ввести имя исполняемого файла в поле **Имя файла** , не выполняются никакие проверки, чтобы определить наличие этого файла или содержание в нем необходимых данных заголовков. По возможности нажмите кнопку **Обзор** и выберите исполняемый файл, использование которого требуется контролировать.
        >
        >  Подстановочные знаки не допускаются в имени файла.
        >
        >  Это поле не является обязательным, если указано значение параметра **Исходное имя файла** .

    -   **Исходное имя файла** — имя исполняемого файла, использование которого требуется контролировать. Данное имя соответствует сведениям в заголовке файла, а не самому имени файла, поэтому указанный параметр рекомендуется использовать в случаях, когда исполняемый файл был переименован, но вам требуется контролировать его использование по исходному имени.

        > [!NOTE]
        >  Подстановочные знаки не допускаются в исходном имени файла.
        >
        >  Это поле не является обязательным, если указано значение параметра **Имя файла** .

    -   **Версия** — версия исполняемого файла, использование которого требуется контролировать. Можно использовать подстановочный знак (&#42;), чтобы представить любою строкй символов, или подстановочный знак (?), чтобы представить любой отдельный символ. Если требуется отслеживать использование всех версий исполняемого файла, выберите значение по умолчанию (&#42;).

    -   **Язык** — язык исполняемого файла, использование которого требуется отслеживать. Значением по умолчанию является текущий языковой стандарт используемой операционной системы. Если контролируемый исполняемый файл выбран с помощью кнопки **Обзор** , это поле заполняется автоматически при наличии сведений о языке в заголовке файла. Чтобы контролировать все языковые версии файла, в раскрывающемся списке выберите вариант **Любой** .

    -   **Описание** — необязательное описание правила отслеживания использования программного обеспечения.

    -   **Применить это правило отслеживания использования программного обеспечения к следующим клиентам** : выберите, следует ли применять правило контроля использования программных продуктов ко всем клиентам в иерархии или только к клиентам, назначенным сайту, указанному в списке **Сайт** .

5.  Чтобы продолжить, нажмите кнопку **Далее**.

6.  Просмотрите и подтвердите параметры, после чего завершите работу мастера, чтобы создать правило контроля использования программных продуктов. Новое правило контроля использования программных продуктов отображается в узле **Отслеживание использования программного обеспечения** рабочей области **Активы и соответствие** .

##  <a name="configure-automatic-software-metering-rules"></a>Настройка автоматического создания правил контроля использования программных продуктов
 Функция контроля использования программных продуктов Configuration Manager позволяет автоматически создавать отключенные правила контроля использования программных продуктов на основе данных последней инвентаризации, которые содержатся в базе данных сайта. Эти данные инвентаризации вы можете настроить таким образом, чтобы правила контроля использования программных продуктов создавались только для приложений, используемых на заданной доле компьютеров. Кроме того, можно указать максимальное число автоматически создаваемых правил отслеживания использования программного обеспечения, разрешенных для сайта.

> [!NOTE]
>  По умолчанию автоматически создаваемые правила контроля использования программных продуктов отключены. Прежде чем можно будет выполнять сбор данных об использовании, полученных с помощью этих правил, такие правила необходимо включить.

1.  В консоли Configuration Manager выберите **Активы и соответствие** > **Отслеживание использования программного обеспечения**, а затем на вкладке **Главная** в группе **Параметры** щелкните **Свойства отслеживания использования программного обеспечения**.

3.  В диалоговом окне **Свойства отслеживания использования программного обеспечения** настройте перечисленные ниже параметры.

    -   **Хранение данных (в днях)** : задает период, в течение которого созданные правилами контроля использования программных продуктов данные хранятся в базе данных сайта. Значение по умолчанию равно **90** дням.

    -   Установите флажок **Автоматически создавать отключенные правила отслеживания использования из данных последней инвентаризации использования**.

    -   **Укажите долю компьютеров в иерархии (в процентах), на которых должна быть использована программа, чтобы правило отслеживания использования программного обеспечения создавалось автоматически** — значение по умолчанию **10** процентов.

    -   **Укажите число правил отслеживания использования программного обеспечения, которое должно быть превышено в иерархии для отключения автоматического создания правил** — значение по умолчанию **100** правил.

4.  Нажмите кнопку **ОК** , чтобы закрыть диалоговое окно **Свойства отслеживания использования программного обеспечения** .

##  <a name="manage-software-metering-rules"></a>Управление правилами контроля использования программных продуктов
 В рабочей области **Активы и соответствие** выберите **Отслеживание использования программного обеспечения**, выберите нужное правило отслеживания использования программного обеспечения, затем выберите задачу управления.

 Для получения дополнительных сведений о задачах управления, которые могут требовать указания некоторой информации перед их выбором, используйте следующую таблицу.

|Задача управления|Сведения|
|---------------------|-------------|
|**Разрешить**<br /><br /> **Отключено**|Позволяет включить или отключить правило контроля использования программных продуктов. Этот параметр загружается на клиентские компьютеры в соответствии со значением параметра **Интервал опроса политики клиента** , настраиваемого в разделе **Политика клиента** параметров клиента. Значение по умолчанию составляет 60 минут.<br /><br /> См. раздел [Настройка параметров клиента](../../core/clients/deploy/configure-client-settings.md).|

##  <a name="monitor-software-metering"></a>Мониторинг контроля использования программных продуктов
 Функция контроля использования программных продуктов в Configuration Manager включает встроенные отчеты, которые позволяют отслеживать сведения об операциях контроля использования программных продуктов. Эти отчеты относятся к категории отчетов **Отслеживание использования программного обеспечения**.

 Дополнительные сведения о настройке отчетов в Configuration Manager см. в разделе [Общие сведения об отчетах](../../core/servers/manage/introduction-to-reporting.md).

 Дополнительно можно создавать запросы и коллекции на основе данных, сохраняемых в базе данных Configuration Manager функцией контроля использования программных продуктов.

 Дополнительные сведения о коллекциях в Configuration Manager см. в разделе [Общие сведения о коллекциях](../../core/clients/manage/collections/introduction-to-collections.md).

 Дополнительные сведения о запросах в Configuration Manager см. в разделе [Общие сведения о запросах](../../core/servers/manage/introduction-to-queries.md).

##  <a name="security-and-privacy-for-software-metering"></a>Безопасность и конфиденциальность контроля использования программных продуктов

### <a name="security-issues-for-software-metering"></a>Вопросы безопасности для отслеживания использования программного обеспечения
 Злоумышленник может отправить в Configuration Manager неправильные сведения о контроле использования программных продуктов, которые будут приняты точкой управления, даже если соответствующий клиентский параметр контроля отключен. Это может привести к появлению большого количества правил контроля использования, реплицируемых во всей иерархии и вызывающих отказ в обслуживании на серверах сайта Configuration Manager и в сети.

 Так как злоумышленник может создать недопустимые данные отслеживания использования программного обеспечения, не следует считать их заслуживающими доверия.

 Отслеживание использования программного обеспечения включено по умолчанию в качестве клиентского параметра.

###  <a name="privacy-information-for-software-metering"></a>Сведения о соблюдении конфиденциальности для отслеживания использования программного обеспечения
 Функция отслеживания использования программного обеспечения наблюдает за использованием приложений на клиентских компьютерах. Она включена по умолчанию. Вам необходимо настроить, какие приложения будут отслеживаться. Информация о контроле использования хранится в базе данных Configuration Manager. Эта информация шифруется во время передачи точке управления, но не сохраняется в зашифрованном виде в базе данных Configuration Manager.

 Информация хранится в базе данных до тех пор, пока не будет удалена при выполнении задач обслуживания сайта **Удаление устаревших данных отслеживания использования программного обеспечения** (каждые пять дней) и **Удаление устаревших сводных данных отслеживания использования программного обеспечения** (каждые 270 дней). Можно настроить интервал удаления. Сведения об отслеживании не отправляются в Майкрософт.

 Перед настройкой отслеживания использования программного обеспечения рассмотрите требования к конфиденциальности.

## <a name="example-scenario-for-using-software-metering"></a>Пример сценария с применением контроля использования программных продуктов
 В этом разделе вы создадите пример правила контроля использования программных продуктов, помогающего решать следующие бизнес-задачи:

- Определить, сколько копий того или иного приложения используется в вашей компании.

- Выявлять неиспользуемые копии приложения.

- Определять, какие пользователи регулярно работают с тем или иным приложением.

  В банке Woodgrove Bank приложение Microsoft Office 2010 развернуто в качестве стандартного пакета для работы в офисе. Тем не менее для поддержки устаревшего приложения на некоторых компьютерах пришлось оставить Microsoft Office Word 2003. Чтобы сократить затраты на поддержку и лицензирование, ИТ-отдел решил удалить данные копии Word 2003 на компьютерах, где устаревшее приложение уже не используется. Кроме того, служба технической поддержки хочет определить, какие пользователи работают с устаревшим приложением.

  Для решения этих задач менеджер по ИТ-системам в банке Woodgrove применяет контроль использования программных продуктов в Configuration Manager. Администратор выполняет такие действия:

- Проверяет, выполняются ли необходимые условия для контроля использования программных продуктов, а также установлена ли и работает ли точка служб отчетов.
- Настраивает параметры клиента по умолчанию для контроля использования программных продуктов:<br>Администратор активирует контроль использования программных продуктов и использует расписание еженедельного сбора данных по умолчанию.<br>Администратор настраивает инвентаризацию программного обеспечения для сбора файлов с расширением .exe, выбрав в клиенте инвентаризации программного обеспечения параметр **Проводить инвентаризацию файлов этих типов**.<br>Администратор добавляет новое правило отслеживания использования программного обеспечения с именем **woodgrove.exe**, чтобы отслеживать устаревшее приложение.
- Через семь дней клиентские компьютеры начинают отправлять данные об использовании исполняемого файла **woodgrove.exe**.
- С помощью отчета Configuration Manager с именем **Установочная база для всех программ отслеживания использования программного обеспечения** Администратор определяет, на какие компьютеры загружен файл **woodgrove.exe**.
- Через шесть месяцев администратор формирует отчет **Компьютеры с установленной и не запускавшейся с указанной даты контролируемой программой**, указывая правило отслеживания использования программного обеспечения и дату, наступившую шесть месяцев назад. Этот отчет определяет 120 компьютеров, на которых в течение шести последних месяцев программа не запускалась.
- Администратор проверяет, что устаревшее приложение больше не используется на включенных в отчет компьютерах, и удаляет его и копию пакета Word 2003 с этих компьютеров.<br>Администратор формирует отчет **Пользователи, запускавшие определенную отслеживаемую программу**, чтобы предоставить службе технической поддержки список пользователей, которые продолжают работать с устаревшим приложением.
- Администратор продолжает еженедельно проверять отчеты об отслеживании использования программного обеспечения и при необходимости применяет исправления.

  Описанные выше действия позволили ИТ-отделу сократить расходы на поддержку и лицензирование, удалив приложения, которые больше не требовались. Кроме того, служба технической поддержки получила необходимый ей список пользователей, работавших с устаревшим приложениям.