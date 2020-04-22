---
title: Сообщения о состоянии
titleSuffix: Configuration Manager
description: В этой статье описаны сообщения о состоянии в поддерживаемых версиях Configuration Manager.
ms.date: 03/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f04c0a71-57bc-4443-a47c-592373050d04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fe173e37d888dfe594ad8953ff5d7167d43a2981
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704592"
---
# <a name="state-messages-in-configuration-manager"></a>Сообщения о состоянии в Configuration Manager 

*Область применения: Configuration Manager (Current Branch)*

Сообщения о состоянии содержат краткую информацию о состоянии клиента Configuration Manager. Систему отправки сообщений о состоянии используют отдельные компоненты Configuration Manager, например программные обновления и параметры конфигурации.

Клиенты Configuration Manager отправляют сообщения о состоянии в резервную точку состояния или в системы сайта точек управления, чтобы сообщить о текущем состоянии операций. Вы можете создавать отчеты, чтобы просматривать сообщения о состоянии, отправленные клиентами Configuration Manager.

Каждый компонент Configuration Manager, который использует сообщения о состоянии, определяется по типу темы сообщения о состоянии. С помощью описанных в этой статье типов тем сообщений о состоянии можно определить компонент Configuration Manager, к которому относится конкретное сообщение о состоянии.

> [!NOTE]  
> Идентификатор сообщения о состоянии с нулевым значением (0) обычно означает, что состояние типа темы неизвестно.

## <a name="300-state_topictype_sum_assignment_compliance"></a>300 STATE_TOPICTYPE_SUM_ASSIGNMENT_COMPLIANCE

|      Идентификатор сообщения о состоянии     |  Описание сообщения о состоянии |
|:-------------|:------|
| 0 | Неизвестное состояние соответствия|
| 1 | соответствующие требованиям | 
| 2 | Не соответствует | 

## <a name="301-state_topictype_sum_assignment_enforcement"></a>301 STATE_TOPICTYPE_SUM_ASSIGNMENT_ENFORCEMENT

|       Идентификатор сообщения о состоянии     |  Описание сообщения о состоянии |
|:-------------|:------|
| 0  | Неизвестное состояние принудительного применения |
| 1  | Установка обновлений        | 
| 2  | Ожидание перезагрузки          | 
| 3  | Ожидание завершения другого процесса установки         | 
| 4  | Установка обновлений успешно завершена          | 
| 5  | Ожидание перезагрузки системы         | 
| 6  | Не удалось установить обновления         | 
| 7  | Скачивание обновлений   | 
| 8  | Скачанные обновления    | 
| 9  | Не удалось скачать обновления     | 
| 10 | Ожидание периода обслуживания перед установкой         | 
| 11 | Ожидание оркестрации         | 

## <a name="302-state_topictype_sum_assignment_evaluation"></a>302 STATE_TOPICTYPE_SUM_ASSIGNMENT_EVALUATION

|     Идентификатор сообщения о состоянии     |  Описание сообщения о состоянии |
|:-------------|:------|      
| 0 | Неизвестное состояние оценки|                 
| 1 |Оценка активирована      |
| 2 |Оценка успешно завершена      |
| 3 |Не удалось оценить      |


## <a name="400-state_topictype_sum_ci_detection"></a>400 STATE_TOPICTYPE_SUM_CI_DETECTION

|     Идентификатор сообщения о состоянии     |  Описание сообщения о состоянии |
|:-------------|:------|
| 0 | Неизвестное состояние обнаружения|
| 1 | Не требуется   |
| 2 | Не обнаружено    |
| 3 | Обнаружено   |

## <a name="401-state_topictype_sum_ci_compliance"></a>401 STATE_TOPICTYPE_SUM_CI_COMPLIANCE

|     Идентификатор сообщения о состоянии     |  Описание сообщения о состоянии |
|:-------------|:------|
| 0 | Неизвестное состояние соответствия|
| 1 |соответствующие требованиям     |
| 2 |Не соответствует     |
| 3 |Обнаружен конфликт    |
| 4 |Ошибка      |
| 5 |Неизвестно     |
| 6 |Частичное соответствие   |
| 7 |Соответствие не настроено    |

## <a name="402-state_topictype_sum_ci_enforcement"></a>402 STATE_TOPICTYPE_SUM_CI_ENFORCEMENT

|     Идентификатор сообщения о состоянии     |  Описание сообщения о состоянии |
|:-------------|:------|
| 0  | Неизвестное состояние принудительного применения|
| 1  |Принудительное применение запущено          |
| 2  |Принудительное применение ожидает поступления содержимого         |
| 3  | Ожидание завершения другого процесса установки        |
| 4  |Ожидание периода обслуживания перед установкой         |
| 5  |Перед установкой требуется перезагрузка         |
| 6  |Общий сбой        |
| 7  |Ожидание установки         |
| 8  |Установка обновления          |
| 9  |Ожидание перезагрузки системы        |
| 10 |Установка обновления успешно завершена         |
| 11 |Не удалось установить обновление        |
| 12 |Скачивание обновления        |
| 13 | Скачанное обновление        |
| 14 |Не удалось скачать обновление        |

