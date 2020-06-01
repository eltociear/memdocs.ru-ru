---
title: Устранение неполадок с подключенным кэшем
titleSuffix: Configuration Manager
description: Технические сведения о подключенном кэше Майкрософт, которые помогут устранить неполадки.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 121e0341-4f51-4d54-a357-732c26caf7c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0a8c975798c506339a981e8648003387dc1e9838
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/27/2020
ms.locfileid: "83878096"
---
# <a name="troubleshoot-microsoft-connected-cache-in-configuration-manager"></a>Устранение неполадок с подключенным кэшем Майкрософт в Configuration Manager

Эта статья содержит технические сведения о подключенном кэше Майкрософт в Configuration Manager. Они помогают устранять неполадки, которые могут возникнуть в вашей среде. Дополнительные сведения о его работе и использовании см. в статье [Подключенный кэш Майкрософт в Configuration Manager](../../../plan-design/hierarchy/microsoft-connected-cache.md).

> [!NOTE]
> Начиная с версии 1910 эта функция теперь называется **подключенным кэшем Майкрософт**. Ранее она называлась оптимизацией доставки с помощью сетевого кэша.

## <a name="verify"></a>Проверка

При правильной установке сервера кэша для оптимизации доставки и правильной настройке клиентов они скачивают данные с сервера кэша, установленного на точке распространения, а не в Интернете.

