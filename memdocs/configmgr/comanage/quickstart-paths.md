---
title: Пути для совместного управления
titleSuffix: Configuration Manager
description: Сведения о предварительных требованиях для двух основных путей настройки совместного управления.
ms.date: 06/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 5beb5564-2fdf-4f0a-8801-d0cec8214c43
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 27994107c32fac87a465240f07b68d57fddfc140
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/27/2020
ms.locfileid: "83983827"
---
# <a name="paths-to-co-management"></a>Пути для совместного управления

Существует два основных пути настройки совместного управления. Важно понимать все предварительные требования для каждого из этих путей. Оба они требуют определенного сочетания функциональных возможностей Azure Active Directory (AAD), Configuration Manager, Microsoft Intune и Windows 10. 

1. [Автоматическая регистрация существующих устройств, управляемых Configuration Manager, в Intune](#bkmk_path1)  
2. [Начальная загрузка клиента Configuration Manager с помощью современных средств подготовки](#bkmk_path2)  

![Схема путей совместного управления](media/co-management-paths.png)



## <a name="path-1-auto-enroll-existing-clients"></a><a name="bkmk_path1"></a> Путь 1. Автоматическая регистрация существующих клиентов

Этот путь позволяет быстро зарегистрировать в Intune существующие устройства, управляемые Configuration Manager. Управление такими устройствами через Configuration Manager никак не изменится по сравнению с ситуацией до включения совместного управления. Но теперь вы получите все преимущества облачных технологий. Этот путь полностью незаметен для всех пользователей.

Для его настройки вам потребуется следующее:
- Гибридный экземпляр Azure AD
    - Один из следующих [вариантов гибридного идентификатора Azure AD](https://docs.microsoft.com/azure/active-directory/hybrid/plan-connect-user-signin):  
       - [Синхронизация хэшированных паролей](https://docs.microsoft.com/azure/active-directory/hybrid/plan-connect-user-signin#password-hash-synchronization) с использованием [простого единого входа](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso).
       - [Сквозная аутентификация](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-pta) с использованием [простого единого входа](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso).
       - [Федеративный единый вход с использованием служб федерации Active Directory (AD FS)](https://docs.microsoft.com/azure/active-directory/hybrid/plan-connect-user-signin#federation-that-uses-a-new-or-existing-farm-with-ad-fs-in-windows-server-2012-r2).
    - Azure AD Connect.
    - Лицензия Azure Active Directory Premium.
    - Настройка гибридного присоединения к Azure AD (один из следующих вариантов):
        - для управляемых доменов;
        - для федеративных доменов.
- Параметры агента клиента для гибридного присоединения к Azure AD.
- Настройка автоматической регистрации устройств в Intune
- Включение совместного управления в Configuration Manager

Руководство по этому пути см. в статье [Руководство. Включение совместного управления для существующих клиентов Configuration Manager](tutorial-co-manage-clients.md).



## <a name="path-2-bootstrap-with-modern-provisioning"></a><a name="bkmk_path2"></a> Путь 2. Подготовка к работе с помощью современных средств

Для его настройки вам потребуется следующее:

1. [Улучшенный протокол HTTP](../core/plan-design/hierarchy/enhanced-http.md).  
2. [Создание облачных служб в Azure](../core/servers/deploy/configure/azure-services-wizard.md).  
3. [Настройка точки управления и клиентов для использования шлюза облачного управления](../core/clients/manage/cmg/setup-cloud-management-gateway.md).  
4. [Развертывание клиента Configuration Manager с помощью Intune](how-to-prepare-Win10.md).  

> [!Note]  
> Руководство по этому пути будет подготовлено в ближайшее время.

