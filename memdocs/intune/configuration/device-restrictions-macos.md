---
title: Параметры устройств с macOS в Microsoft Intune — Azure | Документация Майкрософт
titleSuffix: ''
description: Добавление, настройка или создание для устройств с macOS параметров, которые позволяют ограничить функциональность, в том числе задать требования к паролю, управлять блокировкой экрана, использовать встроенные приложения, добавлять ограниченные или утвержденные приложения, управлять устройствами Bluetooth, подключаться к облаку для резервного копирования и хранения данных, включать режим киоска, добавлять домены, а также управлять взаимодействием пользователей с веб-браузером Safari в Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/06/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: kakyker; annovich
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: e48ba131d97e68570f1d6cb85b285ddc3198971c
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429750"
---
# <a name="macos-device-settings-to-allow-or-restrict-features-using-intune"></a>Параметры устройства с macOS, которые позволяют разрешить или ограничить некоторые функции через Intune

В этой статье перечислены и описаны параметры, которыми можно управлять на устройствах с macOS. В решении по управлению мобильными устройствами (MDM) эти параметры позволяют разрешать или отключать использование функций, задавать правила для паролей, разрешать и ограничивать отдельные приложения и т. д.

Эти параметры можно добавить в профиль конфигурации устройства в Intune, а затем назначить или развернуть на устройствах c macOS.

> [!NOTE]
> Пользовательский интерфейс может не соответствовать типам регистрации в этой статье. В этой статье приведены правильные сведения. Пользовательский интерфейс будет обновлен в предстоящем выпуске.

## <a name="before-you-begin"></a>Подготовка к работе

[Создайте профиль конфигурации ограничений устройств macOS](device-restrictions-configure.md).

> [!NOTE]
> Эти параметры применяются к различным типам регистрации. Дополнительные сведения о различных типах регистрации см. в статье о [регистрации устройств с macOS](../enrollment/macos-enroll.md).

## <a name="built-in-apps"></a>Встроенные приложения

### <a name="settings-apply-to-all-enrollment-types"></a>Область применения параметров: Все типы регистрации.

- **Блокировать автозаполнение в Safari**. Значение **Да** отключает функцию автозаполнения в браузере Safari на устройствах. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить пользователям изменять параметры автозаполнения в браузере.
- **Блокировать использование камеры**. Значение **Да** запрещает доступ к камере на устройствах. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить доступ к камере устройства.

  Intune управляет доступом только к камере устройства. У него нет доступа к изображениям или видео.
  
- **Блокировать Apple Music**. Значение **Да** возвращает приложение "Музыка" в классический режим и отключает службу Music. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить использовать приложение Apple Music.
- **Блокировать предложения Spotlight**. Значение **Да** запрещает Spotlight возвращать результаты путем поиска в Интернете. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить функции поиска Spotlight подключаться к Интернету для получения результатов.
- **Блокировать передачу файлов с помощью Finder или iTunes**. Значение **Да** отключает службы общего доступа к файлам приложений. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить использование служб общего доступа к файлам приложений.

  Данная функция применяется к:  
  - macOS 10.13 и более поздние версии

## <a name="cloud-and-storage"></a>Облако и хранилище

### <a name="settings-apply-to-all-enrollment-types"></a>Область применения параметров: Все типы регистрации.