Проверьте это поведение [на клиенте](#bkmk_verify-client) или [на сервере](#bkmk_verify-server).

### <a name="verify-on-a-client"></a><a name="bkmk_verify-client"></a> Проверка на клиенте

1. На клиенте под управлением Windows 10 версии 1809 или более поздней скачайте содержимое, управляемое облаком. Дополнительные сведения о типах содержимого, поддерживаемых подключенным кэшем, см. в разделе [Проверка подключенного кэша](../../../plan-design/hierarchy/microsoft-connected-cache.md#verify).

2. Откройте PowerShell и выполните следующую команду: `Get-DeliveryOptimizationStatus`

Пример.

```PowerShell
PS C:\> Get-DeliveryOptimizationStatus

FileId                      : ec523d49c4f7c3c4444f0d9b952286ce40fdcee4
FileSize                    : 549064
TotalBytesDownloaded        : 549064
PercentPeerCaching          : 0
BytesFromPeers              : 0
BytesFromHttp               : 0
Status                      : Caching
Priority                    : Background
BytesFromCacheServer        : 549064
BytesFromLanPeers           : 0
BytesFromGroupPeers         : 0
BytesFromInternetPeers      : 0
BytesToLanPeers             : 0
BytesToGroupPeers           : 0
BytesToInternetPeers        : 0
DownloadDuration            : 00:00:00.0780000
HttpConnectionCount         : 2
LanConnectionCount          : 0
GroupConnectionCount        : 0
InternetConnectionCount     : 0
DownloadMode                : 99
SourceURL                   : http://au.download.windowsupdate.com/c/msdownload/update/software/defu/2019/09/am_delta_p
                              atch_1.301.664.0_ec523d49c4f7c3c4444f0d9b952286ce40fdcee4.exe
NumPeers                    : 0
PredefinedCallerApplication : WU Client Download
ExpireOn                    : 9/6/2019 8:36:19 AM
IsPinned                    : False
```

Обратите внимание, что атрибут `BytesFromCacheServer` не равен нулю.

Если клиент настроен неправильно или сервер кэша не установлен должным образом, клиент оптимизации доставки откатывается на исходный облачный источник. Тогда атрибут BytesFromCacheServer будет равен нулю.

### <a name="verify-on-the-server"></a><a name="bkmk_verify-server"></a> Проверка на сервере

Сначала убедитесь, что свойства реестра настроены правильно: `HKLM\SOFTWARE\Microsoft\Delivery Optimization In-Network Cache`. Например, расположение кэша на диске — `PrimaryDrivesInput\DOINC-E77D08D0-5FEA-4315-8C95-10D359D59294`, где `PrimaryDrivesInput` может задавать несколько дисков, например `C,D,E`.

Затем используйте следующий метод для имитации запроса на скачивание от клиента на сервер с обязательными заголовками.

1. Откройте окно 64-разрядной версии PowerShell от имени администратора.
2. Выполните следующую команду и замените имя или IP-адрес сервера на `<DoincServer>`:

```PowerShell
Invoke-WebRequest -URI "http://<DoincServer>/mscomtest/wuidt.gif" -Headers @{"Host"="b1.download.windowsupdate.com"}
```

Вывод имеет следующий вид.

```PowerShell
PS C:\WINDOWS\system32> Invoke-WebRequest -URI "http://SERVER01.CONTOSO.COM/mscomtest/wuidt.gif" -Headers @{"Host"="b1.download.windowsupdate.com"}


StatusCode        : 200
StatusDescription : OK
Content           : {71, 73, 70, 56...}
RawContent        : HTTP/1.1 200 OK
                    X-HW: 1567797125.dop019.se2.t,1567797125.cds058.se2.s,1567797125.dop114.at2.r,1567797125.cds079.at2
                    .p,1567797125.cds058.se2.p
                    X-CCC: cdP+dRBgUCoZO1mezA9zhg2VwQ7P1JWTh9k+GhfQmu8=_SLwv...
Headers           : {[X-HW, 1567797125.dop019.se2.t,1567797125.cds058.se2.s,1567797125.dop114.at2.r,1567797125.cds079.a
                    t2.p,1567797125.cds058.se2.p], [X-CCC,
                    cdP+dRBgUCoZO1mezA9zhg2VwQ7P1JWTh9k+GhfQmu8=_SLwvtSBQdT3uPQ5ikBe1ABMbdYIIncem+h5dtcLI6GY=],
                    [X-CID, 100], [Accept-Ranges, bytes]...}
RawContentLength  : 969710
```

Следующие атрибуты указывают на успешное выполнение:

- `StatusCode : 200`
- `StatusDescription : OK`

## <a name="log-files"></a>Файлы журнала

- Журнал установки ARR: `%temp%\arr_setup.log`

- Журнал установки сервера кэша оптимизации доставки: `SMS_DP$\Ms.Dsp.Do.Inc.Setup\DoincSetup.log` в точке распространения и `DistMgr.log` на сервере сайта

- Рабочие журналы IIS: По умолчанию — `%SystemDrive%\inetpub\logs\LogFiles`

- Журнал операций сервера кэша оптимизации доставки: `C:\Doinc\Product\Install\Logs`

    > [!TIP]
    > Помимо прочего, этот журнал поможет определить проблемы с подключением к облаку Майкрософт.

## <a name="setup-error-codes"></a>Коды ошибок установки

В следующей таблице перечислены возможные коды ошибок, которые могут возникнуть, когда Configuration Manager устанавливает компонент подключенного кэша в точке распространения:

| Код ошибки | Описание ошибки |
|------------|-------------------|
| 0x00000000 | Успех |
| 0x00000BC2 | Успех, необходима перезагрузка |
| 0x00000643 | Общая ошибка при установке |
| 0x00D00001 | Программу установки подключенного кэша можно запустить, только если установлены службы IIS |
| 0x00D00002 | Программу установки подключенного кэша можно запустить, только если на сервере существует веб-сайт по умолчанию |
| 0x00D00003 | Невозможно установить подключенный кэш, если уже установлена маршрутизация запросов приложений (ARR) |
| 0x00D00004 | Программу установки подключенного кэша можно запустить, только если служба маршрутизации запросов приложений (ARR) была установлена с помощью сценария install.ps1 |
| 0x00D00005 | Для установки подключенного кэша требуется сеанс PowerShell, работающий от имени администратора |
| 0x00D00006 | Программу установки подключенного кэша можно запустить только из 64-разрядной среды PowerShell |
| 0x00D00007 | Программу установки подключенного кэша можно запустить только на сервере Windows Server |
| 0x00D00008 | Сбой: Указанное количество дисков кэша должно соответствовать количеству указанных процентных значений размера диска кэша |
| 0x00D00009 | Сбой: Необходимо указать допустимый идентификатор узла кэша |
| 0x00D0000A | Сбой: Необходимо указать допустимый набор дисков кэша |
| 0x00D0000B | Сбой: Необходимо указать допустимый набор процентных значений дискового пространства кэша |
| 0x00D0000C | Сбой: Необходимо указать допустимый процент размера диска кэша или размер диска кэша в ГБ |
| 0x00D0000D | Сбой: Необходимо указать допустимый процент размера диска кэша или размер диска кэша в ГБ, но не оба значения одновременно |
| 0x00D0000E | Сбой: Указанное количество дисков кэша должно соответствовать количеству указанных значений размера диска кэша в ГБ |
| 0x00D0000F | Сбой: Не удалось создать резервную копию файла applicationhost.config из $AppHostConfig в $AppHostConfigDestinationName |
| 0x00D00010 | Сбой: Не удалось создать резервную копию файла web.config веб-сайта по умолчанию с $WebsiteConfigFilePath на $WebConfigDestinationName |
| 0x00D00011 | Сбой: Произошло исключение в SetupARRWebFarm.ps1 |
| 0x00D00012 | Сбой: Произошло исключение в SetupARRWebFarmRewriteRules.ps1 |
| 0x00D00013 | Сбой: Произошло исключение в SetupARRWebFarmProperties.ps1 |
| 0x00D00014 | Сбой: Произошло исключение в SetupAllowableServerVariables.ps1 |
| 0x00D00015 | Сбой: Произошло исключение в SetupFirewallRules.ps1 |
| 0x00D00016 | Сбой: Произошло исключение в SetupAppPoolProperties.ps1 |
| 0x00D00017 | Сбой: Произошло исключение в SetupARROutboundRules.ps1 |
| 0x00D00018 | Сбой: Произошло исключение в SetupARRDiskCache.ps1 |
| 0x00D00019 | Сбой: Произошло исключение в SetupARRProperties.ps1 |
| 0x00D0001A | Сбой: Произошло исключение в SetupARRHealthProbes.ps1 |
| 0x00D0001B | Сбой: Произошло исключение в VerifyIISSItesStarted.ps1 |
| 0x00D0001C | Сбой: Произошло исключение в SetDrivesToHealthy.ps1 |
| 0x00D0001D | Сбой: Произошло исключение в VerifyCacheNodeSetup.ps1 |
| 0x00D0001E | Невозможно установить подключенный кэш, если веб-сайт по умолчанию не находится на порте 80 |
| 0x00D0001F | Сбой: Распределение кэша в процентах дискового пространства не может превышать 100 |
| 0x00D00020 | Сбой: Выделение дискового накопителя в ГБ не может превышать свободное место на диске |
| 0x00D00021 | Сбой: Распределение дискового кэша в процентах должно быть больше 0 |
| 0x00D00022 | Сбой: Распределение дискового кэша в ГБ должно быть больше 0 |
| 0x00D00023 | Сбой: Произошло исключение в RegisterScheduledTask_CacheNodeKeepAlive |
| 0x00D00024 | Сбой: Произошло исключение в RegisterScheduledTask_Maintenance |
| 0x00D00025 | Сбой: Произошло исключение при настройке правил перезаписи для фермы HTTPS: $FarmName |
| 0x00D00026 | Сбой: Произошло исключение при настройке правил перезаписи для фермы HTTP: $FarmName |
| 0x00D00027 | Невозможно установить подключенный кэш, так как не удалось установить зависимое программное обеспечение "Маршрутизация запросов приложений (ARR)". См. файл журнала %temp%\arr_setup.log |

## <a name="iis-configurations"></a>Конфигурации IIS

Установка сервера кэша оптимизации доставки вносит несколько изменений в конфигурацию IIS в точке распространения.

### <a name="application-request-routing"></a>Маршрутизация запросов приложения

Сервер кэша устанавливает и настраивает [маршрутизацию запросов приложений IIS (ARR)](https://www.iis.net/downloads/microsoft/application-request-routing). Во избежание потенциальных конфликтов точка распространения не может уже содержать этот компонент.

### <a name="allowed-server-variables"></a>Допустимые переменные сервера

После установки сервера кэша веб-сайт по умолчанию будет иметь следующие *локальные* переменные сервера:

- HTTP_HOST
- QUERY_STRING
- X-CCC
- X-CID
- X-DOINC-OUTBOUND

### <a name="rewrite-rules"></a>Правила перезаписи

Сервер кэша добавляет следующие правила перезаписи:

#### <a name="inbound-rewrite-rules"></a>Правила перезаписи входящих сообщений

- `Doinc_ForwardToFarm_shswda01.download.manage-selfhost.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_swdc01.manage.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_swdc02.manage.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_dl.delivery.mp.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_officecdn.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_b1.download.windowsupdate.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_download.windowsupdate.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_officecdn.microsoft.com.edgesuite.net_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_au.b1.download.windowsupdate.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_assets1.xboxlive.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_au.download.windowsupdate.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_emdl.ws.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_tlu.dl.delivery.mp.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_assets2.xboxlive.com_E77D08D0-5FEA-4315-8C95-10D359D59294`

#### <a name="outbound-rewrite-rules"></a>Правила перезаписи исходящих сообщений

- `Doinc_Outbound_SetHeader_X_CID_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_Outbound_SetHeader_X_CCC_E77D08D0-5FEA-4315-8C95-10D359D59294`

## <a name="manage-server-resources"></a>Управление ресурсами сервера

Место на диске, необходимое для каждого сервера кэша, может отличаться в зависимости от требований организации к обновлению. 100 ГБ должно быть достаточно для кэширования следующего содержимого:

- Обновление компонентов
- От двух до трех месяцев обновлений для повышения качества и обновлений для Office
- Приложения Microsoft Intune и приложения папки "Входящие" Windows

Сервер кэша не должен потреблять значительный объем системной памяти или процессорного времени. Если после установки сервера кэша заметна значительная загрузка ресурсов процесса или памяти, проанализируйте файлы журналов IIS и ARR.

Если файлы журнала IIS и ARR занимают слишком много пространства на сервере, для управления файлами журнала можно использовать несколько методов. Дополнительные сведения см. в статье [Управление файловым хранилищем журналов IIS](https://docs.microsoft.com/iis/manage/provisioning-and-managing-iis/managing-iis-log-file-storage#overview).

## <a name="see-also"></a>См. также

[Подключенный кэш Майкрософт в Configuration Manager](../../../plan-design/hierarchy/microsoft-connected-cache.md)
