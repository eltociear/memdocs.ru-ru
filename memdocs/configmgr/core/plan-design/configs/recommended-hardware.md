---
title: Рекомендуемое оборудование
titleSuffix: Configuration Manager
description: Ознакомьтесь с рекомендациями в отношении оборудования, которые помогут вам в масштабировании базового развертывания Configuration Manager.
ms.date: 05/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5267f0af-34d3-47a0-9ab8-986c41276e6c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 36b90627f25c5cf19b867a78e141b69266478c58
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/15/2020
ms.locfileid: "83428784"
---
# <a name="recommended-hardware-for-configuration-manager"></a>Рекомендуемое оборудование для Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Руководствуйтесь приведенными ниже рекомендациями при масштабировании среды Configuration Manager, чтобы обеспечить поддержку расширенных возможностей развертывания сайтов, систем сайта и клиентов. Они не предполагают описание всех возможных вариантов конфигурации сайтов и иерархий.  

Используйте сведения в следующих разделах при планировании обновления оборудования. Убедитесь, что оборудование соответствует вычислительным нагрузкам для клиентов и сайтов, использующих доступные функции Configuration Manager.

Дополнительные сведения см. в [руководстве по повышению производительности и масштабированию Configuration Manager](https://gallery.technet.microsoft.com/Configuration-Manager-ba55428e).

## <a name="site-systems"></a><a name="bkmk_ScaleSieSystems"></a> Системы сайта

В этом разделе приводятся рекомендуемые конфигурации оборудования для систем сайта Configuration Manager. Используйте эти рекомендации для поддержки максимального числа клиентов и полноценного использования Configuration Manager. Если среда поддерживает меньшее количество клиентов и использует не все доступные функции, может требоваться меньший объем ресурсов. Как правило, производительность системы ограничивают следующие факторы.

1. Скорость чтения и записи диска

2. Объем доступной памяти

3. ЦП

Для достижения оптимальной производительности используйте конфигурации RAID 10 для всех дисков с данными и сеть Ethernet 1 Гбит/с.

### <a name="site-servers"></a><a name="bkmk_ScaleSiteServer"></a> Серверы сайта

|Конфигурация сайта|ЦП (ядра)|Память (ГБ)|% выделения памяти для SQL Server|  
|-------------------------------|---------------|---------------|----------------------------------------|  
|Автономный сервер первичного сайта с ролью базы данных сайта на том же сервере <sup>[Примечание 1](#bkmk_note1)</sup>|16|96|80|  
|Автономный первичный сервер сайта с удаленной базой данных сайта|8|16|-|  
|Удаленный сервер базы данных для автономного первичного сайта|16|72|90|  
|Сервер сайта центра администрирования с ролью базы данных сайта на том же сервере <sup>[Примечание 1](#bkmk_note1)</sup>|20|128|80|  
|Сервер сайта центра администрирования с удаленной базой данных сайта|8|16|-|  
|Удаленный сервер базы данных для сайта центра администрирования|16|96|90|  
|Подчиненный первичный сайт с ролью базы данных сайта на том же сервере|16|96|80|  
|Сервер дочернего первичного сайта с базой данных удаленного сайта|8|16|-|  
|Удаленный сервер базы данных для дочернего первичного сайта|16|72|90|  
|Сервер вторичного сайта|8|16|-|  

#### <a name="note-1-collocated-sql"></a><a name="bkmk_note1"></a> Примечание 1. SQL с совместным размещением

При установке сервера сайта и SQL Server на одном компьютере развертывание поддерживает максимальные [значения размера и масштабирования](size-and-scale-numbers.md) для сайтов и клиентов. Эта конфигурация может ограничить [параметры высокой доступности](../../servers/deploy/configure/high-availability-options.md), например использование кластера SQL Server. Если у вас большая среда из-за более высоких требований к вводу-выводу для поддержки обеих ролей на одном компьютере, рассмотрите возможность использования удаленного SQL Server.

### <a name="remote-site-system-servers"></a><a name="bkmk_RemoteSiteSystem"></a> Удаленные серверы системы сайта

Эти указания предназначены для компьютеров с одной ролью системы сайта. При установке нескольких ролей системы сайта на одном компьютере внесите в план необходимые коррективы.

|Роль системы сайта|ЦП (ядра)|Память (ГБ)|Пространство на диске (ГБ)|  
|----------------------|---------------|---------------|--------------------|  
|Точка управления|4|8|50|  
|Точка распространения|2|8|Согласно требованиям операционной системы и для хранения развертываемого содержимого|  
|Точка обновления программного обеспечения <sup>[Примечание 2](#bkmk_note2)</sup>|8|16|Согласно требованиям операционной системы и для хранения развертываемых обновлений|  
|Все остальные роли системы сайта|4|8|50|  

#### <a name="note-2-wsus-configurations"></a><a name="bkmk_note2"></a> Примечание 2. Конфигурации WSUS

На компьютере, где размещается точка обновления программного обеспечения, требуются следующие конфигурации для пулов приложений IIS.  

- Увеличение **длины очереди WsusPool** до **2000**.  

- Увеличение **предельного значения выделенной памяти WsusPool** в 4 раза или установка его в **0** (без ограничений).  

### <a name="disk-space-for-site-systems"></a><a name="bkmk_DiskSpace"></a> Пространство на диске для систем сайта

Распределение и конфигурация дискового пространства влияют на производительность Configuration Manager. Каждая среда Configuration Manager имеет индивидуальные характеристики, поэтому реальные цифры могут отличаться от приводимых здесь значений.

Для достижения наивысшей производительности располагайте каждый объект в отдельном выделенном томе RAID. Наибольшее быстродействие томов с данными для Configuration Manager и файлов базы данных обеспечивается при использовании массивов RAID 10.

|Использование данных|Минимальное место на диске|25 000 клиентов|50 000 клиентов|100 000 клиентов|150 000 клиентов|700 000 клиентов (сайт центра администрирования)|  
|----------------|------------------------|--------------------|--------------------|---------------------|---------------------|-----------------------------------------------------|  
|Приложение и файлы журналов Configuration Manager|25 ГБ|50 Гб|100 ГБ|200 Мб|300 ГБ|200 Мб|  
|Файл MDF базы данных сайта|75 ГБ на каждые 25 000 клиентов|75 ГБ|150 ГБ|300 ГБ|500 ГБ|2 ТБ|  
|Файл LDF базы данных сайта|25 ГБ на каждые 25 000 клиентов|25 ГБ|50 Гб|100 ГБ|150 ГБ|100 ГБ|  
|Файлы временной базы данных (MDF и LDF)|По мере необходимости|По мере необходимости|По мере необходимости|По мере необходимости|По мере необходимости|По мере необходимости|  

Сведения о системном диске Windows см. в руководстве по выбору размера для установленной версии ОС.

Содержимое в точках распространения зависит от ваших развертываний. Это руководство не включает место на диске, необходимое для содержимого библиотеки на сервере сайта или в точках распространения. Дополнительные сведения см. в статье [Библиотека содержимого](../../../core/plan-design/hierarchy/the-content-library.md).

При планировании дискового пространства опирайтесь на следующие дополнительные рекомендации.

- Для каждого клиента в базе данных требуется примерно 5–10 МБ места. Это значение зависит от типа иерархии, конфигурации и числа клиентов. Размер обычно меньше для более крупных сред. У сайтов меньшего размера использование базы данных для каждого клиента получается более интенсивным.<!-- SCCMDocs#1048 -->

- Для временной базы данных первичного сайта ориентируйтесь на общую величину в 25–30 % от размера MDF-файла базы данных сайта. Фактический размер может быть меньше или больше. Это зависит от производительности сервера сайта и объема данных, поступающих как за короткие, так и за длинные интервалы времени.

  > [!NOTE]
  > При наличии 50 000 или более клиентов на сайте предусмотрите использование четырех или более MDF-файлов временной базы данных.

- Размер временной базы данных сайта центра администрирования, как правило, значительно меньше размера базы данных первичного сайта.

- При использовании SQL Server Express для базы данных вторичного сайта размер базы данных ограничивается 10 ГБ.

## <a name="clients"></a><a name="bkmk_ScaleClient"></a> Клиенты

В этом разделе приводятся рекомендуемые конфигурации оборудования для компьютеров, управляемых с помощью клиентского программного обеспечения Configuration Manager.

### <a name="client-for-windows-computers"></a>Клиент для компьютеров Windows

Ниже приведены минимальные требования для компьютеров с ОС Windows, которыми вы управляете с помощью Configuration Manager, включая встроенные выпуски:

- **Процессор и память.** См. требования к процессору и ОЗУ для ОС.

- **Пространство на диске.** 500 МБ свободного места на диске. Рекомендуется 5 ГБ для кэша клиентов Configuration Manager. Если при установке клиента Configuration Manager применить пользовательские параметры, потребуется меньше места на диске.

  - Используйте свойство **SMSCACHESIZE** в client.msi, чтобы задать размер кэша меньше, чем определенное по умолчанию значение 5120 МБ. Минимальный размер составляет 1 МБ. В следующем примере создается кэш на 2 МБ: `CCMSetup.exe SMSCACHESIZE=2`

    Дополнительные сведения см. в разделе [о свойствах установки клиентов](../../../core/clients/deploy/about-client-installation-properties.md).

    > [!TIP]
    > Установка клиента с минимальным дисковым пространством рекомендуется для устройств с Windows Embedded, которые обычно имеют диски меньшего размера, чем стандартные компьютеры с Windows.

Ниже приведены дополнительные минимальные требования к оборудованию для дополнительных функций в Configuration Manager:

- **Развертывание ОС.** Объем ОЗУ — не менее 384 МБ.

- **Центр программного обеспечения.** Частота процессора — 500 МГц.

- **Удаленное управление.** Для оптимальной производительности требуется как минимум Pentium 4 с поддержкой технологии Hyper-Threading, с частотой 3 ГГц (одноядерный) или сравнимый процессор, минимум 1 ГБ ОЗУ.

### <a name="client-for-linux-and-unix"></a>Клиент для Linux и UNIX

Ниже приведены минимальные требования для серверов Linux и UNIX, которые управляются с помощью Configuration Manager.

|Требование|Сведения|  
|-----------------|-------------|  
|Процессор и память|См. требования к процессору и ОЗУ для ОС компьютера.|  
|Пространство на диске|500 МБ свободного места на диске. Рекомендуется 5 ГБ для кэша клиентов Configuration Manager.|  
|Возможность подключения к сети|Клиентские компьютеры Configuration Manager должны иметь сетевое подключение к системам сайта Configuration Manager для обеспечения управления.|  

## <a name="configuration-manager-console"></a><a name="bkmk_ScaleConsole"></a> Консоль Configuration Manager

Минимальные требования к оборудованию применяются к каждому компьютеру с консолью Configuration Manager.

- Intel i3 или совместимый ЦП  

- 2 ГБ ОЗУ  

- 2 ГБ места на диске  

|Масштаб|Минимальное разрешение|  
|-----------------|------------------------|  
|96/100 %|1024 x 768|  
|120/125 %|1280 x 960|  
|144/150 %|1600 x 1200|  
|196/200 %|2500 x 1600|  

## <a name="lab-deployments"></a><a name="bkmk_ScaleLab"></a> Лабораторные развертывания

Используйте приведенные ниже минимальные рекомендации по оборудованию для лабораторных и тестовых развертываний Configuration Manager. Эти рекомендации применяются ко всем типам сайтов при использовании до 100 клиентов.  

|Роль|ЦП (ядра)|Память (ГБ)|Пространство на диске (ГБ)|  
|----------|---------------|-------------------|-----------------------|  
|Сервер сайта и базы данных|2–4|8–12|100|  
|Сервер системы сайта|1–4|2–4|50|  
|Клиент|1–2|1–3|30|  
