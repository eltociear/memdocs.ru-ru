---
title: Сосуществование сторонних решений по MDM
titleSuffix: Configuration Manager
description: Узнайте об использовании сторонней службы MDM с Configuration Manager
ms.date: 05/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: ed4dc65e-e5d5-4f75-88ac-f4849ec8fc10
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f22ba6f29e0c85e19ab66d1b052085db5303cc2c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690312"
---
# <a name="third-party-mdm-coexistence-with-configuration-manager"></a>Сосуществование сторонних решений по MDM с Configuration Manager

Функция [совместного управления](overview.md) позволяет параллельно управлять устройствами Windows 10 с помощью Configuration Manager и Microsoft Intune. Когда вы управляете устройствами с помощью Configuration Manager и регистрируетесь в сторонней службе MDM, эта функция называется *сосуществованием*. Наличие двух центров управления для одного устройства может быть проблематичным, если неправильно организована оркестрация между ними. Благодаря совместному управлению Configuration Manager и Intune выполняют балансировку [рабочих нагрузок](workloads.md), чтобы избежать конфликтов. Это взаимодействие недоступно для сторонних служб, поэтому существуют ограничения для возможностей управления при сосуществовании.

Клиент Configuration Manager может сосуществовать со сторонней службой MDM на устройстве с Windows 10 версии 1709 или более поздней, подключенном к Azure Active Directory. Устройство может иметь один из следующих типов.

- [Присоединенное только к Azure AD](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan). (Этот тип иногда называют "присоединенным к облачному домену".)  

- [Гибридные устройства, присоединенные к домену](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan), если устройство присоединено к локальной среде Active Directory и зарегистрировано в Azure Active Directory.  

> [!Note]  
> [Личные устройства](https://docs.microsoft.com/windows/client-management/mdm/mdm-enrollment-of-windows-devices#connecting-personally-owned-devices-bring-your-own-device) не поддерживаются.  

Когда клиент Configuration Manager обнаруживает, что сторонняя служба MDM также управляет устройством, он автоматически деактивирует определенные рабочие нагрузки в Configuration Manager. Такое поведение позволяет службе MDM взять на себя эти функции. Это также предотвращает возникновение конфликтующих параметров в клиенте, которые могут негативно повлиять на устройство и взаимодействие с пользователем. В этом случае деактивируются следующие рабочие нагрузки в Configuration Manager:

- Политики доступа к ресурсам для настройки параметров VPN, Wi-Fi, электронной почты и сертификатов.
- Управление приложениями, включая устаревшие пакеты.
- Сканирование и установка обновлений программного обеспечения.
- Endpoint Protection — пакет Защитника Windows с набором функций защиты от вредоносных программ.
- Управление политикой соответствия для условного доступа.
- Конфигурация устройства
- Управление Office "нажми и работай".

Клиент Configuration Manager избегает конфликта со сторонним центром управления, продолжая выполнять следующие операции "только для чтения":

- Наличие оборудования и программного обеспечения
- Аналитика активов
- Контроль использования программных продуктов
- Создание отчетов об управлении питанием.

Дополнительные сведения о преимуществах совместного управления с использованием Configuration Manager и Intune см. в разделе [Преимущества](overview.md#benefits).
