---
title: Данные о диагностике и использовании для версии 1902
titleSuffix: Configuration Manager
description: Сведения о конкретных данных, которые Configuration Manager собирает на каждом уровне в версии 1902.
ms.date: 05/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bce9e299-7b3a-4f51-8863-a322877daa2c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 77b4af9d6f5c84cc2c7aaa62d151f9c89b7f474a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703842"
---
# <a name="diagnostic-and-usage-data-for-version-1902"></a>Данные о диагностике и использовании для версии 1902

*Область применения: Configuration Manager (Current Branch)*

В следующих разделах приведены дополнительные сведения о том, какие данные собираются на каждом из уровней. Дополнительные сведения об уровнях и их изменении см. в разделе [Уровни диагностических данных об использовании](levels-overview.md).

Изменения по сравнению с предыдущими версиями отмечены как ***[Новое]***, ***[Обновлено]***, ***[Удалено]*** или ***[Перемещено]***.

> [!IMPORTANT]
> Configuration Manager не собирает коды или имена сайтов, IP-адреса, имена пользователей или компьютеров, физические адреса или адреса электронной почты на базовом и расширенном уровнях. Сбор таких сведений на полном уровне не является целенаправленным. Они могут входить в состав дополнительных диагностических данных, например в файлы журналов или моментальные снимки памяти. Корпорация Майкрософт не использует их для установления вашей личности, связи с вами или в рекламных целях.

## <a name="level-1---basic"></a><a name="bkmk_level1"></a> Уровень 1. Базовый

В Configuration Manager версии 1902 этот уровень включает такие данные:

- Статистка подключений консоли Configuration Manager: версия операционной системы, язык, SKU и архитектура, память системы, число логических процессоров, код сайта, установленные версии .NET и языковые пакеты консоли.

- Основные количественные показатели для приложений и типов развертывания: общее число приложений, общее число приложений с несколькими типами развертывания, общее число приложений с зависимостями, общее число заменяемых приложений, число используемых технологий развертывания.

- Основные сведения об иерархии сайтов Configuration Manager: список сайтов, тип, версия, состояние, число клиентов и часовой пояс.

- Базовая конфигурация базы данных: процессоры, объем памяти, параметры памяти, конфигурация базы данных Configuration Manager, размер базы данных Configuration Manager, конфигурация кластера, конфигурация распределенных представлений и версия для отслеживания изменений.  

- Основная статистика обнаружений: число обнаружений, минимальные, максимальные и средние размеры групп, в том числе при выполнении сайта полностью на службах Azure Active Directory.

- Основные сведения об Endpoint Protection: версии клиентов защиты от вредоносных программ.

- Число развертывания основных операционных систем.

- Основные сведения о сервере системы сайта: используемые роли системы сайта, состояние Интернета и SSL, операционная система, процессоры, физический компьютер или виртуальная машина, использование сервера сайта с высоким уровнем доступности.

- Схема базы данных Configuration Manager (хэш всех определений объектов)

- Настроенный уровень данных о диагностике и использовании, режим (в сети или автономно) и конфигурация быстрого обновления

- Число языков и языковых стандартов клиентов

- Число версий клиентов Configuration Manager, версий операционной системы и версий Office.

- Число операционных систем для управляемых устройств и политики, заданные соединителем Exchange

- Число устройств Windows 10 по каждой ветви, сборке и уникальному лесу Active Directory.  

- Число клиентов Windows 10, использующих Центр обновления Windows для бизнеса  

- Метрики производительности базы данных: информация об обработке репликации, хранимые процедуры SQL Server, использующие больше всего ресурсов процессора, использование диска.

- Сведения о типах и базовых конфигурациях точек распространения и точек управления: защита, предварительная подготовка, PXE, многоадресная рассылка, состояние SSL, точки распространения по запросу или одноранговые, поддержка управления мобильными устройствами и поддержка протокола SSL.

- Хэшированный список расширений для мастеров и страниц свойств в консоли администрирования.

