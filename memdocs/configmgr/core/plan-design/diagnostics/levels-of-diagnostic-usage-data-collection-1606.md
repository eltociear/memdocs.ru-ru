---
title: Диагностические данные для версии 1606
titleSuffix: Configuration Manager
description: Сведения об уровнях данных диагностики и сведений об использовании, которые собирает Configuration Manager версии 1606.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f7350d03-f440-4744-82d4-75f8c6c25028
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: cd58fb2ad105d3fb94fcc1d2fe56f0ae64f766f1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697072"
---
# <a name="levels-of-diagnostic-usage-data-collection-for-version-1606-of-configuration-manager"></a>Уровни сбора данных диагностики и сведений об использовании для Configuration Manager версии 1606

*Область применения: Configuration Manager (Current Branch)*

Configuration Manager версии 1606 собирает данные о диагностике и использовании на трех уровнях: **Базовый**, **Расширенный** и **Полный**. По умолчанию для этого компонента задан расширенный уровень. В следующих разделах приведены дополнительные сведения о том, какие данные собираются на каждом из уровней.

Изменения по сравнению с предыдущими версиями отмечены как ***[Новое]***, ***[Обновлено]***, ***[Удалено]*** или ***[Перемещено]***.


> [!IMPORTANT]
>  Configuration Manager не собирает коды или имена сайтов, IP-адреса, имена пользователей или компьютеров, физические адреса или адреса электронной почты на базовом и расширенном уровнях. Любой сбор таких сведений на полном уровне не является преднамеренным (они могут входить в состав дополнительных диагностических данных, например файлов журнала или моментальных снимков памяти). Корпорация Майкрософт не будет использовать их для установления вашей личности, связи с вами или в рекламных целях.

##  <a name="how-to-change-the-level"></a><a name="bkmk_change"></a> Изменение уровня
 Администраторы, роль администрирования которых предусматривает разрешения на **изменение** для класса объектов **Сайт**, могут изменить уровень сбора в параметрах данных диагностики и сведений об использовании в консоли Configuration Manager.

   Для этого в консоли перейдите на вкладку Backstage (левая верхняя вкладка со стрелкой раскрывающегося списка), выберите пункт **Данные об использовании**, после чего выберите нужный уровень данных.  

##  <a name="level-1---basic"></a><a name="bkmk_level1"></a> Уровень 1. Базовый
 Базовый уровень включает данные по иерархии, данные, необходимые для улучшения процедур установки или обновления, а также данные, которые помогают определить, какие обновления Configuration Manager применимы к вашей иерархии.

 Начиная с Configuration Manager версии 1606, этот уровень включает следующее:


-   Сведения об установке:
      - Сборка, тип установки, языковые пакеты, включенные функции  

      -   Изменение состояния развертывания пакета и ошибки, ход выполнения скачивания и ошибки предварительных требований 

      -  Версия сценария после обновления

      -  Использование режима быстрого доступа к обновлениям

-   Метрики производительности базы данных (информация об обработке репликации, хранимые процедуры SQL Server, использующие больше всего ресурсов процессора, использование диска).

-   Основная конфигурация базы данных (процессоры, конфигурация кластера, конфигурация распределенных представлений)

-   Схема базы данных Configuration Manager (хэш всех определений объектов)

-   Число версий клиентов Configuration Manager и версий операционной системы

-   Число операционных систем для управляемых устройств и политики, заданные соединителем Exchange

-   Число языков и языковых стандартов клиентов

-   Число устройств Windows 10 по ветви и сборке

-   Основные сведения об иерархии сайтов Configuration Manager (список сайтов, тип, версия, состояние, число клиентов и часовой пояс)

-   Основные сведения о сервере системы сайта (используемые роли системы сайта, состояние Интернета и SSL, операционная система, процессоры, физический компьютер или виртуальная машина)

-   Основная статистика обнаружения пользователей (число обнаружений пользователей, минимальный, максимальный и средний размер группы)

-   Основные сведения об Endpoint Protection (версии клиентов защиты от вредоносных программ)

-   Основные количественные показатели для приложений и типов развертывания (общее число приложений, общее число приложений с несколькими типами развертывания, общее число приложений с зависимостями, общее число заменяемых приложений, число используемых технологий развертывания)

-   Основные количественные показатели для развертываний операционных систем (образов)

-   Сведения о типах и базовых конфигурациях точек распространения и точек управления (защита, предварительная подготовка, PXE, многоадресная рассылка, состояние SSL, точки распространения по запросу или одноранговые, поддержка управления мобильными устройствами, поддержка протокола SSL и т. д.)

