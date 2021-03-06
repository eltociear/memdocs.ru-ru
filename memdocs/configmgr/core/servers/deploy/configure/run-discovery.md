---
title: Обнаружение ресурсов устройств и пользователей
titleSuffix: Configuration Manager
description: Общие сведения о процессе обнаружения и записях данных обнаружения.
ms.date: 02/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 30844519-ce14-456f-bfb8-4318b578e9f6
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1869c9e6de455b7086a051db91bb26bc00a91a5f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700992"
---
# <a name="run-discovery-for-configuration-manager"></a>Запуск обнаружения в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

В Configuration Manager используется один или несколько методов обнаружения для поиска ресурсов устройств и пользователей, которыми можно управлять. Кроме того, вы можете использовать обнаружение для идентификации сетевой инфраструктуры в своей среде. Существует несколько различных методов, которые вы можете использовать для обнаружения различных объектов. Каждый из этих методов имеет свои собственные конфигурации и ограничения.  

## <a name="overview-of-discovery"></a>Обзор процесса обнаружения  
 Обнаружение — это процесс, с помощью которого Configuration Manager узнает о том, какими объектами можно управлять. Ниже приведены доступные методы обнаружения.  

-   Обнаружение лесов Active Directory  

-   Обнаружение групп Active Directory  

-   Обнаружение систем Active Directory  

-   Обнаружение пользователей Active Directory  

-   Обнаружение пакетов пульса  

-   Обнаружение сети  

-   обнаружения серверов  

> [!TIP]  
>  Сведения об отдельных методах обнаружения см. в разделе [Сведения о методах обнаружения для Configuration Manager](../../../../core/servers/deploy/configure/about-discovery-methods.md).  
>   
>  Сведения о том, как выбрать подходящий метод и на каких сайтах в иерархии его использовать, см. в разделе [Выбор методов обнаружения для Configuration Manager](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md).  

 Для использования большинства методов обнаружения необходимо включить нужный метод на сайте и настроить его для поиска в определенных расположениях в сети или в Active Directory. При запуске он запрашивает в указанном расположении сведения об устройствах и пользователях, которыми может управлять Configuration Manager. Если метод обнаружения успешно находит сведения о ресурсе, он помещает эту информацию в файл, который называется записью данных обнаружения (DDR). Этот файл затем обрабатывается на первичном сайте или сайте центра администрирования. Обработка DDR создает новую запись в базе данных сайта для вновь обнаруженных ресурсов или обновляет существующие записи новой информацией.  

 Некоторые методы обнаружения могут генерировать большой объем сетевого трафика, и обработка создаваемых ими записей данных обнаружения может значительно нагружать процессор. Поэтому используйте только те методы обнаружения, которые абсолютно необходимы для достижения ваших целей. Для начала можно задействовать всего один или два метода, а затем контролируемым образом включать другие методы, чтобы расширить возможности обнаружения в данной среде.  

 После добавления сведений обнаружения в базу данных сайта они реплицируются на каждый сайт в иерархии независимо от того, на каком сайте они были обнаружены или обработаны. Таким образом, хотя на разных сайтах можно настроить различные расписания и параметры для методов обнаружения, каждый определенный метод обнаружения запускается только на одном сайте. Это позволяет снизить использование пропускной способности сети, а также дублирование действий обнаружения и обработку избыточных данных обнаружения на нескольких сайтах.  

 Вы можете использовать данные обнаружения для создания пользовательских коллекций и запросов, в которых ресурсы логически группируются для задач управления. Пример.  

-   Принудительная отправка установок клиента или обновления.  

-   Развертывание содержимого для пользователей или устройств.  

-   Развертывание параметров клиента и соответствующих конфигураций.

##  <a name="about-discovery-data-records"></a><a name="BKMK_DDRs"></a> Сведения о записях данных обнаружения  
 Записи данных обнаружения (DDR) — это файлы, созданные методом обнаружения. Они содержат сведения о ресурсе, которым можно управлять в Configuration Manager, например компьютере, пользователе и, в некоторых случаях, сетевой инфраструктуре. Они обрабатываются на первичных сайтах или на сайтах центра администрирования. После ввода в базу данных сведений о ресурсах из записи DDR запись DDR удаляется, а полученные из нее сведения реплицируются на все сайты иерархии как глобальные данные.  

 Сайт, на котором обрабатывается запись DDR, зависит от сведений, которые она содержит.  

-   Записи DDR для вновь обнаруженных ресурсов, которых еще нет в базе данных, обрабатываются на сайте иерархии верхнего уровня. Сайт верхнего уровня создает новую запись ресурса в базе данных и назначает ей уникальный идентификатор. Записи DDR передаются посредством репликации на основе файлов до тех пор, пока не достигают сайта верхнего уровня.  

-   Записи DDR ранее обнаруженных объектов обрабатываются на первичных сайтах. Дочерние первичные сайты не передают записи DDR сайту центра администрирования, если DDR содержит сведения о ресурсе, который уже присутствует в базе данных.  

-   Вторичные сайты не обрабатывают записи данных обнаружения и всегда передают их посредством репликации на основе файлов на родительский первичный сайт.  

Файлы DDR имеют расширение .ddr и размер, примерно равный 1 КБ.  

## <a name="get-started-with-discovery"></a>Начало работы с обнаружением  
 Прежде чем использовать консоль Configuration Manager для настройки обнаружения, важно понять различия между методами, их возможности и, в некоторых случаях, их ограничения.  

Сведения в следующих разделах послужат хорошей базой, которая поможет вам в дальнейшем успешно использовать методы обнаружения.  

-   [Сведения о методах обнаружения для Configuration Manager](../../../../core/servers/deploy/configure/about-discovery-methods.md)  

-   [Выбор методов обнаружения для Configuration Manager](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md)  

Выбрав нужные методы, вы можете настроить их, обратившись к разделу [Настройка методов обнаружения для Configuration Manager](../../../../core/servers/deploy/configure/configure-discovery-methods.md).  
