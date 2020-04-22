---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/13/2019
ms.openlocfilehash: b21365d0c355adab6819e13537c1b25316583ec2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704092"
---
<!-- ## Update and configure the .NET Framework to support TLS 1.2 Note: the heading in in the 2 articles (enable-tls-1-2-client & enable-tls-1-2-server) to better facilitate linking. -->

### <a name="determine-net-version"></a>Определение версии .NET

Сначала определите установленные версии .NET. Подробные сведения см. в статье [Как узнать, какие версии и пакеты обновления Microsoft .NET Framework установлены на компьютере](https://support.microsoft.com/help/318785/how-to-determine-which-versions-and-service-pack-levels-of-the-microso).

### <a name="install-net-updates"></a>Установка обновлений .NET

Установите обновления .NET, чтобы можно было включить криптостойкость. Некоторые версии .NET Framework могут потребовать обновления, чтобы обеспечить поддержку криптостойкости. Руководствуйтесь следующим:

- NET Framework 4.6.2 и более поздних версий поддерживает TLS 1.1 и TLS 1.2. Проверьте параметры реестра, но дополнительные изменения не требуются.

- Обновите NET Framework 4.6 и более ранних версий, чтобы обеспечить поддержку TLS 1.1 и TLS 1.2. Подробные сведения см. в статье [Версии и зависимости платформы .NET Framework](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies).

- Если вы используете .NET Framework 4.5.1 или 4.5.2 в Windows 8.1 или Windows Server 2012, важные обновления и подробные сведения можно найти в [Центре загрузки](https://www.microsoft.com/download/details.aspx?id=42883).


### <a name="configure-for-strong-cryptography"></a>Настройка криптостойкости

Настройте .NET Framework для поддержки криптостойкости. Задайте для параметра реестра `SchUseStrongCrypto` значение `DWORD:00000001`. Это приведет к отключению потока шифрования RC4 и потребует перезагрузки. Подробные сведения об этом параметре см. в статье [Microsoft Security Advisory 296038](https://docs.microsoft.com/security-updates/SecurityAdvisories/2015/2960358) (Советы корпорации Майкрософт по безопасности 296038).

Обязательно задайте указанные ниже разделы реестра на всех компьютерах, которые обмениваются данными по сети с системой, где включен протокол TLS 1.2. Например, это могут быть клиенты Configuration Manager, роли удаленной системы сайта, которые не установлены на сервере сайта, и сам сервер сайта.

Для 32-разрядных приложений, которые выполняются в 32-разрядных ОС, или 64-разрядных приложений, которые выполняются в 64-разрядных ОС, обновите следующее значение подраздела:

``` Registry
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v2.0.50727]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
```

Для 32-разрядных приложений, которые выполняются в 64-разрядных ОС, обновите следующее значение подраздела:

``` Registry
[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v2.0.50727]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
[HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.0.30319]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
```

> [!Note]  
> Параметр `SchUseStrongCrypto` позволяет .NET использовать TLS 1.1 и TLS 1.2. Параметр `SystemDefaultTlsVersions` позволяет .NET использовать конфигурацию ОС. Подробные сведения см. в статье [Рекомендации по использованию протокола TLS с .NET Framework](https://docs.microsoft.com/dotnet/framework/network-programming/tls).
