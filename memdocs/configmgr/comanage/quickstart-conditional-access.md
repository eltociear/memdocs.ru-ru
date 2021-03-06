---
title: Условный доступ с совместным управлением
titleSuffix: Configuration Manager
description: Управление доступом пользователей к ресурсам организации на основе правил соответствия из Intune
ms.date: 05/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 4cf640b3-610c-4c3c-b966-c62e9f5654ff
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 94f002ecd12d08ffd5f3d4767e315e0d83714929
ms.sourcegitcommit: 9a700a72735f9a316bdb51c44f86f9cc3bfb7be2
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/21/2020
ms.locfileid: "83764056"
---
# <a name="conditional-access-with-co-management"></a>Условный доступ с совместным управлением

Совместный доступ гарантирует, что только доверенные пользователи смогут обращаться к ресурсам организации на доверенных устройствах через доверенные приложения. Это решение полностью создается в облаке. Взаимодействие выполняется совершенно одинаково для управления устройствами с помощью Intune и для применения совместного управления к развертыванию Configuration Manager.

В следующем видео руководитель программы Джоуи Глоке (Joey Glocke) и менеджер по маркетингу продуктов Локи Эйнли (Locky Ainley) обсуждают и демонстрируют условный доступ с совместным управлением:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/The-Security-Benefits-of-Conditional-Access/player]

Когда используется совместное управление, Intune оценивает каждое устройство в сети и определяет, насколько ему можно доверять. Для этой оценки применяются следующие два механизма.

1. Intune проверяет, что для устройства или приложения управление и настройка выполняются безопасно. Эта проверка зависит от того, как настроены политики соответствия в вашей организации. Например, можно проверять наличие шифрования и защиты на всех устройствах.  

    - Эта оценка выполняется на основе конфигурации и защиты от нарушений безопасности.  

    - Для совместно управляемых устройств в Configuration Manager также выполняется оценка на основе конфигурации. Например, можно проверять требуемые обновления и соответствие приложений требованиям. Intune сочетает собственную оценку с этими проверками.  

