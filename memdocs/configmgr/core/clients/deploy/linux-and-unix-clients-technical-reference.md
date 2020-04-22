---
title: Команды и службы компонентов клиента UNIX и Linux
titleSuffix: Configuration Manager
description: Узнайте о службах компонентов и командах для клиентов Linux и UNIX в Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e5a8c79f-5791-49c5-8055-086d742e5559
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: de564595ce51a336b5f11d4050928fa812269601
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693892"
---
# <a name="linux-and-unix-clients-component-services-and-commands-for-configuration-manager"></a>Команды и службы компонентов клиента UNIX и Linux в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

> [!Important]  
> Начиная с версии 1902, Configuration Manager не поддерживает клиенты Linux и UNIX. 
> 
> Вы можете управлять серверами Linux с помощью портала управления Microsoft Azure. Решения Azure располагают расширенной поддержкой Linux, которая в большинстве случаев превышает функциональные возможности Configuration Manager, включая полное управление исправлениями для Linux.


 В следующей таблице приведены службы компонентов клиента Configuration Manager для Linux и UNIX.  

|Имя файла|Дополнительные сведения|  
|---------------|----------------------|  
|ccmexec.bin|Эта служба похожа на службу ccmexc на клиентском компьютере под управлением Windows. Она отвечает за все связи с ролями системы сайта Configuration Manager, а также взаимодействует со службой omiserver.bin для сбора данных инвентаризации оборудования с локального компьютера.<br /><br /> Чтобы получить список поддерживаемых аргументов командной строки, выполните `ccmexec -h`.|  
|omiserver.bin|Эта служба является CIM-сервером. CIM-сервер предоставляет платформу для подключаемых программных модулей, которые называются поставщиками. Поставщики взаимодействуют с ресурсами компьютеров Linux и UNIX и собирают данные инвентаризации оборудования. Например **процесс поставщика** для Linux компьютер собирает данные, связанные с процессами операционной системы Linux.|  

 Следующие команды список таблиц, которые можно использовать для запуска, остановить или перезапустить службы клиента (ccmexec.bin и omiserver.bin) на каждой версии Linux или UNIX. При запуске или остановке службы ccmexec также происходит запуск или остановка службы omiserver.  

|Операционная система|Команды|  
|----------------------|--------------|  
|Universal Agent<br /><br /> RHEL 4 и SLES 9|Начало: `/etc/init d/ccmexecd start`<br /><br /> Остановка: `/etc/init d/ccmexecd stop`<br /><br /> Перезапуск: `/etc/init d/ccmexecd restart`|  
|Solaris 9|Начало: `/etc/init d/ccmexecd start`<br /><br /> Остановка: `/etc/init d/ccmexecd stop`<br /><br /> Перезапуск: `/etc/init d/ccmexecd restart`|  
|Solaris 10|Запуск:<br /><br /> `svcadm enable -s svc:/application/management/omiserver`<br /><br /> `svcadm enable -s svc:/application/management/ccmexecd`<br /><br /> Остановка:<br /><br /> `svcadm disable -s svc:/application/management/ccmexecd`<br /><br /> `svcadm disable -s svc:/application/management/omiserver`|  
|Solaris 11|Запуск:<br /><br /> `svcadm enable -s svc:/application/management/omiserver`<br /><br /> `svcadm enable -s svc:/application/management/ccmexecd`<br /><br /> Остановка:<br /><br /> `svcadm disable -s svc:/application/management/ccmexecd`<br /><br /> `svcadm disable -s svc:/application/management/omiserver`|  
|AIX|Запуск:<br /><br /> `startsrc -s omiserver`<br /><br /> `startsrc -s ccmexec`<br /><br /> Остановка:<br /><br /> `stopsrc -s ccmexec`<br /><br /> `stopsrc -s omiserver`|  
|HP-UX|Начало: `/sbin/init.d/ccmexecd start`<br /><br /> Остановка: `/sbin/init.d/ccmexecd stop`<br /><br /> Перезапуск: `/sbin/init.d/ccmexecd restart`|  
