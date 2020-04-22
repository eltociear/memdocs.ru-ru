---
title: Международная поддержка
titleSuffix: Configuration Manager
description: Настройка Configuration Manager в соответствии с определенными международными требованиями.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 46dd9cb2-a812-4b6a-a747-b840f92fef8b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 05e90466ec3ee9529e4eb770839347ad7ac94447
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704602"
---
# <a name="international-support-in-configuration-manager"></a>Международная поддержка в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

В следующих разделах приводятся технические сведения, помогающие привести Configuration Manager в соответствие с определенными международными требованиями.  

## <a name="gb18030-requirements"></a>Требования GB18030  
 Configuration Manager отвечает стандартам, установленным в GB18030, поэтому Configuration Manager можно использовать в Китае. Для соответствия требованиям GB18030 при развертывании Configuration Manager должны использоваться следующие конфигурации.  

-   На каждом компьютере сервера сайта и компьютере с SQL Server, используемом с Configuration Manager, должна быть установлена операционная система на китайском языке.  

-   В базе данных каждого сайта и в каждом экземпляре SQL Server в иерархии должна использоваться одна и та же сортировка, а именно:  

    -   Chinese_Simplified_Pinyin_100_CI_AI  

    -   Chinese_Simplified_Stroke_Order_100_CI_AI  

    > [!NOTE]  
    >  Такие параметры сортировки являются исключением из требований, описанных в статье [Поддержка версий SQL Server в Configuration Manager](../../../core/plan-design/configs/support-for-sql-server-versions.md).  

-   Необходимо разместить файл с именем **GB18030.SMS** в корневой папке системного тома на каждом компьютере сервера сайта в иерархии. Этот файл не содержит данных и может представлять собой пустой текстовый файл с именем, соответствующим данному требованию.  
