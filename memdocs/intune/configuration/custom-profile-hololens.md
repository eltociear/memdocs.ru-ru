---
title: Использование управления приложениями в Windows Defender на устройствах HoloLens 2 в Microsoft Intune — Azure | Документация Майкрософт
description: Настройте CSP для управления приложениями в Windows Defender (WDAC), чтобы разрешить или запретить открытие приложений на устройствах HoloLens 2 в Microsoft Intune. Используйте PowerShell и настраиваемый профиль конфигурации.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/20/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6d2d19b03253725bde7b0ee27f3c94b42adb5917
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990125"
---
# <a name="use-wdac-and-windows-powershell-to-allow-or-blocks-apps-on-hololens-2-devices-with-microsoft-intune"></a>Используйте WDAC и Windows PowerShell, чтобы разрешить или блокировать приложения на устройствах HoloLens 2 с помощью Microsoft Intune

Устройства Microsoft HoloLens 2 поддерживают [CSP управления приложениями в Windows Defender (WDAC)](https://docs.microsoft.com/windows/client-management/mdm/applicationcontrol-csp), который заменяет [CSP AppLocker](https://docs.microsoft.com/windows/client-management/mdm/applocker-csp).

Используя Windows PowerShell и Microsoft Intune, можно с помощью CSP WDAC разрешать или запрещать открытие конкретных приложений на устройствах Microsoft HoloLens 2. Например, вы можете разрешить или запретить открытие приложения Cortana на устройствах HoloLens 2 в своей организации.

Данная функция применяется к:

- устройствам HoloLens 2 под управлением Windows Holographic for Business

CSP WDAC построен на [функции управления приложениями в Windows Defender (WDAC)](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control). Вы также можете использовать [несколько политик WDAC](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/deploy-multiple-windows-defender-application-control-policies).

В этой статье показано, как:

1. создавать политики WDAC с помощью Windows PowerShell;
2. использовать Windows PowerShell для преобразования правил политики WDAC в XML, обновления XML, а затем преобразования XML в двоичный файл.
3. В Microsoft Intune создайте [настраиваемый профиль конфигурации устройства](custom-settings-windows-holographic.md), добавьте этот двоичный файл политики WDAC и примените политику к устройствам HoloLens 2.

В Intune необходимо создать настраиваемый профиль конфигурации, чтобы использовать CSP управления приложениями в Windows Defender (WDAC). 

Используйте действия, описанные в этой статье, в качестве шаблона, чтобы разрешать или запрещать открывать определенные приложения на устройствах HoloLens 2.

## <a name="prerequisites"></a>Предварительные условия

- Знание Windows PowerShell.
- Войдите в Intune в качестве:

  - члена роли Intune **Диспетчер политик и профилей** или **Администратор ролей Intune**

    ИЛИ

  - члена роли Azure AD**Глобальный администратор** или **Администратор службы Intune**

  Дополнительные сведения см. в разделе [Управление доступом на основе ролей (RBAC) с помощью Intune](../fundamentals/role-based-access-control.md).

- Создайте группу пользователей или устройств с вашими устройствами HoloLens 2. Дополнительные сведения см. в разделе [Группы пользователей и группы устройств](device-profile-assign.md#user-groups-vs-device-groups).

## <a name="example"></a>Пример

В этом примере с помощью Windows PowerShell создается политика управления приложениями Windows Defender (WDAC). Эта политика запрещает открывать определенные приложения. Затем с помощью Intune эта политика развертывается на устройствах HoloLens 2.

1. На своем настольном компьютере откройте приложение **Windows PowerShell**.
2. Получите сведения об установленном пакете приложения на вашем настольном компьютере:

    ```powershell
    $package1 = Get-AppxPackage -name *<applicationname>*
    ```

    Например, введите:

    ```powershell
    $package1 = Get-AppxPackage -name *cortana*
    ```

    Затем убедитесь, что пакет имеет атрибуты приложения:

    ```powershell
    $package1
    ```

    Вы должны увидеть атрибуты, подобные приведенным ниже.

    ```powershell
    Name              : Microsoft.Windows.Cortana
    Publisher         : CN=Microsoft Windows, O=Microsoft Corporation, L=Redmond, S=Washington, C=US
    Architecture      : Neutral
    ResourceId        : neutral
    Version           : 1.13.0.18362
    PackageFullName   : Microsoft.Windows.Cortana_1.13.0.18362_neutral_neutral_cw5n1h2txyewy
    InstallLocation   : C:\Windows\SystemApps\Microsoft.Windows.Cortana_cw5n1h2txyewy
    IsFramework       : False
    PackageFamilyName : Microsoft.Windows.Cortana_cw5n1h2txyewy
    PublisherId       : cw5n1h2txyewy
    IsResourcePackage : False
    IsBundle          : False
    IsDevelopmentMode : False
    NonRemovable      : True
    IsPartiallyStaged : False
    SignatureKind     : System
    Status            : Ok
    ```

3. Создайте политику WDAC и добавьте этот пакет приложения в правило DENY.

    ```powershell
    $rule = New-CIPolicyRule -Package $package1 -Deny
    ```

4. Повторите шаги 2 и 3 для всех остальных приложений, открытие которых вы хотите ЗАПРЕТИТЬ.

    ```powershell
    $rule += New-CIPolicyRule -Package $package<2..n> -Deny
    ```

    Например, введите:

    ```powershell
    $package2 = Get-AppxPackage -name *windowsstore*
    $rule += New-CIPolicyRule -Package $package<2..n>  -Deny
    ```

5. Преобразуйте политику WDAC в **newPolicy.xml**.

    ```powershell
    New-CIPolicy -rules $rule -f .\newPolicy.xml -UserPEs
    ```

    Чтобы учесть все версии приложения, убедитесь, что в файле newPolicy.xml `PackageVersion="65535.65535.65535.65535"` находится в узле Deny.

    ```xml
    <Deny ID="ID_DENY_D_1" FriendlyName="Microsoft.WindowsStore_8wekyb3d8bbwe FileRule" PackageFamilyName="Microsoft.WindowsStore_8wekyb3d8bbwe" PackageVersion="65535.65535.65535.65535" />
    ```

    Для `PackageFamilyNameRules` можно использовать следующие версии.

    - **Разрешить**. Введите `PackageVersion, 0.0.0.0`, что означает "Разрешить эту версию и все последующие".
    - **Запретить**. Введите `PackageVersion, 65535.65535.65535.65535`, что означает "Запретить эту версию и все предыдущие".

6. Объедините файл **newPolicy.xml** с политикой по умолчанию на своем настольном компьютере. Это действие создает файл **mergedPolicy.xml**. Например, разрешите выполнение подписанных драйверов Windows, WHQL и подписанных приложений Store.

    ```powershell
    Merge-CIPolicy -PolicyPaths .\newPolicy.xml,C:\Windows\Schemas\codeintegrity\examplepolicies\DefaultWindows_Audit.xml -o mergedPolicy.xml
    ```

7. Отключите правило **Режим аудита** в файле **mergedPolicy.xml**. После объединения режим аудита включается автоматически.

    ```powershell
    Set-RuleOption -o 3 -Delete .\mergedPolicy.xml
    ```

8. Включите правило **InvalidateEAs при перезагрузке** в файле **mergedPolicy.xml**.

    ```powershell
    Set-RuleOption -o 15 .\mergedPolicy.xml
    ```

    Дополнительные сведения об этих правилах см. в разделе [Общие сведения о правилах политики WDAC и о правилах файлов](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/select-types-of-rules-to-create).

9. Преобразуйте файл **mergedPolicy.xml** в двоичный формат. Это действие создает файл **compiledPolicy.bin**. Позднее вы добавите этот двоичный файл **compiledPolicy.bin** в Intune.

    ```powershell
    ConvertFrom-CIPolicy .\mergedPolicy.xml .\compiledPolicy.bin
    ```

10. Создайте в Intune настраиваемый профиль конфигурации устройства.

    1. В [центре администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) создайте настраиваемый профиль конфигурации устройства Windows 10.

        Конкретные действия см. в разделе [Создание настраиваемого профиля с помощью OMA-URI в Intune](custom-settings-configure.md).

    2. При создании профиля введите следующие параметры.

      - **OMA-URI**: Введите `./Vendor/MSFT/ApplicationControl/Policies/<PolicyGUID>`. Замените `<PolicyGUID>` узлом PolicyTypeID в файле **mergedPolicy.xml**, созданном на шаге 6.

        Используя наш пример, введите `./Vendor/MSFT/ApplicationControl/Policies/A244370E-44C9-4C06-B551-F6016E563076`.

        Идентификатор GUID политики **должен соответствовать** узлу PolicyTypeID в файле **mergedPolicy.xml** (созданном на шаге 6).

      - **Тип данных**. Установите **файл Base64**. Файл будет автоматически преобразован из двоичного в base64.
      - **Файл сертификата**. Отправьте двоичный файл **compiledPolicy.bin** (созданный на шаге 9).

      Ваши настройки будут выглядеть следующим образом:

      :::image type="content" source="./media/custom-profile-hololens/custom-applicationcontrol-omauri.png" alt-text="Добавьте настраиваемый OMA-URI для настройки CSP ApplicationControl в Microsoft Intune.":::

11. Когда профиль будет [назначен](device-profile-assign.md) вашей группе устройств HoloLens 2, проверьте состояние профиля. После успешного применения профиля перезагрузите устройства HoloLens 2.

## <a name="next-steps"></a>Дальнейшие шаги

[Назначение профиля](device-profile-assign.md) и [отслеживание его состояния](device-profile-monitor.md).

[Узнайте больше о настраиваемых профилях в Intune](custom-settings-configure.md).
