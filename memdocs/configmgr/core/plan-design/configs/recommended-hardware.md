---
title: Рекомендуемое оборудование
titleSuffix: Configuration Manager
description: Ознакомьтесь с рекомендациями в отношении оборудования, которые помогут вам в масштабировании базового развертывания Configuration Manager.
ms.date: 05/23/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5267f0af-34d3-47a0-9ab8-986c41276e6c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d741e34325da859d4fe1f0af554544ce146a42f9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702122"
---
# <a name="recommended-hardware-for-configuration-manager"></a>Рекомендуемое оборудование для Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Руководствуйтесь приведенными ниже рекомендациями при масштабировании среды Configuration Manager, чтобы обеспечить поддержку расширенных возможностей развертывания сайтов, систем сайта и клиентов. Они не предполагают описание всех возможных вариантов конфигурации сайтов и иерархий.  

Примените сведения из следующих разделов в качестве вспомогательных рекомендаций при выборе оборудования, соответствующего рабочим нагрузкам при использовании клиентами и сайтами доступных возможностей Configuration Manager с конфигурациями по умолчанию.  



##  <a name="site-systems"></a><a name="bkmk_ScaleSieSystems"></a> Системы сайта  
В этом разделе приводятся рекомендуемые конфигурации оборудования для систем сайта Configuration Manager для развертываний, которые поддерживают максимальное количество клиентов и используют большую часть функций или все функции Configuration Manager. Для развертываний, которые поддерживают меньшее количество клиентов и используют не все доступные функции, может требоваться меньший объем ресурсов компьютера. В общем случае, ключевыми факторами, ограничивающими производительность системы, являются (по порядку):  

1.  Скорость чтения и записи диска  

2.  Объем доступной памяти  

3.  ЦП  

Для достижения оптимальной производительности используйте конфигурации RAID 10 для всех дисков с данными и сеть Ethernet 1 Гбит/с.  

###  <a name="site-servers"></a><a name="bkmk_ScaleSiteServer"></a> Серверы сайта  

|Конфигурация сайта|ЦП (ядра)|Память (ГБ)|% выделения памяти для SQL Server|  
|-------------------------------|---------------|---------------|----------------------------------------|  
|Автономный сервер первичного сайта с ролью базы данных сайта на том же сервере <sup>1</sup>|16|96|80|  
|Автономный первичный сервер сайта с удаленной базой данных сайта|8|16|-|  
|Удаленный сервер базы данных для автономного первичного сайта|16|72|90|  
|Сервер сайта центра администрирования с ролью базы данных сайта на том же сервере <sup>1</sup>|20|128|80|  
|Сервер сайта центра администрирования с удаленной базой данных сайта|8|16|-|  
|Удаленный сервер базы данных для сайта центра администрирования|16|96|90|  
|Подчиненный первичный сайт с ролью базы данных сайта на том же сервере|16|96|80|  
|Сервер дочернего первичного сайта с базой данных удаленного сайта|8|16|-|  
|Удаленный сервер базы данных для дочернего первичного сайта|16|72|90|  
|Сервер вторичного сайта|8|16|-|  

<sup>1</sup> При установке сервера сайта и SQL Server на одном компьютере развертывание поддерживает максимальные [значения размера и масштабирования](size-and-scale-numbers.md) для сайтов и клиентов. Но эта конфигурация может ограничить [возможности обеспечения высокой доступности для Configuration Manager](../../servers/deploy/configure/high-availability-options.md), например использование кластера SQL Server. Кроме того, в связи с более высокими требованиями к подсистеме ввода-вывода, необходимой для поддержки работающих на одном компьютере SQL Server и сервера сайта Configuration Manager, рекомендуется использовать конфигурацию с удаленным компьютером SQL Server, если у вас более крупное развертывание.  

###  <a name="remote-site-system-servers"></a><a name="bkmk_RemoteSiteSystem"></a> Удаленные серверы системы сайта  
Эти указания предназначены для компьютеров с одной ролью системы сайта. При установке нескольких ролей системы сайта на одном компьютере внесите в план необходимые коррективы.  

