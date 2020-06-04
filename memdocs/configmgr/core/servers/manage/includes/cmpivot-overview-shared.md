---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 05/26/2020
ms.openlocfilehash: ad725a2aeb01984d8bce71f66307792e8d1691ee
ms.sourcegitcommit: 0d2f6132428b5fa994e5b770ab1d2bf7d78ac179
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/30/2020
ms.locfileid: "84226436"
---
<!--This file is shared by the CMPivot overview articles for both Microsoft Endpoint Manager tenant attach and Configuration Manager-->

## <a name="queries"></a>Запросы

Запросы можно использовать для поиска условий, определения трендов, анализа закономерностей и предоставления других аналитических сведений на основе имеющихся данных. CMPivot использует подмножество модели потока данных [аналитики журнала Azure](https://docs.microsoft.com/azure/kusto/query) для оператора табличного выражения. Стандартная структура оператора табличного выражения представляет собой комбинацию сущностей клиента и операторов табличных данных (например, фильтров и проекций). Такая комбинация представлена вертикальной чертой (|), придавая оператору стандартную форму, которая визуально представляет поток табличных данных с направлением слева направо. Все операторы принимают набор табличных данных "из вертикальной черты" и дополнительные входные данные (включая другие наборы табличных данных) из текстовой области оператора, а затем передают набор табличных данных следующему оператору в последовательности: `entity | operator1 | operator2 | ...`

В следующем примере сущность представляет собой `CCMRecentlyUsedApplications` (ссылка на недавно использованные приложения) и используется оператор where (который отфильтровывает записи из входных данных в соответствии с предикатом для каждой отдельной записи):

```
CCMRecentlyUsedApplications | where CompanyName like '%Microsoft%'
```

## <a name="entities"></a>Entities

Сущности представляют собой объекты, которые можно запрашивать у клиента. В настоящее время поддерживаются следующие сущности:


|Сущность|Описание:|
|---|---|
|AadStatus|Состояние Azure Active Directory|
|Администраторы|Участники локальной группы администраторов|
|AppCrash|Отчеты о последних сбоях приложений|
|AppVClientApplication|AppV Client Application (Клиентское приложение AppV)|
|AppVClientPackage|AppV Client Package (Пакет клиента AppV)|
|AutoStartSoftware|Программное обеспечение, которое автоматически запускается вместе с операционной системой или сразу после ее запуска|
|BaseBoard|BaseBoard|
|Аккумулятор|Аккумулятор|
|BIOS|Сведения о системе BIOS|
|BitLocker|BitLocker|
|BitLockerEncryptionDetails|BitLocker Encryption Details (Сведения о шифровании BitLocker)|
|BitLockerPolicy|BitLocker Policy|
|BootConfiguration|Boot Configuration (Конфигурация загрузки)|
|BrowserHelperObject|Browser Helper Object (Вспомогательный элемент браузера)|
|BrowserUsage|Использование браузера|
|CcmLog()|Строки за 24 часа (по умолчанию) из файла журнала CCM|
|CCMRAX|CCM_RAX|
|CCMRecentlyUsedApplications|Последние использованные приложения|
|CCMWebAppInstallInfo|Веб-приложения|
|CDROM|Устройство чтения компакт-дисков|
|ClientEvents|Client Events (События клиента)|
|ComputerSystem|Компьютерная система|
|ComputerSystemEx|Computer System Ex (Расширенная компьютерная система)|
|ComputerSystemProduct|Продукт компьютерной системы|
|ConnectedDevice|Connected Device (Подключенное устройство)|
|Подключение|Активное входящее или исходящее TCP-соединение устройства|
|Настольные|Настольные|
|DesktopMonitor|Настольный монитор|
|Устройство|Основные сведения об устройстве|
|Диск|Сведения об устройстве локального хранилища на компьютере под управлением ОС Windows|
|DMA|DMA|
|DMAChannel|DMA Channel (Канал DMA)|
|DriverVxD|Driver - VxD (Драйвер — VxD)|
|EmbeddedDeviceInformation|Embedded Device Information (Сведения об устройстве Embedded)|
|Среда|Среда|
|EPStatus|Состояние антивредоносного ПО на компьютере|
|EventLog()|События за 24 часа (по умолчанию) из журнала событий|
|File()|Сведения о конкретном файле|
|FileShare|Сведения об активной общей папке|
|Firmware (Встроенное ПО)|Firmware (Встроенное ПО)|
|IDEController|IDE Controller (Контроллер IDE)|
|InstalledExecutable|Installed Executable (Установленный исполняемый файл)|
|InstalledSoftware|Приложение, установленное на устройстве|
|IPConfig|Получает конфигурацию сети, включая используемые интерфейсы, IP-адреса и DNS-серверы|
|IRQTable|IRQ Table (Таблица запросов прерываний)|
|Keyboard (Клавиатура)|Keyboard (Клавиатура)|
|LoadOrderGroup|Load Order Group (Группа порядка загрузки)|
|LogicalDisk|Logical Disk (Логический диск)|
|MDMDevDetail|Сведения об устройстве|
|Память|Память|
|Modem (Модем)|Modem (Модем)|
|Motherboard (Системная плата)|Motherboard (Системная плата)|
|NetworkAdapter|Сетевой адаптер|
|NetworkAdapterConfiguration|Network Adapter Configuration (Конфигурация сетевого адаптера)|
|NetworkClient|Network Client (Сетевой клиент)|
|NetworkLoginProfile|Network Login Profile (Профиль сетевого входа)|
|NTEventlogFile|NT Eventlog File (Файл журнала событий NT)|
|Office365ProPlusConfigurations|Конфигурации Office 365 профессиональный плюс|
|OfficeAddin|Надстройки Office|
|OfficeClientMetric|Office Client Metric (Метрика клиента Office)|
|OfficeDeviceSummary|Office Device Summary (Сводка по устройствам Office)|
|OfficeDocumentMetric|Метрики документов Office|
|OfficeDocumentSolution|Office Document Solution (Решение для документов Office)|
|OfficeMacroError|Office Macro Error (Ошибка макроса Office)|
|OfficeProductInfo|Office Product Info (Сведения о продукте Office)|
|OfficeVbaRuleViolation|Office Vba Rule Violation (Нарушение правила VBA)|
|OfficeVbaSummary|Сводка проверки VBA Office|
|OperatingSystem|Операционная система|
|OperatingSystemEx|Operating System Ex (Операционная система расширенная)|
|OperatingSystemRecoveryConfiguration|Operating System Recovery Configuration (Конфигурация восстановления операционной системы)|
|OptionalFeature|Optional Feature (Дополнительная функция)|
|ОС|Основные сведения об операционной системе|
|PageFileSetting|Page File Setting (Параметр файла подкачки)|
|ParallelPort|Parallel Port (Параллельный порт)|
|Partition (Раздел)|Разделы диска|
|PCMCIAController|PCMCIA Controller (PCMCIA-контроллер)|
|PhysicalDisk|PhysicalDisk|
|PhysicalMemory|Физическая память|
|PNPDEVICEDRIVER|Драйвер устройства PNP|
|PointingDevice|Pointing Device (Указывающее устройство)|
|PortableBattery|Переносная батарея|
|Порты|Порты|
|PowerCapabilities|Power Capabilities (Возможности электропитания)|
|PowerClientOptOutSettings|Параметры исключения управления электропитанием|
|PowerConfigurations|Схема управления питанием|
|PowerManagementDaily|Ежедневные данные управления питанием|
|PowerManagementInsomniaReasons|Причины невозможности перехода в спящий режим|
|PowerManagementMonthly|Ежемесячные данные управления питанием|
|PowerSettings|Power Settings (Параметры управления питанием)|
|PrinterConfiguration|Printer Configuration (Конфигурация принтера)|
|PrinterDevice|Printer Device (Печатающее устройство)|
|PrintJobs|Print Jobs (Задания печати)|
|Процесс|Процесс в операционной системе|
|ProcessModule()|Модули, загружаемые указанными процессами|
|Процессор|Процессор|
|ProtectedVolumeInformation|Protected Volume Information (Сведения о защищенном томе)|
|Протокол|Протокол|
|QuickFixEngineering|Quick Fix Engineering (Исправление QFE)|
|Registry()|Все значения для отдельного раздела реестра|
|SCSIController|SCSI Controller (Контроллер SCSI)|
|SerialPortConfiguration|Serial Port Configuration (Конфигурация последовательного порта)|
|SerialPorts|Serial Ports (Последовательные порты)|
|ServerFeature|Серверный компонент|
|Служба|Служба на компьютере под управлением ОС Windows|
|Службы|Службы|
|Shares (Общие папки)|Shares (Общие папки)|
|SMBConfig|Конфигурация SMB устройства|
|SMSAdvancedClientPorts|Порты клиента Configuration Manager|
|SMSAdvancedClientSSLConfigurations|Конфигурации SSL клиента Configuration Manager|
|SMSAdvancedClientState|Состояние клиента Configuration Manager|
|SMSDefaultBrowser|Браузер по умолчанию|
|SMSSoftwareTag|Тег программы|
|SMSWindows8Application|Приложение Windows|
|SMSWindows8ApplicationUserInfo|Сведения о пользователе приложения Windows|
|SoftwareShortcut|Software Shortcut (Ярлык программы)|
|SoftwareUpdate|Обновление программного обеспечения применимо, но не установлено на устройстве|
|SoundDevices|Sound Devices (Звуковые устройства)|
|SWLicensingProduct|Продукт лицензирования ПО|
|SWLicensingService|Служба лицензирования ПО|
|SystemAccount|System Account (Системная учетная запись)|
|SystemBootData|System Boot Data (Данные о загрузке системы)|
|SystemBootSummary|System Boot Summary (Сводка по загрузке системы)|
|SystemConsoleUsage|System Console Usage (Использование системной консоли)|
|SystemConsoleUser|System Console User (Пользователь системной консоли)|
|SystemDevices|System Devices (Системные устройства)|
|SystemDrivers|System Drivers (Системные драйверы)|
|SystemEnclosure|System Enclosure (Системный корпус)|
|TapeDrive|Tape Drive (Ленточный накопитель)|
|TimeZone|Часовой пояс|
|TPM (Доверенный платформенный модуль)|TPM (Доверенный платформенный модуль)|
|TPMStatus|TPM Status (Состояние доверенного платформенного модуля)|
|TSIssuedLicense|TS Issued License (Лицензия, выпущенная TS)|
|TSLicenseKeyPack|TS License Key Pack (Пакет лицензионных ключей TS)|
|UninterruptiblePowerSupply|Uninterruptible Power Supply (Источник бесперебойного питания)|
|USBController|USB-контроллер|
|USBDevice|USB-устройство|
|User (Пользователь)|Учетная запись с активным подключением к устройству|
|USMFolderRedirectionHealth|Работоспособность перенаправления папок|
|USMUserProfile|Работоспособность профиля пользователя|
|VideoController|Видеоконтроллер|
|VirtualMachine|Виртуальная машина|
|VirtualMachine64|Virtual Machine (64) (Виртуальная машина (64))|
|Том|Том|
|WindowsUpdate|Центра обновления Windows;|
|WindowsUpdateAgentVersion|Windows Update Agent Version (Версия агента обновления Windows)|
|WinEvent()|События за 24 часа (по умолчанию) из журнала событий Windows|
|WriteFilterState|Write Filter State (Состояние фильтра записи)|

## <a name="table-operators"></a>Табличные операторы

Табличные операторы можно использовать для фильтрации, суммирования и преобразования потоков данных. В настоящее время поддерживаются следующие операторы:

|Табличные операторы|Описание:|
|---|---|
|count|Возвращает таблицу с одной записью, содержащей число записей.|
|distinct|Создает таблицу с уникальной комбинацией указанных столбцов входной таблицы.|
|join|Слияние строк двух таблиц для формирования новой таблицы путем сопоставления для того же устройства|
|order by|Сортирует строки входной таблицы по одному столбцу или нескольким.|
|project|Выбирает столбцы для включения, переименования или удаления и вставляет новые вычисляемые столбцы.|
|summarize|Создает таблицу, которая агрегирует содержимое входной таблицы.|
|take|Возвращает не более указанного количества строк.|
|top|Возвращает первые N записей, отсортированных по указанным столбцам.|
|where|Фильтрует таблицу до подмножества строк, удовлетворяющего предикату.|

## <a name="scalar-operators"></a>Скалярные операторы

В следующей таблице перечислены операторы.

|Операторы|Описание:|Пример
|---|---|---|
|==|Равно|`1 == 1, 'aBc' == 'AbC'`|
|!=|Не равно|`1 != 2, 'abc' != 'abcd'`|
|< |Меньше|`1 < 2, 'abc' < 'DEF'`|
|> |Больше|`2 > 1, 'xyz' > 'XYZ'`|
|<=|Меньше или равно|`1 <= 2, 'abc' <= 'abc'`|
|>=|Больше или равно|`2 >= 1, 'abc' >= 'ABC'`|
|+|Add|`2 + 1, now() + 1d`|
|-|Subtract|`2 - 1, now() - 1h`|
|*|Multiply|`2 * 2`|
|/|Divide|`2 / 1`|
|%|Modulo|`2 % 1`|
|like|Левая сторона (LHS) содержит соответствие для правой стороны (RHS).|`'abc' like '%B%'`|
|!like|LHS не содержит совпадение для RHS|`'abc' !like '_d_'`|
|содержит|RHS возникает как последовательность LHS|`'abc' contains 'b'`|
|!contains|RHS не возникает в LHS|`'team' !contains 'i'`|
|startswith|RHS является начальной последовательностью LHS|`'team' startswith 'tea'`|
|!startswith|RHS не является начальной последовательностью LHS|`'abc' !startswith 'bc'`|
|endswith|RHS является закрывающей последовательностью LHS|`'abc' endswith 'bc'`|
|!endswith|RHS не является закрывающей последовательностью LHS|`'abc' !endswith 'a'`|
|и|Значение True, только если RHS и LHS имеют значение True.|`(1 == 1) and (2 == 2)`|
|или|Значение True, только если RHS или LHS имеет значение True.|`(1 == 1) or (1 == 2)`|

## <a name="aggregation-functions"></a>Агрегатные функции

Агрегатные функции можно использовать с оператором суммирования таблицы для вычисления суммированных значений. Сейчас поддерживаются следующие агрегатные функции.

|Функция|Описание:|
|---|---|
|avg()|Возвращает среднее по значениям в группе.|
|count()|Возвращает число записей на группу формирования сводных данных.|
|countif()|Возвращает число строк, на которых предикат равен True.|
|dcount()|Возвращает число уникальных значений в группе.|
|max()|Возвращает максимальное значение в группе.|
|min()|Возвращает минимальное значение в группе.|
|percentile()|Возвращает оценку для указанного процентиля ближайшего ранга популяции, определенной Expr|
|sum()|Возвращает сумму значений в группе.|
|sumif()|Возвращает сумму Expr, для которого Predicate возвращает значение true|

## <a name="scalar-functions"></a>Скалярные функции

Скалярные функции могут использоваться в выражениях. В настоящее время поддерживаются следующие скалярные функции.

|Функция|Описание:|
|---|---|
|ago()|вычитает данный временной диапазон из текущего времени в формате UTC.|
|bin()|Округляет значения в меньшую сторону до значения даты и времени, кратного заданному размеру ячейки.|
|case()|Вычисляет список предикатов и возвращает первое выражение, предикат которого выполняется|
|datetime_add()|Вычисляет новую дату и время, умножая заданную часть даты на определенную величину и добавляя к указанным дате и времени полученное значение.|
|datetime_diff()|Вычисляет разницу между двумя значениями даты и времени.|
|iif()|Вычисляет первый аргумент и возвращает значение второго или третьего аргумента в зависимости от того, вернул предикат значение true (второй) или false (третий)|
|indexof()|Функция возвращает отсчитываемый от нуля индекс первого вхождения указанной строки во входной строке|
|isnotnull()|Вычисляет свой единственный аргумент и возвращает логическое значение, указывающее, получено ли ненулевое значение аргумента.|
|isnull()|Вычисляет свой единственный аргумент и возвращает логическое значение, указывающее, получено ли нулевое значение аргумента.|
|now()|возвращает текущее время в формате UTC.|
|strcat()|Объединяет от 1 до 64 аргументов|
|strlen()|Возвращает длину входной строки в символах|
|substring()|Извлекает подстроку из исходной строки, начиная с какого-либо индекса до конца строки|
|tostring()|Преобразует входные данные в строковое представление.|

## <a name="additional-entities-operators-and-functions-for-cmpivot-from-configuration-manager"></a><a name="bkmk_onprem_only"></a> Дополнительные сущности, операторы и функции для CMPivot из Configuration Manager

> [!Important]
> Эти элементы не поддерживаются при запуске CMPivot из Центра администрирования Microsoft Endpoint Manager.

|Type|Элемент|Описание:|
|--|--|---|
|Сущность|AccountSID|Account SID (Идентификатор безопасности учетной записи)|
|Сущность|FileContent()|Содержимое конкретного файла|
|Сущность|NAPClient|NAP Client (Клиент NAP)|
|Сущность|NAPSystemHealthAgent|NAP System Health Agent (Агент работоспособности системы защиты доступа к сети)|
|Табличный оператор|render|Отображает результаты как графический вывод.|
