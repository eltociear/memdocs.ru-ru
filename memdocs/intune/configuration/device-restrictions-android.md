---
title: Параметры ограничений для устройств Android в Microsoft Intune в Azure | Документация Майкрософт
description: Список всех параметров для администратора устройства Android, которые можно администрировать и ограничивать в Microsoft Intune. Используйте эти параметры, чтобы управлять паролями, доступом к Google Play, разрешать или запрещать использовать приложения, управлять параметрами браузера, блокировать приложения, выполнять резервное копирование в облако Google, а также управлять сообщениями, голосовыми сообщениями, передачей данных в роуминге и параметрами подключения по Wi-Fi и Bluetooth.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/30/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: chmaguir, chrisbal
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5fc11d7302c30dd53314eb2312d37842b081a6b3
ms.sourcegitcommit: 5f9d5d22114ae5aeb0270c7fb59c5dced5f48826
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/06/2020
ms.locfileid: "82862366"
---
# <a name="android-and-samsung-knox-standard-device-restriction-settings-lists-in-intune"></a>Списки параметров ограничений для устройств Android и Samsung KNOX Standard в Intune

В этой статье описаны все параметры ограничения устройств в Microsoft Intune, которые можно настроить для устройств под управлением Android.

>[!TIP]
>Если нужные параметры недоступны, можно настроить устройства с помощью [пользовательского профиля](custom-settings-android.md).

## <a name="before-you-begin"></a>Подготовка к работе

[Создайте профиль конфигурации устройства](device-restrictions-configure.md).

## <a name="general"></a>Общие

- **Камера**. Значение **Блокировать** запрещает доступ к камере на устройстве. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить доступ к камере устройства.

  Intune управляет доступом только к камере устройства. У него нет доступа к изображениям или видео.

- **Копирование и вставка (только Samsung Knox)** . Значение **Блокировать** запрещает копирование и вставку. Если выбрать вариант **Не настроено**, операции копирования и вставки на устройствах будут разрешены.
- **Совместное использование буфера обмена приложениями (только Samsung Knox)** . Если выбрать значение **Блокировать**, использование буфера обмена для копирования и вставки между приложениями будет запрещено. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить функции копирования и вставки на устройствах.
- **Отправка диагностических данных (только Samsung Knox)** . Значение **Блокировать** запрещает пользователям отправлять отчеты об ошибках с устройств. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить пользователям отправлять данные.
- **Очистка (только Samsung Knox)** . Разрешает пользователям выполнять действие [очистки](../remote-actions/devices-wipe.md) на устройствах. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр.
- **Геолокация (только Samsung Knox)** . Значение **Блокировать** запрещает устройствам использовать сведения о расположении. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить устройствам использовать сведения о расположении.
- **Отключение питания (только Samsung Knox)** . Значение **Блокировать** запрещает пользователям выключать питание устройства. Оно также запрещает настраивать и использовать параметр **Число неудачных попыток входа перед очисткой устройства**. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить пользователям отключать устройства.
- **Снимок экрана (только Samsung Knox)** . Значение **Блокировать** запрещает делать снимки экрана. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить пользователям записывать содержимое экрана в виде изображения.
- **Голосовой помощник (только Samsung Knox)** . Значение **Блокировать** отключает службу S Voice. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить использовать службу и приложение S Voice на устройствах. Этот параметр не применяется к Bixby или голосовому помощнику специальных возможностей, который читает содержимое экрана.
- **YouTube (только Samsung Knox)** . Значение **Блокировать** запрещает использовать приложение YouTube. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить использовать приложение YouTube на устройствах.
- **Общие устройства (только Samsung Knox)** . Настройка общего доступа к управляемому устройству Samsung Knox. Значение **Разрешить** позволяет пользователям входить на устройства с помощью учетных данных Azure AD. Устройства остаются управляемыми, даже если не используются.

  Если эту функцию использовать с профилем сертификата SCEP, пользователи смогут использовать устройства с тем же набором приложений совместно со всеми пользователями. Но у каждого пользователя будет свой сертификат SCEP. После выхода пользователя из системы все данные приложения удаляются. Эта функция поддерживается только для бизнес-приложений.

  Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может запретить нескольким пользователям одновременно входить в приложение "Корпоративный портал" на устройстве, используя свои учетные данные Azure AD.
- **Блокировать изменение даты и времени (Samsung Knox)** . Значение **Блокировать** запрещает пользователям изменять параметры даты и времени устройств. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить пользователям изменять параметры даты и времени.

## <a name="password"></a>Пароль