- Сведения об установке:  

    - Сборка, тип установки, языковые пакеты, включенные функции   

    - Предварительное использование, тип установочного носителя, тип ветви.  

    - Дата истечения срока действия Software Assurance  

    - Изменение состояния развертывания пакета и ошибки, ход выполнения скачивания и ошибки предварительных требований 

    - Использование режима быстрого доступа к обновлениям  

    - Версия сценария после обновления  

- Версия SQL, уровень пакета обновления, выпуск, идентификатор параметров сортировки, кодировка  

- Статистика по данным о диагностике и использовании: когда запускались, среда выполнения, ошибки  

- Включено ли обнаружение сетевых ресурсов.  

- Число клиентов, присоединенных к службам Azure Active Directory  

- Число поэтапных развертываний, созданных по типу  

- Число клиентов расширенного взаимодействия  

- Хэшированный список свойств инвентаризации оборудования, длина которых превышает 255 символов  

- Число клиентов по методу регистрации совместного управления.  

- Статистика ошибок для регистрации совместного управления.  

- Число клиентов по времени существования ОС Windows до ближайшего трехмесячного интервала  

- 10 самых популярных названий процессоров, используемых в клиентах и на серверах.  

- Количество и скорость обработки ключевых объектов Configuration Manager: записи данных обнаружения (DDR), сообщения о состоянии, сообщения о статусе, инвентаризация оборудования, инвентаризация программного обеспечения и общее количество файлов в папках "Входящие"  

- Сведения о производительности процессора и диска сервера сайта  

- Сведения об использовании памяти и времени работы для процессов сервера сайта Configuration Manager  

- Число сбоев процессов сервера сайта Configuration Manager и ИД подписи "Доктор Ватсон" (если доступно)  

- Хэшированный список ведущих запросов SQL по использованию памяти и количеству блокировок.  

- Сводная статистика использования по совместному управлению: число зарегистрированных клиентов за все время, число зарегистрированных клиентов, число ожидающих регистрации клиентов, число получающих политику клиентов, сведения о состоянии рабочей нагрузки, размеры коллекции пилотного развертывания, исключения и ошибки регистрации.  

- ***[Новое]*** Сведения о наличии серверных расширений администрирования и мониторинга Microsoft BitLocker (MBAM).  

- ***[Новое]*** Число приложений с категориями и без для аналитики активов.



## <a name="level-2---enhanced"></a><a name="bkmk_level2"></a> Уровень 2. Расширенный

В Configuration Manager версии 1902 этот уровень включает такие данные:

### <a name="application-management"></a>Управление приложениями  

- Требования приложений: количество встроенных условий, на которые ссылается технология развертывания.  

- Замена приложений, максимальная глубина цепочки  

- Статистика по утверждению приложений и частота использования.  

- Статистика размеров для содержимого приложений.  

- Сведения о развертывании приложений: сравнение операций установки и удаления, потребность в утверждении, включение или отключение взаимодействия с пользователем, зависимость, замена, число применений функции поведения при установке.  

- Статистические данные о размере и сложности политики приложения  

- Статистика запросов доступных приложений  

- Основные данные о конфигурации пакетов и программ: варианты развертывания и флаги программы.  

- Основные сведения об использовании или нацеливании для типов развертывания: сравнение числа целевых пользователей и устройств, требуемого и доступного числа, универсальные приложения.  

- Число сред App-V и свойств развертывания  

- Число примененных приложений по операционной системе.  

- Число приложений, на которые ссылается последовательность задач.  

- Число неповторяющихся элементов фирменной символики для каталога приложений.  

- Число приложений Office 365, созданных с помощью панели мониторинга.  

- Число пакетов по типу  

- Число развертываний пакетов и программ.  

- Число лицензий для лицензированных приложений Windows 10  

- Число типов развертывания для установщика Windows в соответствии с настройками содержимого для удаления.  

