---
title: Advanced Threat Protection в Microsoft Defender
titleSuffix: Configuration Manager
description: Узнайте о возможностях управления и мониторинга новой службы Advanced Threat Protection в Microsoft Defender, которая помогает предприятию противостоять сложным кибератакам.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a5fc033e-828e-4e45-9097-bbbd0697ebdf
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 186751bb8b1768b34573e2b614ce992b58fa9232
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706242"
---
# <a name="microsoft-defender-advanced-threat-protection"></a>Advanced Threat Protection в Microsoft Defender

*Область применения: Configuration Manager (Current Branch)*

Endpoint Protection помогает отслеживать службу [Расширенная защита от угроз (ATP) в Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) (прежнее название — ATP в Защитнике Windows). Служба ATP в Microsoft Defender помогает предприятиям обнаруживать и анализировать сложные атаки в своих сетях и принимать необходимые меры. Политики Configuration Manager помогут вам подключить клиентов Windows 10 и отслеживать их.

Служба ATP в Microsoft Defender доступна в интерфейсе [Безопасность Windows](https://securitycenter.windows.com). Добавив специальный файл конфигурации для подключения клиента и развернув эту конфигурацию, вы сможете использовать Configuration Manager для мониторинга состояния развертывания и работоспособности агента ATP в Microsoft Defender. ATP в Microsoft Defender поддерживается на компьютерах с клиентом Configuration Manager или [под управлением Microsoft Intune](https://docs.microsoft.com/intune/protect/advanced-threat-protection).

## <a name="prerequisites"></a>Предварительные условия

- Подписка на веб-службу Advanced Threat Protection в Microsoft Defender  
- Клиентские компьютеры под управлением клиента Configuration Manager
- Клиенты, использующие ОС из раздела [Поддерживаемые клиентские операционные системы](#bkmk_os). 

### <a name="supported-client-operating-systems"></a><a name="bkmk_os"></a> Поддерживаемые клиентские операционные системы
В зависимости от используемой версии Configuration Manager можно подключить следующие клиентские операционные системы.

#### <a name="configuration-manager-version-1910-and-prior"></a>Configuration Manager версии 1910 и более ранних

- Клиентские компьютеры под управлением Windows 10 версии 1607 и выше

#### <a name="configuration-manager-version-2002-and-later"></a>Configuration Manager версии 2002 и более поздних
<!--5229962-->
- Windows 7 с пакетом обновления 1 (SP1);
- Windows 8.1
- Windows 10 версии 1607 или более поздней
- Windows Server 2008 R2 с пакетом обновления 1 (SP1)
- Windows Server 2012 R2
- Windows Server 2016
- Windows Server 2016, версия 1803
- Windows Server 2019

## <a name="create-an-onboarding-configuration-file"></a>Создание файла конфигурации подключения

1. Войдите в веб-службу [ATP в Microsoft Defender](https://securitycenter.windows.com/).
1. В разделе **Параметры** выберите **Управление компьютером**, а затем выберите **Подключение**.
1. Выберите операционные системы, которые вы хотите подключить, из списка.
   - Если вы подключаете Windows 10, Windows Server 1803 и Windows Server 2019
      1. Выберите **Configuration Manager (текущая ветвь) версии 1606** и нажмите кнопку **Скачать пакет**.
      1. Скачайте сжатый файл архива (ZIP-файл) и извлеките его содержимое.
   - Если вы подключаете другую операционную систему Windows 
      1. Выберите операционные системы, которые вы хотите подключить, из списка. Например, выберите **Windows 7 и 8.1** или **Windows Server 2008 R2 SP1, 2012 R2 и 2016**.
      1. Скопируйте значения **ключа рабочей области** и **идентификатора рабочей области** из раздела **Настройка подключения** после завершения процесса.

> [!IMPORTANT]
> Файл конфигурации ATP в Microsoft Defender содержит конфиденциальные сведения, которые должны быть защищены.

## <a name="onboard-devices"></a>Подключенные устройства

1. В консоли Configuration Manager последовательно выберите **Активы и соответствие** > **Endpoint Protection** > **Политики ATP в Защитнике Windows** и щелкните **Создать политику ATP в Защитнике Windows**. Откроется мастер политик ATP в Microsoft Defender.  
1. Введите **Имя** и **Описание** политики ATP в Microsoft Defender и выберите **Подключение**.
1. Выберите **Обзор** и укажите файл конфигурации, предоставленный клиентом облачной службы ATP в Microsoft Defender вашей организации.
   - Для **Windows 7 и 8.1** или **Windows Server 2008 R2 SP1, 2012 R2 и 2016** укажите **ключ рабочей области** и **идентификатор рабочей области**.
1. Укажите образцы файлов, которые собираются и совместно используются с управляемых устройств для анализа.  

   - **Нет**

   - **Все типы файлов**  
1. Просмотрите сводные данные и завершите работу мастера.  

Выберите **Развернуть**, чтобы нацелить политику ATP в Microsoft Defender на клиенты.

## <a name="monitor"></a>Монитор

1. В консоли Configuration Manager последовательно выберите **Мониторинг** > **Безопасность** и щелкните **ATP в Microsoft Defender**.  

1. Просмотрите сведения на панели мониторинга Advanced Threat Protection в Microsoft Defender.  

    - **Состояния развертывания агента Защитнике WIndows**. Количество и процент доступных управляемых клиентских компьютеров с активной подключенной политикой ATP в Microsoft Defender.  

    - **Работоспособность агента ATP в Защитнике WIndows**. Процент клиентских компьютеров, сообщающих о состоянии для своего агента ATP в Microsoft Defender.  

        - **Работоспособно** — работает должным образом.  

        - **Неактивно** — в течение определенного периода времени данные в службу не отправляются.  

        - **Состояние агента** — системная служба для агента в Windows не запущена.  

        - **Не подключено** — политика была применена, но агент не сообщил о ее подключении.  

## <a name="create-an-offboarding-configuration-file"></a>Создание файла конфигурации отключения  

1. Войдите в [веб-службу ATP в Microsoft Defender](https://securitycenter.windows.com/).

1. В разделе **Параметры** выберите **Управление компьютером**, а затем выберите **Подключение**.  

1. Выберите **Configuration Manager (текущая ветвь) версии 1606** и нажмите кнопку **Отключить конечную точку**.  

1. Скачайте сжатый файл архива (ZIP-файл) и извлеките его содержимое. Файлы отключения действуют в течение 30 дней.

1. В консоли Configuration Manager последовательно выберите **Активы и соответствие** > **Endpoint Protection** > **Политики ATP в Защитнике Windows** и щелкните **Создать политику ATP в Защитнике Windows**. Откроется мастер политик ATP в Microsoft Defender.  

1. Введите **Имя** и **Описание** политики ATP в Microsoft Defender и выберите **Отключение**.

1. Выберите **Обзор** и укажите файл конфигурации, предоставленный клиентом облачной службы ATP в Microsoft Defender вашей организации.

1. Просмотрите сводные данные и завершите работу мастера.  

Выберите **Развернуть**, чтобы нацелить политику ATP в Microsoft Defender на клиенты.  

> [!IMPORTANT]
> Файлы конфигурации ATP в Microsoft Defender содержат конфиденциальные сведения, которые должны быть защищены.

## <a name="next-steps"></a>Дальнейшие шаги

- [Advanced Threat Protection в Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection)

- [Устранение неполадок с подключением Advanced Threat Protection в Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/troubleshoot-onboarding)
