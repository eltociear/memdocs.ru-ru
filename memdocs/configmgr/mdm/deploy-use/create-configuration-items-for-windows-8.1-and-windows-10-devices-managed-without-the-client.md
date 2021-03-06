---
title: Создание элементов конфигурации для Windows
titleSuffix: Configuration Manager
description: Создание элементов конфигурации для управления параметрами компьютеров Windows 10 с помощью локального управления мобильными устройствами (MDM) в Configuration Manager.
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 23e1e4dc-623a-4521-ad04-ae9482927097
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1987ba504630ab1d4b23cdb54710f0cbaa3db28a
ms.sourcegitcommit: 7f542c97ac55bbd329f5befda97d671213c24e9a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/08/2020
ms.locfileid: "84506262"
---
# <a name="create-configuration-items-for-windows-devices-with-on-premises-mdm-in-configuration-manager"></a>Создание элементов конфигурации для устройств Windows с помощью локальной системы MDM в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Используйте элемент конфигурации Configuration Manager **Windows 8.1 и Windows 10** для управления параметрами устройств Windows, которыми вы управляете с помощью локального управления мобильными устройствами (MDM).

Дополнительные общие сведения о параметрах соответствия в Configuration Manager см. в следующих статьях:

- [Приступая к работе с параметрами соответствия](../../compliance/get-started/get-started-with-compliance-settings.md)

- [Планирование и Настройка параметров соответствия](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)

## <a name="create-a-configuration-item"></a>Создание элемента конфигурации

1. В консоли Configuration Manager перейдите в рабочую область **активы и соответствие** , разверните узел **Параметры соответствия**и выберите узел **элементы конфигурации** .

1. На вкладке ленты **Главная** в группе **Создать** выберите **Создать элемент конфигурации**.

1. На странице **Общие** **мастера создания элементов конфигурации** укажите перечисленные ниже сведения.

    - **Имя**: уникальное имя, идентифицирующее этот элемент конфигурации.

    - **Описание**: необязательное описание для предоставления дополнительных сведений об использовании.

    - В разделе **параметры для устройств, управляемых *без* Configuration Manager клиента**, выберите **Windows 8.1 и Windows 10**.

    - **Категории**. Вы можете создавать и назначать категории для поиска и фильтрации элементов конфигурации в консоли Configuration Manager.

1. На странице **Поддерживаемые платформы** в мастере выберите конкретные платформы Windows для вычисления этого элемента конфигурации.

