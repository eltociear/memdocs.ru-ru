---
title: Интерактивный сценарий. Безопасные мобильные приложения Microsoft Office
titleSuffix: Microsoft Intune
description: Ознакомьтесь с интерактивным сценарием развертывания безопасных мобильных приложений Microsoft Office с портала управления устройствами Microsoft 365.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/06/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7aabc09e276c723e9aeaed4ec8eb3dd4c0332b4e
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "79362515"
---
# <a name="guided-scenario---secure-microsoft-office-mobile-apps"></a>Интерактивный сценарий. Безопасные мобильные приложения Microsoft Office

Следуя этому интерактивному сценарию на портале управления устройствами, можно включить базовую защиту приложений Intune на устройствах с iOS/iPadOS и Android.

При включенной защите приложений будут применяться следующие действия:

- шифрование рабочих файлов;
- Требование ПИН-кода для доступа к рабочим файлам.
- Требование сброса ПИН-кода после пяти неудачных попыток ввода.
- Запрет резервного копирования рабочих файлов в службах резервного копирования iTunes, iCloud или Android.  
- Требование сохранения рабочих файлов только в OneDrive или SharePoint.
- Запрет защищенным приложениям загружать рабочие файлы на устройствах со снятой защитой или с административным доступом.
- Блокировка доступа к рабочим файлам, если устройство находится в автономном режиме в течение 720 минут.
- Удаление рабочих файлов, если устройство находится в автономном режиме в течение 90 дней.

## <a name="background"></a>Краткая справка

Мобильные приложения Office, а также Microsoft Edge для мобильных устройств, поддерживают двойное удостоверение. Двойное удостоверение позволяет приложениям управлять рабочими файлами отдельно от личных. 

![Изображение корпоративных данных и персональных данных](./media/guided-scenarios-office-mobile/guided-scenarios-office-mobile-01.png)

[Политики защиты приложений Intune](../apps/app-protection-policy.md) помогают защитить рабочие файлы на устройствах, зарегистрированных в Intune. Политики защиты приложений также можно использовать на устройствах, принадлежащих сотрудникам, которые не зарегистрированы для управления в Intune. В этом случае, даже если компания не управляет устройством, все равно необходимо обеспечить защиту рабочих файлов и ресурсов.

Политики защиты приложений можно использовать, чтобы запретить пользователям сохранять рабочие файлы в незащищенных расположениях. Вы также можете ограничить перемещение данных в другие приложения, которые не защищены с помощью политик защиты приложений. К параметрам политик защиты приложений можно отнести следующие.

- Политики перемещения данных, такие как **Сохранение копий корпоративных данных** и **Блокировать вырезание, копирование и вставку**.
- Параметры политик доступа, такие как "Требовать простой ПИН-код для доступа" и "Блокировать запуск управляемых приложений на устройствах со снятой защитой или с административным доступом".

Функции условного доступа на основе приложений и управления клиентскими приложениями позволяют реализовать дополнительный уровень безопасности, предоставляя доступ к Exchange Online и другим службам Office 365 только клиентским приложениям, поддерживающим политики защиты приложений Intune.

Вы можете заблокировать встроенные приложения электронной почты iOS/iPadOS и Android и разрешить доступ к Exchange Online только для приложения Microsoft Outlook. Кроме того, вы можете заблокировать доступ к SharePoint Online для приложений, к которым не применяются политики защиты приложений Intune.

В этом примере администратор применил к приложению Outlook политики защиты приложений, а также правило условного доступа, по которому приложение Outlook добавляется в список утвержденных приложений, которые можно использовать для доступа к корпоративной электронной почте.

![Последовательность процесса условного доступа приложения Outlook](./media/guided-scenarios-office-mobile/guided-scenarios-office-mobile-02.png)

## <a name="prerequisites"></a>Предварительные условия

Вам потребуются следующие разрешения администратора Intune.

- Управляемые приложения: чтение, создание, удаление и назначение
- Наборы политик: чтение, создание и назначение
- Организация: чтение

## <a name="step-1---introduction"></a>Шаг 1. Введение

Следуя приведенному ниже интерактивному сценарию **Защита приложений Intune**, вы предотвратите общий доступ к данным или их утечку за пределы организации. 

Назначенные пользователи iOS/iPadOS и Android должны вводить ПИН-код при каждом открытии приложения Office. После 5 неудачных попыток ПИН-кода пользователи должны будут сбросить свой ПИН-код. Если ПИН-код устройства уже требуется, пользователи не будут затронуты.

### <a name="what-you-will-need-to-continue"></a>Что потребуется для продолжения

Мы спросим вас, какие приложения необходимы пользователям, и о том, что необходимо для доступа к ним. Убедитесь, что у вас есть следующие сведения.

