---
title: Развертывание конфигурационных баз
titleSuffix: Configuration Manager
description: Развертывание шаблонов базовых конфигураций для определения развертываний шаблонов базовой конфигурации, а также для добавления или удаления шаблонов базовой конфигурации из развертываний.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 9be8aaf3-075e-4acd-abd2-7459254e16e2
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 55b559f9b16eabfe2c2096497e6f63816b400803
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692452"
---
# <a name="how-to-deploy-configuration-baselines-in-configuration-manager"></a>Способы развертывания конфигурационных баз в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Прежде чем клиентские устройства в коллекциях пользователей или устройств смогут выполнять проверку соответствия конфигурационной базе, такие конфигурационные базы в Configuration Manager необходимо развернуть для одной или нескольких коллекций.  

С помощью диалогового окна **Развертывание шаблонов базовой конфигурации** можно определить развертывания шаблонов конфигурации, включая добавление и удаление шаблонов конфигурации из развертываний, а также настройку расписания оценки.  

## <a name="deploy-a-configuration-baseline"></a>Развертывание конфигурационной базы  

1.  В консоли Configuration Manager последовательно выберите **Активы и соответствие** > **Параметры соответствия** > **Шаблоны базовой конфигурации**.  

3.  В списке **Шаблоны базовой конфигурации** выберите нужную конфигурационную базу, затем на вкладке **Главная** в группе **Развертывание** щелкните элемент **Развернуть**.  

4.  В диалоговом окне **Развертывание шаблонов базовой конфигурации** в списке **Доступные шаблоны базовой конфигурации** выберите конфигурационные базы для развертывания. Нажмите кнопку **Добавить** , чтобы добавить шаблоны в список **Выбранные шаблоны базовой конфигурации** .  

    > [!IMPORTANT]  
    >  Если изменить элемент конфигурации, добавленный в развернутую конфигурационную базу, такой измененный элемент не проверяется на соответствие до момента следующей запланированной проверки.  

5.  Укажите следующие дополнительные сведения.  

    -   **Исправлять несоответствующие параметры, когда это возможно** — автоматическое исправление правил, не соответствующих параметрам инструментария WMI, реестра, скриптов и другим параметрам мобильных устройств, зарегистрированным с помощью Configuration Manager.  

    -   **Разрешить исправление за пределами периодов обслуживания** — если для коллекции, в которой развертывается конфигурационная база, был настроен период обслуживания, установите этот флажок, чтобы разрешить исправление параметров соответствия за пределами периода обслуживания. Дополнительные сведения о периодах обслуживания см. в разделе [Использование периодов обслуживания](../../core/clients/manage/collections/use-maintenance-windows.md).  

6.  **Создавать оповещение** — настройка предупреждения, которое будет создаваться, если соответствие конфигурационной базы меньше заданного процентного значения в указанную дату и время. Также можно указать, требуется ли отправлять оповещение в System Center Operations Manager.  

7.  **Коллекция** — нажмите кнопку **Обзор** , чтобы выбрать коллекцию, в которой требуется развернуть конфигурационную базу.  

8.  **Задайте расписание оценки соответствия для этого шаблона базовой конфигурации** — задание расписания проверки развернутого шаблона базовой конфигурации на клиентских компьютерах. Это может быть простое или настраиваемое расписание.  

    > [!NOTE]  
    >  Если конфигурационная база развернута на компьютере, оценка соответствия выполняется в течение двух часов от момента запланированного запуска, указанного в расписании. Если конфигурационная база развернута для пользователя, оценка будет выполнена при входе пользователя в систему.  

9. Нажмите кнопку **ОК** , чтобы закрыть диалоговое окно **Развертывание шаблонов базовой конфигурации** и создать развертывание. Дополнительные сведения о мониторинге развертывания см. в разделе [Мониторинг параметров соответствия](monitor-compliance-settings.md).  