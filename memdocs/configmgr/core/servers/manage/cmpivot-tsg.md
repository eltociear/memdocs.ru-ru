---
title: Устранение неполадок с CMPivot
titleSuffix: Configuration Manager
description: Сведения об устранении неполадок CMPivot в Configuration Manager.
ms.date: 10/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 36385bea-f05e-4300-947f-cb3927b3bac5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 69178f9ac1c1acb1ee2a2931c88a55a0784435b8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708022"
---
# <a name="troubleshoot-cmpivot"></a>Устранение неполадок с CMPivot

CMPivot — это средство, предоставляющее доступ к данным о состоянии устройств в вашей среде в реальном времени. Оно отправляет запрос на все подключенные устройства в целевой коллекции и возвращает результаты.

В работе CMPivot могут возникать неполадки. Например, если сообщение о состоянии, направляемое клиентом в CMPivot, повреждено, сервер сайта не сможет обработать сообщение. Эта статья поможет вам разобраться в процессе передачи данных для CMPivot.

## <a name="troubleshoot-cmpivot-in-version-1902-and-later"></a><a name="bkmk_CMPivot-1902"></a> Устранение неполадок с CMPivot в Configuration Manager 1902 и последующих версий

В Configuration Manager версии 1902 и последующих версиях CMPivot можно запускать на сайте центра администрирования в иерархии. Первичный сайт по-прежнему обеспечивает связь с клиентом.