- Число приложений Microsoft Store для бизнеса и статистика синхронизации: сводные типы приложений, состояние лицензированных приложений и число приложений, лицензированных через Интернет и в автономном режиме.  

- Тип и длительность периода обслуживания  

- Минимальное/максимальное/среднее число развертываний приложения на пользователя или устройство за период времени  

- Распространенные коды ошибок при установке приложений с разбивкой по технологиям развертывания.  

- Счетчики и параметры конфигурации MSI  

- Статистика по взаимодействию с конечным пользователем с уведомлением о требуемых развертываниях программного обеспечения.  

- Использование универсального подключения к данным (UDA), каким образом создано.  

- Сводная статистика сопоставления пользователей и устройств  

- Максимальное и среднее число основных пользователей на устройство  

- Использование глобального условия приложений по типу  

- Настройка центра программного обеспечения  

- Сведения о готовности диспетчера преобразования пакетов  

- Число методов обнаружения приложений по типу  

- Число ошибок принудительного применения приложения  

- Свойства установщика MSI  

- Статистика запросов пользователя на установку  

- Агрегированная статистика по использованию функции утверждения по электронной почте.  

- Число файлов, размер содержимого, количество служб и число настраиваемых действий для MSI-файлов в каталоге приложений.  

- ***[Новое]*** Число устройств, готовых к установке Office профессиональный плюс.


### <a name="client"></a>Клиент  

- Версия клиента технологии Active Management Technology (AMT)  

- Возраст BIOS в годах  

- Число устройств, для которых включена безопасная загрузка  

- Число устройств по состоянию доверенного платформенного модуля (TPM)  

- Автоматическое обновление клиентов: конфигурация развертывания, включая пилотное развертывание клиентов и использование исключений (клиент расширенного взаимодействия).  

- Конфигурация размера кэша клиента  

- Ошибки скачивания для развертывания клиента  

- ***[Обновлено]*** Сводка по основным проблемам и статистике работоспособности клиента по версиям клиента, компонентам, ОС и рабочим нагрузкам.  

- Состояние действий операции уведомления клиента: число выполнений каждого действия, максимальное число целевых клиентов, средняя частота успешного выполнения.  

- Число установок клиента из каждого типа расположения источника  

- Число сбоев при установке клиента  

- Число виртуализированных устройств в Hyper-V или Azure.  

- Число действий центра программного обеспечения  

- Число устройств с поддержкой UEFI.  

- Методы развертывания, используемые для клиента, и число клиентов на каждый метод развертывания  

- Список/число поддерживаемых агентов клиента  

- Возраст ОС в месяцах  

- Число классов инвентаризации оборудования, правил инвентаризации программного обеспечения и правил коллекций файлов.  

- Статистика по аттестации работоспособности устройств: распространенные коды ошибок, число локальных серверов и число устройств в каждом из состояний.  

- Число устройств по браузеру по умолчанию  

- Число сертификатов проверки подлинности сервера, созданных Configuration Manager  

- Число устройств Microsoft Surface по моделям  

- ***[Новое]*** Число ошибок проверки работоспособности клиента по типам проблем.


### <a name="cloud-services"></a>Облачные службы  

- Статистика обнаружения для Azure Active Directory.  

- Статистика настроек и использования для шлюза управления облачными клиентами: число областей и сред, статистика проверки подлинности и авторизации.  

- Число приложений и служб Azure Active Directory, подключенных к Configuration Manager.  

- Число коллекций, синхронизированных с Azure Log Analytics.  

- Число соединителей Upgrade Analytics.  

- Включен ли облачный соединитель Azure Log Analytics.  

- Число точек распространения по запросу с облачной точкой распространения в качестве источника  


### <a name="cmpivot"></a>CMPivot

- Статистика использования CMPivot  

- Количество сохраненных запросов CMPivot.  

- Количество запросов по типам сущности.  


### <a name="co-management"></a>Совместное управление  

- Расписание регистрации и статистика за прошлые периоды.  

