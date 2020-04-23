---
title: Мониторинг содержимого
titleSuffix: Configuration Manager
description: Узнайте, как отслеживать распространяемое содержимое с помощью консоли Configuration Manager.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 82e8a693-9adf-4ca3-8484-7e101c34c7c1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 31edf096c57b726c3723d261db7a3103fcc311f0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701132"
---
# <a name="monitor-content-you-distribute-with-configuration-manager"></a>Мониторинг распространяемого с помощью Configuration Manager содержимого

*Область применения: Configuration Manager (Current Branch)*

С помощью консоли Configuration Manager можно отслеживать распространяемое содержимое, в том числе:  

- Состояние всех типов пакетов для соответствующих точек распространения.  
- состояние проверки содержимого для содержимого в пакете;  
- состояние содержимого, назначенного конкретной группе точек распространения;  
- состояние содержимого, назначенного точке распространения;  
- состояние дополнительных функций для каждой точки распространения (проверка содержимого, PXE и многоадресная рассылка).  

> [!NOTE]  
> Configuration Manager наблюдает только за содержимым точки распространения, находящимся в библиотеке содержимого. Содержимое точки распространения, хранящееся в пакете или в настраиваемых общих папках, не отслеживается.  

## <a name="content-status-monitoring"></a><a name="BKMK_ContentStatus"></a> Мониторинг состояния содержимого

Узел **Состояние содержимого** в рабочей области **Мониторинг** содержит сведения о пакетах содержимого. В консоли Configuration Manager просмотрите следующую информацию:  

- имя, тип и идентификатор пакета
- Число точек распространения, на которые был отправлен пакет
- Уровень соответствия
- Время создания пакета
- Версия исходных файлов

Вы также найдете подробные сведения о состоянии для любого пакета, в том числе:  

- Состояние распространения
- количество ошибок;
- Ожидающие распространения  
- число установок.

Кроме того, вы можете управлять распространениями, которые выполняются в точку распространения или которым не удалось распространить содержимое в точку распространения.  

- Соответствующий параметр для отмены или повторного распространения содержимого доступен во время просмотра сообщения о состоянии развертывания задания распространения для точки распространения в области **Сведения об активе**. Эта область находится на вкладке **Выполняется** или **Ошибка** в узле **Состояние содержимого**.  
- Кроме того, при просмотре сведений о задании на вкладке **Выполняется** отображается ход выполнения задания в процентах. В сведениях о задании также отображается количество повторных попыток, оставшихся для задания. При просмотре сведений о задании на вкладке **Ошибка** отображается время до следующей повторной попытки.  

Когда вы отменяете развертывание, которое еще не завершено, работа по передаче содержимого,приведенного ниже, прекращается:  

- Состояние развертывание обновляется, чтобы показать сбой распространения и отмену действия пользователем.  
- Новое состояние отображается на вкладке **Ошибка** .  

> [!NOTE]  
> Когда развертывание приближается к завершению, возможно, что действие по отмене этого распространения не будет выполнено до завершения распространения в точку распространения. Если это происходит, действие по отмене развертывания игнорируется и состояние развертывания получает значение "Успешно".  
>
> Несмотря на возможность отмены распространения в точку распространения, которая находится на сервере сайта, это действие выполнено не будет. Это связано с тем, что сервер сайта и точка распространения на сервере сайта совместно используют хранилище единственных копий содержимого. Фактическое задание распространения, которое нужно отменить, отсутствует.  

При повторном распространении содержимого, которое ранее не удалось передать в точку распространения, Configuration Manager сразу же начинает повторно развертывать содержимое в точке распространения. Configuration Manager обновляет состояние развертывания, чтобы отразить текущее состояние повторного развертывания.  

### <a name="tasks-to-monitor-content"></a>Задачи для отслеживания содержимого

1. В консоли Configuration Manager перейдите в рабочую область **Мониторинг**, разверните узел **Состояние распространения** и выберите узел **Состояние содержимого**. Этот узел отображает пакеты.  

2. Выберите пакет, которым требуется управлять.  

3. На вкладке ленты **Главная** в группе **Содержимое** выберите**Просмотр состояния**. В консоли отображаются подробные сведения о состоянии пакета.

Перейдите к одному из следующих разделов для выполнения дополнительных действий.

#### <a name="cancel-a-distribution-that-remains-in-progress"></a>Отмена текущего оставшегося распространения  

1. Перейдите на вкладку **Выполняется**.

2. В области **Сведения об активе**, правой кнопкой мыши щелкните запись распространения, которое нужно отменить, и выберите пункт **Отмена**.  

3. Чтобы подтвердить действие и отменить задание распространения в эту точку распространения, нажмите кнопку **Да**.  

#### <a name="redistribute-content-that-failed-to-distribute"></a>Повторное распространение содержимого, которое не удалось распространить  

1. Перейдите на вкладку **Ошибка**.

2. В области **Сведения об активе**, правой кнопкой мыши щелкните запись распространения, которое нужно распространить повторно, и выберите пункт **Повторить**.  

3. Чтобы подтвердить действие и запустить процесс распространения в эту точку распространения, нажмите кнопку **Да**.  


## <a name="distribution-point-group-status"></a>Состояние группы точек распространения

Узел **Состояние группы точек распространения** в рабочей области **Мониторинг** содержит сведения о группах точек распространения. Вы можете просмотреть следующую информацию:  