-   Статистика телеметрии (время запуска, среда выполнения, ошибки)

-  Настроенный уровень телеметрии, режим (в сети или автономно) и конфигурация быстрого обновления

-  Использование обнаружения сетевых ресурсов (включено или выключено)
-  Консоль администрирования:

    -  Статистика подключений консоли (версия операционной системы, язык, SKU и архитектура, память системы, число логических процессоров, код сайта, установленные версии .NET и языковые пакеты консоли).    


- ***[Новое]*** версия SQL, уровень пакета обновления, выпуск, идентификатор параметров сортировки, кодировка.


##  <a name="level-2---enhanced"></a><a name="bkmk_level2"></a> Уровень 2. Расширенный
Расширенный уровень используется по умолчанию после завершения установки. Этот уровень включает в себя данные, собираемые на базовом уровне, а также сведения о конкретных функциях (частота и длительность использования), параметры клиента Configuration Manager (имя компонента, состояние и отдельные параметры, например интервалы опроса) и общие сведения об обновлениях программного обеспечения.

Этот уровень является рекомендуемым, так как предоставляет корпорации Майкрософт необходимый минимум сведений для внесения полезных изменений в последующие версии продуктов и служб. На этом уровне не осуществляется сбор имен объектов (сайты, пользователи, компьютеры или объекты), сведений об объектах, связанных с безопасностью, или уязвимостях, например количестве систем, требующих обновления программного обеспечения.

Начиная с Configuration Manager версии 1606, этот уровень включает следующее:

-   **Управление приложениями**  

    -    Основные сведения об использовании или нацеливании для типов развертывания, применяемых в организации (сравнение пользователей и целевых устройств, требуемого и доступного числа, универсальные приложения)  

    -   Сведения о развертывании приложений (установка и удаление, потребность в утверждении, включение или отключение взаимодействия с пользователем, зависимость, замена)  

    -   Статистика запросов доступных приложений  

    -   Число пакетов по типу  

    -   Количество примененных приложений по операционной системе  

    -   Число развертываний пакетов и программ  

    -   Число сред App-V и свойств развертывания  

    -   Число лицензий для лицензированных приложений Windows 10  

    -   Минимальное/максимальное/среднее число развертываний приложения на пользователя или устройство за период времени

    -   Тип и длительность периода обслуживания  

    -  Статистические данные о размере и сложности политики приложения

    - ***[Новое]*** Число приложений Магазина Windows для бизнеса и статистика синхронизации (включая обобщенные типы приложений).  

    - ***[Новое]*** статистика по группам границ (сколько быстрых, сколько медленных, количество на группу).

    - ***[Новое]*** Счетчики и параметры конфигурации MSI.

    - ***[Новое]*** требования приложений (количество встроенных условий, на которые ссылается технология развертывания).

    - ***[Новое]*** Замена приложений, максимальная глубина цепочки.

    - ***[новое]*** использование UDA, каким образом создано;



-   **Клиент:**  

    -   Список/число поддерживаемых агентов клиента  

    -   Число установок клиента из каждого типа расположения источника  

    -   Число сбоев при установке клиента  

    -  ***[новое]*** конфигурация развертывания автоматического обновления клиента, включая пилотное развертывание клиента;

    -  ***[Новое]*** Сводка основных проблем и статистика работоспособности клиента.

    - ***[Новое]*** Возраст BIOS в годах.

    - ***[новое]*** возраст операционной системы в месяцах;

    - ***[Новое]*** Число действий Центра программного обеспечения.

    - ***[Новое]*** Версия клиента технологии Active Management Technology (AMT).

    - ***[Новое]*** Ошибки загрузки для развертывания клиента.

    - ***[Новое]*** Состояние действий операции уведомления клиента (число выполнений каждого действия, максимальное число целевых клиентов, средняя частота успешного выполнения).

    - ***[Новое]*** Методы развертывания, используемые для клиента, и число клиентов на каждый метод развертывания.

    - ***[Новое]*** Конфигурация размера кэша клиента.



- ***[Новое]*** **Облачные службы:**

  - ***[Новое]*** Число коллекций, синхронизированных с Operations Management Suite.

  - ***[Новое]*** включен ли облачный соединитель Operations Management Suite.



- ***[Новое] Коллекции***

    -  ***[Перемещено]*** Статистика оценки изменений коллекции (время запроса, число назначенных и неназначенных, число по типу, смена идентификатора и использование правил).

    - ***[Новое]*** Коллекции без развертывания.

    - ***[Новое]*** Использование идентификатора коллекции (не исчерпывает идентификаторы).



