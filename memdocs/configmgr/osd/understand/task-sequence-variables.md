---
title: Справочник по переменным последовательности задач
titleSuffix: Configuration Manager
description: Сведения о переменных, которые управляют порядком и параметрами для последовательности задач Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 62f15230-d3a6-4afc-abd4-1e07e7ba6c97
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e99efed5d506ddf30e818243ad8b899e8f8b8aca
ms.sourcegitcommit: 99a6e83219978433ec5a91d09beeaf69acbeb522
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/04/2020
ms.locfileid: "82782130"
---
# <a name="task-sequence-variables"></a>Переменные последовательности задач

*Область применения: Configuration Manager (Current Branch)*

Эта статья содержит справочные сведения обо всех доступных переменных в алфавитном порядке. Функция браузера **Найти** (обычно вызывается нажатием клавиш **CTRL** + **F**) позволяет найти в тексте статьи конкретную переменную. Для переменных указано, относятся ли они к определенному шагу последовательности. Описание [шагов последовательности задач](task-sequence-steps.md) содержит список переменных для каждого шага.

См. дополнительные сведения об [использовании переменных последовательности задач](using-task-sequence-variables.md).

## <a name="task-sequence-variable-reference"></a><a name="bkmk_tsvar"></a> Справочник по переменным последовательности задач

### <a name="_osddetectedwindir"></a><a name="OSDDetectedWinDir"></a> _OSDDetectedWinDir

При запуске среды предустановки Windows последовательность задач проверяет жесткие диски компьютера на наличие установки предыдущей операционной системы. Расположение папки Windows хранится в этой переменной. Можно настроить последовательность задач таким образом, чтобы это значение получалось из среды и использовалось для указания того же расположения папки Windows при установке новой операционной системы.

### <a name="_osddetectedwindrive"></a><a name="OSDDetectedWinDrive"></a> _OSDDetectedWinDrive

При запуске среды предустановки Windows последовательность задач проверяет жесткие диски компьютера на наличие установки предыдущей операционной системы. Расположение на жестком диске, куда устанавливается операционная система, хранится в этой переменной. Можно настроить последовательность задач таким образом, чтобы это значение получалось из среды и использовалось для указания того же расположения на жестком диске для новой операционной системы.

### <a name="_osdmigrateusmtpackageid"></a><a name="OSDMigrateUsmtPackageID"></a> _OSDMigrateUsmtPackageID

