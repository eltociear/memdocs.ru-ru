---
title: Установка клиента с помощью Azure AD
titleSuffix: Configuration Manager
description: Установка и назначение клиента Configuration Manager на устройствах Windows 10 с проверкой подлинности при помощи Azure AD
ms.date: 03/20/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a44006eb-8650-49f6-94e1-18fa0ca959ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9a55440e7ba61ec62d9f0c91c0a23b98bab5884c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694112"
---
# <a name="install-and-assign-configuration-manager-windows-10-clients-using-azure-ad-for-authentication"></a>Установка и назначение клиентов Configuration Manager для Windows 10 с проверкой подлинности при помощи Azure AD

Чтобы установить клиент Configuration Manager на устройствах Windows 10 с использованием проверки подлинности Azure AD, интегрируйте Configuration Manager с Azure Active Directory (Azure AD). Эти клиенты могут находиться в интрасети и напрямую взаимодействовать с точкой управления, поддерживающей HTTPS, или любой точкой управления на сайте с включенной поддержкой улучшенного протокола HTTP. Кроме того, это могут быть клиенты в Интернете, взаимодействующие с интернет-точкой управления или через шлюз управления облачными клиентами. В этом процессе для проверки подлинности клиентов, обращающихся к сайтам Configuration Manager, используется Azure AD. Azure AD избавляет от необходимости настраивать и применять клиентские сертификаты для аутентификации.

Настройка Azure AD может быть проще для некоторых клиентов, чем настройка инфраструктуры открытого ключа для проверки подлинности на основе сертификатов. Существуют компоненты, требующие подключения к Azure AD сайта, но не требующие подключения клиентов.<!-- SCCMDocs issue 1259 --> Дополнительные сведения см. в следующих статьях:

