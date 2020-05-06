---
title: Журналы событий BitLocker
titleSuffix: Configuration Manager
description: Узнайте, как устранять неполадки с помощью сведений о BitLocker в журнале событий Windows.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a9ece9e8-37ec-441d-937c-be4941afce7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4875e7875321294d815bfcd8a25a805d3e085aab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706032"
---
# <a name="bitlocker-event-logs"></a>Журналы событий BitLocker

*Область применения: Configuration Manager (Current Branch)*

Агент управления и веб-службы BitLocker используют журналы событий Windows для записи сообщений. В средстве просмотра событий перейдите к узлу **Журналы приложений и служб** > **Майкрософт** > **Windows**. Канал журнала (узел) зависит от компьютера и компонента.

- **MBAM**: агент управления BitLocker на клиентском компьютере.
- **MBAM-Web**:
  - служба восстановления в точке управления.
  - Портал самообслуживания
  - Веб-сайт администрирования и мониторинга

Дополнительные сведения о конкретных сообщениях в этих журналах см. в следующих статьях:

- [Журналы событий клиента](client-event-logs.md)
- [Журналы событий сервера](server-event-logs.md)

По умолчанию в каждом узле имеется два канала журнала: **Администратор** и **Операционное**. Чтобы получить более подробные сведения для устранении неполадок, можно также отобразить [журналы аналитики и отладки](#bkmk_debug).

## <a name="log-properties"></a>Свойства журнала

В средстве просмотра событий Windows выберите конкретный журнал, например **Администратор**. В меню **Действие** выберите пункт **Свойства**. Настройте следующие параметры.

- **Максимальный размер журнала (КБ)** : по умолчанию этот параметр имеет значение `1028` (1 МБ) для всех журналов.
- **При достижении максимального размера**: по умолчанию для журналов **Администратор** и **Операционное** выбрано значение **Переписывать события при необходимости (сначала старые события)** .

## <a name="analytic-and-debug-logs"></a><a name="bkmk_debug"></a> Журналы аналитики и отладки

Вы можете включить более подробные журналы для устранения неполадок. В средстве просмотра событий в меню **Вид** выберите команду **Отобразить аналитический и отладочный журналы**. Теперь при переходе к каналу журнала вы увидите два дополнительных журнала: **Аналитический** и **Отладка**.

> [!TIP]
> По умолчанию эти журналы имеют указанные ниже свойства.
>
> - **Максимальный размер журнала (КБ)** : `1028` (1 МБ)
> - **Не перезаписывать события (Очищать журнал вручную)**

## <a name="export-logs-to-text"></a>Экспорт журналов в текстовые файлы

Просматривать записи журналов, особенно [аналитического и отладочного](#bkmk_debug), может быть проще в одном текстовом файле. Используйте следующие команды PowerShell для экспорта записей журнала событий в текстовые файлы:

``` PowerShell
# Out-String with a larger -Width does a better job compared to using Out-File with -Width. -Oldest is only required with debug/analytic logs.

# Debug log
Get-WinEvent -LogName Microsoft-Windows-MBAM/Debug -Oldest | Format-Table -AutoSize | Out-String -Width 4096 | Out-File C:\Temp\MBAM_Log_Debug.txt

# Analytic log
Get-WinEvent -LogName Microsoft-Windows-MBAM/Analytic -Oldest | Format-Table -AutoSize | Out-String -Width 4096 | Out-File C:\Temp\MBAM_Log_Analytic.txt

# Admin log
# The above command truncates the output from the admin log, this sample reformats the strings
Get-WinEvent -LogName Microsoft-Windows-MBAM/Admin |
    Select TimeCreated, LevelDisplayName, TaskDisplayName, @{n='Message';e={$_.Message.trim()}} |
    Format-Table -AutoSize -Wrap | Out-String -Width 4096 |
    Out-File -FilePath C:\Temp\MBAM_Log_Admin.txt
```