## <a name="500-state_topictype_sum_update_detection"></a>500 STATE_TOPICTYPE_SUM_UPDATE_DETECTION

|     Идентификатор сообщения о состоянии     |  Описание сообщения о состоянии |
|:-------------|:------|
|0 |Неизвестное состояние обнаружения|
| 1 | Обновление не требуется  |
| 2 | Требуется обновление   |
| 3 | Обновление установлено  |

## <a name="501-state_topictype_sum_update_source_scan"></a>501 STATE_TOPICTYPE_SUM_UPDATE_SOURCE_SCAN

|     Идентификатор сообщения о состоянии     |  Описание сообщения о состоянии |
|:-------------|:------|
| 0 |Неизвестное состояние проверки|
| 1 | Проверка ожидает поступления содержимого   |
| 2 | Проверка запущена    |
| 3 | Проверка завершена    |
| 4 | Проверка ожидает выполнения повторной попытки   |
| 5 | Не удалось выполнить проверку   |
| 6 | Проверка завершена с ошибками |

## <a name="700-state_topictype_resync_state_msg"></a>700 STATE_TOPICTYPE_RESYNC_STATE_MSG

Идентификаторы состояния отсутствуют.

## <a name="701-state_topictype_system_heartbeat"></a>701 STATE_TOPICTYPE_SYSTEM_HEARTBEAT

Идентификаторы состояния отсутствуют.

## <a name="702-state_topictype_ckd_update"></a>702 STATE_TOPICTYPE_CKD_UPDATE
 
Идентификаторы состояния отсутствуют.

## <a name="800-state_topictype_client_deployment"></a>800 STATE_TOPICTYPE_CLIENT_DEPLOYMENT

|     Идентификатор сообщения о состоянии     |  Описание сообщения о состоянии |
|:-------------|:------|
| 100 |Начато развертывание клиента      |       
| 101 |Ожидание скачивания       |       
| 102 |Развертывание запланировано       |       
| 103 | Ожидание окна перед развертыванием |
| 104 |Развертывание пропущено       |       
| 301 |Неизвестная ошибка при развертывании клиента |       
| 302 |Не удалось создать службу Ccmsetup  |       
| 303 |Не удалось удалить службу Ccmsetup |       
| 304 |Не удалось установить во встроенную операционную систему с файловым фильтром записи (FBWF), включенным на системном диске |       
| 305 |Основной режим безопасности недействителен в Windows 2000  |       
| 306 |Не удалось запустить процесс скачивания Ccmsetup  |       
| 307 |Недопустимая командная строка Ccmsetup |       
| 308 |Не удалось скачать файл через WINHTTP по адресу |       
| 309 |Не удалось скачать файлы через BITS по адресу |       
| 310 |Не удалось установить версию BITS |       
| 311 |Не удалось проверить, подписан ли корпорацией Майкрософт файл необходимых компонентов  |       
| 312 |Не удалось скопировать файл, так как диск заполнен |       
| 313 |Сбой установки Client.msi с ошибкой MSI |       
| 314 |Не удалось загрузить файл манифеста ccmsetup.xml |       
| 315 |Не удалось получить сертификат клиента  |       
| 316 |Файл необходимых компонентов не подписан корпорацией Майкрософт |       
| 317 |Для продолжения установки требуется перезагрузка  |       
| 318 |Не удалось установить клиент в точке управления, так как версии точки управления и клиента не совпадают |       
| 319 |Операционная система или пакет обновлений не поддерживаются  |       
| 320 |Развертывание не поддерживается       |       
| 321 |Отсутствуют биты        |       
| 322 |Исходная папка недоступна       |       
| 323 |AppV не поддерживается              |       
| 324 |Неправильная версия сайта              |       
| 325 |Несоответствие хэша необходимых компонентов       |       
| 326 |Не удалось отменить регистрацию MDM      |       
| 327 |Обнаружена регистрация MDM      |       
| 328 |Обнаружено решение Intune       |       
| 329 |Сеть с лимитным тарифным планом запрещена      |       
| 400 |Развертывание клиента успешно завершено |  
| 401 |Развертывание выполнено успешно, требуется перезагрузка     |       
| 402 |Развертывание выполнено успешно, перезагрузка выполнена успешно     |
| 500 |Начато назначение клиента|
| 601 |Неизвестный сбой при назначении клиента|
| 602 |Следующий код сайта является недопустимым|
| 603 |Не удалось назначить точку управления|
| 604 |Не удалось обнаружить точку управления по умолчанию|
| 605 |Не удалось скачать сертификат для подписи сайта|
| 606 |Не удалось автоматически обнаружить код сайта|
| 607 |Не удалось назначить сайт, версия клиента выше версии сайта|
| 608 |Не удалось получить версию сайта из доменных служб Active Directory и SLP|
| 609 |Не удалось получить версию клиента|
| 700 |Клиент успешно назначен|

