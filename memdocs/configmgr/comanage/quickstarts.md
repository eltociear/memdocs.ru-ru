---
title: Облачные подключения при использовании совместного управления
titleSuffix: Configuration Manager
description: Совместное управление предлагает прямые преимущества сразу при подключении.
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 8d878443-90e7-46e4-9cd3-99e2a19b2ad0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ebadb47ca67f331ac88f8947b396438893e12386
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690872"
---
# <a name="cloud-connecting-with-co-management"></a>Облачные подключения при использовании совместного управления

![Баннер из серии "Взлет"](media/blastoff-banner.png)

Совместное управление дополняет существующее развертывание Configuration Manager новыми функциями, не изменяя используемых методов работы. Включив совместное управление, вы немедленно получите преимущества от использования облака. Эти преимущества можно применить к существующей инфраструктуре и процессам управления.

В этой серии кратких руководств по совместному управлению вы узнаете, как можно быстро улучшить систему управления. Совместное управление проектировалось так, чтобы предоставить вам функции и средства для немедленного использования.

В следующем видео корпоративный вице-президент корпорации Майкрософт Брэд Андерсон (Brad Anderson) расскажет вам об этой серии по совместному управлению:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Cloud-Connecting-with-Co-Management/player]

| Значение интерпретации | начало работы |
|-----------------|-----------------|
| - [Условный доступ](#bkmk_ca)<br> - [Действия, выполняемые удаленно из Intune](#bkmk_remote)<br> - [Работоспособность клиента](#bkmk_client-health)<br> - [Гибридное присоединение к Azure AD](#bkmk_hybrid-aad)<br> - [Windows Autopilot](#bkmk_autopilot) | - [Пути для совместного управления](#bkmk_paths)<br> - [Настройка гибридного экземпляра Azure AD](#bkmk_setup-hybrid-aad)<br> - [Обновление до Windows 10](#bkmk_upgrade-win10)<br> - [Получение справки FastTrack](#bkmk_fasttrack) |

## <a name="immediate-value"></a>Значение интерпретации

| | | |
|-|-|-|
| <a name="bkmk_ca"></a>**Условный доступ на основе соответствия устройств требованиям** | Доступ пользователей к корпоративным ресурсам на основе правил соответствия из Intune. | [![Эскиз видео об условном доступе](media/thumbnail-conditional-access.png)](quickstart-conditional-access.md) |
| <a name="bkmk_remote"></a>**Действия, выполняемые удаленно из Intune** | Запуск удаленных действий из Intune для совместно управляемых устройств. Например, очистка и сброс настроек устройства или поддержка регистрации и учетных записей. | [![Эскиз видео об удаленных действиях](media/thumbnail-remote-action.png)](quickstart-remote-actions.md) |
| <a name="bkmk_client-health"></a>**Работоспособность клиента Configuration Manager** | Сведения о контроле работоспособности клиента Configuration Manager через Intune на портале Azure. | [![Эскиз видео о работоспособности клиента](media/thumbnail-client-health.png)](quickstart-client-health.md) |
| <a name="bkmk_hybrid-aad"></a>**Azure Active Directory (Azure AD)** | Azure AD позволяет повысить продуктивность работы пользователей и безопасность ресурсов как в облачной, так и в локальной средах. | [![Эскиз видео о гибридном подключении к Azure AD](media/thumbnail-azure-ad.png)](quickstart-hybrid-aad.md) |
| <a name="bkmk_autopilot"></a>**Windows Autopilot** | Сократите затраты времени и ресурсов, а также упростите процессы развертывания, администрирования, снятия с учета и повторного использования устройств. Autopilot также повышает удобство работы для пользователей. | [![Эскиз видео о Windows Autopilot](media/thumbnail-autopilot.png)](quickstart-autopilot.md) |

## <a name="getting-started"></a>начало работы

Если вы хотите включить совместное управление, начните с этого документа с ответами на технические вопросы, которые могут вас беспокоить.

| | | |
|-|-|-|
| <a name="bkmk_paths"></a>**Пути для совместного управления** | Существует два основных способа для настройки совместного управления, и вам важно понимать предварительные требования для каждого из них.  Каждый из способов требует определенного сочетания функциональных возможностей Azure AD, Configuration Manager, Intune и клиента Windows. | [![Эскиз слайда о путях совместного управления](media/thumbnail-paths.png)](quickstart-paths.md) |
| <a name="bkmk_setup-hybrid-aad"></a>**Настройка гибридного экземпляра Azure AD** | Если в среде существуют присоединенные к домену устройства Windows 10, настройте гибридное присоединение к Azure AD перед включением совместного управления. | [![Эскиз видео о настройке гибридного присоединения к Azure AD](media/thumbnail-setup-azure-ad.png)](quickstart-setup-hybrid-aad.md) |
| <a name="bkmk_upgrade-win10"></a>**Обновление до Windows 10** | Для совместного управления требуется Windows 10 версии 1709 или более поздней. | [![Эскиз видео об обновлении до Windows 10](media/thumbnail-upgrade-win10.png)](quickstart-upgrade-win10.md) |
| <a name="bkmk_fasttrack"></a>**Получение справки FastTrack** | Организация FastTrack — это большая группа инженеров Майкрософт, которые специализируются на помощи организациям всех типов в развертывании приложений Microsoft 365, в том числе в настройке совместного управления. | [![Эскиз видео о FastTrack](media/thumbnail-fasttrack.png)](quickstart-fasttrack.md) |
