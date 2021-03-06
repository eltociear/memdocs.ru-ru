---
title: Контрольный список для версии 1902
titleSuffix: Configuration Manager
description: См. дополнительные сведения о действиях, которые нужно выполнить перед обновлением до Configuration Manager версии 1902.
ms.date: 04/11/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b87ac054-9b37-4725-a3f3-2340cfb10bff
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 150194be4d7d2fa07fb868e9a5f65f52f3bdd768
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707672"
---
# <a name="checklist-for-installing-update-1902-for-configuration-manager"></a>Контрольный список для установки обновления 1902 для Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Если вы используете текущую ветвь Configuration Manager, обновление иерархии до версии 1902 можно установить из консоли поверх предыдущей версии. <!-- baseline only statement:-->(Так как версия 1902 также доступна как [базовый носитель](updates.md#bkmk_Baselines), вы можете использовать установочный носитель для установки первого сайта новой иерархии.)

Чтобы получить обновление для версии 1902, нужно использовать точку подключения службы на сайте верхнего уровня в иерархии. Роль системы сайта может находиться как в оперативном, так и в автономном режиме. После того как иерархия загрузит пакет обновления от корпорации Майкрософт, его можно будет найти в консоли. В рабочей области **Администрирование** выберите узел **Обновления и обслуживание**.