|Роль системы сайта|ЦП (ядра)|Память (ГБ)|Пространство на диске (ГБ)|  
|----------------------|---------------|---------------|--------------------|  
|Точка управления|4|8|50|  
|Точка распространения|2|8|Согласно требованиям операционной системы и для хранения развертываемого содержимого|  
|Точка обновления программного обеспечения<sup>1</sup>|8|16|Согласно требованиям операционной системы и для хранения развертываемых обновлений|  
|Все остальные роли системы сайта|4|8|50|  

<sup>1</sup> На компьютере, где размещается точка обновления программного обеспечения, требуются следующие конфигурации для пулов приложений IIS:  

- Увеличение **длины очереди WsusPool** до **2000**.  

- Увеличение **предельного значения выделенной памяти WsusPool** в 4 раза или установка его в **0** (без ограничений).  

###  <a name="disk-space-for-site-systems"></a><a name="bkmk_DiskSpace"></a> Пространство на диске для систем сайта  
Распределение и конфигурация дискового пространства влияют на производительность Configuration Manager. Каждая среда Configuration Manager имеет индивидуальные характеристики, поэтому реальные цифры могут отличаться от приводимых здесь значений.  

Для достижения наивысшей производительности располагайте каждый объект в отдельном выделенном томе RAID. Наибольшее быстродействие томов с данными (Configuration Manager и файлы базы данных) обеспечивается при использовании массивов RAID 10.  

|Использование данных|Минимальное место на диске|25 000 клиентов|50 000 клиентов|100 000 клиентов|150 000 клиентов|700 000 клиентов (сайт центра администрирования)|  
|----------------|------------------------|--------------------|--------------------|---------------------|---------------------|-----------------------------------------------------|  
|Операционная система|См. руководство по операционной системе.|См. руководство по операционной системе.|См. руководство по операционной системе.|См. руководство по операционной системе.|См. руководство по операционной системе.|См. руководство по операционной системе.|  
|Приложение и файлы журналов Configuration Manager|25 ГБ|50 Гб|100 ГБ|200 Мб|300 ГБ|200 Мб|  
|Файл MDF базы данных сайта|75 ГБ на каждые 25 000 клиентов|75 ГБ|150 ГБ|300 ГБ|500 ГБ|2 ТБ|  
|Файл LDF базы данных сайта|25 ГБ на каждые 25 000 клиентов|25 ГБ|50 Гб|100 ГБ|150 ГБ|100 ГБ|  
|Файлы временной базы данных (MDF и LDF)|По мере необходимости|По мере необходимости|По мере необходимости|По мере необходимости|По мере необходимости|По мере необходимости|  
|Содержимое (общие папки точек распространения)|По мере необходимости<sup>1</sup>|По мере необходимости<sup>1</sup>|По мере необходимости<sup>1</sup>|По мере необходимости<sup>1</sup>|По мере необходимости<sup>1</sup>|По мере необходимости<sup>1</sup>|  

<sup>1</sup> Рекомендуемый объем дискового пространства не включает место на диске, необходимое для содержимого, расположенного в библиотеке содержимого на сервере сайта или в точках распространения. Сведения о планировании библиотеки содержимого см. в разделе [Библиотека содержимого](../../../core/plan-design/hierarchy/the-content-library.md).  

Помимо указанных выше рекомендаций учитывайте следующие рекомендации при планировании дискового пространства.  

- Для каждого клиента требуется примерно 5 МБ места.  

- При планировании размера временной базы данных первичного сайта ориентируйтесь на общую величину в 25–30 % от размера MDF-файла базы данных сайта. В реальности размер базы данных может оказаться значительно меньше или больше в зависимости от производительности сервера сайта и объема данных, поступающих как за короткие, так и за длинные интервалы времени.  

  > [!NOTE]  
  >  При наличии 50 000 или более клиентов на сайте предусмотрите использование четырех или более MDF-файлов временной базы данных.  

- Размер временной базы данных сайта центра администрирования, как правило, значительно меньше размера базы данных первичного сайта.  

- База данных вторичного сайта имеет следующие ограничения по объему:  

  - SQL Server 2012 Express: 10 Гб  

  - SQL Server 2014 Express: 10 Гб  

