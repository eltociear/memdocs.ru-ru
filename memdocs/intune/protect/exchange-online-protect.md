---
title: Exchange без управления устройствами
titleSuffix: Microsoft Intune
description: Используйте Microsoft Intune для предоставления сотрудникам доступа к электронной почте Office 365 Exchange Online без настройки системы управления устройствами.
keywords: Доступ к электронной почте Office 365 Exchange
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/31/2017
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.topic: archived
ms.technology: ''
ms.assetid: 88a0d3b9-2622-403b-8374-1396afd8066e
ms.reviewer: pchacon
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8746a6dee0b35dec7886a596d0448874dfb04f16
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "79352024"
---
# <a name="protect-office-365-exchange-online-without-requiring-device-management"></a>Защита Office 365 Exchange Online без необходимости управления устройствами

Если вы хотите предоставить сотрудникам доступ к рабочей электронной почте без издержек по настройке системы управления устройствами, это возможно. Доступ к Office 365 Exchange Online можно предоставить через Intune. Чтобы выполнить необходимые действия, убедитесь в наличии лицензий для Microsoft 365 или Azure Active Directory (Premium) и Intune. Сотрудники должны иметь [поддерживаемые устройства iOS, iPadOS или Android](../fundamentals/supported-devices-browsers.md). 

При желании вы также можете настроить систему управления устройствами. Эта функция защиты приложений работает независимо от системы управления устройствами. 

## <a name="action-plan"></a>План действий

1. [См. подробнее об условном доступе](conditional-access.md). 
2. [См. подробнее об условном доступе на основе приложений](app-based-conditional-access-intune.md).
3. [Настройте политики условного доступа на основе приложений для Exchange Online](app-based-conditional-access-intune-create.md).
4. [Заблокируйте приложения, которые не поддерживают управление](app-modern-authentication-block.md), в частности, приложения, не использующие библиотеку Azure Active Directory Authentication Library (ADAL).
5. (Дополнительно.) [Настройте политики условного доступа на основе приложений для SharePoint Online](app-based-conditional-access-intune-create.md). Эти политики блокируют доступ к данным компании из приложений, для которых недоступно управление и защита. Политики также ограничивают доступ с помощью SharePoint для мобильных устройств. 

## <a name="what-to-tell-employees-and-students"></a>Что следует рассказать сотрудникам и учащимся

* Попросите сотрудников и учащихся скачать и установить приложение Microsoft Outlook или Microsoft SharePoint для iOS, iPadOS (в Apple App Store) или Android (в Google Play Маркет). 
* Если предполагается блокировать доступ к приложениям, которые не используют современную проверку подлинности, расскажите сотрудникам и учащимся об этом ограничении. 

## <a name="next-steps"></a>Дальнейшие действия

Вы использовали условный доступ на основе приложений для повышения безопасности корпоративных данных. В рамках следующей процедуры вы узнаете о других способах повышения безопасности данных компании, включая: 

* настройку [условного доступа на основе соответствия устройств, риска для устройств, расположения и атрибутов пользователей в Active Directory и Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal);  
* настройку политик защиты приложений, помогающих защитить данные компании от намеренной или случайной утечки данных; 
* использование Azure Information Protection для защиты данных компании за пределами вашей сети. 

Требуется помощь по реализации этого сценария EMS или Office 365 или других? При наличии хотя бы 150 лицензий для Microsoft 365, Microsoft Enterprise Mobility + Security или Azure Active Directory Premium воспользуйтесь [преимуществами FastTrack](https://docs.microsoft.com/enterprise-mobility-security/solutions/enterprise-mobility-fasttrack-program). 
