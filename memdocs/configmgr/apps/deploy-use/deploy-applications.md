---
title: Развертывание приложений
titleSuffix: Configuration Manager
description: Создание или имитация развертывания приложения в коллекции пользователей или устройств
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2629c376-ec43-4f0e-a78b-4223cc9302bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a7bbf395a5de98459043609986e51647362e7a0b
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075342"
---
# <a name="deploy-applications-with-configuration-manager"></a>Развертывание приложений с помощью Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Создавайте или имитируйте развертывания приложения в коллекции пользователей или устройств в Configuration Manager. Это развертывание предоставляет клиенту Configuration Manager инструкции о том, как и когда установить программное обеспечение.

Перед развертыванием приложения создайте хотя бы один тип развертывания для приложения. Дополнительные сведения см. в статье [Создание приложений](create-applications.md).

Начиная с версии 1906 вы можете создать группу приложений для отправки пользователю или коллекцию устройств как одно развертывание. Дополнительные сведения см. в статье [Создание групп приложений](create-app-groups.md).

Кроме того, вы можете имитировать развертывание приложения. Имитация позволяет проверить применимость развертывания, не устанавливая и не удаляя приложение. Имитация развертывания позволяет выполнить оценку метода обнаружения, требований и зависимостей для данного типа развертывания. Результаты оценки отображаются в узле **Развертывания** рабочей области **Наблюдение**. Дополнительные сведения см. в статье [Имитация развертываний приложений в System Center Configuration Manager](simulate-application-deployments.md).

> [!Note]
> Вы можете имитировать развертывание только необходимых приложений, но не пакетов или обновлений программного обеспечения.
>
> Устройства, зарегистрированные в системе управления мобильными устройствами, не поддерживают имитацию развертывания, взаимодействие с пользователем и параметры планирования.



## <a name="deploy-an-application"></a><a name="bkmk_deploy"></a> Развертывание приложения

1. В консоли Configuration Manager перейдите в рабочую область **Библиотека программного обеспечения**, разверните узел **Управление приложениями** и выберите узел **Приложения** или **Группы приложений**.

2. Выберите приложение или группу приложений из списка для развертывания. На ленте щелкните **Развернуть**.  

