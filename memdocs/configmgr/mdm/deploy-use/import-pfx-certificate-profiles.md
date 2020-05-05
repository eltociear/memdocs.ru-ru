---
title: Импорт профилей сертификатов PFX
titleSuffix: Configuration Manager
description: Узнайте, как использовать PFX-файлы в Configuration Manager для создания пользовательских сертификатов, поддерживающих обмен зашифрованными данными.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e3bb3e13-3037-4122-93bc-504bfd080a4d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7f72dcba7e7f1e3af0bf168ca83deb958094879a
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724598"
---
# <a name="import-pfx-certificate-profiles"></a>Импорт профилей сертификатов PFX

*Область применения: Configuration Manager (Current Branch)*

Узнайте, как создать профиль сертификата, импортировав учетные данные из внешних сертификатов. В этой статье описываются конкретные сведения о профилях сертификатов для обмена личной информацией (PFX). Дополнительные сведения о создании и настройке этих профилей см. в разделе [Профили сертификатов](../../protect/deploy-use/introduction-to-certificate-profiles.md).

Configuration Manager поддерживает различные типы хранилищ сертификатов для различных устройств и версий ОС. Например, Windows 10 и Windows 10 Mobile. Дополнительные сведения см. в статье [Предварительные требования для профиля сертификата](../../protect/plan-design/prerequisites-for-certificate-profiles.md).

Используйте Configuration Manager, чтобы импортировать учетные данные сертификата и затем подготавливать PFX-файлы на устройствах. Эти файлы можно использовать для создания пользовательских сертификатов для поддержки обмена зашифрованными данными.

> [!TIP]  
> Пошаговое руководство по этому процессу см. в записи блога [Создание и развертывание профилей сертификатов PFX в Configuration Manager](https://blogs.technet.microsoft.com/karanrustagi/2015/09/01/how-to-create-and-deploy-pfx-certificate-profiles-in-configuration-manager/).  

## <a name="create-a-profile"></a>Создание профиля

1. В консоли Configuration Manager перейдите в рабочую область **активы и соответствие** , разверните узел **Параметры соответствия**, а затем — **доступ к ресурсам компании**, а затем выберите **Профили сертификатов**.

1. На вкладке ленты **Главная** в группе **Создать** выберите **Создать профиль сертификата**.

1. На странице **Общие** **мастера создания профиля сертификата**укажите следующие сведения.  

    - **Имя**: введите уникальное имя для профиля сертификата. Можно использовать не более 256 символов.  

    - **Описание**: введите описание, которое содержит обзор профиля сертификата, помогающего опознать его в консоли Configuration Manager. Можно использовать не более 256 символов.  

1. Выберите **файл обмена личной информацией — параметры PKCS #12 (PFX) — импорт**. Этот параметр позволяет импортировать сведения из существующего сертификата для создания профиля сертификата.

    > [!NOTE]
    > Параметр **создать** запрашивает сертификат от имени пользователя из подключенного локального центра сертификации (ЦС). Этот процесс затем безопасно доставляет сертификаты клиентам в виде PFX-файлов. Дополнительные сведения см. [в статье Создание профилей сертификатов PFX с помощью центра сертификации](create-pfx-certificate-profiles.md).

1. На странице **PFX-сертификат** **мастера создания профиля сертификата**укажите поставщика хранилища ключей устройств (KSP):

    - **Установить в доверенный платформенный модуль (TPM) при его наличии**  
    - **Установка в доверенный платформенный модуль (TPM) (TPM) в ином случае завершается сбоем**
    - **Установить в Windows Hello для бизнеса в ином случае не удалось**
    - **Установить в поставщик хранилища ключей программного обеспечения**

1. На странице **Поддерживаемые платформы** Выберите поддерживаемые платформы устройств.

1. Завершите работу мастера.

## <a name="deploy-the-profile"></a>Развертывание профиля

После создания и инициализации профиля сертификата он будет доступен в узле **Профили сертификатов** . Дополнительные сведения о развертывании см. в разделе [развертывание профилей доступа к ресурсам](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md).

## <a name="assign-primary-users"></a>Назначение основных пользователей

Назначьте конечных пользователей в качестве основных пользователей на устройствах Windows 10, где необходимо установить сертификаты PFX. Дополнительные сведения см. в разделе [Сопоставление пользователей и устройств](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).

## <a name="provision-a-create-pfx-script"></a>Подготавливает скрипт создания PFX

Чтобы импортировать PFX-сертификат, выполните следующие командлеты Configuration Manager PowerShell, чтобы создать сценарий PFX.

- [Get-Кмклиентцертификатепфкс](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmclientcertificatepfx?view=sccm-ps)
- [Import-Кмклиентцертификатепфкс](https://docs.microsoft.com/powershell/module/configurationmanager/import-cmclientcertificatepfx?view=sccm-ps)
- [Remove-Кмклиентцертификатепфкс](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmclientcertificatepfx?view=sccm-ps)

### <a name="example-script"></a>Пример сценария

Чтобы подготавливать PFX-файл к профилю сертификата для пользователя, откройте PowerShell на компьютере с консолью Configuration Manager. Измените переменные значениями из среды.

``` PowerShell
# The display name of your PFX Import certificate profile
$PfxProfileDisplayName = "ImportPFX"

# The password you used to protect/encrypt the external PFX file that was created/exported from your certificate storage provider
# If you omit this password, PowerShell will securely prompt you for it. You can specify it as a parameter for process automation.
$password = ""

# The username of the user who will receive this PFX certificate on their device
$user = "Melissa"

# The full path to the PFX file you exported from the certificate store
$pfxfile = "c:\p1.pfx"

# If the target user isn't in the same domain as the user running this script, specify a different domain
Import-CMClientCertificatePfx -UserName "$env:USERDOMAIN\$user" -Password (ConvertTo-SecureString -String $password -AsPlainText -Force) -CertificateProfilePfx (Get-CMCertificateProfilePfx -Fast -Name $PfxProfileDisplayName) -Path $pfxfile
```

## <a name="see-also"></a>См. также

[Создание нового профиля сертификата](../../protect/deploy-use/create-certificate-profiles.md)

[Создание профилей сертификатов PFX с помощью центра сертификации](create-pfx-certificate-profiles.md)

[Развертывание профилей Wi-Fi, VPN, электронной почты и сертификатов](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md)