-   **Параметры соответствия**  

    -   Число элементов конфигурации по типу  

    -   Основные сведения о конфигурационных базах (число, количество развертываний и количество ссылок)  

    -   ***[Изменено]*** Число развертываний, ссылающихся на встроенные параметры (теперь записывается параметр исправления).  

    -   ***[Изменено]*** Число развертываний, ссылающихся на пользовательские параметры (теперь записывается параметр исправления).  
    -   Число развернутых шаблонов SCEP, VPN, Wi-Fi, сертификатов (PFX) и политики соответствия

    -  Число развертываний сертификатов SCEP, VPN, Wi-Fi, сертификатов (PFX) и политики соответствия по платформам.

    - ***[Новое]*** Политика Passport for Work (создана, развернута).



-   **Содержимое**  

    -   Число границ по типу  

    -   Сведения о группах границ (число границ и систем сайта, назначенных каждой группе границ)  

    -   Сведения о группах точек распространения (число пакетов и точек распространения, назначенных каждой группе точек распространения).  

    -   Сведения о конфигурации точек распространения (использование BranchCache, мониторинг точек распространения)  

    -   Сведения о конфигурации диспетчера распространения (потоки, задержки при повторе, число повторных попыток и параметры точек распространения по запросу)  


-   **Endpoint Protection**  

    -   Использование политик брандмауэра Windows и защиты от вредоносных программ Endpoint Protection (число уникальных политик, назначенных группе)<br /><br /> Сюда не входят сведения о параметрах, включенных в политику.  

    -   Ошибки развертывания Endpoint Protection (количество кодов ошибок развертывания политик Endpoint Protection)  

    -   Число коллекций, выбранных для отображения на панели мониторинга Endpoint Protection.  

    -   Число предупреждений, настроенных для компонента Endpoint Protection.  

    - ***[Новое]*** Политики Advanced Threat Protection (ATP) (число политик, развернуты ли политики).


-   ***[Удалено]*** **Управление мобильными приложениями (MAM):**  

    -   ***[Удалено]*** Количество приложений Office, бизнес-приложений и политик с поддержкой MAM по операционным системам  

    -   ***[Удалено]*** Число развертываний приложений/политик MAM.  

    -   ***[Удалено]*** Число правил, созданных для каждого параметра MAM.  


- ***[Новое]*** **Миграция:**

  -  ***[Новое]*** Число перенесенных объектов (использование мастера миграции).



-   **Управление мобильными устройствами (MDM)**  

    -   Число выданных команд на выполнение действий с мобильными устройствами (блокировка, сброс ПИН-кода, очистка и снятие с учета).  

    -   Число мобильных устройств под управлением Configuration Manager и Microsoft Intune и сведения о том, как они были зарегистрированы (массово или для отдельных пользователей).  

    -   Расписание опроса мобильных устройств и статистика по длительности возврата мобильных устройств  

    -   Число политик для мобильных устройств  

    -   Число пользователей с несколькими зарегистрированными мобильными устройствами  

-   **Устранение неполадок Microsoft Intune:**

    -   Число и размер сообщений о состоянии, инвентаризации, RDR, записях данных обнаружения, UDX, состоянии клиента, POL, LOG, сертификатах, CRP, повторной синхронизации, CFD, RDO, BEX, ISM и соответствии, загруженных из Microsoft Intune

    -   Число и размер сообщений о действиях с устройствами (очистка, снятие с учета, блокировка), телеметрии и данных, реплицированных в Microsoft Intune

    -   Статистика полной и разностной синхронизации пользователей для Microsoft Intune


-   **Локальное управление мобильными устройствами (MDM)**  

    -   Статистика успешных завершений и сбоев развертывания для локальных развертываний приложений MDM  

    -   Число профилей и пакетов массовой регистрации Windows 10  



-   **Развертывание операционной системы**  

    -   Число образов загрузки, драйверов, пакетов драйверов, точек распространения с поддержкой многоадресной рассылки, точек распространения с поддержкой PXE и последовательностей задач  

    -   ***[Новое]*** Данные об использовании шага последовательности задач.



-   **Обновления сайта:**

    - Версии установленных исправлений Configuration Manager