- Число соответствующих клиентов для совместного управления.  

- Связанные клиенты Microsoft Intune  


### <a name="collections"></a>Коллекции  

- Использование идентификатора коллекции (не исчерпывает идентификаторы)  

- Статистика оценки изменений коллекции: время запроса, число назначенных и неназначенных, число по типу, смена идентификатора и использование правил.  

- Коллекции без развертывания  


### <a name="compliance-settings"></a>Параметры соответствия  

- Основные сведения о конфигурационных базах: число, количество развертываний и количество ссылок.  

- Статистика несоблюдения политик соответствия.  

- Число элементов конфигурации по типу  

- Число развертываний, ссылающихся на встроенные параметры, включая параметр исправления.  

- Число развертываний, ссылающихся на пользовательские параметры, включая параметр исправления.  

- Число развернутых шаблонов SCEP, VPN, Wi-Fi, сертификатов (PFX) и политики соответствия.  

- Число развертываний сертификатов SCEP, VPN, Wi-Fi, сертификатов (PFX) и политики соответствия по платформам  

- Политика Windows Hello для бизнеса (создана, развернута).  

- Число развернутых политик браузера Microsoft Edge  

- ***[Новое]*** Число политик OneDrive (созданных и развернутых).


### <a name="content"></a>Content  

- Статистика по группам границ: сколько быстрых, сколько медленных, количество на группу и резервные отношения  

- Сведения о группах границ: число границ и систем сайта, назначенных каждой группе границ.  

- Связи групп границ и конфигурация резервирования.  

- Статистика по скачиванию содержимого клиентом.  

- Число границ по типу  

- Число клиентов однорангового кэша, статистика использования и статистика частичных скачиваний.  

- Сведения о конфигурации диспетчера распространения: потоки, задержки при повторе, число повторных попыток и параметры точек распространения по запросу.  

- Сведения о конфигурации точек распространения: использование BranchCache, мониторинг точек распространения.  

- Сведения о группах точек распространения: число пакетов и точек распространения, назначенных каждой группе точек распространения.  

- Тип содержимого библиотеки: локальный или удаленный  

- Число границ групп по каждой конфигурации.  


### <a name="endpoint-protection"></a>Endpoint Protection  

- Политики Advanced Threat Protection (ATP) в Microsoft Defender (прежнее название — ATP в Защитнике Windows): число политик и статус их развертывания.

- Число предупреждений, настроенных для компонента Endpoint Protection  

- Число коллекций, выбранных для отображения на панели мониторинга Endpoint Protection  

- Число политик Exploit Guard в Защитнике Windows, развертываний и целевых клиентов.  

- Ошибки развертывания Endpoint Protection, количество кодов ошибок развертывания политик Endpoint Protection.  

- Использование политик брандмауэра Windows и защиты от вредоносных программ Endpoint Protection (число уникальных политик, назначенных группе). Эти данные не включают сведения о параметрах, включенных в политику.  


### <a name="migration"></a>Миграция  

- Число перенесенных объектов (использование мастера миграции)  


### <a name="mobile-device-management-mdm"></a>Управление мобильными устройствами (MDM)  

- Число выданных команд на выполнение действий с мобильными устройствами: блокировка, сброс ПИН-кода, очистка, снятие с учета и немедленная синхронизация.  

- Число политик для мобильных устройств  

- Число мобильных устройств под управлением Configuration Manager и Microsoft Intune и сведения о том, как они были зарегистрированы (массово, по отдельным пользователям).  

- Число пользователей с несколькими зарегистрированными мобильными устройствами  

- Расписание опроса мобильных устройств и статистика по длительности возврата мобильных устройств  


### <a name="microsoft-intune-troubleshooting"></a>Устранение неполадок Microsoft Intune  

- Число и размер сообщений о действиях с устройствами (очистка, снятие с учета, блокировка), данных об использовании и данных, реплицированных в Microsoft Intune  

