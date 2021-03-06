---
title: Имитация развертываний приложений
titleSuffix: Configuration Manager
description: Оцените метод обнаружения, требования и зависимости для типа развертывания, не устанавливая приложение.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 28b240a4-d358-40ce-8006-c697b1622ece
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: bed491b4800dd6ae8b53a837618abf3d8a5a597d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689982"
---
# <a name="simulate-application-deployments-with-configuration-manager"></a>Имитация развертываний приложений в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Имитацию развертывания можно использовать для проверки развертывания приложения без его установки или удаления. Имитация развертывания позволяет оценить метод обнаружения, требования и зависимости для типа развертывания. Результаты приводятся в узле **Развертывания** в рабочей области **Наблюдение**. В этом разделе описывается процедура имитации развертывания приложения в Configuration Manager.  

> [!NOTE]  
> Нельзя имитировать развертывания в коллекциях мобильных устройств.  
>   
> Нельзя выполнить развертывание приложения, указав цель развертывания **Удалить** , если активна имитация развертывания этого же приложения.  

## <a name="configure-a-simulated-application-deployment"></a>Настройка имитации развертывания приложения

1.  В консоли Configuration Manager выберите один из следующих элементов:  
    -   Коллекция пользователей.  
    -   Коллекция устройств.  
    -   Приложение Configuration Manager.  

2.  На вкладке **Главная** в группе **Развертывание** нажмите кнопку **Имитировать развертывание**.  

3.  В мастере имитации развертывания приложения укажите приведенные ниже сведения.  

    -   **Приложение**. Нажмите кнопку **Обзор** и выберите приложение, для которого требуется имитировать развертывание.  

    -   **Коллекция**. Нажмите кнопку **Обзор** и выберите коллекцию, для которой требуется имитировать развертывание.  

    -   **Действие**. В раскрывающемся списке укажите, какое действие требуется имитировать — установку или удаление выбранного приложения.  

    -   **Развертывать автоматически независимо от того, находится ли пользователь в системе**. Если этот флажок установлен, клиенты оценивают имитацию развертывания вне зависимости от того, вошли ли они в систему.  

4.  Нажмите кнопку **Далее**, просмотрите сведения на странице **Сводка**, после чего завершите работу мастера, чтобы создать имитацию развертывания приложения.  

5.  Имитируемые приложения отображаются в узле **Развертывания** рабочей области **Наблюдение** с целью **Имитировать**. Дополнительные сведения о мониторинге развертывания приложений см. в разделе [Monitor applications from the Configuration Manager console](../../apps/deploy-use/monitor-applications-from-the-console.md) (Мониторинг приложений из консоли Configuration Manager).  