-   **Обновления программного обеспечения:**  

    -   Общее и среднее число коллекций, имеющих развертывания обновлений программного обеспечения, и максимальное и среднее число развернутых обновлений  

    -   Число правил автоматического развертывания, связанных с синхронизацией  

    -   Число правил автоматического развертывания, создающих или добавляющих обновления в существующую группу  

    -   Доступные и крайние изменения, используемые в правилах автоматического развертывания  

    -   Среднее и максимальное число назначений на обновление  

    -   Число обновлений, созданных и развернутых с помощью System Center Update Publisher  

    -   Число групп обновления и назначений  

    -   Число пакетов обновлений, а также максимальное, минимальное и среднее число точек распространения, на которые ориентированы пакеты  

    -   Количество групп обновления и минимальное/максимальное/среднее число обновлений на группу  

    -   Число обновлений и процент обновлений, которые были развернуты, имеют истекший срок действия, заменены, скачаны и содержат лицензионные соглашения  

    -   Коды ошибок поиска обновлений и число компьютеров  

    -   Оценки обновления клиента и расписания проверки  

    -   Расписание синхронизации точки обновления программного обеспечения  

    -   Число правил автоматического развертывания с несколькими развертываниями  

    -   Конфигурации, используемые для активных планов обслуживания Windows 10  

    -   Версии содержимого панелей мониторинга Windows 10  

    -   Число клиентов Windows 10, использующих Центр обновления Windows для бизнеса  

    -   Статистика исправления кластера  

    -   Число развернутых обновлений Office 365  

    -   Классификации, синхронизированные точкой обновления программного обеспечения.

    -   ***[Новое]*** Статистика балансировки нагрузки точки обновления программного обеспечения.



-   **Данные о производительности/SQL**  

    -   Число наибольших таблиц базы данных  

    -   Сведения о реплике SQL Always-On.  

    -  Срок хранения данных для отслеживания изменений в SQL

    - ***[Новое]*** Типы обнаружения, включено ли и расписание (полное, добавочное).

    - ***[Новое]*** Статистика работы обнаружения (число найденных объектов).

    - ***[Новое]*** Проблемы производительности отслеживания изменений в SQL, срок хранения и состояние автоматической очистки.



- ***[Новое]*** **Прочее**

    - ***[Новое]*** Число сайтов с пробуждением по локальной сети (WOL).



##  <a name="level-3---full"></a><a name="bkmk_level3"></a> Уровень 3. Полный
Полный уровень включает все данные базового и расширенного уровней. Помимо этого, к нему относятся дополнительные сведения об Endpoint Protection, процентах соответствия обновлений и сведения об обновлениях программного обеспечения. Кроме того, этот уровень может содержать дополнительные диагностические сведения, такие как системные файлы и моментальные снимки памяти, которые могут содержать личные сведения, присутствующие в памяти или файлах журнала во время записи.

Начиная с Configuration Manager версии 1606, этот уровень включает следующее:

-   Статистика оценки и обновления коллекций

-   Сводка работоспособности Endpoint Protection (включая число защищенных, подверженных риску, неизвестных и не поддерживаемых клиентов)

-   Конфигурация политики Endpoint Protection

-   Сведения о развертывании обновлений программного обеспечения (процент развертываний с назначенным клиентом и временем UTC; необходимые, необязательные и автоматические; подавление перезагрузки).

-   Общее соответствие развертываний обновлений программного обеспечения

-   Сведения о расписании оценки правил автоматического развертывания

-   ***[УДАЛЕНО]*** Число клиентов с политиками защиты доступа к сети.

-   Коды и число ошибок развертывания обновлений программного обеспечения

-   Минимальное/максимальное/среднее число неактивных клиентов в коллекциях развертывания обновлений программного обеспечения

-   Число групп с просроченными обновлениями программного обеспечения

-   Минимальное/максимальное/среднее число обновлений программного обеспечения для каждого пакета

-   Процент успешных поисков обновлений программного обеспечения

-   Минимальное/максимальное/среднее число часов с момента последнего поиска обновлений программного обеспечения

-    Продукты с обновлением программного обеспечения, синхронизированные точкой обновления программного обеспечения
-    Параметры соответствия: сведения о конфигурации шаблона SCEP, VPN, Wi-Fi и политике соответствия требованиям.

-    Тип политик условного доступа EAS (блокировка или карантин) для устройств под управлением Intune

-   ***[Новое]*** 50 основных процессоров в среде.

-   ***[Новое]*** Пакет конфигурации DCM для использования Configuration Manager

-   ***[Новое]*** Код продукта MSI (типичные приложения, развертываемые клиентами).

-   ***[Новое]*** Сводка по работоспособности ATP.

-   ***[Новое]*** Подробные ошибки установки развертывания клиента.