- Число и размер сообщений о состоянии, инвентаризации, RDR, записях данных обнаружения, UDX, состоянии клиента, POL, LOG, сертификатах, CRP, повторной синхронизации, CFD, RDO, BEX, ISM и соответствии, загруженных из Microsoft Intune  

- Статистика полной и разностной синхронизации пользователей для Microsoft Intune  


### <a name="on-premises-mobile-device-management-mdm"></a>Локальное управление мобильными устройствами (MDM)  

- Число профилей и пакетов массовой регистрации Windows 10  

- Статистика успешных завершений и сбоев развертывания для локальных развертываний приложений MDM  


### <a name="os-deployment"></a>Развертывание операционной системы  

- Число образов загрузки, драйверов, пакетов драйверов, точек распространения с поддержкой многоадресной рассылки, точек распространения с поддержкой PXE и последовательностей задач  

- Число образов загрузки с разбивкой по версиям клиента Configuration Manager.  

- Число образов загрузки с разбивкой по версиям Windows PE.  

- Число политик обновления выпуска.  

- Число идентификаторов оборудования, исключенных их PXE.  

- Число развертываний операционной системы с разбивкой по версии ОС.  

- Число обновлений ОС за период.  

- Число развертываний последовательностей задач, использующих режим предварительного скачивания содержимого.  

- Данные об использовании шага последовательности задач  

- Установленная версия Windows ADK.  

- Количество задач обслуживания образов  

- Количество импортированных компьютеров.  


### <a name="site-updates"></a>Обновления сайта  

- Версии установленных исправлений Configuration Manager  


### <a name="software-updates"></a>Обновления программного обеспечения  

- Доступные и крайние изменения, используемые в правилах автоматического развертывания  

- Среднее и максимальное число назначений на обновление.  

- Оценки обновления клиента и расписания проверки  

- Классификации, синхронизированные точкой обновления программного обеспечения.  

- Статистика исправления кластера  

- Настройка экспресс-обновлений Windows 10.  

- Конфигурации, используемые для активных планов обслуживания Windows 10.  

- Число развернутых обновлений Office 365  

- Число синхронизированных драйверов Microsoft Surface.  

- Число групп обновления и назначений  

- Число пакетов обновлений, а также максимальное, минимальное и среднее число точек распространения, на которые ориентированы пакеты.  

- Число обновлений, созданных и развернутых с помощью System Center Update Publisher  

- Число созданных и развернутых политик Центра обновления Windows для бизнеса.  

- Сводная статистика по конфигурациям Центра обновления Windows для бизнеса  

- Число правил автоматического развертывания, связанных с синхронизацией  

- Число правил автоматического развертывания, создающих или добавляющих обновления в существующую группу.  

- Число правил автоматического развертывания с несколькими развертываниями.  

- Количество групп обновления и минимальное/максимальное/среднее число обновлений на группу  

- Число обновлений и процент обновлений, которые были развернуты, имеют истекший срок действия, заменены, скачаны и содержат лицензионные соглашения  

- Статистика балансировки нагрузки точки обновления программного обеспечения  

- Расписание синхронизации точки обновления программного обеспечения  

- Общее и среднее число коллекций, имеющих развертывания обновлений программного обеспечения, и максимальное и среднее число развернутых обновлений  

- Коды ошибок поиска обновлений и число компьютеров  

- Версии содержимого панелей мониторинга Windows 10  

- Число подписок на каталог обновлений программного обеспечения сторонних производителей и данные об использовании  

- Число обновлений программного обеспечения, развернутых с содержимым и без него  

- Статистические данные о числе обязательных, развернутых, устаревших, замененных и скачанных UUP-обновлений.  

- Сведения об использовании категорий продуктов UUP.  

- Число клиентов, которые развернули по крайней мере одно обновление качества или обновление компонентов UUP.  

- Основные коды ошибок UUP и число затронутых устройств.  


### <a name="sqlperformance-data"></a>Данные о производительности/SQL  

- Конфигурации и продолжительность формирования сводных данных сайта.  

