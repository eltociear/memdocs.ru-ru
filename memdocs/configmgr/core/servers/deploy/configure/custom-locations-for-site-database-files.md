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
ms.openlocfilehash: cc7eb1a8ba721545bdee50d45887ab9d3aa8e952
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704702"
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

-   Следуйте инструкциям по перемещению пользовательской базы данных, приведенным в документации для вашей версии SQL Server. Например, если вы используете SQL Server 2014, см. статью [Перемещение пользовательских баз данных](https://technet.microsoft.com/library/ms345483\(v=sql.120\).aspx) на сайте TechNet.  

-   После перемещения файлов базы данных перезапустите службу **SMS_Executive** на сервере сайта Configuration Manager.  
