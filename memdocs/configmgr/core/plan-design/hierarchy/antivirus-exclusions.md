---
title: Исключения антивирусной программы
titleSuffix: Configuration Manager
description: Узнайте о рекомендуемых исключениях антивирусной программы, которые можно использовать при устранении возможных проблем.
ms.date: 10/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: deb470e3-6f6b-4ccf-b3d8-1598d79d3490
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: df951bfb44313cfec8dacb8c0df34abb7beb0c56
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703742"
---
# <a name="recommended-antivirus-exclusions-for-configuration-manager"></a>Рекомендуемые исключения антивирусной программы для Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Эта статья содержит рекомендации для администраторов. Эти сведения помогут определить причину потенциальной нестабильной работы компьютера с поддерживаемой версией серверов сайта, систем сайта и клиентов Configuration Manager при их совместном использовании с антивирусной программой.

> [!IMPORTANT]
>
> - Рекомендуем временно применить эти процедуры, чтобы определить состояние системы. Если приведенные в этой статье рекомендации помогли повысить уровень производительности или стабильности системы, обратитесь к поставщику антивирусной программы за инструкциями или ее обновленной версией.
> - Из этой статьи вы узнаете, как понизить уровень ограничений параметров безопасности или временно отключить функции защиты на компьютере. Эти изменения помогут определить характер конкретной проблемы. Прежде чем вносить изменения, рекомендуем оценить риски, связанные с реализацией этого обходного пути в конкретной среде.

## <a name="possible-symptoms"></a>Возможные симптомы 

Антивирусная защита в реальном времени может вызвать множество проблем на серверах сайта, в системах сайта и клиентах Configuration Manager.

Вот неполный список возможных симптомов:

- Компоненты системы удаленного сайта не установлены. SiteComp.log, Distmgr.log, hman.log, или другие файлы журналов Configuration Manager могут содержать ошибки, например ошибку 80070005.
- Не удается принудительно установить клиент Configuration Manager.
- Неточные или устаревшие данные инвентаризации клиента либо их отсутствие.
- Невыполненная работа в папках *Install_Directory*\Program Files\Microsoft Configuration Manager\Inboxes.
- В центр программного обеспечения не поступают данные от развернутого программного обеспечения в клиентских системах, или же он не запускается. Кроме того, файл CCMRepair.log может содержать примерно такие сообщения об ошибках:

  > Database verification failed with result: 0x80004005 but DB: C:\Windows\CCM\filename.sdf could be opened, skipping DB repair (Произошел сбой проверки базы данных с результатом 0x80004005, но файл базы данных C:\Windows\CCM\имя_файла.sdf можно открыть, пропустив восстановление базы данных).

- Не удается установить программное обеспечение, развернутое в клиентах.
- Неточные данные о соответствии для развертываний программного обеспечения.

## <a name="exclusions"></a>Исключения

Чтобы предотвратить такие проблемы, рекомендуем реализовать следующие исключения для защиты в режиме реального времени:

### <a name="default-installation-folders"></a>Папки установки по умолчанию

|  |  |
| - | - |
|*Папка установки ConfigMgr*  |  %ProgramFiles%\Microsoft Configuration Manager  |  
|*Папка установки пакета управления*  |%ProgramFiles%\SMS_CCM  |  
|*Папка установки клиента*  |%Windir%\CCM  |  

### <a name="folder-exclusions-for-site-servers"></a>Исключения папок для серверов сайта

- *Папка установки ConfigMgr*\Inboxes
- *Папка установки ConfigMgr*\Logs
- *Папка установки ConfigMgr*\EasySetupPayload

### <a name="folder-exclusions-for-site-systems"></a>Исключения папок для систем сайта

- Точки управления
  - *Папка установки пакета управления*\ServiceData
  - Один из следующих вариантов:
    - *папка установки ConfigMgr*\MP\OUTBOXES;
    - *установочный диск*\SMS\MP\OUTBOXES.
- Точки распространения
  - *Папка установки клиента*\ServiceData
  - *ContentLib_Drive*\SMS_DP$
  - *ContentLib_Drive*\SMSPKG*Drive_Letter*$
  - *ContentLib_Drive*\SMSPKG
  - *ContentLib_Drive*\SMSPKGSIG
  - *ContentLib_Drive*\SMSSIG$
- Серверы базы данных сайта
  - [Выбор антивирусной программы для запуска на компьютерах под управлением SQL Server](https://support.microsoft.com/en-us/help/309422)

### <a name="folder-exclusions-for-clients"></a>Исключения папок для клиентов

- *Папка установки клиента*\\\*.sdf
- *Папка установки клиента*\ServiceData
- C:\Windows\CCMCache
- C:\Windows\CCMSetup
- *Папка установки клиента*\Logs

### <a name="file-exclusions-for-mps"></a>Исключения файлов для пакетов управления

- POL00000.pol в
  - *папке установки пакета управления*\PolReqStaging

### <a name="process-exclusions"></a>Исключения процессов

Исключения процессов необходимы, только если агрессивные антивирусные программы определяют файлы программ (EXE-файлы) Configuration Manager как процессы с высоким уровнем риска.

- *Папка установки ConfigMgr*\bin\64\Smsexec.exe
- Один из следующих процессов:
  - *Папка установки клиента*\Ccmexec.exe
  - *Папка установки пакета управления*\Ccmexec.exe
- *Папка установки клиента*\CmRcService.exe (на стороне клиента)
- *Папка установки ConfigMgr*\bin\64\Sitecomp.exe
- *Папка установки ConfigMgr*\bin\64\Smswriter.exe
- *Папка установки ConfigMgr*\bin\64\Smssqlbkup.exe или SMS_*SQLFQDN*\bin\x64\Smssqlbkup.exe
- *Папка установки ConfigMgr*\bin\64\Cmupdate.exe
- *Папка установки клиента*\Ccmrepair.exe (на стороне клиента)
- %*windir*%\CCMSetup\Ccmsetup.exe (на стороне клиента)

## <a name="next-steps"></a>Дальнейшие шаги

Дополнительные сведения о конкретных ограничениях антивирусных программ см. в следующих статьях:

[Статья об исключениях антивирусных программ Configuration Manager (Current Branch) в блоге ведущих специалистов по эксплуатации System Center](https://blogs.technet.microsoft.com/systemcenterpfe/2017/05/24/configuration-manager-current-branch-antivirus-update/)

[Обновленные исключения антивирусных программ для System Center 2012 Configuration Manager с дополнительными сведениями об OSD и образах загрузки](https://blogs.technet.microsoft.com/systemcenterpfe/2013/01/11/updated-system-center-2012-configuration-manager-antivirus-exclusions-with-more-details-on-osd-and-boot-images-etc/)

[Выбор антивирусной программы для запуска на компьютерах под управлением SQL Server](https://support.microsoft.com/en-us/help/309422/how-to-choose-antivirus-software-to-run-on-computers-that-are-running-sql-server)

[Рекомендации по проверке компьютеров с поддерживаемыми версиями Windows, используемых на крупных предприятиях, на наличие вирусов](https://support.microsoft.com/en-us/help/822158/virus-scanning-recommendations-for-enterprise-computers-that-are-running-currently-supported-versions-of-windows)
