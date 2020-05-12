---
title: Настраиваемые расположения для файлов базы данных
titleSuffix: Configuration Manager
description: Узнайте, как задать настраиваемые расположения для файлов базы данных SQL Server.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 500a9aa6-68aa-44eb-bf49-350c1314a697
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d3f01e54ba196ee9c27295d8f970a7dbe352f63f
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906193"
---
# <a name="custom-locations-for-configuration-manager-site-database-files"></a>Настраиваемые расположения для файлов базы данных сайта Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

 Configuration Manager поддерживает настраиваемые расположения для файлов базы данных SQL Server.  

> [!NOTE]  
>  При использовании кластера SQL Server возможность указания расположений файлов не по умолчанию недоступна.  

 **Во время установки** нового первичного сайта или сайта центра администрирования вы можете:  

-   **Указать нестандартные расположения для базы данных сайта** — программа установки Configuration Manager создаст базу данных сайта, используя эти расположения.  

-   **Задать использование предварительно созданной базы данных SQL Server, которая использует настраиваемые расположения файлов** —  программа установки Configuration Manager будет использовать эту заранее созданную базу данных и ее предварительно настроенные расположения файлов.  

**После установки** вы можете изменить расположение файлов базы данных сайта. Для этого необходимо остановить сайт и изменить расположение файлов в SQL Server.  

-   На сервер сайта Configuration Manager остановите службу **SMS_Executive**.  

-   Дополнительные сведения о перемещении пользовательской базы данных см. в [этой статье](https://docs.microsoft.com/sql/relational-databases/databases/move-user-databases?view=sql-server-2014).  

-   После перемещения файлов базы данных перезапустите службу **SMS_Executive** на сервере сайта Configuration Manager.  
