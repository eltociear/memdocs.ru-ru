---
title: Контрольный список для версии 1702
titleSuffix: Configuration Manager
description: Сведения о действиях, которые необходимо выполнить перед обновлением до Configuration Manager версии 1702.
ms.date: 06/06/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b587779e-1bd3-4ee3-8146-8e31f53499bd
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: d3ae44892cd46a438113fb54dad0e290b8fb148e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707742"
---
# <a name="checklist-for-installing-update-1702-for-configuration-manager"></a>Контрольный список для установки обновления 1702 для Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

При использовании текущей ветви Configuration Manager можно установить обновление в консоль для версии 1702 для обновления иерархии по сравнению с предыдущей версией.

> [!TIP]
> Версия 1702 также доступна как [базовый носитель](updates.md#bkmk_Baselines), который можно использовать для установки первого сайта новой иерархии.

Чтобы получить обновление для версии 1702, необходимо использовать роль системы сайта "Точка подключения службы" на сайте верхнего уровня в иерархии. Допускается как оперативный, так и автономный режим. После того как иерархия скачает пакет обновления с серверов Майкрософт, его можно найти в консоли в узле **Администрирование &gt; Обзор &gt; Облачные службы &gt; Обновления и обслуживание**.

-   Если обновление имеет состояние **Доступно**, оно готово к установке. Прежде чем установить версию 1702, просмотрите [сведения об установке обновления 1702](#about-installing-update-1702) и [контрольный список настроек](#checklist), которые нужно выполнить перед началом обновления.

-   Если обновление имеет состояние **Загружается**, которое не меняется, просмотрите файлы **hman.log** и **dmpdownloader.log**, чтобы проверить наличие ошибок.

    -   Если dmpdownloader.log указывает, что процесс dmpdownloader находится в спящем режиме и ожидает завершения интервала для проверки наличия обновлений, вы можете перезапустить службу **SMS_Executive** на сервере сайта, чтобы возобновить скачивание распространяемых файлов для обновления.

    -   Еще одна распространенная проблема загрузки возникает, когда параметры прокси-сервера блокируют загрузку с `silverlight.dlservice.microsoft.com` и `download.microsoft.com`.

Дополнительные сведения об установке обновлений см. в разделе [Обновления в консоли и обслуживание](updates.md#bkmk_inconsole).

Сведения о версиях Current Branch см. в подразделе [Базовые и обновленные версии](updates.md#bkmk_Baselines) раздела [Обновления для Configuration Manager](updates.md).

## <a name="about-installing-update-1702"></a>Информация об установке обновления 1702

**Сайты.**  
Обновление 1702 можно установить только на сайте верхнего уровня в иерархии. Это означает, что установку следует запустить на сайте центра администрирования, если таковой имеется, или на автономном первичном сайте. После установки обновления на сайте верхнего уровня дочерние сайты обновляются в следующем порядке.

-   Подчиненные первичные сайты автоматически устанавливают обновление, как только сайт центра администрирования завершит установку обновления. Для управления временем установки обновлений можно использовать периоды обслуживания. Дополнительные сведения см. в статье [Service windows for site servers](service-windows.md) (Периоды обслуживания для серверов сайта).

-   После того, как на родительском первичном сайте завершится установка обновления, необходимо вручную обновить вторичные сайты через консоль Configuration Manager. Автоматическое обновление серверов вторичных сайтов не поддерживается.

**Роли системы сайта.**  
Когда сервер сайта устанавливает обновление, автоматически обновляются все роли системы сайта, установленные на сервере сайта и на удаленных компьютерах. Перед установкой обновления нужно убедиться, что каждый сервер системы сайта отвечает предварительным требованиям для работы с новой версией обновления.

**Консоли Configuration Manager.**    
При первом использовании консоли Configuration Manager после завершения обновления появится запрос на обновление этой консоли. Чтобы обновить консоль, необходимо запустить программу установки Configuration Manager на компьютере, где размещена консоль, и выбрать параметр для обновления консоли. Мы рекомендуем не откладывать установку обновления на консоль.

> [!IMPORTANT]  
> Имейте в виду, что после установки обновления на сайте центра администрирования и вплоть до завершения обновлений на всех дочерних первичных сайтах будут существовать следующие ограничения и задержки.    
> - **Обновления клиента** не запускаются. Сюда относится автоматическое обновление клиентов и подготовительных клиентов. Кроме того, невозможно повысить уровень подготовительных клиентов до рабочих клиентов, пока установка обновлений не завершится на всех сайтах. Когда завершится установка обновлений на последнем сайте, начинается обновление клиентов с учетом выбранной вами конфигурации.   
> - Недоступны **новые возможности**, которые вы активировали при обновлении. Это сделано специально, чтобы предотвратить репликацию данных, связанных с такими функциями, на сайт, на котором поддержка этих функций еще не установлена. Новые функции будут доступны для использования, когда обновление завершится на всех основных сайтах.   
> - **Связи репликации** между сайтом центра администрирования и дочерними основными сайтами отображаются как необновленные. В связи с этим состояние установки пакета обновления отображается как завершенное с предупреждением для инициализации репликации мониторинга. В узле мониторинга на консоли отображается статус *Выполняется конфигурация ссылки*.



## <a name="checklist"></a>Контрольный список

**Убедитесь, что на всех сайтах установлена версия Configuration Manager, поддерживающая обновление до версии 1702:**    
На каждом сервере сайта в иерархии должна выполняться одна и та же версия Configuration Manager, прежде чем можно будет начать установку обновления 1702. Чтобы обновить версию до 1702, необходимо использовать версию 1602, 1606 или 1610.

**Проверьте состояние Software Assurance или аналогичной подписки.**    
Для установки обновления 1702 необходимо действующее соглашение Software Assurance. При установке этого обновления на вкладке **Лицензирование** будет предложено подтвердить **дату истечения срока действия Software Assurance**.

Это необязательное значение, которое можно использовать для напоминания о предстоящем завершении срока действия лицензии. Эта дата отображается при установке последующих обновлений. Возможно, вы уже указали это значение во время установки, настройки, обновления или через вкладку **Лицензирование** в разделе **параметров иерархии** консоли Configuration Manager.

Дополнительные сведения см. в разделе [Лицензирование и ветви в Configuration Manager](../../understand/learn-more-editions.md).

**Проверьте установленные версии платформы Microsoft .NET на серверах системы сайта**. При установке сайтом этого обновления Configuration Manager автоматически устанавливает платформу .NET Framework 4.5.2 на каждом компьютере, на котором размещается одна из следующих ролей системы сайта (если на нем еще не установлена платформа .NET Framework 4.5 или более поздней версии).

-   Прокси-точка регистрации.
-   Точка регистрации
-   Точка управления
-   Точка подключения службы

Этот процесс установки может перевести сервер системы сайта в состояние ожидания перезагрузки и сообщать об ошибках средству просмотра состояния компонентов Configuration Manager. Кроме того, до перезагрузки сервера на нем возможны произвольные сбои приложений .NET.

Дополнительные сведения см. в разделе [Необходимые компоненты для сайта и системы сайта](../../plan-design/configs/site-and-site-system-prerequisites.md).

**Проверьте версию комплекта средств для развертывания и оценки (ADK) для Windows 10**. Комплект Windows 10 ADK должен иметь версию не ниже 1607. Если вам нужно обновить ADK, сделайте это до начала обновления Configuration Manager. Так обеспечите автоматическое обновление загрузочных образов по умолчанию до последней версии Windows PE. (Пользовательские образы загрузки нужно обновлять вручную.)

Если вы обновили сайт раньше, чем ADK, восстановить образы загрузки можно с помощью скрипта, предоставленного в блоге [Configuration Manager and the Windows ADK for Windows 10, version 1607](https://blogs.technet.microsoft.com/enterprisemobility/2016/09/09/configuration-manager-and-the-windows-adk-for-windows-10-version-1607/) (Configuration Manager и Windows ADK для Windows 10, версия 1607).

**Проверьте состояние сайта и иерархии и убедитесь в том, что все проблемы разрешены:** Перед обновлением сайта устраните все проблемы эксплуатации для сервера сайта, сервера базы данных сайта и ролей системы сайта, установленных на удаленных компьютерах. Обновление сайта может завершиться неудачей из-за существующих проблем в работе.

Дополнительные сведения см. в разделе [Использование оповещений и системы состояния для Configuration Manager](use-alerts-and-the-status-system.md).

**Проверьте репликацию файлов и данных между сайтами.**    
Убедитесь в том, что репликация файлов и базы данных между сайтами действует и является актуальной. Задержки или невыполненная работа могут помешать бесперебойному, успешному выполнению обновления.
Для репликации базы данных можно использовать Replication Link Analyzer, который поможет устранить проблемы перед началом обновления.

Дополнительные сведения см. в статье [Replication Link Analyzer](monitor-replication.md#BKMK_RLA) в разделе [Мониторинг репликации базы данных](monitor-replication.md) .

**Установите все доступные важные обновления для операционных систем на компьютерах, где размещен сайт, сервер базы данных сайта и удаленные роли системы сайта:** Перед установкой обновления для Configuration Manager установите все критические обновления для каждой соответствующей системы сайта. Если устанавливаемое обновление требует перезагрузки, перезагрузите соответствующие компьютеры перед началом обновления.

**Выключите реплики базы данных для точек управления на первичных сайтах.**    
Configuration Manager не может обновить первичный сайт с включенными репликами баз данных для точек управления. Отключите репликацию базы данных, прежде чем устанавливать обновления для Configuration Manager.

Дополнительные сведения см. в статье [Реплики базы данных для точек управления для Configuration Manager](../deploy/configure/database-replicas-for-management-points.md).

**Настройте группы доступности SQL Server AlwaysOn для отработки отказа вручную.**    
Если вы используете группу доступности, настройте для нее отработку отказа вручную перед запуском установки обновления. После обновления сайта можно восстановить автоматическую отработку отказа. Дополнительные сведения см. в статье [SQL Server AlwaysOn для базы данных сайта](../deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).

**Перенастройка точек обновления программного обеспечения, использующих балансировку сетевой нагрузки.**    
Configuration Manager не может обновить сайт, использующий кластер балансировки сетевой нагрузки (NLB) для точек обновления программного обеспечения.

Если для точек обновления программного обеспечения используются кластеры балансировки сетевой нагрузки, удалите кластер балансировки сетевой нагрузки с помощью Windows PowerShell.
Дополнительные сведения см. в статье [Планирование обновлений программного обеспечения](../../../sum/plan-design/plan-for-software-updates.md).

**Отключите все задачи обслуживания сайта на каждом сайте на период установки обновления на этом сайте.**    
Перед установкой обновления отключите все задачи обслуживания сайта, которые могут запускаться в то время, когда активен процесс обновления. В частности, необходимо отключить следующие задачи:

-   Резервное копирование сервера сайта
-   Удаление устаревших операций клиента
-   Удаление устаревших данных обнаружения

Если во время установки обновления выполняется задача обслуживания базы данных сайта, то обновление может завершиться сбоем. Прежде чем отключить задачу, запишите ее расписание, чтобы восстановить конфигурацию после установки обновления.

Дополнительные сведения см. в разделах [Задачи обслуживания для Configuration Manager](maintenance-tasks.md) и [Справочные сведения о задачах обслуживания в Configuration Manager](reference-for-maintenance-tasks.md).

**Приостановите на время все антивирусные программы на серверах Configuration Manager:** Перед обновлением сайта убедитесь, что антивирусное программное обеспечение остановлено на серверах Configuration Manager. <!--SMS.503481--> 

**Создайте резервную копию базы данных сайта на сайте центра администрирования и первичных сайтах.** Перед обновлением сайта создайте резервную копию базы данных сайта, чтобы гарантировать успешное резервирование для использования при аварийном восстановлении.

Дополнительные сведения см. в разделе [Резервное копирование и восстановление в Configuration Manager](backup-and-recovery.md).

<!-- Removed from update guidance 6/6/2017
**Test the database upgrade on a copy of the most recent site database backup:** 
Before you update a Configuration Manager central administration site or primary site, you can test the site database upgrade process on a copy of the site database.

-   We recommend that you test the site database upgrade process because when you upgrade a site, the site database might be modified.

-   Although a test database upgrade is not required, it can identify problems for the upgrade before your production database is affected.

-   A failed site database upgrade can render your site database inoperable and might require a site recovery to restore functionality.

-   Although the site database is shared between sites in a hierarchy, plan to test the database at each applicable site before you upgrade that site.

-   If you use database replicas for management points at a primary site, disable replication before you create the backup of the site database.

Configuration Manager does not support the backup of secondary sites nor does it support the test upgrade of a secondary site database.

Do not run a test database upgrade on the production site database. Doing so updates the site database and could render your site inoperable. For more information, see [Step 2: Test the database upgrade before installing an update](install-in-console-updates.md#bkmk_step2) from **Before you install an in-console update**.
-->

**Запланируйте пилотное развертывание клиента.**    
При установке обновления, которое изменяет клиент, можно проверить это новое обновление клиента в подготовительной среде, прежде чем развернуть его и обновить активные клиенты.

Чтобы воспользоваться этой возможностью, перед началом установки обновления нужно настроить сайт для поддержки автоматического обновления в подготовительной среде.

Дополнительные сведения см. в статьях [Обновление клиентов](../../clients/manage/upgrade/upgrade-clients.md) и [Проверка обновления клиента в предварительной коллекции](../../clients/manage/upgrade/test-client-upgrades.md).

**Запланируйте периоды обслуживания для управления временем установки обновлений серверами сайта.**    
Вы можете использовать периоды обслуживания, чтобы определить период времени для установки обновлений на сервере сайта.

Это поможет контролировать время установки обновлений на сайты в иерархии. Дополнительные сведения см. в статье [Service windows for site servers](service-windows.md) (Периоды обслуживания для серверов сайта).

**Запустите средство проверки готовности к установке** .  
Если обновление указано в консоли с состоянием **Доступно**, можно запустить средство проверки готовности независимо от установки обновления. (При установке обновления на сайт средство запустится снова.)

Чтобы запустить средство проверки готовности из консоли, последовательно выберите **Администрирование > Обзор > Облачные службы > Обновления и обслуживание**. Затем щелкните правой кнопкой мыши **пакет обновления Configuration Manager 1702** и выберите пункт **Запустить проверку готовности**.

Дополнительные сведения о запуске и мониторинге проверки готовности см. в разделе **Шаг 3. Перед установкой обновления запустите средство проверки готовности** статьи [Установка обновлений в консоли для Configuration Manager](install-in-console-updates.md).

> [!IMPORTANT]  
> Когда средство проверки готовности запускается в ходе обновления или отдельно, этот процесс обновляет некоторые исходные файлы продукта, которые используются для выполнения задач обслуживания сайта. Поэтому, если вам нужно выполнить задачу обслуживания после проверки готовности, но перед установкой обновления, запустите программу установки Configuration Manager **Setupwpf.exe** из папки CD.Latest на сервере сайта.

**Обновите сайты.**    
Теперь вы готовы начать установку обновления для иерархии. Дополнительные сведения об установке обновления см. в разделе [Установка обновлений в консоли](install-in-console-updates.md#bkmk_install).

Мы рекомендуем назначать установку обновления для каждого сайта на нерабочее время, чтобы процесс установки обновления и его действия по переустановке компонентов сайта и ролей системы сайта как можно меньше влияли на обычные бизнес-операции.

Дополнительные сведения см. в статье [Обновления для Configuration Manager](updates.md).

## <a name="post-update-checklist"></a>Контрольный список после обновления
Изучите список действий, которые нужно выполнить после завершения установки обновления.
1. Убедитесь, что активна межсайтовая репликация. В консоли откройте пункты **Мониторинг** > **Иерархия сайтов** и **Мониторинг** > **Репликация базы данных**, чтобы проверить наличие проблем или убедиться, что связи репликации активны.
2. Убедитесь, что каждый сервер сайта и каждая роль системы сайта обновились до версии 1702. В консоли можно добавить дополнительный столбец **Версия** в отображениях некоторых узлов, например для **сайтов** и **точек распространения**.

   При необходимости роль системы сайта будет автоматически переустановлена для обновления до новой версии. Удаленные системы сайта, обновление которых не прошло успешно, можно попробовать перезагрузить.
3. Перенастройте реплики базы данных для точек управления на первичных сайтах, которые вы отключали перед началом обновления.
4. Перенастройте задачи обслуживания базы данных, которые вы отключали перед началом обновления.
5. Если перед установкой обновления вы настроили подготовку клиента, обновите клиенты согласно составленному плану.