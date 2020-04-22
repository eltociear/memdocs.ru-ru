---
title: Использование многоадресной рассылки для развертывания Windows по сети
titleSuffix: Configuration Manager
description: С помощью многоадресной рассылки в среде Configuration Manager можно обеспечить одновременное скачивание образа операционной системы несколькими компьютерами.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 4cafb7fc-380b-41b1-b83e-045aebfb7131
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f81b23d3783d397d83a3925b98c0c8f601fa4012
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703492"
---
# <a name="use-multicast-to-deploy-windows-over-the-network-with-configuration-manager"></a>Использование многоадресной рассылки для развертывания Windows по сети с Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Многоадресная рассылка — это метод оптимизации сети, который можно использовать в средах Configuration Manager, где высока вероятность того, что несколько клиентов будут одновременно загружать один образ операционной системы. Когда используется многоадресная рассылка, несколько компьютеров могут одновременно загружать образ операционной системы, рассылаемый точкой распространения. Этот механизм заменяет сценарий отправки точкой распространения копии данных на каждый клиентский компьютер через отдельное подключение.  

 Вы можете развертывать операционные системы по сети с использованием многоадресной рассылки в следующих сценариях развертывания операционной системы:  

- [Обновление существующего компьютера до новой версии Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

- [Установка новой версии Windows на новом компьютере (без операционной системы)](install-new-windows-version-new-computer-bare-metal.md)  

  Выполните действия, указанные для одного из сценариев развертывания операционной системы, а затем используйте сведения из приведенных ниже разделов для обеспечения поддержки многоадресной рассылки.  

##  <a name="configure-a-distribution-point-to-support-multicast"></a><a name="BKMK_Configure"></a> Настройка точки распространения для обеспечения поддержки многоадресной рассылки  
 Перед использованием многоадресной рассылки при развертывании операционной системы необходимо настроить точку распространения на поддержку такой рассылки. Дополнительные сведения см. в разделе [Установка и настройка точек распространения](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-multicast). Список портов, необходимых для поддержки многоадресной рассылки, см. в статье [Порты](../../core/plan-design/hierarchy/ports.md#BKMK_PortsClient-DP2).  

## <a name="prepare-an-operating-system-image-for-multicast-deployments"></a>Подготовка образа операционной системы для многоадресных развертываний  
 Сведения о настройке пакета образа операционной системы для поддержки многоадресной рассылки см. в разделе [Подготовка образа операционной системы для многоадресных развертываний](../get-started/manage-operating-system-images.md#BKMK_OSImageMulticast).  

##  <a name="deploy-the-task-sequence"></a><a name="BKMK_Deploy"></a> Развертывание последовательности задач  
 Выполните развертывание операционной системы в целевой коллекции. Дополнительные сведения см. в статье [Deploy a task sequence](deploy-a-task-sequence.md).  
