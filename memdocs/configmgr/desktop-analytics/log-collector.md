---
title: Сборщик журналируемых данных
titleSuffix: Configuration Manager
description: Устранение неполадок с Аналитикой компьютеров с помощью сборщика журналируемых данных
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 349b2a69-af46-481f-afb2-24d98774e852
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 8782913e40bffdcbe5a151fac8821f05b7e7fece
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268578"
---
# <a name="desktop-analytics-log-collector"></a>Сборщик журналируемых данных Аналитики компьютеров

Начиная с версии 1906 Configuration Manager, средство **DesktopAnalyticsLogsCollector.ps1** из каталога установки Configuration Manager позволяет устранить неполадки с регистрацией устройств в Аналитике компьютеров. Оно выполняет некоторые основные действия по устранению неполадок и собирает соответствующие данные журналов в одну рабочую папку. Вы можете поделиться этим содержимым со службой поддержки Майкрософт.


## <a name="prerequisites"></a>Предварительные условия

- Клиент Аналитики компьютеров под управлением Windows 10, Windows 8.1 или Windows 7 с пакетом обновления 1.

- Запустите сценарий на устройстве с правами администратора и выполните команду **Запуск от имени администратора**.

    > [!Tip]
    > С этим средством можно использовать компонент **Сценарии** в Configuration Manager. Дополнительные сведения см. в разделе [Пример 5. Развертывание скрипта с помощью компонента **Сценарии** в Configuration Manager](#bkmk_ex5).

- Windows 7 с пакетом обновления 1, PowerShell версии 4.0 или более поздней.
    - [.NET Framework версии 4.6 или более поздней](https://dotnet.microsoft.com/download/dotnet-framework).

    - Windows Management Framework [версии 4.0](https://support.microsoft.com/help/2819745) (aka.ms/wmf4download) или [версии 5.1](https://www.microsoft.com/download/details.aspx?id=54616) (aka.ms/wmf5download)

## <a name="usage"></a>Использование

Получите скрипт из содержимого установки Configuration Manager: `SMSSETUP\TOOLS\DesktopAnalyticsLogsCollector\DesktopAnalyticsLogsCollector.ps1`.

``` Syntax
DesktopAnalyticsLogsCollector.ps1
    [-LogPath] <String>
    [-LogMode] <Int16>
    [-CollectNetTrace] <Int16>
    [-CollectUTCTrace] <Int16>
```

## <a name="parameters"></a>Параметры

### `-LogPath`

Указывает локальный или UNC-путь для размещения журнала и других выходных файлов.

**Значения**:

- Локальный путь (максимальная длина = 130), например: `c:\myfolder`.

- UNC-путь (максимальная длина = 130), например: `\\myserver\myfolder`.

**Тип** — Строка

**Позиция**: 1

**Значение по умолчанию**: `$Env:SystemDrive\M365AnalyticsLogs` (Если этот параметр имеет значение null, является пустым или пробелом, скрипт создает папку M365AnalyticsLogs на системном диске.)

### `-LogMode`

Задает уровень детализации журналов.

**Значения**:

- `0`: Запись сообщений скрипта только в командное окно PowerShell.

- `1`: Запись сообщений скрипта в файл журнала в выходной папке и в командное окно PowerShell.

- `2`: Запись сообщений скрипта только в файл журнала в выходной папке.

**Тип** — Int16

**Позиция**: 2

**Значение по умолчанию**: `1` (Запись сообщений скрипта в файл журнала и в командное окно PowerShell.)

### `-CollectNetTrace`

Указывает, собирает ли скрипт трассировку сети.

**Значения**:

- `0`: Не включает трассировку сети.

- `1` (любое значение ненулевого целого числа): Включает трассировку сети и собирает результаты.

**Тип** — Int16

**Позиция**: 3

**Значение по умолчанию**: `0` (Не включает трассировку сети).

### `-CollectUTCTrace`

Указывает, собирает ли скрипт трассировку времени в формате UTC для Windows и выполняет ли диагностику подключения.

**Значения**:

- `0`: Не включает трассировку времени в формате UTC и не выполняет диагностику подключений.

- `1` (любое значение ненулевого целого числа): Включает трассировку времени в формате UTC, выполняет диагностику подключений и собирает результаты.

**Тип** — Int16

**Позиция**: 4

**Значение по умолчанию**: `0` (Не включает трассировку времени в формате UTC и не выполняет диагностику подключений).


## <a name="output"></a>Выходные данные

Скрипт создает *рабочую папку* по указанному пути. Например, **M365AnalyticsLogs_yy_MM_dd_HH_mm_ss**. И помещает в нее все свои выходные файлы.

Если активировать для скрипта запись в *файл журнала*, он создаст его в рабочей папке. Например, **M365AnalyticsLogs_yy_MM_dd_HH_mm_ss.txt**.

Скрипт также создает другие *диагностические файлы* в рабочей папке. Пример.

- `installedKBs.txt`: список обновлений Windows, установленных на устройстве.
- `appcompat`: данные о совместимости приложений.
- `Reg*.txt`: ряд файлов с экспортированными данными из реестра Windows.


## <a name="examples"></a>Примеры

### <a name="example-1-run-script-via-powershell-command-window-with-default-values"></a><a name="bkmk_ex1"></a> Пример 1. Выполнение скрипта с помощью командного окна PowerShell со значениями по умолчанию.

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1
```

### <a name="example-2-run-script-via-powershell-command-window-with-specified-parameters"></a><a name="bkmk_ex2"></a> Пример 2. Выполнение скрипта с помощью командного окна PowerShell с указанными параметрами.

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1 -LogPath "c:\testABC" -LogMode 0 -CollectNetTrace 0 -CollectUTCTrace 0
```

### <a name="example-3-run-script-via-powershell-command-window-with-specified-parameters-in-position"></a><a name="bkmk_ex3"></a> Пример 3. Выполнение скрипта с помощью командного окна PowerShell с указанными параметрами в позиции.

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1 "c:\testABC" 2 0 0
```

### <a name="example-4-run-script-via-powershell-command-window-with-specified-parameter-and-verbose-messages"></a><a name="bkmk_ex4"></a> Пример 4. Выполнение скрипта с помощью командного окна PowerShell с указанным параметром и подробными сообщениями.

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1 -LogMode 1 -Verbose
```

### <a name="example-5-deploy-script-via-configuration-manager-scripts"></a><a name="bkmk_ex5"></a> Пример 5. Развертывание скрипта с помощью компонента **Сценарии** в Configuration Manager.

См. дополнительные сведения о [создании и запуске скриптов PowerShell из консоли Configuration Manager](../apps/deploy-use/create-deploy-scripts.md).

DesktopAnalyticsLogsCollector.ps1 имеет цифровую подпись корпорации Майкрософт. Возможно нужно будет добавить этот сертификат подписывания кода Майкрософт в качестве доверенного издателя на целевом устройстве.

1. Откройте окно свойств скрипта в проводнике Windows. Перейдите на вкладку **Цифровые подписи** и выберите **Сведения**.

2. На вкладке **Общие** выберите **Просмотр сертификата**.

    > [!Note]
    > Чтобы распространить сертификат с помощью других механизмов, сначала экспортируйте его в файл. Перейдите на вкладку **Сведения** и выберите **Копировать в файл**.

3. Нажмите кнопку **Установить сертификат**. Импортируйте сертификат, поместив его в хранилище **доверенных издателей**.


## <a name="see-also"></a>См. также

- [Устранение проблем с Аналитикой компьютера](troubleshooting.md)

- [Создание и запуск сценариев PowerShell из консоли Configuration Manager](../apps/deploy-use/create-deploy-scripts.md)
