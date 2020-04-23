---
title: Мониторинг профилей сертификатов
titleSuffix: Configuration Manager
description: Сведения об отслеживании состояния соответствия для профилей сертификатов в Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 98feaa06-64b1-4e86-a122-93017c97cd4f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ee1f43e113aa91f75c09bd264e8b3bc2704220a8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706312"
---
# <a name="how-to-monitor-certificate-profiles-in-configuration-manager"></a>Мониторинг профилей сертификатов в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*


##  <a name="view-compliance-results-in-the-configuration-manager-console"></a>Просмотр результатов проверки на соответствие в консоли Configuration Manager  

Для отслеживания соответствия сертификатов SCEP не следует использовать консоль. Для этой цели используйте [отчеты](#view-compliance-results-by-using-reports). 

1. В консоли Configuration Manager щелкните **Наблюдение**>  **Развертывания**.  

2. Выберите необходимое развертывание профиля сертификата.  

3. Просмотрите сводные сведения о соответствии сертификата на главной странице. Для просмотра более подробных сведений выберите профиль сертификата, а затем на вкладке **Главная** в группе **Развертывание** выберите элемент **Просмотр состояния**, чтобы открыть страницу **Состояние развертывания**.  

    Страница **Состояние развертывания** содержит следующие вкладки.  

   -   **Соответствует**. Содержит сведения о соответствии профиля сертификата в зависимости от числа затронутых активов. Можно дважды щелкнуть правило, чтобы создать временный узел в узле **Пользователи** рабочей области **Активы и соответствие** . Этот узел будет включать всех пользователей, которые соответствуют профилю сертификата. В области **Сведения об активе** также отображаются пользователи, соответствующие данному профилю. Чтобы получить дополнительные сведения, дважды щелкните пользователя в списке.  

       > [!IMPORTANT]  
       >  Профиль сертификата не проверяется, если он неприменим к клиентскому устройству. Однако он возвращается как соответствующий.  

   -   **Ошибка**. Содержит список всех ошибок для выбранного развертывания профиля сертификата в зависимости от числа затронутых активов. Можно дважды щелкнуть правило, чтобы создать временный узел в узле **Пользователи** рабочей области **Активы и соответствие** . Этот узел будет включать всех пользователей, которые создали ошибки, связанные с данным профилем. При выборе пользователя в области **Сведения об активе** отображаются пользователи, затронутые выбранной проблемой. Чтобы получить дополнительные сведения, дважды щелкните пользователя в списке.  

   -   **Не соответствует**. Содержит список всех несоответствующих правил для профиля сертификата в зависимости от числа затронутых активов. Можно дважды щелкнуть правило, чтобы создать временный узел в узле **Пользователи** рабочей области **Активы и соответствие** . Этот узел будет включать всех пользователей, которые не соответствуют данному профилю. При выборе пользователя в области **Сведения об активе** отображаются пользователи, затронутые выбранной проблемой. Чтобы просмотреть дополнительные сведения о проблеме, дважды щелкните пользователя в списке.  

   -   **Неизвестно**. Содержит список всех пользователей, не передавших данные о соответствии для выбранного развертывания профиля сертификата, а также сведения о текущем состоянии клиента для устройств.  

4. На странице **Состояние развертывания** просмотрите подробные сведения о соответствии развернутого профиля сертификата. В узле **Развертывания** создается временный узел, который упрощает повторный поиск этих сведений.  

    Состояние регистрации сертификата отображается в виде числа. Воспользуйтесь следующей таблицей, чтобы понять, что означает каждое число.  


   | Состояние регистрации |                                                                                                                   Описание:                                                                                                                   |
   |-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |    0x00000001     |                                                                                         Регистрация успешно завершена, и выдан сертификат.                                                                                          |
   |    0x00000002     |                                                                    Запрос отправлен, и регистрация находится в состоянии ожидания, или запрос выдан вне диапазона.                                                                    |
   |    0x00000004     |                                                                                                          Регистрация должна быть отложена.                                                                                                           |
   |    0x00000010     |                                                                                                               Произошла ошибка.                                                                                                                |
   |    0x00000020     |                                                                                                        Состояние регистрации неизвестно.                                                                                                        |
   |    0x00000040     | Сведения о состоянии пропущены. Это может произойти, если центр сертификации HYPERLINK "<https://msdn.microsoft.com/windows/ms721572>" \l "_security_certification_authority_gly" является недопустимым или не был выбран для мониторинга. |
   |    0x00000100     |                                                                                                           В регистрации отказано.                                                                                                           |

##  <a name="view-compliance-results-by-using-reports"></a>Просмотр результатов проверки на соответствие с помощью отчетов

Параметры соответствия в Configuration Manager включают встроенные отчеты, с помощью которых можно отслеживать сведения о профилях сертификатов. Такие отчеты относятся к категории **Управление соответствием и параметрами**.  

> [!IMPORTANT]  
>  При использовании параметров **Фильтр устройств** и **Фильтр пользователей** в отчетах о параметрах соответствия необходимо использовать подстановочный знак (%).  

Для отслеживания соответствия сертификата SCEP используйте отчеты о сертификатах, которые находятся в узле отчетов **Доступ к ресурсам компании**.  

-   Журнал выдачи сертификатов  
-   Список активов с сертификатами с истекающим сроком действия  
-   Список активов по состоянию выдачи сертификата  



 Дополнительные сведения о настройке отчетов в Configuration Manager см. в разделе [Общие сведения об отчетах](../../core/servers/manage/introduction-to-reporting.md).  