---
title: CMTrace
titleSuffix: Configuration Manager
description: Сведения о том, как использовать средство CMTrace для просмотра файлов журналов для Configuration Manager.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6a4a3290-5228-4871-918a-554aa1c20834
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8c9c42dcd1e6a6a4ca064953f0513157f5ebb228
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707902"
---
# <a name="cmtrace"></a>CMTrace

*Область применения: Configuration Manager (Current Branch)*

CMTrace является одним из [средств Configuration Manager](tools.md). Оно позволяет просматривать и отслеживать файлы журналов, включая следующие:  

- Файлы журналов в формате Configuration Manager или Client Component Manager (CCM)  

- Обычные текстовые файлы в формате ASCII или Юникода, например журналы установщика Windows  

Это средство помогает анализировать файлы журналов благодаря функциям выделения, фильтрации и поиска ошибок.

Начиная с версии 1806 средство просмотра журналов CMTrace автоматически устанавливается вместе с клиентом Configuration Manager. Оно добавляется в каталог установки клиента. По умолчанию это каталог `%WinDir%\CCM\CMTrace.exe`.<!--1357971-->

> [!Note]  
> CMTrace не регистрируется в Windows автоматически для открытия файлов с расширением LOG. Дополнительные сведения см. в разделе [Сопоставления файлов](#file-associations).  

Начиная с версии 1906, **OneTrace** является новым средством просмотра журналов для центра поддержки. Оно работает аналогично CMTrace, но обладает некоторыми усовершенствованиями. Дополнительные сведения о средстве OneTrace для центра поддержки см. [здесь](support-center-onetrace.md).

## <a name="usage"></a>Использование

Запустите **CMTrace.exe**. При первом запуске средства появляется запрос для сопоставления файлов. Дополнительные сведения см. в разделе [Сопоставления файлов](#file-associations).

Большинство операций CMTrace выполняется из следующих меню:

- [File](#file-menu)
- [Сервис](#tools-menu)

### <a name="file-menu"></a>Меню "Файл"

В меню **Файл** доступны приведенные ниже действия.  

- [Открыть](#open)
- [Open on Server](#open-on-server) (Открыть на сервере)
- [Печать](#print)
- [Настройки](#preferences)

В меню "Файл" также указаны восемь последних файлов. Чтобы быстро открыть один из этих журналов, выберите его в меню "Файл".

#### <a name="open"></a>Открыть

Отображает диалоговое окно "Открыть" для поиска файла журнала.

В представлении можно отфильтровать файлы следующих типов:

- Файлы журналов (\*.log)  
- Старые файлы журналов (\*.lo_)
- Все файлы (\*.\*)

Следующие два параметра не используются по умолчанию:  

- **Ignore existing lines** (Игнорировать существующие строки): при выборе этого параметра CMTrace игнорирует существующее содержимое выбранного файла журнала и отображает только новые строки по мере их добавления. Используйте этот параметр, чтобы отслеживать только новые действия, когда не требуется изучать файл журнала полностью.  

- **Merge selected files** (Объединить выбранные файлы): если включить этот параметр и выбрать несколько файлов журналов, CMTrace объединяет выбранные журналы в этом представлении. Они отображаются так, как если бы являлись одним файлом журнала. Объединенный журнал обновляется так же и поддерживает все остальные функции CMTrace, как если бы это был отдельный файл журнала.  

#### <a name="open-on-server"></a>Open on Server (Открыть на сервере)

Позволяет просмотреть папки журналов Configuration Manager на компьютере системы сайта с помощью стандартного диалогового окна просмотра. Вы также можете просмотреть сеть для удаленного компьютера.

Когда вы выбираете удаленный компьютер для просмотра, CMTrace проверяет общую папку Configuration Manager. Если найти общую папку с файлами журналов Configuration Manager не удается, отображается сообщение об ошибке.  

Чтобы подключиться непосредственно к известному компьютеру без просмотра, используйте действие [Открыть](#open). Затем введите имя сервера и общей папки в формате UNC.

#### <a name="print"></a>Печать

Позволяет отобразить стандартное диалоговое окно печати Windows. Это действие отправляет текущий файл журнала на принтер. Оно форматирует выходные данные в соответствии с параметрами на вкладке "Печать" в настройках CMTrace.

#### <a name="preferences"></a>Настройки

Позволяет настроить параметры для CMTrace. Доступны следующие параметры.  

- Вкладка**Общие**  

    - **Update Interval** (Интервал обновления): определяет, как часто CMTrace проверяет наличие изменений в файлах журналов и загружает новые строки. По умолчанию это значение составляет 500 миллисекунд.  

    - **Выделить**: задает цвет, используемый CMTrace для выделения выбранных вами строк журнала. По умолчанию используется базовый желтый цвет (красный: 255, зеленый: 255, синий: 0).  

    - **Столбцы**: настраивает столбцы, видимые в представлении журнала, и порядок их отображения. По умолчанию отображаются столбцы "Текст журнала", "Компонент", "Дата/время" и "Поток".  

- Вкладка **Печать**  

    - **Столбцы**: настраивает столбцы, используемые при печати файлов журналов, и их порядок. По умолчанию распечатывает те же столбцы, которые и отображает.  

    - **Ориентация**: задает ориентацию печати по умолчанию при печати файлов журналов. Переопределите этот параметр в диалоговом окне печати. По умолчанию использует книжную ориентацию.  

- Вкладка **Дополнительно**  

    - **Интервал обновления**: принуждает CMTrace обновлять представления журналов с заданным интервалом при загрузке большого количества строк. По умолчанию этот параметр отключен с нулевым значением.  

        > [!Note]  
        > В общем случае изменять **Интервал обновления** не следует. Он может значительно увеличить время, необходимое для открытия больших файлов журналов.

### <a name="tools-menu"></a>Меню "Сервис"

В меню **Сервис** доступны приведенные ниже действия.

- [Найти](#find)
- [Найти далее](#find-next)
- [Копировать в буфер обмена](#copy-to-clipboard)
- [Выделить](#highlight)
- [Фильтр](#filter)
- [Поиск ошибки](#error-lookup)
- [Пауза](#pause)
- [Показать/скрыть подробности](#showhide-details)
- [Show/Hide Info Pane](#showhide-info-pane) (Показать/скрыть область информации)

#### <a name="find"></a>Найти

Позволяет найти конкретную текстовую строку в открытом файле журнала.  

#### <a name="find-next"></a>Найти далее

Позволяет найти следующее совпадение для строки, указанной ранее в диалоговом окне поиска.  

#### <a name="copy-to-clipboard"></a>Копировать в буфер обмена

Копирует выбранные строки в буфер обмена в виде обычного текста. Если вы изучаете Configuration Manager и файлы журналов CCM, это действие копирует столбцы в том же порядке, что и в представлении. При этом каждый столбец отделяется символом табуляции. Используйте это действие при копировании журналов в сообщения электронной почты или другие документы.  

#### <a name="highlight"></a>Выделить

Введите строку, которую CMTrace использует для поиска в тексте каждой записи журнала. Затем действие выделяет любой текст журнала, который соответствует введенной строке.  

- Для выделения используется цвет, указанный в настройках.  

- Чтобы отключить выделение, удалите строку из этого поля.  

- При вводе десятичного или шестнадцатеричного числа CMTrace пытается сопоставить значение со столбцом потока. Используйте это поведение, чтобы выделить обработку из одного потока, не отфильтровывая другие потоки, которые могут с ним взаимодействовать.  

- Чтобы сравнить строки по регистру, включите параметр **С учетом регистра**.  

#### <a name="filter"></a>Фильтр

Позволяет показать или скрыть строки журнала на основе заданных критериев. Вы можете применить фильтры к любому из четырех столбцов, независимо от того, видимы ли они. Эти параметры применяются к каждому открытому файлу журнала.

Примеры:
<!--SCCMDocs issue #603-->

- Фильтрация **smsts.log** по тексту записи, содержащему "the action" или "the group".
- Фильтрация **InventoryAgent.log**, где текст записи содержит "destination".

#### <a name="error-lookup"></a>Поиск ошибки

Позволяет ввести или вставить код ошибки в десятичном или шестнадцатеричном формате, чтобы просмотреть его описание. Возможные источники ошибки включают: Windows, WMI или Winhttp.

#### <a name="pause"></a>Пауза

Позволяет приостановить или перезапустить отслеживание журнала. В следующих вариантах применения приведены некоторые возможные причины для использования этого действия:  

- Когда CMTrace отображает сведения файла журнала слишком быстро  

- При приостановке отслеживания журнала сведения, отображаемые в CMTrace, не будут потеряны при переносе текущего файла в новый журнал  

- Если нужно остановить вывод новых данных CMTrace, пока вы просматриваете файл журнала  

#### <a name="showhide-details"></a>Показать/скрыть подробности

Позволяет показать или скрыть все столбцы, кроме текста журнала. Кроме того, расширяет столбец текста журнала до ширины окна. Это действие используется при просмотре журналов на компьютере с низким разрешением экрана. Оно отображает больше текста журнала.  

> [!Note]  
> При просмотре файлов в формате обычного текста CMTrace автоматически скрывает подробности, так как они всегда пусты.  

#### <a name="showhide-info-pane"></a>"Show/Hide Info Pane" (Показать/скрыть область информации)

Позволяет показать/скрыть область информации. Это действие используется при просмотре журналов на компьютере с низким разрешением экрана. Оно отображает больше сведений журнала.  


## <a name="log-pane"></a>Область журналов

Область журналов находится в верхней части окна CMTrace. В ней отображаются строки из файлов журналов.

При выборе строки она временно выделяется с использованием выбранной для Windows цветовой схемы.

Выделенные строки соответствуют условиям, определенным с помощью параметра **Выделить** в меню **Сервис**. Для выделения используется цвет, указанный в меню **Настройки**.

CMTrace отображает строки с ошибками, используя красный цвет фона и желтый цвет текста. В журналах формата CCM записи имеют явное значение типа, обозначающее запись как ошибку. Для других форматов журналов CMTrace ищет текстовую строку "error" без учета регистра в каждой записи.

Строки с предупреждениями отображаются на желтом фоне. В журналах формата CCM записи имеют явное значение типа, обозначающее запись как предупреждение. Для других форматов журналов CMTrace ищет текстовую строку "warn" без учета регистра в каждой записи.


## <a name="info-pane"></a>Область информации

Область информации находится в нижней части окна CMTrace. Она включает следующие компоненты.

- Сведения о выбранной записи журнала  

- Текстовое поле, отображающее текст журнала  

- Отображение символов возврата каретки, чтобы форматированный текст было удобнее читать  

- Более удобное чтение длинных записей, которые отображаются в области журналов не полностью  

Показать или скрыть область информации можно с помощью параметра **Show/Hide Info Pane** (Показать/скрыть область информации) в меню **Сервис**. Если область информации занимает больше половины окна журнала, CMTrace автоматически скрывает ее.

### <a name="progress-bar"></a>Индикатор выполнения

При первом открытии файла журнала CMTrace заменяет область информации индикатором хода выполнения. Он указывает, сколько существующего содержимого файла загружено. Когда ход выполнения достигает 100 процентов, CMTrace удаляет индикатор хода выполнения и заменяет его областью информации. При загрузке больших файлов такое поведение позволяет узнать, сколько времени может занять загрузка.

### <a name="status-bar"></a>Строка состояния

Для файлов журналов в формате Configuration Manager и CCM строка состояния отображает время для выбранных записей журнала. Если выбрать одну запись, средство отображает время от первой записи журнала до выбранной записи. Если выбрать несколько записей, оно вычисляет время от самой верхней до самой нижней выбранной записи. CMTrace форматирует эти сведения следующим образом:

`Elapsed time is <hours>h <minutes>m <seconds>s <milliseconds>ms (<seconds+milliseconds> seconds)`


## <a name="windows-shell-integration"></a>Интеграция с оболочкой Windows

CMTrace поддерживает [сопоставления файлов](#file-associations) и [перетаскивание](#drag-and-drop).

### <a name="file-associations"></a>Сопоставления файлов

CMTrace можно сопоставить с расширениями имен файлов LOG и LO_. При запуске средство проверяет реестр, чтобы определить, сопоставлено ли оно уже с этими расширениями. Если CMTrace не сопоставлено с каким-либо расширением имени файла, вам будет предложено сопоставить расширения имен файлов с CMTrace. При выборе параметра **Больше не спрашивать** CMTrace пропускает эту проверку при запуске на данном компьютере.

### <a name="drag-and-drop"></a>Перетаскивание

CMTrace поддерживает основные функции перетаскивания. Перетащите файл журнала из проводника в CMTrace, чтобы открыть его.


## <a name="other-tips"></a>Другие советы

### <a name="last-directory-registry-key"></a>Раздел реестра "Last Directory" (Последний каталог)

<!--511280-->
По умолчанию CMTrace сохраняет расположение последнего открытого журнала. Это удобно на сервере сайта, так как он каждый раз по умолчанию использует путь к журналам.

При первом его запуске на клиенте он по умолчанию использует текущий рабочий каталог. Это расположение может быть путем, по которому вы сохранили CMTrace, или путем вида `%userprofile%\Desktop`.

Значение **Last Directory** (Последний каталог) в разделе реестра `HKEY_CURRENT_USER\Software\Microsoft\Trace32` управляет этим расположением по умолчанию. Если присвоить этому значению `%windir%\CCM\Logs` на клиентах, то при первом запуске CMTrace открывает файлы в расположении журналов клиента.


## <a name="see-also"></a>См. также

- [Файлы журнала](../plan-design/hierarchy/log-files.md)

- [Средство просмотра файлов журнала центра поддержки](support-center.md#support-center-log-file-viewer)

- [Средство OneTrace для центра поддержки](support-center-onetrace.md)
