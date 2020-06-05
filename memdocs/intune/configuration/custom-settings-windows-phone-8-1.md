---
title: Добавление настраиваемых параметров Microsoft Intune для устройств Windows Phone 8.1 в Azure | Документация Майкрософт
titleSuffix: ''
description: Добавьте или создайте настраиваемый профиль для использования параметров OMA-URI для устройств под управлением Windows Phone 8.1 в Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ce8433ee87c0f5e4b397003b78c0ceb751eb46b7
ms.sourcegitcommit: 169e279ba686c28d9a23bc0a54f0a2a0d20bdee4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2020
ms.locfileid: "83556274"
---
# <a name="use-custom-settings-for-windows-phone-81-devices-in-intune"></a>Использование настраиваемых параметров для устройств с Windows Phone 8.1 в Intune

Microsoft Intune позволяет добавить или создать настраиваемые параметры для ваших устройств Windows Phone 8.1 с помощью настраиваемых профилей. Настраиваемые профили являются компонентом Intune. Они предназначены для добавления параметров и функций устройств, которые не встроены в Intune.

В настраиваемых профилях Windows Phone 8.1 используются параметры OMA-URI для настройки различных функций. Эти параметры обычно используются производителями мобильного устройства для управления функциями на устройстве. Список параметров представлен в [документации по протоколу MDM в Windows Phone 8.1](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-phone/dn499787(v=technet.10)).

Эта статья описывает создание настраиваемого профиля для устройств Windows Phone 8.1. 

## <a name="before-you-begin"></a>Подготовка к работе

[Создайте настраиваемый профиль Windows Phone 8.1](custom-settings-configure.md).

## <a name="custom-oma-uri-settings"></a>Настраиваемые параметры OMA-URI

- **Параметры OMA-URI**: **Добавьте** следующие параметры:

  - **Имя** — Введите уникальное имя для параметра OMA-URI, чтобы его было проще найти в списке параметров.
  - **Описание**. Укажите в описании общие сведения о параметре и актуальную информацию о расположении профиля.
  - **OMA-URI** (с учетом регистра): введите код OMA-URI, для которого нужно указать параметр.
  - **Тип данных**. Выберите тип данных для этого параметра OMA-URI. Доступны следующие параметры:

    - Строка
    - Строка (XML-файл)
    - Дата и время
    - Целое число
    - Число с плавающей запятой
    - Логическое значение
    - Base64 (файл)

  - **Значение**: введите значение данных, которое нужно сопоставить с указанным OMA-URI. Значение зависит от выбранного типа данных. Например, если вы выбрали **Дата и время**, выберите значение из управляющего элемента выбора даты.

  После добавления нескольких параметров можно выбрать **Экспорт**. Элемент **Экспорт** создает список всех добавленных значений в файле с разделителями-запятыми (CSV).

## <a name="example"></a>Пример

В следующем примере устройствам Windows 8.1 запрещено изменять сети сотовой связи за пределами зоны действия сети оператора.

- **Имя** — Разрешить передачу данных в роуминге
- **Описание**. Разрешить или запретить передачу данных в роуминге
- **OMA-URI** (с учетом регистра): ./Vendor/MSFT/PolicyManager/My/Connectivity/AllowCellularDataRoaming
- **Тип данных**. Целое число
- **Значение**. 0

## <a name="next-steps"></a>Дальнейшие шаги

[Назначение профиля](device-profile-assign.md) и [отслеживание его состояния](device-profile-monitor.md).

Создайте [настраиваемый профиль на устройствах с Windows 10](custom-settings-windows-10.md).