## <a name="801-state_topictype_device_client_deployment"></a>801 STATE_TOPICTYPE_DEVICE_CLIENT_DEPLOYMENT

Идентификаторы состояния отсутствуют.

## <a name="810-state_topictype_client_comanagement"></a>810 STATE_TOPICTYPE_CLIENT_COMANAGEMENT

|     Идентификатор сообщения о состоянии     |  Описание сообщения о состоянии |
|:-------------|:------|
| 100 | Состояние регистрации   |
| 101 | Регистрация запланирована   |
| 102 | Регистрация отменена   |
| 105 | Регистрация начата   |
| 106 | Регистрация выполнена успешно, но не подготовлена
| 107 | Регистрация выполнена успешно и подготовлена
| 108 | Нет активного пользователя при регистрации   |
| 110 | Сбой регистрации   |


## <a name="820--state_topictype_client_wufb"></a>820 STATE_TOPICTYPE_CLIENT_WUFB

|     Идентификатор сообщения о состоянии     |  Описание сообщения о состоянии |
|:-------------|:------|
| 1 | Состояние клиента Центра обновления Windows для бизнеса| 

## <a name="900-state_topictype_branch_dp"></a>900 STATE_TOPICTYPE_BRANCH_DP

|     Идентификатор сообщения о состоянии     |  Описание сообщения о состоянии |
|:-------------|:------|
| 1 | Место на диске   | 

## <a name="901-state_topictype_remote_dp_monitoring"></a>901 STATE_TOPICTYPE_REMOTE_DP_MONITORING

Идентификаторы состояния отсутствуют.

## <a name="902-state_topictype_pull_dp_monitoring"></a>902 STATE_TOPICTYPE_PULL_DP_MONITORING

Идентификаторы состояния отсутствуют.

## <a name="903-state_topictype_dp_usage"></a>903 STATE_TOPICTYPE_DP_USAGE

Идентификаторы состояния отсутствуют.

## <a name="1000--state_topictype_client_framework_comm"></a>1000 STATE_TOPICTYPE_CLIENT_FRAMEWORK_COMM

|     Идентификатор сообщения о состоянии     |  Описание сообщения о состоянии |
|:-------------|:------|
| 1 | Клиент успешно связался с точкой управления |
| 2 | Клиенту не удалось связаться с точкой управления |

## <a name="1001-state_topictype_client_framework_local"></a>1001 STATE_TOPICTYPE_CLIENT_FRAMEWORK_LOCAL

|     Идентификатор сообщения о состоянии     |  Описание сообщения о состоянии |
|:-------------|:------|
| 1 |Клиент успешно получил сертификат из локального хранилища сертификатов    |
| 2 |Клиенту не удалось получить сертификат из локального хранилища сертификатов |

## <a name="1002-state_topictype_device_client_framework_comm"></a>1002 STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_COMM

Идентификаторы состояния отсутствуют.

## <a name="1003-state_topictype_device_client_framework_local"></a>1003 STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_LOCAL

Идентификаторы состояния отсутствуют.

## <a name="1004-state_topictype_device_client_framework_certificate"></a>1004 STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_CERTIFICATE

Идентификаторы состояния отсутствуют.

## <a name="1005-state_topictype_device_client_wipe"></a>1005 STATE_TOPICTYPE_DEVICE_CLIENT_WIPE

Идентификаторы состояния отсутствуют.

## <a name="1006-state_topictype_device_client_retire"></a>1006 STATE_TOPICTYPE_DEVICE_CLIENT_RETIRE

Идентификаторы состояния отсутствуют.

## <a name="1007-state_topictype_device_client_wipe_intune"></a>1007 STATE_TOPICTYPE_DEVICE_CLIENT_WIPE_INTUNE

Идентификаторы состояния отсутствуют.

## <a name="1008-state_topictype_device_client_retire_intune"></a>1008 STATE_TOPICTYPE_DEVICE_CLIENT_RETIRE_INTUNE

Идентификаторы состояния отсутствуют.

## <a name="1009-state_topictype_device_client_devicelock"></a>1009 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICELOCK

Идентификаторы состояния отсутствуют.

## <a name="1010-state_topictype_device_client_devicelock_intune"></a>1010 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICELOCK_INTUNE

Идентификаторы состояния отсутствуют.

## <a name="1011-state_topictype_device_client_devicepinreset"></a>1011 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET

Идентификаторы состояния отсутствуют.

## <a name="1012-state_topictype_device_client_devicepinreset_intune"></a>1012 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET_INTUNE

Идентификаторы состояния отсутствуют.

## <a name="1013-state_topictype_device_client_devicepinreset_onprem"></a>1013 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET_ONPREM

