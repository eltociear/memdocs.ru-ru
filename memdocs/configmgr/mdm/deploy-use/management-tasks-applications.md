---
title: Управление приложениями для локальной среды MDM
titleSuffix: Configuration Manager
description: Управление приложениями для локального управления мобильными устройствами (MDM) в Configuration Manager.
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 8adbe2e2-de26-4a80-8bbd-a5f34b8bac79
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 693f661f2a2db59335ec8e463842a0ad03c977f3
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724788"
---
# <a name="manage-apps-for-on-premises-mdm-in-configuration-manager"></a>Управление приложениями для локальной среды MDM в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

При управлении устройствами с помощью Configuration Manager локального управления мобильными устройствами (MDM) можно управлять следующими типами приложений:

- Пакет приложения Windows Phone (XAP-файл)
- Пакет приложения для ОС Windows Phone (в Магазине Windows)
- Установщик Windows через MDM (MSI)
- Веб-приложение

Дополнительные общие сведения об управлении Configuration Manager приложениями и типами развертывания см. в разделе [задачи управления для Configuration Manager приложений](../../apps/deploy-use/management-tasks-applications.md).

## <a name="create-windows-phone-application"></a><a name="bkmk_winphone"></a>Создание приложения Windows Phone

В приложении Configuration Manager доступны один или несколько типов развертывания. Тип развертывания включает файлы установки и сведения, необходимые для развертывания программного обеспечения на устройстве. Тип развертывания также содержит правила, определяющие время и способ развертывания программного обеспечения.

Общие шаги по созданию приложения и типов развертывания см. в разделе [Создание приложения](../../apps/deploy-use/create-applications.md#bkmk_create).

Configuration Manager поддерживает следующие типы файлов приложений для устройств Windows Mobile:

|Тип устройства|Поддерживаемые типы файлов|
|-----------------|---------------------|
|Windows Phone 8|xap|
|Windows Phone 8.1|xap, appx, appxbundle|
|Windows 10 Mobile|xap, appx, appxbundle|

Развертывайте приложения Windows Phone в статусе **Доступно** или **Необходимо**. Также используйте развертывание для удаления приложений.

## <a name="deploy-and-monitor-apps"></a>Развертывание и мониторинг приложений

Развертывайте и отслеживайте приложения для мобильных устройств в Configuration Manager так же, как и для других устройств, таких как настольные компьютеры и серверы. Дополнительные сведения см. в следующих статьях:

- [Развертывание приложений](../../apps/deploy-use/deploy-applications.md)
- [Мониторинг приложений](../../apps/deploy-use/monitor-applications-from-the-console.md)

Ознакомьтесь со следующими ограничениями, характерными для мобильных устройств.

- Устройства, зарегистрированные в системе управления мобильными устройствами, не поддерживают имитацию развертывания, взаимодействие с пользователем и параметры планирования.

- Не добавляйте в одно приложение более 100 языков. Это действие предотвращает установку приложения на устройстве.

## <a name="next-step"></a>Следующий шаг

Чтобы внести изменения, удалить или заменить развернутое приложение новым приложением, управляйте им так же, как любое приложение в Configuration Manager. Дополнительные сведения см. в статье [Обновление и прекращение использования приложений](../../apps/deploy-use/update-and-retire-applications.md).