При запуске CMPivot на сайте центра администрирования взаимодействие с первичным сайтом осуществляется по высокоскоростному каналу подписки на сообщения. CMPivot не использует стандартную репликацию SQL между сайтами. Если ваш экземпляр SQL Server или поставщик расположен удаленно или вы используете SQL Server Always On, у вас будет сценарий двойного прыжка для CMPivot. Сведения о том, как определить ограниченное делегирование для сценария двойного прыжка, см. в разделе [CMPivot с версии 1902](cmpivot.md#bkmk_cmpivot1902).

>[!IMPORTANT]
> При устранении неполадок с CMPivot включите подробное ведение журнала для точек управления и компонента SMS_MESSAGE_PROCESSING_ENGINE на сервере сайта для получения дополнительных сведений. Если при этом размер выходных данных клиента превышает 80 КБ, включите подробное ведение журнала для точки управления и компонента SMS_STATE_SYSTEM на сервере сайта. Сведения о том, как включить подробное ведение журнала, см. в разделе [Параметры ведения журнала для сервера сайта](../../plan-design/hierarchy/about-log-files.md#bkmk_reg-site).

### <a name="get-information-from-the-site-server"></a>Получение сведений с сервера сайта

По умолчанию файлы журналов сервера сайта находятся в папке `C:\Program Files\Microsoft Configuration Manager\logs`. Это расположение может быть иным, если вы выбрали другой каталог установки или перенесли такие компоненты, как поставщик SMS, на другой сервер. Если CMPivot запущен на сайте центра администрирования, журналы будут находиться на сервере основного сайта.

В файле `smsprov.log` найдите такие строки:

- Configuration Manager версии 1906:
  <pre><code lang="Log">Auditing: User &ltusername> initiated client operation 145 to collection &ltCollectionId>. </code></pre>

- Configuration Manager версии 1902:
  <pre><code lang="Log">Type parameter is 135.
  Auditing: User &ltusername> ran script 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14 with hash dc6c2ad05f1bfda88d880c54121c8b5cea6a394282425a88dd4d8714547dc4a2 on collection &ltCollectionId>. </code></pre>

 `7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14` — это идентификатор GUID скрипта для CMPivot. Этот идентификатор GUID можно также просмотреть в [сообщениях о состоянии аудита CMPivot](cmpivot.md#cmpivot-audit-status-messages).

Далее найдите идентификатор в окне CMPivot. Это `ClientOperationID`.

![Окно CMPivot с выделенным значением ClientOperationID](media/cmpivot-client-operationid-1902.png)

Найдите значение `TaskID`, полученное из таблицы ClientAction. `TaskID` соответствует значению `UniqueID` в таблице ClientAction.

``` SQL
select * from ClientAction where ClientOperationId=<id>
```

В `BgbServer.log` найдите значение `TaskID`, полученное из SQL, и обратите внимание на `PushID`. `TaskID` сопровождается указанием `TaskGUID`. Пример.

<pre><code lang="Log">Starting to send push task (<b>PushID: 9</b> TaskID: 12 <b>TaskGUID: 9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0</b> TaskType: 15 TaskParam: PFNjcmlwdENvbnRlbnQgU2NyaXB0R3VpZD0nN0RDNkI2RjEtRTdGNi00M0MxL (truncated log entry)
Finished sending push task (<b>PushID: 9</b> TaskID: 12) to 2 clients
</code></pre>

### <a name="client-logs"></a>Журналы клиента

Получив сведения с сервера сайта, проверьте журналы клиента. По умолчанию журналы клиента находятся в папке `C:\Windows\CCM\Logs`.

В `CcmNotificationAgent.log` найдите записи журнала, которые выглядят как следующие строки:  

<pre><code lang="Log">Receive task from server with <b>pushid=9</b>, taskid=12, <b>taskguid=9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0</b>, tasktype=15 and taskParam=PFNjcmlwdEhhc2ggU2NyaXB0SGF (truncated log entry)
Send Task response message &ltBgbResponseMessage TimeStamp="2019-09-13T17:29:09Z"><b>&ltPushID>5</b>&lt/PushID>&ltTaskID>4&lt/TaskID>&ltReturnCode>1&lt/ReturnCode>&lt/BgbResponseMessage> successfuly.
 </code></pre>

В файле `Scripts.log` найдите `TaskID`. В следующем примере `Task ID` имеет значение `{9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}`:

<pre><code lang="Log">Sending script state message (fast): <b>{9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}</b>
Result are sent for ScriptGuid: 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14 and <b>TaskID: {9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}</b>
</code></pre>

> [!NOTE]
> Если в журнале `Scripts.log` не отображается (fast), вероятно, что размер данных превышает 80 КБ. В этом случае сведения отправляются на сервер сайта в виде сообщения о состоянии. Используйте журнал `StateMessage.log` клиента и журнал `Statesys.log` сервера сайта.

### <a name="review-messages-on-the-site-server"></a>Просмотр сообщений на сервере сайта

Если в точке управления включено [подробное ведение журнала](../../plan-design/hierarchy/about-log-files.md#bkmk_reg-client), вы можете увидеть, как обрабатываются входящие клиентские сообщения. В `MP_RelayMsgMgr.log` найдите `TaskID`.

В примере с `MP_RelayMsgMgr.log` отображается идентификатор клиента `(GUID:83F67728-2E6D-4E4F-8075-ED035C31B783)` и `Task ID {9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}`. Идентификатор сообщения назначается ответу клиента перед его отправкой в подсистему обработки сообщений:

<pre><code lang="Log">MessageKey: GUID:83F67728-2E6D-4E4F-8075-ED035C31B783<b>{9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}</b>
Create message succeeded for <b>message id 22f00adf-181e-4bad-b35e-d18912f39f89</b>
Add message payload succeeded for message id 22f00adf-181e-4bad-b35e-d18912f39f89
Put message succeeded for message id 22f00adf-181e-4bad-b35e-d18912f39f89
CRelayMsgMgrHandler::HandleMessage(): ExecuteTask() succeeded
</code></pre>

Если для `SMS_MESSAGE_PROCESSING_ENGINE.log` включено [подробное ведение журнала](../../plan-design/hierarchy/about-log-files.md#bkmk_logoptions), результаты клиента будут обрабатываться. Используйте идентификатор сообщения из `MP_RelayMsgMgr.log`. Записи журнала обработки аналогичны приведенным ниже примерам.

<pre><code lang="Log">Processing 2 messages with type Instant and IDs <b>22f00adf-181e-4bad-b35e-d18912f39f89[19]</b>, 434d80ae-09d4-4d84-aebf-28a4a29a9852[20]...
Processed 2 messages with type Instant. Failed to process 0 messages. All message IDs <b>22f00adf-181e-4bad-b35e-d18912f39f89[19]</b>, 434d80ae-09d4-4d84-aebf-28a4a29a9852[20]
</code></pre>

> [!TIP]
> Если во время обработки возникает исключение, его можно просмотреть в столбце Exception, выполнив следующий SQL-запрос. После обработки сообщение больше не будет находиться в таблице `MPE_RequestMessages_Instant`.
>
> ```SQL
> select * from MPE_RequestMessages_Instant where MessageID=<ID from SMS_MESSAGE_PROCESSING_ENGINE.log>
> ```

В `BgbServer.log` найдите значение `PushID`, чтобы просмотреть количество клиентов, которые сообщили об ошибках.

<pre><code lang="Log">Generated BGB task status report c:\ConfigMgr\inboxes\bgb.box\Bgb5c1db.BTS at 09/16/2019 16:46:39. (<b>PushID: 9</b> ReportedClients: 2 FailedClients: 0)
</code></pre>

Проверьте представление мониторинга для CMPivot из SQL, используя значение `TaskID`.

``` SQL
select * from vSMS_CMPivotStatus where TaskID='{9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}'
```

[ ![SQL-запросы CMPivot для устранения неполадок в версии 1902](media/cmpivot-sql-queries-1902.png)](media/cmpivot-sql-queries-1902.png#lightbox)

## <a name="troubleshoot-cmpivot-in-1810-and-earlier"></a><a name="bkmk_CMPivot-1810"></a> Устранение неполадок с CMPivot в версии 1810 и предшествующих версиях

В Configuration Manager 1810 и прежних версиях обмен данными с клиентом обрабатывается сервером сайта.

### <a name="get-information-from-the-site-server"></a>Получение сведений с сервера сайта

По умолчанию файлы журналов сервера сайта находятся в папке `C:\Program Files\Microsoft Configuration Manager\logs`. Это расположение может быть иным, если вы выбрали другой каталог установки или перенесли такие компоненты, как поставщик SMS, на другой сервер.

В `smsprov.log` найдите такую строку:

<pre><code lang="Log">Auditing: User <username> initiated client operation 135 to collection &ltCollectionId>.
</code></pre>

Найдите идентификатор в окне CMPivot. Это `ClientOperationID`.

![Окно CMPivot с выделенным значением ClientOperationID](media/cmpivot-clientoperationid.png)

Найдите значение `TaskID`, полученное из таблицы ClientAction. `TaskID` соответствует значению `UniqueID` в таблице ClientAction.

``` SQL
select * from ClientAction where ClientOperationId=<id>
```

В `BgbServer.log` найдите значение `TaskID`, полученное из SQL. Оно помечено как `TaskGUID`. Пример.

<pre><code lang="Log">Starting to send push task (PushID: 260 TaskID: 258 TaskGUID: <b>F8C7C37F-B42B-4C0A-B050-2BB44DF1098A</b> TaskType: 15
TaskParam: PFNjcmlwdEhhc2ggU2NyaXB0SGF...truncated...to 5 clients with throttling (strategy: 1 param: 42)
Finished sending push task (PushID: 260 TaskID: 258) to 5 clients
</code></pre>

### <a name="client-logs"></a>Журналы клиента

Получив сведения с сервера сайта, проверьте журналы клиента. По умолчанию журналы клиента находятся в папке `C:\Windows\CCM\Logs`.

В `CcmNotificationAgent.log` найдите журналы, аналогичные приведенным ниже.  

<pre><code lang="Log"><b>Error! Bookmark not defined.</b>+PFNjcmlwdEhhc2ggU2NyaXB0SGFzaEFsZz0nU0hBMjU2Jz42YzZmNDY0OGYzZjU3M2MyNTQyNWZiNT
g2ZDVjYTIwNzRjNmViZmQ1NTg5MDZlMWI5NDRmYTEzNmFiMDE0ZGNjPC9TY3JpcHRIYXNoPjxTY3Jp (truncated log entry)
</code></pre>

В файле `Scripts.log` найдите `TaskID`. В следующем примере `Task ID {F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}` имеет такое значение:

<pre><code lang="Log">Sending script state message: 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14
State message: Task Id <b>{F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}</b>
</code></pre>

Просмотрите `StateMessage.log`. В следующем примере видно, что `TaskID` находится ближе к концу сообщения рядом с `<Param>`:

``` XML
StateMessage body: <?xml version="1.0" encoding="UTF-16"?>
<Report><ReportHeader><Identification><Machine><ClientInstalled>1</ClientInstalled><ClientType>1
</ClientType><ClientID>GUID:DBAC52C9-57E6-47D7-A8D6-E0A5A64B57E6</ClientID><ClientVersion>5.00.8670.1000</ClientVersion>
<NetBIOSName>R613924</NetBIOSName><CodePage>437</CodePage>
<SystemDefaultLCID>1033</SystemDefaultLCID><Priority>0</Priority></Machine></Identification>
<ReportDetails><ReportContent>State Message Data</ReportContent><ReportType>Full</ReportType>
<Date>20180703184447.673000+000</Date><Version>1.0</Version><Format>1.0</Format>
</ReportDetails></ReportHeader><ReportBody><StateMessage MessageTime="20180703184447.517000+000"><Topic ID="7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14" Type="9003" IDType="0" User="" UserSID=""/><State ID="1" Criticality="0"/>
<StateDetails Type="1"><![CDATA["PAA/AHgAbQBsACAAdgBlAHIAcwBpAG8AbgA9ACIAMQAuADAAIgAgAGUAbgBjAG8AZABpAG4AZwA9ACIAdQB0AGYALQAxADYAIgA/AD4APAByAGUAcwB1AGwAdAAgAFIAZQBzAHUAbAB0AEMAbwBkAGUAPQAiADAAIgA+ADwAZQAgAE4AYQBtAGUAPQAiAEkAbgB0AGUAbAAoAFIAKQAgAFgAZQBvAG4AKABSACkAIABDAFAAVQAgAEUANQAtADIANgA3ADMAIAB2ADQAIABAACAAMgAuADMAMABHAEgAegAiACAATQBhAG4AdQBmAGEAYwB0AHUAcgBlAHIAPQAiAEEAbQBlAHIAaQBjAGEAbgAgAE0AZQBnAGEAdAByAGUAbgBkAHMAIABJAG4AYwAuACIAIABWAGUAcgBzAGkAbwBuAD0AIgBWAFIAVABVAEEATAAgAC0AIAA2ADAAMAAxADcAMAAyACIAIABSAGUAbABlAGEAcwBlAEQAYQB0AGUAPQAiADIAMAAxADcALQAwADYALQAwADIAIAAwADAAOgAwADAAOgAwADAAIgAgAFMAZQByAGkAYQBsAE4AdQBtAGIAZQByAD0AIgAwADAAMAAwAC0AMAAwADEAOAAtADMANgA4ADIALQA0ADcAMAA4AC0ANwA2ADQAMAAtADcANgAwADAALQAzADMAIgAgAFMATQBCAEkATwBTAEIASQBPAFMAVgBlAHIAcwBpAG8AbgA9ACIAMAA5ADAAMAAwADcAIAAiACAALwA+ADwALwByAGUAcwB1AGwAdAA+AA=="~~]]></StateDetails><UserParameters Flags="0" Count="2">
<Param>{F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}</Param><Param>0</Param></UserParameters></StateMessage></ReportBody></Report>

Successfully forwarded State Messages to the MP StateMessage 7/3/2018 11:44:47 AM 5036 (0x13AC)
```

### <a name="review-messages-on-the-site-server"></a>Просмотр сообщений на сервере сайта

Откройте файл `statesys.log`, чтобы проверить, было ли сообщение получено и обработано. В следующем примере видно, что `TaskID` находится ближе к концу сообщения рядом с `<Param>`. Чтобы просмотреть эти записи журнала, необходимо включить [подробное ведение журнала](../../plan-design/hierarchy/about-log-files.md#bkmk_logoptions) для компонента SMS_STATE_SYSTEM.

``` XML
CMessageProcessor - the cmdline to DB exec dbo.spProcessStateReport N'?<?xml version="1.0" encoding="UTF-
16"?>~~<Report><ReportHeader><Identification><Machine><ClientInstalled>1</ClientInstalled><ClientType>1
</ClientType><ClientID>GUID:DBAC52C9-57E6-47D7-A8D6-E0A5A64B57E6</ClientID><ClientVersion>5.00.8670.1000</ClientVersion>
<NetBIOSName>R613924</NetBIOSName><CodePage>437</CodePage>
<SystemDefaultLCID>1033</SystemDefaultLCID><Priority>0</Priority></Machine></Identification>
<ReportDetails><ReportContent>State Message Data</ReportContent><ReportType>Full</ReportType>
<Date>20180703184447.673000+000</Date><Version>1.0</Version><Format>1.0</Format>
</ReportDetails></ReportHeader><ReportBody><StateMessage MessageTime="20180703184447.517000+000"><Topic ID="7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14" Type="9003" IDType="0" User="" UserSID=""/><State ID="1" Criticality="0"/>
<StateDetails Type="1"><![CDATA["PAA/AHgAbQBsACAAdgBlAHIAcwBpAG8AbgA9ACIAMQAuADAAIgAgAGUAbgBjAG8AZABpAG4AZwA9ACIAdQB0AGYALQAxADYAIgA/AD4APAByAGUAcwB1AGwAdAAgAFIAZQBzAHUAbAB0AEMAbwBkAGUAPQAiADAAIgA+ADwAZQAgAE4AYQBtAGUAPQAiAEkAbgB0AGUAbAAoAFIAKQAgAFgAZQBvAG4AKABSACkAIABDAFAAVQAgAEUANQAtADIANgA3ADMAIAB2ADQAIABAACAAMgAuADMAMABHAEgAegAiACAATQBhAG4AdQBmAGEAYwB0AHUAcgBlAHIAPQAiAEEAbQBlAHIAaQBjAGEAbgAgAE0AZQBnAGEAdAByAGUAbgBkAHMAIABJAG4AYwAuACIAIABWAGUAcgBzAGkAbwBuAD0AIgBWAFIAVABVAEEATAAgAC0AIAA2ADAAMAAxADcAMAAyACIAIABSAGUAbABlAGEAcwBlAEQAYQB0AGUAPQAiADIAMAAxADcALQAwADYALQAwADIAIAAwADAAOgAwADAAOgAwADAAIgAgAFMAZQByAGkAYQBsAE4AdQBtAGIAZQByAD0AIgAwADAAMAAwAC0AMAAwADEAOAAtADMANgA4ADIALQA0ADcAMAA4AC0ANwA2ADQAMAAtADcANgAwADAALQAzADMAIgAgAFMATQBCAEkATwBTAEIASQBPAFMAVgBlAHIAcwBpAG8AbgA9ACIAMAA5ADAAMAAwADcAIAAiACAALwA+ADwALwByAGUAcwB1AGwAdAA+AA=="~~]]></StateDetails><UserParameters Flags="0" Count="2">
<Param>{F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}</Param><Param>0</Param></UserParameters></StateMessage></ReportBody></Report>~~'
```

Если сообщение не было обработано, проверьте папку входящих сообщений о состоянии. По умолчанию она расположена здесь: `C:\Program Files\Microsoft Configuration Manager\inboxes\auth\statesys.box\`. Просмотрите файлы в следующих расположениях:

- Входящие
- Поврежденные
- Как это работает

Проверьте представление мониторинга для CMPivot из SQL, используя значение `TaskID`.

``` SQL
select * from vSMS_CMPivotStatus where TaskID='{F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}'
```

>[!NOTE]
>Для клиентов, использующих версию 1810 или более позднюю, сообщения о состоянии не используются, если размер выходных данных превышает 80 КБ. При устранении неполадок с CMPivot в таких случаях включите подробное ведение журнала для точки управления и SMS_MESSAGE_PROCESSING_ENGINE сервера сайта, чтобы получить дополнительные сведения. Сведения о том, как включить подробное ведение журнала, см. в разделе [Параметры ведения журнала для сервера сайта](../../plan-design/hierarchy/about-log-files.md#bkmk_reg-site).
>
> Для устранения неполадок используйте следующие журналы.
>
> - `MP_Relay.log`
> - `SMS_MESSAGE_PROCESSING_ENGINE.log`

## <a name="next-steps"></a>Дальнейшие действия

- [Использование CMPivot](cmpivot.md)
- [Создание и выполнение сценариев PowerShell](../../../apps/deploy-use/create-deploy-scripts.md)