Идентификаторы состояния отсутствуют.

## <a name="1014-state_topictype_device_client_devicealbypass"></a>1014 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEALBYPASS

Идентификаторы состояния отсутствуют.

## <a name="1015-state_topictype_device_client_devicealbypass_intune"></a>1015 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEALBYPASS_INTUNE

Идентификаторы состояния отсутствуют.

## <a name="1100-state_topictype_client_framework_modereadiness"></a>1100 STATE_TOPICTYPE_CLIENT_FRAMEWORK_MODEREADINESS

|     Идентификатор сообщения о состоянии     |  Описание сообщения о состоянии |
|:-------------|:------|
| 1 |Клиент не готов к работе в основном режиме  |
| 2 |Клиент готов к работе в основном режиме     |


## <a name="1300-state_topictype_client_health"></a>1300 STATE_TOPICTYPE_CLIENT_HEALTH

|     Идентификатор сообщения о состоянии     |  Описание сообщения о состоянии |
|:-------------|:------|
| 1 | Успех|
| 2 | Не выполнено |

## <a name="1401-state_topictype_state_report"></a>1401 STATE_TOPICTYPE_STATE_REPORT

Идентификаторы состояния отсутствуют.

## <a name="1500-state_topictype_cal_track_ut"></a>1500 STATE_TOPICTYPE_CAL_TRACK_UT

Идентификаторы состояния отсутствуют.

## <a name="1502-state_topictype_cal_track_mt"></a>1502 STATE_TOPICTYPE_CAL_TRACK_MT

Идентификаторы состояния отсутствуют.

## <a name="1503-state_topictype_cal_track_ml"></a>1503 STATE_TOPICTYPE_CAL_TRACK_ML

Идентификаторы состояния отсутствуют. 

## <a name="1600-state_topictype_user_affinity"></a>1600 STATE_TOPICTYPE_USER_AFFINITY

|     Идентификатор сообщения о состоянии     |  Описание сообщения о состоянии |
|:-------------|:------|
| 1 |Сопоставление пользователей задано       |
| 2 |Сопоставление пользователей удалено       |

## <a name="1700-state_topictype_app_ci_scan"></a>1700 STATE_TOPICTYPE_APP_CI_SCAN

Идентификаторы состояния отсутствуют.

## <a name="1701-state_topictype_app_ci_compliance"></a>1701 STATE_TOPICTYPE_APP_CI_COMPLIANCE

Идентификаторы состояния отсутствуют.

## <a name="1702-state_topictype_app_ci_enforcement"></a>1702 STATE_TOPICTYPE_APP_CI_ENFORCEMENT

|     Идентификатор сообщения о состоянии     |  Описание сообщения о состоянии |
|:-------------|:------|
| 1000  |Элемент конфигурации успешно используется           |
| 1001 |Успешно используемый элемент конфигурации уже установлен         |
| 1002 |Элемент конфигурации успешно подготовлен          |
| 1003 |Успешно выполнено быстрое получение сведений о состоянии элемента конфигурации          |
| 2000 |Элемент конфигурации выполняется           |
| 2001 |Элемент конфигурации в состоянии выполнения ожидает поступления содержимого         |
| 2002 |Элемент конфигурации в состоянии выполнения установки          |
| 2003 |Элемент конфигурации в состоянии выполнения ожидает перезагрузки         |
| 2004 |Элемент конфигурации в состоянии выполнения ожидает периода обслуживания        |
| 2005 |Элемент конфигурации в состоянии выполнения ожидает расписания         |
| 2006 |Элемент конфигурации в состоянии выполнения скачивает зависимое содержимое     |
| 2007 |Элемент конфигурации в состоянии выполнения устанавливает зависимости        |
| 2008 |Элемент конфигурации в состоянии выполнения ожидает перезагрузки         |
| 2009 |Содержимое элемента конфигурации в состоянии выполнения скачано         |
| 2010 |Элемент конфигурации в состоянии выполнения ожидает обновления         |
| 2011 |Элемент конфигурации в состоянии выполнения ожидает переподключения пользователя        |
| 2012 |Элемент конфигурации в состоянии выполнения ожидает выхода пользователя         |
| 2013 |Элемент конфигурации в состоянии выполнения ожидает входа пользователя         |
| 2014 |Элемент конфигурации в состоянии выполнения ожидает установки         |
| 2015 |Элемент конфигурации в состоянии выполнения ожидает повторной попытки         |
| 2016 |Элемент конфигурации в состоянии выполнения ожидает presmode         |
| 2017 |Элемент конфигурации в состоянии выполнения ожидает оркестрации        |
| 2018 |Элемент конфигурации в состоянии выполнения ожидает подключения к сети         |
| 2019 |Элемент конфигурации в состоянии выполнения ожидает обновления VE         |
| 2020 |Для элемента конфигурации в состоянии выполнения обновляется VE         |
| 3000 |Не выполнены требования элемента конфигурации           |
| 3001 |Не выполнены требования элемента конфигурации, узел неприменим        |
| 4000 |Неизвестный элемент конфигурации           |
| 5000 |Ошибка элемента конфигурации            |
| 5001 |Элемент конфигурации — ошибка при оценке элемента          |
| 5002 |Элемент конфигурации — ошибка при установке          |
| 5003 |Элемент конфигурации — ошибка при получении содержимого         |
| 5004 |Элемент конфигурации — ошибка при установке зависимости         |
| 5005 |Элемент конфигурации — ошибка при получении зависимости содержимого        |
| 5006 |Элемент конфигурации — ошибка, связанная с конфликтом правил          |
| 5007 |Элемент конфигурации — ошибка ожидания повторной попытки          |
| 5008 |Элемент конфигурации — ошибка удаления замены        |
| 5009 |Элемент конфигурации — ошибка скачивания замены         |
| 5010 |Элемент конфигурации — ошибка при обновлении VE          |
| 5011 |Элемент конфигурации — ошибка при установке лицензии         |
| 5012 |Элемент конфигурации — ошибка получения разрешения для всех доверенных приложений       |
| 5013 |Элемент конфигурации — ошибка, связанная с отсутствием доступных лицензий         |
| 5014 |Элемент конфигурации — ошибка, связанная с отсутствием поддержки ОС          |
| 6000 |Успешный запуск элемента конфигурации            |
| 6010 |Ошибка при запуске элемента конфигурации            |
| 6020 |Неизвестное состояние запуска элемента конфигурации|