*Применяется к шагу [Записать пользовательское состояние](task-sequence-steps.md#BKMK_CaptureUserState).*

(входная)

Указывает ИД пакета Configuration Manager, который содержит файлы средства миграции пользовательской среды. Это обязательная переменная.

### <a name="_osdmigrateusmtrestorepackageid"></a><a name="OSDMigrateUsmtRestorePackageID"></a> _OSDMigrateUsmtRestorePackageID

*Применяется к шагу [Восстановить пользовательское состояние](task-sequence-steps.md#BKMK_RestoreUserState).*

(входная)

Указывает ИД пакета Configuration Manager, который содержит файлы средства миграции пользовательской среды. Это обязательная переменная.

### <a name="_smstsadvertid"></a><a name="SMSTSAdvertID"></a> _SMSTSAdvertID

Содержит уникальный идентификатор развертывания текущей выполняемой последовательности задач. Используется тот же формат, что и для идентификатора развертывания распространения программного обеспечения Configuration Manager. Если последовательность задач выполняется с автономного носителя, эта переменная не задается.

#### <a name="example"></a>Пример

`ABC20001`

### <a name="_smstsassettag"></a><a name="SMSTSAssetTag"></a> _SMSTSAssetTag

*Применяется к шагу [Установить динамические переменные](task-sequence-steps.md#BKMK_SetDynamicVariables).*

Указывает ярлык компьютера.

### <a name="_smstsbootimageid"></a><a name="SMSTSBootImageID"></a> _SMSTSBootImageID

Если текущая выполняемая последовательность задач ссылается на пакет загрузочного образа, эта переменная содержит идентификатор пакета загрузочного образа. Если последовательность задач не ссылается на пакет загрузочного образа, эта переменная не задается.

#### <a name="example"></a>Пример

`ABC00001`  

### <a name="_smstsbootuefi"></a><a name="SMSTSBootUEFI"></a> _SMSTSBootUEFI

Последовательность задач устанавливает эту переменную при обнаружении компьютера, находящегося в режиме UEFI.

### <a name="_smstsclientcache"></a><a name="SMSTSClientCache"></a> _SMSTSClientCache

<!-- SCCMDocs issue 1400 -->
Последовательность задач задает эту переменную при кэшировании содержимого на локальном диске. Переменная содержит путь к кэшу. Если эта переменная не существует, значит кэш отсутствует.

### <a name="_smstsclientguid"></a><a name="SMSTSClientGUID"></a> _SMSTSClientGUID

Содержит значение GUID клиента Configuration Manager. Если последовательность задач выполняется с автономного носителя, эта переменная не устанавливается.

#### <a name="example"></a>Пример

`0a1a9a4b-fc56-44f6-b7cd-c3f8ee37c04c`

### <a name="_smstscurrentactionname"></a><a name="SMSTSCurrentActionName"></a> _SMSTSCurrentActionName

Задает имя текущего выполняемого шага последовательности задач. Эта переменная задается перед запуском диспетчером последовательностей задач каждого из шагов.

#### <a name="example"></a>Пример

`run command line`

### <a name="_smstsdefaultgateways"></a><a name="SMSTSDefaultGateways"></a> _SMSTSDefaultGateways

*Применяется к шагу [Установить динамические переменные](task-sequence-steps.md#BKMK_SetDynamicVariables).*

Указывает шлюзы по умолчанию, используемые компьютером.

### <a name="_smstsdownloadondemand"></a><a name="SMSTSDownloadOnDemand"></a> _SMSTSDownloadOnDemand

Если текущая последовательность задач выполняется в режиме загрузки по требованию, для этой переменной задается значение `true`. Режим загрузки по требованию означает, что диспетчер последовательности задач загружает содержимое локально, только когда к нему требуется доступ.

### <a name="_smstsinwinpe"></a><a name="SMSTSInWinPE"></a> _SMSTSInWinPE

Если текущий шаг последовательности задач выполняется в среде Windows PE, для этой переменной задается значение `true`. Проверив значение этой переменной последовательности задач, можно определить текущую среду операционной системы.

### <a name="_smstsipaddresses"></a><a name="SMSTSIPAddresses"></a> _SMSTSIPAddresses

*Применяется к шагу [Установить динамические переменные](task-sequence-steps.md#BKMK_SetDynamicVariables).*

Указывает используемые компьютером IP-адреса.

### <a name="_smstslastactionname"></a><a name="SMSTSLastActionName"></a> _SMSTSLastActionName

Содержит имя последнего выполненного действия. Эта переменная относится к **_SMSTSLastActionRetCode**. Последовательность задач записывает эти значения в файл smsts.log. Эта переменная полезна при устранении неполадок в последовательности задач. Если при выполнении шага происходит сбой, настраиваемый сценарий может включать имя шага, а также код возврата.

### <a name="_smstslastactionretcode"></a><a name="SMSTSLastActionRetCode"></a> _SMSTSLastActionRetCode

Содержит код возврата, возвращенный последним выполненным действием. Эта переменная может использоваться в качестве условия для определения того, запущен ли следующий шаг.

#### <a name="example"></a>Пример

`0`

### <a name="_smstslastactionsucceeded"></a><a name="SMSTSLastActionSucceeded"></a> _SMSTSLastActionSucceeded

- Если последний шаг выполнен успешно, этой переменной присваивается значение `true`.  

- Если последний шаг завершился с ошибкой, присваивается значение `false`.  

- Если последовательность задач пропустила последний шаг из-за того, что он отключен или связанное с ним условие имеет значение **false**, эта переменная не сбрасывается. Она по-прежнему содержит значение для предыдущего действия.  

### <a name="_smstslastcontentdownloadlocation"></a><a name="SMSTSLastContentDownloadLocation"></a> _SMSTSLastContentDownloadLocation

<!-- 2840337 -->
Начиная с версии 1906 эта переменная содержит последнее расположение, где скачивалась последовательность задач или была предпринята попытка скачать содержимое. Проверяйте эту переменную вместо синтаксического анализа журналов клиента для этого расположения содержимого.

### <a name="_smstslaunchmode"></a><a name="SMSTSLaunchMode"></a> _SMSTSLaunchMode

Указывает, с помощью какого метода запущена последовательность задач:  

- **SMS**: клиент Configuration Manager, например запуск пользователем из центра программного обеспечения;
- **UFD**: USB-носитель старого формата;
- **UFD+FORMAT**: более новые USB-носители;
- **CD**: загрузочный компакт-диск;
- **DVD**: загрузочный DVD-диск;
- **PXE**: сетевая загрузка по протоколу удаленной загрузки PXE;
- **HD**: предварительно подготовленный носитель на жестком диске.

### <a name="_smstslogpath"></a><a name="SMSTSLogPath"></a> _SMSTSLogPath

Содержит полный путь к папке журнала. Это значение позволяет определить, где последовательность задач хранит журнал действий. Если жесткий диск недоступен, это значение не устанавливается.

### <a name="_smstsmacaddresses"></a><a name="SMSTSMacAddresses"></a> _SMSTSMacAddresses

*Применяется к шагу [Установить динамические переменные](task-sequence-steps.md#BKMK_SetDynamicVariables).*

Указывает используемые компьютером MAC-адреса.

### <a name="_smstsmachinename"></a><a name="SMSTSMachineName"></a> _SMSTSMachineName

Содержит и указывает имя компьютера. Содержит имя компьютера, который используется последовательностью задач для регистрации всех сообщений об изменении состояния. Чтобы изменить имя компьютера в новой операционной системе, используйте переменную [OSDComputerName](#OSDComputerName-input).

### <a name="_smstsmake"></a><a name="SMSTSMake"></a> _SMSTSMake

*Применяется к шагу [Установить динамические переменные](task-sequence-steps.md#BKMK_SetDynamicVariables).*

Указывает исполнение компьютера.

### <a name="_smstsmdatapath"></a><a name="SMSTSMDataPath"></a> _SMSTSMDataPath

Задает путь, определенный в переменной [SMSTSLocalDataDrive](#SMSTSLocalDataDrive). Этот путь указывает, где последовательность задач сохраняет временные файлы кэша при выполнении на конечном компьютере. Если вы определите переменную SMSTSLocalDataDrive перед запуском последовательности задач, например настроив переменную коллекции, то Configuration Manager определит переменную _SMSTSMDataPath в момент запуска последовательности задач.

### <a name="_smstsmediatype"></a><a name="SMSTSMediaType"></a> _SMSTSMediaType

Указывает тип носителя, используемого для инициализации установки. Примерами типов носителя могут быть загрузочный носитель, полный носитель, PXE и предварительно подготовленный носитель.

### <a name="_smstsmodel"></a><a name="SMSTSModel"></a> _SMSTSModel

*Применяется к шагу [Установить динамические переменные](task-sequence-steps.md#BKMK_SetDynamicVariables).*

Указывает модель компьютера.

### <a name="_smstsmp"></a><a name="SMSTSMP"></a> _SMSTSMP

Содержит URL- или IP-адрес точки управления Configuration Manager.

### <a name="_smstsmpport"></a><a name="SMSTSMPPort"></a> _SMSTSMPPort

Содержит номер порта точки управления Configuration Manager.

### <a name="_smstsorgname"></a><a name="SMSTSOrgName"></a> _SMSTSOrgName

Содержит название организации, отображаемое последовательностью задач в диалоговом окне хода выполнения.

### <a name="_smstsosupgradeactionreturncode"></a><a name="SMSTSOSUpgradeActionReturnCode"></a> _SMSTSOSUpgradeActionReturnCode

*Применяется к шагу [Обновить операционную систему](task-sequence-steps.md#BKMK_UpgradeOS).*

Содержит значение кода выхода, возвращаемое программой установки Windows, чтобы указать на успех или неудачу. Эту переменную удобно использовать с параметром командной строки `/Compat`.

#### <a name="example"></a>Пример

После завершения сканирования compat-only действия в следующих шагах выполняются в зависимости от состояния кода завершения. В случае успешного выполнения начните обновление. Или настройте в среде маркер для сбора с данными об оборудовании. Например, добавьте файл или создайте раздел реестра. Этот маркер используется для создания коллекции компьютеров, готовых к обновлению или требующих определенных действий перед обновлением.

### <a name="_smstspackageid"></a><a name="SMSTSPackageID"></a> _SMSTSPackageID

Содержит идентификатор текущей выполняемой последовательности задач. В этом идентификаторе используется тот же формат, что и в идентификаторе пакета Configuration Manager.

#### <a name="example"></a>Пример

`HJT00001`

### <a name="_smstspackagename"></a><a name="SMSTSPackageName"></a> _SMSTSPackageName

Содержит имя текущей выполняемой последовательности задач. Это имя, заданное администратором Configuration Manager при создании последовательности задач.

#### <a name="example"></a>Пример

`Deploy Windows 10 task sequence`

### <a name="_smstsrunfromdp"></a><a name="SMSTSRunFromDP"></a> _SMSTSRunFromDP

Получает значение `true`, если текущая последовательность задач выполняется в режиме выполнения из точки распространения. Этот режим означает, что диспетчер последовательности задач получает требуемые пакеты из точки распространения.

### <a name="_smstsserialnumber"></a><a name="SMSTSSerialNumber"></a> _SMSTSSerialNumber

*Применяется к шагу [Установить динамические переменные](task-sequence-steps.md#BKMK_SetDynamicVariables).*

Указывает серийный номер компьютера.

### <a name="_smstssetuprollback"></a><a name="SMSTSSetupRollback"></a> _SMSTSSetupRollback

Указывает, выполняла ли программа установки Windows операции отката в процессе обновления на месте. Переменная может иметь значение `true` или `false`.

### <a name="_smstssitecode"></a><a name="SMSTSSiteCode"></a> _SMSTSSiteCode

Содержит код сайта Configuration Manager.

#### <a name="example"></a>Пример

`ABC`

### <a name="_smststimezone"></a><a name="SMSTSTimezone"></a> _SMSTSTimezone

В этой переменной хранятся данные о часовом поясе в следующем формате:

`Bias,StandardBias,DaylightBias,StandardDate.wYear,wMonth,wDayOfWeek,wDay,wHour,wMinute,wSecond,wMilliseconds,DaylightDate.wYear,wMonth,wDayOfWeek,wDay,wHour,wMinute,wSecond,wMilliseconds,StandardName,DaylightName`

#### <a name="example"></a>Пример

Для часового пояса **Восточное время (США и Канада)** :

`300,0,-60,0,11,0,1,2,0,0,0,0,3,0,2,2,0,0,0,Eastern Standard Time,Eastern Daylight Time`

### <a name="_smststype"></a><a name="SMSTSType"></a> _SMSTSType

Задает тип текущей выполняемой последовательности задач. Может иметь одно из следующих значений:  

- **1**: обычная последовательность задач;
- **2**: последовательность задач развертывания операционной системы.

### <a name="_smstsusecrl"></a><a name="SMSTSUseCRL"></a> _SMSTSUseCRL

Эта переменная указывает, использует ли последовательность задач список отзыва сертификатов, если для связи с точкой управления используется протокол HTTPS.

### <a name="_smstsuserstarted"></a><a name="SMSTSUserStarted"></a> _SMSTSUserStarted

Указывает, запущена ли последовательность задач пользователем. Эта переменная задается, только если последовательность задач запускается из центра программного обеспечения. Например, если переменная [_SMSTSLaunchMode](#SMSTSLaunchMode) имеет значение `SMS`.

Эта переменная может принимать следующие значения:  

- `true`: указывает, что последовательность задач запущена пользователем вручную из центра программного обеспечения.  

- `false`: указывает, что последовательность задач запущена автоматически планировщиком Configuration Manager.

### <a name="_smstsusessl"></a><a name="SMSTSUseSSL"></a> _SMSTSUseSSL

Указывает, использует ли последовательность задач протокол SSL для связи с точкой управления Configuration Manager. Если для систем сайта настроен протокол HTTPS, присваивается значение `true`.

### <a name="_smstsuuid"></a><a name="SMSTSUUID"></a> _SMSTSUUID

*Применяется к шагу [Установить динамические переменные](task-sequence-steps.md#BKMK_SetDynamicVariables).*

Указывает UUID компьютера.

### <a name="_smstswtg"></a><a name="SMSTSWTG"></a> _SMSTSWTG

определяет, работает ли компьютер как устройство Windows To Go.

### <a name="_ts_crmemory"></a><a name="TSCRMEMORY"></a> _TS_CRMEMORY

*Начиная с версии 2002* <!--6005561-->  
*Область применения: шаг [Проверка готовности](task-sequence-steps.md#BKMK_CheckReadiness).*

Переменная только для чтения, которая определяет, вернула ли проверка параметра **Минимальный объем памяти (МБ)** значение true (`1`) или false (`0`). Если не включить проверку, значение соответствующей переменной только для чтения будет пустым.

### <a name="_ts_crspeed"></a><a name="TSCRSPEED"></a> _TS_CRSPEED

*Начиная с версии 2002* <!--6005561-->  
*Область применения: шаг [Проверка готовности](task-sequence-steps.md#BKMK_CheckReadiness).*

Переменная только для чтения, которая определяет, вернула ли проверка параметра **Минимальная скорость процессора (МГц)** значение true (`1`) или false (`0`). Если не включить проверку, значение соответствующей переменной только для чтения будет пустым.

### <a name="_ts_crdisk"></a><a name="TSCRDISK"></a> _TS_CRDISK

*Начиная с версии 2002* <!--6005561-->  
*Область применения: шаг [Проверка готовности](task-sequence-steps.md#BKMK_CheckReadiness).*

Переменная только для чтения, которая определяет, вернула ли проверка параметра **Минимальное свободное место на диске (МБ)** значение true (`1`) или false (`0`). Если не включить проверку, значение соответствующей переменной только для чтения будет пустым.

### <a name="_ts_crostype"></a><a name="TSCROSTYPE"></a> _TS_CROSTYPE

*Начиная с версии 2002* <!--6005561-->  
*Область применения: шаг [Проверка готовности](task-sequence-steps.md#BKMK_CheckReadiness).*

Переменная только для чтения, которая определяет, вернула ли проверка параметра **Текущая операционная система для обновления** значение true (`1`) или false (`0`). Если не включить проверку, значение соответствующей переменной только для чтения будет пустым.

### <a name="_ts_crarch"></a><a name="TSCRARCH"></a> _TS_CRARCH

*Начиная с версии 2002* <!--6005561-->  
*Область применения: шаг [Проверка готовности](task-sequence-steps.md#BKMK_CheckReadiness).*

Переменная только для чтения, которая определяет, вернула ли проверка параметра **Архитектура текущей ОС** значение true (`1`) или false (`0`). Если не включить проверку, значение соответствующей переменной только для чтения будет пустым.

### <a name="_ts_crminosver"></a><a name="TSCRMINOSVER"></a> _TS_CRMINOSVER

*Начиная с версии 2002* <!--6005561-->  
*Область применения: шаг [Проверка готовности](task-sequence-steps.md#BKMK_CheckReadiness).*

Переменная только для чтения, которая определяет, вернула ли проверка параметра **Минимальная версия ОС** значение true (`1`) или false (`0`). Если не включить проверку, значение соответствующей переменной только для чтения будет пустым.

### <a name="_ts_crmaxosver"></a><a name="TSCRMAXOSVER"></a> _TS_CRMAXOSVER

*Начиная с версии 2002* <!--6005561-->  
*Область применения: шаг [Проверка готовности](task-sequence-steps.md#BKMK_CheckReadiness).*

Переменная только для чтения, которая определяет, вернула ли проверка параметра **Максимальная версия ОС** значение true (`1`) или false (`0`). Если не включить проверку, значение соответствующей переменной только для чтения будет пустым.

### <a name="_ts_crclientminver"></a><a name="TSCRCLIENTMINVER"></a> _TS_CRCLIENTMINVER

*Начиная с версии 2002* <!--6005561-->  
*Область применения: шаг [Проверка готовности](task-sequence-steps.md#BKMK_CheckReadiness).*

Переменная только для чтения, которая определяет, вернула ли проверка параметра **Минимальная версия клиента** значение true (`1`) или false (`0`). Если не включить проверку, значение соответствующей переменной только для чтения будет пустым.

### <a name="_ts_croslanguage"></a><a name="TSCROSLANGUAGE"></a> _TS_CROSLANGUAGE

*Начиная с версии 2002* <!--6005561-->  
*Область применения: шаг [Проверка готовности](task-sequence-steps.md#BKMK_CheckReadiness).*

Переменная только для чтения, которая определяет, вернула ли проверка параметра **Язык текущей ОС** значение true (`1`) или false (`0`). Если не включить проверку, значение соответствующей переменной только для чтения будет пустым.

### <a name="_ts_cracpower"></a><a name="TSCRACPOWER"></a> _TS_CRACPOWER

*Начиная с версии 2002* <!--6005561-->  
*Область применения: шаг [Проверка готовности](task-sequence-steps.md#BKMK_CheckReadiness).*

Переменная только для чтения, которая определяет, вернула ли проверка параметра **Питание от сети включено** значение true (`1`) или false (`0`). Если не включить проверку, значение соответствующей переменной только для чтения будет пустым.

### <a name="_ts_crnetwork"></a><a name="TSCRNETWORK"></a> _TS_CRNETWORK

*Начиная с версии 2002* <!--6005561-->  
*Область применения: шаг [Проверка готовности](task-sequence-steps.md#BKMK_CheckReadiness).*

Переменная только для чтения, которая определяет, вернула ли проверка параметра **Сетевой адаптер подключен** значение true (`1`) или false (`0`). Если не включить проверку, значение соответствующей переменной только для чтения будет пустым.

### <a name="_ts_crwired"></a><a name="TSCRWIRED"></a> _TS_CRWIRED

*Начиная с версии 2002* <!--6005561-->  
*Область применения: шаг [Проверка готовности](task-sequence-steps.md#BKMK_CheckReadiness).*

Переменная только для чтения, которая определяет, вернула ли проверка параметра **Сетевой адаптер не является беспроводным** значение true (`1`) или false (`0`). Если не включить проверку, значение соответствующей переменной только для чтения будет пустым.

### <a name="_tsappinstallstatus"></a><a name="TSAppInstallStatus"></a> _TSAppInstallStatus

Последовательность задач сохраняет в этой переменной состояние установки приложения на шаге [Установить приложение](task-sequence-steps.md#BKMK_InstallApplication). Допустимы следующие значения:  

- **Не определено**: Шаг "Установить приложение" не был выполнен.  

- **Ошибка** — сбой по меньшей мере одного приложения из-за ошибки на шаге "Установить приложение".  

- **Предупреждение**. Не получено ошибок на шаге "Установить приложение". Пропущена установка одного или нескольких приложений или необходимой зависимости из-за невыполнения некоторых условий.  

- **Успешно** — Не получено ошибок или предупреждений во время выполнения шага "Установить приложение".  

### <a name="_tssecureboot"></a><a name="TSSecureBoot"></a> _TSSecureBoot

*Начиная с версии 2002* <!--5842295-->  

Используйте эту переменную для определения состояния безопасной загрузки на устройстве с поддержкой UEFI. Эта переменная может принимать следующие значения:

- `NA`: связанное значение реестра не существует, то есть устройство не поддерживает безопасную загрузку.
- `Enabled`: для устройства включена безопасная загрузка.
- `Disabled`: для устройства отключена безопасная загрузка.

### <a name="osdadapter"></a><a name="OSDAdapter"></a> OSDAdapter

*Применяется к шагу [Применить параметры сети](task-sequence-steps.md#BKMK_ApplyNetworkSettings).*

(входная)

Эта переменная последовательности задач является *массивом*. Каждый элемент массива содержит параметры для одного сетевого адаптера на компьютере. Для доступа к параметрам для каждого адаптера следует использовать имя переменной массива, индекс сетевого адаптера (нумерация начинается с 0) и имя свойства.

Если на шаге "Применить параметры сети" выполняется настройка нескольких сетевых адаптеров, свойства для *второго* сетевого адаптера задаются в переменной, к имени которой добавлен индекс **1**. Пример. OSDAdapter1EnableDHCP, OSDAdapter1IPAddressList и OSDAdapter1DNSDomain.

Приведенные ниже имена переменных позволяют задать свойства *первого* сетевого адаптера, который будет настраиваться на этом шаге:

#### <a name="osdadapter0enabledhcp"></a>OSDAdapter0EnableDHCP

Это обязательный параметр. Возможные значения: `True` или `False`. Пример.

`true` — включение протокола DHCP для адаптера.

#### <a name="osdadapter0ipaddresslist"></a>OSDAdapter0IPAddressList

Разделенный запятыми список IP-адресов для адаптера. Это свойство игнорируется, если свойство **EnableDHCP** имеет значение, отличное от `false`. Это обязательный параметр.

#### <a name="osdadapter0subnetmask"></a>OSDAdapter0SubnetMask

Разделенный запятыми список масок подсетей. Это свойство игнорируется, если свойство **EnableDHCP** имеет значение, отличное от `false`. Это обязательный параметр.

#### <a name="osdadapter0gateways"></a>OSDAdapter0Gateways

Разделенный запятыми список IP-адресов шлюзов. Это свойство игнорируется, если свойство **EnableDHCP** имеет значение, отличное от `false`. Это обязательный параметр.

#### <a name="osdadapter0dnsdomain"></a>OSDAdapter0DNSDomain

Домен службы доменных имен (DNS-домен) для адаптера.

#### <a name="osdadapter0dnsserverlist"></a>OSDAdapter0DNSServerList

Разделенный запятыми список DNS-серверов для адаптера. Это обязательный параметр.

#### <a name="osdadapter0enablednsregistration"></a>OSDAdapter0EnableDNSRegistration

Значение `true` означает, что IP-адрес адаптера регистрируется в DNS.

#### <a name="osdadapter0enablefulldnsregistration"></a>OSDAdapter0EnableFullDNSRegistration

Задайте значение `true`, чтобы зарегистрировать IP-адрес адаптера в DNS с указанием полного DNS-имени компьютера.

#### <a name="osdadapter0enableipprotocolfiltering"></a>OSDAdapter0EnableIPProtocolFiltering

Задайте значение `true`, чтобы включить для адаптера фильтрацию протокола IP.

#### <a name="osdadapter0ipprotocolfilterlist"></a>OSDAdapter0IPProtocolFilterList

Разделенный запятыми список протоколов, для которых разрешена работа через протокол IP. Это свойство игнорируется, если свойство **EnableIPProtocolFiltering** имеет значение `false`.

#### <a name="osdadapter0enabletcpfiltering"></a>OSDAdapter0EnableTCPFiltering

Задайте значение `true`, чтобы включить для адаптера фильтрацию TCP-портов.

#### <a name="osdadapter0tcpfilterportlist"></a>OSDAdapter0TCPFilterPortList

Разделенный запятыми список разрешенных TCP-портов. Это свойство игнорируется, если свойство **EnableTCPFiltering** имеет значение `false`.

#### <a name="osdadapter0tcpipnetbiosoptions"></a>OSDAdapter0TcpipNetbiosOptions

Использование NetBIOS через TCP/IP. Возможные значения:  

- `0`: использовать параметры NetBIOS с DHCP-сервера;  
- `1`: включить NetBIOS через TCP/IP;  
- `2`: отключить NetBIOS через TCP/IP.  

#### <a name="osdadapter0enablewins"></a>OSDAdapter0EnableWINS

Задайте значение `true`, чтобы использовать разрешение имен WINS.

#### <a name="osdadapter0winsserverlist"></a>OSDAdapter0WINSServerList

Разделенный запятыми список IP-адресов WINS-серверов. Это свойство игнорируется, если свойство **EnableWINS** имеет значение, отличное от `true`.

#### <a name="osdadapter0macaddress"></a>OSDAdapter0MacAddress

MAC-адрес, используемый для сопоставления параметров с физическим сетевым адаптером.

#### <a name="osdadapter0name"></a>OSDAdapter0Name

Имя сетевого подключения, отображаемое на панели управления "Сетевые подключения" программы. Длина имени должна иметь длину от 0 до 255 знаков.

#### <a name="osdadapter0index"></a>OSDAdapter0Index

Позиция параметров сетевого адаптера в массиве параметров.

#### <a name="example"></a>Пример

- **OSDAdapterCount** = `1`  
- **OSDAdapter0EnableDHCP** = `FALSE`  
- **OSDAdapter0IPAddressList** = `192.168.0.40`  
- **OSDAdapter0SubnetMask** = `255.255.255.0`  
- **OSDAdapter0Gateways** = `192.168.0.1`  
- **OSDAdapter0DNSSuffix** = `contoso.com`  

### <a name="osdadaptercount"></a><a name="OSDAdapterCount"></a> OSDAdapterCount

*Применяется к шагу [Применить параметры сети](task-sequence-steps.md#BKMK_ApplyNetworkSettings).*

(входная)

Указывает количество сетевых адаптеров, установленных на конечном компьютере. Присваивая значение переменной **OSDAdapterCount**, обязательно задайте все параметры конфигурации для каждого адаптера.

Например, если для первого адаптера задано значение **OSDAdapter0TCPIPNetbiosOptions**, необходимо настроить и все остальные значения для этого адаптера.

Если это значение не указано, последовательность задач игнорирует все значения **OSDAdapter**.

### <a name="osdapplydriverbootcriticalcontentuniqueid"></a><a name="OSDApplyDriverBootCriticalContentUniqueID"></a> OSDApplyDriverBootCriticalContentUniqueID

*Применяется к шагу [Применить пакет драйверов](task-sequence-steps.md#BKMK_ApplyDriverPackage).*

(входная)

Указывает идентификатор содержимого драйвера запоминающего устройства, устанавливаемого из пакета драйверов. Если эта переменная не указана, установка драйвера запоминающего устройства не выполняется.

### <a name="osdapplydriverbootcriticalhardwarecomponent"></a><a name="OSDApplyDriverBootCriticalHardwareComponent"></a> OSDApplyDriverBootCriticalHardwareComponent

*Применяется к шагу [Применить пакет драйверов](task-sequence-steps.md#BKMK_ApplyDriverPackage).*

(входная)

Указывает, установлен ли драйвер запоминающего устройства; переменной должно быть задано значение **scsi**.

Эта переменная является обязательной, если задано значение переменной [OSDApplyDriverBootCriticalContentUniqueID](#OSDApplyDriverBootCriticalContentUniqueID).

### <a name="osdapplydriverbootcriticalid"></a><a name="OSDApplyDriverBootCriticalID"></a> OSDApplyDriverBootCriticalID

*Применяется к шагу [Применить пакет драйверов](task-sequence-steps.md#BKMK_ApplyDriverPackage).*

(входная)

Указывает ИД загрузки устанавливаемого драйвера запоминающего устройства. Этот ИД указан в разделе **scsi** файла txtsetup.oem драйвера устройства.

Эта переменная является обязательной, если задано значение переменной [OSDApplyDriverBootCriticalContentUniqueID](#OSDApplyDriverBootCriticalContentUniqueID).

### <a name="osdapplydriverbootcriticalinffile"></a><a name="OSDApplyDriverBootCriticalINFFile"></a> OSDApplyDriverBootCriticalINFFile

*Применяется к шагу [Применить пакет драйверов](task-sequence-steps.md#BKMK_ApplyDriverPackage).*

(входная)

Указывает INF-файл устанавливаемого драйвера накопителя большой емкости.

Эта переменная является обязательной, если задано значение переменной [OSDApplyDriverBootCriticalContentUniqueID](#OSDApplyDriverBootCriticalContentUniqueID).

### <a name="osdautoapplydriverbestmatch"></a><a name="OSDAutoApplyDriverBestMatch"></a> OSDAutoApplyDriverBestMatch

*Применяется к шагу [Применять драйверы автоматически](task-sequence-steps.md#BKMK_AutoApplyDrivers).*

(входная)

Если в каталоге драйверов есть несколько драйверов, совместимых с устройством, эта переменная указывает, какие операции выполняет действие.

#### <a name="valid-values"></a>Допустимые значения

- `true` (по умолчанию): устанавливать только наиболее подходящий драйвер устройства;  

- `false`: устанавливать все совместимые драйверы устройств, из числа которых Windows выберет наиболее подходящий драйвер.  

### <a name="osdautoapplydrivercategorylist"></a><a name="OSDAutoApplyDriverCategoryList"></a> OSDAutoApplyDriverCategoryList

*Применяется к шагу [Применять драйверы автоматически](task-sequence-steps.md#BKMK_AutoApplyDrivers).*

(входная)

Список уникальных идентификаторов категорий каталога драйверов с разделителями-запятыми. Шаг **Автоматически применить драйвер** распространяется только на те драйверы, которые относятся по меньшей мере к одной из указанных категорий. Это значение является необязательным и не присваивается по умолчанию. Доступные идентификаторы категорий можно получить посредством перечисления списка объектов **SMS_CategoryInstance** на сайте.

### <a name="osdbitlockerrebootcount"></a><a name="OSDBitLockerRebootCount"></a> OSDBitLockerRebootCount

*Применяется к шагу [Отключить BitLocker](task-sequence-steps.md#BKMK_DisableBitLocker).*

<!-- 4512937 -->
Начиная с версии 1906, используйте эту переменную, чтобы задать число перезапусков, после которых будет возобновлена защита.

#### <a name="valid-values"></a>Допустимые значения

Целое число от `1` до `15`.

### <a name="osdbitlockerrebootcountoverride"></a><a name="OSDBitLockerRebootCountOverride"></a> OSDBitLockerRebootCountOverride

*Применяется к шагу [Отключить BitLocker](task-sequence-steps.md#BKMK_DisableBitLocker).*

<!-- 4512937 -->
Начиная с версии 1906, задавайте это значение чтобы переопределить значение счетчика, заданное с помощью шага или переменной [OSDBitLockerRebootCount](#OSDBitLockerRebootCount). В других методах принимаются только значения 1–15, но если задать этой переменной значение 0, BitLocker останется отключенным на неопределенное время. Эта переменная полезна в случаях, когда последовательность задач устанавливает одно значение, но вы хотите установить разные значения для каждого устройства или коллекции.

#### <a name="valid-values"></a>Допустимые значения

Целое число от `0` до `15`.

### <a name="osdbitlockerrecoverypassword"></a><a name="OSDBitLockerRecoveryPassword"></a> OSDBitLockerRecoveryPassword

*Применяется к шагу [Включить BitLocker](task-sequence-steps.md#BKMK_EnableBitLocker).*

(входная)

Задача **Включить BitLocker** будет использовать заданное здесь значение вместо созданного случайным образом пароля восстановления. Значение должно быть допустимым числовым паролем восстановления BitLocker.

### <a name="osdbitlockerstartupkey"></a><a name="OSDBitLockerStartupKey"></a> OSDBitLockerStartupKey

*Применяется к шагу [Включить BitLocker](task-sequence-steps.md#BKMK_EnableBitLocker).*

(входная)

Вместо создания случайного ключа запуска для параметра управления ключами **Ключ запуска на USB** шаг **Включить BitLocker** использует доверенный платформенный модуль (TPM) в качестве ключа запуска. Значение должно представлять собой допустимый 256-разрядный ключ запуска, зашифрованный с использованием Base64.

### <a name="osdcaptureaccount"></a><a name="OSDCaptureAccount"></a> OSDCaptureAccount

*Применяется к шагу [Записать образ операционной системы](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).*

(входная)

Указывает имя учетной записи пользователя Windows с разрешениями хранить записанный образ в общей сетевой папке ([OSDCaptureDestination](#OSDCaptureDestination)). Также задайте значение [OSDCaptureAccountPassword](#OSDCaptureAccountPassword).

Дополнительные сведения об учетной записи образа ОС см. в разделе [Accounts](../../core/plan-design/hierarchy/accounts.md#capture-os-image-account) (Учетные записи).

### <a name="osdcaptureaccountpassword"></a><a name="OSDCaptureAccountPassword"></a> OSDCaptureAccountPassword

*Применяется к шагу [Записать образ операционной системы](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).*

(входная)

Указывает пароль для учетной записи Windows ([OSDCaptureAccount](#OSDCaptureAccount)), в которой расположена сетевая папка ([OSDCaptureDestination](#OSDCaptureDestination)) с записанным образом.

### <a name="osdcapturedestination"></a><a name="OSDCaptureDestination"></a> OSDCaptureDestination

*Применяется к шагу [Записать образ операционной системы](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).*

(входная)

Указывает расположение, в котором последовательность задач сохраняет записанный образ операционной системы. Максимальная длина имени каталога составляет 255 знаков. Если общий сетевой ресурс требует аутентификации, задайте значения переменных [OSDCaptureAccount](#OSDCaptureAccount) и [OSDCaptureAccountPassword](#OSDCaptureAccountPassword).

### <a name="osdcomputername-input"></a><a name="OSDComputerName-input"></a> OSDComputerName (входная)

*Применяется к шагу [Применить настройки Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

Указывает имя конечного компьютера.

#### <a name="example"></a>Пример

`%_SMSTSMachineName%` (по умолчанию)

### <a name="osdcomputername-output"></a><a name="OSDComputerName-output"></a> OSDComputerName (выходная)

*Применяется к шагу [Сохранить параметры Windows](task-sequence-steps.md#BKMK_CaptureWindowsSettings).*

Указывает NetBIOS-имя компьютера. Это значение присваивается, только если переменная [OSDMigrateComputerName](#OSDMigrateComputerName) имеет значение `true`.

### <a name="osdconfigfilename"></a><a name="OSDConfigFileName"></a> OSDConfigFileName

*Применяется к шагу [Применить образ операционной системы](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).*

(входная)

Указывает имя файла ответов для развертывания операционной системы, связанного с пакетом развертывания операционной системы.  

### <a name="osddataimageindex"></a><a name="OSDDataImageIndex"></a> OSDDataImageIndex

*Применяется к шагу [Применить образ данных](task-sequence-steps.md#BKMK_ApplyDataImage).*

(входная)

Указывает значение индекса для образа, применяемого к конечному компьютеру.

### <a name="osddiskindex"></a><a name="OSDDiskIndex"></a> OSDDiskIndex

*Применяется к шагу [Отформатировать диск и создать разделы](task-sequence-steps.md#BKMK_FormatandPartitionDisk).*

(входная)

Указывает номер физического диска, подлежащего разбиению на разделы.

### <a name="osddnsdomain"></a><a name="OSDDNSDomain"></a> OSDDNSDomain

*Применяется к шагу [Применить параметры сети](task-sequence-steps.md#BKMK_ApplyNetworkSettings).*

(входная)

Задает первичный DNS-сервер, который используется конечным компьютером.

### <a name="osddnssuffixsearchorder"></a><a name="OSDDNSSuffixSearchOrder"></a> OSDDNSSuffixSearchOrder

*Применяется к шагу [Применить параметры сети](task-sequence-steps.md#BKMK_ApplyNetworkSettings).*

(входная)

Задает порядок поиска DNS для конечного компьютера.

### <a name="osddomainname"></a><a name="OSDDomainName"></a> OSDDomainName

*Применяется к шагу [Применить параметры сети](task-sequence-steps.md#BKMK_ApplyNetworkSettings).*

(входная)

Задает имя домена Active Directory, к которому присоединяется конечный компьютер. Заданное значение должно быть допустимым именем домена доменных служб Active Directory.

### <a name="osddomainouname"></a><a name="OSDDomainOUName"></a> OSDDomainOUName

*Применяется к шагу [Применить параметры сети](task-sequence-steps.md#BKMK_ApplyNetworkSettings).*

(входная)

Задает в формате RFC 1779 имя подразделения (OU), к которому должен быть присоединен конечный компьютер. Если это значение задано, оно должно содержать полный путь.

#### <a name="example"></a>Пример

`LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com`

### <a name="osddonotlogcommand"></a><a name="OSDDoNotLogCommand"></a> OSDDoNotLogCommand

<!--1358493-->
*Используется на шаге [Установить пакет](task-sequence-steps.md#BKMK_InstallPackage).*

*Начиная с версии 1902*  
*Применяется к шагу [Выполнить из командной строки](task-sequence-steps.md#BKMK_RunCommandLine).*

(входная)

Чтобы предотвратить отображение или сохранение в журнал потенциально конфиденциальных данных, присвойте этой переменной значение `TRUE`. Эта переменная маскирует имя программы в файле **smsts.log** во время выполнения шага **Установить пакет**.

Начиная с версии 1902 в случае присвоения этой переменной значения `TRUE` в файле журнала в записи, соответствующей шагу **Выполнить из командной строки**, теперь также скрывается командная строка.<!--3654172-->

### <a name="osdenabletcpipfiltering"></a><a name="OSDEnableTCPIPFiltering"></a> OSDEnableTCPIPFiltering

*Применяется к шагу [Применить параметры сети](task-sequence-steps.md#BKMK_ApplyNetworkSettings).*

(входная)

Указывает, должна ли быть включена фильтрация TCP/IP.

#### <a name="valid-values"></a>Допустимые значения

- `true`  
- `false` (по умолчанию)  

### <a name="osdgptbootdisk"></a><a name="OSDGPTBootDisk"></a> OSDGPTBootDisk

*Применяется к шагу [Отформатировать диск и создать разделы](task-sequence-steps.md#BKMK_FormatandPartitionDisk).*

(входная)

Указывает, требуется ли создание раздела EFI на жестком диске GPT. Этот диск используется в качестве загрузочного на компьютерах, поддерживающих EFI.

#### <a name="valid-values"></a>Допустимые значения

- `true`  
- `false` (по умолчанию)

### <a name="osdimagecreator"></a><a name="OSDImageCreator"></a> OSDImageCreator

*Применяется к шагу [Записать образ операционной системы](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).*

(входная)

Необязательное имя пользователя, создавшего образ. Это имя хранится в WIM-файле. Максимальная длина имени пользователя составляет 255 знаков.

### <a name="osdimagedescription"></a><a name="OSDImageDescription"></a> OSDImageDescription

*Применяется к шагу [Записать образ операционной системы](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).*

(входная)

Необязательное описание записанного образа операционной системы, которое задается пользователем. Это описание хранится в WIM-файле. Максимальная длина описания составляет 255 знаков.

### <a name="osdimageindex"></a><a name="OSDImageIndex"></a> OSDImageIndex

*Применяется к шагу [Применить образ операционной системы](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).*

(входная)

Указывает значение индекса образа для WIM-файла, который применяется к конечному компьютеру.

### <a name="osdimageversion"></a><a name="OSDImageVersion"></a> OSDImageVersion

*Применяется к шагу [Записать образ операционной системы](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).*

(входная)

Необязательный номер версии, который задается пользователем и присваивается записанному образу операционной системы. Этот номер версии хранится в WIM-файле. Это значение может содержать любое сочетание буквенно-цифровых символов общей длиной до 32 знаков.

### <a name="osdinstalldriversadditionaloptions"></a><a name="OSDInstallDriversAdditionalOptions"></a> OSDInstallDriversAdditionalOptions

<!--516679/2840016-->
*Применяется к шагу [Применить пакет драйверов](task-sequence-steps.md#BKMK_ApplyDriverPackage).*

(входная)

Указывает дополнительные параметры, которые нужно включить в командную строку DISM при применении пакета драйверов. Последовательность задач не проверяет эти параметры командной строки.

Чтобы использовать эту переменную, включите параметр **Install driver package via running DISM with recurse option** (Установить пакет драйверов путем запуска команды DISM с параметром recurse) на шаге **Применить пакет драйверов**.

См. дополнительные сведения о [параметрах командной строки для DISM в Windows 10](https://docs.microsoft.com/windows-hardware/manufacture/desktop/deployment-image-servicing-and-management--dism--command-line-options).

### <a name="osdjoinaccount"></a><a name="OSDJoinAccount"></a> OSDJoinAccount

*Применяется к следующим шагам:*  

- [Применить параметры сети](task-sequence-steps.md#BKMK_ApplyNetworkSettings)  
- [Присоединить к домену или рабочей группе](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup).  

(входная)

Указывает учетную запись пользователя домена, которая будет использоваться для добавления конечного компьютера в домен. Эта переменная является обязательной при присоединении к домену.

Дополнительные сведения об учетной записи для присоединения к домену см. в разделе [Accounts](../../core/plan-design/hierarchy/accounts.md#task-sequence-domain-join-account) (Учетные записи).

### <a name="osdjoindomainname"></a><a name="OSDJoinDomainName"></a> OSDJoinDomainName

*Применяется к шагу [Присоединить к домену или рабочей группе](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup).*

(входная)

Задает имя домена Active Directory, к которому будет присоединен целевой компьютер. Имя домена должно содержать от 1 до 255 символов.

### <a name="osdjoindomainouname"></a><a name="OSDJoinDomainOUName"></a> OSDJoinDomainOUName

*Применяется к шагу [Присоединить к домену или рабочей группе](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup).*

(входная)

Задает в формате RFC 1779 имя подразделения (OU), к которому должен быть присоединен конечный компьютер. Если это значение задано, оно должно содержать полный путь. Имя домена подразделения должно содержать от 0 до 32 767 символов. Это значение не задается, если переменной [OSDJoinType](#OSDJoinType) задано значение `1` (присоединение к рабочей группе).

#### <a name="example"></a>Пример

`LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com`  

### <a name="osdjoinpassword"></a><a name="OSDJoinPassword"></a> OSDJoinPassword

*Применяется к следующим шагам:*  

- [Применить параметры сети](task-sequence-steps.md#BKMK_ApplyNetworkSettings)  
- [Присоединить к домену или рабочей группе](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup).  

(входная)

Указывает пароль для учетной записи [OSDJoinAccount](#OSDJoinAccount), которую конечный компьютер использует для присоединения к домену Active Directory. Если эта переменная отсутствует в среде последовательности задач, программа установки Windows пытается использовать пустой пароль. Это значение является обязательным, если переменной [OSDJoinType](#OSDJoinType) задано значение `0` (присоединение к домену).

### <a name="osdjoinskipreboot"></a><a name="OSDJoinSkipReboot"></a> OSDJoinSkipReboot

*Применяется к шагу [Присоединить к домену или рабочей группе](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup).*

(входная)

Указывает, следует ли пропустить перезагрузку после присоединения конечного компьютера к домену или рабочей группе.

#### <a name="valid-values"></a>Допустимые значения

- `true`  
- `false`  

### <a name="osdjointype"></a><a name="OSDJoinType"></a> OSDJoinType

*Применяется к шагу [Присоединить к домену или рабочей группе](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup).*

(входная)

Указывает, к чему присоединяется конечный компьютер — к домену Windows или рабочей группе Windows.

#### <a name="valid-values"></a>Допустимые значения

- `0`: присоединение конечного компьютера к домену Windows;  
- `1`: присоединение конечного компьютера к рабочей группе.  

### <a name="osdjoinworkgroupname"></a><a name="OSDJoinWorkgroupName"></a> OSDJoinWorkgroupName

*Применяется к шагу [Присоединить к домену или рабочей группе](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup).*

(входная)

Задает имя рабочей группы, к которой будет присоединен конечный компьютер. Имя рабочей группы должно иметь длину от 1 до 32 символов.

### <a name="osdkeepactivation"></a><a name="OSDKeepActivation"></a> OSDKeepActivation

*Применяется к шагу [Подготовка Windows перед снятием образа](task-sequence-steps.md#BKMK_PrepareWindowsforCapture).*

(входная)

Указывает, будет ли программа Sysprep сохранять или сбрасывать флаг активации продукта.

#### <a name="valid-values"></a>Допустимые значения

- `true`: сохранение флага активации
- `false` (по умолчанию): сброс флага активации

### <a name="osdlocaladminpassword"></a><a name="OSDLocalAdminPassword"></a> OSDLocalAdminPassword

*Применяется к шагу [Применить настройки Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

(входная)

Указывает пароль локальной учетной записи администратора. Шаг игнорирует эту переменную, если включен параметр **Randomly generate the local administrator password and disable the account on all supported platforms** (Задать пароль локального администратора случайным образом и отключить учетную запись локального администратора на всех поддерживаемых платформах). Указанное значение должно иметь длину от 1 до 255 знаков.

### <a name="osdlogpowershellparameters"></a><a name="OSDLogPowerShellParameters"></a> OSDLogPowerShellParameters

<!--3556028-->
*Начиная с версии 1902*  
*Применяется к шагу [Запустить сценарий PowerShell](task-sequence-steps.md#BKMK_RunPowerShellScript).*

(входная)

Чтобы предотвратить запись потенциально конфиденциальных данных, на шаге **Запустить сценарий PowerShell** не осуществляется запись параметров сценария в файл **smsts.log**. Чтобы включить параметры сценария в журнал последовательности задач, задайте для этой переменной значение **TRUE**.

### <a name="osdmigrateadaptersettings"></a><a name="OSDMigrateAdapterSettings"></a> OSDMigrateAdapterSettings

*Применяется к шагу [Сохранить параметры сети](task-sequence-steps.md#BKMK_CaptureNetworkSettings).*

(входная)

Указывает, будет ли последовательность задач сохранять сведения о сетевых адаптерах. Сюда относятся параметры конфигурации TCP/IP, DNS и WINS.

#### <a name="valid-values"></a>Допустимые значения

- `true` (по умолчанию)
- `false`

### <a name="osdmigrateadditionalcaptureoptions"></a><a name="OSDMigrateAdditionalCaptureOptions"></a> OSDMigrateAdditionalCaptureOptions

*Применяется к шагу [Записать пользовательское состояние](task-sequence-steps.md#BKMK_CaptureUserState).*

(входная)

Укажите параметры командной строки для средства миграции пользовательской среды (USMT), которые последовательность задач применит для записи пользовательского состояния. Этот шаг не отображает эти параметры в редакторе последовательности задач. Укажите эти параметры в виде строки, которую последовательность задач присоединяет к автоматически созданной для ScanState командной строке средства USMT.

Параметры USMT, указанные в этой переменной последовательности задач, не проверяются на точность перед выполнением последовательности задач.

Дополнительные сведения о доступных параметрах см. в разделе с описанием [синтаксиса ScanState](https://docs.microsoft.com/windows/deployment/usmt/usmt-scanstate-syntax).

### <a name="osdmigrateadditionalrestoreoptions"></a><a name="OSDMigrateAdditionalRestoreOptions"></a> OSDMigrateAdditionalRestoreOptions

*Применяется к шагу [Восстановить пользовательское состояние](task-sequence-steps.md#BKMK_RestoreUserState).*

(входная)

Указывает параметры командной строки для средства миграции пользовательской среды (USMT), которые последовательность задач применит при восстановлении пользовательского состояния. Укажите дополнительные параметры в виде строки, которую последовательность задач присоединяет к автоматически созданной для LoadState командной строке средства USMT.

Параметры USMT, указанные в этой переменной последовательности задач, не проверяются на точность перед выполнением последовательности задач.

Дополнительные сведения о доступных вариантах см. в разделе, посвященном [синтаксису LoadState](https://docs.microsoft.com/windows/deployment/usmt/usmt-loadstate-syntax).

### <a name="osdmigratecomputername"></a><a name="OSDMigrateComputerName"></a> OSDMigrateComputerName

*Применяется к шагу [Сохранить параметры Windows](task-sequence-steps.md#BKMK_CaptureWindowsSettings).*

(входная)

Указывает, переносится ли имя компьютера.

#### <a name="valid-values"></a>Допустимые значения

- `true` (по умолчанию). Переменной [OSDComputerName (выходная)](#OSDComputerName-output) присваивается NetBIOS-имя компьютера.  
- `false`  

### <a name="osdmigrateconfigfiles"></a><a name="OSDMigrateConfigFiles"></a> OSDMigrateConfigFiles

*Применяется к шагу [Записать пользовательское состояние](task-sequence-steps.md#BKMK_CaptureUserState).*

(входная)

Указывает файлы конфигурации, используемые для управления записью профилей пользователей. Эта переменная используется, только если переменной [OSDMigrateMode](#OSDMigrateMode) присвоено значение `Advanced`. Это значение списка с разделителями-запятыми задается с целью выполнения настраиваемой миграции профилей пользователей.

#### <a name="example"></a>Пример

`miguser.xml,migsys.xml,migapps.xml`  

### <a name="osdmigratecontinueonlockedfiles"></a><a name="OSDMigrateContinueOnLockedFiles"></a> OSDMigrateContinueOnLockedFiles

*Применяется к шагу [Записать пользовательское состояние](task-sequence-steps.md#BKMK_CaptureUserState).*

(входная)

Если средство USMT не сможет записать какие-то файлы, эта переменная позволит продолжить процесс записи.

#### <a name="valid-values"></a>Допустимые значения

- `true` (по умолчанию)  
- `false`  

### <a name="osdmigratecontinueonrestore"></a><a name="OSDMigrateContinueOnRestore"></a> OSDMigrateContinueOnRestore

*Применяется к шагу [Восстановить пользовательское состояние](task-sequence-steps.md#BKMK_RestoreUserState).*

(входная)

Продолжение процесса, даже если средству USMT не удается восстановить некоторые файлы.

#### <a name="valid-values"></a>Допустимые значения

- `true` (по умолчанию)  
- `false`  

### <a name="osdmigrateenableverboselogging"></a><a name="OSDMigrateEnableVerboseLogging"></a> OSDMigrateEnableVerboseLogging

*Применяется к следующим шагам:*  

- [Записать пользовательское состояние](task-sequence-steps.md#BKMK_CaptureUserState);  
- [Восстановить пользовательское состояние](task-sequence-steps.md#BKMK_RestoreUserState).  

(входная)

Включает запись подробных сведений в журнал средством USMT. Этот шаг требует наличия этого значения.

#### <a name="valid-values"></a>Допустимые значения

- `true`  
- `false` (по умолчанию)  

### <a name="osdmigratelocalaccounts"></a><a name="OSDMigrateLocalAccounts"></a> OSDMigrateLocalAccounts

*Применяется к шагу [Восстановить пользовательское состояние](task-sequence-steps.md#BKMK_RestoreUserState).*

(входная)

Указывает, будет ли восстановлена учетная запись локального компьютера.

#### <a name="valid-values"></a>Допустимые значения

- `true`  
- `false` (по умолчанию)  

### <a name="osdmigratelocalaccountpassword"></a><a name="OSDMigrateLocalAccountPassword"></a> OSDMigrateLocalAccountPassword

*Применяется к шагу [Восстановить пользовательское состояние](task-sequence-steps.md#BKMK_RestoreUserState).*

(входная)

Если переменная [OSDMigrateLocalAccounts](#OSDMigrateLocalAccounts) имеет значение `true`, в этой переменной должен содержаться пароль, назначенный *всем* перенесенным локальным учетным записям. USMT назначает один и тот же пароль всем перенесенным локальным учетным записям. Он считается временным и подлежит изменению каким-либо другим методом.

### <a name="osdmigratemode"></a><a name="OSDMigrateMode"></a> OSDMigrateMode

*Применяется к шагу [Записать пользовательское состояние](task-sequence-steps.md#BKMK_CaptureUserState).*

(входная)

Позволяет настраивать, какие файлы записывает средство USMT.

#### <a name="valid-values"></a>Допустимые значения

- `Simple`: последовательность задач использует только стандартные файлы конфигурации USMT;  

- `Advanced`: переменная последовательности задач [OSDMigrateConfigFiles](#OSDMigrateConfigFiles) определяет файлы конфигурации, которые использует средство USMT.  

### <a name="osdmigratenetworkmembership"></a><a name="OSDMigrateNetworkMembership"></a> OSDMigrateNetworkMembership

*Применяется к шагу [Сохранить параметры сети](task-sequence-steps.md#BKMK_CaptureNetworkSettings).*

(входная)

Указывает, должна ли последовательность задач переносить сведения о членстве в рабочей группе или домене.

#### <a name="valid-values"></a>Допустимые значения

- `true` (по умолчанию)
- `false`

### <a name="osdmigrateregistrationinfo"></a><a name="OSDMigrateRegistrationInfo"></a> OSDMigrateRegistrationInfo

*Применяется к шагу [Сохранить параметры Windows](task-sequence-steps.md#BKMK_CaptureWindowsSettings).*

(входная)

Указывает, выполняет ли этот шаг миграцию сведений о пользователях и организации.

#### <a name="valid-values"></a>Допустимые значения

- `true` (по умолчанию). Переменной [OSDRegisteredOrgName (выходная)](#OSDRegisteredOrgName-output) присваивается значение зарегистрированного в организации имени компьютера.  
- `false`  

### <a name="osdmigrateskipencryptedfiles"></a><a name="OSDMigrateSkipEncryptedFiles"></a> OSDMigrateSkipEncryptedFiles

*Применяется к шагу [Записать пользовательское состояние](task-sequence-steps.md#BKMK_CaptureUserState).*

(входная)

Указывает, записываются ли зашифрованные файлы.

#### <a name="valid-values"></a>Допустимые значения

- `true`  
- `false` (по умолчанию)  

### <a name="osdmigratetimezone"></a><a name="OSDMigrateTimeZone"></a> OSDMigrateTimeZone

*Применяется к шагу [Сохранить параметры Windows](task-sequence-steps.md#BKMK_CaptureWindowsSettings).*

(входная)

Указывает, переносится ли часовой пояс компьютера.

#### <a name="valid-values"></a>Допустимые значения

- `true` (по умолчанию). Переменной [OSDTimeZone (выходная)](#OSDTimeZone-output) присваивается значение часового пояса компьютера.  
- `false`  

### <a name="osdnetworkjointype"></a><a name="OSDNetworkJoinType"></a> OSDNetworkJoinType

*Применяется к шагу [Применить параметры сети](task-sequence-steps.md#BKMK_ApplyNetworkSettings).*

(входная)

Указывает, к чему присоединяется конечный компьютер — к домену Active Directory или рабочей группе.

#### <a name="value-values"></a>Допустимые значения

- `0`: присоединение к домену Active Directory;  
- `1`: Присоединить к рабочей группе

### <a name="osdpartitions"></a><a name="OSDPartitions"></a> OSDPartitions

*Применяется к шагу [Отформатировать диск и создать разделы](task-sequence-steps.md#BKMK_FormatandPartitionDisk).*

(входная)

Эта переменная последовательности задач является массивом для настроек раздела. Каждый элемент массива содержит параметры для одного раздела на жестком диске. Для доступа к параметрам, заданным для каждого раздела, следует использовать имя переменной массива, номер раздела (нумерация начинается с 0) и имя свойства.

Приведенные ниже имена переменных задают свойства *первого* раздела, который этот шаг создает на жестком диске.

#### <a name="osdpartitions0type"></a>OSDPartitions0Type

Задает тип раздела. Это свойство обязательно. Допустимые значения: `Primary`, `Extended`, `Logical` и `Hidden`.

#### <a name="osdpartitions0filesystem"></a>OSDPartitions0FileSystem

Задает тип файловой системы, используемой при форматировании раздела. Это свойство необязательно. Если вы не укажете файловую систему, форматирование раздела не выполняется. Допустимые значения: `FAT32` и `NTFS`.

#### <a name="osdpartitions0bootable"></a>OSDPartitions0Bootable

Указывает, является ли раздел загрузочным. Это свойство обязательно. Если эта переменная имеет значение `TRUE` для MBR-дисков, шаг помечает этот раздел как активный.

#### <a name="osdpartitions0quickformat"></a>OSDPartitions0QuickFormat

Задает используемый тип форматирования. Это свойство обязательно. Если значение равно `TRUE`, шаг выполняет быстрое форматирование. В противном случае используется полное форматирование.

#### <a name="osdpartitions0volumename"></a>OSDPartitions0VolumeName

Указывает имя, назначаемое тому при форматировании. Это свойство необязательно.

#### <a name="osdpartitions0size"></a>OSDPartitions0Size

Определяет размер раздела. Это свойство необязательно. Если это свойство не указано, для раздела выделяется полный объем свободного пространства. Единицы задаются переменной **OSDPartitions0SizeUnits** .

#### <a name="osdpartitions0sizeunits"></a>OSDPartitions0SizeUnits

Шаг использует эти единицы измерения для значения, указанного в переменной **OSDPartitions0Size**. Это свойство необязательно. Допустимые значения: `MB` (по умолчанию), `GB` и `Percent`.

#### <a name="osdpartitions0volumelettervariable"></a>OSDPartitions0VolumeLetterVariable

Когда этот шаг создает разделы, в Windows PE всегда используется следующая доступная буква диска. Используйте этот необязательный параметр, чтобы указать имя другой переменной последовательности задач. В шаге эта переменная служит для сохранения новой буквы диска с целью последующего использования.

Если в этом шаге последовательности задач определено несколько разделов, свойства для *второго* раздела содержат в имени переменной индекс **1**. Пример. **OSDPartitions1Type**, **OSDPartitions1FileSystem**, **OSDPartitions1Bootable**, **OSDPartitions1QuickFormat** и **OSDPartitions1VolumeName**.

### <a name="osdpartitionstyle"></a><a name="OSDPartitionStyle"></a> OSDPartitionStyle

*Применяется к шагу [Отформатировать диск и создать разделы](task-sequence-steps.md#BKMK_FormatandPartitionDisk).*

(входная)

Задает стиль раздела для использования при создании разделов на диске.

#### <a name="valid-values"></a>Допустимые значения

- `GPT`: использование формата таблицы разделов GPT;
- `MBR`: использование формата основной загрузочной записи раздела.

### <a name="osdproductkey"></a><a name="OSDProductKey"></a> OSDProductKey

*Применяется к шагу [Применить настройки Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

(входная)

Указывает ключ продукта Windows. Указанное значение должно иметь длину от 1 до 255 знаков.

### <a name="osdrandomadminpassword"></a><a name="OSDRandomAdminPassword"></a> OSDRandomAdminPassword

*Применяется к шагу [Применить настройки Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

(входная)

Указывает, что пароль для учетной записи администратора в новой операционной системе нужно сгенерировать случайным образом.

#### <a name="valid-values"></a>Допустимые значения

- `true` (по умолчанию): программа установки Windows отключит учетную запись локального администратора на конечном компьютере.  

- `false`: программа установки Windows включит учетную запись локального администратора на конечном компьютере и установит для этой учетной записи в качестве пароля значение переменной [OSDLocalAdminPassword](#OSDLocalAdminPassword).  

### <a name="osdregisteredorgname-input"></a><a name="OSDRegisteredOrgName-input"></a> OSDRegisteredOrgName (входная)

*Применяется к шагу [Применить настройки Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

Указывает зарегистрированное имя организации по умолчанию в новой операционной системе. Указанное значение должно иметь длину от 1 до 255 знаков.

### <a name="osdregisteredorgname-output"></a><a name="OSDRegisteredOrgName-output"></a> OSDRegisteredOrgName (выходная)

*Применяется к шагу [Сохранить параметры Windows](task-sequence-steps.md#BKMK_CaptureWindowsSettings).*

Этой переменной задается зарегистрированное имя организации компьютера. Это значение задается, только если переменная [OSDMigrateRegistrationInfo](#OSDMigrateRegistrationInfo) имеет значение `true`.

### <a name="osdregisteredusername"></a><a name="OSDRegisteredUserName"></a> OSDRegisteredUserName

*Применяется к шагу [Применить настройки Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

(входная)

Указывает зарегистрированное имя пользователя по умолчанию в новой операционной системе. Указанное значение должно иметь длину от 1 до 255 знаков.

### <a name="osdserverlicenseconnectionlimit"></a><a name="OSDServerLicenseConnectionLimit"></a> OSDServerLicenseConnectionLimit

*Применяется к шагу [Применить настройки Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

(входная)

Задает максимальное число подключений. Указанное число должно быть в диапазоне от 5 до 9999.

### <a name="osdserverlicensemode"></a><a name="OSDServerLicenseMode"></a> OSDServerLicenseMode

*Применяется к шагу [Применить настройки Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

(входная)

Задает используемый режим лицензирования Windows Server.

#### <a name="valid-values"></a>Допустимые значения

- `PerSeat`
- `PerServer`

### <a name="osdsetupadditionalupgradeoptions"></a><a name="OSDSetupAdditionalUpgradeOptions"></a> OSDSetupAdditionalUpgradeOptions

*Применяется к шагу [Обновить операционную систему](task-sequence-steps.md#BKMK_UpgradeOS).*

(входная)

Задает дополнительные параметры командной строки, добавляемые в программу установки Windows в ходе обновления Windows 10. Последовательность задач не проверяет эти параметры командной строки.

Дополнительные сведения см. в статье [Параметры командной строки программы установки Windows](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options).

### <a name="osdstatefallbacktonaa"></a><a name="OSDStateFallbackToNAA"></a> OSDStateFallbackToNAA

*Применяется к шагу [Запросить хранилище состояний](task-sequence-steps.md#BKMK_RequestStateStore).*

(входная)

Если учетная запись компьютера не может подключиться к точке миграции состояния, эта переменная указывает, будет ли последовательность задач использовать учетную запись сетевого доступа в качестве резервной.

См. дополнительные сведения об [учетной записи доступа к сети](../../core/plan-design/hierarchy/accounts.md#network-access-account).

#### <a name="valid-values"></a>Допустимые значения

- `true`  
- `false` (по умолчанию)  

### <a name="osdstatesmpretrycount"></a><a name="OSDStateSMPRetryCount"></a> OSDStateSMPRetryCount

*Применяется к шагу [Запросить хранилище состояний](task-sequence-steps.md#BKMK_RequestStateStore).*

(входная)

Указывает количество попыток поиска точки миграции состояния последовательностью задач, после которого шаг завершается неудачей. Может быть указано количество от 0 до 600.

### <a name="osdstatesmpretrytime"></a><a name="OSDStateSMPRetryTime"></a> OSDStateSMPRetryTime

*Применяется к шагу [Запросить хранилище состояний](task-sequence-steps.md#BKMK_RequestStateStore).*

(входная)

Указывает время в секундах между попытками поиска, предпринимаемыми последовательностью задач. Можно указать значение периода длиной максимум 30 символов.

### <a name="osdstatestorepath"></a><a name="OSDStateStorePath"></a> OSDStateStorePath

*Применяется к следующим шагам:*  

- [Записать пользовательское состояние](task-sequence-steps.md#BKMK_CaptureUserState);  
- [Освободить хранилище состояний](task-sequence-steps.md#BKMK_ReleaseStateStore);  
- [Запросить хранилище состояний](task-sequence-steps.md#BKMK_RequestStateStore);  
- [Восстановить пользовательское состояние](task-sequence-steps.md#BKMK_RestoreUserState).  

(входная)

Общий сетевой ресурс или локальный путь к папке, в которой последовательность задач сохраняет или из которой восстанавливает пользовательскую среду. Значение по умолчанию отсутствует.

### <a name="osdtargetsystemdrive"></a><a name="OSDTargetSystemDrive"></a> OSDTargetSystemDrive

*Применяется к шагу [Применить образ операционной системы](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).*

(выходная)

Указывает букву диска для раздела, где будут размещены файлы операционной системы после применения образа.

### <a name="osdtargetsystemroot-input"></a><a name="OSDTargetSystemRoot-input"></a> OSDTargetSystemRoot (входная)

*Применяется к шагу [Записать образ операционной системы](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).*

Указывает путь к каталогу Windows с установленной операционной системой на компьютере-образце. Последовательность задач проверяет, поддерживается ли для этой ОС запись с помощью Configuration Manager.

### <a name="osdtargetsystemroot-output"></a><a name="OSDTargetSystemRoot-output"></a> OSDTargetSystemRoot (выходная)

*Применяется к шагу [Подготовка Windows перед снятием образа](task-sequence-steps.md#BKMK_PrepareWindowsforCapture).*

Указывает путь к каталогу Windows с установленной операционной системой на компьютере-образце. Последовательность задач проверяет, поддерживается ли для этой ОС запись с помощью Configuration Manager.

### <a name="osdtimezone-input"></a><a name="OSDTimeZone-input"></a> OSDTimeZone (входная)

*Применяется к шагу [Применить настройки Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

Указывает часовой пояс по умолчанию, который используется в новой операционной системе.

Задайте этой переменной в качестве значения инвариантное имя часового пояса. Например, используйте строку в значении `Std` для часового пояса в следующем разделе реестра: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Time Zones`.

### <a name="osdtimezone-output"></a><a name="OSDTimeZone-output"></a> OSDTimeZone (выходная)

*Применяется к шагу [Сохранить параметры Windows](task-sequence-steps.md#BKMK_CaptureWindowsSettings).*

Указывает часовой пояс компьютера. Это значение задается, только если переменная [OSDMigrateTimeZone](#OSDMigrateTimeZone) имеет значение `true`.

### <a name="osdwindowssettingsinputlocale"></a><a name="OSDWindowsSettingsInputLocale"></a> OSDWindowsSettingsInputLocale

*Применяется к шагу [Применить настройки Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

Указывает параметр языкового стандарта для ввода по умолчанию, который используется в новой операционной системе.

Дополнительные сведения об этих значениях файла ответов программы установки Windows см. в разделе [Microsoft-Windows-International-Core — InputLocale](https://docs.microsoft.com/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core-inputlocale).

### <a name="osdwindowssettingssystemlocale"></a><a name="OSDWindowsSettingsSystemLocale"></a> OSDWindowsSettingsSystemLocale

*Применяется к шагу [Применить настройки Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

Указывает параметр языкового стандарта системы по умолчанию, который используется в новой операционной системе.

Дополнительные сведения об этих значениях файла ответов программы установки Windows см. в разделе [Microsoft-Windows-International-Core — SystemLocale](https://docs.microsoft.com/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core-systemlocale).

### <a name="osdwindowssettingsuilanguage"></a><a name="OSDWindowsSettingsUILanguage"></a> OSDWindowsSettingsUILanguage

*Применяется к шагу [Применить настройки Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

Указывает язык пользовательского интерфейса, который используется по умолчанию в новой операционной системе.

Дополнительные сведения об этих значениях файла ответов программы установки Windows см. в разделе [Microsoft-Windows-International-Core — UILanguage](https://docs.microsoft.com/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core-uilanguage).

### <a name="osdwindowssettingsuilanguagefallback"></a><a name="OSDWindowsSettingsUILanguageFallback"></a> OSDWindowsSettingsUILanguageFallback

*Применяется к шагу [Применить настройки Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

Указывает базовый язык пользовательского интерфейса, который используется в новой операционной системе.

Дополнительные сведения об этих значениях файла ответов программы установки Windows см. в разделе [Microsoft-Windows-International-Core — UILanguageFallback](https://docs.microsoft.com/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core-uilanguagefallback).

### <a name="osdwindowssettingsuserlocale"></a><a name="OSDWindowsSettingsUserLocale"></a> OSDWindowsSettingsUserLocale

*Применяется к шагу [Применить настройки Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

Указывает параметр языкового стандарта пользователя по умолчанию, который используется в новой операционной системе.

Дополнительные сведения об этих значениях файла ответов программы установки Windows см. в разделе [Microsoft-Windows-International-Core — UserLocale](https://docs.microsoft.com/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core-userlocale).

### <a name="osdwipedestinationpartition"></a><a name="OSDWipeDestinationPartition"></a> OSDWipeDestinationPartition

*Применяется к шагу [Применить образ данных](task-sequence-steps.md#BKMK_ApplyDataImage).*

(входная)

Указывает, требуется ли удаление файлов, расположенных в целевом разделе.

#### <a name="valid-values"></a>Допустимые значения

- `true` (по умолчанию)
- `false`

### <a name="osdworkgroupname"></a><a name="OSDWorkgroupName"></a> OSDWorkgroupName

*Применяется к шагу [Применить параметры сети](task-sequence-steps.md#BKMK_ApplyNetworkSettings).*

(входная)

Задает имя рабочей группы Windows, к которой будет присоединен конечный компьютер.

Обязательно присвойте значение этой переменной или переменной [OSDDomainName](#OSDDomainName). Имя рабочей группы не должно быть длиннее 32 символов.

### <a name="setupcompletepause"></a><a name="SetupCompletePause"></a> SetupCompletePause

*Применяется к шагу [Обновить операционную систему](task-sequence-steps.md#BKMK_UpgradeOS).*

<!-- 4680263 -->

Начиная с версии 1910, используйте эту переменную для решения проблем синхронизации последовательности задач обновления Window 10 на месте на высокопроизводительных устройствах после завершения установки Windows. При назначении этой переменной значения в секундах процесс установки Windows использует задержку указанной длительности перед запуском последовательности задач. Это время ожидания дает клиенту Configuration Manager дополнительное время для инициализации.

Следующие записи журнала являются типичными примерами проблемы, которую можно устранить с помощью этой переменной:

- Компонент TSManager регистрирует записи, аналогичные следующим ошибкам, в **smsts.log**:

    ``` log
    Failed to initate policy evaluation for namespace 'root\ccm\policy\machine', hr=0x80041010
    Error compiling client config policies. code 80041010
    Task Sequence Manager could not initialize Task Sequence Environment. code 80041010
    ```

- Программа установки Windows регистрирует записи, аналогичные следующим ошибкам, в **setupcomplete.log**:

    ``` log
    Running C:\windows\CCM\\TSMBootstrap.exe to resume task sequence
    ERRORLEVEL = -1073741701
    TSMBootstrap did not request reboot, resetting registry
    Exiting setupcomplete.cmd
    ```

### <a name="smsclientinstallproperties"></a><a name="SMSClientInstallProperties"></a> SMSClientInstallProperties

*Применяется к шагу [Настроить Windows и Configuration Manager](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr).*

(входная)

Указывает свойства установки клиента, которые последовательность задач использует при установке клиента Configuration Manager.

Дополнительные сведения см. в разделе [Сведения о параметрах и свойствах установки клиента](../../core/clients/deploy/about-client-installation-properties.md).

### <a name="smsconnectnetworkfolderaccount"></a><a name="SMSConnectNetworkFolderAccount"></a> SMSConnectNetworkFolderAccount

*Применяется к шагу [Подключить к сетевой папке](task-sequence-steps.md#BKMK_ConnectToNetworkFolder).*

(входная)

Указывает учетную запись пользователя, используемую для подключения к общей сетевой папке, адрес которой указан в переменной [SMSConnectNetworkFolderPath](#SMSConnectNetworkFolderPath). Пароль к этой учетной записи задается в виде значения [SMSConnectNetworkFolderPassword](#SMSConnectNetworkFolderPassword).

Дополнительные сведения об учетной записи для подключения к общему сетевому ресурсу в последовательности задач см. в разделе [Accounts](../../core/plan-design/hierarchy/accounts.md#task-sequence-network-folder-connection-account) (Учетные записи).

### <a name="smsconnectnetworkfolderdriveletter"></a><a name="SMSConnectNetworkFolderDriveLetter"></a> SMSConnectNetworkFolderDriveLetter

*Применяется к шагу [Подключить к сетевой папке](task-sequence-steps.md#BKMK_ConnectToNetworkFolder).*

(входная)

Указывает букву диска, с которой сопоставляется сетевая папка. Это необязательное значение. Если это значение не указано, сетевое подключение не связывается с буквой диска. Для этого значения допускаются буквы в диапазоне от D до Z. Не используйте букву X, которая используется Windows PE на этапе Windows PE.

#### <a name="examples"></a>Примеры

- `D:`  
- `E:`  

### <a name="smsconnectnetworkfolderpassword"></a><a name="SMSConnectNetworkFolderPassword"></a> SMSConnectNetworkFolderPassword

*Применяется к шагу [Подключить к сетевой папке](task-sequence-steps.md#BKMK_ConnectToNetworkFolder).*

(входная)

Указывает пароль для учетной записи [SMSConnectNetworkFolderAccount](#SMSConnectNetworkFolderAccount), которая используется для подключения к общей сетевой папке, адрес которой указан в переменной [SMSConnectNetworkFolderPath](#SMSConnectNetworkFolderPath).

### <a name="smsconnectnetworkfolderpath"></a><a name="SMSConnectNetworkFolderPath"></a> SMSConnectNetworkFolderPath

*Применяется к шагу [Подключить к сетевой папке](task-sequence-steps.md#BKMK_ConnectToNetworkFolder).*

(входная)

Указывает сетевой путь для подключения. Если вам нужно сопоставить этот путь с буквой диска, используйте значение [SMSConnectNetworkFolderDriveLetter](#SMSConnectNetworkFolderDriveLetter).

#### <a name="example"></a>Пример

`\\server\share`

### <a name="smsinstallupdatetarget"></a><a name="SMSInstallUpdateTarget"></a> SMSInstallUpdateTarget

*Применяется к шагу [Установить обновления программного обеспечения](task-sequence-steps.md#BKMK_InstallSoftwareUpdates).*

(входная)

Указывает, следует ли установить все обновления или только обязательные обновления.

#### <a name="valid-values"></a>Допустимые значения

- `All`  
- `Mandatory`  

### <a name="smsrebootmessage"></a><a name="SMSRebootMessage"></a> SMSRebootMessage

*Применяется к шагу [Перезагрузить компьютер](task-sequence-steps.md#BKMK_RestartComputer).*

(входная)

Указывает сообщение, отображаемое пользователям перед перезагрузкой конечного компьютера. Если эта переменная не задана, отображается сообщение по умолчанию. Длина сообщения не может превышать 512 символов.

#### <a name="example"></a>Пример

`Save your work before the computer restarts.`  

### <a name="smsreboottimeout"></a><a name="SMSRebootTimeout"></a> SMSRebootTimeout

*Применяется к шагу [Перезагрузить компьютер](task-sequence-steps.md#BKMK_RestartComputer).*

(входная)

Указывает время в секундах, которое проходит с момента отображения предупреждения пользователю до перезагрузки компьютера.

#### <a name="examples"></a>Примеры

- `0` (по умолчанию): не отображать сообщение о перезагрузке;  
- `60`: отображать предупреждение в течение одной минуты.  

### <a name="smstsassignmentsdownloadinterval"></a><a name="SMSTSAssignmentsDownloadInterval"></a> SMSTSAssignmentsDownloadInterval

Время ожидания в секундах перед новой попыткой клиента скачать политику с момента последней попытки, не вернувшей политики. По умолчанию клиент ожидает **0** секунд перед повторной попыткой.

Эту переменную можно установить с помощью команды перед запуском с носителя или посредством PXE.

### <a name="smstsassignmentsdownloadretry"></a><a name="SMSTSAssignmentsDownloadRetry"></a> SMSTSAssignmentsDownloadRetry

Количество попыток скачивания политики, выполняемых клиентом, если политики не были найдены с первой попытки. По умолчанию клиент повторяет попытку **0** раз.

Эту переменную можно установить с помощью команды перед запуском с носителя или посредством PXE.

### <a name="smstsassignusersmode"></a><a name="SMSTSAssignUsersMode"></a> SMSTSAssignUsersMode

Указывает, как последовательность задач связывает пользователей с конечным компьютером. Присвойте переменной одно из следующих значений.  

- **Автоматически**: когда последовательность задач развертывает ОС на конечный компьютер, она создает связь между определенными пользователями и этим компьютером.  

- **Ожидание**: последовательность задач создает связь между указанными пользователями и конечным компьютером. Требуется предварительное утверждение администратором.  

- **Отключено**. последовательность задач не связывает пользователей с конечным компьютером во время развертывания операционной системы.

### <a name="smstsdisablestatusretry"></a><a name="SMSTSDisableStatusRetry"></a> SMSTSDisableStatusRetry

<!--512358-->
В сценариях без подключения к сети подсистема выполнения последовательности задач будет пытаться отправлять сообщения о состоянии в точку управления. Такое поведение приводит к задержкам при обработке последовательности задач.

Значение `true` для этой переменной означает, что подсистема выполнения последовательности задач не будет пытаться отправлять сообщения о состоянии после сбоя первого сообщения. Это первая попытка включает в себя несколько повторных попыток.

При перезапуске последовательности задач значение этой переменной сохраняется. Однако последовательность задач пытается отправить начальное сообщение о состоянии. Это первая попытка включает в себя несколько повторных попыток. В случае успешного выполнения последовательность задач продолжает отправлять состояние независимо от значения этой переменной. Если отправить состояние не удается, последовательность задач использует значение этой переменной.

> [!NOTE]  
> [Отчеты о состоянии последовательности задач](../../core/servers/manage/list-of-reports.md#task-sequence---deployment-status) используют эти сведения о состоянии для отображения хода выполнения, журнала и сведений для каждого шага. Если сообщения о состоянии не удается отправить, они не помещаются в очередь. Поэтому они не отправляются и после восстановления подключения к точке управления. В результате отчет о состоянии последовательности задач может быть неполным, в нем могут отсутствовать элементы.

### <a name="smstsdisablewow64redirection"></a><a name="SMSTSDisableWow64Redirection"></a> SMSTSDisableWow64Redirection

*Применяется к шагу [Выполнить из командной строки](task-sequence-steps.md#BKMK_RunCommandLine).*

(входная)

Если используется 64-разрядная версия операционной системы, последовательность задач по умолчанию находит и запускает программу в командной строке с помощью перенаправителя файловой системы WOW64. Это позволяет обнаруживать 32-разрядные версии программ операционной системы и библиотек DLL. Присвойте этой переменной значение `true`, чтобы отключить использование перенаправителя файловой системы WOW64. В этом случае команда будет обнаруживать только 64-разрядные версии программ операционной системы и библиотек DLL. Эта переменная не используется при работе в 32-разрядной версии операционной системы.

### <a name="smstsdownloadabortcode"></a><a name="SMSTSDownloadAbortCode"></a> SMSTSDownloadAbortCode

Эта переменная содержит значение кода прерывания для загрузчика внешней программы. Сама программа указывается в переменной [SMSTSDownloadProgram](#SMSTSDownloadProgram). Если программа возвращает код ошибки, равный значению переменной SMSTSDownloadAbortCode, то скачивание содержимого завершается сбоем и попытки выполнить скачивание с помощью других методов не предпринимаются.

### <a name="smstsdownloadprogram"></a><a name="SMSTSDownloadProgram"></a> SMSTSDownloadProgram

Используйте эту переменную, чтобы задать альтернативного поставщика содержимого (ACP). ACP — это загрузчик, который скачивает содержимое. Последовательность задач использует ACP вместо загрузчика Configuration Manager по умолчанию. Во время скачивания содержимого последовательность задач проверяет эту переменную. Если в ней указано значение, последовательность задач запускает указанную программу для скачивания содержимого.

### <a name="smstsdownloadretrycount"></a><a name="SMSTSDownloadRetryCount"></a> SMSTSDownloadRetryCount

Количество попыток скачивания содержимого из точки распространения средой Configuration Manager. По умолчанию клиент повторяет попытку **2** раза.

### <a name="smstsdownloadretrydelay"></a><a name="SMSTSDownloadRetryDelay"></a> SMSTSDownloadRetryDelay

Время ожидания в секундах перед повторной попыткой скачивания содержимого из точки распространения средой Configuration Manager. По умолчанию клиент ожидает **15** секунд перед повторной попыткой.

### <a name="smstsdriverrequestconnecttimeout"></a><a name="SMSTSDriverRequestConnectTimeOut"></a> SMSTSDriverRequestConnectTimeOut

*Применяется к шагу [Применять драйверы автоматически](task-sequence-steps.md#BKMK_AutoApplyDrivers).*

При запросе каталога драйверов значением этой переменной является количество секунд, в течение которых последовательность задач ожидает подключение к HTTP-серверу. Если подключение занимает больше времени, чем задано параметром времени ожидания, последовательность задач отменяет запрос. Время ожидания по умолчанию составляет **60** секунд.

### <a name="smstsdriverrequestreceivetimeout"></a><a name="SMSTSDriverRequestReceiveTimeOut"></a> SMSTSDriverRequestReceiveTimeOut

*Применяется к шагу [Применять драйверы автоматически](task-sequence-steps.md#BKMK_AutoApplyDrivers).*

При запросе каталога драйверов значением этой переменной является количество секунд, в течение которых последовательность задач ожидает ответ. Если подключение занимает больше времени, чем задано параметром времени ожидания, последовательность задач отменяет запрос. Время ожидания по умолчанию составляет **480** секунд.

### <a name="smstsdriverrequestresolvetimeout"></a><a name="SMSTSDriverRequestResolveTimeOut"></a> SMSTSDriverRequestResolveTimeOut

*Применяется к шагу [Применять драйверы автоматически](task-sequence-steps.md#BKMK_AutoApplyDrivers).*

При запросе каталога драйверов значением этой переменной является количество секунд, в течение которых последовательность задач ожидает разрешение имени HTTP. Если подключение занимает больше времени, чем задано параметром времени ожидания, последовательность задач отменяет запрос. Время ожидания по умолчанию составляет **60** секунд.

### <a name="smstsdriverrequestsendtimeout"></a><a name="SMSTSDriverRequestSendTimeOut"></a> SMSTSDriverRequestSendTimeOut

*Применяется к шагу [Применять драйверы автоматически](task-sequence-steps.md#BKMK_AutoApplyDrivers).*

При запросе каталога драйверов значением этой переменной является количество секунд, в течение которых последовательность задач ожидает отправку запроса. Если запрос занимает больше времени, чем задано параметром времени ожидания, последовательность задач отменяет запрос. Время ожидания по умолчанию составляет **60** секунд.

### <a name="smstserrordialogtimeout"></a><a name="SMSTSErrorDialogTimeout"></a> SMSTSErrorDialogTimeout

При возникновении ошибки в последовательности задач отображается диалоговое окно с ошибкой. Последовательность задач автоматически закрывает его через количество секунд, указанных в этой переменной. Значение по умолчанию: **900** секунд (15 минут).

### <a name="smstslanguagefolder"></a><a name="SMSTSLanguageFolder"></a> SMSTSLanguageFolder

С помощью этой переменной можно изменять язык отображения информации в загрузочных образах, не зависящих от языка.

### <a name="smstslocaldatadrive"></a><a name="SMSTSLocalDataDrive"></a> SMSTSLocalDataDrive

Указывает, где последовательность задач сохраняет временные файлы кэша при выполнении на конечном компьютере.

Обязательно задайте эту переменную перед запуском последовательности задач, например, задав переменную коллекции. После запуска последовательности задач Configuration Manager определяет переменную [_SMSTSMDataPath](#SMSTSMDataPath) в зависимости от того, какое значение определено в переменной SMSTSLocalDataDrive.

### <a name="smstsmp"></a><a name="SMSTSMP"></a> SMSTSMP

Используйте эту переменную, чтобы указать URL- или IP-адрес точки управления Configuration Manager.

### <a name="smstsmplistrequesttimeoutenabled"></a><a name="SMSTSMPListRequestTimeoutEnabled"></a> SMSTSMPListRequestTimeoutEnabled

*Применяется к следующим шагам:*  

- [Установить приложение](task-sequence-steps.md#BKMK_InstallApplication)  
- [Установить обновления программного обеспечения](task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  

(входная)

Используйте эту переменную для включения повторяющихся запросов MPList, чтобы обновить клиент, если он находится не в интрасети. По умолчанию для переменной задано значение `True`.

Если клиенты находятся в Интернете, присвойте этой переменной значение `False`, чтобы избежать ненужных задержек.

### <a name="smstsmplistrequesttimeout"></a><a name="SMSTSMPListRequestTimeout"></a> SMSTSMPListRequestTimeout

*Применяется к следующим шагам:*  

- [Установить приложение](task-sequence-steps.md#BKMK_InstallApplication)  
- [Установить обновления программного обеспечения](task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  

(входная)

Эта переменная указывает, сколько миллисекунд последовательность задач будет ожидать перед повторной попыткой выполнить шаг, который не смог получить список точек управления из служб обнаружения расположения. По умолчанию время ожидания перед повторной попыткой составляет `60000` мс (60 с). Выполняется не более трех повторных попыток.

### <a name="smstspeerdownload"></a><a name="SMSTSPeerDownload"></a> SMSTSPeerDownload

Используйте эту переменную, чтобы позволить клиенту использовать одноранговый кэш Windows PE. Эта функция включается при значении `true` для этой переменной.

### <a name="smstspeerrequestport"></a><a name="SMSTSPeerRequestPort"></a> SMSTSPeerRequestPort

Пользовательское значение сетевого порта, который используется одноранговым кэшем среды предустановки Windows PE для начального вещания. В параметрах клиента по умолчанию настраивается порт **8004**.

### <a name="smstspersistcontent"></a><a name="SMSTSPersistContent"></a> SMSTSPersistContent

С помощью этой переменной можно временно хранить содержимое в кэше последовательности задач. Значение этой переменной отличается от [SMSTSPreserveContent](#SMSTSPreserveContent), которая хранит содержимое в кэше клиента Configuration Manager после завершения последовательности задач. Переменная SMSTSPersistContent использует кэш последовательности задач, а переменная SMSTSPreserveContent — кэш клиента Configuration Manager.

### <a name="smstspostaction"></a><a name="SMSTSPostAction"></a> SMSTSPostAction

Задает команду, которая выполняется после завершения последовательности задач. Например, укажите `shutdown.exe /r /t 30 /f`, чтобы перезагрузить компьютер через 30 секунд после выполнения последовательности задач.

### <a name="smstspreferredadvertid"></a><a name="SMSTSPreferredAdvertID"></a> SMSTSPreferredAdvertID

Заставляет последовательность задач запускать на конечном компьютере определенное целевое развертывание. Задайте эту переменную с помощью выполняемой перед запуском команды с носителя или посредством PXE. Если эта переменная задана, последовательность задач переопределяет все обязательные развертывания.

### <a name="smstspreservecontent"></a><a name="SMSTSPreserveContent"></a> SMSTSPreserveContent

Эта переменная указывает, что содержимое в последовательности задач должно сохраняться в кэше клиента Configuration Manager после развертывания. Она отличается от переменной [SMSTSPersistContent](#SMSTSPersistContent), которая сохраняет содержимое только на время выполнения последовательности задач. Переменная SMSTSPersistContent использует кэш последовательности задач, а переменная SMSTSPreserveContent — кэш клиента Configuration Manager. Чтобы включить эту функцию, задайте для SMSTSPreserveContent значение `true`.

### <a name="smstsrebootdelay"></a><a name="SMSTSRebootDelay"></a> SMSTSRebootDelay

Задает время ожидания в секундах перед перезагрузкой компьютера. Если значение этой переменной равно нулю (0), диспетчер последовательности задач не отображает диалоговое окно с предупреждением перед перезагрузкой компьютера.

#### <a name="example"></a>Пример

- `0` — не отображать уведомление;  

- `60` — отображать уведомление в течение одной минуты.  

### <a name="smstsrebootdelaynext"></a><a name="SMSTSRebootDelayNext"></a> SMSTSRebootDelayNext

<!--4447680-->
Начиная с версии 1906, используйте эту переменную с имеющейся переменной [SMSTSRebootDelay](task-sequence-variables.md#SMSTSRebootDelay). Чтобы последующие перезагрузки выполнялись со временем ожидания, отличным от первого, установите для SMSTSRebootDelayNext другое значение в секундах.

#### <a name="example"></a>Пример

Вы хотите, чтобы пользователи получали уведомление о перезагрузке за 60 минут до нее при запуске последовательности задач обновления на месте Windows 10. После этого первого длительного времени ожидания вы хотите, чтобы дополнительные периоды ожидания составляли всего 60 секунд. Установите для SMSTSRebootDelay значение `3600`, а для SMSTSRebootDelayNext — значение `60`.  


### <a name="smstsrebootmessage"></a><a name="SMSTSRebootMessage"></a> SMSTSRebootMessage

Задает сообщение, отображаемое в диалоговом окне уведомления о перезагрузке. Если эта переменная не задана, отображается сообщение по умолчанию.

#### <a name="example"></a>Пример

`The task sequence is restarting this computer`

### <a name="smstsrebootrequested"></a><a name="SMSTSRebootRequested"></a> SMSTSRebootRequested

Указывает, что после выполнения текущего шага последовательности задач требуется перезагрузка. Присвойте значение этой переменной, если для завершения выполнения шага последовательности задач требуется перезагрузка. После перезагрузки компьютера выполнение последовательности задач продолжится со следующего шага.

- `HD`: перезагрузка в установленную ОС
- `WinPE`: перезагрузка в связанный образ загрузки

### <a name="smstsretryrequested"></a><a name="SMSTSRetryRequested"></a> SMSTSRetryRequested

Запрашивает повторную попытку после завершения текущего шага последовательности задач. Если установлена эта переменная последовательности задач, для переменной [SMSTSRebootRequested](#SMSTSRebootRequested) должно быть задано значение `true`. После перезагрузки компьютера диспетчер последовательности задач повторно выполнит тот же шаг последовательности задач.

### <a name="smstsruncommandlineasuser"></a><a name="SMSTSRunCommandLineAsUser"></a> SMSTSRunCommandLineAsUser

*Начиная с версии 2002* <!-- 5573175 -->  
*Применяется к шагу [Выполнить из командной строки](task-sequence-steps.md#BKMK_RunCommandLine).*

Задайте переменные последовательности задач, чтобы настроить пользовательский контекст для шага **Запуск командной строки**. Не нужно настраивать шаг **Запуск командной строки** с учетной записью-заполнителем, чтобы использовать переменные [SMSTSRunCommandLineUserName](task-sequence-variables.md#SMSTSRunCommandLineUserName) и [SMSTSRunCommandLineUserPassword](task-sequence-variables.md#SMSTSRunCommandLineUserPassword).

Настройте `SMSTSRunCommandLineAsUser` с одним из следующих значений:

- `true`: все последующие шаги **Запуск командной строки** выполняются в контексте, указанном пользователем в `SMSTSRunCommandLineUserName`.

- `false`: все последующие шаги **Запуск командной строки** выполняются в контексте, настроенном в шаге.

### <a name="smstsruncommandlineusername"></a><a name="SMSTSRunCommandLineUserName"></a> SMSTSRunCommandLineUserName

*Применяется к шагу [Выполнить из командной строки](task-sequence-steps.md#BKMK_RunCommandLine).*

(входная)

Указывает учетную запись, которая используется при выполнении командной строки. Значением этой переменной является строка формата "имя_пользователя" или "домен\имя_пользователя". Укажите пароль для учетной записи в переменной [SMSTSRunCommandLineUserPassword](#SMSTSRunCommandLineUserPassword).

> [!NOTE]
> Начиная с версии 2002, используйте переменную [SMSTSRunCommandLineAsUser](task-sequence-variables.md#SMSTSRunCommandLineAsUser) с этой переменной, чтобы настроить контекст пользователя для этого шага.
>
> В версии 1910 и более ранней настройте для шага **Выполнить из командной строки** параметр **Запустить этот шаг в виде следующей учетной записи**. Когда вы включаете этот параметр и задаете имя пользователя и пароль с помощью переменных, укажите любое значение для учетной записи.

Дополнительные сведения об учетной записи, позволяющей выполнить последовательность задач от имени другого пользователя, см. в разделе [Accounts](../../core/plan-design/hierarchy/accounts.md#task-sequence-run-as-account) (Учетные записи).

### <a name="smstsruncommandlineuserpassword"></a><a name="SMSTSRunCommandLineUserPassword"></a> SMSTSRunCommandLineUserPassword

*Применяется к шагу [Выполнить из командной строки](task-sequence-steps.md#BKMK_RunCommandLine).*

(входная)

Указывает пароль для учетной записи, которая определена в переменной [SMSTSRunCommandLineUserName](#SMSTSRunCommandLineUserName).

### <a name="smstsrunpowershellasuser"></a><a name="SMSTSRunPowerShellAsUser"></a> SMSTSRunPowerShellAsUser

*Начиная с версии 2002* <!-- 5573175 -->  
*Применяется к шагу [Запустить сценарий PowerShell](task-sequence-steps.md#BKMK_RunPowerShellScript).*

Используйте переменные последовательности задач, чтобы настроить пользовательский контекст для шага **Запуск скрипта PowerShell**. Не нужно настраивать шаг **Запуск скрипта PowerShell Script** с учетной записью — заполнителем, чтобы использовать переменные [SMSTSRunPowerShellUserName](task-sequence-variables.md#SMSTSRunPowerShellUserName) и [SMSTSRunPowerShellUserPassword](task-sequence-variables.md#SMSTSRunPowerShellUserPassword).

Настройте `SMSTSRunPowerShellAsUser` с одним из следующих значений:

- `true`: все последующие шаги **Запуск скрипта PowerShell** выполняются в контексте, указанном пользователем в `SMSTSRunPowerShellUserName`.

- `false`: все последующие шаги **Запуск скрипта PowerShell** выполняются в контексте, настроенном в шаге.

### <a name="smstsrunpowershellusername"></a><a name="SMSTSRunPowerShellUserName"></a> SMSTSRunPowerShellUserName

*Применяется к шагу [Запустить сценарий PowerShell](task-sequence-steps.md#BKMK_RunPowerShellScript).*

(входная)

Указывает учетную запись, которая используется при выполнении сценария PowerShell. Значением этой переменной является строка формата "имя_пользователя" или "домен\имя_пользователя". Укажите пароль для учетной записи в переменной [SMSTSRunPowerShellUserPassword](#SMSTSRunPowerShellUserPassword).

> [!NOTE]
> Чтобы использовать эти переменные, настройте для шага **Запустить сценарий PowerShell** параметр **Запустите этот этап в виде следующей учетной записи**. Когда вы включаете этот параметр и задаете имя пользователя и пароль с помощью переменных, укажите любое значение для учетной записи.

Дополнительные сведения об учетной записи, позволяющей выполнить последовательность задач от имени другого пользователя, см. в разделе [Accounts](../../core/plan-design/hierarchy/accounts.md#task-sequence-run-as-account) (Учетные записи).

### <a name="smstsrunpowershelluserpassword"></a><a name="SMSTSRunPowerShellUserPassword"></a> SMSTSRunPowerShellUserPassword

*Применяется к шагу [Запустить сценарий PowerShell](task-sequence-steps.md#BKMK_RunPowerShellScript).*

(входная)

Указывает пароль для учетной записи, которая определена в переменной [SMSTSRunPowerShellUserName](#SMSTSRunPowerShellUserName).

### <a name="smstssoftwareupdatescantimeout"></a><a name="SMSTSSoftwareUpdateScanTimeout"></a> SMSTSSoftwareUpdateScanTimeout

*Применяется к шагу [Установить обновления программного обеспечения](task-sequence-steps.md#BKMK_InstallSoftwareUpdates).*

(входная)

Управляет временем ожидания для проверки обновлений программного обеспечения при выполнении этого шага. Например, увеличьте значение, если во время проверки ожидается большое количество обновлений. Значение по умолчанию: `3600` с (60 мин). Значение переменной задается в секундах.

### <a name="smstsudausers"></a><a name="SMSTSUDAUsers"></a> SMSTSUDAUsers

Перечисляет основных пользователей конечного компьютера, используя следующий формат: `<DomainName>\<UserName>`. Разделите пользователей с помощью запятой (`,`). Дополнительные сведения см. в разделе [Связывание пользователей с конечным компьютером](../get-started/associate-users-with-a-destination-computer.md).

#### <a name="example"></a>Пример

`contoso\jqpublic, contoso\megb, contoso\janedoh`

### <a name="smstswaitforsecondreboot"></a><a name="SMSTSWaitForSecondReboot"></a> SMSTSWaitForSecondReboot

*Применяется к шагу [Установить обновления программного обеспечения](task-sequence-steps.md#BKMK_InstallSoftwareUpdates).*

(входная)

Эта необязательная переменная последовательности задач управляет поведением клиента, когда для установки обновления программного обеспечения требуются две перезагрузки. Задайте ее перед этим шагом, чтобы избежать сбоя последовательности задач из-за второй перезагрузки при установке обновления программного обеспечения.

Задайте переменной SMSTSWaitForSecondReboot значение в секундах, чтобы указать продолжительность приостановки последовательности задач на этом шаге при перезагрузке компьютера. Выделите достаточно времени на случай второй перезагрузки.

Например, если переменной SMSTSWaitForSecondReboot задать значение `600`, последовательность задач приостановится на 10 минут после перезагрузки, прежде чем начнет выполнение следующих шагов. Эта переменная полезна, когда в рамках одного шага последовательности задач "Установить обновления программного обеспечения" устанавливаются сотни обновлений программного обеспечения.

> [!Note]
> Эта переменная применяется только к последовательности задач, которая развертывает ОС. Она не работает в настраиваемой последовательности задач. <!-- 2839998 -->

### <a name="tsdebugmode"></a><a name="TSDebugMode"></a> TSDebugMode

<!--3612274-->
Начиная с версии 1906, задавайте этой переменной значение `TRUE` для коллекции или объекта-компьютера, где развертывается последовательность задач. Любое устройство с таким значением этой переменной поместит все последовательности задач, развернутые на него, в режим отладки.

Дополнительные сведения см. в статье [Отладка последовательности задач](../deploy-use/debug-task-sequence.md).

### <a name="tsdebugonerror"></a><a name="TSDebugOnError"></a> TSDebugOnError

<!-- 5012536 -->
Начиная с версии 1910, задавайте этой переменной значение `TRUE`, чтобы автоматически запускать [Отладчик последовательности задач](../deploy-use/debug-task-sequence.md), когда последовательность задач возвращает ошибку.

Задайте эту переменную, используя следующее:

- Шаг [Задать переменную последовательности задач](task-sequence-steps.md#BKMK_SetTaskSequenceVariable)

- Переменная коллекции. Дополнительные сведения см. в разделе об [установке переменных](using-task-sequence-variables.md#bkmk_set).

### <a name="tsdisableprogressui"></a><a name="TSDisableProgressUI"></a> TSDisableProgressUI

<!-- 1354291 -->
Используйте эту переменную, чтобы управлять отображением сведений о ходе выполнения для пользователей. Чтобы скрывать и отображать ход выполнения в разное время, задайте эту переменную в последовательности задач несколько раз.  

- `true`: Скрытие хода выполнения последовательности задач  

- `false`: отобразить ход выполнения последовательности задач.  

### <a name="tserroronwarning"></a><a name="TSErrorOnWarning"></a> TSErrorOnWarning

*Применяется к шагу [Установить приложение](task-sequence-steps.md#BKMK_InstallApplication).*

(входная)

Укажите, рассматривает ли подсистема последовательности задач обнаруженное предупреждение как ошибку во время выполнения этого шага. Последовательность задач устанавливает для переменной [_TSAppInstallStatus](#TSAppInstallStatus) значение `Warning`, если по меньшей мере одно приложение или требуемая зависимость не установлены из-за несоответствия требованиям. Если этой переменной задано значение `True` и последовательность задач задает для **_TSAppInstallStatus** значение `Warning`, возникнет ошибка. Значение `False` определяет поведение по умолчанию.

### <a name="tsprogressinfolevel"></a><a name="TSProgressInfoLevel"></a> TSProgressInfoLevel

*Начиная с версии 2002*<!--5932692-->  

Укажите эту переменную, чтобы управлять типом информации, отображаемой в окне хода выполнения последовательности задач. Эта переменная может принимать следующие значения.

- `1`: включение текущего шага и общего количества шагов в текст хода выполнения. Например, **2 из 10**.
- `2`: включение текущего шага, общего количества шагов и процента выполнения. Например, **2 из 10 (выполнено 20 %)** .
- `3`: включение процента выполнения. Например, **(выполнено 20 %)** .

### <a name="workingdirectory"></a><a name="WorkingDirectory"></a> WorkingDirectory

*Применяется к шагу [Выполнить из командной строки](task-sequence-steps.md#BKMK_RunCommandLine).*

(входная)

Задает начальный каталог для действия командной строки. Указанное имя каталога не должно быть длиннее 255 символов.

#### <a name="examples"></a>Примеры

- `C:\`  
- `%SystemRoot%`  


## <a name="deprecated-variables"></a>Устаревшие переменные

Устаревшими считаются следующие переменные:

- **OSDAllowUnsignedDriver**: не используется при развертывании Windows Vista и более поздних версий операционной системы;
- **OSDBuildStorageDriverList**: этот параметр применим только в операционных системах Windows XP и Windows Server 2003.
- **OSDDiskpartBiosCompatibilityMode**: применяется только при развертывании Windows XP или Windows Server 2003.
- **OSDInstallEditionIndex**: не требуется после Windows Vista.
- **OSDPreserveDriveLetter**: дополнительные сведения см. в разделе [OSDPreserveDriveLetter](#osdpreservedriveletter).

### <a name="osdpreservedriveletter"></a>OSDPreserveDriveLetter

> [!Important]
> Использовать эту переменную последовательности задач не рекомендуется.
>
> Во время развертывания операционной системы программа установки Windows по умолчанию самостоятельно определяет оптимальную букву диска (обычно диск C:).

*Предыдущее поведение*: при применении образа переменная OSDPreverveDriveLetter определяет, использует ли последовательность задач букву диска, записанную в WIM-файле образа. Задайте для этой переменной значение `false`, чтобы использовать расположение, указанное в параметре **Назначение** на шаге последовательности задач **Применить операционную систему**. См. дополнительные сведения о [применении образа операционной системы](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).


## <a name="see-also"></a>См. также

- [Шаги последовательности задач](task-sequence-steps.md)
- [Использование переменных последовательности задач](using-task-sequence-variables.md).
- [Вопросы планирования для автоматизации задач](../plan-design/planning-considerations-for-automating-tasks.md)
