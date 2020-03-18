---
title: Назначение роли пользователю Intune
description: Узнайте, как назначить встроенную или пользовательскую роль пользователю в Microsoft Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/26/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: pjain
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: e4ea84b0b378030a02c73da20b4a59d0b65ca288
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/13/2020
ms.locfileid: "79363152"
---
# <a name="assign-a-role-to-an-intune-user"></a>Назначение роли пользователю Intune

Вы можете назначить [встроенную](role-based-access-control.md#built-in-roles) или [пользовательскую](create-custom-role.md) роль пользователю Intune.

Для создания, изменения и назначения ролей учетная запись должна иметь одно из следующих разрешений в Azure AD:
- **Глобальный администратор**
- **Администратор службы Intune**

1. В [Центре администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) выберите **Администрирование клиента** > **Роли** > **Все роли**.

2. В колонке **"Все роли" в разделе ролей Intune** выберите встроенную роль, которую требуется назначить, и щелкните **Назначения** > **Назначить**.

5. На панели **Базовые** введите **Имя назначения** и необязательное **Описание назначения**, а затем щелкните **Далее**.

6. На странице **Группы администраторов** выберите группу, содержащую пользователя, которому необходимо предоставить разрешения. Нажмите кнопку **Далее**.

7. На странице **Область (группы)** выберите группу, содержащую пользователей или устройства, которыми сможет управлять вышеуказанный участник. Нажмите кнопку **Далее**.

8. На странице **Область (теги)** выберите теги областей, в которых будет применяться это назначение роли. Нажмите кнопку **Далее**.

9. На странице **Проверка и создание** после завершения нажмите **Создать**. Новое назначение отобразится в списке назначений.

## <a name="next-steps"></a>Дальнейшие шаги
- [Дополнительные сведения об управлении доступом на основе ролей в Intune](role-based-access-control.md)
- [Создание пользовательской роли](create-custom-role.md)