> [!Note]  
> При просмотре свойств существующего развертывания следующие разделы соответствуют вкладкам в окне свойств развертывания:  
>
> - [Общие](#bkmk_deploy-general)
> - [Содержимое](#bkmk_deploy-content)
> - [Параметры развертывания](#bkmk_deploy-settings)
> - [Планирование](#bkmk_deploy-sched)
> - [Взаимодействие с пользователем](#bkmk_deploy-ux)
> - [Предупреждения](#bkmk_deploy-alerts)


### <a name="deployment-general-information"></a><a name="bkmk_deploy-general"></a>**Общие** сведения о развертывании

На странице **Общие** мастера развертывания программного обеспечения укажите приведенные ниже сведения.  

- **Программное обеспечение**: Это значение содержит приложение, которое требуется развернуть. Чтобы выбрать другое приложение, нажмите кнопку **Обзор**.  

- **Коллекция**. Нажмите кнопку **Обзор**, чтобы выбрать коллекцию, в которой требуется развернуть приложение.  

- **Использовать группы точек распространения по умолчанию, связанные с этой коллекцией**. Содержимое приложения сохраняется в используемой по умолчанию группе точки распространения коллекции. Этот параметр недоступен, если выбранная коллекция не была связана с группой точек распространения.  

- **Автоматически распространять содержимое для зависимостей**. Если какой-либо тип развертывания в приложении содержит зависимости, содержимое зависимого приложения также будет отправляться в точки распространения.  

    >[!Note]  
    > При обновлении зависимого приложения после развертывания основного приложения сайт не будет автоматически распространять новое содержимое для зависимости.  

- **Комментарии (необязательно)** . При необходимости введите описание для этого развертывания.  


### <a name="deployment-content-options"></a><a name="bkmk_deploy-content"></a> Параметры **содержимого** для развертывания

На странице **Содержимое** нажмите кнопку **Добавить**, чтобы передать содержимое для этого приложения в точку распространения или группу точек распространения.

Этот параметр задается автоматически при выборе параметра **Использовать точки распространения по умолчанию, связанные с этой коллекцией** на странице "Общие". Этот параметр может изменить только член роли безопасности **Администратор приложений**.

Если содержимое приложения уже распространено, оно приводится здесь.


### <a name="deployment-settings"></a><a name="bkmk_deploy-settings"></a>**Параметры развертывания**

На странице **Параметры развертывания** укажите следующие сведения:  

- **Действие**. В раскрывающемся списке выберите цель развертывания: **Установка** или **Удаление** приложения.  

    > [!NOTE]  
    > Если вы создаете развертывание для **установки** приложения и еще одно развертывание для **удаления** этого же приложения с того же устройства, развертывание типа **Установка** имеет приоритет.  

    Созданное действие развертывания изменить нельзя.  

- **Назначение**. В раскрывающемся списке выберите одно из следующих значений.  

  - **Доступное**. Пользователь видит приложение в центре программного обеспечения. Он может установить его по требованию.  

  - **Обязательное**. Клиент автоматически устанавливает приложение в соответствии с настроенным расписанием. Если приложение не скрыто, пользователь может отслеживать его состояние развертывания. Он также может установить приложение с помощью центра программного обеспечения до наступления крайнего срока.  

    > [!NOTE]  
    > Если в качестве действия развертывания выбрано **Удаление**, намерение развертывания автоматически получает значение **Обязательное**. Это поведение не может быть изменено.  

- **Разрешить конечным пользователям пробовать восстановить это приложение**. Начиная с версии 1810, создав приложение с помощью командной строки восстановления, включите этот параметр. В центре программного обеспечения пользователям будет отображаться команда для **восстановления** приложения.<!--1357866-->  

- **Предварительно развертывать программное обеспечение на основном устройстве пользователя**. Если развертывание адресовано пользователю, выберите данный вариант, чтобы развернуть приложение на основном устройстве пользователя. В этом варианте пользователю не требуется входить в систему перед выполнением развертывания. Не устанавливайте этот параметр, если пользователь должен выполнять какие-либо действия во время установки. Этот вариант доступен только в том случае, если развертывание является **обязательным**.  

- **Отправлять wake-up пакеты**. Если развертывание является **обязательным**, то перед тем как клиент запустит развертывание, Configuration Manager отправит на компьютеры wake-up пакеты. Эти пакеты выводят компьютеры из спящего режима при наступлении крайнего срока установки. Для использования этого параметра необходимо включить поддержку пробуждения по локальной сети на компьютерах и в сетях. Дополнительные сведения см. в разделе [Планирование пробуждения клиентов](../../core/clients/deploy/plan/plan-wake-up-clients.md).  

- **Все клиенты должны использовать лимитное подключение к Интернету для скачивания содержимого после наступления крайнего срока установки. Это может повлечь дополнительные затраты**. Этот вариант доступен, только если указана цель развертывания **Обязательно**.  

- **Автоматически обновлять замененные версии этого приложения**. Клиент обновляет все замененные версии приложения до заменяющего приложения.

    > [!Note]  
    > Этот параметр действует вне зависимости от утверждения администратором. Если администратор уже утвердил замененную версию, ему не нужно также утверждать заменяющую версию. Утверждение требуется только для новых запросов, а не при замене обновлений.<!--515824-->  
    >
    > Можно включить или отключить параметр **Доступно** для установки. <!--1351266-->


#### <a name="approval-settings"></a><a name="bkmk_approval"></a> Параметры утверждения

Поведение одобрения приложения зависит от того, включена ли рекомендуемая дополнительная функция — **Утверждение запросов приложений для пользователей на каждом устройстве**.

- **Администратор должен утвердить запрос для этого приложения на устройстве**. Если вы включите дополнительную функцию, администратор должен утвердить все запросы пользователя для приложения, прежде чем пользователь может установить его на запрошенном устройстве. Если администратор одобряет запрос, пользователь может установить приложение только на этом устройстве. Пользователь должен отправить другой запрос, чтобы установить приложение на другом устройстве. Этот параметр недоступен при развертывании с целью **Обязательное** и в том случае, если приложение развертывается в коллекции устройств.

- **Запрос пользователем этого приложения должен утвердить администратор**. Если вы не включите дополнительную функцию, администратор должен утверждать все запросы пользователя для приложения, прежде чем пользователь сможет установить его. Этот параметр недоступен при развертывании с целью **Обязательное** и в том случае, если приложение развертывается в коллекции устройств.  

Дополнительные сведения см. в статье [Утверждение приложений](app-approval.md).


#### <a name="deployment-properties-deployment-settings"></a>**Параметры развертывания** в свойствах развертывания

При просмотре свойств развертывания следующий параметр имеется на вкладке **Параметры развертывания**, если он поддерживается технологией типа развертывания:

**Автоматически закрывать все запущенные исполняемые файлы, указанные на вкладке "Способ установки" диалогового окна "Свойства типа развертывания"** . Дополнительные сведения см. в статье о [проверке наличия запущенных исполняемых файлов перед установкой приложения](#bkmk_exe-check).



### <a name="deployment-scheduling-settings"></a><a name="bkmk_deploy-sched"></a> Параметры **планирования** для развертывания

На странице **Планирование** укажите время развертывания или доступности приложения для клиентских устройств.

По умолчанию Configuration Manager сразу делает политику развертывания доступной для клиентов. Если вы хотите создать развертывание, но пока не делать его доступным для клиентов, настройте параметр **Приложение доступно с**. Затем выберите дату и время, а также укажите часовой пояс: UTC или часовой пояс клиента.

Если развертывание является **обязательным**, также укажите **Крайний срок установки**. По умолчанию крайний срок имеет значение "Как можно скорее".

Например, нужно развернуть новое бизнес-приложение. Оно должно быть развернуто для всех пользователей к определенному времени, однако пользователям также необходимо предоставить возможность установки раньше срока. Кроме того, необходимо убедиться в том, что содержимое передано с сайта во все точки распространения. Вы настраиваете расписание, согласно которому приложение должно стать доступным через пять дней от сегодняшнего дня. Таким образом, у вас будет достаточно времени для распространения содержимого и проверки его состояния. Затем вы задаете крайний срок установки: один месяц от сегодняшнего дня. Пользователи увидят приложение в центре программного обеспечения, когда оно станет доступно, то есть через пять дней. Если они ничего не предпримут, клиент автоматически установит приложение, когда наступит крайний срок.

Если развертываемое приложение заменяет другое, настройте крайний срок для установки этого нового приложения. Установите параметр **Крайний срок установки**, чтобы обновить заменяемые приложения у пользователей.


#### <a name="delay-enforcement-with-a-grace-period"></a>Настройка периода отсрочки

Может потребоваться предоставить пользователям *больше времени* на установку обязательных приложений (по сравнению с заданными крайними сроками). Такое поведение обычно требуется, если компьютер был выключен в течение длительного времени и на него необходимо установить большое число приложений. Например, когда пользователь возвращается из отпуска, ему придется довольно долго ждать, пока клиент не установит просроченные развертывания. Чтобы решить эту проблему, можно определить период отсрочки применения.

- Сначала настройте период отсрочки с помощью свойства **Льготный период для принудительного применения после крайнего срока развертывания (ч)** в параметрах клиента. Дополнительные сведения см. в группе [Агент компьютера](../../core/clients/deploy/about-client-settings.md#computer-agent). Укажите значение в диапазоне от **1** до **120** часов.  

- На странице **Планирование** для обязательного развертывания приложения включите параметр **Отложить применение этого развертывания в соответствии с пользовательскими предпочтениями вплоть до окончания льготного периода, определенного в настройках клиента**. Льготный период применения действует для всех развертываний, для которых установлен этот параметр и которые предназначены для устройств с развернутым параметром клиента.

По достижении крайнего срока клиент устанавливает приложение в первом нерабочем периоде, настроенном пользователем, в течение периода отсрочки. Тем не менее пользователь может открыть Центр программного обеспечения и установить приложение в любой момент. По истечении льготного периода режим принудительного применения возвращается к нормальному поведению для просроченных развертываний.

![Схема временной шкалы периода отсрочки](media/grace-period.svg)

<!-- SCCMDocs issue #1599 -->

> [!Note]  
> В большинстве случаев эта функция решает проблему, если устройство отключено, а пользователь находится за пределами офиса. С технической точки зрения, период отсрочки начинается, когда клиент получает политику после наступления крайнего срока развертывания. Такое же поведение возникает, если вы останавливаете службу клиента Configuration Manager (CcmExec), а затем перезапускаете ее через некоторое время после наступления крайнего срока развертывания.

### <a name="deployment-user-experience-settings"></a><a name="bkmk_deploy-ux"></a> Параметры **взаимодействия с пользователем** для развертывания

На странице **Взаимодействие с пользователем** укажите сведения о действиях пользователей при установке приложения.

- **Уведомления для пользователей**. Укажите, нужно ли отображать уведомление в центре программного обеспечения в установленное доступное время. Этот параметр также определяет, следует ли уведомлять пользователей на клиентских компьютерах. Выбрать параметр **Скрыть в центре программного обеспечения и во всех уведомлениях** для доступных развертываний невозможно.  

    - **Если требуется изменить программное обеспечение, показывать диалоговое окно вместо всплывающего уведомления.**<!--3555947-->: Начиная с версии 1902 выбор этого параметра позволяет принудительно вызывать диалоговое окно для пользователей. Он применяется только к обязательным развертываниям. Подробные сведения см. в разделе о [замене всплывающего уведомления диалоговым окном](../plan-design/plan-for-software-center.md#bkmk_impact).

- **Установка программного обеспечения** и **Перезапуск системы**. Настройте эти параметры только для обязательных развертываний. Они определяют действия при достижении крайнего срока развертывания за пределами заданных периодов обслуживания. Дополнительные сведения о периодах обслуживания см. в разделе [Использование периодов обслуживания](../../core/clients/manage/collections/use-maintenance-windows.md).  

- **Обработка фильтра записи для устройств Windows Embedded**. Этот параметр управляет режимом установки на устройствах Windows Embedded, включенных с помощью фильтра записи. Выберите этот параметр, чтобы фиксировать изменения по наступлении крайнего срока установки или в течение периода обслуживания. При выборе этого параметра требуется перезагрузка, и изменения сохраняются на устройстве. В противном случае приложение устанавливается во временное наложение и фиксируется позднее.  

    - При развертывании обновления программного обеспечения на устройстве Windows Embedded убедитесь в том, что устройство входит в коллекцию, для которой настроен период обслуживания. Дополнительные сведения о периодах обслуживания и об устройствах Windows Embedded см. в разделе [Создание приложений Windows Embedded](../get-started/creating-windows-embedded-applications.md).  


### <a name="deployment-alerts"></a><a name="bkmk_deploy-alerts"></a>**Оповещения** для развертывания

На странице **Оповещения** укажите, каким образом Configuration Manager будет создавать оповещения для этого развертывания. Если также используется System Center Operations Manager, настройте оповещения и для него. Некоторые оповещения можно настроить только для обязательных развертываний. 


## <a name="create-a-phased-deployment"></a><a name="bkmk_phased"></a> Создание поэтапного развертывания

<!--1358147-->
Начиная с версии 1806 можно создать поэтапное развертывание для приложения. Поэтапные развертывания позволяют организовать согласованное, последовательное развертывание программного обеспечения на основе настраиваемых условий и групп. Например, можно развернуть приложение в пилотной коллекции, а затем автоматически продолжить выпуск в соответствии с условиями успеха.

Дополнительные сведения см. в следующих статьях:  

- [Создание поэтапного развертывания](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  

- [Мониторинг поэтапных развертываний и управление ими](../../osd/deploy-use/manage-monitor-phased-deployments.md?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  



## <a name="delete-a-deployment"></a><a name="bkmk_delete"></a> Удаление развертывания

1. В консоли Configuration Manager перейдите в рабочую область **Библиотека программного обеспечения**, разверните узел **Управление приложениями** и выберите узел **Приложения** или **Группы приложений**.  

2. Выберите приложение или группу приложений, развертывание которых требуется удалить.  

3. В области сведений на вкладке **Развертывания** выберите развертывание.  

4. На ленте на вкладке **Развертывание** в группе **Развертывание** нажмите кнопку **Удалить**.  

При удалении развертывания приложения его экземпляры, уже установленные клиентами, не удаляются. Чтобы удалить эти приложения, разверните приложение на компьютерах с действием **Удаление**. После удаления развертывания приложения или ресурса из коллекции, в которой выполняется развертывание, приложение больше не будет отображаться в центре программного обеспечения.



## <a name="user-notifications-for-required-deployments"></a><a name="bkmk_notify"></a> Уведомления для пользователей об обязательных развертываниях

Когда пользователь получает необходимое программное обеспечение и выбирает параметр **Отложить и напомнить снова через**, он может выбрать один из следующих вариантов:  

- **Позднее**. Указывает, что вывод уведомлений запланирован на основе параметров уведомлений клиента.  

- **Фиксированное время**. Указывает, что по истечении установленного времени уведомление будет запланировано для повторного отображения. Например, если вы выбрали 30 минут, уведомление от отобразится повторно через 30 минут.  

![Группа агента компьютера в параметрах клиента по умолчанию](media/ComputerAgentSettings.png)

Максимальное значение времени переноса всегда зависит от параметров уведомлений, настраиваемых в параметрах клиента на временной шкале развертывания. Пример.  

- Укажите значение 10 часов для параметра **Крайний срок развертывания превышает 24 часа, напоминать пользователям каждые ... (ч)** на странице **Агент компьютера**.  

- Клиент отображает диалоговое окно с уведомлением ранее чем за 24 часа до крайнего срока развертывания.  

- Время переноса в диалоговом окне растет, но никогда не превысит 10 часов.  

- По мере приближения крайнего срока развертывания количество параметров в диалоговом окне уменьшается. Эти параметры соответствуют параметрам агента клиента для каждого компонента временной шкалы развертывания.  

Для развертываний с высоким уровнем риска, таких как последовательность задач для развертывания операционной системы, уведомление конечных пользователей осуществляется более активно. Вместо временных уведомлений на панели задач отображается следующее диалоговое окно, информирующее пользователя о необходимости обслуживания критического программного обеспечения:

![Диалоговое окно "Необходимое программное обеспечение", уведомляющее пользователя о необходимости обслуживания критического программного обеспечения](media/client-toast-notification.png)



## <a name="check-for-running-executable-files"></a><a name="bkmk_exe-check"></a> Проверка на наличие запущенных исполняемых файлов

Вы можете настроить развертывание так, чтобы выполнялась проверка запуска определенных исполняемых файлов в клиенте. Таким образом можно проверять наличие процессов, которые могут нарушить установку приложения. Если запущен один из этих исполняемых файлов, установка для этого типа развертывания будет заблокирована. Для того чтобы клиент продолжил установку для этого типа развертывания, пользователь должен закрыть запущенный исполняемый файл. Для развертываний с целью "Обязательное" клиент может автоматически закрыть запущенный исполняемый файл.

1. Откройте диалоговое окно **Свойства** для типа развертывания.  

2. Перейдите на вкладку **Способ установки** и нажмите кнопку **Добавить**.  

3. В диалоговом окне **Добавление исполняемого файла** введите имя целевого исполняемого файла. Можно также ввести необязательное понятное имя приложения, которое поможет идентифицировать его в списке.  

4. Нажмите кнопку **ОК**, а затем еще раз нажмите кнопку **ОК**, чтобы закрыть окно свойств типа развертывания.  

5. При развертывании приложения выберите параметр **Автоматически закрывать все запущенные исполняемые файлы, указанные на вкладке "Способ установки" диалогового окна "Свойства типа развертывания"** . Он находится на вкладке **Параметры развертывания** в свойствах развертывания.  

> [!Note]
> Если приложение настроено на проверку запуска исполняемых файлов и включено в шаг последовательности задач [Установка приложения](../../osd/understand/task-sequence-steps.md#BKMK_InstallApplication), то последовательность задач не сможет установить его. Если не настроить этот шаг последовательности задач таким образом, чтобы выполнение продолжилось в случае ошибки, вся последовательность задач завершится ошибкой.

### <a name="client-behaviors-and-user-notifications"></a>Поведение клиентов и уведомления для пользователей

После того как клиенты получают развертывание, применяется следующее поведение:  

- Если приложение развернуто как **доступное** и пользователь пытается установить его, ему будет предложено закрыть все запущенные исполняемые файлы, включенные в этот список, перед продолжением установки.  

- Если приложение развернуто как **обязательное** и задан параметр **Автоматически закрывать все запущенные исполняемые файлы, указанные на вкладке "Способ установки" диалогового окна "Свойства типа развертывания"** , клиент выводит уведомление. Оно сообщает пользователю о том, что указанные исполняемые файлы будут автоматически закрыты по достижении крайнего срока установки приложения.  

    - Отображение этих диалоговых окон можно запланировать в группе **Агент компьютера** параметров клиента. Дополнительные сведения см. в статье [Агент компьютера](../../core/clients/deploy/about-client-settings.md#computer-agent).  

    - Если пользователь не должен видеть эти сообщения, выберите параметр **Скрыть в центре программного обеспечения и во всех уведомлениях** на вкладке **Взаимодействие с пользователем** в окне свойств развертывания. Дополнительные сведения см. в разделе [Параметры взаимодействия с пользователем для развертывания](#bkmk_deploy-ux).  

- Если приложение развернуто как **Обязательное** без параметра **Автоматически закрывать все запущенные исполняемые файлы, указанные на вкладке "Способ установки" диалогового окна "Свойства типа развертывания"** , установка приложения завершится с ошибкой, если запущено одно или несколько указанных приложений.  



## <a name="deploy-user-available-applications-on-azure-ad-joined-devices"></a>Развертывание приложений, доступных для пользователя, на устройствах, присоединенных к Azure AD

<!-- 1322613 -->
Приложения, развертываемые в качестве доступных для пользователей, можно просматривать и устанавливать через центр программного обеспечения на устройствах Azure Active Directory (Azure AD).  

### <a name="prerequisites"></a>Предварительные условия

- Включите HTTPS в точке управления  

- Интегрируйте сайт с [Azure AD](../../core/servers/deploy/configure/azure-services-wizard.md) для службы **Управление облачными клиентами**  

    - Настройте [Azure AD User Discovery](../../core/servers/deploy/configure/configure-discovery-methods.md#azureaadisc)  

- Разверните приложение как доступное для коллекции пользователей Azure AD  

- Распределите любое содержимое приложения в [облачную точку распространения](../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md)  

- В группе [Агент компьютера](../../core/clients/deploy/about-client-settings.md#computer-agent) включите параметр клиента **Используйте новый Центр программного обеспечения**.  

- В качестве ОС клиента должна использоваться Windows 10, и клиент должен быть присоединен к Azure AD. Допускается облачное присоединение к домену либо гибридное присоединение к Azure AD.  

- Для поддержки интернет-клиентов:  

    - [Шлюз управления облаком](../../core/clients/manage/cmg/plan-cloud-management-gateway.md)  

    - Включение параметра клиента: **Включить запросы политик пользователей с интернет-клиентов** в группе [Политика клиента](../../core/clients/deploy/about-client-settings.md#client-policy)  

- Для поддержки клиентов в интрасети:  

    - Добавьте точку распределения облака в группу границы, используемую клиентами  

    - Клиенты должны разрешать полное доменное имя точки управления, поддерживающей протокол HTTPS.  



## <a name="next-steps"></a>Дальнейшие шаги

- [Мониторинг приложений](monitor-applications-from-the-console.md)
- [Устранение неполадок, связанных с развертываниями приложений](troubleshoot-application-deployment.md)
- [Другие задачи управления для приложений](management-tasks-applications.md)
- [Руководство пользователя центра программного обеспечения](../../core/understand/software-center.md)
