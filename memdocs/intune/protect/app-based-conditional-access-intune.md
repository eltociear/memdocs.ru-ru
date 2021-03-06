---
title: Условный доступ на основе приложений с помощью Intune
titleSuffix: Microsoft Intune
description: Узнайте, как работает условный доступ на основе приложений с помощью Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/06/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: b399fba0-5dd4-4777-bc9b-856af038ec41
ms.reviewer: elocholi
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 27033c2452224bc93e335f3517c9548ad65666c4
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2020
ms.locfileid: "82080153"
---
# <a name="app-based-conditional-access-with-intune"></a>Условный доступ на основе приложений с помощью Intune

[Политики защиты приложений Intune](../apps/app-protection-policy.md) помогают защитить данные компании на устройствах, зарегистрированных в Intune. Политики защиты приложений также можно использовать на устройствах, принадлежащих сотрудникам, которые не зарегистрированы для управления в Intune. В этом случае, даже если контроля над устройством нет, все равно необходимо обеспечить защиту данных и ресурсов компании.

Функции условного доступа на основе приложений и управления клиентскими приложениями позволяют реализовать дополнительный уровень безопасности, предоставляя доступ к Exchange Online и другим службам Office 365 только клиентским приложениям, поддерживающим политики защиты приложений Intune.

> [!NOTE]
> Под управляемым понимается приложение, к которому применены политики защиты приложений и которое может управляться в Intune.

Вы можете заблокировать встроенные приложения электронной почты iOS/iPadOS и Android и разрешить доступ к Exchange Online только для приложения Microsoft Outlook. Кроме того, вы можете заблокировать доступ к SharePoint Online для приложений, к которым не применяются политики защиты приложений Intune.

## <a name="prerequisites"></a>Предварительные условия

Требования для создания политики условного доступа на основе приложений:

- **Enterprise Mobility + Security (EMS)** или **Azure Active Directory (AD) Premium**.
- Пользователи должны иметь лицензию на EMS или Azure AD.

Дополнительные сведения см. в статье [Цены Enterprise Mobility + Security](https://www.microsoft.com/cloud-platform/enterprise-mobility-pricing) или [Цены на Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/).

## <a name="supported-apps"></a>Поддерживаемые приложения

Список приложений, которые поддерживают условный доступ на основе приложений, см. в [технической документации по условному доступу Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-technical-reference).

Модель условного доступа на основе приложений [также поддерживает бизнес-приложения](app-modern-authentication-block.md), однако такие приложения должны использовать [современные средства проверки подлинности Office 365](https://support.office.com/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a). 

## <a name="how-app-based-conditional-access-works"></a>Принципы реализации условного доступа на основе приложений

В этом примере администратор применил к приложению Outlook политики защиты приложений, а также правило условного доступа, по которому приложение Outlook добавляется в список утвержденных приложений, которые можно использовать для доступа к корпоративной электронной почте.

> [!NOTE]
> Для других управляемых приложений можно использовать приведенную ниже блок-схему.

![Процесс условного доступа на основе приложений проиллюстрирован на схеме](./media/app-based-conditional-access-intune/ca-intune-common-ways-3.png)

1. Пользователь пытается пройти проверку подлинности в Azure AD из приложения Outlook.

2. При первичной проверке подлинности пользователь перенаправляется в магазин приложений, чтобы установить приложение посредника. В качестве приложения посредника могут выступать решения Microsoft Authenticator для iOS или корпоративный портал Майкрософт для устройств Android.

   При попытке использовать нативное приложение электронной почты пользователь будет перенаправляться в магазин приложений для последующей установки приложения Outlook.

3. Приложение посредника устанавливается на устройстве.

4. Приложение посредника запускает процесс регистрации Azure AD, в ходе которого в Azure AD создается запись устройства. Этот процесс отличается от процесса регистрации для функции управления мобильными устройствами (MDM), однако такая запись необходима для применения политик условного доступа к устройству.

5. Приложение посредника проверяет подлинность приложения. Благодаря наличию уровня безопасности приложение брокера может проверить, разрешено ли использование приложения пользователем.

6. Приложение брокера передает идентификатор клиента приложения в Azure AD в рамках процесса проверки подлинности пользователя для сопоставления со списком утвержденных политик.

7. Azure AD разрешает пользователю пройти проверку подлинности и использовать приложение на основе списка утвержденных политик. Если приложение отсутствует в списке, Azure AD запрещает доступ к нему.

8. Приложение Outlook обменивается данными с облачной службой Outlook, инициируя взаимодействие с Exchange Online.

9. Облачная служба Outlook связывается с Azure AD и получает токен доступа к службе Exchange Online для пользователя.

10. Приложение Outlook обменивается данными с Exchange Online для получения корпоративного адреса электронной почты пользователя.

11. Корпоративный адрес отправляется в почтовый ящик пользователя.

## <a name="next-steps"></a>Дальнейшие шаги
[Set up app-based Conditional Access policies with Intune](app-based-conditional-access-intune-create.md) (Настройка политик условного доступа на основе приложений с помощью Intune)

[Блокировка приложений, не поддерживающих современные средства проверки подлинности](app-modern-authentication-block.md)
