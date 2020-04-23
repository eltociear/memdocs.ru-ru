---
title: Обеспечение соответствия устройств
titleSuffix: Configuration Manager
description: Вы можете управлять конфигурациями и соответствием устройств в организации с помощью Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 7568c9aa-b99e-4466-bfc8-0301aa376930
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: e9844c20373f2442be2c5c1f06f893eae3b0fe57
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692162"
---
# <a name="ensure-device-compliance-with-configuration-manager"></a>Обеспечьте соответствие устройства с Configuration Manager.

*Область применения: Configuration Manager (Current Branch)*

Параметры соответствия в Configuration Manager предоставляют средства и ресурсы, необходимые для управления конфигурациями и соответствием требованиям устройств в вашей организации. Это поможет поддерживать следующие бизнес-требования.  

-   Сравнение конфигурации компьютеров под управлением Windows и Mac, серверов и мобильных устройств, которыми вы управляете, с рекомендуемыми конфигурациями, которые вы создаете или получаете от других поставщиков.  

-   Определение несанкционированных конфигураций устройств.  

-   Составление отчетов о соответствии законодательным требованиям и внутренним политикам безопасности.  

-   Определение уязвимостей системы безопасности.  

-   Предоставление службе поддержки сведений для обнаружения возможных причин зарегистрированных инцидентов и проблем путем выявления несоответствующих конфигураций.  

-   Автоматическое исправление некоторых несовместимых параметров на мобильных устройствах.  

-   Устранение несоответствий путем развертывания приложений, пакетов и программ или скриптов в коллекции, в которую автоматически добавляются устройства, отправившие отчет о своем несоответствии требованиям.  


## <a name="get-started"></a>Начало работы  
 Получите общее представление о параметрах соответствия и задачах, которые они позволяют выполнять.  

 [Приступая к работе с параметрами соответствия](../../compliance/get-started/get-started-with-compliance-settings.md)  

## <a name="plan-and-design"></a>Планирование и проектирование  
 Перед началом работы с параметрами совместимости убедитесь, что выполнены все необходимые условия, описанные в этом разделе.  

 [Планирование и настройка параметров соответствия](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)  

## <a name="common-tasks"></a>Типичные задачи  
 В этом разделе вы найдете ряд распространенных сценариев, с помощью которых научитесь использовать параметры соответствия в Configuration Manager.  

 [Распространенные задачи по управлению соответствием](../../compliance/plan-design/common-tasks-for-managing-compliance.md)  

## <a name="remote-connection-profiles"></a>Профили удаленного подключения  
 Элемент конфигурации этого типа позволяет настроить для компьютеров пользователей удаленное подключение к рабочим компьютерам, когда они не подключены к домену или если персональные компьютеры подключены через Интернет.  

 [Создание профилей удаленного подключения](../deploy-use/create-remote-connection-profiles.md)  

## <a name="user-data-and-profiles"></a>Профили и данные пользователей  
 Элементы конфигурации этого типа содержат параметры, управляющие перенаправлением папок, автономными файлами и перемещаемыми профилями на компьютерах с Windows 8 и более поздней версии для пользователей в вашей иерархии.  

 [Создание элементов конфигурации данных и профилей пользователя](../deploy-use/create-user-data-and-profiles-configuration-items.md)  

## <a name="windows-edition-upgrade-policy"></a>Политика обновления выпусков Windows  
 Политика обновления выпусков позволяет автоматически обновлять устройства на базе Windows 10 до более новой версии. Можно указать ключ продукта для обновления классических версий Windows 10 или файл лицензии, используемый для обновления устройства под управлением Windows 10 Mobile и Windows 10 Holographic.  

 [Обновление устройств Windows с помощью политики обновления выпусков](../deploy-use/upgrade-windows-version.md)  