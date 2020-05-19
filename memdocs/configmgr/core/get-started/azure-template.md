---
title: Создание лаборатории в Azure
titleSuffix: Configuration Manager
description: Автоматизируйте создание лабораторной среды Configuration Manager версии Technical Preview или лабораторной среды для оценки текущей ветви с помощью шаблонов Azure
ms.date: 07/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9875c443-19bf-43a0-9203-3a741f305096
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 23cc7d0c642637a310f53280bafed6a2a28d2834
ms.sourcegitcommit: 4174f7e485067812c29aea01a4767989ffdbb578
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/15/2020
ms.locfileid: "83406688"
---
# <a name="create-a-configuration-manager-lab-in-azure"></a>Создание лабораторной среды Configuration Manager в Azure

*Область применения: Configuration Manager (Current Branch, Technical Preview)*

<!--3556017-->

В этом руководстве описывается создание лабораторной среды Configuration Manager в Microsoft Azure. Для упрощения и автоматизации создания лаборатории с помощью ресурсов Azure используются шаблоны Azure. Предоставляются два шаблона Azure: 

- При использовании шаблона Azure Configuration Manager версии Technical Preview устанавливается последняя версия ветви Configuration Manager версии Technical Preview.
- При использовании шаблона Azure текущей ветви Configuration Manager устанавливается последняя версия текущей ветви Configuration Manager. 

Дополнительные сведения см. в статье [Вопросы и ответы по использованию Configuration Manager в Azure](../understand/configuration-manager-on-azure.md).



## <a name="prerequisites"></a>Предварительные условия

Для выполнения этой процедуры требуется подписка Azure, в которой можно создать следующие объекты: 
- Две виртуальные машины Standard_B2s для контроллера домена, точки управления и точки распространения.
- Одна виртуальная машина Standard_B2ms для сервера основного сайта и сервера базы данных SQL.
- учетная запись хранения Standard_LRS.

> [!Tip]  
> Чтобы определить возможные затраты, воспользуйтесь [калькулятором цен Azure](https://azure.microsoft.com/pricing/calculator/).  



## <a name="process"></a>Процесс

1. Перейдите к [шаблону Configuration Manager версии Technical Preview](https://azure.microsoft.com/resources/templates/sccm-technicalpreview/) или к [шаблону текущей ветви Configuration Manager](https://azure.microsoft.com/resources/templates/sccm-currentbranch/).  

2. Нажмите кнопку **Развертывание в Azure**. Откроется портал Azure.  

3. Заполните шаблон быстрого запуска Azure приведенными ниже сведениями.

    - Основные  

        - **Подписка**: имя подписки, в которой следует создать виртуальные машины.  

        - **Группа ресурсов**: выберите группу ресурсов, которую следует использовать для этих виртуальных машин.  

        - **Расположение** — выберите центр обработки данных Azure для размещения этой лабораторной среды.  

    - "Настройки"  

        - **Префикс**: имя префикса виртуальных машин. Дополнительные сведения см. в разделе [Сведения о виртуальных машинах Azure](#azure-vm-info).  

        - **Имя администратора**: имя пользователя с административными правами на виртуальных машинах. Это имя будет использоваться для входа на виртуальные машины.  

        - **Пароль администратора**: пароль должен соответствовать требованиям Azure к сложности. Дополнительные сведения см. в описании параметра [adminPassword](https://docs.microsoft.com/rest/api/compute/virtualmachines/createorupdate#osprofile).  

    > [!Important]  
    > Приведенные ниже параметры требуются Azure. Используйте значения по умолчанию. Не изменяйте их.  
    > 
    > - **\_artifacts Location**: расположение сценариев для этого шаблона. <!-- https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/sccm-technicalpreview/ -->  
    >
    > - **\_artifacts Location Sas Token**: маркер SAS требуется для доступа к расположению артефактов.  
    > 
    > - **Расположение** — расположение для всех ресурсов.

4. Прочитайте условия. Если вы согласны с ними, выберите **Я принимаю указанные выше условия**. Затем, чтобы продолжить, выберите **Приобрести**. 

Azure проверит параметры, а затем начнет развертывание. Проверить состояние развертывания можно на портале Azure. 

> [!NOTE]
> Процесс может занять 2–4 часа. Даже если на портале Azure сообщается, что развертывание успешно завершилось, скрипты настройки продолжают выполняться. Не перезапускайте виртуальные машины во время этого процесса.

Чтобы проверить состояние выполнения скриптов настройки, подключитесь к серверу `<prefix>PS1` и просмотрите следующий файл: `%windir%\TEMP\ProvisionScript\PS1.json`. Если все этапы отображаются как выполненные, процесс завершен.

Чтобы подключиться к виртуальным машинам, сначала получите с портала Azure общедоступные IP-адреса для каждой из них. При подключении к виртуальной машине доменное имя — `contoso.com`. Используйте учетные данные, указанные в шаблоне развертывания. Дополнительные сведения см. в статье [Как подключиться к виртуальной машине Azure под управлением Windows и войти на нее](https://docs.microsoft.com/azure/virtual-machines/windows/connect-logon).



## <a name="azure-vm-info"></a>Сведения о виртуальных машинах Azure

Все три виртуальные машины имеют следующие характеристики:
- 150 ГБ места на диске;
- общедоступный и частный IP-адреса. Общедоступные IP-адреса входят в группу безопасности сети, которая разрешает подключения к удаленному рабочему столу только через TCP-порт 3389. 

Префикс, указанный в шаблоне развертывания, — это префикс имени виртуальной машины. Например, если задан префикс "contoso", то имя компьютера контроллера домена — `contosoDC`.


### `<prefix>DC01`

- Контроллер домена Active Directory
- Standard_B2s с двумя процессорами и 4 ГБ оперативной памяти
- Выпуск Windows Server 2019 Datacenter

#### <a name="windows-features-and-roles"></a>Функции и роли Windows
- Доменные службы Active Directory (ADDS)
- .NET
- Удаленное разностное сжатие (RDC)


### `<prefix>PS01`

- Standard_B2ms с двумя процессорами и 8 ГБ памяти
- выпуск Windows Server 2016 Datacenter;
- SQL Server
- Windows 10 ADK с Windows PE 
- Первичный сайт Configuration Manager

#### <a name="windows-features-and-roles"></a>Функции и роли Windows
- .NET
- Удаленное разностное сжатие (RDC) 
- Службы IIS


### `<prefix>DPMP01`

- Standard_B2s с двумя процессорами и 4 ГБ оперативной памяти
- Выпуск Windows Server 2019 Datacenter
- Точка распространения
- Точка управления

#### <a name="windows-features-and-roles"></a>Функции и роли Windows
- .NET
- Удаленное разностное сжатие (RDC) 
- Службы IIS
- Фоновая интеллектуальная служба передачи (BITS)

### `<prefix>CL01`

- Только для шаблона оценки текущей ветви Configuration Manager
- быть под управлением ОС Windows 10;
- Клиент Configuration Manager
