---
title: Настройка политики условного доступа на основе приложений в Intune
titleSuffix: Microsoft Intune
description: Узнайте, как настроить политику условного доступа на основе приложений в Intune.
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
ms.assetid: d1693515-de18-4553-91ef-801976cd3ec7
ms.reviewer: elocholi
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 73b471d7eefa8e696b17a949756ce1395530c5f7
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/27/2020
ms.locfileid: "80323197"
---
# <a name="set-up-app-based-conditional-access-policies-with-intune"></a>Настройка политик условного доступа на основе приложений в Intune

Настройте политики условного доступа на основе приложений для приложений, входящих в список утвержденных. В список утвержденных входят приложения, протестированные корпорацией Майкрософт.

Перед использованием политик условного доступа на основе приложений к приложениям должны быть применены [политики защиты приложений Intune](../apps/app-protection-policies.md).

> [!IMPORTANT]
> Эта статья описывает, как добавить политику условного доступа на основе приложения. Можно использовать одни и те же действия при добавлении таких приложений, как SharePoint Online, Microsoft Teams и Microsoft Exchange Online, из списка утвержденных приложений.

## <a name="create-app-based-conditional-access-policies"></a>Создание политик условного доступа на основе приложений

Условный доступ — это технология Azure Active Directory (Azure AD). Узел условного доступа, доступ к которому осуществляется из *Intune*, является тем же узлом, доступ к которому осуществляется из *Azure AD*. Это означает, что для настройки политик нет необходимости переключаться между Intune и Azure AD.

Прежде чем создавать политики условного доступа из центра администрирования Microsoft Endpoint Manager, необходимо получить лицензию на Azure AD Premium.

### <a name="to-create-an-app-based-conditional-access-policy"></a>Создание политики условного доступа на базе приложений

1. Войдите в [Центр администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431)

2. Выберите **Endpoint security** (Защита конечной точки) > **Условный доступ**  > **Новая политика**.

3. Введите **имя** политики, а затем в разделе *Назначения* выберите **Пользователи и группы**. Используйте варианты включения или исключения, чтобы добавить группы для политики, и нажмите кнопку **Готово**.

4. Выберите **Облачные приложения или действия**, а затем — приложения, которые следует защищать. Например, выберите **Выбрать приложения**, а затем — **Office 365 SharePoint Online** или **Office 365 Exchange Online**.

   Нажмите кнопку **Готово**, чтобы сохранить изменения.

5. Выберите **Условия** > **Клиентские приложения**, чтобы применить политику к приложениям и браузерам. Например, выберите **Да**, а затем включите **Браузер** и **Mobile apps and desktop clients** (Мобильные приложения и настольные клиенты).

   Нажмите кнопку **Готово**, чтобы сохранить изменения.

6. В разделе *Элементы управления доступом* выберите **Предоставить**, чтобы применить условный доступ на основе соответствия устройств. Например, выберите **Предоставить доступ** > **Require device to be marked as compliant** (Требовать, чтобы устройство было отмечено как соответствующее).

   Нажмите кнопку **ОК**, чтобы сохранить изменения.

7. Для параметра **Включить политику** установите значение **Вкл.** , а затем выберите **Создать**, чтобы сохранить изменения.





## <a name="next-steps"></a>Дальнейшие шаги
[Блокировка приложений, не поддерживающих современные средства проверки подлинности](app-modern-authentication-block.md)

## <a name="see-also"></a>См. также

[Защита данных приложения с помощью политик защиты приложений](../apps/app-protection-policies.md)
[Условный доступ в Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access)
