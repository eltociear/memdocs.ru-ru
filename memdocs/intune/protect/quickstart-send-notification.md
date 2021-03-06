---
title: Краткое руководство. Отправка уведомлений на несоответствующие устройства
titleSuffix: Microsoft Intune
description: В этом кратком руководстве вы используете Microsoft Intune для отправки уведомлений по электронной почте на несоответствующие устройства.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 11/21/2019
ms.topic: quickstart
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: a1b89f2d-7937-46bb-926b-b05f6fa9c749
ms.reviewer: jinyoon
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d02329f65d7b7ecec1dbfeaf84ecbe5c8fb53013
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2020
ms.locfileid: "82079490"
---
# <a name="quickstart-send-notifications-to-noncompliant-devices"></a>Краткое руководство. Отправка уведомлений на несоответствующие устройства

В этом кратком руководстве вы будете использовать Microsoft Intune для отправки уведомлений по электронной почте сотрудникам компании, которые имеют несоответствующие устройства.

Когда Intune обнаруживает устройство, не соответствующе требованиям, по умолчанию оно сразу же помечается как несоответствующее. Затем [условный доступ](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal) Azure Active Directory (Azure AD) блокирует устройство. Если устройство не соответствует требованиям, Intune позволяет добавить различные действия при несоответствии. Например, можно предоставить пользователям льготный период для выполнения требований, прежде чем несоответствующие устройства будут заблокированы.

Одно из действий, которое можно предпринять, если устройство не соответствует требованиям, — отправить сообщение электронной почты пользователю устройства. Вы также можете настроить уведомление по электронной почте перед отправкой. В частности, можно настроить получателей, тему, текст сообщения, включая логотип организации, и контактную информацию. Кроме того, Intune включает в уведомление дополнительные сведения об устройстве, которое не соответствует требованиям.

Если у вас нет подписки Intune, [зарегистрируйтесь для получения бесплатной пробной учетной записи](../fundamentals/free-trial-sign-up.md).

## <a name="prerequisites"></a>Предварительные условия

При использовании политик соответствия устройств для блокировки доступа к корпоративным ресурсам необходимо настроить условный доступ Azure AD. Если вы выполнили краткое руководство по [созданию политики соответствия устройств](quickstart-set-password-length-android.md), вы используете Azure Active Directory. Дополнительные сведения об Azure AD см. в статье [Что собой представляет условный доступ](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal) или [Каковы стандартные способы использования условного доступа с помощью Intune?](../protect/conditional-access-intune-common-ways-use.md).

## <a name="sign-in-to-intune"></a>Вход в Intune

