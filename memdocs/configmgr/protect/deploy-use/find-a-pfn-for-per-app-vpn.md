---
title: Поиск имени семейства пакетов для VPN для каждого приложения
titleSuffix: Configuration Manager
description: Сведения о двух способах поиска имени семейства пакетов (PFN) для настройки VPN для каждого приложения.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 47118499-3d26-4c25-bfde-b129de7eaa59
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f109e4ea4bee4a1de767508d62bc3f080d24f625
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697122"
---
# <a name="find-a-package-family-name-pfn-for-per-app-vpn"></a>Поиск имени семейства пакетов для VPN для каждого приложения

*Область применения: Configuration Manager (Current Branch)*


Существует два способа поиска PFN-имени для настройки VPN для каждого приложения.

## <a name="find-a-pfn-for-an-app-thats-installed-on-a-windows-10-computer"></a>Поиск PFN-имени для приложения, установленного на компьютере Windows 10

Если вы работаете с приложением, которое уже установлено на компьютере Windows 10, для получения PFN-имени можно использовать командлет PowerShell [Get-AppxPackage](https://technet.microsoft.com/library/hh856044.aspx).

Ниже приведен синтаксис командлета Get-AppxPackage.

``` Syntax
Get-AppxPackage [[-Name] <String> ] [[-Publisher] <String> ] [-AllUsers] [-User <String> ] [ <CommonParameters>]
```

> [!NOTE]
> Для получения PFN-имени может потребоваться запустить PowerShell от имени администратора.

Например, для получения сведений обо всех универсальных приложениях, установленных на компьютере, используйте команду `Get-AppxPackage`.

Чтобы получить сведения о приложении, имя или часть имени которого вам известны, используйте команду `Get-AppxPackage *<app_name>`. Обратите внимание на использование подстановочных знаков, которые особенно удобны, если вы не знаете полного имени приложения. Например, для получения сведений о OneNote используйте команду `Get-AppxPackage *OneNote`.


Ниже приведена информация, полученная для OneNote.

`Name                   : Microsoft.Office.OneNote`

`Publisher              : CN=Microsoft Corporation, O=Microsoft Corporation, L=Redmond, S=Washington, C=US`

`Architecture           : X64`

`ResourceId             :`

`Version                : 17.6769.57631.0`

`PackageFullName        : Microsoft.Office.OneNote_17.6769.57631.0_x64__8wekyb3d8bbwe`

`InstallLocation        : C:\Program Files\WindowsApps`

`\Microsoft.Office.OneNote_17.6769.57631.0_x64__8wekyb3d8bbwe`

`IsFramework            : False`

**`PackageFamilyName      : Microsoft.Office.OneNote_8wekyb3d8bbwe`**

`PublisherId            : 8wekyb3d8bbwe`



## <a name="find-a-pfn-if-the-app-is-not-installed-on-a-computer"></a>Поиск PFN-имени для приложения, не установленного на компьютере

1. Перейдите на страницу https://www.microsoft.com/store/apps.
2. Введите имя приложения в строке поиска. Мы выполняем поиск OneNote.
3. Щелкните ссылку на приложение. Обратите внимание, что в конце URL-адреса содержится последовательность букв. В нашем примере URL-адрес выглядит так: `https://www.microsoft.com/store/apps/onenote/9wzdncrfhvjl`
4. В другой вкладке вставьте следующий URL-адрес, `https://bspmts.mp.microsoft.com/v1/public/catalog/Retail/Products/<app id>/applockerdata`, заменив `<app id>` идентификатором приложения, полученным на странице https://www.microsoft.com/store/apps (последовательность букв в конце URL-адреса на шаге 3). В нашем примере OneNote вставьте: `https://bspmts.mp.microsoft.com/v1/public/catalog/Retail/Products/9wzdncrfhvjl/applockerdata`.

В Microsoft Edge будут выведены нужные сведения; в браузере Internet Explorer для просмотра сведений нажмите кнопку **Открыть**. Значение PFN указано в первой строке. Ниже приведены результаты для нашего примера:

``` JSON
{
  "packageFamilyName": "Microsoft.Office.OneNote_8wekyb3d8bbwe",
  "packageIdentityName": "Microsoft.Office.OneNote",
  "windowsPhoneLegacyId": "ca05b3ab-f157-450c-8c49-a1f127f5e71d",
  "publisherCertificateName": "CN=Microsoft Corporation, O=Microsoft Corporation, L=Redmond, S=Washington, C=US"
}
```
