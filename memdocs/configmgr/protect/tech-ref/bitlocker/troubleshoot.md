---
title: Устранение неполадок BitLocker
titleSuffix: Configuration Manager
description: Дополнительные сведения об устранении неполадок, связанных с управлением BitLocker в Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 134c5b50-edeb-4d60-aaca-944d26deb9ba
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ed8e464e0ab7c17e87e3de2bf72aa0dfb0acd071
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708612"
---
# <a name="troubleshoot-bitlocker"></a>Устранение неполадок BitLocker

*Область применения: Configuration Manager (Current Branch)*

Используйте сведения в этой статье для устранения неполадок, связанных с управлением BitLocker в Configuration Manager.

## <a name="server-error-in-self-service"></a>Ошибка сервера при самообслуживании

При первой попытке открыть портал самообслуживания (`https://webserver.contoso.com/SelfService`) отображается следующее сообщение об ошибке.

``` error
Configuration Error - Server Error in '/SelfService' Application

Description: An error occurred during the processing of a configuration file required to service this request. Please review the specific error details below and modify your configuration file appropriately.

Parser Error Message: Could not load file or assembly 'System.Web.Mvc, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' or one of its dependencies. The system cannot find the file specified.
```

Чтобы устранить эту проблему, убедитесь, что вы выполнили на веб-сервере все [требования](../../plan-design/bitlocker-management.md#prerequisites) для **Microsoft ASP.NET MVC 4.0**.

## <a name="see-also"></a>См. также

Дополнительные сведения об использовании журналов событий BitLocker см. в статье [Журналы событий BitLocker](about-event-logs.md).

Список известных ошибок и возможные причины создания записей в журнале событий см. в следующих статьях:

- [Журналы событий клиента](client-event-logs.md)
- [Журналы событий сервера](server-event-logs.md)

Сведения о том, почему клиенты сообщают о несоответствии политике управления BitLocker, см. в разделе [Коды несоответствия](non-compliance-codes.md).