Войдите в [Центр администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) в качестве [глобального администратора](../fundamentals/users-add.md#types-of-administrators) или [администратора службы Intune](../fundamentals/users-add.md#types-of-administrators). Если вы создали подписку на пробную версию Intune, учетная запись, с помощью которой вы создали подписку, является глобальным администратором.

## <a name="create-a-notification-message-template"></a>Создание шаблона уведомлений

Создайте шаблон сообщения уведомления для отправки электронных сообщений пользователям. Если устройство не соответствует требованиям, сведения, введенные в шаблоне, отображаются в сообщении электронной почты, отправляемом пользователем.

1. В Intune выберите **Устройства** > **Политики соответствия** > **Уведомления** > **Создать уведомление**.
2. Введите следующие сведения.

   - **Имя** — *Администратор Contoso*
   - **Тема**. *Соответствие устройства*
   - **Сообщение**: *Ваше устройство не соответствует требованиям нашей организации.*
   - **Заголовок электронного письма — включить логотип компании**: Установите значение **Включено**, чтобы отобразить логотип вашей организации.
   - **Нижний колонтитул электронного письма — включить имя компании**: Установите значение **Включено**, чтобы отобразить название вашей организации.
   - **Нижний колонтитул электронного письма — включить контактные данные**: Установите значение **Включено**, чтобы отобразить контактные сведения вашей организации.

   ![Пример уведомления о соответствии требованиям в Intune](./media/quickstart-send-notification/quickstart-send-notification-01.png)

3. Нажмите кнопку **Далее** и просмотрите уведомление. Нажмите кнопку **Создать**. После этого шаблон уведомляющих сообщений будет доступен для использования.

   > [!NOTE]
   > Можно также изменить ранее созданный шаблон уведомления.

Дополнительные сведения о настройке имени компании, ее контактной информации и логотипа см. в следующих разделах:

- [Данные организации и заявление о конфиденциальности](../apps/company-portal-app.md#configuration)
- [Сведения о поддержке](../apps/company-portal-app.md#support-information)
- [Настройка пользовательского интерфейса](../apps/company-portal-app.md#customizing-the-user-experience)

## <a name="add-a-noncompliance-policy"></a>Добавление политики несоответствия

Когда вы создаете политику соответствия устройств, Intune автоматически создает действие при несоответствии. Если устройства не соответствуют политике соответствия требованиям, Intune помечает устройства как несоответствующие требованиям. Вы можете настроить, как долго устройство будет иметь эту метку. Можно также добавить другое действие при создании политики соответствия требованиям или изменении существующей политики.

Ниже приведена процедура создания политики соответствия для устройств Windows 10.

1. В Intune выберите **Устройства** > **Политики соответствия** > **Создать политику**.

2. Введите следующие сведения.

   - **Имя** — *Соответствие Windows 10*
   - **Описание**. *Политика соответствия Windows 10*
   - **Платформа**. Windows 10 и более поздней версии

3. Выберите **Параметры** > **Безопасность системы**, чтобы отобразить параметры безопасности устройств.

4. Настройте следующие параметры.

   - Для параметра **Требовать пароль для разблокировки мобильных устройств** задайте **Требовать**. Этот параметр указывает, потребуется ли пользователю вводить пароль, прежде чем он сможет получить доступ к данным на своем мобильном устройстве.

   - Для параметра **Минимальная длина пароля** задайте значение **6**. Этот параметр задает минимальное число цифр или символов в пароле.

   ![Параметры безопасности системы для новой политики соответствия](./media/quickstart-send-notification/system-security-settings-01.png)

5. Выберите **ОК** > **ОК** > **Создать**, чтобы создать политику соответствия требованиям.

6. Выберите **Свойства** > **Действие при несоответствии** > **Добавить**.

7. Убедитесь, что в раскрывающемся списке **Действие** выбран вариант **Отправить сообщение электронной почты пользователю**.

8. Выберите **Шаблон сообщения**, шаблон, который вы создали ранее в этой статье, а затем нажмите кнопку **Выбрать**,чтобы выбрать шаблон сообщения.

9. Выберите **Добавить** > **ОК** > **Сохранить** для сохранения изменений.

## <a name="assign-the-policy"></a>Назначение политики

Политику соответствия можно назначить определенной группе пользователей или всем пользователям. Если Intune определит устройство как несоответствующее, пользователь получит уведомление о необходимости обновить устройство в соответствии с политикой соответствия. Чтобы назначить политику, сделайте следующее:

1. В Intune перейдите в раздел **Устройства** > **Политики соответствия** и выберите созданную ранее политику **соответствия требованиям для Windows 10**.

2. Выберите **Назначения**.

3. В раскрывающемся списке **Кому назначить** выберите **Все пользователи**. При этом будут выбраны все пользователи. Все пользователи, имеющие устройства **Windows 10 и более поздней версии**, которые не соответствуют этой политике, получат уведомления.

    > [!NOTE]
    > При назначении политик соответствия можно включать и исключать группы пользователей.

4. Нажмите кнопку **Сохранить**.

Созданная и сохраненная политика появится в списке **Compliance policies — Policies** (Политики соответствия — политики). Обратите внимание, что в списке для параметра **Назначено** задано значение **Да**.

## <a name="next-steps"></a>Дальнейшие шаги

В этом кратком руководстве описано, как с помощью Intune создать и назначить политику соответствия требованиям для устройств Windows 10 сотрудников, в соответствии с которой пароль должен иметь длину не менее шести символов. Дополнительные сведения о создании политик соответствия требованиям для устройств Windows см. в разделе [Добавление политики соответствия требованиям для устройств Windows в Intune](compliance-policy-create-windows.md).

Чтобы выполнить эту серию кратких руководств по Intune, переходите к следующему руководству.

> [!div class="nextstepaction"]
> [Краткое руководство. Добавление и назначение клиентского приложения](../apps/quickstart-add-assign-app.md)