## <a name="1703-state_topictype_app_ci_assignment_evaluatio"></a>1703 STATE_TOPICTYPE_APP_CI_ASSIGNMENT_EVALUATIO

Идентификаторы состояния отсутствуют.

## <a name="1704-state_topictype_app_ci_launch"></a>1704 STATE_TOPICTYPE_APP_CI_LAUNCH

Идентификаторы состояния отсутствуют.

## <a name="1800-state_topictype_event_intrinsic"></a>1800 STATE_TOPICTYPE_EVENT_INTRINSIC

Идентификаторы состояния отсутствуют.

## <a name="1801-state_topictype_event_extrinsic"></a>1801 STATE_TOPICTYPE_EVENT_EXTRINSIC

Идентификаторы состояния отсутствуют.

## <a name="1900-state_topictype_ep_am_infection"></a>1900 STATE_TOPICTYPE_EP_AM_INFECTION

Идентификаторы состояния отсутствуют.

## <a name="1901-state_topictype_ep_am_health"></a>1901 State_Topictype_Ep_Am_Health

Идентификаторы состояния отсутствуют.

## <a name="1902-state_topictype_ep_malware"></a>1902 STATE_TOPICTYPE_EP_MALWARE

Идентификаторы состояния отсутствуют.

## <a name="1950-state_topictype_atp_health_status"></a>1950 STATE_TOPICTYPE_ATP_HEALTH_STATUS

Идентификаторы состояния отсутствуют.

## <a name="2001-state_topictype_ep_client_deployment"></a>2001 STATE_TOPICTYPE_EP_CLIENT_DEPLOYMENT

|     Идентификатор сообщения о состоянии     |  Описание сообщения о состоянии |
|:-------------|:------|
| 1 |Endpoint Protection не управляется   |
| 2 |Endpoint Protection ожидает установки  |
| 3 |Endpoint Protection управляется   |
| 4 |Не удалось установить Endpoint Protection  |
| 5 |Endpoint Protection ожидает перезагрузки  |
| 6 |Endpoint Protection не поддерживается   |
| 7 |Endpoint Protection управляется совместно   |

## <a name="2002-state_topictype_ep_client_policyapplication"></a>2002 STATE_TOPICTYPE_EP_CLIENT_POLICYAPPLICATION

|     Идентификатор сообщения о состоянии     |  Описание сообщения о состоянии |
|:-------------|:------|
| 0 |Неизвестное состояние приложения политики Endpoint Protection    |
| 1 |Приложение политики Endpoint Protection успешно выполнено    |
| 2 |Не удалось выполнить приложение политики Endpoint Protection    |

## <a name="2003-state_topictype_client_action"></a>2003 STATE_TOPICTYPE_CLIENT_ACTION

|     Идентификатор сообщения о состоянии     |  Описание сообщения о состоянии |
|:-------------|:------|
| 0 |  Неизвестно    |
| 1 |  Активно    |
| 2 |  Неактивно    |

## <a name="2100-state_topictype_wp_client_deployment"></a>2100 STATE_TOPICTYPE_WP_CLIENT_DEPLOYMENT

