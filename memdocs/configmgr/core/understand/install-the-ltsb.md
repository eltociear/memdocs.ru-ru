---
title: 'Установка сайта с помощью базового носителя версии 1606 '
titleSuffix: Configuration Manager
description: Установка LTSB для System Center Configuration Manager или обновление до этой версии.
ms.date: 09/06/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f4f9a5fd-f573-4b99-ad93-b2c76812e922
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7d70611aff329f48c8223a47dfa238e5a4559972
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707012"
---
# <a name="install-and-upgrade-with-the-version-1606-baseline-media"></a>Установка и обновление с помощью базового носителя версии 1606

*Область применения: System Center Configuration Manager (Long-Term Servicing Branch)*

При запуске программы установки с базового носителя версии 1606 для Configuration Manager вы можете установить сайт Long Term Servicing Branch решения System Center Configuration Manager.

Базовый носитель доступен на DVD-диске в составе выпуска Microsoft System Center 2016 или System Center Configuration Manager (Long-Term Servicing Branch) 1606. Дополнительные сведения о базовых носителях см. в разделе [Базовые и обновленные версии](../servers/manage/updates.md#bkmk_Baselines).


При использовании базового носителя версии 1606 устанавливается следующий сайт (или производится обновление до этой версии):
- *Сайт Current Branch*, который эквивалентен сайту, который был изначально установлен с помощью базового носителя версии 1511, а затем обновлен до версии 1606 с пакетом исправлений 1606 (KB3186654).
- *Сайт LTSB*, который эквивалентен сайту Current Branch версии 1606 с пакетом исправлений 1606 (KB3186654). Базовый носитель уже содержит пакет исправлений.  Однако версия LTSB поддерживает не все функции и возможности, доступные в Current Branch. Подробные сведения см. в разделе [Общие сведения о версии System Center Configuration Manager (Long-Term Servicing Branch)](introduction-to-the-ltsb.md).

Если вы не знакомы с различными ветвями Configuration Manager, см. раздел [Выбор ветви Configuration Manager](which-branch-should-i-use.md).




## <a name="changes-to-setup-with-the-1606-baseline-media"></a>Изменения в программе установки на базовом носителе версии 1606
На базовом носителе версии 1606 в программу установки Configuration Manager были внесены перечисленные ниже изменения.

### <a name="branch-and-edition"></a>Ветвь и выпуск
При запуске программы установки теперь выводится страница лицензирования, на которой можно выбрать ветвь Configuration Manager, которую нужно установить. Вы можете выбрать Current Branch или LTSB в качестве лицензионной установки или выбрать ознакомительный выпуск Current Branch для установки без лицензии.

Дополнительные сведения см. в разделе [Лицензирование и ветви в Configuration Manager](learn-more-editions.md).

### <a name="software-assurance-expiration"></a>Истечение срока действия Software Assurance
Во время установки можно ввести **дату истечения срока действия Software Assurance**. Это необязательное значение, которое можно указать для напоминания.

> [!NOTE]
> Майкрософт не проверяет указанную дату окончания срока действия и не будет использовать ее для проверки лицензии.  Вы сами можете использовать эти сведения в качестве напоминания об окончании срока действия. Это удобно, так как Configuration Manager периодически проверяет наличие новых обновлений программного обеспечения, предлагаемых через Интернет, поэтому ваши лицензии в рамках Software Assurance должны иметь соответствующее состояние для использования этих дополнительных обновлений.    

- Вы можете указать значение даты на странице **Ключ продукта** мастера установки при запуске программы установки с базового носителя Configuration Manager версии 1606.
- Эту дату также можно указать, выбрав **Свойства параметров иерархии** > **Лицензирование** в консоли Configuration Manager

Дополнительные сведения см. в подразделе "Соглашения Software Assurance" раздела [Лицензирование и ветви в Configuration Manager](learn-more-editions.md).


### <a name="additional-pre-upgrade-configurations"></a>Дополнительные настройки перед обновлением
Перед тем как начинать обновление System Center 2012 Configuration Manager до версии LTSB, необходимо выполнить указанные ниже дополнительные действия в рамках контрольного списка перед обновлением.  
Удалите роли системы сайта, которые не поддерживаются LTSB:
- точка синхронизации каталога аналитики активов;
- Соединитель Microsoft Intune
- Облачные точки распространения

Дополнительные сведения см. в разделе [Обновление до Configuration Manager](../servers/deploy/install/upgrade-to-configuration-manager.md).


### <a name="new-scripted-installation-options"></a>Новые параметры установки с помощью скрипта
Базовый носитель версии 1606 поддерживает новый ключ файла скрипта для автоматической установки нового сайта верхнего уровня. Он относится к установке нового автономного первичного сайта или добавлению сайта центра администрирования в рамках сценария расширения иерархии.

При использовании автоматического скрипта для установки лицензированной ветви необходимо добавить указанный ниже раздел, имена ключей и значения в раздел Options скрипта. Использовать эти значения в скрипте для установки ознакомительного выпуска Current Branch не нужно.  

 **SABranchOptions**
- **Имя ключа: SAActive**
  - Значения: 0 или 1.  
  - Подробные сведения:  значение 0 соответствует установке ознакомительного выпуска Current Branch без лицензии, а значение 1 — установке лицензированного выпуска.   

- **CurrentBranch**
  - Значения: 0 или 1.  
  - Подробные сведения:  значение 0 соответствует установке Long-Term Servicing Branch, а значение 1 — установке Current Branch.  

Например, чтобы установить лицензированный выпуск Current Branch, используйте следующие значения:

**Имя ключа: SABranchOptions**
- **SAActive = 1**
- **CurrentBranch = 1**


> [!IMPORTANT]  
> Раздел **SABranchOptions** работает только с программой установки с базового носителя. Он не применяется, если программа установки запускается из папки CD.Latest на сайте, которую вы установили ранее с помощью базового носителя версии 1606.
>
> **SABranchOptions** не применяется при обновлении с System Center 2012 Configuration Manager с помощью скрипта и всегда приводит к установке Current Branch.

Дополнительные сведения см. в разделе [Установка сайтов Configuration Manager с помощью командной строки](../servers/deploy/install/use-a-command-line-to-install-sites.md).


## <a name="install-a-new-site"></a>Установка нового сайта
При использовании базового носителя версии 1606 для установки нового сайта любой ветви выполните процедуры планирования, подготовки и установки, описанные в разделе [Установка сайтов Configuration Manager](../servers/deploy/install/installing-sites.md), с учетом приведенных ниже рекомендаций касательно программы установки.

- Во время установки необходимо выбрать ветвь Configuration Manager, которую нужно установить, и можно указать сведения о соглашении Software Assurance.
- На всех сайтах в одной иерархии должна использоваться одна ветвь. Иерархия с версиями LTSB и Current Branch на разных сайтах не поддерживается.
- Новая установка с помощью скрипта. Дополнительные сведения см. в подразделе "Новые параметры установки с помощью скрипта" ранее в этом разделе.

## <a name="expand-a-stand-alone-primary-site"></a>Развертывание автономного первичного сайта
Вы можете развернуть автономный первичный сайт LTSB.  Процесс не отличается от используемого для развертывания сайта Current Branch, за одним исключением.

- При установке нового сайта центра администрирования необходимо использовать программу установки с исходного носителя, который вы применяли для установки сайта LTSB. Запускать программу установки из папки CD.Latest в этом сценарии нельзя.

Дополнительные сведения о расширении сайта см. в подразделе "Расширение автономного первичного сайта" раздела [Установка сайта с помощью мастера установки](../servers/deploy/install/use-the-setup-wizard-to-install-sites.md).

## <a name="upgrade-from-system-center-2012-configuration-manager"></a>Обновление с версии System Center 2012 Configuration Manager
При обновлении с версии System Center 2012 Configuration Manager выполните процедуры планирования, подготовки и обновления сайта, описанные в разделе [Обновление до Configuration Manager](../servers/deploy/install/upgrade-to-configuration-manager.md), с учетом указанных ниже изменений.

**Обновление до Current Branch**
- Во время установки необходимо выбрать Current Branch и можно указать сведения о соглашении Software Assurance.
- Новая установка с помощью скрипта. Дополнительные сведения см. в подразделе "Новые параметры установки с помощью скрипта" ранее в этом разделе.

**Обновление до LTSB**  
- Необходимо выполнить дополнительные действия из контрольного списка перед обновлением.
- Во время установки необходимо выбрать LTSB и можно указать сведения о соглашении Software Assurance.
- Можно обновить только сайт System Center 2012 Configuration Manager с пакетом обновления 1 (SP1), System Center 2012 Configuration Manager с пакетом обновления 2 (SP2), System Center 2012 R2 Configuration Manager с пакетом обновления 1 (SP1) или System Center 2012 R2 Configuration Manager без пакета обновления.

### <a name="in-place-upgrade-paths-for-the-1606-baseline-media"></a>Варианты обновления на месте для базового носителя версии 1606
С помощью базового носителя версии 1606 можно обновить следующие лицензированные выпуски Configuration Manager.
- System Center 2012 R2 Configuration Manager с пакетом обновления 1 (SP1).
- System Center 2012 R2 Configuration Manager без пакета обновления (необходимо использовать базовый носитель для версии 1606, выпущенный 15 декабря 2016 г.);
- System Center 2012 Configuration Manager с пакетом обновления 2 (SP2);
- System Center 2012 Configuration Manager с пакетом обновления 1 (SP1) (необходимо использовать базовый носитель для версии 1606, выпущенный 15 декабря 2016 г.).


С помощью этого носителя можно также обновить ознакомительный выпуск Current Branch без лицензии до полной лицензированной версии Current Branch.

Этот носитель не поддерживает обновление следующих версий:
- другие версии System Center 2012 Configuration Manager;
- Configuration Manager 2007 или более ранней версии;
- установка версии-кандидата Configuration Manager.

## <a name="about-the-cdlatest-folder-and-the-ltsb"></a>Сведения о папке CD.Latest и LTSB
Ниже приведены ограничения, касающиеся использования носителя, который Configuration Manager создает в папке CD.Latest на сервере сайта. К сайтам с выпуском LTSB применяются указанные ниже ограничения.

Носитель в папке CD.Latest можно использовать в следующих целях:
- восстановление сайта;
- обслуживание сайта;
- установка дополнительных подчиненных первичных сайтов.

Носитель в папке CD.Latest нельзя использовать в следующих целях:  
- установка сайта центра администрирования в рамках сценария расширения сайта.

Дополнительные сведения см. в разделе [Папка CD.Latest](../servers/manage/the-cd.latest-folder.md).

## <a name="backup-recovery-and-site-maintenance-for-the-ltsb"></a>Резервное копирование, восстановление и обслуживание сайта LTSB
Для резервного копирования, восстановления и обслуживания сайта LTSB используйте указания и процедуры, приведенные в разделе [Резервное копирование и восстановление в Configuration Manager](../servers/manage/backup-and-recovery.md).  

Используйте программу установки Configuration Manager из папки CD.Latest в резервной копии сайта LTSB.