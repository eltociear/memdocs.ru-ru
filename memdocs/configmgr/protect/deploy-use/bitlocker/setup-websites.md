---
title: Настройка порталов BitLocker
titleSuffix: Configuration Manager
description: Установка компонентов управления BitLocker для портала самообслуживания и веб-сайт администрирования и мониторинга
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 1cd8ac9f-b7ba-4cf4-8cd2-d548b0d6b1df
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: cbd7c516515718cca96bff9b1715233964cb2aa5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81699632"
---
# <a name="set-up-bitlocker-portals"></a>Настройка порталов BitLocker

*Область применения: Configuration Manager (Current Branch)*

<!--3601034-->

Чтобы использовать следующие компоненты управления BitLocker в Configuration Manager, необходимо сначала установить их:

- Портал самообслуживания для пользователей
- Веб-сайт администрирования и мониторинга (портал службы технической поддержки)

Вы можете установить порталы на существующий сервер сайта с IIS или использовать для их размещения автономный веб-сервер.

> [!NOTE]
> Установите только портал самообслуживания и веб-сайт администрирования и мониторинга с базой данных первичного сайта. В иерархии установите эти веб-сайты для каждого первичного сайта.

Перед началом работы убедитесь, что для этих компонентов выполнены все [необходимые условия](../../plan-design/bitlocker-management.md#prerequisites).

## <a name="script-usage"></a>Использование скрипта

Этот процесс использует скрипт PowerShell, MBAMWebSiteInstaller.ps1, для установки этих компонентов на веб-сервере. Он принимает следующие параметры:

- `-SqlServerName <ServerName>` (обязательно): Полное доменное имя сервера базы данных первичного сайта.

- `-SqlInstanceName <InstanceName>`: Имя экземпляра SQL Server для базы данных первичного сайта. Если SQL использует экземпляр по умолчанию, не включайте этот параметр.

- `-SqlDatabaseName <DatabaseName>` (обязательно): Имя базы данных первичного сайта, например `CM_ABC`.

- `-ReportWebServiceUrl <ReportWebServiceUrl>`: URL-адрес веб-службы точки службы отчетов первичного сайта. Это значение **URL-адреса веб-службы** в **Reporting Services Configuration Manager**.

    > [!NOTE]
    > Этот параметр предназначен для установки **Отчета об аудите восстановления**, связанного с веб-сайтом администрирования и мониторинга. По умолчанию Configuration Manager включает другие отчеты по управлению BitLocker.

- `-HelpdeskUsersGroupName <DomainUserGroup>`: Например, `contoso\BitLocker help desk users`. Группа пользователей домена, члены которой имеют доступ к разделам **Управление TPM** и **Восстановление дисков** веб-сайта администрирования и мониторинга. При использовании этих параметров эта роль должна заполнить все поля, включая имя домена и учетной записи пользователя.

- `-HelpdeskAdminsGroupName <DomainUserGroup>`: Например, `contoso\BitLocker help desk admins`. Группа пользователей домена, члены которой имеют доступ ко всем областям восстановления веб-сайта администрирования и мониторинга. Чтобы помочь пользователям восстановить свои диски, эта роль должна только ввести ключ восстановления.

- `-MbamReportUsersGroupName <DomainUserGroup>`: Например, `contoso\BitLocker report users`. Группа пользователей домена, члены которой имеют доступ только для чтения к области **Отчеты** на веб-сайте администрирования и мониторинга.

    > [!NOTE]
    > Сценарий установщика не создает группы пользователей домена, указанные в параметрах **-HelpdeskUsersGroupName**, **-HelpdeskAdminsGroupName**, и **-MbamReportUsersGroupName**. Перед запуском скрипта обязательно создайте эти группы.
    >
    > При указании параметров **-HelpdeskUsersGroupName**, **-HelpdeskAdminsGroupName**, и **-MbamReportUsersGroupName**, убедитесь, что указаны и доменное имя, и имя группы. Используйте следующий формат: `"domain\user_group"`. Не исключайте доменное имя. Если доменное имя или имя группы содержит пробелы или специальные символы, заключите параметр в кавычки (`"`).

- `-SiteInstall Both`: Укажите, какие компоненты следует установить. Допустимые параметры:
  - `Both`: установка обоих компонентов.
  - `HelpDesk`: Установка только веб-сайта для администрирования и мониторинга.
  - `SSP`: установка только портала самообслуживания.

- `-IISWebSite`: веб-сайт, на котором скрипт устанавливает веб-приложения MBAM. По умолчанию используется стандартный веб-сайт IIS. Создайте настраиваемый веб-сайт перед использованием этого параметра.

- `-InstallDirectory`: путь, по которому скрипт устанавливает файлы веб-приложения. По умолчанию используется путь `C:\inetpub`. Создайте настраиваемый каталог перед использованием этого параметра.

- `-Uninstall`: удаляет сайты службы технической поддержки и веб-портала самообслуживания на веб-сервере, на котором они были установлены ранее.


## <a name="run-the-script"></a>Выполнение скрипта

На целевом веб-сервере выполните указанные далее действия.

> [!NOTE]
> В зависимости от структуры сайта может потребоваться запустить скрипт несколько раз. Например, запустите сценарий на точке управления, чтобы установить веб-сайт администрирования и мониторинга. Затем снова запустите его на отдельном веб-сервере, чтобы установить портал самообслуживания.

1. Скопируйте следующие файлы из `SMSSETUP\BIN\X64` в папке установки Configuration Manager на сервере сайта в локальную папку на целевом сервере:

    - `MBAMWebSite.cab`
    - `MBAMWebSiteInstaller.ps1`

1. Запустите PowerShell от имени администратора, а затем в командной строке выполните скрипт, аналогичный приведенному ниже:

    ``` PowerShell
    .\MBAMWebSiteInstaller.ps1 -SqlServerName <ServerName> -SqlInstanceName <InstanceName> -SqlDatabaseName <DatabaseName> -ReportWebServiceUrl <ReportWebServiceUrl> -HelpdeskUsersGroupName <DomainUserGroup> -HelpdeskAdminsGroupName <DomainUserGroup> -MbamReportUsersGroupName <DomainUserGroup> -SiteInstall Both
    ```

    Например,

    ``` PowerShell
    .\MBAMWebSiteInstaller.ps1 -SqlServerName sql.contoso.com -SqlInstanceName instance1 -SqlDatabaseName CM_ABC -ReportWebServiceUrl https://rsp.contoso.com/ReportServer -HelpdeskUsersGroupName "contoso\BitLocker help desk users" -HelpdeskAdminsGroupName "contoso\BitLocker help desk admins" -MbamReportUsersGroupName "contoso\BitLocker report users" -SiteInstall Both
    ```

    > [!IMPORTANT]
    > В этом примере командная строка использует все возможные параметры для отображения их использования. Настройте использование в соответствии с вашими требованиями в среде.

После установки получите доступ к порталам с помощью следующих URL-адресов:

- Портал самообслуживания: `https://webserver.contoso.com/SelfService`
- Веб-сайт администрирования и мониторинга: `https://webserver.contoso.com/HelpDesk`

> [!NOTE]
> Корпорация Майкрософт рекомендует, но не требует использования протокола HTTPS. Дополнительные сведения см. в статье [Как настроить SSL в службах IIS](https://docs.microsoft.com/iis/manage/configuring-security/how-to-set-up-ssl-on-iis).

## <a name="verify"></a>Проверка

Для мониторинга и устранения неполадок используйте следующие журналы:

- Журналы событий Windows в разделе **Microsoft-Windows-MBAM-Web**. Дополнительные сведения см. в разделе [Журналы событий BitLocker](../../tech-ref/bitlocker/about-event-logs.md) и [Журналы событий сервера](../../tech-ref/bitlocker/server-event-logs.md).

- Журналы трассировки для каждого компонента находятся в следующих расположениях по умолчанию:

  - Портал самообслуживания: `C:\inetpub\Microsoft BitLocker Management Solution\Logs\Self Service Website`

  - Веб-сайт администрирования и мониторинга: `C:\inetpub\Microsoft BitLocker Management Solution\Logs\Help Desk Website`

Дополнительные сведения об устранении неполадок см. в разделе [Устранение неполадок BitLocker](../../tech-ref/bitlocker/troubleshoot.md).

## <a name="next-steps"></a>Дальнейшие шаги

[Настройка портала самообслуживания](customize-self-service-portal.md)

Дополнительные сведения об использовании установленных компонентов см. в следующих статьях:

- [Веб-сайт администрирования и мониторинга BitLocker](helpdesk-portal.md)
- [Портал самообслуживания BitLocker](self-service-portal.md)
