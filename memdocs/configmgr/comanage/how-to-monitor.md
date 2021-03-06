---
title: Мониторинг совместного управления
titleSuffix: Configuration Manager
description: Просмотрите сведения о совместно управляемых устройствах с помощью панели мониторинга совместного управления.
ms.date: 05/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: e83a7b0d-b381-4b4a-8eca-850385abbebb
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e4516ca9baa7398322c204908c25248921a69d25
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268068"
---
# <a name="how-to-monitor-co-management-in-configuration-manager"></a>Сведения о мониторинге совместного управления в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Включив совместное управление, наблюдайте за совместно управляемыми устройствами с помощью следующих методов.

- [Панель мониторинга совместного управления](#co-management-dashboard)  

- [Политики развертывания](#deployment-policies)

- [Данные WMI об устройствах](#wmi-device-data)

## <a name="co-management-dashboard"></a>Панель мониторинга совместного управления

Начиная с версии 1802 вы можете просматривать сведения о совместном управлении на панели мониторинга. На этой панели можно узнать, какие компьютеры в вашей среде работают в режиме совместного управления. С помощью диаграмм можно определять устройства, требующие внимания.<!--1356648-->

В консоли Configuration Manager перейдите в рабочую область **Мониторинг** и выберите узел **Совместное управление**.

С версии 1810 в панель мониторинга совместного управления добавлены более подробные сведения. <!--1358980-->

![Снимок экрана с панелью мониторинга совместного управления](media/co-management-dashboard.png)

### <a name="co-managed-devices"></a>Совместно управляемые устройства

*Применимо к версии 1802 и 1806*

Показаны сведения о доле совместно управляемых устройств в вашей среде.

![Плитка "Совместно управляемые устройства"](media/co-management-dashboard/Percent-Co-managed-graph.PNG)

### <a name="client-os-distribution"></a>Распределение клиентских ОС

*Применяется ко всем версиям* 

Показано число клиентских устройств с каждой версией операционной системы. Здесь используются следующие группирования:  

- Windows 7 и 8.x
- Windows 10 версии ниже 1709  
- Windows 10 версии 1709 и выше  

    > [!Tip]  
    > Windows 10, версия 1709 и выше — необходимое условие для совместного управления.  

При наведении указателя мыши на раздел диаграммы выводится доля устройств в выбранной группе ОС.

![Плитка "Распределение клиентских ОС"](media/co-management-dashboard/Co-management-OS-distribution-graph.PNG)

### <a name="co-management-status-donut"></a>Состояние совместного управления

*Применимо к версии 1802 и 1806*

Показано группирование устройств по успешному и неуспешному выполнению в следующих категориях:

- Успех, гибридное присоединение к Azure AD
- Успех, присоединение к Azure AD  
- Сбой: Сбой автоматической регистрации  

При наведении указателя мыши на раздел диаграммы выводится доля устройств в выбранной категории.

![Плитка "Состояние совместного управления" (круговая диаграмма)](media/co-management-dashboard/Co-management-status-graph.PNG)

Выберите раздел диаграммы, чтобы просмотреть список устройств для этой категории.

![Список устройств с ошибкой регистрации](media/co-management-dashboard/Enrollment-Failure_Device-List.PNG)

### <a name="co-management-status-funnel"></a>Состояние совместного управления (воронка)

*Применимо к версии 1810 и более поздним*

Воронкообразная диаграмма, показывающая количество устройств со следующими состояниями в процессе регистрации:
  
- Соответствующие устройства
- Запланировано  
- Регистрация инициирована  
- Зарегистрировано  

![Плитка "Состояние совместного управления" (воронка)](media/co-management-dashboard/1358980-status-funnel.png)

### <a name="co-management-enrollment-status"></a>Состояние регистрации совместного управления

*Применимо к версии 1810 и более поздним*

Показано группирование устройств по состоянию в следующих категориях:

- Успешно, присоединено к Azure AD в гибридном режиме  
- Успешно, присоединено к Azure AD  
- Регистрация, присоединено к Azure AD в гибридном режиме  
- Сбой, присоединено к Azure AD в гибридном режиме  
- Сбой, присоединено к Azure AD  
- Ожидание входа пользователя  

    > [!Note]  
    > Начиная с версии 1906, для уменьшения количества устройств в этом состоянии ожидания новое устройство с совместным управлением теперь автоматически регистрируется в службе Microsoft Intune на основе его маркера *устройства* Azure AD. Ему не нужно ждать входа пользователя на устройство для начала автоматической регистрации. Для поддержки этого поведения устройства должны работать под управлением Windows 10 версии 1803 или более поздней.
    >
    > В случае сбоя с токеном устройство возвращается к предыдущему режиму с токеном пользователя. См. в файле **ComanagementHandler.log** следующую запись: `Enrolling device with RegisterDeviceWithManagementUsingAADDeviceCredentials`

Выберите состояние на плитке для вывода списка устройств в этом состоянии.  

![Плитка "Состояние регистрации совместного управления"](media/co-management-dashboard/1358980-enrollment-status.png)


### <a name="workload-transition"></a>Переход рабочей нагрузки

*Применяется ко всем версиям*

Гистограмма, показывающая количество устройств, которые вы перевели в Microsoft Intune для четырех доступных рабочих нагрузок.

Список рабочих нагрузок зависит от версии Configuration Manager. Дополнительные сведения см. в статье [Переключение рабочих нагрузок Configuration Manager на Intune](workloads.md).

При наведении указателя мыши на раздел диаграммы будет выведено количество устройств, перенесенных для рабочей нагрузки. 

![Гистограмма "Переход рабочей нагрузки"](media/co-management-dashboard/Workload-Transition.PNG)


### <a name="enrollment-errors"></a>Ошибки при регистрации

*Применимо к версии 1810 и более поздним*

В этой таблице приведен список ошибок регистрации, которые могут возникнуть на устройствах. Эти ошибки могут поступать от компонента MDM в Windows, ядра ОС Windows или клиента Configuration Manager.

Число возможных ошибок измеряется сотнями. В следующей таблице перечислены лишь самые распространенные из них.
<!-- SCCMDocs issue 1064, BUG 3158555 -->

| Ошибка | Описание: |
|---------|---------|
| 2147549183 (0x8000FFFF) | Регистрация в MDM не настроена в Azure AD или получен недопустимый URL-адрес регистрации.<br><br>[Включение автоматической регистрации Windows 10](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment). |
| 2149056536 (0x80180018)<br>MENROLL_E_USERLICENSE | Блокировка регистрации из-за недопустимого состояния лицензии пользователя.<br><br>[Назначение лицензий пользователям](https://docs.microsoft.com/intune/licenses-assign). |
| 2149056555 (0x8018002B)<br>MENROLL_E_MDM_NOT_CONFIGURED | При попытке автоматической регистрации в Intune конфигурация Azure AD не полностью применена. Такая проблема обычно бывает временной, так как устройство повторяет попытку через некоторое время. |
| 2149056554 (0x‭8018002A‬)<br>&nbsp; | Пользователь отменил операцию.<br><br>Если регистрация MDM требует многофакторной проверки подлинности, но пользователь не применяет для входа поддерживаемый второй фактор, Windows отображает всплывающее уведомление с предложением регистрации. Если пользователь не отвечает на это уведомление, возникает такая ошибка. Эта проблема обычно бывает временной, так как Configuration Manager повторно отправит запрос пользователю. Пользователям следует применять многофакторную проверку подлинности при входе в Windows. Объясните им этот процесс и необходимые действия при появлении запроса. | 
| 2149056533 (0x80180015)<br>MENROLL_E_NOTSUPPORTED | Управление мобильными устройствами обычно не поддерживается. | 
| 2149056514 (0x80180002)<br>MENROLL_E_DEVICE_AUTHENTICATION_ERROR | Серверу не удалось проверить подлинность пользователя.<br><br> Для пользователя отсутствует маркер безопасности Azure AD. Убедитесь, что пользователь может пройти проверку подлинности в Azure AD. |
| 2147942450 (0x‭80070032‬)<br>&nbsp; | Автоматическая регистрация в MDM поддерживается только для Windows RS3 и более поздних версий.<br><br>Убедитесь, что устройство соответствует [минимальным требованиям](overview.md#windows-10) для совместного управления. |
| 3400073293 | Неизвестный ответ учетной записи для области пользователя ADAL<br><br>Проверьте конфигурацию Azure AD и убедитесь, что пользователи могут успешно выполнять проверку подлинности. | 
| 3399548929 | Требуется вход пользователя.<br><br>Эта проблема обычно бывает временной. Она происходит в тех случаях, когда пользователь быстро выходит из системы до выполнения задачи регистрации. | 
| 3400073236 | Не удалось запросить маркер безопасности ADAL.<br><br>Проверьте конфигурацию Azure AD и убедитесь, что пользователи могут успешно выполнять проверку подлинности. |
| 2149122477 | Общая проблема HTTP |
| 3400073247 | Проверка подлинности Windows с интеграцией ADAL поддерживается только в федеративном потоке.<br><br>[Планирование реализации гибридного подключения к Azure Active Directory](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan). | 
| 3399942148 | Не найден сервер или прокси-сервер.<br><br>Эта проблема обычно бывает временной и возникает только в период проблем связи клиента с облаком. Если ситуация не меняется, проверьте стабильность подключения клиента к Azure. | 
| 2149056532 | Определенная платформа или версия не поддерживается.<br><br>Убедитесь, что устройство соответствует [минимальным требованиям](overview.md#windows-10) для совместного управления. |
| 2147943568 | Элемент не найден.<br><br>Эта проблема обычно бывает временной. Если ситуация не меняется, обратитесь в службу поддержки Майкрософт. |
| 2192179208 | Недостаточно ресурсов памяти для обработки этой команды.<br><br>Такая проблема должна быть временной и устраняться без дополнительных действий при повторной попытке клиента. |
| 3399614467 | Не удалось назначить авторизацию ADAL для этого утверждения.<br><br>Проверьте конфигурацию Azure AD и убедитесь, что пользователи могут успешно выполнять проверку подлинности. |
| 2149056517 | Общая ошибка с сервера управления, например ошибка доступа к базе данных.<br><br>Эта проблема обычно бывает временной. Если ситуация не меняется, обратитесь в службу поддержки Майкрософт. |
| 2149134055 | Имя Winhttp не разрешено.<br><br>Клиент не может разрешить имя службы. Поверьте конфигурацию DNS. | 
| 2149134050 | Превышено время ожидания для Интернета.<br><br>Эта проблема обычно бывает временной и возникает только в период проблем связи клиента с облаком. Если ситуация не меняется, проверьте стабильность подключения клиента к Azure. |

Дополнительные сведения см. в разделе [об ошибках регистрации MDM](https://docs.microsoft.com/windows/desktop/mdmreg/mdm-registration-constants).

## <a name="deployment-policies"></a>Политики развертывания

Две политики созданы в узле **Развертывания** рабочей области **Мониторинг**. Одна политика для пилотной группы, а другая — для рабочей среды. Эти политики сообщают только число устройств, где Configuration Manager применил данную политику. Они не учитывают число устройств, зарегистрированных в Intune, что является требованием для совместного управления устройствами.  

Рабочая политика (CoMgmtSettingsProd) нацелена на коллекцию **Все системы**. У нее есть условие применимости, которое проверяет тип и версию ОС. Если клиентом является серверная ОС или не Windows 10, политика не применяется и никакие действия не предпринимаются.

## <a name="wmi-device-data"></a>Данные WMI об устройствах

Запросите класс WMI **SMS_Client_ComanagementState** в пространстве имен **ROOT\SMS\site_&lt;SITECODE>** на сервере сайта. Вы можете создать в Configuration Manager настраиваемые коллекции, чтобы определить состояние развертывания для совместного управления. Дополнительные сведения о создании настраиваемых коллекций см. в статье [Создание коллекций](../core/clients/manage/collections/create-collections.md).

В классе WMI доступны следующие поля:  

- **MachineId**. Уникальный идентификатор устройства для клиента Configuration Manager.  

- **MDMEnrolled**. Указывает, зарегистрировано ли устройство в системе MDM.  

- **Authority**. Центр, в котором регистрируется устройство.  

- **ComgmtPolicyPresent**. Определяет, существует ли политика совместного управления Configuration Manager на клиенте. Если значение **MDMEnrolled** равно **0**, устройство не управляется совместно, независимо от наличия политики совместного управления на клиенте.  

Устройство управляется совместно, когда поля **MDMEnrolled** и **ComgmtPolicyPresent** равны **1**.  