- **Блокировать синхронизацию цепочки ключей с iCloud**. Значение **Да** отключает синхронизацию хранящихся в цепочке ключей учетных данных с iCloud. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить пользователям синхронизировать эти учетные данные.
- **Блокировать синхронизацию документов и рабочего стола в iCloud**. Значение **Да** запрещает синхронизацию документов и данных в iCloud. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить синхронизацию документов и пар "ключ — значение" в хранилище iCloud.
- **Блокировать резервное копирование почты в iCloud**. Значение **Да** запрещает синхронизацию почтового приложения macOS в iCloud. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить синхронизацию почты с iCloud.
- **Блокировать резервное копирование контактов в iCloud**. Значение **Да** запрещает синхронизацию контактов устройства в iCloud. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить синхронизацию контактов с помощью iCloud.
- **Блокировать резервное копирование календаря в iCloud**. Значение **Да** запрещает синхронизацию приложения "Календарь" macOS в iCloud. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить синхронизацию календаря с iCloud.
- **Блокировать резервное копирование напоминаний в iCloud**. Значение **Да** запрещает синхронизацию приложения "Напоминания" macOS в iCloud. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить синхронизацию напоминаний с iCloud.
- **Блокировать резервное копирование закладок в iCloud**. Значение **Да** запрещает синхронизацию закладок устройства в iCloud. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить синхронизацию закладок с iCloud.
- **Блокировать резервное копирование заметок в iCloud**. Значение **Да** запрещает синхронизацию заметок с устройства в iCloud. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить синхронизацию заметок с iCloud.
- **Блокировать резервное копирование фотографий iCloud**. Значение **Да** отключает медиатеку iCloud и запрещает синхронизировать фотографии на устройствах в iCloud. Все фотографии, не скачанные полностью из медиатеки iCloud, будут удалены из локального хранилища устройств. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить синхронизацию фотографий между устройством и медиатекой iCloud.
- **Блокировать функцию Handoff**. Эта функция позволяет пользователям начинать работу на устройстве macOS, а затем продолжать ее на другом устройстве iOS, iPadOS или macOS. Значение **Да** запрещает функцию Handoff на устройствах. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить эту функцию на устройствах.

  Данная функция применяется к:  
  - macOS 10.15 и более поздние версии;

## <a name="connected-devices"></a>Подключенные устройства

### <a name="settings-apply-to-all-enrollment-types"></a>Область применения параметров: Все типы регистрации.

- **Блокировать AirDrop**. Значение **Да** запрещает использование функции AirDrop на устройствах. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить использовать функцию AirDrop для обмена содержимым с устройствами поблизости.
- **Блокировать автоматическую разблокировку с помощью Apple Watch**. Значение **Да** запрещает пользователям разблокировку устройства macOS с помощью их Apple Watch. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить пользователям разблокировать свои устройства macOS при помощи Apple Watch.

## <a name="domains"></a>Домены

### <a name="settings-apply-to-all-enrollment-types"></a>Область применения параметров: Все типы регистрации.

- **Неотмеченные домены электронной почты**. Добавьте в список один **URL-адрес домена электронной почты** или несколько. Если пользователь отправляет или получает сообщение электронной почты из домена, отличного от добавленного вами домена, то это сообщение отмечается как недоверенное в почтовом приложении macOS.

## <a name="general"></a>Общие

### <a name="settings-apply-to-all-enrollment-types"></a>Область применения параметров: Все типы регистрации.

