---
title: Общие сведения о LTSB
titleSuffix: Configuration Manager
description: Дополнительные сведения о Long-Term Servicing Branch в Configuration Manager.
ms.date: 08/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 694bc29f-a7fd-4e06-815a-1a9c5e9ac563
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: eda58982094860ccf075bcd2d1d8ed9e3d3bb2df
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706922"
---
# <a name="introduction-to-the-long-term-servicing-branch-of-configuration-manager"></a>Общие сведения о Long-Term Servicing Branch в Configuration Manager

*Применимо к: System Center Configuration Manager (Long-Term Servicing Branch)*

Configuration Manager (Long-Term Servicing Branch) является отдельной ветвью, которая разработана в качестве варианта установки, доступного для всех клиентов. Однако этот вариант предназначен только для клиентов, у которых истек срок действия соглашения Software Assurance (SA) или аналогичных прав по подписке Configuration Manager.

С учетом Configuration Manager версии 1606 возможности Long-Term Servicing Branch (LTSB) ограничены по сравнению с Configuration Manager (Current Branch).

> [!TIP]   
> Configuration Manager (LTSB) не связан с вариантом System Center (Long-Term Servicing Channel). Дополнительные сведения см. в статье [Overview of System Center release options](https://docs.microsoft.com/system-center/ltsc-and-sac-overview) (Обзор вариантов выпуска System Center).

## <a name="features-that-arent-available"></a>Недоступные функции

Configuration Manager (Current Branch) поддерживает следующие возможности, недоступные в LTSB:

- Обновления в консоли, добавляющие новые функции и улучшения.
- Поддержка недавно выпущенных операционных систем, которые будут использоваться в качестве серверов сайта и клиентов.
- локальное управление мобильными устройствами (MDM).
- Панель мониторинга обслуживания Windows 10 и планы обслуживания, включая поддержку последних версий Windows 10.  
- Поддержка будущих выпусков Windows Server и Windows 10 LTSB.
- Аналитика активов
- Облачные точки распространения
- Использование Exchange Online как соединителя Exchange.    

Хотя поддержка для этих функций не включена в LTSB, некоторые функции остаются видимыми в консоли Configuration Manager, однако они неактивны.

Интеграции с облаком, а также любые функции, входящие в Configuration Manager (Current Branch) версии 1610 или более поздней, недоступны для LTSB. Эти функции включают в себя, помимо прочего, следующие:<!--SCCMDocs#1823-->

- Совместное управление
- Аналитика компьютеров
- Шлюз управления облаком
- интеграция с Azure Active Directory;
- приложения, приобретенные в Microsoft Store для бизнеса.

## <a name="find-ltsb-documentation"></a>Поиск документации по LTSB

Ветвь LTSB основана на версии Current Branch 1606. Используйте [документацию по Current Branch](https://docs.microsoft.com/sccm/) с учетом предупреждений и ограничений, относящихся к LTSB. Эти предупреждения и ограничения указаны в следующих статьях:

- [Установка и обновление с помощью базового носителя версии 1606 для System Center Configuration Manager](install-the-ltsb.md)
- [Обновление Long-Term Servicing Branch до Current Branch](convert-to-current-branch.md)
- [Поддерживаемые конфигурации для System Center Configuration Manager (Long-Term Servicing Branch)](supported-configurations-for-ltsb.md)
- [Управление ветвью Configuration Manager (Long-Term Servicing Branch)](manage-the-ltsb.md)

При просмотре документации по Current Branch для LTSB примите во внимание, что сведения о версии 1606 или более ранней также применяются к LTSB. Функции или сведения, внесенные в версию 1610 или более позднюю, не поддерживаются LTSB.

## <a name="licensing-overview-for-the-ltsb"></a>Общие сведения о лицензировании LTSB   

Клиенты с действующим соглашением Software Assurance (SA) для лицензий Configuration Manager или с эквивалентными правами по подписке с 1 октября 2016 г. имеют право на использование выпуска Configuration Manager версии 1606 за октябрь 2016 г. Клиенты с правами на Configuration Manager, действительными на 1 октября 2016 г. или после этой даты, могут выбрать один из двух вариантов лицензирования после установки: Current Branch и Long-Term Servicing Branch (LTSB).

Клиенты, имеющие бессрочные права на System Center Configuration Manager или срок действия SA или подписки которых истекает после 1 октября, могут установить версию System Center Configuration Manager LTSB, которая является текущей на момент истечения срока действия соглашения.

Дополнительные сведения об этих лицензиях см. на странице со [всеми условиями в отношении продуктов, приобретаемых в рамках программ корпоративного лицензирования Майкрософт](https://go.microsoft.com/fwlink/?LinkId=800052).

Дополнительные сведения о лицензировании ветвей Configuration Manager см. в статье [Лицензирование и ветви в System Center Configuration Manager](learn-more-editions.md).

## <a name="next-steps"></a>Дальнейшие шаги

Если вы решили, что Configuration Manager LTSB — это нужная ветвь для вашей среды, [установите новый сайт LTSB](install-the-ltsb.md#install-a-new-site) как часть новой иерархи или [обновите сайт System Center 2012 Configuration Manager](install-the-ltsb.md#upgrade-from-system-center-2012-configuration-manager) и иерархию.
