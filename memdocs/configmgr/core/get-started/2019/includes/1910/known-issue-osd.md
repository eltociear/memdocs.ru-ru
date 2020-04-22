---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 10/17/2019
ms.openlocfilehash: 668db6aa10fbee0a078eef04f0560973e5ed9454
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697852"
---
### <a name="task-sequences-arent-available-to-pxe-or-media"></a><a name="ki_osd"></a> Последовательности задач недоступны для PXE или носителей

<!--5578298-->
При развертывании последовательности задач для PXE или носителя (USB или DVD) клиент не получает политику. Следующее сообщение указано в **smsts.log**:

`There are no task sequences available to this computer.`

#### <a name="workaround"></a>Обходной путь

Запустите последовательность задач из центра программного обеспечения.