1. На странице **Параметры устройства** выберите группы параметров, которые требуется настроить. Дополнительные сведения о доступных параметрах см. в разделе [Справочник по параметрам](#bkmk_setref).

    > [!TIP]
    > Если нужный параметр отсутствует в списке, выберите параметр для **настройки дополнительных параметров, которые не входят в группы параметров по умолчанию**. Этот параметр добавляет страницу « **Дополнительные параметры** » в мастер.

1. На странице «Параметры» настройте необходимые параметры. Когда параметры поддерживают этот параметр, можно также **исправлять несоответствующие параметры**. Если устройство оценивает параметр как не соответствующий этому элементу конфигурации, он будет исправлять соответствующий параметр.

    Для каждой группы параметров можно также настроить серьезность, которую сообщает, если параметр не соответствует требованиям. Выберите одно из следующих значений для параметра **важность несоответствия для отчетов** :

    - **Нет** — устройства, которые не отвечают этому правилу соответствия, не передают сведения о серьезности сбоя для отчетов Configuration Manager.

    - **Сведения**

    - **!**

    - **Критически важно**

    - **Критический с событием** — устройства, которые не отвечают этому правилу соответствия, передают для отчетов Configuration Manager сведения о сбое с уровнем серьезности **Критический с событием**. Он также регистрирует несоответствующее состояние как событие Windows в журнале событий приложений.

1. На странице **применимость платформы** мастера проверьте все параметры, несовместимые с выбранными поддерживаемыми платформами. Вернитесь назад и удалите эти параметры, измените платформы поддержки или продолжайте.

    > [!IMPORTANT]
    > Устройства не оценивают соответствие неподдерживаемым параметрам.

1. Завершите работу мастера.

Созданный элемент конфигурации вы можете просмотреть в узле **Элементы конфигурации** рабочей области **Активы и соответствие** .

## <a name="settings-reference"></a><a name="bkmk_setref"></a>Справочник по параметрам  

В следующих разделах подробно описаны конкретные параметры, доступные в каждой группе. Настройте эти параметры на странице **Параметры устройства** **мастера создания элементов конфигурации** для устройств **Windows 8.1 и Windows 10** , управляемых *без* клиента Configuration Manager.

### <a name="password"></a>Пароль

Эти параметры предназначены только для устройств под Windows 10 и более поздних версий.

- **Требовать параметры пароля на устройствах**: требовать пароль на поддерживаемых устройствах.
- **Минимальная длина пароля (в символах)**: Минимальная длина пароля.
- **Срок действия пароля в днях**: количество дней, по истечении которого пользователь должен сменить пароль.
- **Число сохраненных паролей**: предотвращает повторное использование ранее использованных паролей.
- **Число неудачных попыток входа до очистки устройства**: если это число попыток входа не удалось, MDM очищает устройство
- **Время бездействия до блокировки устройства**: Укажите период времени, в течение которого устройство может быть бездействует, прежде чем оно будет заблокировано. Устройство бездействует, когда нет вводимых пользователем данных.
- **Сложность пароля**. Укажите, можно ли указать цифровой ПИН-код `1234` , например, или укажите, нужно ли указывать надежный пароль.
  - **Количество наборов сложных символов, необходимых в пароле**: если сложность пароля **надежна**, выберите, сколько типов символов требуется для пароля: прописные буквы, строчные буквы, цифры и символы. Значение по умолчанию — `2`.
- **Отправить ПИН-код восстановления пароля на сервер Exchange Server**

### <a name="device"></a>Устройство

- **Снимок экрана**: Включите этот параметр, чтобы разрешить пользователю воспринимать снимок экрана устройства. (только Windows 10)
- **Отправка диагностических данных**. Включите этот параметр, чтобы разрешить использование диагностических данных Windows для аналитики. (только Windows 8.1)
- **Разрешить отправку диагностических данных (Windows 10)**: Установите уровень диагностических данных Windows для аналитики: Disable, Basic, расширенная или полная. (только Windows 10)
- **Географическое расположение**: Включите этот параметр, чтобы разрешить устройству использовать сведения о службах обнаружения. (только Windows 10)
- **Копировать и вставить**: Включите этот параметр, чтобы использовать копирование и вставку для перемещения данных между приложениями. (только Windows 10)
- **Сброс до заводских**настроек: Включите этот параметр, чтобы разрешить пользователю сбрасывать параметры устройства к первоначальным параметрам. (только Windows 10)
- **Bluetooth**. разрешение или запрет на использование возможностей Bluetooth устройства.
- **Режим обнаружения Bluetooth**: разрешение или запрет на обнаружение устройства другими устройствами Bluetooth. (только Windows 10)
- **Реклама Bluetooth**: разрешение или запрет на использование рекламных объявлений Bluetooth. (только Windows 10)
- **Запись голоса**: разрешение или запрет на использование функций записи голоса устройства. (только Windows 10)
- **Кортана**: разрешение или запрет на использование голоса Assistant. (только Windows 10)
- **Уведомления центра**уведомлений: Включение или отключение панели уведомлений в Windows 10. (только Windows 10)
- **Изменение параметров региона (только для настольных систем)**: разрешить или запретить пользователю изменять региональные параметры на устройстве.
- **Изменение параметров питания и спящего режима (только для настольных систем)**. разрешает или запрещает пользователю изменять параметры питания и спящего режима на устройстве.
- **Изменение языковых параметров (только для настольных систем)**: разрешить или запретить пользователю изменять языковые параметры на устройстве.
- **Изменение системного времени**: разрешить или запретить пользователю изменять дату и время устройства.
- **Изменение имени устройства**: разрешение или запрет пользователю на изменение имени устройства.

### <a name="email-management"></a>Управление электронной почтой

Эти параметры используются для устройств под управлением Windows 8.1 и Windows 10.  

- **Электронная почта POP и IMAP**: разрешение или запрет подключений к учетным записям электронной почты, ИСПОЛЬЗУЮЩИМ стандарты POP и IMAP.
- **Максимальное время хранения электронной почты**: срок хранения электронной почты, по истечении которого сервер удаляет ее.
- **Допустимые форматы сообщений**: укажите, является ли электронная почта **обычным текстом** или **HTML и обычным текстом**.
- **Максимальный размер сообщения электронной почты в формате обычного текста (загружается автоматически)**: задает максимальный размер сообщений электронной почты при автоматической загрузке.
- **Максимальный размер сообщения электронной почты в формате HTML (загружается автоматически)**: задает максимальный размер HTML-сообщений при автоматической загрузке.
- **Максимальный размер вложения (загружается автоматически)**: задает максимальный размер автоматически загружаемых вложений электронной почты.
- **Синхронизация календаря**: разрешение или запрет на синхронизацию календарей на устройстве.
- **Настраиваемая учетная запись электронной почты**: разрешение или запрет использования неорганизации электронной почты на устройстве.
- **Сделать учетную запись Майкрософт необязательной в приложении "Почта Windows**". Включите этот параметр, чтобы не требовать учетная запись Майкрософт в почте Windows.

### <a name="store"></a>Магазин

Эти параметры предназначены только для устройств под Windows 10 и более поздних версий.

- **Магазин приложений**: разрешение или запрет доступа к Microsoft Store на устройстве.
- **Введите пароль для доступа к хранилищу приложений**: Включите этот параметр, чтобы требовать от пользователей ввести пароль для доступа к Microsoft Store приложению.
- **Покупки из приложений**: разрешить или запретить пользователям выполнять покупки в приложении.
- **Запуск приложения из магазина**. Отключите все приложения, которые были предварительно установлены на устройстве или установлены из Microsoft Store.
- **Автоматически обновлять приложения из хранилища**: разрешить или запретить автоматическое обновление приложений, установленных из Microsoft Store.
- **Установить приложения на системный диск**: разрешить или запретить устройству устанавливать приложения на системный диск, который обычно является `C:` диском.
- **Установить данные приложения на системный том**: Включите этот параметр, чтобы разрешить приложениям сохранять данные на системном диске.
- **Использовать только частный магазин**: требовать от пользователей скачивать приложения из частного хранилища.
- **DVR для игр**: отключение записи и вещания игр Windows

### <a name="browser"></a>Браузер

Эти параметры используются для устройств под управлением Windows 8.1 и Windows 10.

- **Разрешить веб-браузер**: разрешить или запретить использование веб-браузера на устройстве.
- **Автозаполнение**: разрешить или запретить изменение параметров автозаполнения в браузере.
- **Активные скрипты**: разрешить или запретить запуск скриптов, таких как скрипты ActiveX, в браузере.
- **Подключаемые**модули: разрешение или запрет на добавление подключаемых модулей в Internet Explorer.
- **Блокирование всплывающих окон**: разрешение или запрет на блокирование всплывающих окон в браузере.
- **Файлы cookie**: разрешить или запретить сохранение файлов cookie на устройстве.
- **Предупреждение о мошенничестве**: разрешение или запрет предупреждений о потенциально мошеннических веб-сайтах.

### <a name="internet-explorer"></a>Internet Explorer

Эти параметры используются для устройств под управлением Windows 8.1 и Windows 10.

- **Всегда отправлять заголовок "не записывать**": разрешить или запретить отправку сведений о просмотре сторонним сайтам.
- **Зона безопасности интрасети**: разрешение или запрет назначения уровня безопасности зоне безопасности интрасети.
- **Уровень безопасности зоны Интернета**: задайте уровень безопасности для зоны Интернета: высокий, средний, высокий или средний.
- **Уровень безопасности для зоны интрасети**: задайте уровень безопасности для зоны интрасети: высокая, средняя-высокая, средняя, средняя-низкая или низкая.
- **Уровень безопасности зоны надежных узлов**: задайте уровень безопасности для зоны надежных узлов: высокий, средний, средний, средний, низкий или низкий.
- **Уровень безопасности зоны ограниченных узлов**: задайте уровень безопасности для зоны ограниченных узлов: высокая.
- **Пространства имен для зоны интрасети**: Настройка веб-сайтов для добавления или удаления из зоны интрасети.
- **Переход на сайт интрасети при вводе одного слова**: разрешить или запретить Internet Explorer автоматически переходить на сайт интрасети, если пользователь введет допустимое имя сайта без предшествующего протокола, например `https://` .
- **Параметр меню режим предприятия**: разрешить пользователям активировать и деактивировать режим предприятия в меню **Сервис** Internet Explorer.
  - **Расположение отчетов в журнале (URL-адрес)**. Если активен режим предприятия, укажите URL-адрес для ведения журнала посещенных веб-сайтов.
- **Расположение списка сайтов в режиме предприятия (URL-адрес)**. Если активен режим предприятия, укажите список веб-сайтов, которые его используют.

### <a name="cloud"></a>Cloud

Эти параметры используются для устройств под управлением Windows 8.1 и Windows 10.

- **Синхронизация параметров**: разрешает или запрещает синхронизацию параметров между устройствами.
- **Синхронизация учетных данных**: разрешение или запрет на синхронизацию учетных данных между устройствами.
- **Учетная запись Майкрософт**. Включите этот параметр, чтобы разрешить использование учетная запись Майкрософт на устройстве.
- **Синхронизация параметров через Лимитные подключения**: разрешить или запретить синхронизацию параметров при лимитном сетевом подключении.

### <a name="security"></a>Безопасность

- **Установка неподписанного файла**: позволяет пользователям устанавливать неподписанный файл. (только Windows 10)
- **Неподписанные приложения**: разрешение или запрет на установку неподписанных приложений. (только Windows 10)
- **Обмен сообщениями SMS и MMS**: разрешение или запрещение протоколов текстовых сообщений на устройстве. (только Windows 10)
- **Съемные**носители: разрешение или запрет на использование съемных носителей, например SD-карт. (только Windows 10)
- **Камера**: разрешение или запрет на использование камеры устройства. (только Windows 10)
- **NFC**: разрешение или запрет связи с помощью NFC. (только Windows 10)
- **Режим защиты от кражи**: разрешить или запретить использование режима защиты от краж Windows 10. (только Windows 10)
- **Разрешить USB-подключение**: разрешить или запретить другим устройствам подключаться к этому устройству по USB-подключению. (только Windows 10)
- **Профиль VPN Windows RT**: подготовка профиля VPN для устройств Windows RT (только Windows 8.1)

### <a name="peak-synchronization"></a>Синхронизация в рабочее время

Эти параметры предназначены только для устройств под Windows 10 и более поздних версий.

- **Укажите пиковое время**: укажите пиковое время и дни недели для синхронизации мобильных устройств.
- **Периодичность синхронизации в рабочее время**: настройте частоту синхронизации в часы пиковой нагрузки.
- **Периодичность синхронизации в нерабочее время**: настройте частоту синхронизации за пределами пиковых часов.

### <a name="roaming"></a>Роуминг

- **Управление устройствами в роуминге**: разрешение или запрет Configuration Manager управления устройством при роуминге. (только Windows 10)
- **Загрузка программного обеспечения в роуминге**: разрешение или запрет загрузки приложений и программного обеспечения в роуминге. (только Windows 10)
- **Загрузка электронной почты в роуминге**: разрешить или запретить загрузку электронной почты в роуминге. (только Windows 10)
- **Перемещение данных**: разрешение или запрет роуминга между сетями при доступе к данным.
- **VPN через сотовую**сеть: разрешает или запрещает устройству использовать VPN-подключение при подключении к сети сотовой связи. (только Windows 10)
- **Роуминг VPN через сотовую**сеть: разрешает или запрещает устройству использовать VPN-подключение в роуминге в сети мобильной связи. (только Windows 10)

### <a name="encryption"></a>Шифрование

- **Шифрование карты памяти**: задайте значение ON, чтобы требовать от пользователя зашифровать все карты памяти, используемые на устройстве. (только Windows 10)
- **Шифрование файлов на устройстве**: задается для шифрования файлов, хранящихся на устройстве.
- **Требовать подписание электронной почты**. пользователь должен подписать электронные письма перед отправкой.
  - **Алгоритм подписи**: выберите алгоритм для подписи сообщений электронной почты: по умолчанию, SHA или MD5.
- **Требовать шифрование по электронной почте**: пользователь должен зашифровать сообщения электронной почты перед их отправкой.
  - **Алгоритм шифрования**: выберите алгоритм шифрования сообщений электронной почты: по умолчанию Triple DES, DES, RC2 128-bit, RC2 64-бит, RC2 40-bit

### <a name="wireless-communications"></a>Беспроводная связь

Эти параметры предназначены только для устройств под Windows 10 и более поздних версий.

- **Беспроводное сетевое подключение**: разрешение или запрет возможности Wi-Fi устройства.
- **Модем Wi-Fi**: позволяет пользователю использовать устройство в качестве мобильного хот-спота.
- По **возможности разгружать данные в Wi-Fi**: позволяет устройству использовать подключение Wi-Fi насколько это возможно.
- **Отчеты о хот-спотах Wi/Fi**. Включите для устройства отправку сведений о подключениях Wi-Fi, чтобы помочь пользователю обнаружить соседние подключения.
- **Настройка Wi-Fi вручную**: позволяет пользователю вручную настроить беспроводные подключения.

#### <a name="configured-wireless-network-connections"></a>Настроены беспроводные сетевые подключения

1. На странице **Настройка параметров беспроводной связи мобильных устройств** нажмите кнопку **Добавить**.

1. В окне **Беспроводное сетевое** подключение укажите следующие сведения о беспроводном подключении для предоставления на мобильных устройствах.

    - **Сетевое имя (SSID)**: введите имя сети Wi-Fi.
    - **Сетевое подключение**: выберите вариант " **Интернет** " или " **работа**".
    - **Проверка подлинности**: выберите метод проверки подлинности для беспроводного подключения:
        - **Открыть**
        - **Общий**
        - **ПОДДЕРЖКУ**
        - **WPA-PSK**
        - **WPA2**
        - **WPA2-PSK**
    - **Шифрование данных**: выберите метод шифрования, используемый этим соединением. Доступные значения изменяются в зависимости от выбранного метода **проверки подлинности** :
        - **Отключено**
        - **WEP**
        - **TKIP**
        - **AES**
    - **Индекс ключа**: Если для параметра **Шифрование данных** задано значение **WEP**, выберите индекс ключа от **1** до **4**.
    - **Эта сеть подключается к Интернету**: укажите параметры прокси-сервера, чтобы разрешить мобильным устройствам в беспроводной сети подключаться к Интернету.
        - **Параметры прокси-сервера**. Настройте параметры **сервера** и **порта** для прокси **-серверов HTTP**, **WAP**и **сокетов** .
    - **параметры 802.1 x**:
        - **Включить доступ к сети 802.1 x**: Обеспечьте безопасность соединения, УКАЗАВ тип EAP.
        - **Тип EAP**: выберите один из следующих протоколов проверки подлинности:
            - **PEAP**
            - **Смарт-карта или сертификат**

### <a name="certificates"></a>Сертификаты

Импорт сертификатов для установки на мобильных устройствах.

Выберите **Импорт**и укажите следующие значения:

- **Файл сертификата**: Найдите и выберите файл сертификата (**CER**) для импорта.
- **Целевое хранилище**: выберите одно или несколько из следующих хранилищ сертификатов:
  - **Корневой**
  - **Корнев**
  - **Normal**
  - **Привилегированное**
  - **SPC**
  - **Кэширующий узел**
- **Роль**. Если вы выбираете хранилище сертификатов **SPC** (сертификат издателя программного обеспечения), выберите роль, которая будет связана с сертификатом:
  - **Оператор мобильной связи**
  - **Manager**
  - **Пользователь, прошедший проверку подлинности**
  - **ИТ-администратор**
  - **Пользователь, не прошедший проверку подлинности**
  - **Доверенный сервер отслеживания использования**

### <a name="system-security"></a>Безопасность системы

- **Контроль учетных записей пользователей**. Настройте поведение контроля учетных записей Windows на устройстве.
- **Сетевой брандмауэр**: обязательное использование Windows для включения встроенного брандмауэра. (Windows 8.1)
- **Обновления**. Настройте поведение обновлений программного обеспечения Windows. (Windows 8.1)
  - **Минимальная Классификация обновлений**: Выберите минимальную классификацию обновлений для скачивания и установки: **нет**, **важно**или **рекомендуется**.
- **Обновления (Windows 10)**: Настройка поведения обновлений программного обеспечения Windows. (только Windows 10)
  - **День установки**: выберите запланированный день, когда устройство автоматически устанавливает обновления и перезагрузки. (только Windows 10)
  - **Время установки**: выберите запланированное время, когда устройство автоматически устанавливает обновления и перезагрузки. (только Windows 10)
- **SmartScreen**: Включение или отключение интеллектуального экрана Windows.
- **Защита от вирусов**. требуется, чтобы в Windows было антивирусное программное обеспечение.
- **Сигнатуры антивирусной защиты**обновлены: требуется актуальность файлов сигнатур антивирусных программ.
- **Представление уведомлений экрана блокировки**: Включение или отключение уведомлений для отображения на экране блокировки.
- **Функции предварительной версии**: укажите, принимает ли устройство параметры и функции предварительной версии. (только Windows 10)
- **Установка корневого сертификата вручную**. Включите или отключите установку корневого сертификата вручную, что позволяет доверять любому сертификату, выданному этим корнем. (только Windows 10)
- **Разрешить отмену регистрации вручную**: разрешить или запретить пользователю отменять регистрацию устройства в локальном управлении мобильными устройствами с помощью Configuration Manager.

### <a name="windows-server-work-folders"></a>Рабочие папки Windows Server

Эти параметры используются для устройств под управлением Windows 8.1 и Windows 10.

- **URL-адрес рабочих папок**: укажите расположение рабочей папки Windows Server, к которой пользователи могут подключаться с устройства.

### <a name="allowed-and-blocked-apps-list"></a>Список разрешенных и заблокированных приложений

Эти параметры предназначены только для устройств под управлением Windows Phone, которые Configuration Manager локальной системе MDM не поддерживаются. Дополнительные сведения см. в статье [Что случилось с гибридными средами?](../understand/what-happened-to-hybrid.md).

### <a name="windows-10-team"></a>Windows 10 для совместной работы

Эти параметры предназначены только для устройств под Windows 10 для совместной работы.

- **Разрешить автоматическое пробуждение экрана, если датчики обнаруживают кого-либо в комнате**. разрешение или запрет автоматического пробуждения устройства при обнаружении другого датчика в комнате.
- **Требовать ПИН-код для беспроводной проекции**: Включение или отключение ввода ПИН-кода перед беспроводным подключением другого устройства к проекции.
- **Период обслуживания**: Включите этот параметр, чтобы настроить окно, когда обновления могут устанавливать и перезапускать устройство.
  - **Время начала**: задайте время начала периода обслуживания.
  - **Длительность (в часах)**: Задайте длину периода обслуживания в часах.
- **Оперативная аналитика Azure**. разрешает [службе оперативной аналитики Azure](https://azure.microsoft.com/resources/videos/azure-operational-insights-overview/) выполнять накопление, хранение и анализ данных файлов журналов с устройств Windows 10 для совместной работы.
  - **Идентификатор рабочей области**: введите допустимый идентификатор рабочей области.
  - **Ключ рабочей области**: введите ключ для связанной рабочей области.
- **Беспроводная проекция Miracast**: разрешить проецирование устройств с поддержкой Miracast на это устройство Windows 10 для совместной рабочей группы.
  - **Канал Miracast**: выберите канал Miracast для содержимого проекта.
- **Сведения о собрании, отображаемые на экране приветствия**: выберите тип информации, отображаемой на плитке **собраний** экрана **приветствия** :
  - **Отображать только организатора и время**
  - **Отображение организатора, времени и темы (тема скрыта для частных собраний)**
- **URL-адрес фонового изображения**экранной заставки: укажите URL-адрес для отображения пользовательского фона на экране **приветствия** устройства Windows 10 для совместной работы. Начните использовать URL-адрес в `https://` формате PNG.

### <a name="windows-information-protection"></a>Windows Information Protection  

Дополнительные сведения о настройке защиты корпоративных данных с Configuration Manager см. в статье [Защита корпоративных данных с помощью Windows Information Protection (WIP)](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/protect-enterprise-data-using-wip).

### <a name="microsoft-edge-legacy"></a>Устаревший Microsoft ребро

Эти параметры предназначены только для устройств под Windows 10 и более поздних версий.  

- **Разрешить варианты поиска в адресной строке**: Позвольте поисковой подсистеме предлагать сайты при вводе фраз поиска.
- **Разрешить Do Not Track**: уведомлять веб-сайты о том, что вы не хотите, чтобы они пропускали посещение.
- **Включить SmartScreen**: Убедитесь, что Скачанные файлы не содержат вредоносного кода.
- **Разрешить всплывающие окна**: Настройка всплывающих окон браузера.
- **Разрешить файлы cookie**: Настройка использования файлов cookie.
- **Разрешить автозаполнение**: позволяет браузеру автоматически заполнять формы сохраненными сведениями, такими как имя, адрес и телефон.
- **Разрешить диспетчер паролей. разрешает**браузеру сохранять пароли для веб-сайтов и управлять ими.
- **Средства для разработчиков**. Разрешите или запрещайте использование средств разработчика пограничных функций.
- **Расширения**: разрешение или запрет расширений ребра.
- **Просмотр InPrivate**: разрешение или запрет на просмотр InPrivate, в котором не хранятся журналы и файлы cookie.
- **WebRTC LOCALHOST IP Address**: разрешает или запрещает отображение IP-адреса localhost устройства, когда пользователь выполняет телефонные звонки с помощью протокола Web RTC.
- **Блокировать доступ к: flags**: разрешить или запретить пользователю доступ к `about:flags` странице, содержащей параметры разработчика и экспериментальных настроек.
- **Переопределение запросов SmartScreen для файлов**: разрешить или запретить пользователю обходить предупреждения фильтра SmartScreen о загрузке потенциально вредоносных файлов.
- **Переопределение запроса SmartScreen**: разрешает или запрещает пользователю обходить предупреждения фильтра SmartScreen о потенциально вредоносных веб-сайтах.
- **URL-адрес первого запуска**: укажите веб-сайт, который будет отображаться, когда пользователь впервые открывает ребро.

### <a name="windows-defender-antivirus"></a>Антивирусная программа "Защитник Windows"

Эти параметры предназначены только для устройств под Windows 10 и более поздних версий.

- **Разрешить мониторинг в режиме реального времени**: включить сканирование в реальном времени для вредоносных программ, шпионских программ и других нежелательных программ.
- **Разрешить мониторинг поведения**: защитник проверяет наличие определенных известных шаблонов подозрительных действий на устройствах.
- **Включить система проверки сети**: система проверки сети (NIS) помогает защищать устройства от сетевых эксплойтов. Она использует сигнатуры известных уязвимостей из Microsoft Endpoint Protection Center, чтобы обнаружить и заблокировать вредоносный трафик.
- **Проверять все загрузки**: защитник сканирует все файлы, скачанные из Интернета.
- **Разрешить проверку сценариев**: защитник сканирует скрипты, используемые в Internet Explorer.
- **Мониторинг активности файлов и программ**: защитник отслеживает действия с файлами и программами на устройствах.
  - **Отслеживаемые файлы**: выберите тип файлов для отслеживания: "все", "входящий" или "исходящий".
- **Дни для трассировки разрешенных вредоносных программ**: защитник по мере необходимости следит за разрешенной вредоносной программой на указанное число дней. Затем можно вручную проверить ранее затронутые устройства. Если задать число дней равным 0, вредоносная программа останется в папке карантина и не будет автоматически удалена. Максимальное значение — 90.
- **Разрешить доступ к пользовательскому интерфейсу клиента**: определяет, следует ли скрывать пользовательский интерфейс защитника от пользователей. При изменении этого параметра он вступает в силу при следующем перезапуске устройства.
- **Запланировать проверку системы**: выберите полную или быструю проверку, которая выполняется регулярно в указанные день и время:
  - **Запланированный день**: выберите запланированный день запуска сканирования защитником.
  - **Запланированное время**: выберите запланированное время, когда защитник запускает проверку.
- **Запланировать ежедневную быструю проверку**: выберите запланированное время, когда защитник ежедневно запускает быструю проверку.
- **Ограничить загрузку ЦП во время проверки**: укажите процент процессора, который защитник может использовать при выполнении проверки. Введите значение от 1 до 100.
- **Проверять архивные файлы**: защитник сканирует сжатые архивы, такие как ZIP-или CAB-файлы.
- **Проверять сообщения электронной почты**: защитник сканирует сообщения по мере их поступления на устройство.
- **Проверять съемные диски**: защитник сканирует съемные диски, такие как USB-накопители.
- **Проверять подключенные диски**. защитник сканирует диски, сопоставленные с сетевыми общими папками. Например, `H:` сопоставляется с личным диском пользователя. Если файлы на диске доступны только для чтения, защитник не сможет удалить вредоносные программы, обнаруженные им.
- **Проверять файлы, открытые из общих сетевых папок**: защитник сканирует файлы, когда пользователь открывает их по общему сетевому пути. Например, `\\server\share\file.doc`. Если файл в общей папке доступен только для чтения, защитник не сможет удалить найденные вредоносные программы.
- **Интервал обновления сигнатур**: выберите интервал времени, в течение которого защитник проверяет наличие новых файлов сигнатур.
- **Разрешить защиту в облаке**. Защитник использует облако Майкрософт для получения сведений о действиях вредоносных программ и включает такие функции, как блок на первом уровне.
- **Предлагать пользователям отправлять образцы**. Выберите поведение для защитника, когда файлы могут потребовать дальнейшего анализа. Например, защитник может автоматически отправить файлы в корпорацию Майкрософт, чтобы определить, являются ли они вредоносными.
- **Обнаружение потенциально нежелательных приложений**. защищает устройство от работы программного обеспечения, которое классифицируется защитником как потенциально нежелательное. Можно защититься от работы этих приложений или использовать режим аудита для сообщения о том, что пользователь устанавливает потенциально нежелательное приложение.
- **Исключения файлов и папок**: добавьте один или несколько файлов и папок в список исключений. Например, `C:\Path` или `%ProgramFiles%\Path\filename.exe`. Защитник не включает эти файлы и папки во время проверок в режиме реального времени или по расписанию.
- **Исключения расширений файлов**: Добавьте одно или несколько расширений файлов в список исключений. Например, `java` или `exe`. Защитник не включает файлы с этими расширениями во время проверок в режиме реального времени или по расписанию.
- **Исключения процессов**: Добавьте определенные процессы в список исключений. Например, `C:\path\myproc.exe`. Этот тип исключения поддерживает только следующие расширения: `exe` , `com` или `scr` . Защитник не включает эти процессы во время проверок в режиме реального времени или по расписанию.

### <a name="additional-settings"></a>Дополнительные параметры

На странице **Параметры устройства** мастера, если выбран параметр для **настройки дополнительных параметров, которые не входят в группы параметров по умолчанию**, используйте эту страницу **Дополнительные параметры** для настройки этих параметров. Выберите **Добавить** , а затем выберите из списка доступных мобильных параметров. Выберите **выбрать** , чтобы изменить встроенные параметры, или **Создайте параметр** , чтобы создать настраиваемое значение реестра или тип параметра URI OMA.

## <a name="next-steps"></a>Дальнейшие действия

[Мониторинг параметров соответствия](../../compliance/deploy-use/monitor-compliance-settings.md)