- Список приложений Office, утвержденных для корпоративного использования.
- Любые требования к ПИН-коду для запуска утвержденных приложений на неуправляемых устройствах.

## <a name="step-2---basics"></a>Шаг 2. Основные сведения

На этом шаге необходимо ввести **Префикс** и **Описание** новой политики защиты приложений. При добавлении **префикса** сведения, относящиеся к ресурсам, создаваемым в ходе сценария, будут обновлены. Эти сведения облегчают поиск политик в дальнейшем, если необходимо изменить назначения и конфигурацию.

> [!TIP]
> Стоит записать ресурсы, которые будут созданы, чтобы их можно было использовать позже.

## <a name="step-3---apps"></a>Шаг 3. Приложения

Чтобы помочь вам приступить к работе, в этом интерактивном сценарии для защиты заранее выбраны следующие мобильные приложения на устройствах с iOS/iPadOS и Android:

- Microsoft Excel
- Microsoft Word
- Microsoft Teams
- Microsoft Edge
- Microsoft PowerPoint
- Microsoft Outlook
- Microsoft OneDrive

Этот интерактивный сценарий также позволяет настроить эти приложения для открытия веб-ссылок в Microsoft Edge, чтобы обеспечить открытие рабочих сайтов в защищенном браузере.

Измените список управляемых политикой приложений, которые требуется защитить. Добавьте или удалите приложения из этого списка.

Выбрав приложения, нажмите кнопку **Далее**.

## <a name="step-4---configuration"></a>Шаг 4. Настройка

На этом шаге необходимо настроить требования для доступа к корпоративным файлам и сообщениям электронной почты в этих приложениях и предоставления к ним общего доступа. По умолчанию пользователи могут сохранять данные в учетных записях OneDrive и SharePoint вашей организации.

| Параметр | Описание | Значение по умолчанию |
|---------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|
| Тип ПИН-кода | Числовые ПИН-коды состоят из цифр. Секретные коды состоят из буквенно-цифровых и специальных символов.  Чтобы настроить тип секретного кода в iOS или iPadOS, для приложения требуется пакет SDK для Intune версии 7.1.12 или более поздней. Числовой тип не имеет ограничений версии пакета SDK для Intune. | Числовой |
| Выберите минимальную длину ПИН-кода | укажите минимальное число цифр в ПИН-коде. | 6 |
| Перепроверять требования доступа через (минут бездействия) | Если приложение, управляемое политикой, находится в неактивном состоянии дольше, чем указано, приложение применяет требования к доступу (т. е. ПИН-код, параметры условного запуска) для повторной проверки после запуска приложения. | 30 |
| Печать данных организации | Если заблокировать печать, приложение не сможет печатать защищенные данные. | Блокировать |
| Открытие ссылок на управляемые политикой приложения в неуправляемых браузерах | Если параметр заблокирован, ссылки на приложения, управляемые политикой, должны открываться в управляемом браузере. | Блокировать |
| Копирование данных в неуправляемые приложения | При блокировке управляемые данные останутся в управляемых приложениях. | Allow |

## <a name="step-5---assignments"></a>Шаг 5. Назначения

На этом шаге можно выбрать группы пользователей, которые необходимо включить, чтобы обеспечить им доступ к корпоративным данным. Защита приложений назначается пользователям, а не устройствам, поэтому корпоративные данные будут защищены независимо от используемого устройства и состояния его регистрации.

Пользователи без политик защиты приложений и назначенных параметров условного доступа смогут сохранять данные из своего корпоративного профиля в личных приложениях и неуправляемом локальном хранилище на мобильных устройствах. Они могут также подключаться к корпоративным службам данных, таким как Microsoft Exchange, используя персональные приложения.

## <a name="step-6---review--create"></a>Шаг 6. Проверка и создание

На последнем шаге вы можете ознакомиться с краткими сведениями о настроенных параметрах. После просмотра настроек нажмите кнопку **Создать**, чтобы завершить интерактивный сценарий. После завершения интерактивного сценария отобразится таблица ресурсов. Эти ресурсы можно изменить позже, но после выхода из представления сводки таблица не будет сохранена.

> [!IMPORTANT]
> После завершения интерактивного сценария отобразится сводка. Ресурсы, перечисленные в сводке, можно изменить позже, однако таблица, в которой они отображаются, не будет сохранена.

## <a name="next-steps"></a>Дальнейшие действия

- Повышение безопасности рабочих файлов путем назначения пользователям политики условного доступа на основе приложений для защиты облачных служб от отправки рабочих файлов в незащищенные приложения. Дополнительные сведения см. в статье [Настройка политик условного доступа на основе приложений с помощью Intune](../protect/app-based-conditional-access-intune-create.md).
