---
title: Настройка интеграции решения Wandera для защиты мобильных приложений от угроз в Intune
titleSuffix: Intune on Azure
description: Как настроить решение Wandera для защиты мобильных приложений от угроз в Microsoft Intune для управления доступом к корпоративным ресурсам с мобильных устройств.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 12/18/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 02ee6eb85e5ce330233711fe276a585eb80553cc
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990978"
---
# <a name="integrate-wandera-mobile-threat-protection-with-intune"></a>Интеграция решения Wandera для защиты мобильных приложений от угроз с Intune  

Чтобы интегрировать решение Wandera Mobile Threat Defense с Intune, выполните описанные ниже действия.  

> [!NOTE]
> Этот поставщик защиты от мобильных угроз не поддерживается для незарегистрированных устройств.

## <a name="before-you-begin"></a>Подготовка к работе  

Прежде чем начать интеграцию Wandera с Intune, убедитесь в наличии следующего:
- Подписка на Microsoft Intune  
- Учетные данные администратора Azure Active Directory для предоставления следующих разрешений:  
  - Вход и чтение профилей пользователей  
  - Доступ к каталогу от имени вошедшего в систему пользователя  
  - Чтение данных каталога  
  - Отправка сведений об устройстве в Intune  

- Подписка Wandera:
  - одна или несколько учетных записей Wandera, лицензированные для подключения EMM;  
  - учетная запись с привилегиями суперадминистратора в Wandera.  
 
### <a name="wandera-mobile-threat-defense-app-authorization"></a>Авторизация приложения Wandera Mobile Threat Defense  

Процесс авторизации приложения Wandera Mobile Threat Defense:  
- Вы разрешаете службе Wandera Mobile Threat Defense передавать в Intune сведения о состоянии работоспособности устройства.  
- Wandera синхронизируется с членством в группе регистрации Azure AD и заполняет базу данных устройства.  
- Вы разрешаете единый вход Azure AD для портала администрирования Wandera RADAR.  
- Вы разрешаете единый вход Azure AD для приложения Wandera Mobile Threat Defense.  


## <a name="set-up-wandera-mobile-threat-defense-integration"></a>Настройка интеграции Wandera Mobile Threat Defense  
*EMM Connect* для Wandera однократно настраивается в консолях Intune и Wandera. Настройка занимает около 15 минут. Можно выполнить настройку без согласования с представителем службы технической поддержки или управления учетными записями Wandera.  

### <a name="enable-support-for-wandera-in-intune"></a>Включение поддержки Wandera в Intune

