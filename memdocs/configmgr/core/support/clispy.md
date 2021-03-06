---
title: Client Spy
titleSuffix: Configuration Manager
description: Используйте Client Spy для устранения неполадок с распространением программного обеспечения, инвентаризацией и контролем использования программных продуктов на клиентах Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 60575413-44fe-43bb-bcfb-39ec5ed5055b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 43c3d0f25cf9a71bf07189315ee5f11eba47de1d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707912"
---
# <a name="client-spy"></a>Client Spy

*Область применения: Configuration Manager (Current Branch)*

Client Spy является одним из [средств Configuration Manager](tools.md). Оно предназначено для устранения неполадок с распространением программного обеспечения, инвентаризацией и контролем использования программных продуктов на клиентах Configuration Manager. 

Основная часть информации, полученной с помощью этого средства, относится к развертываниям программного обеспечения:
- Все текущие развертывания программного обеспечения 
- Журнал распространения программного обеспечения
- Конфигурация кэша клиента
- Кэшированные элементы
- Ожидающие необходимые развертывания
- Доступные развертывания  

Оно также содержит следующие сведения инвентаризации:
- Дата последнего цикла инвентаризации
- Дата последнего отчета
- Основной и дополнительный номера версий для инвентаризации программного обеспечения
- Сбор файлов
- Инвентаризация оборудования
- Сбор IDMIF
- Записи данных обнаружения (DDR) 

Также отображаются правила контроля использования программных продуктов. 

> [!Note]   
> Для повышения производительности средство собирает сведения для каждой из вкладок только при ее открытии. Аналогичным образом, при нажатии кнопки **Обновить** оно обновляет только данные для открытой вкладки.



## <a name="usage"></a>Использование


### <a name="tools-menu"></a>Меню "Сервис"

В меню **Сервис** доступны приведенные ниже действия.  

#### <a name="connect"></a>Подключить
Получение сведений с другого компьютера.  

- По умолчанию средство отображает данные с текущего компьютера. 

- Подключение с использованием имени удаленного компьютера, имени пользователя и пароля для учетной записи. Средство подключается к общей папке IPC$ на удаленном компьютере. Это соединение удаляется при завершении работы средства или при подключении к другому компьютеру.  

- Требуется учетная запись с достаточными правами для получения сведений.  

- Если не указать имя пользователя и пароль, Client Spy использует контекст безопасности вошедшего в систему пользователя, чтобы предпринять попытку подключения.  

- При подключении к удаленному компьютеру сведения на всех отображаемых вкладках относятся к удаленному компьютеру.

