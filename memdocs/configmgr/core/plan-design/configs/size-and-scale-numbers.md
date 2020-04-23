---
title: Размер и масштаб
titleSuffix: Configuration Manager
description: Определите количество ролей системы сайта и сайтов, необходимое для поддержки устройств в вашей среде.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c5a42100-2f60-4952-b495-918025ea6559
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 0861bb73769beb6c7595b896afc8d0e156eef94d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688622"
---
# <a name="size-and-scale-numbers-for-configuration-manager"></a>Данные по размерам и масштабированию для Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Каждое развертывание Configuration Manager может поддерживать некоторое максимальное количество сайтов, ролей системы сайта и устройств. Это количество зависит от структуры вашей иерархии (сколько сайтов вы используете и какого типа) и от развертываемых ролей системы сайта. Сведения в этой статье помогут вам определить количество ролей системы сайта и сайтов, необходимое для поддержки устройств, которыми вы планируете управлять.

Дополнительные сведения см. в следующих статьях:

- [Рекомендуемое оборудование](recommended-hardware.md)
- [Поддерживаемые операционные системы для серверов системы сайта](supported-operating-systems-for-site-system-servers.md)  
- [Поддерживаемые операционные системы для клиентов и устройств](supported-operating-systems-for-clients-and-devices.md)
- [Предварительные требования к сайтам и системе сайта](site-and-site-system-prerequisites.md)

Эти значения определены на основе рекомендуемого оборудования для Configuration Manager. Они также основаны на параметрах по умолчанию для всех доступных функций Configuration Manager. Если вы используете нерекомендуемое оборудование или более агрессивные пользовательские параметры, это может привести к снижению производительности систем сайта. Системы сайта могут не удовлетворять заявленным уровням поддержки. Пример более агрессивных пользовательских параметров — это инвентаризация оборудования или программного обеспечения с частотой более одного раза в семь дней (значение по умолчанию).

## <a name="site-types"></a><a name="bkmk_SiteSystemScale"></a> Типы сайтов  

### <a name="central-administration-site"></a>Сайт центра администрирования  

- Сайт центра администрирования поддерживает до 25 подчиненных первичных сайтов.  

### <a name="primary-site"></a>Первичный сайт  

- Каждый первичный сайт поддерживать до 250 вторичных сайтов.  

