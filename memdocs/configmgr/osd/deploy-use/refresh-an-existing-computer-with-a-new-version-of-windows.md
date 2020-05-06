---
title: Обновление ОС на существующем компьютере
titleSuffix: Configuration Manager
description: Configuration Manager позволяет использовать несколько методов для создания и форматирования разделов на существующем компьютере и установки на нем новой ОС.
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b189a346-8c0d-4870-a876-0719fbb0ab04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9582d6840e1f750d53504da4e8e7f6bf54f44965
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708412"
---
# <a name="refresh-an-existing-computer-with-a-new-version-of-windows"></a>Обновление существующего компьютера до новой версии Windows

*Область применения: Configuration Manager (Current Branch)*

Configuration Manager позволяет создавать и форматировать разделы на существующем компьютере и устанавливать на нем новую ОС. Этот процесс иногда называется *пересозданием образа* или *очисткой и загрузкой*. В этом сценарии вы можете выбирать самые разные методы развертывания, например PXE, загрузочный носитель или Центр программного обеспечения. Можно также использовать точку миграции состояния для хранения параметров, а затем восстановить их в новой ОС.

Чтобы выбрать правильный сценарий развертывания ОС, см. раздел [Сценарии развертывания операционных систем предприятия](scenarios-to-deploy-enterprise-operating-systems.md).  

## <a name="plan"></a><a name="BKMK_Plan"></a> План  

### <a name="plan-for-and-implement-infrastructure-requirements"></a>Планирование и реализация требований к инфраструктуре

Имеется ряд требований к инфраструктуре, которые должны быть удовлетворены перед развертыванием ОС. Помимо прочего, к ним относятся наличие Windows ADK, средства миграции пользовательской среды (USMT) и служб развертывания Windows (WDS). Дополнительные сведения см. в статье [Требования к инфраструктуре для развертывания операционной системы](../plan-design/infrastructure-requirements-for-operating-system-deployment.md).  

### <a name="install-a-state-migration-point"></a>Установка точки миграции состояния

Если вы хотите сохранить параметры с существующего компьютера, а затем восстановить их в новой ОС, рекомендуется использовать точку миграции состояния. Дополнительные сведения см. в разделе [Точка миграции состояния](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints).  

## <a name="configure"></a><a name="BKMK_Configure"></a> Настройка  

### <a name="prepare-a-boot-image"></a>Подготовка загрузочного образа

Загрузочные образы запускают компьютер в среде Windows PE. Windows PE — это минимальная ОС с ограниченным набором компонентов и служб. Затем из Windows PE Configuration Manager может установить на компьютере полную ОС Windows.

Дополнительные сведения см. в следующих статьях:

- [Управление загрузочными](../get-started/manage-boot-images.md) образами

- [Настройка загрузочных образов](../get-started/customize-boot-images.md)

- [Распространение содержимого](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)

### <a name="prepare-an-os-image"></a>Подготовка образа ОС

Образ ОС содержит файлы, необходимые для установки ОС на конечном компьютере.

Дополнительные сведения см. в следующих статьях:

- [Управление образами ОС](../get-started/manage-operating-system-images.md)

- [Распространение содержимого](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)

### <a name="create-a-task-sequence-to-deploy-an-os"></a>Создание последовательности задач для развертывания ОС

Используйте последовательности задач для автоматизации установки ОС. В зависимости от выбранного метода развертывания могут потребоваться и другие действия для последовательности задач.

Дополнительные сведения см. в следующих статьях:

- [Создание последовательности задач для установки ОС](create-a-task-sequence-to-install-an-operating-system.md)

- [Управление пользовательской средой](../get-started/manage-user-state.md)

## <a name="deploy"></a><a name="BKMK_Deploy"></a> Развернуть

- Используйте один из следующих методов для развертывания ОС:  

  - [Использование PXE для развертывания Windows по сети](use-pxe-to-deploy-windows-over-the-network.md)  

  - [Использование многоадресной рассылки для развертывания Windows по сети](use-multicast-to-deploy-windows-over-the-network.md)  

  - [Создание образа для изготовителей оборудования в фабрике или локальном хранилище](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

  - [Использование автономного носителя для развертывания Windows без применения сети](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

  - [Использование загрузочного носителя для развертывания Windows по сети](use-bootable-media-to-deploy-windows-over-the-network.md)  

  - [Использование центра программного обеспечения для развертывания Windows по сети](use-software-center-to-deploy-windows-over-the-network.md)  

## <a name="monitor"></a>Монитор  

Дополнительные сведения см. в разделе [Мониторинг развертываний ОС](monitor-operating-system-deployments.md).  

> [!Note]
> При повторном создании образа устройства UEFI диспетчер загрузки Windows создает новую запись в загрузчике. Это поведение особенно заметно при многократном повторном создании образа устройства, например в тестовой или лабораторной среде. Обычно оно не влияет на производительность или использование устройства. Если список становится слишком велик, на некоторых устройствах могут начаться проблемы с функциональностью. Например, это может быть невозможность загрузки с внешнего USB-накопителя или выбора текущей загрузочной записи из списка. Чтобы очистить ненужные загрузочные записи, используйте команду Windows **bcdedit**. Дополнительные сведения см. в статье [BCDEdit /deletevalue](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--deletevalue).<!-- 2841926 -->