##  <a name="clients"></a><a name="bkmk_ScaleClient"></a> Клиенты  
В этом разделе приводятся рекомендуемые конфигурации оборудования для компьютеров, управляемых с помощью клиентского программного обеспечения Configuration Manager.  

### <a name="client-for-windows-computers"></a>Клиент для компьютеров Windows  
Ниже приведены минимальные требования для компьютеров с ОС Windows, которыми вы управляете с помощью Configuration Manager, включая встроенные операционные системы.  

- **Процессор и память.** См. требования к процессору и ОЗУ для ОС компьютера.  

- **Пространство на диске.** 500 МБ свободного места на диске. Рекомендуется 5 ГБ для кэша клиентов Configuration Manager. Если при установке клиента Configuration Manager применить пользовательские параметры, потребуется меньше места на диске.  

    - Используйте свойство SMSCACHESIZE в Client.msi, чтобы задать размер кэша меньше, чем определенное по умолчанию значение 5120 МБ. Минимальный размер составляет 1 МБ. Например, `CCMSetup.exe SMSCachesize=2` создает кэш размером 2 МБ.  

    Дополнительные сведения об этих параметрах установки клиентов см. в разделе [Сведения о свойствах установки клиента](../../../core/clients/deploy/about-client-installation-properties.md).  

    > [!TIP]  
    > Установка клиента с минимальным дисковым пространством рекомендуется для устройств с Windows Embedded, которые обычно имеют диски меньшего размера, чем стандартные компьютеры с Windows.  

Ниже приведены дополнительные минимальные требования к оборудованию для дополнительных функций в Configuration Manager.  

- **Развертывание операционной системы** 384 МБ ОЗУ  

- **Центр программного обеспечения.** Процессор с частотой 500 МГц  

- **Удаленное управление.** Pentium 4 с поддержкой технологии Hyper-Threading, с частотой 3 ГГц (одноядерный) или сравнимый процессор, минимум 1 ГБ ОЗУ для оптимальной производительности.  

### <a name="client-for-linux-and-unix"></a>Клиент для Linux и UNIX  
Ниже приведены минимальные требования для серверов Linux и UNIX, которые управляются с помощью Configuration Manager.  

|Требование|Сведения|  
|-----------------|-------------|  
|Процессор и память|См. требования к процессору и ОЗУ для ОС компьютера.|  
|Пространство на диске|500 МБ свободного места на диске. Рекомендуется 5 ГБ для кэша клиентов Configuration Manager.|  
|Возможность подключения к сети|Клиентские компьютеры Configuration Manager должны иметь сетевое подключение к системам сайта Configuration Manager для обеспечения управления.|  

##  <a name="configuration-manager-console"></a><a name="bkmk_ScaleConsole"></a> Консоль Configuration Manager  
Требования, указанные в приведенной ниже таблице, применяются к каждому компьютеру с консолью Configuration Manager.  

**Минимальная конфигурация оборудования**  

- Intel i3 или совместимый ЦП  

- 2 ГБ ОЗУ  

- 2 ГБ места на диске  

|Масштаб|Минимальное разрешение|  
|-----------------|------------------------|  
|96/100 %|1024 x 768|  
|120/125 %|1280 x 960|  
|144/150 %|1600 x 1200|  
|196/200 %|2500 x 1600|  

**Поддержка PowerShell**  

При установке поддержки PowerShell на компьютере, на котором работает консоль Configuration Manager, можно запускать командлеты PowerShell, чтобы управлять Configuration Manager.

- Поддерживается PowerShell 3.0 или более поздней версии.

Помимо PowerShell поддерживается Windows Management Framework (WMF) 3.0 и более поздней версии.   


##  <a name="lab-deployments"></a><a name="bkmk_ScaleLab"></a> Лабораторные развертывания  
Используйте приведенные ниже минимальные рекомендации по оборудованию для лабораторных и тестовых развертываний Configuration Manager. Эти рекомендации применяются ко всем типам сайтов при использовании до 100 клиентов.  

|Роль|ЦП (ядра)|Память (ГБ)|Пространство на диске (ГБ)|  
|----------|---------------|-------------------|-----------------------|  
|Сервер сайта и базы данных|2–4|8–12|100|  
|Сервер системы сайта|1–4|2–4|50|  
|Клиент|1–2|1–3|30|  