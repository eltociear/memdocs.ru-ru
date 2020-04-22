---
title: Центр поддержки OneTrace (предварительная версия)
titleSuffix: Configuration Manager
description: OneTrace — это новое средство просмотра журналов в центре поддержки, которое обладает усовершенствованиями по сравнению с CMTrace.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4cde43d1-9b09-4601-b389-0776de451b4e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 150090556d63b1bdf0b35dc9b53b450137d7f9d3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707452"
---
# <a name="support-center-onetrace-preview"></a>Центр поддержки OneTrace (предварительная версия)

<!--3555962-->

Начиная с версии 1906, OneTrace является новым средством просмотра журналов для центра поддержки. Оно действует аналогично CMTrace, но обладает следующими усовершенствованиями:

- Представление со вкладками
- Закрепляемые окна
- Расширенные возможности поиска
- Возможность включить фильтры, не выходя из представления журнала
- Подсказки полосы прокрутки для быстрого определения кластеров ошибок
- Быстрое открытие больших файлов журнала

[![Снимок экрана средства просмотра журналов OneTrace](media/3555962-onetrace.png)](media/3555962-onetrace.png#lightbox)

OneTrace работает со многими типами файлов журнала, такими как:

- Журналы клиента Configuration Manager
- Журналы сервера Configuration Manager
- Сообщения о состоянии
- Файлы журнала трассировки событий Windows для Центра обновления Windows в Windows 10
- Файлы журнала Центра обновления Windows в Windows 7 и Windows 8.1

## <a name="prerequisites"></a>Предварительные условия

- Платформа .NET Framework версии 4.6 или более поздней

## <a name="install"></a>Установить

OneTrace устанавливается в составе центра поддержки. Найдите установщик центра поддержки на сервере сайта по следующему пути: `cd.latest\SMSSETUP\Tools\SupportCenter\SupportCenterInstaller.msi`.

По умолчанию приложение OneTrace устанавливается здесь: `C:\Program Files (x86)\Configuration Manager Support Center\CMPowerLogViewer.exe`.

> [!Note]  
> Центр технической поддержки и OneTrace используют Windows Presentation Foundation (WPF). Этот компонент недоступен в среде предустановки Windows. Продолжайте использовать CMTrace в загрузочных образах при развертывании через последовательность задач.  

## <a name="log-groups"></a>Группы журналов

<!--5559993-->

Начиная с версии 2002, OneTrace поддерживает настраиваемые группы журналов, аналогично этой функции в центре поддержки. Группы журналов позволяют открывать все файлы журналов для одного сценария. В настоящее время OneTrace включает группы для следующих сценариев:

- Управление приложениями
- Параметры соответствия (или управление требуемой конфигурацией)
- Обновления программного обеспечения

Чтобы просмотреть группы журналов, перейдите в меню **Вид** и выберите **Группы журналов**.

![Снимок экрана: группа журналов OneTrace для управления приложениями](media/5559993-onetrace-log-groups.png)

### <a name="customize-log-groups"></a>Настройка групп журналов

Вы можете настроить эти группы, изменив XML-файл конфигурации, который по умолчанию находится по следующему пути: `C:\Program Files (x86)\Configuration Manager Support Center\LogGroups.xml`.

В следующем примере показана одна часть файла конфигурации по умолчанию:

``` XML
<LogGroups>
  <LogGroup Name="Desired Configuration Management" GroupType="1" GroupFilePath="">
    <LogFile>CIAgent.log</LogFile>
    <LogFile>CIDownloader.log</LogFile>
    <LogFile>CIStateStore.log</LogFile>
    <LogFile>CIStore.log</LogFile>
    <LogFile>CITaskMgr.log</LogFile>
    <LogFile>ccmsdkprovider.log</LogFile>
    <LogFile>DCMAgent.log</LogFile>
    <LogFile>DCMReporting.log</LogFile>
    <LogFile>DcmWmiProvider.log</LogFile>
  </LogGroup>
</LogGroups>
```

Свойство `GroupType` принимает следующие значения:

- `0`: неизвестно или другое
- `1`: Журналы клиента Configuration Manager
- `2`: Журналы сервера Configuration Manager

Свойство `GroupFilePath` может включать явный путь к файлам журнала. Если оно пустое, OneTrace полагается на конфигурацию реестра для типа группы. Например, если задать `GroupType=1`, по умолчанию OneTrace будет автоматически искать в `C:\Windows\CCM\Logs` журналы в группе. В этом примере не нужно указывать `GroupFilePath`.

## <a name="see-also"></a>См. также

- [Средство просмотра журналов центра поддержки](support-center-ui-reference.md#bkmk_log-viewer)

- [CMTrace](cmtrace.md)