-   Если обновление имеет состояние **Доступно**, оно готово к установке. Прежде чем установить версию 1902, просмотрите [сведения об установке обновления 1902](#about-installing-update-1902) и [контрольный список](#checklist) настроек, которые нужно выполнить перед началом обновления.

-   Если обновление имеет состояние **Загружается**, которое не меняется, просмотрите файлы **hman.log** и **dmpdownloader.log**, чтобы проверить наличие ошибок.

    -   Файл dmpdownloader.log может означать, что процесс dmpdownloader ожидает окончания определенного интервала перед проверкой на наличие обновлений. Чтобы повторно начать загрузку распространяемых файлов обновления, перезапустите службу **SMS_Executive** на сервере сайта.

    -   Ещё одна распространенная проблема при загрузке возникает, когда настройки прокси-сервера запрещают загрузку с `silverlight.dlservice.microsoft.com`, `download.microsoft.com` и `go.microsoft.com`.

Дополнительные сведения об установке обновлений см. в разделе [Обновления в консоли и обслуживание](updates.md#bkmk_inconsole).

Дополнительные сведения о версиях Current Branch см. в разделе [Базовые и обновленные версии](updates.md#bkmk_Baselines).



## <a name="about-installing-update-1902"></a>Об установке обновления 1902

#### <a name="sites"></a>Сайты
Обновление 1902 устанавливается на сайте верхнего уровня в иерархии. Запустите установку на сайте центра администрирования или на автономном первичном сайте. После установки обновления на сайте верхнего уровня дочерние сайты обновляются в указанном далее порядке.

-   Подчиненные первичные сайты автоматически устанавливают обновление, как только сайт центра администрирования завершит установку обновления. Для управления временем установки обновлений можно использовать периоды обслуживания. Дополнительные сведения см. в статье [Service windows for site servers](service-windows.md) (Периоды обслуживания для серверов сайта).

-   После того как на родительском первичном сайте завершится установка обновления, вручную обновите вторичные сайты через консоль Configuration Manager. Автоматическое обновление серверов вторичных сайтов не поддерживается.

#### <a name="site-system-roles"></a>Роли систем сайта
Если сервер сайта устанавливает обновление, он автоматически обновляет все роли системы сайта. Эти роли доступны на сервере сайта или установлены на удаленных серверах. Перед установкой обновления убедитесь, каждый сервер системы сайта отвечает актуальным предварительным требованиям для новой версии обновления.

#### <a name="configuration-manager-consoles"></a>Консоли Configuration Manager   
При первом использовании консоли Configuration Manager после завершения обновления появится запрос на обновление этой консоли. Можно также запустить программу установки Configuration Manager на компьютере, где размещена консоль, и выбрать параметр для обновления консоли. Обновление для консоли следует устанавливать как можно быстрее. Дополнительные сведения см. в статье [Установка консоли Configuration Manager](../deploy/install/install-consoles.md).

> [!IMPORTANT]  
> Имейте в виду, что после установки обновления на сайте центра администрирования и вплоть до завершения обновлений на всех дочерних первичных сайтах будут существовать следующие ограничения и задержки.    
> - **Обновления клиента** не запускаются. Сюда относится автоматическое обновление клиентов и подготовительных клиентов. Кроме того, невозможно повысить уровень подготовительных клиентов до рабочих клиентов, пока установка обновлений не завершится на всех сайтах. Когда завершится установка обновлений на последнем сайте, начинается обновление клиентов с учетом выбранной вами конфигурации.   
> - Недоступны **новые возможности**, которые вы активировали при обновлении. Это сделано специально, чтобы предотвратить репликацию данных, связанных с такими функциями, на сайт, на котором поддержка этих функций еще не установлена. Новые функции будут доступны для использования, когда обновление завершится на всех основных сайтах.   
> - **Связи репликации** между сайтом центра администрирования и дочерними основными сайтами отображаются как необновленные. В связи с этим состояние установки пакета обновления отображается как завершенное с предупреждением для инициализации репликации мониторинга. В узле мониторинга на консоли отображается статус *Выполняется конфигурация ссылки*.


## <a name="checklist"></a>Контрольный список

#### <a name="all-sites-run-a-supported-version-of-configuration-manager"></a>На всех сайтах выполняется поддерживаемая версия Configuration Manager  
Перед началом установки обновления 1902 на каждом сервере сайта в иерархии должна работать одна и та же версия Configuration Manager. Чтобы обновить версию до 1902, нужно использовать версии 1802, 1806 или 1810.

#### <a name="review-the-status-of-your-product-licensing"></a>Проверка состояния лицензирования продукта 
Для установки этого обновления требуется действующее соглашение Software Assurance (SA) или эквивалентные права по подписке. При обновлении сайта на странице **Лицензирование** предлагается подтвердить **дату истечения срока действия Software Assurance**.

Это необязательное значение. Его можно использовать для напоминания о предстоящем завершении срока действия лицензии. Эта дата отображается при установке последующих обновлений. Возможно, это значение было указано ранее во время работы программы установки или установки обновления. Это значение можно также указать в консоли Configuration Manager. В рабочей области **Администрирование** разверните узел **Конфигурация сайта** и выберите **Сайты**. На ленте щелкните **Параметры иерархии** и перейдите на вкладку **Лицензирование**.

Дополнительные сведения см. в статье [Лицензирование и ветви](../../understand/learn-more-editions.md).

#### <a name="review-microsoft-net-versions"></a>Проверка версий Microsoft .NET 
При установке этого обновления с сайта, если не установлена минимальная требуемая версия .NET Framework 4.5, в Configuration Manager автоматически устанавливается .NET Framework 4.5.2. Если этот необходимый компонент еще не установлен, сайт устанавливает его на каждом сервере, где размещается одна из следующих ролей системы сайта:

-   Точка управления
-   Точка подключения службы
-   Прокси-точка регистрации.
-   Точка регистрации

Этот процесс установки может перевести сервер системы сайта в состояние ожидания перезагрузки и сообщать об ошибках средству просмотра состояния компонентов Configuration Manager. Кроме того, до перезагрузки сервера на нем возможны произвольные сбои приложений .NET.

Дополнительные сведения см. в разделе  [Необходимые компоненты для сайта и системы сайта](../../plan-design/configs/site-and-site-system-prerequisites.md).

#### <a name="review-the-version-of-the-windows-adk-for-windows-10"></a>Проверка версии Windows ADK для Windows 10
Для Configuration Manager версии 1902 должна поддерживаться версия комплекта средств для развертывания и оценки (ADK) для Windows 10. Дополнительные сведения о поддерживаемых версиях Windows ADK см. в разделе [Windows 10 ADK](../../plan-design/configs/support-for-windows-10.md#windows-10-adk). Если вам нужно обновить Windows ADK, сделайте это до начала обновления Configuration Manager. Так вы обеспечите автоматическое обновление загрузочных образов по умолчанию до последней версии Windows PE. После обновления сайта вручную обновите все настраиваемые загрузочные образы.

Если вы обновляете сайт перед обновлением Windows ADK, см. раздел [Обновление точек распространения с использованием образа загрузки](../../../osd/get-started/manage-boot-images.md#update-distribution-points-with-the-boot-image).

#### <a name="review-sql-server-native-client-version"></a>Проверка версии SQL Server Native Client
Необходимо установить минимальную версию SQL Server 2012 Native Client, которая включает поддержку TLS 1.2. Дополнительные сведения см. в статье [Список проверок на наличие необходимых компонентов для Configuration Manager](../deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).

#### <a name="review-the-site-and-hierarchy-status-for-unresolved-issues"></a>Проверка состояния сайта и иерархии на наличие неразрешенных проблем 
Обновление сайта может завершиться неудачей из-за существующих проблем в работе. Перед обновлением сайта решите все проблемы эксплуатации для следующих систем:  
- сервер сайта;  
- Сервер базы данных сайта  
- Удаленные роли системы сайта на других серверах   

Дополнительные сведения см. в статье  [Использование оповещений и системы состояния](use-alerts-and-the-status-system.md).

#### <a name="review-file-and-data-replication-between-sites"></a>Проверка репликации файлов и данных между сайтами   
Убедитесь в том, что репликация файлов и базы данных между сайтами действует и является актуальной. Задержки или невыполненная работа могут помешать бесперебойному, успешному выполнению обновления. Для репликации базы данных можно использовать Replication Link Analyzer, который поможет устранить проблемы перед началом обновления.

Дополнительные сведения см. в разделе [Сведения о Replication Link Analyzer](monitor-replication.md#BKMK_RLA).

#### <a name="install-all-applicable-critical-windows-updates"></a>Установка всех доступных важных обновлений Windows
Перед установкой обновления для Configuration Manager установите все важные обновления операционной системы для каждой соответствующей системы сайта. В число таких серверов входит сервер сайта, сервер базы данных сайта и роли удаленной системы сайта. Если устанавливаемое обновление требует перезагрузки, перезагрузите соответствующие серверы перед началом обновления.

#### <a name="disable-database-replicas-for-management-points-at-primary-sites"></a>Отключение реплик базы данных для точек управления на первичных сайтах   
Configuration Manager не может обновить первичный сайт с включенными репликами баз данных для точек управления. Перед установкой обновления для Configuration Manager отключите репликацию базы данных.

Дополнительные сведения см. в статье [Реплики базы данных для точек управления](../deploy/configure/database-replicas-for-management-points.md).

#### <a name="set-sql-server-alwayson-availability-groups-to-manual-failover"></a>Настройка групп доступности SQL Server AlwaysOn для отработки отказа вручную   
Если вы используете группу доступности, настройте для нее отработку отказа вручную перед запуском установки обновления. После обновления сайта можно восстановить автоматическую отработку отказа. Дополнительные сведения см. в статье  [SQL Server AlwaysOn для базы данных сайта](../deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).

#### <a name="disable-site-maintenance-tasks-at-each-site"></a>Отключение задачи обслуживания сайта на каждом сайте
Перед установкой обновления отключите все задачи обслуживания сайта, которые могут запускаться в то время, когда активен процесс обновления. Ниже перечислены некоторые из этих задач.

-   Резервное копирование сервера сайта
-   Удаление устаревших операций клиента
-   Удаление устаревших данных обнаружения

Если во время установки обновления выполняется задача обслуживания базы данных сайта, то обновление может завершиться сбоем. Прежде чем отключить задачу, запишите ее расписание, чтобы восстановить конфигурацию после установки обновления.

Дополнительные сведения см. в статьях  [Задачи обслуживания](maintenance-tasks.md)  и [Справочник по задачам обслуживания](reference-for-maintenance-tasks.md).

#### <a name="temporarily-stop-any-antivirus-software"></a>Временная остановка всего антивирусного программного обеспечения 
Перед обновлением сайта остановите антивирусное программное обеспечение на серверах Configuration Manager. Антивирусное программное обеспечение может блокировать некоторые обновляемые файлы, что приведет к сбою обновления. <!--SMS.503481--> 

#### <a name="create-a-backup-of-the-site-database"></a>Создание резервной копии базы данных сайта 
Перед обновлением сайта создайте резервную копию базы данных сайта на сайте центра администрирования и первичных сайтах. Ее можно использовать для аварийного восстановления.

Дополнительные сведения см. в статье  [Резервное копирование и восстановление](backup-and-recovery.md).

#### <a name="plan-for-client-piloting"></a>Планирование пилотного развертывания клиента   
При установке обновления, которое изменяет клиент, можно проверить это новое обновление клиента в подготовительной среде, прежде чем развернуть его и обновить активные клиенты. Чтобы воспользоваться этой возможностью, перед началом установки обновления нужно настроить сайт для поддержки автоматического обновления в подготовительной среде.

Дополнительные сведения см. в статьях  [Обновление клиентов](../../clients/manage/upgrade/upgrade-clients.md)  и [Проверка обновления клиента в предварительной коллекции](../../clients/manage/upgrade/test-client-upgrades.md).

#### <a name="plan-to-use-service-windows"></a>Планирование периодов обслуживания   
Используйте периоды обслуживания, чтобы определить период времени для установки обновлений на сервере сайта. Это поможет контролировать время установки обновлений на сайты в иерархии. Дополнительные сведения см. в статье  [Периоды обслуживания для серверов сайта](service-windows.md).

#### <a name="review-supported-extensions"></a>Проверка поддерживаемых расширений
<!--SCCMdocs#587-->
Если вы расширяете возможности Configuration Manager с помощью других продуктов корпорации Майкрософт или ее партнеров, убедитесь в том, что они поддерживают версию 1902. Эту информацию можно получить у поставщика продукта. Например, см. [заметки о выпуске](../../../mdt/release-notes.md) Microsoft Deployment Toolkit.

#### <a name="run-the-setup-prerequisite-checker"></a>Запуск средства проверки готовности к установке   
Если обновление указано в консоли с состоянием **Доступно**, можно запустить средство проверки готовности независимо от установки обновления. (При установке обновления на сайт средство запустится снова.)

Чтобы запустить средство проверки готовности из консоли, перейдите в рабочую область **Администрирование** и выберите узел **Обновления и обслуживание**. Выберите пакет обновления **Configuration Manager 1902** и на ленте щелкните **Запустить проверку на наличие необходимых компонентов**.

Дополнительные сведения см. в подразделе **Шаг 2. Перед установкой обновления запустите средство проверки готовности** раздела [Перед установкой обновлений в консоли](install-in-console-updates.md#bkmk_beforeinstall).

> [!IMPORTANT]  
> Когда средство проверки готовности запускается, этот процесс обновляет некоторые исходные файлы продукта, которые используются для выполнения задач обслуживания сайта. Поэтому, если вам нужно выполнить задачу обслуживания после проверки готовности, но перед установкой обновления, запустите программу установки Configuration Manager  **Setupwpf.exe**  из папки CD.Latest на сервере сайта.

#### <a name="update-sites"></a>Обновление сайтов   
Теперь вы готовы начать установку обновления для иерархии. Дополнительные сведения об установке обновления см. в статье [Установка обновлений в консоли](install-in-console-updates.md#bkmk_install).

Вы можете запланировать установку обновления во внерабочее время. Определите, когда процесс будет оказывать наименьшее влияние на бизнес-операции. Установка обновления и его действия приводят к переустановке компонентов сайта и ролей системы сайта.

Дополнительные сведения см. в статье  [Обновления для Configuration Manager](updates.md).



## <a name="post-update-checklist"></a>Контрольный список действий, выполняемых после обновления

После обновления сайта используйте следующий контрольный список для выполнения типичных задач и настроек.


#### <a name="confirm-version-and-restart-if-necessary"></a>Подтверждение версии и перезапуск (если нужно)
Убедитесь, что каждый сервер сайта и каждая роль системы сайта обновлены до версии 1902. В консоли в рабочей области **Администрирование** добавьте столбец **Версии** в узлы **Сайты** и **Точки распространения**. При необходимости роль системы сайта автоматически переустанавливается для обновления до новой версии. 

Удаленные системы сайта, обновление которых не прошло успешно, можно попробовать перезагрузить. Просмотрите вашу инфраструктуру сайта и убедитесь, что соответствующие серверы сайта и удаленные серверы системы сайта успешно перезапущены. Как правило, серверы сайта перезапускаются, только если Configuration Manager устанавливает .NET в качестве необходимого компонента для роли системы сайта.


#### <a name="confirm-site-to-site-replication-is-active"></a>Убедитесь, что межсайтовая репликация активна
В консоли Configuration Manager перейдите к следующим расположениям, чтобы проверить состояние и активность репликации.  

-   Рабочая область **Мониторинг**, узел **Иерархия сайтов**  

-   Рабочая область **Мониторинг**, узел **Репликация базы данных**  

Дополнительные сведения см. в следующих статьях:  

- [Иерархия мониторов](monitor-hierarchy.md)
- [Монитор репликации](monitor-replication.md)
- [Сведения об анализаторе канала репликации](monitor-replication.md#BKMK_RLA)  


#### <a name="update-configuration-manager-consoles"></a>Обновление консолей Configuration Manager
Обновите все удаленные консоли Configuration Manager до той же версии. Обновить консоль предлагается в следующих случаях:  

-   При открытии консоли.  

-   При переходе на новый узел в консоли.  


#### <a name="reconfigure-database-replicas-for-management-points"></a>Перенастройте реплики баз данных для точек управления
После обновления первичного сайта заново настройте в реплике базы данных точки управления, которые вы удалили перед обновлением сайта. Дополнительные сведения см. в статье [Реплики базы данных для точек управления](../deploy/configure/database-replicas-for-management-points.md).  


#### <a name="reconfigure-any-disabled-maintenance-tasks"></a>Перенастройте все отключенные задачи обслуживания
Если перед установкой обновления вы отключили на сайте [задачи обслуживания](maintenance-tasks.md) базы данных, снова настройте их. используя те же параметры, которые использовались до обновления.  


#### <a name="update-clients"></a>Обновление клиентов
Если перед установкой обновления вы настроили подготовку клиентов, обновите клиенты согласно составленному плану. Дополнительные сведения см. в разделе [Обновление клиентов для компьютеров Windows](../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  


#### <a name="third-party-extensions"></a>Расширения от сторонних производителей
Если используются расширения Configuration Manager, обновите их до последней версии для  включения поддержки Configuration Manager версии 1902. 


#### <a name="update-custom-boot-images-and-media"></a>Обновление настраиваемых образов загрузки и носителей
<!--SCCMDocs issue 775-->

Используйте действие **Обновить точки распространения** для всех используемых образов загрузки — как стандартных, так и настраиваемых. Это действие гарантирует, что клиенты могут использовать последнюю версию. Даже если отсутствует новая версия Windows ADK, при обновлении могут изменяться компоненты клиента Configuration Manager. Если вы не обновите образы загрузки и носители, развертывания последовательности задач на устройствах могут завершиться сбоем. 

При обновлении сайта Configuration Manager автоматически обновляет *стандартные* образы загрузки. Но обновленное содержимое не распространяется в точки распространения автоматически. Примените действие **Обновить точки распространения** для конкретных образов загрузки, когда вы будете готовы распространить это содержимое в сети организации. 

Завершив обновление сайта, вручную обновите все *настраиваемые* образы загрузки. Это действие помещает в образ загрузки последние версии компонентов клиента, при необходимости обновляет его до текущей версии Windows PE, а затем публикует содержимое в точки распространения. 

См. дополнительные сведения об [обновлении точек распространения с помощью загрузочного образа](../../../osd/get-started/manage-boot-images.md#update-distribution-points-with-the-boot-image). 
