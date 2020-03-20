---
title: Добавление параметров файла предпочтений на устройства macOS в Microsoft Intune в Azure | Документация Майкрософт
titleSuffix: ''
description: Вы можете добавить XML- или PLIS-файл, который содержит сведения о ключах для вашего приложения. Используйте профиль конфигурации устройства для файла предпочтений, чтобы изменить сведения о ключах в файле списка свойств и назначить файл устройствам с macOS.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 01/09/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d226888c3d710a7b80357ebb92130b34ab2fef94
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/13/2020
ms.locfileid: "79360760"
---
# <a name="add-a-property-list-file-to-macos-devices-using-microsoft-intune"></a>Добавление файла списка свойств на устройства с macOS с помощью Microsoft Intune

С помощью Microsoft Intune можно добавить файл списка свойств (PLIST-файл) на устройства macOS или в приложения на устройствах macOS.

Данная функция применяется к:

- устройства macOS версии 10.7 и новее

Файлы списка свойств обычно содержат сведения о приложениях macOS. Дополнительные сведения см. в документах о [файлах списков свойств](https://developer.apple.com/library/archive/documentation/General/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html) (на веб-сайте Apple) и [пользовательских параметрах полезных данных](https://support.apple.com/guide/mdm/custom-mdm9abbdbe7/1/web/1).

В этой статье перечислены и описаны различные параметры файла списка свойств, которые можно добавить на устройства с macOS. Используйте эти параметры как часть решения управления мобильными устройствами (MDM), чтобы добавить идентификатор пакета приложения (`com.company.application`) и его PLIST-файл.

Эти параметры можно добавить в профиль конфигурации устройства в Intune, а затем назначить или развернуть на устройствах c macOS.

## <a name="before-you-begin"></a>Подготовка к работе

[Создайте профиль](device-profile-create.md).

## <a name="what-you-need-to-know"></a>Что необходимо знать

- Эти параметры не проверяются. Обязательно протестируйте изменения перед назначением профиля устройствам.
- Если вы не знаете, как ввести ключ приложения, измените параметр в приложении. Затем с помощью [Xcode](https://developer.apple.com/xcode/) просмотрите файл настроек приложения, чтобы увидеть, как настроен этот параметр. Компания Apple рекомендует удалить неуправляемые параметры с помощью Xcode перед импортом файла.
- Управляемые параметры используются только в некоторых приложениях, и эти приложения могут не позволить управлять всеми параметрами.
- Не забудьте отправить файлы списков свойств, которые предназначены для параметров канала устройств, а не параметров канала пользователей. Файлы списков свойств применяются для всего устройства.

## <a name="preference-file"></a>Файл предпочтений

- **Предпочитаемое имя домена**. Как правило, файлы списков свойств используются для веб-браузеров (Microsoft Edge), [Advanced Threat Protection в Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) и пользовательских приложений. При создании домена предпочтений также создается идентификатор пакета. Введите идентификатор пакета, например `com.company.application`. Например, введите `com.Contoso.applicationName`, `com.Microsoft.Edge` или `com.microsoft.wdav`.
- **Файл списка свойств**. Выберите файл списка свойств, связанный с вашим приложением. Это должен быть файл `.plist` или `.xml`. Например, отправьте файл `YourApp-Manifest.plist` или `YourApp-Manifest.xml`.
- **Содержимое файла**. В файле списка свойств содержатся сведения о ключах. Чтобы изменить эти сведения, откройте файл списка в другом редакторе, а затем повторно отправьте файл в Intune.

Убедитесь, что файл имеет правильный формат. В файле должны содержаться только пары "ключ-значение", которые не должны быть заключены в теги `<dict>`, `<plist>`или `<xml>`. Например, файл списка свойств должен быть аналогичен следующему файлу:

```xml
<key>SomeKey</key>
<string>someString</string>
<key>AnotherKey</key>
<false/>
...
```

Щелкните **OK** > **Создать**, чтобы сохранить изменения. Созданный профиль отобразится в списке профилей.

## <a name="next-steps"></a>Дальнейшие шаги

Профиль создан, но он пока ничего не делает. Далее [назначьте профиль](device-profile-assign.md) и [отслеживайте его состояние](device-profile-monitor.md).

Дополнительные сведения о файлах предпочтений для Microsoft Edge см. в статье [Настройка параметров политики Microsoft Edge для macOS с помощью файла PLIST](https://docs.microsoft.com/deployedge/configure-microsoft-edge-on-mac).
