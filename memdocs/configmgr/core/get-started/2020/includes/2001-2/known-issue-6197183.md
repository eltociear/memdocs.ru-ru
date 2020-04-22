---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 02/03/2020
ms.openlocfilehash: 0db30a8fdc96bc1e1d2d1ff2a059eca8d454d48e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692102"
---
### <a name="cant-create-or-edit-some-collections"></a><a name="ki_coll"></a> Не удается создать или изменить некоторые коллекции

<!--6197183-->
В этой версии ветви Technical Preview отсутствует возможность создать новую коллекцию. Также не удастся изменить свойства существующей коллекции пользователя.

Чтобы обойти эту ошибку, используйте командлеты PowerShell Configuration Manager для создания новых коллекций и редактирования существующих коллекций пользователей. Ниже перечислены некоторые из доступных командлетов для управления коллекциями.

- [New-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmcollection?view=sccm-ps)

- [Get-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollection?view=sccm-ps)

- [Set-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmcollection?view=sccm-ps#related-links)

- [Add-CMCollectionMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/add-cmcollectionmembershiprule?view=sccm-ps)
