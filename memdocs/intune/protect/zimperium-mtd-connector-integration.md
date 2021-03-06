---
title: Интеграция Zimperium MTD с Microsoft Intune
titleSuffix: Microsoft Intune
description: Как настроить решение Zimperium Mobile Threat Defense (MTD) в Microsoft Intune для управления доступом к корпоративным ресурсам с мобильных устройств
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
ms.assetid: 363fd280-1865-4a61-855b-eb75c3c62753
ms.reviewer: davidra
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4666c8c765f15ddd103727ccf2a7d840cb69bd20
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989360"
---
# <a name="integrate-zimperium-with-intune"></a>Интеграция Zimperium с Intune

Чтобы интегрировать решение Mobile Threat Defense Zimperium с Intune, следуйте инструкциям ниже.

## <a name="before-you-begin"></a>Подготовка к работе

Следующие шаги необходимо выполнить в [консоли Zimperium MTD](https://www.zimperium.com/platform), чтобы установить соединение со службой Zimperium для зарегистрированных устройств Intune (с помощью политики соответствия устройств) и незарегистрированных устройств (с помощью политик защиты приложений).

Перед началом интеграции Zimperium с Intune убедитесь в наличии следующей подписки и учетных данных:

- Подписка Microsoft Intune

- Учетные данные глобального администратора Azure Active Directory для предоставления следующих разрешений:

  - Вход и чтение профилей пользователей

  - Доступ к каталогу от имени вошедшего в систему пользователя

  - Чтение данных каталога

  - Отправка сведений об устройстве в Intune

- Учетные данные администратора для доступа к консоли MTD Zimperium.

### <a name="zimperium-app-authorization"></a>Авторизация приложения Zimperium

Авторизация приложения Zimperium выполняется так:

- Вы предоставляете разрешение службе Zimperium на передачу в Intune сведений о состоянии работоспособности устройства. Для этого необходимо использовать учетные данные глобального администратора. Предоставление разрешений — это разовая операция. После предоставления разрешений учетные данные глобального администратора больше не понадобятся.

- Zimperium синхронизируется с членством в группе регистрации Azure Active Directory (AD) и заполняет базу данных устройства.

- Вы разрешаете консоли администрирования Zimperium использовать единый вход (SSO) Azure AD.

- Вы разрешаете приложению Zimperium выполнять вход в режиме единого входа Azure AD.

Дополнительные сведения о предоставлении согласия и приложениях Azure Active Directory см. в разделе [Запрос разрешений у администратора каталога](https://docs.microsoft.com/azure/active-directory/develop/v2-permissions-and-consent#request-the-permissions-from-a-directory-admin) в статье *Разрешения и предоставление согласия в конечной точке Azure Active Directory версии 2.0*.


## <a name="to-set-up-zimperium-integration"></a>Настройка интеграции Zimperium

1. Перейдите в [консоль MTD Zimperium](https://www.zimperium.com/platform) и выполните вход, используя свои учетные данные. Чтобы выполнить процесс настройки интеграции Zimperium, необходимо войти в систему с помощью учетных данных пользователя Azure Active Directory, имеющего роль глобального администратора. Эта одноразовая операция настройки использует права глобального администратора для предоставления разрешения в вашей организации на взаимодействие приложений Zimperium с Intune. 

2. Выберите в левом меню пункт **Управление**.

3. Перейдите на вкладку **Параметры MDM**.

4. Выберите **Добавить MDM,** а затем **Microsoft Intune** в списке **поставщиков MDM**.

5. Когда вы настроите Microsoft Intune как службу управления мобильными устройствами, откроется окно **Настройка Microsoft Intune**. Выберите вариант **Добавить Azure Active Directory** для каждого параметра: **Zimperium zConsole**, **Приложения iOS и Android zIPS**, чтобы разрешить Zimperium взаимодействовать с Intune и Azure AD в режиме единого входа Azure AD.

    > [!IMPORTANT]  
    > Чтобы завершить процесс интеграции с Intune, вам потребуется добавить приложения zConsole Zimperium, zIPS iOS и Android.

6. Нажмите кнопку **Принять**, чтобы разрешить приложению Zimperium взаимодействовать с Intune и Azure Active Directory.

7. После добавления приложений **Zimperium zConsole** и **zIPS iOS и Android** в Azure AD добавьте группы безопасности Azure AD. Это позволит Zimperium синхронизировать группу безопасности Azure AD со своей службой.

8. Нажмите кнопку **Готово**, чтобы сохранить конфигурацию и запустить первую синхронизацию групп безопасности Azure AD.

9. Выйдите из консоли Zimperium MTD.

## <a name="next-steps"></a>Дальнейшие действия

- [Настройка приложений Zimperium для зарегистрированных устройств](mtd-apps-ios-app-configuration-policy-add-assign.md)
- [Настройка приложений Zimperium для незарегистрированных устройств](mtd-add-apps-unenrolled-devices.md)
