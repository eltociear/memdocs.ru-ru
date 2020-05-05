---
title: Устранение неполадок с устройством
titleSuffix: Configuration Manager
description: Устранение неполадок в техническом справочнике по действиям устройств для Configuration Manager
ms.date: 04/01/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 44c2eb8a-3ccc-471f-838b-55d7971bb79e
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: 72da589a3f4213fb64b4123d5580cb1be945de0e
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "82140279"
---
# <a name="troubleshooting-device-actions-for-configuration-manager-devices"></a>Устранение неполадок в действиях устройств для Configuration Manager устройств

*Область применения: Configuration Manager (Current Branch)*

Начиная с Configuration Manager 2002, Configuration Manager клиенты могут быть синхронизированы с центром администрирования Microsoft Endpoint Manager. Некоторые клиентские действия можно запустить из центра администрирования Microsoft Endpoint Manager на синхронизированных клиентах.

Доступны следующие действия:
- Синхронизация политики компьютера
- Синхронизация политики пользователя
- Цикл оценки приложения


[![Обзор устройств в центре администрирования Microsoft Endpoint Manager](./media/3555758-device-overview-actions.png)](./media/3555758-device-overview-actions.png#lightbox)
  
Когда администратор выполняет действие центра администрирования Microsoft Endpoint Manager, запрос уведомления перенаправляется на Configuration Manager сайт и с сайта на клиент.

## <a name="configuration-manager-components"></a>Компоненты Configuration Manager

- **SMS_SERVICE_CONNECTOR**: использует рабочий процесс уведомления шлюза для обработки уведомления от центра администрирования Microsoft Endpoint Manager.
- **SMS_NOTIFICATION_SERVER**: получает уведомление и создает уведомление клиента.
- **Бгбажент**: клиент получает задачу и выполняет запрошенное действие.

## <a name="sms_service_connector"></a>SMS_SERVICE_CONNECTOR

Когда действие инициируется из центра администрирования Microsoft Endpoint Manager, запрос обрабатывается **кмгатевайнотификатионворкер. log** .  

```text
Received new notification. Validating basic notification details...
Validating device action message content...
Authorized to perform client action. TemplateID: RequestMachinePolicy TenantId: a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2 AADUserID:     a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2
Forwarded BGB remote task. TemplateID: 1 TaskGuid: a43dd1b3-a006-4604-b012-5529380b3b6f TaskParam: TargetDeviceIDs: 1  
```
 
1. Получено уведомление от центра администрирования Microsoft Endpoint Manager.

   ```text
   Received new notification. Validating basic notification details..
   ```

1. Проверка действий пользователей и устройств.

   ```text
   Validating device action message content... 
   Authorized to perform client action. TemplateID: RequestMachinePolicy TenantId: a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2 AADUserID:     a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2
   ```

1. Удаленная задача перенаправляется в SMS_NOTIFICATION_SERVER.

    ```text
   Forwarded BGB remote task. TemplateID: 1 TaskGuid: a43dd1b3-a006-4604-b012-5529380b3b6f TaskParam: TargetDeviceIDs: 1  
    ```


## <a name="sms_notification_server"></a>SMS_NOTIFICATION_SERVER

После отправки сообщения в SMS_NOTIFICATION_SERVER задача отправляется из точки управления в соответствующий клиент. В **BgbServer. log**, который находится в точке управления, вы увидите следующее:

```text
Get one push message from database.
Starting to send push task (PushID: 7 TaskID: 8 TaskGUID: A43DD1B3-A006-4604-B012-5529380B3B6F TaskType: 1 TaskParam: ) to 1 clients  with throttling (strategy: 1 param: 42)
```

## <a name="bgbagent"></a>бгбажент

Последний шаг выполняется на клиенте и может быть показан в **журнале ккмнотификатионажент. log**. Когда задача будет получена, она запросит у планировщика запрос на выполнение действия. При выполнении действия вы увидите сообщение с подтверждением:

```text
Receive task from server with pushid=7, taskid=8, taskguid=A43DD1B3-A006-4604-B012-5529380B3B6F, tasktype=1 and taskParam=

Send Task response message <BgbResponseMessage TimeStamp="2020-01-21T15:43:43Z"><PushID>8</PushID><TaskID>9</TaskID><ReturnCode>1</ReturnCode></BgbResponseMessage> successfully.
```

## <a name="common-issues"></a>Распространенные проблемы

Если у администратора нет необходимых разрешений в Configuration Manager, вы увидите `Unauthorized` ответ в **журнале кмгатевайнотификатионворкер. log**.

```text
Received new notification. Validating basic notification details..
Validating device action message content...
Unauthorized to perform client action. TemplateID: RequestMachinePolicy TenantId: a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2 AADUserID: 3a1e89e6-e190-4615-9d38-a208b0eb1c78
```  

Убедитесь, что пользователь, запускающий действие из центра администрирования Microsoft Endpoint Manager, имеет необходимые разрешения на Configuration Manager сайте. Дополнительные сведения см. в разделе [Предварительные требования к подключению клиента Microsoft Endpoint Manager](device-sync-actions.md#prerequisites).

## <a name="next-steps"></a>Дальнейшие действия

[Включите совместное управление](../comanage/overview.md) , чтобы получить дополнительные возможности на основе облака, такие как условный доступ.
