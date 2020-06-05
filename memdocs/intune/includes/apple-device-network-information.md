---
title: Включить имя файла
description: Включить файл
author: ErikjeMS
ms.service: microsoft-intune
ms.topic: include
ms.date: 06/02/2020
ms.author: erikje
ms.custom: include file
ms.openlocfilehash: bc8bb79d4f950edc303fb12504ef1a4a8dda9a64
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347270"
---
## <a name="apple-device-network-information"></a>Сведений о сети на устройстве Apple

|**Назначение**|**Имя узла (IP-адрес/подсеть)**|**Протокол**|**Порт**|
|------------|-----------|------------|-----------|
|Извлечение и отображение содержимого с серверов Apple|itunes.apple.com<br>\*.itunes.apple.com<br>\*.mzstatic.com<br>\*.phobos.apple.com<br>\*.phobos.itunes-apple.com.akadns.net|HTTP|80|
|Обмен данными с серверами APNS|#-courier.push.apple.com<br># — это случайное число от 0 до 50.|TCP|5223 и 443|
|Различные функциональные возможности, включая доступ к Интернету, магазину iTunes, магазину приложений macOS, iCloud, службе сообщений и т. д.|phobos.apple.com<br>ocsp.apple.com<br>ax.itunes.apple.com<br>ax.itunes.apple.com.edgesuite.net|HTTP/HTTPS|80 или 443|

Дополнительные сведения см. на странице

- [Порты TCP и UDP, используемые программными продуктами Apple](https://support.apple.com/HT202944)
- [Сведения о подключениях узлов серверов macOS, iOS/iPadOS и iTunes и фоновых процессах iTunes](https://support.apple.com/HT201999)
- [Если клиенты macOS и iOS/iPadOS не получают push-уведомления Apple](https://support.apple.com/HT203609)