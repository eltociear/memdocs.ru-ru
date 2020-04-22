---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 02/13/2020
ms.openlocfilehash: 54e00688c1375f9ec54ada86d2b2c4b9347d5405
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81691852"
---
### <a name="cant-delete-collections"></a><a name="ki_coll"></a> Не удается удалить коллекции

<!--6245446-->
В этой ветви технической версии отсутствует возможность удаления коллекций.

Чтобы обойти эту ошибку, используйте для удаления коллекций следующий командлет PowerShell Configuration Manager:

- [Remove-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollection?view=sccm-ps)