|     Идентификатор сообщения о состоянии     |  Описание сообщения о состоянии |
|:-------------|:------|
| 1 | Не установлен прокси-сервер пробуждения    |
| 2 | Прокси-сервер пробуждения ожидает установки   |
| 3 | Прокси-сервер пробуждения установлен    |
| 4 | Не удалось установить прокси-сервер пробуждения   |
| 5 | Прокси-сервер пробуждения ожидает перезагрузки   |
| 6 | Прокси-сервер не поддерживается в этой ОС  |
| 7 | Отказ от прокси-сервера пробуждения   |
| 8 | Не удалось удалить прокси-сервер пробуждения   |
| 9 | Среда выполнения прокси-сервера пробуждения не поддерживается   |

## <a name="2200-state_topictype_fdm"></a>2200 STATE_TOPICTYPE_FDM

Идентификаторы состояния отсутствуют.

## <a name="2201-state_topictype_ccm_cert_binding"></a>2201 STATE_TOPICTYPE_CCM_CERT_BINDING

Идентификаторы состояния отсутствуют.

## <a name="2202-state_topictype_server_statistic"></a>2202 STATE_TOPICTYPE_SERVER_STATISTIC

Идентификаторы состояния отсутствуют.

## <a name="3000-state_topictype_dm_wns_channel"></a>3000 STATE_TOPICTYPE_DM_WNS_CHANNEL

|     Идентификатор сообщения о состоянии     |  Описание сообщения о состоянии |
|:-------------|:------|
|0 | Задан канал службы push-уведомлений Windows|

## <a name="4000-state_topictype_mdm_device_property"></a>4000 STATE_TOPICTYPE_MDM_DEVICE_PROPERTY

Идентификаторы состояния отсутствуют.

## <a name="4002-state_topictype_mdm_client_idenitity"></a>4002 STATE_TOPICTYPE_MDM_CLIENT_IDENITITY

Идентификаторы состояния отсутствуют.

## <a name="4003-state_topictype_mdm_application_request"></a>4003 STATE_TOPICTYPE_MDM_APPLICATION_REQUEST

Идентификаторы состояния отсутствуют.

## <a name="4004-state_topictype_mdm_application_state"></a>4004 STATE_TOPICTYPE_MDM_APPLICATION_STATE

Идентификаторы состояния отсутствуют.

## <a name="4005-state_topictype_mdm_license_device_relation"></a>4005 STATE_TOPICTYPE_MDM_LICENSE_DEVICE_RELATION

Идентификаторы состояния отсутствуют.

## <a name="4006-state_topictype_mdm_license_keys"></a>4006 STATE_TOPICTYPE_MDM_LICENSE_KEYS

Идентификаторы состояния отсутствуют.

## <a name="4007-state_topictype_mdm_policy_assignment"></a>4007 STATE_TOPICTYPE_MDM_POLICY_ASSIGNMENT

Идентификаторы состояния отсутствуют.

## <a name="4008-state_topictype_mdm_android_count"></a>4008 STATE_TOPICTYPE_MDM_ANDROID_COUNT

Идентификаторы состояния отсутствуют.

## <a name="4009-state_topictype_mdm_slk_status"></a>4009 STATE_TOPICTYPE_MDM_SLK_STATUS

Идентификаторы состояния отсутствуют.

## <a name="4010-state_topictype_mdm_user_company_term_acceptance"></a>4010 STATE_TOPICTYPE_MDM_USER_COMPANY_TERM_ACCEPTANCE

Идентификаторы состояния отсутствуют.

## <a name="4022-state_topictype_mdm_dep_syncnow_status"></a>4022 STATE_TOPICTYPE_MDM_DEP_SYNCNOW_STATUS

Идентификаторы состояния отсутствуют.

## <a name="4023-state_topictype_mdm_mam_store_app_sync"></a>4023 STATE_TOPICTYPE_MDM_MAM_STORE_APP_SYNC

Идентификаторы состояния отсутствуют.

## <a name="5000-state_topictype_certificate_enrollment"></a>5000 STATE_TOPICTYPE_CERTIFICATE_ENROLLMENT

|     Идентификатор сообщения о состоянии     |  Описание сообщения о состоянии |
|:-------------|:------|
| 1 |Запрос защиты выдан         |
| 2 |Не удалось выдать запрос защиты        |
| 3 |Не удалось создать запрос        |
| 4 |Не удалось отправить запрос        |
| 5 |Проверка запроса защиты выполнена       |
| 6 |Не удалось проверить запрос защиты       |
| 7 |Сбой выдачи         |
| 8 |Ожидание выдачи         |
| 9 |Выдано          |
| 10 |Не удалось обработать ответ       |
| 11 |Ожидание ответа         |
| 12 |Регистрация выполнена         |
| 13 |Регистрация не требуется         |
| 14 |Отозвано          |
| 15 |Удалено из коллекции        |
| 16 |Возобновление проверено         |
| 17 |Сбой установки        |
| 18 |Установлено         |
| 19 |Сбой удаления         |
| 20 |Удалено         |
| 21 |Запрошено продление        |


## <a name="5001-state_topictype_certificate_crp"></a>5001 STATE_TOPICTYPE_CERTIFICATE_CRP