- Число наибольших таблиц базы данных  

- Статистика работы обнаружения (число найденных объектов)  

- Типы обнаружения, включено ли и расписание (полное, добавочное).  

- Сведения о реплике SQL AlwaysOn, ее использовании и состоянии работоспособности.  

- Проблемы производительности отслеживания изменений в SQL, срок хранения и состояние автоматической очистки  

- Срок хранения данных для отслеживания изменений в SQL  

- Статистика состояний и статусов для сообщений о производительности, в том числе информация о самых распространенных и самых дорогих типах сообщений.  

- Статистика трафика (всего байт отправлено и получено конечной точкой) для точки управления.  

- Измерения счетчиков производительности в точке управления.  


### <a name="miscellaneous"></a>Прочее  

- ***[Обновлено]*** Конфигурация точки обслуживания для хранилища данных, включая расписание и среднюю продолжительность синхронизации, а также сведения об использовании функции настраиваемых таблиц.  

- ***[Обновлено]*** Число скриптов, а также статистика их выполнения и изменения.  

- Число сайтов с пробуждением по локальной сети (WOL).  

- Использование отчетов и статистика по производительности.  

- Статистика использования поэтапного развертывания  

- Число элементов аналитики управления и сведения о ходе выполнения  

- Число сбоев уникальных процессов, отличных от процессов Configuration Manager, на сервере сайта и ИД подписи "Доктор Ватсон" (если доступно)  

- ***[Новое]*** Агрегированная статистика по ошибкам регистрации и использованию Аналитики компьютеров.

- ***[Новое]*** Число некритических уведомлений консоли.

- ***[Новое]*** Агрегированная статистика по времени загрузки системы по ОС, форм-факторам и типам диска.



## <a name="level-3---full"></a><a name="bkmk_level3"></a> Уровень 3. Полный

В Configuration Manager версии 1902 этот уровень включает такие данные:

- Сведения о расписании оценки правил автоматического развертывания  

- Сводка по работоспособности ATP  

- Статистика оценки и обновления коллекций  

- Статистика по соблюдению и несоблюдению политик соответствия.  

- Параметры соответствия Сведения о конфигурации шаблона SCEP, VPN, Wi-Fi и политике соответствия требованиям.  

- Пакет конфигурации DCM для использования Configuration Manager  

- Подробные ошибки установки развертывания клиента  

- Сводка работоспособности Endpoint Protection: включая число защищенных, подверженных риску, неизвестных и не поддерживаемых клиентов.  

- Конфигурация политики Endpoint Protection  

- Список процессов, для которых настроен режим установки приложений.  

- Минимальное/максимальное/среднее число часов с момента последнего поиска обновлений программного обеспечения  

- Минимальное/максимальное/среднее число неактивных клиентов в коллекциях развертывания обновлений программного обеспечения  

- Минимальное/максимальное/среднее число обновлений программного обеспечения для каждого пакета  

- Статистика развертывания кода продукта MSI  

- Общее соответствие развертываний обновлений программного обеспечения  

- Число групп с просроченными обновлениями программного обеспечения  

- Коды и число ошибок развертывания обновлений программного обеспечения  

- Сведения о развертывании обновлений программного обеспечения: доля развертываний с назначенным клиентом и временем UTC; необходимые, необязательные и автоматические; подавление перезагрузки.  

- Продукты с обновлением программного обеспечения, синхронизированные точкой обновления программного обеспечения.  

- Процент успешных поисков обновлений программного обеспечения  

- 50 основных процессоров в среде  

- Тип политик условного доступа Exchange Active Sync (EAS) (блокировка или карантин) для устройств под управлением Microsoft Intune.  

- Сведения о приложениях Microsoft Store для бизнеса: неагрегированный список синхронизируемых приложений, включая AppID, состояние (в сети или автономное) и общее число приобретенных лицензий.  

- Число клиентов, которым отправляется параметр запрета отката к NTLM.  