- [Планирование Azure Active Directory](../../plan-design/security/plan-for-security.md#bkmk_planazuread)
- [Использование Azure AD для совместного управления](../../../comanage/quickstart-hybrid-aad.md)

## <a name="before-you-begin"></a>Подготовка к работе

- Вам потребуется клиент Azure AD.  

- Требования к устройствам  

  - быть под управлением ОС Windows 10;  

  - Устройство должно входить в состав Azure AD — допускается либо только облачное присоединение к домену, либо гибридное присоединение к Azure AD.  

- Требования к пользователю  

  - Вошедший в систему пользователь должен иметь удостоверение Azure AD.

  - Если пользователь имеет федеративное или синхронизированное удостоверение, необходимо использовать [обнаружение пользователей Active Directory](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser) Configuration Manager, а также [обнаружение пользователей Azure AD](../../servers/deploy/configure/about-discovery-methods.md#azureaddisc). Дополнительные сведения о гибридных удостоверениях см. в разделе [Определение стратегии внедрения гибридной идентификации](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-identity-adoption-strategy).<!--497750-->  

- Помимо выполнения [существующих предварительных требований](../../plan-design/configs/site-and-site-system-prerequisites.md#bkmk_2012MPpreq) к роли системы сайта "Точка управления", активируйте **ASP.NET 4.5** на этом сервере. Включите другие параметры, которые выбираются автоматически при активации ASP.NET 4.5.  

- Определите, требуется ли поддержка HTTPS для точки управления. Дополнительные сведения см. в статье [Включение точки управления для HTTPS](../manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_mphttps).  

- Чтобы развернуть интернет-клиенты, можно настроить [шлюз управления облачными клиентами](../manage/cmg/plan-cloud-management-gateway.md) (CMG). Для локальных клиентов, на которых применяется проверка подлинности с помощью Azure AD, шлюз CMG не требуется.  

> [!TIP]
> Начиная с версии 2002,<!--5686290--> Configuration Manager также предоставляет поддержку для интернет-клиентов, которые не так часто подключаются к внутренней сети, не могут присоединяться к Azure Active Directory (Azure AD) и для которых не предусмотрен метод установки сертификата, выданного PKI. Дополнительные сведения см. в разделе [Маркеры проверки подлинности в шлюзе управления облачными клиентами](deploy-clients-cmg-token.md).

## <a name="configure-azure-services-for-cloud-management"></a>Настройка служб Azure для управления облачными клиентами

Первым шагом является подключение сайта Configuration Manager к Azure AD. Подробные сведения об этом процессе см. в статье [Настройка служб Azure](../../servers/deploy/configure/azure-services-wizard.md). Создайте подключение к службе **Управление облачными клиентами**.

В ходе внедрения службы **Управление облачными клиентами** включите [обнаружение пользователей Azure AD](../../servers/deploy/configure/configure-discovery-methods.md#azureaadisc).

После выполнения этих действий ваш сайт Configuration Manager буде подключен к Azure AD.

## <a name="configure-client-settings"></a>Настройка параметров клиента

Эти параметры клиента используются для присоединения устройств Windows 10 к Azure AD. Они также позволяют интернет-клиентам использовать шлюз CMG и облачную точку распространения.

1. Настройте следующие параметры клиента (в разделе **Облачные службы**), используя сведения из статьи [Настройка параметров клиента](configure-client-settings.md).  

    - **Разрешить доступ к точке распространения в облаке**. Включите этот параметр, чтобы подключенные через Интернет устройства могли получить содержимое, которое требуется для установки клиента Configuration Manager. Если содержимое недоступно в облачной точке распространения, устройства могут получить содержимое из шлюза CMG. Начальная загрузка установки клиента повторно обращается к облачной точке распространения в течение четырех часов, после чего она возвращается к CMG.<!--495533-->  

    - **Автоматически регистрировать новые присоединенные к домену устройства с Windows 10 в Azure Active Directory**. Установите значение **Да** или **Нет**. Значение по умолчанию — **Да**. Это поведение также используется по умолчанию в Windows 10 версии 1709.

    - **Разрешение клиентам использовать шлюз управления облачными клиентами**. Задайте значение **Да** (по умолчанию) или **Нет**.  

2. Разверните параметры клиента в нужную коллекцию устройств. Не развертывайте эти параметры для коллекций пользователей.

Чтобы подтвердить, что устройство присоединено к Azure AD, выполните `dsregcmd.exe /status` в командной строке. Если устройство присоединено к Azure AD, в поле **AzureAdjoined** отображается значение **Да**.

## <a name="install-and-register-the-client-using-azure-ad-identity"></a>Установка и регистрация клиента с помощью удостоверения Azure AD

Чтобы вручную установить клиент, используя удостоверение Azure AD, сначала ознакомьтесь с общим процессом в разделе [Установка клиентов вручную](deploy-clients-to-windows-computers.md#BKMK_Manual).

 > [!Note]  
 > Для связи с Azure AD устройству требуется доступ к Интернету, но оно не должно быть интернет-устройством.

В следующем примере показана общая структура командной строки: `ccmsetup.exe /mp:<source management point> CCMHOSTNAME=<internet-based management point> SMSSiteCode=<site code> SMSMP=<initial management point> AADTENANTID=<Azure AD tenant identifier> AADCLIENTAPPID=<Azure AD client app identifier> AADRESOURCEURI=<Azure AD server app identifier>`

Дополнительные сведения см. в статье [Свойства установки клиента](about-client-installation-properties.md).

В зависимости от сценария параметр **/mp** и свойство **CCMHOSTNAME** указывают один из следующих компонентов.

- Локальная точка управления. Следует указать только параметр **/mp**. Свойство **CCMHOSTNAME** указывать не требуется.
- Шлюз управления облаком
- интернет-точка управления;

Свойство **SMSMP** указывает локальную или интернет-точку управления.

В этом примере используется шлюз управления облачными клиентами. Он подставляет образцы значений: `ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC SMSMP=https://mp1.contoso.com AADTENANTID=daf4a1c2-3a0c-401b-966f-0b855d3abd1a AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver`

Сайт публикует дополнительные сведения, связанные с Azure AD, в шлюзе управления облачными клиентами. Присоединенный к домену AD клиент Azure получает эти сведения из шлюза управления облачными клиентами во время процесса ccmsetup, используя тот же клиент, к которому он присоединен. Такое поведение дополнительно упрощает установку клиента в среде с несколькими арендаторами Azure AD. Нужны только два свойства ccmsetup: **CCMHOSTNAME** и **SMSSiteCode**.<!--3607731-->

Автоматизировать установку клиента с использованием удостоверения Azure AD в Microsoft Intune помогут инструкции в разделе о [подготовке интернет-устройств к совместному управлению](../../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client).

## <a name="next-steps"></a>Дальнейшие шаги

Завершив эти действия, переходите к статье [Мониторинг клиентов в System Center Configuration Manager](../manage/monitor-clients.md).
