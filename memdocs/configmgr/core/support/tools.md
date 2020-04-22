---
title: Средства Configuration Manager
titleSuffix: Configuration Manager
description: Сведения о средствах для управления инфраструктурой Configuration Manager и устранения неполадок с ней.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 395403dc-6997-4415-93fd-6b1eeb6ba31a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 06e308a54ee9636a7781667823e7b7f98ae6f25c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701272"
---
# <a name="configuration-manager-tools"></a>Средства Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

В число средств Configuration Manager входят [клиентские](#client-tools) и [серверные инструменты](#server-tools). Используйте эти средства для поддержки инфраструктуры Configuration Manager и устранения неполадок с ней.

Начиная с Configuration Manager версии 1806 эти средства содержатся в папке `CD.Latest\SMSSETUP\Tools` на сервере сайта. Больше никакой установки не требуется.<!--1357145--> Используйте эти версии средств с Configuration Manager версии 1806 и более поздними версиями.

С этими средствами работают все операционные системы Windows, указанные как поддерживаемые клиенты в разделе [Поддерживаемые операционные системы для клиентов и устройств](https://docs.microsoft.com/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices).

> [!Note]  
> [System Center 2012 R2 Configuration Manager Toolkit](https://www.microsoft.com/download/details.aspx?id=50012) по-прежнему доступен из Центра загрузки Майкрософт. При работе с Configuration Manager версии 1806 и более поздними версиями используйте версии этих средств в папке CD.Latest на сервере сайта. Некоторые средства были ранее доступны в наборе средств, но не включены в версию 1806. Эти устаревшие средства больше не поддерживаются.


## <a name="client-tools"></a>Клиентские инструменты

Эти средства находятся во вложенной папке `ClientTools`:

- [CMTrace](cmtrace.md): просмотр, мониторинг и анализ файлов журналов Configuration Manager  

- [Client Spy](clispy.md): устранение неполадок, связанных с распространением, инвентаризацией и контролем использования программного обеспечения

- [Средство наблюдения за развертыванием](deployment-monitoring-tool.md): устранение неполадок с приложениями, обновлениями и развертываниями базовых шаблонов  

- [Средство Policy Spy](policy-spy.md): просмотр назначений политик  

- [Средство Power Viewer](power-viewer-tool.md): просмотр состояния функции управления питанием  

- [Средство для работы с расписанием отправок](send-schedule-tool.md): запуск расписаний и оценок конфигурационных баз  

> [!Note]  
> В папке `ClientTools` также находится файл Microsoft.Diagnostics.Tracing.EventSource.dll. Эта библиотека требуется нескольким клиентским средствам. Ее нельзя использовать напрямую.  


## <a name="server-tools"></a>Серверные инструменты

Эти средства находятся во вложенной папке `ServerTools`:

- [Диспетчер очередей заданий DP](dp-job-manager.md): устраняет неполадки с заданием распространения содержимого в точках распространения  

- [Средство просмотра оценки коллекции](ceviewer.md): просмотр сведений об оценке коллекции  

- [Проводник библиотеки содержимого](content-library-explorer.md): просмотр содержимого хранилища отдельных экземпляров библиотеки содержимого  

- [Перенос содержимого библиотеки](content-library-transfer.md): перенос содержимого библиотеки между дисками  

- [Средство владения содержимым](content-ownership-tool.md): изменение права собственности на потерянные пакеты. Эти пакеты существуют на сайте без собственного сервера сайта.

- [Средство ролевого администрирования и аудита](rbaviewer.md): помогает администраторам настроить роли для аудита  

- [Средство формирования сводных данных по контролю использования](run-meter-summ.md): запуск задачи формирования сводных данных по контролю использования программных продуктов и анализу данных отслеживания использования

> [!Note]  
> Папка ServerTools также содержит следующие файлы:
>
> - AdminUI.WqlQueryEngine.dll;
> - Microsoft.ConfigurationManagement.ManagementProvider.dll;
> - Microsoft.Diagnostics.Tracing.EventSource.dll.
>
> Эти библиотеки требуются нескольким серверным средствам. Их нельзя использовать напрямую.  

## <a name="other-tools-and-toolkits"></a>Другие средства и наборы инструментов

- [Центр поддержки](support-center.md). Собирайте сведения от клиентов для облегчения анализа при устранении неполадок.

    Начиная с версии 1906, **OneTrace** является новым средством просмотра журналов для центра поддержки. Оно работает аналогично CMTrace, но обладает некоторыми усовершенствованиями. Дополнительные сведения о средстве OneTrace для центра поддержки см. [здесь](support-center-onetrace.md).

- [Расширение и миграция локального сайта в Microsoft Azure](azure-migration-tool.md): позволяет программно создавать виртуальные машины Azure для Configuration Manager. <!--3556022--> 

- [Средство очистки библиотеки содержимого](../plan-design/hierarchy/content-library-cleanup-tool.md): используйте **ContentLibraryCleanup.exe** в `CD.Latest\SMSSETUP\TOOLS\ContentLibraryCleanup` для удаления потерянного содержимого из точки распространения.  

- [Средство обслуживания иерархии](../servers/manage/hierarchy-maintenance-tool-preinst.exe.md): используйте **Preinst.exe** в общей папке `\<SiteServerName>\SMS_<SiteCode>\bin\X64\00000409` на сервере сайта для передачи команд компоненту диспетчера иерархии.  

- [Средство сброса обновлений](../servers/manage/update-reset-tool.md): используйте **CMUpdateReset.exe** в папке `CD.Latest\SMSSETUP\TOOLS\CMUpdateReset` для устранения проблем с загрузкой или репликацией, возникающих при обновлениях в консоли.  

- [Средство подключения службы](../servers/manage/hierarchy-maintenance-tool-preinst.exe.md): используйте **ServiceConnectionTool.exe** в папке `CD.Latest\SMSSETUP\TOOLS\ServiceConnectionTool`, чтобы поддерживать актуальное состояние сайта, когда точка подключения службы находится в автономном режиме.   

- [Microsoft Deployment Toolkit (MDT)](../../mdt/use-the-mdt.md). Коллекция средств, процессов и руководств для автоматизации развертывания рабочих столов и серверных ОС.

- [System Center Updates Publisher (SCUP)](../../sum/tools/updates-publisher.md). Автономное средство для администрирования и импорта пользовательских обновлений программного обеспечения.

- [Диспетчер преобразования пакетов](../../apps/pcm/package-conversion-manager.md). Преобразовывайте устаревшие пакеты в приложения.
