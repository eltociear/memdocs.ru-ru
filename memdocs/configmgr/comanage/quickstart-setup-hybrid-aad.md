---
title: Настройка гибридного экземпляра Azure AD
titleSuffix: Configuration Manager
description: Если в среде существуют присоединенные к домену устройства Windows 10, настройте гибридное присоединение к Azure AD перед включением совместного управления.
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 27dd26d1-e99c-4431-b2f8-60406394b6db
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8e2f7bbb51c72fa3d0f2a36e8a5419552d468b4c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81691222"
---
# <a name="set-up-hybrid-azure-ad-for-co-management"></a>Настройка гибридного присоединения к Azure AD для совместного управления

Если у вас есть устройства Windows 10, присоединенные к локальной службе Active Directory, то перед включением совместного управления в Configuration Manager следует присоединить эти устройства к Azure Active Directory (Azure AD). Этот процесс называется гибридным присоединением к Azure AD. 

В следующем видео руководитель программы Сандип Део (Sandeep Deo) и менеджер по маркетингу продуктов Адам Харбор (Adam Harbour) обсуждают и демонстрируют настройку устройств в Azure AD:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Configuring-Devices-in-Azure-Active-Directory/player]

В процессе гибридного присоединения к Azure AD локальные устройства, присоединенные к домену, автоматически регистрируются в службе Azure AD. См. дополнительные сведения:
- [Общие сведения об управлении устройствами в Azure Active Directory](https://docs.microsoft.com/azure/active-directory/device-management-introduction). 
- [Планирование реализации гибридного присоединения к Azure Active Directory](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan).

Гибридное присоединение к Azure AD является одним из ключевых механизмов для совместного управления. Этот процесс может создавать затруднения для клиентов в некоторых случаях, например:
- если организация использует сторонние решения для управления удостоверениями; 
- если есть сложности с настройкой служб федерации Active Directory (ADFS).

Для решения этих проблем могут потребоваться советы и рекомендации. Эта статья поможет вам устранить все возможные препятствия.


## <a name="how-to-do-it"></a>Необходимые действия

Процесс создания удостоверений для защиты почти идентичен для пользователей и устройств. Чтобы гарантировать защиту удостоверения устройства в любое время и в любом месте, это удостоверение устройства необходимо передать в Azure AD.

Для этого есть два основных способа в зависимости от используемого типа домена. Настройте гибридное присоединение к Azure AD для одного из следующих типов домена:  
- [федеративные домены](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-federated-domains);  
- [управляемые домены](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-managed-domains).  

Два указанных выше способа дают наилучшие результаты. Дополнительные сведения, включая полный процесс для настройки вручную, приводятся в следующих статьях:
- [How To: Plan your hybrid Azure Active Directory join implementation](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) (Практическое руководство. Планирование реализации гибридного присоединения к Azure Active Directory).  
- [Сведения о сквозной проверке подлинности для гибридного развертывания Azure AD](https://docs.microsoft.com/windows-server/identity/ad-fs/ad-fs-overview), в том числе об обнаружении Azure AD.  

Также может оказаться полезным [руководство по устранению неполадок для Windows 10 при гибридном присоединении к Azure AD](https://docs.microsoft.com/azure/active-directory/devices/troubleshoot-hybrid-join-windows-current).



## <a name="case-study"></a>Пример

Крупный европейский производитель программного обеспечения, в сети которого работают более 100 000 пользователей, применил детализированный и поэтапный подход по реализации гибридного присоединения к Azure AD.

На этапе планирования администраторы Configuration Manager тесно сотрудничали с группой по управлению удостоверениями, так как гибридное присоединение к Azure AD является важным элементом совместного управления. Эта компания, разрабатывающая программное обеспечение, создала много правил ADFS, некоторые из которых достаточно сложные. Чтобы справиться с этими трудностями, специалисты по управлению удостоверениями изучили существующие правила ADSF перед реализацией гибридного присоединения к Azure AD. Также ИТ-специалисты решили обновить Azure AD Connect до последней версии. Теперь Azure AD Connect предоставляет автоматизированный поток процессов для гибридного присоединения к Azure AD.

После успешного развертывания и тестирования подготовительной среды клиент включил гибридное присоединение к Azure AD для всего рабочего пространства. Всего за неделю они распространили совместное управление на все устройства Windows 10.



## <a name="contact-fasttrack"></a>Обратитесь в службу FastTrack

Если вам нужна помощь на любом этапе процесса настройки Azure AD, перейдите на страницу [Microsoft FastTrack](https://Microsoft.com/FastTrack/), выполните вход и опишите вашу проблему. 

Дополнительные сведения см. в руководстве [по обращению в службу FastTrack](quickstart-fasttrack.md). 