2. Intune обнаруживает инциденты безопасности на устройстве. Для этого используется интеллектуальная служба безопасности [Advanced Threat Protection в Защитнике Microsoft](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) (ранее ATP в Защитнике Windows) и другие [поставщики защиты мобильных устройств от угроз](https://www.lookout.com/about/partners/microsoft). Эти работающие вместе средства выполняют постоянный анализ поведения на устройствах. При таком анализе обнаруживаются активные инциденты и сведения о них передаются в Intune для оценки соответствия в реальном времени.  

    - Эта оценка основана на фактических инцидентах нарушения системы безопасности.  

Корпоративный вице-президент Майкрософт Брэд Андерсон (Brad Anderson) подробно описывает возможности условного доступа с практическими примерами во время выступления на конференции Ignite 2018. 

> [!VIDEO https://www.youtube.com/embed/7tDbUhVCX_I?start=1071]

Условный доступ также служит централизованным источником сведений о работоспособности всех устройств, подключенных к сети. Вы сможете использовать преимущества масштабирования в облаке, что особенно полезно для тестирования экземпляров Configuration Manager в рабочей среде.


## <a name="benefits"></a>Преимущества

Каждый ИТ-отдел предельно обеспокоен безопасностью сети. Каждое устройство, которому предоставляется доступ к сети, обязательно нужно проверить на соответствие требованиям безопасности и бизнеса. Условный доступ позволяет определить следующее: 
- применяется ли шифрование на всех устройствах;  
- установлены ли вредоносные программы;  
- своевременно ли обновляются настройки;  
- есть ли устройства со снятой защитой или административным доступом.  

Условный доступ объединяет в себе детальный контроль над данными организации и удобное взаимодействие с пользователем, позволяя повысить производительность работы всех сотрудников на любом устройстве и в любом месте.

В следующем видео показана интеграция службы [Расширенная защита от угроз](https://www.microsoft.com/windowsforbusiness/windows-atp) (ATP) в нескольких распространенных сценариях, с которыми вы регулярно встречаетесь:

> [!VIDEO https://www.youtube.com/embed/A7IrxAH87wc?start=178]

Благодаря совместному управлению Intune может применить обязанности Configuration Manager для оценки обновлений и (или) приложений на предмет соблюдения стандартов безопасности. Это важно для любой ИТ-организации, в которой Configuration Manager применяется для сложных сценариев управления приложениями и исправлениями.

Условный доступ также станет важной частью при разработке архитектуры сети по принципу ["Никому не доверяй"](https://cloudblogs.microsoft.com/microsoftsecure/2018/06/14/building-zero-trust-networks-with-microsoft-365/). Благодаря условному доступу средства управления доступом для соответствующих устройств распространяются на базовые уровни сети по принципу "Никому не доверяй". Эта функция станет важной основой для защиты вашей организации в будущем.

Дополнительные сведения см. в записи блога [о применении данных о рисках для компьютеров, собранных службой "Расширенная защита от угроз" в Microsoft Defender, в службе условного доступа](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Enhancing-conditional-access-with-machine-risk-data-from-Windows/ba-p/250559).



## <a name="case-studies"></a>Практические примеры

Консалтинговая ИТ-компания Wipro использует условный доступ для администрирования и защиты устройств, которые используются всеми сотрудниками, число которых составляет 91 000. В последнем исследовании вице-президент по вопросам ИТ компании Wipro отметил следующее:

> *Применение условного доступа — это большое достижение Wipro. Теперь все наши сотрудники получают доступ к информации с мобильных устройств по мере необходимости.* 
> *Мы смогли повысить уровень безопасности и производительность сотрудников. Все 91 000 сотрудников могут использовать надежно защищенный доступ к более чем 100 приложениям с любого устройства и из любого места.*

<!-- waiting for the case study to be public
For more information, see [Wipro drives mobile productivity with Microsoft cloud security tools to improve customer engagements](https://customers.microsoft.com/story/446f72f9-2f50-4697-b688-6d279786e010)
-->

Вот еще несколько примеров. 

- Nestlé использует условный доступ на основе приложений более чем для 150 000 сотрудников.  

- Компания Cadence, которая разрабатывает программное обеспечение для автоматизации, теперь может гарантировать, что "только управляемые устройства получают доступ к приложениям Office 365, например Teams, и к корпоративной интрасети". Также они предоставили своему персоналу "более безопасный доступ к другим облачным приложениям, например Workday и Salesforce". Дополнительные сведения о том, как компания Cadence применяет Intune для ускорения развития бизнеса благодаря мобильным средствам для совместной работы в Microsoft 365, вы найдете в [этой статье](https://customers.microsoft.com/story/cadence-partner-professional-services-microsoft-365).

Также Intune полностью интегрируется с такими партнерскими средствами, как Cisco ISE, Aruba Clear Pass и Citrix NetScaler. Эти партнерские средства позволяют сохранять те же элементы управления доступом, основанные на регистрации устройства в Intune и его состоянии соответствия требованиям, при работе с партнерскими платформами.

Дополнительные сведения см. в следующих видео:
- [Бред Андерсон (Brad Anderson) подробно демонстрирует работу условного доступа](https://youtu.be/8321obNofgM?t=547)  
- [Дополнительные сведения о зоне конечной точки 1805](https://youtu.be/f-ILlEuBFZg?t=196)  


## <a name="value-proposition"></a>Ценность предложения

С помощью условного доступа и интеграции ATP вы создадите важнейший для каждой ИТ-организации компонент, а именно защиту доступа к облаку.

Более чем 63 % нарушений конфиденциальности данных происходят из-за применения злоумышленниками слабых, стандартных или украденных учетных данных пользователей для доступа к сети организации. Условный доступ предназначен именно для защиты удостоверений пользователей, а значит, позволяет снизить кражу учетных данных. Условный доступ позволяет контролировать и защищать как привилегированные, так и непривилегированные удостоверения. Это самый лучший из существующих способов для защиты устройств и данных на них.

Так как условный доступ является основным компонентом Enterprise Mobility + Security (EMS), он не требует локальной установки или архитектуры. С помощью Intune и Azure Active Directory (Azure AD) вы можете быстро настроить условный доступ в облаке. Если вы используете Configuration Manager, вашу среду можно легко расширить в облако с помощью совместного управления и мгновенно начать его использовать.

Дополнительные сведения об интеграции ATP см. в записи блога [о том, как оценка риска для устройства ATP в Microsoft Defender помогает выявлять новые кибератаки и поддерживает условный доступ для защиты сетей](https://cloudblogs.microsoft.com/microsoftsecure/2018/11/28/windows-defender-atp-device-risk-score-exposes-new-cyberattack-drives-conditional-access-to-protect-networks/). В ней подробно описано, как группа хорошо подготовленных злоумышленников применила никогда ранее не использовавшиеся средства. Microsoft Cloud удалось обнаружить и остановить их действия благодаря тому, что потенциальные жертвы атаки применяли условный доступ. Вторжение привело к срабатыванию политики условного доступа на основе риска устройств. Несмотря на то, что злоумышленники уже захватили точку опоры в сети, все затронутые компьютеры были автоматически отрезаны от доступа к службам организации и данным под управлением Azure AD.



## <a name="configure"></a>Настройка

Условный доступ очень легко использовать, [включив совместное управление](how-to-enable.md). Для этого нужно переместить в Intune рабочую нагрузку **политик соответствия**. Дополнительные сведения см. в статье о [переключении рабочих нагрузок Configuration Manager на Intune](how-to-switch-workloads.md). 

Дополнительные сведения об использовании условного доступа см. в следующих статьях. 

- [Условный доступ в Azure Active Directory](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)  

- [Политики соответствия устройств Intune](https://docs.microsoft.com/intune/device-compliance)  

- [Условный доступ на основе приложений с помощью Intune](https://docs.microsoft.com/intune/app-based-conditional-access-intune)  

> [!Note]  
> Функции условного доступа сразу же становятся доступными для гибридных устройств, присоединенных к Azure AD. Сюда относятся многофакторная проверка подлинности и управление доступом для гибридных присоединений к Azure AD. Это поведение обусловлено тем, что они основаны на свойствах Azure AD. Чтобы использовать оценку в Intune и Configuration Manager на основе конфигурации, включите совместное управление. Такая конфигурация позволяет выполнять управление доступом для соответствующих устройств напрямую из Intune. Также вы сможете применять функцию Intune для оценки политик соответствия.  

