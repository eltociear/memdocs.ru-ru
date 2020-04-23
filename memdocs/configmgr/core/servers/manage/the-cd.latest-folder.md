---
title: Папка CD.Latest
titleSuffix: Configuration Manager
description: Узнайте, как выполнять процесс доставки обновлений из консоли Configuration Manager.
ms.date: 03/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8db92d67-5d9c-4e9c-80d0-ae6fa0dd4817
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 577bfd865ad3872c386384c3bba95cb009ef83ec
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704052"
---
# <a name="the-cdlatest-folder-for-configuration-manager"></a>Папка CD.Latest для Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Configuration Manager поддерживает процесс доставки обновлений из консоли Configuration Manager. Этот новый метод обновления Configuration Manager предусматривает создание папки с именем **CD.Latest**. В этой папке находятся копии файлов установки Configuration Manager для обновленной версии сайта.  

Папка CD.Latest содержит папку с именем **Redist**, в которой находятся распространяемые файлы, скачиваемые и используемые программой установки. Эти файлы сопоставляются с версией файлов Configuration Manager, содержащихся в папке CD.Latest. При запуске программы установки из папки CD.Latest необходимо использовать файлы, соответствующие данной версии программы установки. Программу установки можно настроить на скачивание нужных файлов с веб-сайта Майкрософт или на использование файлов из папки Redist, находящейся в папке CD.Latest.

На базовом носителе папка **Redist** отсутствует. На сайте папка Redist не создается, пока вы не установите обновление из консоли. Пока же вы можете использовать папку Redist, которую применяли при установке сайтов с базового носителя.  

> [!TIP]  
> Убедитесь, что используются актуальные распространяемые файлы. Если вы недавно не скачивали распространяемые файлы, настройте программу установки на получение файлов с веб-сайта Майкрософт.   

Ниже описаны сценарии, в которых папка CD.Latest создается или обновляется на сайте центра администрирования или сервере первичного сайта.  

- При установке обновления или исправления из консоли Configuration Manager эта папка создается или обновляется на сайте в папке установки Configuration Manager.  

- При запуске встроенной задачи резервного копирования Configuration Manager эта папка создается или обновляется на сайте в папке, указанной для резервного копирования.  

- При установке сайта с помощью базового носителя на сайте создается папка CD.Latest.


## <a name="supported-scenarios"></a>Поддерживаемые сценарии

Исходные файлы из папки CD.Latest используются в таких сценариях:  

### <a name="backup-and-recovery"></a>резервное копирование и восстановление
Для восстановления сайта используйте исходные файлы из папки CD.Latest, соответствующие вашему сайту. Если резервное копирование сайта выполняется с помощью встроенной задачи резервного копирования, для папки CD.Latest также создается резервная копия.

- При переустановке сайта в ходе его восстановления установка выполняется из папки CD.Latest, содержащейся в резервной копии. При этом используются версии файлов, которые соответствуют резервной копии сайта и базы данных сайта.  

    - Если у вас нет доступа к нужной версии папки CD.Latest, создайте ее с нужными версиями файлов, установив сайт в лабораторной среде. Затем обновите сайт до той версии, которую вы хотите восстановить.  

    - Если нужная папка CD.Latest и ее содержимое недоступны, вы не можете восстановить сайт. В этом случае необходимо переустановить сайт.  

- Если у вас нет папки CD.Latest, но есть рабочий дочерний первичный сайт или сайт центра администрирования, вы можете использовать такой сайт в качестве эталонного сайта для восстановления.  

### <a name="install-a-child-primary-site"></a>Установка дочернего первичного сайта
Когда требуется установить новый дочерний первичный сайт в иерархии сайта центра администрирования, на котором установлено одно или несколько обновлений через консоль, используйте программу установки и исходные файлы из папки CD.Latest на сайте центра администрирования. При этом используются установочные файлы, соответствующие версии сайта центра администрирования. Дополнительные сведения см. в разделе [Использование мастера установки для установки сайтов](../deploy/install/use-the-setup-wizard-to-install-sites.md).  

### <a name="expand-a-stand-alone-primary-site"></a>Развертывание автономного первичного сайта
Когда вы развертываете автономный первичный сайт, устанавливая новый сайт центра администрирования, используйте программу установки и исходные файлы из папки CD.Latest на первичном сайте. При этом используются установочные файлы, соответствующие версии первичного сайта. Дополнительные сведения см. в разделе [Расширение автономного первичного сайта](../deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand).

### <a name="install-a-secondary-site"></a>Установка вторичного сайта
<!-- SCCMDocs-pr issue #3164 -->
Когда требуется установить новый вторичный сайт в иерархии первичного сайта, на котором установлено одно или несколько обновлений через консоль, используйте исходные файлы из папки CD.Latest на первичном сайте. 

Дополнительные сведения см. в разделе [Установка вторичного сайта](../deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_secondary). 


## <a name="unsupported-scenarios"></a>Неподдерживаемые сценарии

Обновленные исходные файлы в папке CD.Lates не подходят для таких целей:  

- Установка нового сайта для новой иерархии.  
- Обновление сайта Microsoft System Center 2012 Configuration Manager до Configuration Manager (Current Branch)
- Установка клиентов Configuration Manager.
- Установка консолей Configuration Manager.