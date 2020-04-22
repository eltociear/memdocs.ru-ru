---
title: Что такое Configuration Manager?
titleSuffix: Configuration Manager
description: Общие сведения о Microsoft Endpoint Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3343eccf-bf09-41cd-9e68-03e893c7f904
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 78b9175c10d4389623bfa08ac7895df200944a13
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706912"
---
# <a name="what-is-configuration-manager"></a>Что такое Configuration Manager?

*Область применения: Configuration Manager (Current Branch)*

Начиная с версии 1910 Configuration Manager входит в состав Microsoft Endpoint Manager.

![Microsoft Endpoint Configuration Manager](media/4960084-endpoint-manager-logo.png)

Microsoft Endpoint Manager — это интегрированное решение для управления всеми устройствами. Корпорация Майкрософт объединяет Configuration Manager и Intune без сложной миграции и с упрощенной лицензией. Продолжайте пользоваться имеющимися вложениями в Configuration Manager, используя преимущества Microsoft Cloud в своем темпе.

Следующие решения по управлению Майкрософт теперь являются частью торговой марки **Microsoft Endpoint Manager**:

- [Configuration Manager](https://docs.microsoft.com/configmgr)
- [Intune](https://docs.microsoft.com/intune)
- [Аналитика компьютеров](../../desktop-analytics/overview.md)
- [AutoPilot](https://docs.microsoft.com/intune/enrollment/enrollment-autopilot);
- другие функции в [консоли администратора управления устройствами](https://go.microsoft.com/fwlink/?linkid=2109094).

Дополнительные сведения см. в статье [Вопросы и ответы по Microsoft Endpoint Configuration Manager](microsoft-endpoint-manager-faq.md).

## <a name="introduction"></a>Введение

Используйте Configuration Manager для выполнения следующих действий по управлению системами:

- повысить производительность и эффективность ИТ-отдела благодаря уменьшению объема ручных задач, что позволяет сосредоточиться на особо важных проектах;  
- добиться максимальной отдачи от вложений в оборудование и программное обеспечение;  
- расширить возможности пользователей, предоставляя им подходящее программное обеспечение в нужное время.  

Configuration Manager помогает вам предоставлять более эффективные ИТ-службы за счет следующих возможностей:

- Безопасное и масштабируемое развертывание приложений, обновлений программного обеспечения и операционных систем.
- Действия в реальном времени на управляемых устройствах.
- Аналитика на основе облака и управление для локальных и интернет-устройств.
- Управление параметрами соответствия  
- Комплексное управление серверами, настольными системами и ноутбуками.

Configuration Manager работает параллельно с многими технологиями и решениями Майкрософт и расширяет их возможности. Например, Configuration Manager интегрируется со следующими компонентами:  

- Microsoft Intune для совместного управления разнообразными платформами мобильных устройств
- Microsoft Azure для размещения облачных служб, расширяющих возможности служб управления
- Службы Windows Server Update Services (WSUS) — для управления обновлениями программного обеспечения
- Службы сертификатов
- Exchange Server и Exchange Online
- Групповая политика
- DNS
- Комплект средств для автоматизации развертывания Windows (Windows ADK) и средство миграции пользовательской среды (USMT)
- Службы развертывания Windows (WDS)
- Удаленный рабочий стол и удаленный помощник

Configuration Manager также использует:  

- доменные службы Active Directory и Azure Active Directory для обеспечения безопасности, обнаружения службы, настройки, а также для обнаружения пользователей и устройств, которыми необходимо управлять.  
- Microsoft SQL Server в качестве распределенной базы данных управления изменениями и интегрирован с SQL Server Reporting Services (SSRS) для составления отчетов, позволяющих отслеживать действия по управлению;  
- роли системы сайта, расширяющие функции управления и использующие веб-службы IIS;
- оптимизация доставки, транспортный протокол фоновой передачи с малой дополнительной задержкой (LEDBAT) в Windows, фоновая интеллектуальная служба передачи (BITS), BranchCache и другие технологии однорангового кэширования для управления содержимым в сетях и между устройствами.

Для успешной работы с Configuration Manager в рабочей среде необходимо тщательно спланировать и протестировать функции управления. Configuration Manager является эффективным приложением управления, способным повлиять на каждый компьютер в организации. Если развертывание и управление Configuration Manager осуществляется с тщательным планированием и обеспечением соответствия требованиям организации, Configuration Manager может сократить трудозатраты администраторов и снизить совокупную стоимость владения.  

## <a name="user-interfaces"></a>Пользовательские интерфейсы

### <a name="the-configuration-manager-console"></a><a name="BKMK_Console"></a> Консоль Configuration Manager

После установки Configuration Manager используйте консоль Configuration Manager для настройки сайтов, клиентов, а также выполнения и отслеживания задач управления. Эта консоль является основным инструментом администрирования и позволяет управлять несколькими сайтами.  

Можно установить консоль Configuration Manager на дополнительных компьютерах и ограничить доступ и отображаемые администраторам данные в консоли, используя ролевое администрирование Configuration Manager.  

Дополнительные сведения см. в статье об [использовании консоли Configuration Manager](../servers/manage/admin-console.md).

### <a name="software-center"></a><a name="BKMK_ApplicationCatalog"></a> Центр программного обеспечения

**Центр программного обеспечения** — это приложение, которое автоматически устанавливается при установке клиента Configuration Manager на устройстве Windows. Пользователи используют центр программного обеспечения для запроса и установки развертываемого вами программного обеспечения. Центр программного обеспечения позволяет выполнять следующие действия:  

- Поиск и установка приложений, обновлений программного обеспечения и новых версий ОС
- Просмотр истории запросов программного обеспечения
- Просмотр соответствия устройств политикам вашей организации

Можно также отобразить пользовательские вкладки в центре программного обеспечения, чтобы удовлетворить дополнительные бизнес-требования.

Дополнительные сведения см. в [руководстве пользователя по центру программного обеспечения](software-center.md).

## <a name="next-steps"></a>Дальнейшие шаги

Перед установкой Configuration Manager ознакомьтесь с основными принципами и понятиями.

- Если вы уже работали с System Center 2012 Configuration Manager, см. статью [Изменения по сравнению с System Center 2012 Configuration Manager](../plan-design/changes/what-has-changed-from-configuration-manager-2012.md).

- Общее техническое описание Configuration Manager см. в статье [Основные понятия, связанные с Configuration Manager](fundamentals.md).

Получив общие сведения, обратитесь к библиотеке документации, чтобы выполнить развертывание и приступить к использованию Configuration Manager. Начать можно со следующих статей:

- [Функции и возможности в Configuration Manager](../plan-design/changes/features-and-capabilities.md)  
- [Выбор решения для управления устройствами](../plan-design/choose-a-device-management-solution.md)  
- [Оценка Configuration Manager путем создания собственной лабораторной среды](../get-started/set-up-your-lab.md)
- [Поиск справочных материалов по использованию Configuration Manager](find-help.md)  