#### <a name="software-distribution"></a>Распространение программного обеспечения
Отображает вкладки [Распространение программного обеспечения](#software-distribution) и скрывает другие вкладки. По умолчанию Client Spy отображает вкладки "Распространение программного обеспечения".

#### <a name="inventory"></a>Inventory (Товары)
Отображает вкладку "Инвентаризация" и скрывает другие вкладки.

#### <a name="software-metering"></a>Контроль за использованием программного обеспечения
Отображает вкладку "Отслеживание использования программного обеспечения" и скрывает другие вкладки.

#### <a name="save-current-tab-to-file"></a>Save current tab to file (Сохранить текущую вкладку в файл)
Сохраняет данные с открытой вкладки в указанный вами текстовый файл. 

#### <a name="save-all-tabs-to-file"></a>Save all tabs to file (Сохранить все вкладки в файл)
Сохраняет данные со всех вкладок в указанный вами текстовый файл. Сохраняются только сведения, доступные для вашей учетной записи.



## <a name="software-distribution-tab"></a>Вкладка "Распространение программного обеспечения"

Настройте параметры на следующих четырех вкладках:
- [Software Distribution Execution Requests](#bkmk_exec-requests) (Запросы на выполнение распространения программного обеспечения)
- [Software Distribution History](#bkmk_history) (Журнал распространения программного обеспечения)
- [Software Distribution Cache Information](#bkmk_cache-info) (Информация о кэше распространения программного обеспечения)
- [Software Distribution Pending Executions](#bkmk_pending-exec) (Ожидающие выполнения распространения программного обеспечения)


### <a name="software-distribution-execution-requests"></a><a name="bkmk_exec-requests"></a> "Software Distribution Execution Requests" (Запросы на выполнение распространения программного обеспечения)

Эта вкладка отображает все существующие развертывания, ориентированные как на устройства, так и на пользователей.

Каждый элемент дерева на вкладке "Software Distribution Execution Requests" (Запросы на выполнение распространения программного обеспечения) содержит четыре следующих атрибута:
- ИД объявления. Данное значение может быть пустым, если это доступное развертывание. 
- ИД пакета 
- Имя программы 
- Пользователь. Это может быть идентификатор безопасности конечного пользователя или пользователя, который инициировал запрос. Если оба запроса являются системными, отображает системный пользователь. 

Для каждого запущенного запроса также отображает следующие сведения в структуре поддерева:
- Имя программы 
- ИД пакета 
- Имя пакета 
- Request Creation Time (Время создания запроса) 
- Состояние 
- Running State (Состояние выполнения), если указано запущенное состояние 
- Execution Context (Контекст выполнения) — User или Admin 
- History State (Состояние журнала ) — Success, Failure или NotRun 
- LastRunTime (Never, если программа не запускалась ранее) 
- RetryCount, если State имеет значение WaitingRetry 
- ContentAccess (Retry Count, если State имеет значение WaitingRetry) 
- FailureCode, если State имеет значение WaitingRetry 
- FailureReason, если State имеет значение WaitingRetry 

Если запросу требуется содержимое, состояние имеет значение WaitingContent. Вкладка "Software Distribution Cache Information" (Информация о кэше распространения программного обеспечения) отображает сведения для этого запроса на скачивание.

Если запрос на выполнение является запросом на скачивание, также отображается число скачанных байтов.

> [!Note]   
> Для обозначения различных состояний запроса на выполнение используются разные значки.


### <a name="software-distribution-history"></a><a name="bkmk_history"></a> "Software Distribution History" (Журнал распространения программного обеспечения)

Эта вкладка содержит сведения обо всех ранее запущенных программах. Эта информация хранится в реестре.

Основными ветвями этого дерева являются разные журналы пользователей, включая системные. Отображается поддерево со списком пакетов, откуда запускались программы для каждого пользователя. 

Идентификатор и имя пакета для каждого поддерева пакетов со списком программ, которые запущены. Для каждого элемента отображаются следующие атрибуты: 
- Имя программы
- Состояние выполнения
- Время последнего запуска
- Код ошибки
- Причина сбоя  

Код ошибки и причина сбоя пусты, если программа была выполнена успешно.


### <a name="software-distribution-cache-information"></a><a name="bkmk_cache-info"></a> "Software Distribution Cache Information" (Информация о кэше распространения программного обеспечения)

#### <a name="cache-config"></a>Конфигурация кэша
Содержит сведения о кэше клиента Configuration Manager. Эти сведения включают в себя расположение кэша, размер кэша состояние его использования. 

#### <a name="cached-items"></a>Кэшированные элементы
Содержит поддерево всех элементов, находящихся сейчас в кэше. Каждый элемент дерева содержит следующие сведения о каждом элементе: 
- Расположение элемента (папка) в кэше
- Текущее состояние
- ИД пакета
- Имя пакета
- Версия пакета
- Размер пакета
- Текущее количество ссылок
- Время последнего обращения (UTC)  

#### <a name="downloading-items"></a>Скачивание элементов
Это элементы, которые клиент сейчас скачивает. Каждый из них показывает те же сведения, что и кэшированные элементы, а также количество скачанных килобайт. 


### <a name="software-distribution-pending-executions"></a><a name="bkmk_pending-exec"></a> "Software Distribution Pending Executions" (Ожидающие выполнения распространения программного обеспечения)

Эта вкладка содержит сведения о прошлых и будущих обязательных развертываниях, а также список доступных развертываний.

Каждая ветвь дерева предназначена для учетной записи пользователя с доступными развертываниями, включая системные.

Для каждого пользователя поддерево содержит следующие три элемента:  

#### <a name="mandatory-advertisements-with-future-executions"></a>Mandatory Advertisements With Future Executions (Обязательные объявления с будущими выполнениями)
Это обязательные объявления, по-прежнему содержащие программы для запуска. Это могут быть повторяющиеся, одноразовые или объявления с несколькими расписаниями. Для каждого из них отображается идентификатор объявления, время следующего запуска и расписание, по которому выполняется объявление. 

#### <a name="optional-advertisements"></a>"Optional Advertisements" (Необязательные объявления)
Отображает список всех публикуемых объявлений. Кроме того, отображает для каждого элемента такие сведения, как идентификатор объявления, имя программы и имя пакета. 

#### <a name="past-mandatory-advertisements-with-no-future-scheduled-executions"></a>Past Mandatory Advertisements With No Future Scheduled Executions (Прошлые обязательные объявления без будущих запланированных выполнений)
Это список существующих на клиенте объявлений, для которых не заданы выполняемые в будущем программы. Отображается идентификатор объявления, имя пакета и имя программы. Элемент поддерева отображается для любых объявлений, которые являются необязательными.

> [!Note]  
> Сведения об имени пакета доступны только для пакетов, с которыми сопоставлены объявленные политики на просматриваемом компьютере. Для пакетов, у которых больше нет доступных сопоставленных политик, отображается сообщение "Package Name No Longer Available" (Имя пакета больше не доступно).  



## <a name="inventory-tab"></a>Вкладка инвентаризации

Существует всего одна вкладка с информацией инвентаризации. Основное дерево содержит следующие элементы:  

- **Инвентаризация программного обеспечения**: содержит дату начала последнего цикла, дату последнего отчета, а также основной и дополнительный номера версии для последнего отчета.  

- **Сбор файлов**: содержит дату начала последнего цикла, дату последнего отчета, а также основной и дополнительный номера версии для последнего отчета.  

- **Инвентаризация оборудования**: содержит дату начала последнего цикла, дату последнего отчета, а также основной и дополнительный номера версии для последнего отчета.  

- **Сбор IDMIF**: содержит дату начала последнего цикла, дату последнего отчета, а также основной и дополнительный номера версии для последнего отчета.  

- **DDR**: содержит дату начала последнего цикла, дату последнего отчета, а также основной и дополнительный номера версии для последнего отчета. Информация о записях данных обнаружения также отображается в поддереве.



## <a name="software-metering-tab"></a>Вкладка "Отслеживание использования программного обеспечения"

Эта вкладка отображает информацию в виде поддерева и включает все правила контроля использования программных продуктов. Каждое правило отображается в виде узла, определяемого по имени файла идентификатору правила. Разверните каждый узел в дереве, чтобы просмотреть следующие сведения:
- Имя файла обозревателя 
- Исходное имя файла
- ИД правила
- Версия файла
- Язык