1. Войдите в [Центр администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Выберите **Администрирование клиента** > **Соединители и токены** > **Mobile Threat Defense** > **Добавить**.
3. На странице **Добавление соединителя** используйте раскрывающийся список и выберите **Wandera**. Затем нажмите **Создать**.  
4. На панели Mobile Threat Defense выберите соединитель **Wandera** MTD в списке соединителей, чтобы открыть область *Изменить соединитель*. Выберите **Open the Wandera admin console** (Открыть консоль администрирования Wandera), чтобы открыть консоль администрирования Wandera [RADAR](https://radar.wandera.com/login), и войдите в систему. 
5. В консоли Wandera последовательно выберите **Settings** (Параметры) > **EMM Integration** (Интеграция EMM) и откройте вкладку **EMM Connect**. В раскрывающемся списке *поставщиков EMM* выберите *Microsoft Intune*.

   ![Выбор Intune](./media/wandera-mtd-connector-integration/set-up-intune-in-radar.png)

6. Выберите **Grant permissions** (Предоставить разрешения), чтобы установить подключение к порталу Intune. Зарегистрируйтесь, используя свои учетные данные администратора Intune, установите флажок, а затем **примите** запрос на разрешения.  

   ![Принятие запроса на разрешения](./media/wandera-mtd-connector-integration/permissions.png) 

7. Wandera завершит соединение, и вы вернетесь к консоли администрирования RADAR. Повторите процедуру, чтобы при необходимости **предоставить** доступ для дополнительных конфигураций.  

   ![Интеграция и разрешения](./media/wandera-mtd-connector-integration/integrations-and-permissions.png) 

8. В консоли RADAR скопируйте имя группы **SyncOnly**, которое отображается в столбце **EMM Label** (Метка EMM). Это имя вы будете использовать при настройки группы в Intune для синхронизации с Wandera.

   ![Синхронизация группы](./media/wandera-mtd-connector-integration/sync-group-name.png) 

9. Вернитесь к консоли [Intune](https://go.microsoft.com/fwlink/?linkid=2090973) и измените соединитель Wandera MTD. Установите доступные переключатели в состояние **Вкл.** и **сохраните** конфигурацию.  

   ![Включение Wandera](./media/wandera-mtd-connector-integration/enable-wandera.png) 

Подключение между Intune и Wandera установлено.  

## <a name="configure-the-wandera-applications-and-synchronization-group"></a>Настройка приложений и группы синхронизации Wandera  
Чтобы развернуть Wandera, вы добавите мобильные приложения Wandera для используемых платформ (iOS и Android) в Intune и назначите их определенной группе синхронизации — группе *SyncOnly*. 

Этот процесс описан в следующих разделах.

Дополнительные сведения об этом процессе, предоставленные Wandera, можно найти в консоли Wandera [RADAR](https://radar.wandera.com/login). Перейдите к разделу **Settings** (Параметры) > **EMM Integration** (Интеграция EMM), выберите **App Push** (Принудительная отправка приложений), а затем выберите **Microsoft Intune**. На вкладке App Push (Принудительная отправка приложений) отобразятся инструкции, которые относятся к Intune.  

### <a name="add-the-wandera-apps"></a>Добавление приложений Wandera  
Создайте клиентские приложения в Intune, чтобы развернуть приложение Wandera на устройствах Android и iOS/iPadOS. Инструкции и специальные сведения, касающиеся приложений Wandera, см. в статье о [добавлении приложений MTD](mtd-apps-ios-app-configuration-policy-add-assign.md).  

Когда вы создадите приложения, вернитесь к этому руководству, чтобы создать группу синхронизации и назначить приложения.

### <a name="create-the-synchronization-group-and-assign-the-apps"></a>Создание группы синхронизации и назначение приложений

1. Вам понадобится имя группы **SyncOnly**, которое отображается в столбце **EMM Label** (метка EMM) в консоли Wandera RADAR. Вы скопировали это имя на шаге 7 при [включении поддержки для Wandera в Intune](#enable-support-for-wandera-in-intune). Используйте это имя как имя группы в Intune для синхронизации с Wandera.  

2. В центре администрирования диспетчера конечных точек перейдите к разделу **Группы** и выберите **Новая группа**. Чтобы настроить группу синхронизации для использования с Wandera, укажите следующие сведения:
   - **Тип группы**: **Security**
   - **Имя группы**: укажите имя **SyncOnly**, скопированное в консоли администрирования Wandera RADAR.

   ![Настройка группы синхронизации](./media/wandera-mtd-connector-integration/configure-sync-group.png)

3. Выберите **Участники** и назначьте группы с устройствами Android и iOS/iPadOS, которые нужно использовать с Wandera.

4. Выберите **Создать**, чтобы сохранить группу.

Дополнительные сведения см. в статье о [развертывании приложений](../apps/apps-deploy.md).

### <a name="assign-the-wandera-apps-to-the-synchronization-group"></a>Назначение приложений Wandera группе синхронизации  
Выполните приведенные ниже инструкции для каждого приложения Wandera, созданного для iOS/iPadOS и Android.

1. Войдите в [Центр администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Щелкните **Приложения** > **Все приложения** и выберите приложение Wandera.
3. Последовательно выберите **Назначения** и **Добавить группу**.  
4. В области **Добавление группы** для параметра *Тип назначения* выберите *Обязательное*.
5. Последовательно выберите **Включенные группы** и **Выберите группы для включения**. Укажите группу, созданную для синхронизации с Wandera и щелкните **Выбрать** > **ОК** > **ОК**. Чтобы завершить назначение группы, нажмите кнопку **Сохранить**. 

## <a name="next-steps"></a>Дальнейшие шаги  
Теперь интеграция настроена и можно приступать к настройке политик и расширенного условного доступа, а также просмотру отчетов в консоли администрирования Wandera. Дополнительные сведения об управлении и настройке Wandera см. в [руководстве по началу работы с центром поддержки](https://radar.wandera.com/?return_to=https://wandera.force.com/Customer/s/getting-started) в документации по Wandera. 