- **Пароль**. При значении **Требовать** пользователь должен ввести пароль для доступа к устройству. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить доступ пользователей к устройствам без ввода пароля.

    > [!NOTE]
    > Устройства Samsung Knox автоматически запрашивают 4-значный ПИН-код во время регистрации MDM. Собственные устройства Android могут автоматически запрашивать ПИН-код для обеспечения соответствия с политикой условного доступа.

- **Минимальная длина пароля**. Введите минимальное число обязательных символов (4–16). Например, введите `6`, чтобы требовать по крайней мере шесть символов в пароле.
- **Максимальное время бездействия (в минутах), по истечении которого экран блокируется**. Введите период бездействия устройства, по истечении которого экран автоматически блокируется. Например, введите значение `5`, чтобы блокировать устройства после 5 минут бездействия. Если значение не задано или указано **Не настроено**, Intune не изменяет или не обновляет этот параметр.

  Время бездействия, задаваемое пользователем на устройстве, не может превышать время, заданное в профиле. Пользователи могут задать меньшее значение времени. Например, если в профиле задано `15` минут, пользователь может задать значение, равное 5 минутам. Пользователь не сможет задать значение, равное 30 минутам.

- **Число неудачных попыток входа перед очисткой устройства**. Введите число попыток ввода пароля до очистки устройств (от 4 до 11). `0` (ноль) позволяет отключить функцию очистки устройств. Если значение не указано, Intune не изменяет или не обновляет этот параметр.
- **Срок действия пароля (в днях)** . Укажите число дней до смены пароля на устройстве (от 1 до 365). Например, чтобы изменить пароль через 90 дней, введите `90`. Когда срок действия пароля истекает, пользователям предлагается создать пароль. Если значение не указано, Intune не изменяет или не обновляет этот параметр.
- **Требуемый тип пароля**. Задайте требуемый уровень сложности пароля и укажите, можно ли использовать биометрические устройства. Доступны следующие параметры:
  - **Устройство по умолчанию**.
  - **Биометрический с низким уровнем безопасности**. [Надежные и ненадежные биометрические данные](https://android-developers.googleblog.com/2018/06/better-biometrics-in-android-p.html) (откроется веб-сайт Android).
  - **По крайней мере числа**. Включает числовые символы, например `123456789`.
  - **Числовой комплекс**. Не допускаются комбинации из повторяющихся или идущих подряд цифр, такие как 1111 или 1234. Прежде чем назначить этот параметр целевым устройствам, убедитесь, что на них используется последняя версия приложения "Корпоративный портал".

    Если задано значение **Числовой комплекс** и вы назначаете параметр устройствам с версией Android до 5.0, применяется следующее поведение:

    - Если приложение "Корпоративный портал" работает с версией, предшествующей 1704, то политика в отношении PIN-кодов не будет применена к устройствам и в Центре администрирования Microsoft Endpoint Manager появится ошибка.
    - Если приложение корпоративного портала работает с версией 1704 или более поздней, могут применяться только простые ПИН-коды. Версии Android, предшествующие 5.0, не поддерживают этот параметр. Никакие ошибки не отображаются в центре администрирования Microsoft Endpoint Manager.

  - **Минимальный буквенный**. Включает буквы алфавита. Цифры и символы не требуются.
  - **Минимальный буквенно-цифровой**. Включает прописные буквы, строчные буквы и цифровые символы.
  - **Минимальный буквенно-цифровой и символьный**. Включает прописные и строчные буквы, цифры, знаки пунктуации и символы.

- **Запретить использование предыдущих паролей**. С помощью этого параметра можно запретить пользователю применять использованные ранее пароли. Введите число предыдущих паролей, которые нельзя использовать повторно (1–24). Значение `5` означает, что в качестве нового пароля пользователь не может установить свой текущий или любой из четырех предыдущих паролей. Если значение не указано, Intune не изменяет или не обновляет этот параметр.
- **Разблокировка по отпечатку пальца (только Samsung Knox)** . Значение **Блокировать** запрещает использование отпечатка пальца для разблокировки устройств. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить пользователям разблокировать устройства с помощью отпечатка пальца.
- **Smart Lock и другие доверенные агенты**. Значение **Блокировать** запрещает Smart Lock и другим доверенным агентам изменять настройки параметров экрана блокировки. Если устройство находится в надежном расположении, эта функция, которую также называют доверенным агентом, позволяет отключать или обходить пароль блокировки экрана устройства. Например, используйте эту функцию, когда устройства подключены к определенному устройству Bluetooth или находятся рядом с NFC-тегом. С помощью этого параметра можно запретить пользователям настраивать функцию Smart Lock.

  Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр.

  Эта настройка применяется для:

  - Samsung KNOX Standard 5.0 и более поздней версии

- **Шифрование**. Выберите значение **Требовать**, чтобы шифровать файлы на мобильном устройстве. Не все устройства поддерживают шифрование. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. Чтобы настроить этот параметр и правильно сообщить о соответствии требованиям, также настройте следующие элементы:
  1. **Пароль**. Задайте значение **Требовать**.
  2. **Требуемый тип пароля**. Установите значение **По крайней мере числа**.
  3. **Минимальная длина пароля**. Установите как минимум значение `4`.

  > [!NOTE]
  > Если применяется политика шифрования, пользователям устройств Samsung Knox нужно задать 6-значный сложный пароль для секретного кода устройства.

## <a name="google-play-store"></a>Магазин Google Play

- **Магазин Google Play (только Samsung Knox)** . Выберите значение **Блокировать**, чтобы запретить пользователям доступ к магазину Google Play. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить доступ пользователей к Google Play на устройствах.

## <a name="restricted-apps"></a>Ограниченные приложения

Используйте эти параметры, чтобы разрешить или запретить установку конкретных приложений на устройствах. Эта функция поддерживается на устройствах Android и Samsung Knox Standard.

- **Не настроено** (по умолчанию). Intune не изменяет или не обновляет этот параметр.
- **Запрещенные приложения**. Указывает приложения, не управляемые Intune, которые пользователям запрещено устанавливать и запускать. Если пользователь установит приложение из этого списка, Intune сообщит вам об этом.
- **Утвержденные приложения**. Указывает приложения, которые пользователям разрешено устанавливать. Для сохранения совместимости пользователям не следует устанавливать другие приложения.  Приложения под управлением Intune автоматически разрешены, включая приложение Корпоративного портала.
- **Список приложений**. **Добавление** собственного приложения.
  - **Идентификатор пакета приложений**. Введите идентификатор пакета приложения.
  - **URL в App Store**. Введите URL-адрес Google Play Маркет для выбранного приложения. Например, чтобы добавить приложение "Удаленный рабочий стол (Майкрософт)" для Android, введите `https://play.google.com/store/apps/details?id=com.microsoft.rdc.android`.

    Чтобы найти URL-адрес приложения, откройте[Google Play Маркет](https://play.google.com/store/apps) и найдите это приложение. Например, выполните поиск по фразе `Microsoft Remote Desktop Play Store` или `Microsoft Planner`. Выберите приложение и скопируйте URL-адрес.
  
  - **Имя приложения**. Введите нужное имя. Это имя видят пользователи.
  - **Издатель** (необязательно). Укажите издателя приложения, например `Microsoft`.

Вы также можете **Импортировать** CSV-файл с подробными сведениями о приложении, включая URL-адрес. Укажите сведения в таком формате <*URL-адрес приложения*>, <*имя приложения*>, <*издатель приложения*>. Или **экспортируйте** существующий список ограниченных приложений в том же формате.

> [!IMPORTANT]
> Профили устройств, в которых настроены параметры ограничения приложений, следует назначить группам пользователей, а не группам устройств.

## <a name="browser"></a>Браузер

- **Браузер (только Samsung Knox)** . Выберите значение **Блокировать**, чтобы запретить использование веб-браузера по умолчанию на устройстве. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить использование веб-браузера по умолчанию на устройстве.
- **Автозаполнение (только Samsung Knox)** . Значение **Блокировать** запрещает автоматическое заполнение в браузере. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить автозаполнение.
- **Файлы cookie (только Samsung Knox)** . Выберите способ обработки файлов cookie с веб-сайтов на устройствах. Доступны следующие параметры:
  - Allow
  - Блокировать все файлы cookie.
  - разрешить файлы cookie с посещенных веб-сайтов;
  - разрешить файлы cookie с текущего веб-сайта.
- **JavaScript (только Samsung Knox)** . Значение **Блокировать** запрещает выполнять скрипты JavaScript в браузере. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить эти скрипты.
- **Всплывающие окна (только Samsung Knox)** . Значение **Блокировать** включает блокировку всплывающих окон, чтобы запретить их отображение в веб-браузере. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить всплывающие окна.

## <a name="allow-or-block-apps"></a>Разрешение или блокировка приложений

Используйте эти параметры, чтобы включить, заблокировать или скрыть приложения на устройствах Samsung Knox Standard. Пользователи не могут запускать скрытые приложения.

Доступны следующие параметры:

- **Приложения, которые можно устанавливать (только на стандартных устройствах Samsung KNOX)** . Добавьте приложения, которые пользователи могут устанавливать. Пользователи не могут устанавливать приложения, которых нет в списке.
- **Приложения, которые запрещено запускать (только на стандартных устройствах Samsung KNOX)** . Укажите приложения, которые пользователям запрещено запускать на устройстве.
- **Приложения, скрытые от пользователя (только на стандартных устройствах Samsung KNOX)** . Укажите приложения, которые скрыты на устройствах. Пользователи не могут обнаруживать или запускать эти приложения.

Для каждого параметра добавьте приложения:

- **Добавить приложения по имени пакета**. Введите имя приложения и имя пакета приложения. В основном используется для бизнес-приложений. 
- **Добавить приложения по URL-адресу**. Введите имя и URL-адрес приложения из магазина Google Play.
- **Добавить приложение магазина**. Выберите приложение из существующего списка приложений, которыми вы управляете в Intune.

## <a name="cloud-and-storage"></a>Облако и хранилище

- **Архивация Google (только Samsung Knox)** . Значение **Блокировать** запрещает устройствам синхронизироваться с резервной копией Google. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить использовать резервную копию Google.
- **Автоматическая синхронизация учетной записи Google (только Samsung Knox)** . Выберите значение **Блокировать**, чтобы запретить автоматическую синхронизацию для учетной записи Google на устройствах. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить автоматическую синхронизацию параметров учетной записи Google.
- **Съемные носители (только Samsung Knox)** . Значение **Блокировать** запрещает устройствам использовать съемные носители. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить устройствам использовать съемные носители, например SD-карты.
- **Шифрование карт памяти (только Samsung Knox)** . Задайте значение **Требовать**, чтобы принудительно шифровать карты памяти. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может использовать незашифрованные карты памяти. Не все устройства поддерживают шифрование карт памяти. Для проверки обратитесь к изготовителю устройства.

## <a name="cellular-and-connectivity"></a>Сотовая сеть и подключение

- **Передача данных в роуминге (только Samsung Knox)** . Значение **Блокировать** запрещает передачу данных в роуминге по сети мобильной связи. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить роуминг данных.
- **Обмен сообщениями SMS или MMS (только Samsung Knox)** . Значение **Блокировать** запрещает текстовые сообщения на устройствах. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить использовать SMS и MMS-сообщения.
- **Голосовой набор (только Samsung Knox)** . Значение **Блокировать** запрещает пользователям использовать голосовой набор на устройствах. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить использовать голосовой набор.
- **Голосовой роуминг (только Samsung Knox)** . Значение **Блокировать** запрещает голосовой набор в роуминге по сети мобильной связи. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить использовать голосовой роуминг.
- **Bluetooth (только Samsung Knox)** . Выберите значение **Блокировать**, чтобы запретить использование Bluetooth на устройствах. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить использовать Bluetooth.
- **NFC (только Samsung Knox)** . Значение **Блокировать** отключает операции, которые используют NFC на устройствах, поддерживающих эту технологию. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить операции через NFC.
- **Wi-Fi (только Samsung Knox)** . Значение **Блокировать** запрещает использование Wi-Fi на устройствах. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить использовать Wi-Fi.
- **Модем Wi-Fi (только Samsung Knox)** . Значение **Блокировать** запрещает использование модема Wi-Fi на устройствах. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить использовать модем Wi-Fi.

## <a name="kiosk"></a>Киоск

Параметры киоска применимы только к устройствам Samsung KNOX Standard и приложениям, которые управляются с помощью Intune.

- Добавьте приложения, которые нужно запустить, когда устройство будет в режиме киоска. В режиме киоска запускаются только те приложения, которые вы добавили. Другие приложения не запускаются. Предварительно установленные браузеры не запускаются как приложения, когда устройство находится в режиме киоска. Если требуется браузер, попробуйте использовать [Managed Browser](../apps/app-configuration-managed-browser.md).

  Доступны такие параметры приложений:

  - **Добавить приложения по имени пакета**. В основном используется для бизнес-приложений. Введите имя приложения и имя пакета приложения.
  - **Добавить приложения по URL-адресу**. Введите имя и URL-адрес приложения из магазина Google Play.
  - **Добавить приложение магазина**. Выберите приложение из существующего списка приложений, которыми вы управляете в Intune.

- **Кнопка спящего режима экрана**. Значение **Блокировать** запрещает или скрывает кнопку спящего режима экрана. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить кнопку пробуждения из спящего режима экрана на устройствах.
- **Кнопки громкости**. Выберите значение **Блокировать**, чтобы запретить изменение громкости, отключив кнопки громкости. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить использование кнопок громкости на устройствах.

## <a name="next-steps"></a>Дальнейшие шаги

[Назначьте профиль](device-profile-assign.md) и [отслеживайте его состояние](device-profile-monitor.md).

Вы также можете создать профили киоска для устройств [Android для бизнеса](device-restrictions-android-for-work.md#dedicated-devices) и [Windows 10](kiosk-settings.md).