- **Блокировать поиск**. Значение **Да** запрещает пользователям выделять слова и искать их определения на устройстве. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить функцию поиска определений.
- **Блокировать диктовку**. Значение **Да** запрещает пользователям вводить текст с помощью голосового ввода. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить пользователям использовать диктовку для ввода текста.
- **Блокировать кэширование содержимого**. Значение **Да** запрещает кэширование содержимого. Кэширование содержимого позволяет хранить данные приложений, веб-браузера, скачанные файлы и многое другое локально на устройствах. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию операционная система может включить кэширование содержимого.

  Дополнительные сведения о кэшировании содержимого в macOS см. в разделе [Управление кэшированием содержимого на компьютере Mac](https://support.apple.com/guide/mac-help/manage-content-caching-on-mac-mchl3b6c3720/mac) (открывается другой веб-сайт).

  Данная функция применяется к:  
  - macOS 10.13 и более поздние версии

- **Задержка обновлений ПО**. Значение **Да** позволяет задержать появление обновлений программного обеспечения на устройствах на срок от 0 до 90 дней. Этот параметр не контролирует, устанавливаются ли обновления. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию в ОС могут отображаться обновления на устройствах по мере их выпуска компанией Apple. Например, если обновление macOS выпущено компанией Apple в определенный день, то оно естественным образом появится на устройствах в тот же день. Начальные обновления разрешаются без задержки.  

  - **Задержка показа обновлений ПО**. Введите значение от 0 до 90 дней. Когда задержка истекает, пользователи получают уведомление о том, что необходимо обновить ОС до самой ранней версии, которая была доступна на момент активации задержки.

    Например, если обновление macOS выходит **1 января** и для параметра **Задержка видимости** задано значение **5 дней**, то оно не будет показано как доступное обновление. На **шестой день** после выпуска обновление станет доступно, и пользователи смогут установить его.

    Данная функция применяется к:  
    - macOS 10.13.4 и более поздние версии

- **Блокировать снимки экрана и запись экрана**. Устройство должно быть зарегистрировано в программе автоматической регистрации устройств (DEP) Apple. Значение **Да** запрещает пользователям сохранять снимки экрана. Это также предотвращает наблюдение за удаленными экранами в приложении Classroom. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС позволяет пользователям сохранять снимки экрана, а в приложении Classroom — просматривать удаленные экраны.

  - **Отключить AirPlay, просмотр экрана приложением Classroom и общий доступ к экрану**. Значение **Да** блокирует AirPlay и запрещает совместное использование экрана с другими устройствами. Оно также запрещает преподавателям использовать приложение Classroom для просмотра экранов учащихся. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может позволять преподавателям видеть экраны учащихся.

    Чтобы использовать этот параметр, установите для параметра **Блокировать снимки экрана и запись экрана** значение **Не настроено** (снимки экрана разрешены).

  - **Разрешить приложению Classroom выполнять AirPlay и просматривать экран без запроса**. Значение **Да** позволяет преподавателям просматривать экраны учащихся, не запрашивая их согласие. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может требовать согласия учащихся, прежде чем преподаватели смогут видеть экраны.

    Чтобы использовать этот параметр, установите для параметра **Блокировать снимки экрана и запись экрана** значение **Не настроено** (снимки экрана разрешены).

- **Требовать разрешение преподавателя на выход из неуправляемых классов приложения Classroom**. При выборе значения **Да** учащиеся, зарегистрированные в неуправляемом курсе Classroom, должны будут запрашивать разрешение преподавателя для выхода из курса. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может позволять учащимся покидать курс по желанию.

- **Разрешить Classroom блокировать устройство без запроса**. Значение **Да** позволяет преподавателям блокировать устройство или приложение учащегося без его подтверждения. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может требовать согласия учащихся, прежде чем преподаватели смогут заблокировать устройство или приложение.

- **Учащиеся могут присоединяться к классу Classroom автоматически без запроса**. Значение **Да** позволяет учащимся присоединяться к классу, не отправляя запрос преподавателю. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может требовать, чтобы преподаватель одобрял вступление в класс.

## <a name="password"></a>Пароль

### <a name="settings-apply-to-all-enrollment-types"></a>Область применения параметров: Все типы регистрации.

- **Требовать пароль**. При выборе значения **Да** пользователи должны будут вводить пароль для доступа к устройству. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может не требовать пароль. Не будет также никаких ограничений, таких как блокирование простых паролей или установка минимальной длины.
  - **Требуемый тип пароля**. Введите уровень сложности пароля, который требуется вашей организации. Если значение не указано, Intune не изменяет и не обновляет этот параметр. Доступны следующие параметры:
    - **Не настроено**. Используется устройство по умолчанию.
    - **Буквенно-цифровой**. Включает прописные буквы, строчные буквы и цифровые символы.
    - **Числовой**. Пароль должен состоять только из цифр, например 123456789.

    Данная функция применяется к:  
    - macOS 10.10.3 и более поздние версии

  - **Число символов в пароле, кроме букв и цифр**. Введите количество сложных символов, необходимых в пароле (от 0 до 4). Пример сложного символа — `?` Если поле оставлено пустым или задано значение **Не настроено**, Intune не изменяет и не обновляет этот параметр.
  - **Минимальная длина пароля**. Укажите минимальное число символов, которое должно быть в пароле (от 4 до 16). Если значение не указано, Intune не изменяет и не обновляет этот параметр.
  - **Блокировать использование простых паролей**. Значение **Да** запрещает использование простых паролей, таких как `0000` или `1234`. Если значение не задано или указано **Не настроено**, Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешать простые пароли.
  - **Максимальное время бездействия (в минутах), по истечении которого экран блокируется**. Введите период бездействия устройства, по истечении которого экран автоматически блокируется. Например, введите значение `5`, чтобы блокировать устройства после 5 минут бездействия. Если значение не задано или указано **Не настроено**, Intune не изменяет или не обновляет этот параметр.
  - **Максимальный срок после блокировки экрана (в минутах), по истечении которого запрашивается пароль**. Укажите, как долго устройство должно оставаться неактивным до его блокировки, для снятия которой потребуется пароль. Если значение не задано или указано **Не настроено**, Intune не изменяет или не обновляет этот параметр.
  - **Срок действия пароля (в днях)** . Укажите число дней до смены пароля на устройстве (от 1 до 65535). Например, чтобы изменить пароль через 90 дней, введите `90`. Когда срок действия пароля истекает, пользователям предлагается создать пароль. Если значение не задано или указано **Не настроено**, Intune не изменяет или не обновляет этот параметр.
  - **Запретить использование предыдущих паролей**. С помощью этого параметра можно запретить пользователям применять предыдущие пароли. Введите число предыдущих паролей, которые нельзя использовать повторно (1–24). Значение 5 означает, что в качестве нового пароля пользователь не может установить свой текущий или любой из четырех предыдущих паролей. Если значение не указано, Intune не изменяет или не обновляет этот параметр.

- **Блокировать изменение секретного кода пользователем**. Значение **Да** запрещает изменение, добавление и удаление секретного кода. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить добавлять, изменять и (или) удалять секретные коды.

- **Блокировать Touch ID для разблокировки устройства**. Значение **Да** запрещает использование отпечатка пальца для разблокировки устройств. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить пользователям разблокировать устройство с помощью отпечатка пальца.

- **Блокировать автозаполнение пароля**. Значение **Да** запрещает использование функции автозаполнения паролей в macOS. Кроме того, выбор значения **Да** оказывает следующее воздействие:

  - пользователям не предлагается использовать сохраненный пароль в Safari и в любых других приложениях;
  - отключается функция автоматических надежных паролей и пользователям не предлагаются надежные пароли.

  Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить эти функции.

- **Блокировать запросы близкого взаимодействия пароля**. Значение **Да** запрещает устройствам запрашивать пароли у ближайших устройств. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить эти запросы пароля.

- **Блокировать общий доступ к паролям**. Значение **Да** запрещает обмен паролями между устройствами с помощью AirDrop. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить общий доступ к паролям.

## <a name="privacy-preferences"></a>Параметры конфиденциальности

На устройствах macOS приложения и процессы часто предлагают пользователям разрешить или запретить доступ к таким функциям устройства, как камера, микрофон, календарь, папка "Документы" и т. д. Параметры конфиденциальности позволяют администраторам предварительно одобрять или запрещать доступ к этим функциям устройств. При настройке этих параметров вы управляете согласием на доступ к данным от имени своих пользователей. Ваши параметры переопределяют их предыдущие решения.

Эти параметры предназначены для того, чтобы сократить количество запросов, которые выдают приложения и процессы.

Данная функция применяется к:

- macOS 10.14 и более поздних версий
- Некоторые параметры относятся к macOS 10.15 и более поздних версий.
- Эти параметры применяются только на устройствах с установленным профилем параметров конфиденциальности перед обновлением.

### <a name="settings-apply-to-user-approved-device-enrollment-automated-device-enrollment"></a>Область применения параметров: утвержденная пользователем регистрация устройств, автоматическая регистрация устройств

- **Приложения и процессы**. **Добавление** приложений или процессов для настройки доступа. Кроме того, укажите:
  - **Имя** — Введите имя для приложения или процесса. Например, введите `Microsoft Remote Desktop` или `Microsoft Office 365`.
  
  - **Тип идентификатора**. Доступны следующие параметры:
    - **Идентификатор пакета**. Выберите этот параметр для приложений.
    - **Путь**. Выберите этот параметр для не объединенных в пакет двоичных файлов, которые являются процессами или исполняемыми файлами.

    Вспомогательные инструменты, встроенные в пакет приложения, автоматически наследуют расширения пакета приложения, в который они включены.

  - **Идентификатор**. Введите идентификатор пакета приложения или путь к файлу установки процесса или исполняемого файла. Например, введите `com.contoso.appname`.

    Чтобы получить идентификатор пакета приложения, откройте приложение Terminal и выполните команду `codesign`. Эта команда идентифицирует сигнатуру кода. Таким образом, вы можете одновременно получить идентификатор пакета и сигнатуру кода.

  - **Требование к коду**. Введите сигнатуру кода для приложения или процесса.

    Сигнатура кода создается, когда приложение или двоичный файл подписывается сертификатом разработчика. Чтобы найти это обозначение, выполните команду `codesign` вручную в приложении Terminal: `codesign --display -r -/path/to/app/binary`. Сигнатура кода — это все, что отображается после `=>`.

  - **Включить статическую проверку кода**. Выберите значение **Да**, чтобы выполнялась статическая проверка кода для приложения или процесса. Если задано значение **Не настроено**, Intune не изменяет или не обновляет этот параметр.

    Включайте этот параметр, только если процесс аннулирует свою динамическую сигнатуру кода. В противном случае укажите **Не настроено**.  

  - **Блокировать камеру**. Значение **Да** запрещает приложению доступ к камере. Вы не можете разрешить доступ к камере. Если задано значение **Не настроено**, Intune не изменяет или не обновляет этот параметр.

  - **Блокировать микрофон**. Значение **Да** запрещает приложению доступ к микрофону системы. Вы не можете разрешить доступ к микрофону. Если задано значение **Не настроено**, Intune не изменяет или не обновляет этот параметр.

  - **Блокировать запись экрана**. Значение **Да** запрещает приложению записывать содержимое экрана системы. Вы не можете разрешить доступ к записи экрана и снимкам экрана. Если задано значение **Не настроено**, Intune не изменяет или не обновляет этот параметр.

    Требуется macOS 10.15 или более поздней версии.

  - **Блокировать отслеживание ввода**. Значение **Да** запрещает приложению использовать API-интерфейсы CoreGraphics и HID для прослушивания событий CGEvents и HID из всех процессов. Кроме того, значение **Да** запрещает приложениям и процессам прослушивание и сбор данных с устройств ввода, таких как мышь, клавиатура или сенсорная панель. Вы не можете разрешать доступ к API-интерфейсам CoreGraphics и HID.

    Если задано значение **Не настроено**, Intune не изменяет или не обновляет этот параметр.

    Требуется macOS 10.15 или более поздней версии.

  - **Распознавание речи**. Доступны следующие параметры:
    - **Не настроено**. Intune не изменяет или не обновляет этот параметр.
    - **Разрешить**: Разрешает приложению доступ к системе распознавания речи и отправку речевых данных в Apple.
    - **Блокировать**: Запрещает приложению доступ к системе распознавания речи и отправку речевых данных в Apple.

    Требуется macOS 10.15 или более поздней версии.

  - **Специальные возможности**. Доступны следующие параметры:
    - **Не настроено**. Intune не изменяет или не обновляет этот параметр.
    - **Разрешить**. Разрешает приложению доступ к системному приложению специальных возможностей. Это приложение включает в себя скрытые субтитры, отображение текста при наведении курсора и голосовое управление.
    - **Блокировать**. Запрещает приложению доступ к системному приложению специальных возможностей.

  - **Контакты**. Доступны следующие параметры:
    - **Не настроено**. Intune не изменяет или не обновляет этот параметр.
    - **Разрешить**. Разрешает приложению доступ к контактным данным, которыми управляет приложение "Контакты".  
    - **Блокировать**. Запрещает приложению доступ к контактным данным.

  - **Календарь**. Доступны следующие параметры:
    - **Не настроено**. Intune не изменяет или не обновляет этот параметр.
    - **Разрешить**. Разрешает приложению доступ к данным календаря, которыми управляет системное приложение "Календарь".
    - **Блокировать**. Запрещает приложению доступ к данным календаря.

  - **Напоминания**. Доступны следующие параметры:
    - **Не настроено**. Intune не изменяет или не обновляет этот параметр.
    - **Разрешить**. Разрешает приложению доступ к данным напоминаний, которыми управляет системное приложение "Напоминания".
    - **Блокировать**. Запрещает приложению доступ к данным напоминаний.

  - **Фотографии**. Доступны следующие параметры:
    - **Не настроено**. Intune не изменяет или не обновляет этот параметр.
    - **Разрешить**. Разрешает приложению доступ к изображениям, которыми управляет системное приложение "Фотографии" `~/Pictures/.photoslibrary`.
    - **Блокировать**. Запрещает приложению доступ к этим изображениям.

  - **Библиотека мультимедиа**. Доступны следующие параметры:
    - **Не настроено**. Intune не изменяет или не обновляет этот параметр.
    - **Разрешить**. Разрешает приложению доступ к Apple Music, действиям с музыкой и видео, а также к библиотеке мультимедиа.  
    - **Блокировать**. Запрещает приложению доступ к мультимедиа.

    Требуется macOS 10.15 или более поздней версии.

  - **Присутствие поставщика файлов**. Доступны следующие параметры:
    - **Не настроено**. Intune не изменяет или не обновляет этот параметр.
    - **Разрешить**. Разрешает приложению доступ к приложению "Поставщик файлов" и позволяет ему знать, когда пользователи используют файлы, которыми управляет поставщик файлов. Приложение "Поставщик файлов" разрешает другим приложениям поставщика файлов доступ к документам и каталогам, которые хранятся в этом приложении и управляются им.
    - **Блокировать**. Запрещает приложению доступ к приложению "Поставщик файлов".

    Требуется macOS 10.15 или более поздней версии.

  - **Полный доступ к диску**. Доступны следующие параметры:
    - **Не настроено**. Intune не изменяет или не обновляет этот параметр.
    - **Разрешить**. Разрешает приложению доступ ко всем защищенным файлам, включая файлы системного администрирования. Применяйте этот параметр с осторожностью.
    - **Блокировать**. Запрещает приложению доступ к этим защищенным файлам.

  - **Файлы системного администрирования**. Доступны следующие параметры:
    - **Не настроено**. Intune не изменяет или не обновляет этот параметр.
    - **Разрешить**. Разрешает приложению доступ к некоторым файлам, используемым в системном администрировании.
    - **Блокировать**. Запрещает приложению доступ к этим файлам.

  - **Папка "Рабочий стол"** . Доступны следующие параметры:
    - **Не настроено**. Intune не изменяет или не обновляет этот параметр.
    - **Разрешить**. Разрешает приложению доступ к файлам в папке "Рабочий стол" пользователя.
    - **Блокировать**. Запрещает приложению доступ к этим файлам.

    Требуется macOS 10.15 или более поздней версии.

  - **Папка "Мои документы"** . Доступны следующие параметры:
    - **Не настроено**. Intune не изменяет или не обновляет этот параметр.
    - **Разрешить**. Разрешает приложению доступ к файлам в папке "Мои документы" пользователя.
    - **Блокировать**. Запрещает приложению доступ к этим файлам.

    Требуется macOS 10.15 или более поздней версии.

  - **Папка "Загрузки"** . Доступны следующие параметры:
    - **Не настроено**. Intune не изменяет или не обновляет этот параметр.
    - **Разрешить**. Разрешает приложению доступ к файлам в папке "Загрузки" пользователя.
    - **Блокировать**. Запрещает приложению доступ к этим файлам.

    Требуется macOS 10.15 или более поздней версии.

  - **Сетевые тома**. Доступны следующие параметры:
    - **Не настроено**. Intune не изменяет или не обновляет этот параметр.
    - **Разрешить**. Разрешает приложению доступ к файлам в сетевых томах.
    - **Блокировать**. Запрещает приложению доступ к этим файлам.

    Требуется macOS 10.15 или более поздней версии.

  - **Съемные тома**. Доступны следующие параметры:
    - **Не настроено**. Intune не изменяет или не обновляет этот параметр.
    - **Разрешить**. Разрешает приложению доступ к файлам в съемных томах, таких как жесткий диск.
    - **Блокировать**. Запрещает приложению доступ к этим файлам.

    Требуется macOS 10.15 или более поздней версии.

  - **Системные события**. Доступны следующие параметры:
    - **Не настроено**. Intune не изменяет или не обновляет этот параметр.
    - **Разрешить**. Разрешает приложению использовать API-интерфейсы CoreGraphics для отправки событий CGEvents в поток системных событий.
    - **Блокировать**. Запрещает приложению использовать API-интерфейсы CoreGraphics для отправки событий CGEvents в поток системных событий.

  - **События Apple**. Этот параметр разрешает приложениям отправлять событие Apple с ограниченным доступом в другое приложение или процесс. Нажмите **Добавить**, чтобы добавить получающее приложение или процесс. Введите следующие сведения о получающем приложении или процессе.

    - **Тип идентификатора**. Выберите **Идентификатор пакета**, если получающим объектом является приложение. Выберите **Путь**, если получающим объектом является процесс или исполняемый файл.
    
    - **Идентификатор**. Введите идентификатор пакета приложения или путь к файлу установки процесса, получающего событие Apple.  

    - **Требование к коду**. Введите сигнатуру кода для получающего приложения или процесса.

      Сигнатура кода создается, когда приложение или двоичный файл подписывается сертификатом разработчика. Чтобы найти это обозначение, выполните команду `codesign` вручную в приложении Terminal: `codesign --display -r -/path/to/app/binary`. Сигнатура кода — это все, что отображается после `=>`.

    - **Доступ**. Разрешить отправку события Apple macOS в получающее приложение или процесс. Доступны следующие параметры:
      - **Не настроено**. Intune не изменяет или не обновляет этот параметр.
      - **Разрешить**. Разрешает приложению или процессу отправку события Apple с ограниченным доступом в получающее приложение или процесс.
      - **Блокировать**. Запрещает приложению или процессу отправку события Apple с ограниченным доступом в получающее приложение или процесс.

  - **Сохраните** внесенные изменения.

## <a name="restricted-apps"></a>Ограниченные приложения

### <a name="settings-apply-to-all-enrollment-types"></a>Область применения параметров: Все типы регистрации.

- **Тип списка ограниченных приложений**. Создайте список приложений, которые пользователи не могут устанавливать или использовать. Доступны следующие параметры:

  - **Не настроено** (по умолчанию). Intune не изменяет или не обновляет этот параметр. По умолчанию пользователи могут иметь доступ к назначенным вами приложениям и встроенным приложениям.
  - **Утвержденные приложения**. Указывает приложения, которые пользователям разрешено устанавливать. Для сохранения совместимости пользователям не следует устанавливать другие приложения. Приложения под управлением Intune автоматически разрешены, включая приложение Корпоративного портала. Пользователям не запрещено устанавливать приложения, которых нет в списке утвержденных. Но о такой установке сообщается в Intune.
  - **Запрещенные приложения**. Указывает приложения, не управляемые Intune, которые пользователям запрещено устанавливать и запускать. Пользователям могут устанавливать запрещенные приложения. Если пользователь устанавливает приложение из этого списка, об этом сообщается в Intune.

- **Список приложений**. **Добавьте** приложения в свой список.
  - **Идентификатор набора приложений**. Введите [идентификатор](bundle-ids-built-in-ios-apps.md) пакета приложения. Вы можете добавлять встроенные приложения и бизнес-приложения. На веб-сайте Apple есть список [встроенных приложений Apple](https://support.apple.com/HT208094).

    Чтобы найти URL-адрес приложения, откройте iTunes App Store и найдите это приложение. Например, выполните поиск по фразе `Microsoft Remote Desktop` или `Microsoft Word`. Выберите приложение и скопируйте URL-адрес. Также вы можете найти приложение через iTunes, а затем получить URL-адрес этого приложения с помощью команды **Копировать ссылку**.

  - **Имя приложения**. Введите понятное имя, которое позволит идентифицировать пакет. Например, введите `Intune Company Portal app`.
  - **Издатель** — укажите издателя приложения.

- **Импортируйте** CSV-файл с подробными сведениями о приложении, включая URL-адрес. Используйте формат `<app bundle ID>, <app name>, <app publisher>`. Или нажмите **Экспорт**, чтобы создать список добавленных приложений в том же формате.

## <a name="next-steps"></a>Дальнейшие шаги

[Назначьте профиль](device-profile-assign.md) и [отслеживайте его состояние](device-profile-monitor.md).

Можно также ограничить параметры и функции на устройствах с [iOS/iPadOS](device-restrictions-ios.md).
