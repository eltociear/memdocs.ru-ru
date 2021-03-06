---
title: Развертывание нескольких профилей OEMConfig на устройствах Zebra с помощью Microsoft Intune | Документация Майкрософт
description: Используйте Microsoft Intune для создания и развертывания нескольких профилей конфигурации устройств OEMConfig на устройствах Zebra под управлением Android для бизнеса. Используйте действия и шаги Zebra для упорядочения профилей.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/12/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: ''
ms.technology: ''
ms.assetid: ''
ms.reviewer: jieyan
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2227face347e6d82cf7807bea241eda4856c1d67
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988689"
---
# <a name="deploy-multiple-oemconfig-profiles-to-zebra-devices-in-microsoft-intune"></a>Развертывание нескольких профилей OEMConfig на устройствах Zebra в Microsoft Intune

Используйте приложение OEMConfig в Microsoft Intune, чтобы настроить параметры, относящиеся к изготовителям оборудования, для устройств Android для бизнеса. Эти параметры относятся к производителю устройства и развертываются с помощью профилей конфигурации в Intune.

На устройствах Zebra можно развернуть и назначить несколько профилей одному устройству. Существующие профили OEMConfig смогут использовать эту функцию после следующей синхронизации устройств с Intune.

Данная функция применяется к:

- устройствам Zebra под управлением Android для бизнеса

Дополнительные сведения об OEMConfig, в том числе о его функциях и использовании, см. в разделе [Профиль конфигурации OEMConfig](android-oem-configuration-overview.md).

В этой статье описывается развертывание нескольких профилей OEMConfig на устройствах Zebra, принципы упорядочения и использования функций отчетов в Microsoft Intune.

## <a name="prerequisites"></a>Предварительные условия

Создайте [профиль конфигурации OEMConfig](android-oem-configuration-overview.md).

## <a name="use-multiple-profiles"></a>Использование нескольких профилей

На устройствах Zebra можно использовать несколько профилей одновременно. Эта функция позволяет разделить параметры Zebra OEMConfig между более мелкими профилями. Схема OEMConfig для Zebra также использует **действия**. Действия — это операции, выполняемые на устройстве. Они не связаны с настройкой каких-либо параметров. Используйте действия, чтобы активировать скачивание файла, очистить буфер обмена и т. д. Полный список поддерживаемых действий см. в [документации по Zebra](https://techdocs.zebra.com/oemconfig/10-0/about/) (на веб-сайте Zebra).

Например, вы создали профиль OEMConfig для Zebra, который применяет к устройству некоторые параметры. Другой профиль OEMConfig для Zebra включает действие, которое очищает буфер обмена. Первый профиль назначается группе устройств Zebra. Затем вам необходимо очистить буфер обмена на этих устройствах. Вы назначаете второй профиль той же группе устройств без изменения первого профиля. Буфер обмена устройства очищается без повторной отправки или какого-либо воздействия на параметры конфигурации первого профиля.

В другом примере вы назначили профиль OEMConfig, который настраивает некоторые параметры устройства Zebra. Недавно пользователи жаловались на проблемы с конкретным приложением, и вы хотите очистить кэш приложения. Создайте новый профиль OEMConfig, включающий только действие очистки кэша. Назначьте его устройствам, которым необходимо это действие.

## <a name="ordering"></a>Упорядочение

Если на устройстве присутствует несколько профилей, порядок их развертывания может быть любым. Такое поведение связано с ограничением Google Play. Для запуска операций в определенной последовательности можно использовать [функцию транзакций Zebra](https://techdocs.zebra.com/oemconfig/9-1/mc/) (на веб-сайте Zebra). Давайте рассмотрим пример.

Существует два профиля.

- **Профиль 1**: включает Bluetooth. Этот профиль назначается в понедельник группе **Все устройства**.
- **Профиль 2**: настраивает любой другой параметр. Этот профиль назначается во вторник группе **Все устройства**.

Перед настройкой другого параметра необходимо включить Bluetooth.

В среду вы регистрируете 10 новых устройств Zebra с помощью Intune. Профиль 1 и профиль 2 назначаются группе **Все устройства**. После синхронизации новых устройств с Intune они получат эти профили. Но они могут получить профиль 2 раньше, чем профиль 1.

Используйте функцию **Шаги** в схеме Zebra, чтобы подтвердить последовательность выполнения операций. В этом случае создается один профиль с двумя шагами транзакций. Первый шаг включает параметры Bluetooth, а на втором шаге настраивается другой параметр. Когда приложение OEMConfig на устройстве Zebra получает профиль, оно выполняет шаги по порядку, заданному в Zebra.

Дополнительные сведения см. в разделе [Шаги транзакций Zebra](https://techdocs.zebra.com/oemconfig/9-1/mc/) (на веб-сайте Zebra).

## <a name="enhanced-reporting"></a>Расширенные отчеты

Вы развернули профиль, и он выполняется в приложении Zebra OEMConfig на устройстве. Приложение Zebra OEMConfig сообщает о состоянии профиля в Intune. В центре администрирования Endpoint Manager можно просмотреть состояние развернутых профилей OEMConfig, а также все ошибки и предупреждения.

1. Откройте [центр администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Выберите профиль Zebra OEMConfig > **Отслеживать** > **Состояние устройства**. Этот параметр показывает устройства, которым назначен этот профиль OEMConfig.
3. Выберите устройство > **Конфигурация устройства** > выберите профиль Zebra OEMConfig. Этот параметр показывает успешно примененные параметры профиля и те, которые применить не удалось.

    Выберите строку с параметром, который не был применен. Отображаются подробные сведения о причинах сбоя.

## <a name="next-steps"></a>Дальнейшие шаги

- Дополнительные сведения см в разделе [Профили конфигурации OEMConfig](android-oem-configuration-overview.md).
- В администраторе устройств Android настройте [Расширения для мобильности (MX)](android-zebra-mx-overview.md).
- [Отслеживание состояния профиля](device-profile-monitor.md).