|     Идентификатор сообщения о состоянии     |  Описание сообщения о состоянии |
|:-------------|:------|
| 1 |Запрос защиты выдан         |
| 2 |Не удалось выдать запрос защиты        |
| 3 |Не удалось создать запрос        |
| 4 |Не удалось отправить запрос        |
| 5 |Проверка запроса защиты выполнена       |
| 6 |Не удалось проверить запрос защиты       |
| 7 |Сбой выдачи         |
| 8 |Ожидание выдачи         |
| 9 |Выдано          |
| 10 |Не удалось обработать ответ       |
| 11 |Ожидание ответа         |
| 12 |Регистрация выполнена         |
| 13 |Регистрация не требуется         |
| 14 |Отозвано          |
| 15 |Удалено из коллекции        |
| 16 |Возобновление проверено         |
| 17 |Сбой установки        |
| 18 |Установлено         |
| 19 |Сбой удаления         |
| 20 |Удалено         |
| 21 |Запрошено продление        |

## <a name="5200-state_topictype_resource_access_status"></a>5200 STATE_TOPICTYPE_RESOURCE_ACCESS_STATUS

|     Идентификатор сообщения о состоянии     |  Описание сообщения о состоянии |
|:-------------|:------|
| 1 | Закрепление состояния успешно настроено       |
| 2 | Не удалось настроить закрепление состояния       |
| 3 | Настройка закрепления состояния не поддерживается      |
| 4 | Выполняется настройка закрепления состояния      |

## <a name="6000-state_topictype_remoteapp_subscription_status"></a>6000 STATE_TOPICTYPE_REMOTEAPP_SUBSCRIPTION_STATUS

Идентификаторы состояния отсутствуют.

## <a name="6001-state_topictype_remoteapp_subscription_sync_status"></a>6001 STATE_TOPICTYPE_REMOTEAPP_SUBSCRIPTION_SYNC_STATUS

Идентификаторы состояния отсутствуют.

## <a name="6002-state_topictype_remoteapp_authcookies_sync_status"></a>6002 STATE_TOPICTYPE_REMOTEAPP_AUTHCOOKIES_SYNC_STATUS

Идентификаторы состояния отсутствуют.

## <a name="6003-state_topictype_remoteapplications_sync_status"></a>6003 STATE_TOPICTYPE_REMOTEAPPLICATIONS_SYNC_STATUS

Идентификаторы состояния отсутствуют.

## <a name="6004-state_topictype_remoteapp_lock_result"></a>6004 STATE_TOPICTYPE_REMOTEAPP_LOCK_RESULT

Идентификаторы состояния отсутствуют.

## <a name="7000-state_topictype_user_company_term_acceptance"></a>7000 STATE_TOPICTYPE_USER_COMPANY_TERM_ACCEPTANCE

Идентификаторы состояния отсутствуют.

## <a name="7001-state_topictype_pfx_certificate"></a>7001 STATE_TOPICTYPE_PFX_CERTIFICATE

|     Идентификатор сообщения о состоянии     |  Описание сообщения о состоянии |
|:-------------|:------|
| 1 |Запрос защиты выдан    |
| 2 |Не удалось выдать запрос защиты   |
| 3 |Не удалось создать запрос   |
| 4 |Не удалось отправить запрос   |
| 5 |Проверка запроса защиты выполнена  |
| 6 |Не удалось проверить запрос защиты  |
| 7 |Сбой выдачи    |
| 8 |Ожидание выдачи    |
| 9 |Выдано     |
| 10 |Не удалось обработать ответ  |
| 11 |Ожидание ответа    |
| 12 |Регистрация выполнена    |
| 13 |Регистрация не требуется    |
| 14 |Отозвано     |
| 15 |Удалено из коллекции   |
| 16 |Возобновление проверено    |
| 17 |Сбой установки   |
| 18 |Установлено    |
| 19 |Сбой удаления    |
| 20 |Удалено    |
| 21 |Запрошено продление   |

## <a name="7010-state_topictype_conditional_access_compliance"></a>7010 STATE_TOPICTYPE_CONDITIONAL_ACCESS_COMPLIANCE

|     Идентификатор сообщения о состоянии     |  Описание сообщения о состоянии |
|:-------------|:------|
|| 1 | Надлежащий уровень соответствия    |
| 2 | Ошибка соответствия в точке управления   |
| 3 | Ошибка соответствия в клиенте   |
| 4 | Ошибка соответствия в Intune   |
| 5 | Ошибка соответствия в AAD   |
| 6 | Совместное управление соответствием в Intune   |

## <a name="7200-state_topictype_super_peer_update_cache_map"></a>7200 STATE_TOPICTYPE_SUPER_PEER_UPDATE_CACHE_MAP

|     Идентификатор сообщения о состоянии     |  Описание сообщения о состоянии |
|:-------------|:------|
| 1 |Источник однорангового кэша добавлен       |
| 2 |Источник однорангового кэша удален      |