- Имя, описание и состояние группы точек распространения
- Число точек распространения, являющихся членами группы точек распространения
- Количество пакетов, назначенных группе
- Уровень соответствия

Можно также просмотреть подробные сведения о состоянии для следующих аспектов:  

- Ошибки группы точек распространения  
- Количество выполняемых в данный момент распределений
- Количество успешно завершенных распространений  

### <a name="monitor-distribution-point-group-status"></a>Мониторинг состояния группы точек распространения  

1. В консоли Configuration Manager перейдите в рабочую область **Мониторинг**, разверните узел **Состояние распространения** и выберите **Состояние группы точек распространения**. Здесь отображаются группы точек распространения.  

2. Выберите группу точек распространения, сведения о состоянии которой требуется получить.  

3. На вкладке ленты**Главная** выберите **Просмотр состояния**. Отобразятся подробные сведения для группы точек распространения.  


## <a name="distribution-point-configuration-status"></a>Состояние конфигурации точки распространения

Узел **Состояние конфигурации точек распространения** в рабочей области **Мониторинг** содержит сведения о точке распространения. Вы можете анализировать включенные для точки распространения атрибуты, такие как PXE, многоадресная рассылка и проверка содержимого. Также проверьте состояние распространения для точки распространения.

> [!WARNING]  
> Состояние конфигурации точки распространения определяется для последних 24 часов. Если на точке распространения возникла ошибка, и было выполнено восстановление, состояние ошибки может отображаться до 24 часов после восстановления.  

### <a name="monitor-distribution-point-configuration-status"></a>Мониторинг состояния конфигурации точки распространения  

1. В консоли Configuration Manager перейдите в рабочую область **Мониторинг**, разверните узел **Состояние распространения** и выберите **Состояние конфигурации точек распространения**.  

2. Выберите точку распространения.  

3. В области результатов перейдите на вкладку **Сведения**. Здесь отображаются сведения о состоянии точки распространения.  


## <a name="client-data-sources-dashboard"></a>Панель мониторинга "Клиентские источники данных"

Используйте панель мониторинга **Источники данных клиента**, чтобы лучше понять,откуда клиенты получают содержимое в вашей среде. Панель мониторинга начинает отображать данные после того, как клиенты скачают содержимое и отправят эту информацию обратно на сайт. Этот процесс может занять до 24 часов.

> [!Note]  
> По умолчанию в Configuration Manager эта дополнительная функция отключена. Необходимо включить функцию **Одноранговый кэш клиента** перед использованием. Дополнительные сведения см. в разделе [Включение дополнительных функций из обновлений](../../manage/install-in-console-updates.md#bkmk_options).  

В консоли Configuration Manager перейдите в рабочую область **Мониторинг**, разверните узел **Состояние распространения** и выберите **Источники данных клиента**. Выберите период времени, который будет применен к панели мониторинга. Затем выберите группу границ, для которой требуется просмотреть сведения. Вы можете навести указатель мыши на плитки, чтобы просмотреть дополнительные сведения о различных источниках содержимого или источники политики.

Чтобы просмотреть сводку по источникам данных клиента для каждой группы границ, можно также воспользоваться новым отчетом **Источники данных клиента – сводные данные**.

### <a name="dashboard-tiles"></a>Плитки панели мониторинга

Она содержит следующие элементы:  

#### <a name="client-content-sources"></a>Источники содержимого клиентов

Показывает источник, из которого клиенты получили содержимое:

- Точка распространения
- [Облачная точка распространения](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md)
- [BranchCache,,](../../../plan-design/configs/support-for-windows-features-and-networks.md#bkmk_branchcache)
- [Одноранговый кэш](../../../plan-design/hierarchy/client-peer-cache.md)
- [Оптимизация доставки](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization) (начиная с версии 1906)<sup>[Примечание 1](#bkmk_note1)</sup>
- Центр обновления Майкрософт: Устройства указывают этот источник, если клиент Configuration Manager скачивает обновления программного обеспечения из облачных служб Майкрософт. В число этих служб входят Центр обновления Майкрософт и Office 365.

![Плитка "Источники содержимого клиентов" на панели мониторинга](media/3555759-do-source.png)

<a name="bkmk_note1"></a>

> [!Note]  
> Начиная с версии 1906<!--3555759-->, чтобы включить оптимизацию доставки на этой панели мониторинга, выполните следующие действия:
>
> - Настройте параметр клиента **Разрешить установку экспресс-обновлений на клиентах** в группе обновлений программного обеспечения.
>
> - Разверните экспресс-обновления Windows 10
>
> См. дополнительные сведения об [управлении файлами экспресс-установки для обновлений Windows 10](../../../../sum/deploy-use/manage-express-installation-files-for-windows-10-updates.md).

#### <a name="distribution-points"></a>Точки распространения

Показывает количество точек распространения, которые являются частью выбранной группы границ.

#### <a name="clients-that-used-a-distribution-point"></a>Клиенты, которые использовали точку распространения

Сколько клиентов из выбранной группы границ использовали точку распространения для получения содержимого.

#### <a name="peer-cache-sources"></a>Источники однорангового кэша

Показывает сколько источников однорангового кэша предоставили журнал скачивания для выбранной группы границ.

#### <a name="clients-that-used-a-peer"></a>Клиенты, которые использовали кэширующий узел

Показывает сколько источников однорангового кэша для выбранной группы границ предоставили журнал скачивания.

#### <a name="top-distributed-content"></a>Основное распространяемое содержимое

Наиболее распределенные пакеты по типу источника