---
title: Установка консоли
titleSuffix: Configuration Manager
description: Установите консоль Configuration Manager для подключения к сайту центра администрирования или первичному сайту.
ms.date: 04/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d39c201f-d364-4e7b-bde4-faa76d747f33
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f5fda03090f7ec69eb78b20385dfc009bac88f40
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700802"
---
# <a name="install-the-configuration-manager-console"></a>Установка консоли Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Администраторы используют консоль Configuration Manager для управления средой Configuration Manager. Каждую консоль Configuration Manager можно подключить к сайту центра администрирования (CAS) или первичному сайту. Консоль Configuration Manager нельзя подключить к вторичному сайту.

Консоль Configuration Manager всегда устанавливается на сервере сайта для CAS или первичного сайта. Чтобы установить консоль отдельно от сервера сайта, запустите автономный установщик.  



## <a name="prerequisites"></a>Предварительные условия

- У вас есть права **локального администратора** на целевом компьютере для консоли.  

- У вас есть разрешения на **чтение** из расположения файлов установки консоли Configuration Manager.  



## <a name="source-paths"></a>Исходные пути

Решите, какой исходный путь использовать:  

- Папка ConsoleSetup на сервере сайта: `<Configuration Manager site server installation path>\Tools\ConsoleSetup`.  

    При установке сервера сайта во вложенную папку **Tools\ConsoleSetup** копируются установочные файлы консоли и поддерживаемые языковые пакеты для сайта. Вы можете скопировать папку **ConsoleSetup** в другое расположение для запуска. Обновление сайта обеспечивает сохранение актуального состояния его локальной версии.  

- Установочный носитель Configuration Manager: `<Configuration Manager installation media>\SMSSETUP\BIN\I386`.  

    При установке консоли Configuration Manager с установочного носителя всегда устанавливается англоязычная версия. Это происходит даже в том случае, если сервер сайта поддерживает различные языки или в ОС на целевом компьютере выбран другой язык.  

Если это возможно, запустите установщик консоли из папки **ConsoleSetup**, а не с исходного носителя.

> [!Important]  
> Не устанавливайте консоль, используя исходные файлы **CD.Latest**. Этот сценарий не поддерживается и может вызвать проблемы с установкой консоли. Дополнительные сведения см. в разделе [Папка CD.Latest](../../manage/the-cd.latest-folder.md#unsupported-scenarios).<!-- SCCMDocs issue 1359 -->  

Если вы создаете пакет для установки консоли на других компьютерах, убедитесь, что он содержит следующие файлы:<!--3612513-->

- ConsoleSetup.exe;
- AdminConsole.msi;
- ConfigMgr.AC_Extension.i386.cab (начиная с версии 1902);
- ConfigMgr.AC_Extension.amd64.cab (начиная с версии 1902).



## <a name="use-the-setup-wizard"></a>Использование мастера установки  

1. Перейдите по исходному пути и откройте файл **ConsoleSetup.exe**.  

    > [!IMPORTANT]  
    > Всегда устанавливайте консоль с помощью **ConsoleSetup.exe**. Хотя консоль Configuration Manager можно установить, запустив файл AdminConsole.msi, в этом случае не проверяются необходимые требования и зависимости. Это может привести к некорректной установке.  

2. В мастере нажмите кнопку **Далее**.  

3. На странице **Сервер сайта** укажите полное доменное имя сервера сайта, к которому будет подключена консоль Configuration Manager.  

4. На странице **Папка установки** укажите папку установки для консоли Configuration Manager. Путь к папке не должен содержать пробелы в конце и символы Юникода.  

5. На странице **Программа улучшения качества программного обеспечения** укажите, хотите ли вы принимать участие в программе улучшения качества программного обеспечения (CEIP).  

    > [!Note]  
    > Начиная с Configuration Manager версии 1802 компонент CEIP будет удален из продукта.

6. На странице **Все готово для установки** выберите **Установить**.  



## <a name="install-from-a-command-prompt"></a>Установка из командной строки  

> [!TIP]  
> При установке консоли Configuration Manager из командной строки всегда устанавливается англоязычная версия. Это происходит даже в том случае, если в ОС на целевом компьютере выбран другой язык. Чтобы установить консоль Configuration Manager на языке, отличающемся от английского, [используйте мастер установки](#use-the-setup-wizard).  


### <a name="consolesetupexe-command-line-options"></a>Параметры командной строки для ConsoleSetup.exe

#### <a name="q"></a>/q

Автоматически устанавливает консоль Configuration Manager. Параметры **EnableSQM**, **TargetDir**и **DefaultSiteServerName** при использовании этого параметра являются обязательными.

#### <a name="uninstall"></a>/uninstall

Удаляет консоль Configuration Manager. При использовании совместно с параметром **/q** этот параметр следует указать первым.

#### <a name="langpackdir"></a>LangPackDir

Указывает путь к папке, содержащей языковые файлы. Для скачивания языковых файлов вы можете использовать **загрузчик программы установки** . Если этот параметр не используется, программа установки выполнит поиск языковой папки в текущей папке. Если языковая папка не будет найдена, программа установки продолжит установку только для английского языка. Дополнительные сведения см. в разделе [Загрузчик программы установки](setup-downloader.md).

#### <a name="targetdir"></a>TargetDir

Указывает папку для установки консоли Configuration Manager. Этот параметр является обязательным при использовании параметра **/q** .

#### <a name="enablesqm"></a>EnableSQM

Указывает, следует ли принимать участие в программе улучшения качества программного обеспечения. Чтобы присоединиться к программе, используйте значение **1**, а чтобы отказаться от участия — значение **0**. Этот параметр является обязательным при использовании параметра **/q** .

> [!Important]  
> Начиная с Configuration Manager версии 1802 компонент CEIP будет удален из продукта. В случае использования этого параметра установка завершится сбоем.

#### <a name="defaultsiteservername"></a>DefaultSiteServerName

Определяет полное доменное имя сервера сайта, к которому консоль подключается при открытии. Этот параметр является обязательным при использовании параметра **/q** .


### <a name="examples"></a>Примеры

> [!Important]  
> Для 1802 и более поздних версий не добавляйте параметр **EnableSQM**

#### <a name="silent-install"></a>Автоматическая установка

`ConsoleSetup.exe /q TargetDir="%ProgramFiles%\ConfigMgr Console" DefaultSiteServerName=MyServer.Contoso.com`

#### <a name="silent-install-with-language-packs"></a>Автоматическая установка с языковыми пакетами

`ConsoleSetup.exe /q TargetDir="C:\Program Files\ConfigMgr Console" DefaultSiteServerName=MyServer.Contoso.com LangPackDir=C:\Downloads\ConfigMgr`  

#### <a name="silent-uninstall"></a>Автоматическое удаление

`ConsoleSetup.exe /uninstall /q`  



## <a name="see-also"></a>См. также

Администратор видит объекты в консоли в зависимости от разрешений, назначенных учетной записи пользователя. Дополнительные сведения см. в разделе [Основы ролевого администрирования](../../../understand/fundamentals-of-role-based-administration.md).

Дополнительные сведения о навигации в пользовательском интерфейсе Configuration Manager см. в статье [Использование консоли Configuration Manager](../../manage/admin-console.md).
