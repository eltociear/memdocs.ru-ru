---
title: Основные принципы управления устройствами
titleSuffix: Configuration Manager
description: Сведения об использовании Configuration Manager для управления устройствами.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2bca3db9-115a-451d-8c93-f073ceefe0c7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bbe7f3a69694395f95596f7f1497c7356b33715f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707072"
---
# <a name="fundamentals-of-managing-devices-with-configuration-manager"></a>Основные сведения об управлении устройствами с помощью Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

С помощью Configuration Manager можно управлять двумя основными категориями устройств.

- *Клиенты* — это устройства (рабочие станции, ноутбуки, серверы и мобильные устройства), на которых установлено клиентское программное обеспечение Configuration Manager. Это клиентское программное обеспечение требуется для некоторых функций управления, таких как инвентаризация оборудования.  

- К *управляемым устройствам* могут относиться *клиенты*, но обычно это мобильные устройства, на которых не установлено клиентское программное обеспечение Configuration Manager. Для управления такими устройствами используется встроенное локальное управление мобильными устройствами в Configuration Manager.

Устройства можно также группировать и идентифицировать на основе пользователя, а не только на основе типа клиента.

## <a name="managing-devices-with-the-configuration-manager-client"></a>Управление устройствами с помощью клиента Configuration Manager

Есть два способа использования клиента Configuration Manager для управления устройствами. Первый способ — обнаружение устройств в сети и развертывание клиентского программного обеспечения на этих устройствах. Второй способ — установка клиентского программного обеспечения на новом компьютере вручную и последующее подключение компьютера к вашему сайту при его подключении к вашей сети. Для обнаружения устройств, на которые еще не установлено клиентское программное обеспечение, можно воспользоваться одним из встроенных методов обнаружения или несколькими. После обнаружения устройства используйте один из методов, чтобы установить клиентское программное обеспечение. Дополнительные сведения об обнаружении см. в разделе [Выполнение обнаружения в Configuration Manager](../servers/deploy/configure/run-discovery.md).  

После обнаружения устройств, поддерживающих запуск клиентского программного обеспечения Configuration Manager, можно установить программное обеспечение с помощью одного из нескольких методов. После установки программного обеспечения и назначения клиента на первичный сайт вы сможете управлять мобильными устройствами. К основным методам установки относятся следующие.

- Принудительная установка клиента

- Установка путем обновления программного обеспечения

- Групповая политика

- Установка на компьютере вручную

- Включение клиента в состав развертываемого образа ОС  

После установки клиента можно упростить задачи управления устройствами с помощью коллекций. Коллекции представляют собой группы устройств или пользователей, которыми можно управлять как одним целым. Например, можно установить приложение для мобильного устройства на всех мобильных устройствах, которые зарегистрированы в Configuration Manager. Для этого можно воспользоваться коллекцией "Все мобильные устройства".  

Дополнительные сведения см. в следующих статьях.  

- [Выбор решения для управления устройствами](../plan-design/choose-a-device-management-solution.md)  

- [Методы установки клиента](../clients/deploy/plan/client-installation-methods.md)  

- [Общие сведения о коллекциях](../clients/manage/collections/introduction-to-collections.md)  

### <a name="client-settings"></a>Параметры клиента

При первой установке Configuration Manager на всех клиентах в иерархии задаются параметры по умолчанию, которые можно изменить. Эти параметры позволяют указать:

- как часто устройства должны подключаться к сайту;

- настроены ли на клиенте установка обновлений программного обеспечения и выполнение других административных операций;

- могут ли пользователи регистрировать свои мобильные устройства для управления с помощью Configuration Manager.  

Вы можете создать пользовательские параметры клиентов и назначить их коллекциям. Участники коллекции могут задавать настраиваемые параметры. Вы также можете создать несколько настраиваемых клиентских параметров, которые будут применяться в заданном порядке (в порядке нумерации). При возникновении конфликтов параметр с меньшим порядковым номером переопределяют остальные параметры.  

На следующем рисунке показан пример создания и применения настраиваемых параметров клиента.  

![Параметры клиента](media/ClientSettings.gif)  

Дополнительные сведения о параметрах клиентов см. в следующих статьях.

- [Настройка параметров клиента](../clients/deploy/configure-client-settings.md)
- [О параметрах клиентов](../clients/deploy/about-client-settings.md)


## <a name="managing-devices-without-the-configuration-manager-client"></a>Управление устройствами без помощи клиента Configuration Manager

Configuration Manager поддерживает управление некоторыми устройствами, на которых не установлено клиентское программное обеспечение и которые не находятся под управлением Intune. Дополнительные сведения см. в статьях [Управление мобильными устройствами с помощью локальной инфраструктуры в Configuration Manager](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) и [Управление мобильными устройствами с помощью Configuration Manager и Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

## <a name="user-based-management"></a>Управление на основе пользователя

Configuration Manager поддерживает коллекции пользователей Azure Active Directory и доменных служб Active Directory. При использовании коллекции пользователей можно установить программное обеспечение на всех компьютерах, используемых участниками коллекции. Чтобы развертываемое программное обеспечение устанавливалось только на устройствах, указанных в качестве основного устройства пользователя, настройте сопоставление пользователей и устройств. Пользователь может иметь одно или несколько основных устройств.  

Для управления развертыванием приложений можно использовать **центр программного обеспечения**. **Центр программного обеспечения** автоматически устанавливается на клиентских компьютерах и доступен в меню **Пуск** в Windows. **Центр программного обеспечения** позволяет управлять программным обеспечением, а также выполнять следующие задачи.  

- Установка программного обеспечения  

- Планирование автоматической установки программного обеспечения в нерабочие часы  

- Настройка периода времени, когда Configuration Manager может устанавливать программное обеспечение на устройствах  

- Настройка параметров доступа для удаленного управления, если в Configuration Manager включено удаленное управление  

- Настройка параметров управления электропитанием, если эта функция включена администратором  

- Поиск, установка и запрос программного обеспечения

- Конфигурация параметров

- После настройки укажите основное устройство для сопоставления пользователей и устройств

Дополнительные сведения см. в следующих статьях:

- [Планирование использования Центра программного обеспечения](../../apps/plan-design/plan-for-software-center.md)
- [Связывание пользователей и устройств с помощью сопоставления пользователей и устройств](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)
- [Руководство пользователя центра программного обеспечения](software-center.md)