## <a name="7201-state_topictype_super_peer_update_config"></a>7201 STATE_TOPICTYPE_SUPER_PEER_UPDATE_CONFIG

|     Идентификатор сообщения о состоянии     |  Описание сообщения о состоянии |
|:-------------|:------|
| 1 |Источник однорангового кэша отключен       |
| 2 |Источник однорангового кэша включен       |

## <a name="7202-state_topictype_download_aggregate_data"></a>7202 STATE_TOPICTYPE_DOWNLOAD_AGGREGATE_DATA
|     Идентификатор сообщения о состоянии     |  Описание сообщения о состоянии |
|:-------------|:------|
| 1 |Передача скачиваемых сводных данных       |

## <a name="7203-state_topictype_peersource_req_rejection_stats"></a>7203 STATE_TOPICTYPE_PEERSOURCE_REQ_REJECTION_STATS

|     Идентификатор сообщения о состоянии     |  Описание сообщения о состоянии |
|:-------------|:------|
| 1 |Передача данных отклонения одноранговых источников     |

## <a name="7300-state_topictype_proxy_traffic"></a>7300 STATE_TOPICTYPE_PROXY_TRAFFIC

Идентификаторы состояния отсутствуют.

## <a name="7301-state_topictype_proxy_connection"></a>7301 STATE_TOPICTYPE_PROXY_CONNECTION

Идентификаторы состояния отсутствуют.

## <a name="7302-state_topictype_srs_usage_data"></a>7302 STATE_TOPICTYPE_SRS_USAGE_DATA

Идентификаторы состояния отсутствуют.

## <a name="7303-state_topictype_proxy_traffic_identity"></a>7303 STATE_TOPICTYPE_PROXY_TRAFFIC_IDENTITY

Идентификаторы состояния отсутствуют.

## <a name="8001-state_topictype_has_report"></a>8001 STATE_TOPICTYPE_HAS_REPORT

|     Идентификатор сообщения о состоянии     |  Описание сообщения о состоянии |
|:-------------|:------|
| 1 |Подтверждение работоспособности поддерживается      |
| 2 |Подтверждение работоспособности не поддерживается      |

## <a name="state_topictype_device_client_edplog"></a>STATE_TOPICTYPE_DEVICE_CLIENT_EDPLOG

Идентификаторы состояния отсутствуют.

## <a name="8003-state_topictype_enable_lostmode"></a>8003 STATE_TOPICTYPE_ENABLE_LOSTMODE

Идентификаторы состояния отсутствуют.

## <a name="8004-state_topictype_disable_lostmode"></a>8004 STATE_TOPICTYPE_DISABLE_LOSTMODE

Идентификаторы состояния отсутствуют.

## <a name="8005-state_topictype_locate_device"></a>8005 STATE_TOPICTYPE_LOCATE_DEVICE

Идентификаторы состояния отсутствуют.

## <a name="8006-state_topictype_reboot_device"></a>8006 STATE_TOPICTYPE_REBOOT_DEVICE

Идентификаторы состояния отсутствуют.

## <a name="8007-state_topictype_logoutuser"></a>8007 STATE_TOPICTYPE_LOGOUTUSER

Идентификаторы состояния отсутствуют.

## <a name="8008-state_topictype_userslist"></a>8008 STATE_TOPICTYPE_USERSLIST

Идентификаторы состояния отсутствуют.

## <a name="8009-state_topictype_deleteuser"></a>8009 STATE_TOPICTYPE_DELETEUSER

Идентификаторы состояния отсутствуют.

## <a name="8010-state_topictype_cleanpcretaininguserdata"></a>8010 STATE_TOPICTYPE_CLEANPCRETAININGUSERDATA

Идентификаторы состояния отсутствуют.

## <a name="8011-state_topictype_cleanpcwithoutretaininguserdata"></a>8011 STATE_TOPICTYPE_CLEANPCWITHOUTRETAININGUSERDATA

Идентификаторы состояния отсутствуют.

## <a name="8012-state_topictype_setdevicename"></a>8012 STATE_TOPICTYPE_SETDEVICENAME

Идентификаторы состояния отсутствуют.

## <a name="9000-state_topictype_book_ci_compliance"></a>9000 STATE_TOPICTYPE_BOOK_CI_COMPLIANCE

Идентификаторы состояния отсутствуют.

## <a name="9001-state_topictype_book_ci_enforcement"></a>9001 STATE_TOPICTYPE_BOOK_CI_ENFORCEMENT

Идентификаторы состояния отсутствуют.

## <a name="next-steps"></a>Дальнейшие шаги

- [Описание системы отправки сообщений о состоянии в Configuration Manager](https://support.microsoft.com/help/4459394/description-of-state-messaging-in-system-center-configuration-manager)
- [Технический документ по управлению программными обновлениями для Configuration Manager](https://www.microsoft.com/download/details.aspx?id=44578)