- Число вторичных сайтов для каждого первичного сайта зависит от качества и надежности подключений к глобальной сети. В расположениях с менее 500 клиентами вместо вторичного сайта рекомендуется установить точку распространения.  

  Сведения о числе клиентов и устройств, которые может поддерживать первичный сайт, см. в разделе [Число клиентов для сайтов и иерархий](#bkmk_clientnumbers).  

### <a name="secondary-site"></a>Вторичный сайт  

- Вторичные сайты не поддерживают подчиненные сайты.  

## <a name="site-system-roles"></a><a name="bkmk_roles"></a> Site system roles

### <a name="application-catalog-web-service-point"></a>Точка веб-службы каталога приложений  

> [!Important]
> Пользовательский интерфейс Silverlight каталога приложений не поддерживается в текущей ветви версии 1806. Начиная с версии 1906, обновленные клиенты автоматически используют точку управления для развертываний приложений, доступных пользователю. Но вы не можете устанавливать новые роли каталога приложений. Поддержка ролей каталога приложений прекращена в версии 1910.  
>
> Дополнительные сведения см. в следующих статьях:
>
> - [Настройка центра программного обеспечения](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Удаленные и устаревшие компоненты](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

- На первичный сайтах можно установить несколько экземпляров точки веб-службы каталога приложений.  

### <a name="application-catalog-website-point"></a>Точка веб-сайта каталога приложений  

> [!Important]
> Пользовательский интерфейс Silverlight каталога приложений не поддерживается в текущей ветви версии 1806. Начиная с версии 1906, обновленные клиенты автоматически используют точку управления для развертываний приложений, доступных пользователю. Но вы не можете устанавливать новые роли каталога приложений. Поддержка ролей каталога приложений прекращена в версии 1910.  
>
> Дополнительные сведения см. в следующих статьях:
>
> - [Настройка центра программного обеспечения](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Удаленные и устаревшие компоненты](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

- На первичный сайтах можно установить несколько экземпляров точки веб-сайта каталога приложений.  

### <a name="cloud-management-gateway"></a><a name="bkmk_cmg"></a> Шлюз управления облачными клиентами

- Вы можете установить несколько экземпляров шлюза управления облачными клиентами на первичных сайтах или на сайте центра администрирования.  

    > [!Tip]  
    > В иерархии создайте шлюз управления облачными клиентами на сайте центра администрирования.  

  - Каждый шлюз управления облачными клиентами поддерживает от 1 до 16 экземпляров виртуальных машин в облачной службе Azure.  

  - Каждый экземпляр виртуальной машины шлюза управления облачными клиентами поддерживает 6000 одновременных подключений клиентов. Когда шлюз управления облачными клиентами работает в режиме высокой нагрузки из-за превышения количества поддерживаемых клиентов, он по-прежнему обрабатывает запросы, но с возможными задержками.  

Дополнительные сведения см. в разделе [Производительность и масштабируемость шлюза управления облачными клиентами](../../clients/manage/cmg/plan-cloud-management-gateway.md#performance-and-scale).

### <a name="cloud-management-gateway-connection-point"></a>Точка подключения шлюза управления облачными клиентами

- На первичных сайтах можно установить несколько экземпляров точек подключения шлюза управления облачными клиентами.  

- Одна точка подключения шлюза управления облачными клиентами поддерживает шлюз управления облачными клиентами, содержащий до четырех экземпляров виртуальных машин. Если шлюз управления облачными клиентами содержит более четырех экземпляров виртуальных машин, добавьте вторую точку подключения шлюза управления облачными клиентами для балансировки нагрузки. Шлюз управления облачными клиентами с 16 экземплярами виртуальных машин следует связать с четырьмя точками подключения шлюза управления облачными клиентами.

Дополнительные сведения см. в разделе [Производительность и масштабируемость шлюза управления облачными клиентами](../../clients/manage/cmg/plan-cloud-management-gateway.md#performance-and-scale).

> [!NOTE]
> При изучении требований к оборудованию для точки подключения CMG см. статью [Рекомендуемое оборудование для удаленных серверов системы сайта](recommended-hardware.md#bkmk_RemoteSiteSystem).<!-- SCCMDocs#2276 -->

### <a name="distribution-point"></a>Точка распространения  

- Число точек распространения на каждый сайт:  

  - Каждый первичный и вторичный сайт поддерживает не более 250 точек распространения.  

  - Каждый первичный и вторичный сайт поддерживает до 2000 дополнительных точек распространения, настроенных в качестве точек распространения по запросу. **Например**, один первичный сайт поддерживает 2250 точек распространения, причем 2000 из них настроены как точки распространения по запросу.  

  - Каждая точка распространения поддерживает подключения клиентов в количестве до 4000.  

  - Точка распространения по запросу действует как клиент, когда она осуществляет доступ к содержимому в исходной точке распространения.  

- Каждый первичный сайт поддерживает всего до 5 000 точек распространения. В это число входят все точки распространения на первичном сайте и все точки распространения, принадлежащие подчиненным вторичным сайтам первичного сайта.  

- Каждая точка распространения поддерживает всего до 10 000 пакетов и приложений.  

> [!WARNING]  
> Фактическое число клиентов, поддерживаемых одной точкой распространения, зависит от скорости сети и конфигурации оборудования сервера.  
>
> Количество точек распространения по запросу, поддерживаемых одной исходной точкой распространения, также зависит от скорости сети и конфигурации оборудования исходной точки распространения. Это число также зависит от объема развернутого содержимого. Этот эффект вызван тем, что, в отличие от клиентов, которые обычно обращаются к содержимому в разное время в ходе развертывания, все точки распространения по запросу обращаются к содержимому одновременно. Точки распространения по запросу могут запрашивать все доступное содержимое, а не только то содержимое, которое будет применяться к ним. Если исходная точка распространения имеет слишком высокую нагрузку, это может привести к непредсказуемым задержкам при распространении содержимого в целевые точки распространения.  

### <a name="fallback-status-point"></a>Резервная точка состояния  

- Каждая резервная точка состояния может поддерживать до 100 000 клиентов.  

### <a name="management-point"></a>Точка управления  

- Каждый первичный сайт поддерживает до 15 точек управления.  

    > [!TIP]  
    > Точки управления не следует устанавливать на серверах с медленным каналом связи с сервером первичного сайта или с сервером базы данных сайта.  

- Каждый вторичный сайт поддерживает одну точку управления, которая должна быть установлена на сервере вторичного сайта.  

Сведения о числе клиентов и устройств, которые может поддерживать точка управления, см. в разделе [Точки управления](#bkmk_mp).  

### <a name="software-update-point"></a>Точка обновления программного обеспечения  

Примите за основу следующие рекомендации. Они помогут определить, какие сведения подходят вашей организации для процесса планирования ресурсов, необходимых для поддержки обновления программного обеспечения. Фактические требования к ресурсам могут варьироваться в зависимости от рекомендаций в этой статье, а также зависеть от следующих критериев:

- конкретная сетевая среда;
- оборудование, используемое для размещения системы сайта точки обновления программного обеспечения;
- количество управляемых клиентов;
- другие роли системы сайта, установленные на сервере.  

#### <a name="capacity-planning-for-the-software-update-point"></a><a name="BKMK_SUMCapacity"></a> Планирование ресурсов для точки обновления программного обеспечения  

Количество поддерживаемых клиентов зависит от версии служб Windows Server Update Services (WSUS), запущенных на точке обновления программного обеспечения. Оно также зависит от того, сосуществует ли роль системы сайта точки обновления программного обеспечения с другой ролью системы сайта.  

- Точка обновления программного обеспечения может поддерживать до 25 000 клиентов, если на сервере точки обновления программного обеспечения запущены службы WSUS и эта точка сосуществует с другой ролью системы сайта.  

- Точка обновления программного обеспечения может поддерживать до 150 000 клиентов при условии, что удаленный сервер удовлетворяет требованиям WSUS, WSUS используется с Configuration Manager и вы произвели указанные ниже настройки.

  Пулы приложений IIS.

  - Увеличьте длину очереди WsusPool до 2000.
  - Увеличьте предельное значение выделенной памяти WsusPool в 4 раза или установите его на 0 (без ограничений). Например, если ограничение по умолчанию составляет 1 843 200 КБ, увеличьте его до 7 372 800. Дополнительные сведения см. в этой [публикации блога группы поддержки Configuration Manager](https://www.phoenixtekk.com/configmgr-2012-support-tip-wsus-sync-fails-with-http-503-errors/).  

    Подробные сведения о требованиях к оборудованию для точки обновления программного обеспечения см. в статье [Рекомендуемое оборудование для систем сайта](recommended-hardware.md#bkmk_ScaleSieSystems).  

#### <a name="capacity-planning-for-software-updates-objects"></a><a name="bkmk_sum-capacity-obj"></a> Планирование ресурсов для объектов обновлений программного обеспечения  

При планировании объектов обновлений программного обеспечения используйте следующую информацию о ресурсах.  

- **Ограничение в 1000 обновлений ПО в составе развертывания** — ограничение в 1000 обновлений для каждого развертывания обновления программного обеспечения. При создании правила автоматического развертывания (ADR) укажите условие, ограничивающее количество обновлений программного обеспечения. Правило автоматического развертывания завершается ошибкой, когда указанное условие возвращает более 1000 обновлений программного обеспечения. Проверьте состояние правила автоматического обновления в узле **Правила автоматического развертывания** в консоли Configuration Manager. При развертывании обновлений вручную выбирайте не более 1000 обновлений для развертывания.  

  Кроме того, ограничьте количество обновлений программного обеспечения в конфигурационной базе до 1000. Дополнительные сведения см. в разделе [Создание конфигурационных баз](../../../compliance/deploy-use/create-configuration-baselines.md).

- **Ограничение в 580 областей безопасности для правил автоматического развертывания** -<!--ado 4962928-->
Установите в правилах автоматического развертывания ограничение в 580 областей безопасности. Когда вы создаете правила автоматического развертывания, области безопасности, к которым у вас есть доступ, добавляются автоматически. Если используется более 580 областей безопасности, вам, возможно, не удастся применить правило автоматического развертывания, и в файл ruleengine.log будет записана ошибка.

### <a name="sms-provider"></a>Поставщик SMS

<!-- SCCMDocs#1958 -->

Каждый экземпляр поставщика SMS поддерживает одновременные подключения нескольких запросов. Для этих подключений ограничивается только число доступных серверных подключений в Windows и объем доступных ресурсов на сервере, использующихся для обслуживания запросов на подключение.

Дополнительные сведения см. в разделе [Планирование использования поставщика SMS](../hierarchy/plan-for-the-sms-provider.md).

## <a name="client-numbers-for-sites-and-hierarchies"></a><a name="bkmk_clientnumbers"></a> Число клиентов для сайтов и иерархий

Используйте следующие сведения, чтобы определить, сколько клиентов и какие типы клиентов могут поддерживаться на сайте или в иерархии.  

### <a name="hierarchy-with-a-central-administration-site"></a><a name="bkmk_cas"></a> Иерархия с сайтом центра администрирования

Общее число устройств, которое поддерживает сайт центра администрирования, включает в себя все устройства, входящие в состав следующих трех групп:  

- 700 000 рабочих столов Windows. См. также сведения для [встроенных устройств](#embedded).

- 25 000 устройств под управлением Mac и Windows CE 7.0.  

- 100 000 устройств, управляемых с помощью локального управления мобильными устройствами (MDM).

Например, в иерархии можно поддерживать 700 000 настольных компьютеров, до 25 000 устройств с Mac и Windows CE 7.0 и до 100 000 устройств, управляемых с помощью локального MDM. В общей сложности эта иерархия поддерживает до 825 000 устройств.

> [!IMPORTANT]  
> В иерархии, где сайт центра администрирования использует выпуск Standard сервера SQL Server, иерархия поддерживает не более 50 000 настольных компьютеров и устройств. Для поддержки более 50 000 настольных компьютеров и устройств необходимо использовать выпуск Enterprise для SQL Server. Это требование относится только к сайту центра администрирования. Оно не применяется к автономному первичному сайту и к дочернему первичному сайту. Выпуск SQL Server, используемый для первичного сайта, не должен ограничивать возможности сайта для поддержки указанного числа клиентов.

Выпуск SQL Server, используемый на автономном первичном сайте, не ограничивает емкость сайта и позволяет поддерживать указанное число клиентов.  

### <a name="child-primary-site"></a><a name="bkmk_chipri"></a> Дочерний первичный сайт

Каждый дочерний первичный сайт в иерархии с сайтом центра администрирования поддерживает следующее число клиентов:  

- В общей сумме 150 000 клиентов и устройств, не ограничиваясь определенной группой или типом, при условии, что не превышено число поддерживаемых устройств для иерархии. См. также поддержку [встроенных устройств](#embedded).

Например, первичный сайт поддерживает 25 000 устройств Mac и Windows CE 7.0. Это количество составляет ограничение для иерархии. Этот первичный сайт также поддерживает дополнительные 125 000 настольных компьютеров. Общее количество поддерживаемых устройств для дочернего первичного сайта равно максимальному количеству устройств, поддерживаемому дочерним первичным сайтом — 150 000.

### <a name="stand-alone-primary-site"></a><a name="bkmk_pri"></a> Автономный первичный сайт

Автономный первичный сайт поддерживает следующее число устройств:  

- В общей сумме 175 000 клиентов и устройств, при этом не более:  

  - 150 000 настольных компьютеров (компьютеры с ОС Windows, Linux и UNIX). См. также поддержку [встроенных устройств](#embedded).

  - 25 000 устройств под управлением Mac и Windows CE 7.0.

  - 50 000 устройств, управляемых с помощью локального управления мобильными устройствами;  

Например, автономный первичный сайт, который поддерживает 150 000 настольных компьютеров и 10 000 устройств с Mac, может поддерживать только 15 000 дополнительных мобильных устройств, управляемых с помощью локального управления мобильными устройствами.

### <a name="primary-sites-and-windows-embedded-devices"></a><a name="embedded"></a> Первичные сайты и устройства Windows Embedded

Первичные сайты поддерживают устройства Windows Embedded с активными файловыми фильтрами записи (FBWF). Если на встроенных устройствах не включены фильтры записи, первичный сайт может поддерживать то количество встроенных устройств, которое является допустимым для этого сайта. Если на встроенных устройствах включены файловые фильтры записи (FBWF) или объединенные фильтры записи (UWF), первичный сайт может поддерживать максимум 10 000 встроенных устройств с ОС Windows. Эти устройства должны быть настроены с учетом исключений, указанных в важном замечании в разделе [Планирование развертывания клиентов на устройствах Windows Embedded](../../clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md). Первичный сайт поддерживает только 3000 устройств Windows Embedded с активными расширенными фильтрами записи (EWF) и без настройки исключений.

### <a name="secondary-sites"></a><a name="bkmk_sec"></a> Вторичные сайты

Вторичные сайты поддерживают следующее число устройств:  

- 15 000 настольных компьютеров (компьютеры с ОС Windows, Linux и UNIX).  

### <a name="management-points"></a><a name="bkmk_mp"></a> Точки управления

Каждая точка управления может поддерживать следующее число устройств:  

- В общей сумме 25 000 клиентов и устройств, при этом не более:  

  - 25 000 настольных компьютеров (компьютеры с ОС Windows, Linux и UNIX).  

  - Один из следующих вариантов (не оба):  

    - 10 000 устройств, управляемых с помощью локального управления мобильными устройствами;  

    - 10 000 устройств с клиентами Mac и Windows CE 7.0.