---
title: Переключение на рабочие нагрузки совместного управления
titleSuffix: Configuration Manager
description: Сведения о переключении рабочих нагрузок, управляемых Configuration Manager, в Microsoft Intune.
ms.prod: configuration-manager
ms.technology: configmgr-comanage
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 09/06/2019
ms.topic: conceptual
ms.assetid: 60e2022f-a4f9-40dd-af01-9ecb37b43878
ms.openlocfilehash: 4874d12149f213351740c9e5b300bf04fc536571
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81691062"
---
# <a name="how-to-switch-configuration-manager-workloads-to-intune"></a>Переключение рабочих нагрузок Configuration Manager на Intune

Одним из преимуществ совместного управления является возможность перенести рабочие нагрузки из Configuration Manager в Microsoft Intune. Если на устройстве Windows 10 установлен клиент Configuration Manager и оно зарегистрировано в Intune, вы можете использовать преимущества обеих служб. Вы можете сами выбрать, какие рабочие нагрузки следует переключить с Configuration Manager в Intune. Configuration Manager будет и далее управлять всеми остальными рабочими нагрузками, в том числе всеми не переключенными на Intune рабочими нагрузками и всеми функциями Configuration Manager, для которых не поддерживается совместное управление.

Если вы переключите рабочую нагрузку в Intune, но позднее измените свое решение, вы можете снова переключиться на Configuration Manager.

Дополнительные сведения о поддерживаемых рабочих нагрузках см. в разделе [Рабочие нагрузки](workloads.md).

## <a name="switch-workloads-starting-in-version-1906"></a>Переключение рабочих нагрузок, начиная с версии 1906
<!--3555750 FKA 1357954 -->
Начиная с версии 1906, можно настроить различные пилотные коллекции для каждой из рабочих нагрузок совместного управления. Возможность использовать различные пилотные коллекции позволяет реализовать более детальный подход при изменении рабочих нагрузок. Вы можете переключить рабочие нагрузки сразу при включении совместного управления или позднее, когда вы будете к этому готовы. Если вы еще не включили совместное управление, сделайте это в первую очередь. Дополнительные сведения о включении совместного управления см. в [этой статье](how-to-enable.md). Включив совместное управление, измените соответствующие параметры в свойствах совместного управления.

1. В консоли Configuration Manager перейдите в рабочую область **Администрирование**, разверните **Облачные службы** и выберите узел **Совместное управление**.  
2. Выберите объект для совместного управления и выберите на ленте элемент **Свойства**.  
3. Перейдите на вкладку **Рабочие нагрузки**. По умолчанию для всех рабочих нагрузок выбран вариант **Configuration Manager**. Чтобы переключить рабочую нагрузку, переместите ползунок для этой рабочей нагрузки в нужное положение.  

    ![Снимок экрана с вкладкой "Рабочие нагрузки" на странице свойств совместного управления](media/3555750-co-management-workloads-tab.png)

    - **Configuration Manager**: Управление рабочей нагрузкой по-прежнему осуществляется в Configuration Manager.  

    - **Пилотный проект Intune**. Рабочая нагрузка включается только для устройств в пилотной коллекции. Вы можете изменить состав **пилотной коллекции** на вкладке **промежуточного процесса** на странице свойств совместного управления.  

    - **Intune**. Рабочая нагрузка включается для всех устройств Windows 10, зарегистрированных для совместного управления.  

4. Перейдите на вкладку **промежуточного процесса** и измените **пилотную коллекцию** на любую рабочую нагрузку, если это необходимо.
  
   ![Снимок экрана с вкладкой "Рабочие нагрузки" на странице свойств совместного управления](media/3555750-co-management-staging-tab.png)

> [!Important]  
> - Перед переключением рабочих нагрузок убедитесь, что вы правильно настроили и развернули в Intune соответствующую рабочую нагрузку. Убедитесь, что рабочими нагрузками для ваших устройств всегда управляет одно из средств управления.
> - Начиная с версии Configuration Manager 1806, при переключении рабочей нагрузки совместного управления все совместно управляемые устройства автоматически синхронизируют политику MDM из Microsoft Intune. Синхронизация также происходит при запуске действия **Загрузить политику компьютеров** в клиентских уведомлениях в консоли Configuration Manager. Дополнительные сведения см. в разделе [Запуск получения клиентской политики с помощью уведомления клиента](../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval). <!--1357377-->

## <a name="switch-workloads-in-version-1902-and-earlier"></a>Переключение рабочих нагрузок в версии 1902 и более ранних

Вы можете переключить рабочие нагрузки сразу при включении совместного управления или позднее, когда вы будете к этому готовы. Если вы еще не включили совместное управление, сделайте это в первую очередь. Дополнительные сведения о включении совместного управления см. в [этой статье](how-to-enable.md). Включив совместное управление, измените соответствующие параметры в свойствах совместного управления.

1. В консоли Configuration Manager перейдите в рабочую область **Администрирование**, разверните **Облачные службы** и выберите узел **Совместное управление**.  

2. Выберите объект для совместного управления и выберите на ленте элемент **Свойства**.
   - Вам будет предложено войти в Azure AD. Запрос не блокирует обновление подключения. Тем не менее при каждом открытии страницы **Свойства** будет выдаваться запрос, пока вы не выполните вход.

3. Перейдите на вкладку **Рабочие нагрузки**. По умолчанию для всех рабочих нагрузок выбран вариант **Configuration Manager**. Чтобы переключить рабочую нагрузку, переместите ползунок для этой рабочей нагрузки в нужное положение.  

    ![Снимок экрана с вкладкой "Рабочие нагрузки" на странице свойств совместного управления](media/properties-workloads.png)

    - **Configuration Manager**: Управление рабочей нагрузкой по-прежнему осуществляется в Configuration Manager.  

    - **Пилотный проект Intune**. Рабочая нагрузка включается только для устройств в пилотной коллекции. Вы можете изменить состав **пилотной коллекции** на вкладке **Staging** (Промежуточный процесс) на странице свойств совместного управления.  

    - **Intune**. Рабочая нагрузка включается для всех устройств Windows 10, зарегистрированных для совместного управления.  

4. При необходимости вы можете изменить состав **пилотной коллекции** с учетом своих рабочих нагрузок на вкладке **промежуточного процесса** на странице свойств совместного управления.

5. Нажмите кнопку **ОК**, чтобы сохранить свойства совместного управления и выйти из этого раздела.

> [!Important]  
> - Перед переключением рабочих нагрузок убедитесь, что вы правильно настроили и развернули в Intune соответствующую рабочую нагрузку. Убедитесь, что рабочими нагрузками для ваших устройств всегда управляет одно из средств управления. 
> - Начиная с версии Configuration Manager 1806, при переключении рабочей нагрузки совместного управления все совместно управляемые устройства автоматически синхронизируют политику MDM из Microsoft Intune. Синхронизация также происходит при запуске действия **Загрузить политику компьютеров** в клиентских уведомлениях в консоли Configuration Manager. Дополнительные сведения см. в разделе [Запуск получения клиентской политики с помощью уведомления клиента](../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval). <!--1357377-->

## <a name="next-steps"></a>Дальнейшие шаги

[Мониторинг совместного управления](how-to-monitor.md)