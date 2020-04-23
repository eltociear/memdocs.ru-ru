---
title: Установка Windows на новый компьютер
titleSuffix: Configuration Manager
description: Используйте Configuration Manager для установки операционной системы на новом компьютере без ОС с помощью PXE, OEM-установки или автономного носителя.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: f5ad22d5-7df1-49c6-8a0f-db1c3f0cda19
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6a70269839b4a550fbef4dc5cab1b7ff3d426d87
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690672"
---
# <a name="install-a-new-version-of-windows-on-a-new-computer-bare-metal-with-configuration-manager"></a>Установка новой версии Windows на новом компьютере (без операционной системы) с помощью Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Этот раздел содержит общие шаги в Configuration Manager по установке операционной системы на новый компьютер. В этом сценарии можно выбирать из множества различных способов развертывания, таких как PXE, поставщик вычислительной техники или автономный носитель. Если вы не уверены, что этот сценарий развертывания операционной системы вам подходит, см. раздел [Сценарии развертывания операционных систем предприятия](scenarios-to-deploy-enterprise-operating-systems.md).  

Используйте сведения в следующих разделах для обновления существующего компьютера до новой версии Windows.  

##  <a name="plan"></a><a name="BKMK_Plan"></a> План  

-   **Планирование и реализация требований к инфраструктуре**  

     Существует ряд требований к инфраструктуре, которые должны быть выполнены перед развертыванием операционных систем, например наличие Windows ADK, служб развертывания Windows (WDS), поддерживаемых конфигураций жестких дисков и т. д. Дополнительные сведения см. в разделе [Требования к инфраструктуре для развертывания операционной системы](../plan-design/infrastructure-requirements-for-operating-system-deployment.md).

##  <a name="configure"></a><a name="BKMK_Configure"></a> Настройка  

1.  **Подготовка загрузочного образа**  

     Образы загрузки запускают компьютер в среде Windows PE (минимальная операционная система с ограниченным набором компонентов и служб), в которой потом можно установить полную операционную систему Windows на компьютере.   При развертывании операционных систем необходимо выбрать образ загрузки и распространить его в точку распространения. Используйте следующие сведения для подготовки образа:  

    -   Дополнительные сведения об образах загрузки см. в разделе [Управление загрузочными образами](../get-started/manage-boot-images.md).  

    -   Дополнительные сведения о настройке образа загрузки см. в разделе [Настройка загрузочных образов](../get-started/customize-boot-images.md).  

    -   Распространите загрузочный образ в точки распространения. Дополнительные сведения см. в разделе [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

2.  **Подготовка образа операционной системы**  

     Образ операционной системы содержит файлы, необходимые для установки операционной системы на конечный компьютер. Используйте следующие сведения для подготовки образа операционной системы:  

    -   Дополнительные сведения о создании образа операционной системы см. в разделе [Управление образами операционных систем](../get-started/manage-operating-system-images.md).

    -   Распространите образ в точки распространения. Дополнительные сведения см. в разделе [Распространение содержимого](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

    > [!NOTE]
    > Новые установки Windows можно выполнить из исходных файлов установки через пакеты обновления ОС, но использовать вместо этого образы операционной системы, например **install.wim**.
    >
    > Развертывание новых установок Windows с помощью пакетов обновления ОС по-прежнему поддерживается, но зависит от драйверов, совместимых с этим методом. При выполнении установок Windows из пакета обновления ОС драйверы устанавливаются, находясь в Windows PE, а не просто внедряются в Windows PE. Некоторые драйверы невозможно установить, когда они находятся в Windows PE. Если драйверы невозможно установить, когда они находятся в Windows PE, то используйте образ операционной системы.  

3.  **Создание последовательности задач для развертывания операционных систем по сети**  

     Используйте последовательности задач для автоматизации установки операционной системы по сети. Инструкции по созданию последовательности задач для развертывания операционной системы см. в разделе [Создание последовательности задач для установки операционной системы](create-a-task-sequence-to-install-an-operating-system.md). В зависимости от выбранного метода развертывания могут потребоваться и другие действия для последовательности задач.  

##  <a name="deploy"></a><a name="BKMK_Deploy"></a> Развернуть  

-   Используйте один из следующих методов для развертывания операционной системы:  

    -   [Использование PXE для развертывания Windows по сети](use-pxe-to-deploy-windows-over-the-network.md)  

    -   [Использование многоадресной рассылки для развертывания Windows по сети](use-multicast-to-deploy-windows-over-the-network.md)  

    -   [Создание образа для изготовителей оборудования в фабрике или локальном хранилище](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

    -   [Использование автономного носителя для развертывания Windows без применения сети](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

    -   [Использование загрузочного носителя для развертывания Windows по сети](use-bootable-media-to-deploy-windows-over-the-network.md)  

## <a name="monitor"></a>Монитор  

-   **Мониторинг развертывания последовательности задач**  

     Сведения о мониторинге развертывания последовательности задач для установки операционной системы см. в разделе [Мониторинг развертываний операционных систем](monitor-operating-system-deployments.md).  