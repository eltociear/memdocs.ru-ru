---
title: Настройка интеграции Pradeo с Intune
titleSuffix: Intune on Azure
description: Интеграция соединителя Pradeo с Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/21/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 82872ba6-80f8-4cc9-adf4-0ccd8ff26dd2
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2fb2317474b49dcb4bb39a0590c8ad7fa4ac8aa4
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/27/2020
ms.locfileid: "83984874"
---
# <a name="integrate-pradeo-mobile-threat-defense-with-intune"></a>Интеграция Pradeo Mobile Threat Defense с Intune

Чтобы интегрировать решение Pradeo Mobile Threat Defense с Intune, следуйте инструкциям ниже.

> [!NOTE]  
> Этот поставщик защиты от мобильных угроз не поддерживается для незарегистрированных устройств.

## <a name="before-you-begin"></a>Подготовка к работе

> [!NOTE]
> Следующие шаги выполняются в [консоли Pradeo Security](https://pradeo-security.com/).

Перед началом интеграции Pradeo с Intune убедитесь в наличии следующего:

- Подписка на Microsoft Intune

- Учетные данные администратора Azure Active Directory для предоставления следующих разрешений:

  - Вход и чтение профилей пользователей

  - Доступ к каталогу от имени вошедшего в систему пользователя

  - Чтение данных каталога

  - Отправка сведений об устройстве в Intune

- Учетные данные администратора для доступа к консоли Pradeo Security.

### <a name="pradeo-app-authorization"></a>Авторизация приложения Pradeo

Авторизация приложения Pradeo выполняется так:

- Вы разрешаете службе Pradeo передавать в Intune сведения о состоянии работоспособности устройства.

- Pradeo синхронизирует данные о членстве в группе регистрации Azure AD для заполнения базы данных устройства.

- Вы разрешаете консоли администрирования Pradeo использовать единый вход (SSO) Azure AD.

- Вы разрешаете приложению Pradeo выполнять вход в режиме единого входа Azure AD.

## <a name="to-set-up-pradeo-integration"></a>Настройка интеграции Pradeo

1. Перейдите в [консоль Pradeo Security](https://www.pradeo-security.com) и выполните вход, используя свои учетные данные.

2. В меню выберите **Администрирование — Enterprise Mobility Management** (Управление Enterprise Mobility).

3. Выберите **логотип Intune**.

4. В разделе **Шаг 1** окна **EMM (Enterprise mobility management) - Intune** (EMM (управление Enterprise Mobility) — Intune) нажмите кнопку **Pradeo Connector** (Соединитель Pradeo). 

    ![Снимок экрана: окно Pradeo EMM в Intune](./media/pradeo-mtd-connector-integration/pradeo_setup.png)

5. В окне подключения Microsoft Intune введите свои учетные данные Intune.

5. Снова открывается веб-страница Pradeo. В разделе **Шаг 2** нажмите кнопку **Pradeo Device Health** (Работоспособность устройства Pradeo).

7. В окне соединителя Intune с Pradeo выберите **Принять**. 

8. В окне соединителя API устройства Pradeo выберите **Принять**.

9. Снова открывается веб-страница Pradeo. В разделе **Шаг 3** нажмите кнопку **Connect to Microsoft** (Подключение к Майкрософт). 

10. В окне проверки подлинности Microsoft Intune введите свои учетные данные Intune.

11. При отображении сообщения **Successful Integration** (Интеграция выполнена) интеграция завершена.

## <a name="next-steps"></a>Дальнейшие шаги

- [Настройка приложений Pradeo для зарегистрированных устройств](mtd-apps-ios-app-configuration-policy-add-assign.md)
