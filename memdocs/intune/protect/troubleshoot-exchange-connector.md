---
title: Устранение проблем в работе соединителя с Exchange
titleSuffix: Microsoft Intune
description: Устранение неполадок, связанных с работой соединителя Intune с локальной организацией Exchange.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/02/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: a7e3c742-295b-40bb-9afa-17f243062500
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: af44b09f5e539306a24ae0e0294b3ad674f7cb74
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/13/2020
ms.locfileid: "79338556"
---
# <a name="troubleshoot-the-intune-exchange-connector"></a>Устранение неполадок с соединителем Intune Exchange

Эта статья описывает устранение неполадок, связанных с работой соединителя Intune Exchange.

## <a name="before-you-start"></a>Перед началом работы

Прежде чем начать устранение неполадок в работе соединителя Exchange в Intune, соберите основные сведения, чтобы получить надежный фундамент для работы. Такой подход может помочь лучше понять природу проблемы и ускорить ее решение.

- Убедитесь, что процесс соответствует требованиям к установке. Перейдите к статье [Настройка локального соединителя Exchange для Intune](exchange-connector-install.md).
- Убедитесь, что у вашей учетной записи имеются разрешения администратора Exchange и Intune.
- Зафиксируйте полный и точный текст сообщения об ошибке, а также сведения и место отображения сообщения.
- Определите, когда появилась проблема: 
  - Вы настраиваете соединитель в первый раз? 
  - Соединитель работал правильно, а затем произошел сбой?
  - Если он работал, какие изменения произошли в среде Intune, среде Exchange или на компьютере, где запущено программное обеспечение соединителя?
- Что такое центр MDM?
- Какую версию Exchange вы используете?

### <a name="use-powershell-to-get-more-data-on-exchange-connector-issues"></a>Использование PowerShell для получения дополнительных сведений о неполадках в работе соединителя Exchange

- Чтобы получить список всех мобильных устройств для почтового ящика, воспользуйтесь командой `Get-ActiveSyncDeviceStatistics -mailbox mbx`
- Чтобы получить список SMTP-адресов для почтового ящика, воспользуйтесь командой `Get-Mailbox -Identity user | select emailaddresses | fl`
- Чтобы получить подробные сведения о состоянии доступа устройства, используйте команду `Get-CASMailbox <upn> | fl`.

## <a name="review-the-connector-configuration"></a>Просмотр конфигурации соединителя

Проверьте [требования к локальному соединителю Exchange](exchange-connector-install.md#intune-exchange-connector-requirements), чтобы убедиться, что среда и соединитель настроены правильно. 

### <a name="general-considerations-for-the-connector"></a>Общие рекомендации для соединителя

- Убедитесь, что брандмауэр и прокси-серверы разрешают обмен данными между сервером, на котором размещен соединитель Intune Exchange, и службой Intune.

- Компьютер, на котором размещен соединитель Intune с Exchange, и сервер клиентского доступа Exchange (CAS) должны быть присоединены к домену и находиться в одной локальной сети. Убедитесь, что для учетной записи, используемой соединителем Exchange с Intune, добавлены необходимые разрешения.

- Учетная запись уведомления используется для получения параметров *Автообнаружение*. Дополнительные сведения об автообнаружении в Exchange см. в разделе [Служба автообнаружения в Exchange Server](https://docs.microsoft.com/exchange/architecture/client-access/autodiscover?view=exchserver-2016).

- Соединитель Intune с Exchange отправляет запрос к URL-адресу EWS с помощью учетных данных учетной записи уведомления для отправки уведомлений по электронной почте вместе со ссылкой *Начало работы* (для регистрации в Intune). Для регистрации устройств Android, отличных от Knox, необходимо использовать ссылку *Начало работы*. В противном случае эти устройства будут заблокированы функцией условного доступа.

### <a name="common-issues-for-connector-configurations"></a>Распространенные проблемы, связанные с конфигурациями соединителей

- **Разрешения учетной записи**. В диалоговом окне "Microsoft Intune Exchange Connector" убедитесь, что указана учетная запись пользователя, имеющая соответствующие разрешения на выполнение [необходимых командлетов Exchange в Windows PowerShell](exchange-connector-install.md#exchange-cmdlet-requirements).
- **Сообщения электронной почты с уведомлениями**. Включите уведомления и укажите учетную запись уведомлений.
- **Синхронизация сервера клиентского доступа**. При настройке соединителя Exchange укажите сервер клиентского доступа (CAS), расположенный как можно ближе к серверу, где размещен соединитель Exchange. Задержка взаимодействия между CAS и соединителем Exchange может привести к задержкам обнаружения устройств, особенно при использовании Exchange Online (цен. категория "Выделенный").
- **Расписание синхронизации**: Пользователь с только что зарегистрированным устройством может испытывать задержки доступа, пока соединитель Exchange синхронизируется с Exchange CAS. Полная синхронизация выполняется один раз в день, а разностная (быстрая) синхронизация — несколько раз в день. Чтобы минимизировать задержки, вы можете [принудительно выполнить быструю или полную синхронизацию вручную](exchange-connector-install.md#manually-force-a-quick-sync-or-full-sync).

## <a name="next-steps"></a>Дальнейшие шаги
Сведения в следующих статьях могут помочь в устранении распространенных проблем и определенных ошибок.

- [Устранение распространенных проблем с соединителем Intune с Exchange](troubleshoot-exchange-connector-common-problems.md).
- [Устранение распространенных ошибок с соединителем Intune с Exchange](troubleshoot-exchange-connector-common-errors.md).

Обратитесь за помощью в службу поддержки или в сообщество Intune.

- Обратитесь к разделу [Поддержка](../fundamentals/get-support.md), чтобы использовать консоль Intune для устранения неполадок или для обращения в службу поддержки Майкрософт. 
- Опубликуйте свой вопрос на форумах [Microsoft Intune](https://social.technet.microsoft.com/Forums/en-US/home?forum=microsoftintuneprod).  
