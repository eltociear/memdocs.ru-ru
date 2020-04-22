---
title: Включение TLS 1.2 на клиентах
titleSuffix: Configuration Manager
description: В этой статье описано, как включить TLS 1.2 для клиентов Configuration Manager.
ms.date: 12/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5b094a02-a425-4b67-81d3-8455e4265512
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e5b525da4a58240b34c30403db618ea0d2ca85f1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704112"
---
# <a name="how-to-enable-tls-12-on-clients"></a>Включение TLS 1.2 на клиентах

*Область применения: Configuration Manager (Current Branch)*

При включении TLS 1.2 для среды Configuration Manager сначала убедитесь, что клиенты поддерживают TLS 1.2 и правильно настроены для использования этого протокола, прежде чем включать TLS 1.2 и отключать старые протоколы на серверах сайта и удаленных системах сайта. Необходимо выполнить три действия, чтобы включить TLS 1.2 на клиентах:

- Обновление Windows и WinHTTP
- Убедитесь, что TLS 1.2 включен в качестве протокола для SChannel на уровне операционной системы
- Обновите и настройте .NET Framework для поддержки TLS 1.2

Дополнительные сведения о зависимостях для конкретных компонентов и сценариев Configuration Manager см. в разделе [о включении TLS 1.2](enable-tls-1-2.md).

## <a name="update-windows-and-winhttp"></a><a name="bkmk_winhttp"></a> Обновление Windows и WinHTTP

Windows 8.1, Windows Server 2012 R2, Windows 10, Windows Server 2016 и более поздние версии Windows изначально поддерживают TLS 1.2 для обмена данными между клиентом и сервером через WinHTTP. 

В ранних версиях Windows, например Windows 7 или Windows Server 2012, протокол TLS 1.1 или 1.2 не включен по умолчанию для безопасного обмена данными с помощью WinHTTP. Для этих более ранних версий Windows установите [обновление 3140245](https://support.microsoft.com/help/3140245), чтобы включить значение реестра ниже, которое можно задать для добавления TLS 1.1 и 1.2 в список безопасных протоколов по умолчанию для WinHTTP. После установки исправления создайте следующие параметры реестра:

> [!IMPORTANT]
> Включите эти параметры на всех клиентах, использующих более ранние версии Windows, *прежде*, чем включить TLS 1.2 и отключить старые протоколы на серверах Configuration Manager. В противном случае вы можете непреднамеренно потерять связь с клиентами.

Проверьте значение параметра реестра `DefaultSecureProtocols`, например:

``` Registry
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Internet Settings\WinHttp\
      DefaultSecureProtocols = (DWORD): 0xAA0
HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Internet Settings\WinHttp\
      DefaultSecureProtocols = (DWORD): 0xAA0
```

Если вы изменили это значение, перезагрузите компьютер.

В предыдущем примере для параметра WinHTTP `DefaultSecureProtocols` используется значение `0xAA0`. В статье [KB 3140245: обновление для включения TLS 1.1 и TLS 1.2 в качестве безопасных протоколов по умолчанию в WinHTTP в Windows](https://support.microsoft.com/help/3140245) указано шестнадцатеричное значение для каждого протокола. По умолчанию в Windows используется значение `0x0A0`, чтобы можно было включить SSL 3.0 и TLS 1.0 для WinHTTP. В примере выше сохраняются такие значения по умолчанию и также включаются TLS 1.1 и TLS 1.2 для WinHTTP. Такая конфигурация гарантирует, что изменение не нарушит работу приложений, которые все еще могут использовать SSL 3.0 или TLS 1.0. Вы можете использовать значение `0xA00`, чтобы включить только TLS 1.1 и TLS 1.2. Configuration Manager поддерживает самый безопасный протокол, который согласовывается Windows для двух устройств.

 Если вы хотите полностью отключить SSL 3.0 и TLS 1.0, сделайте это с помощью параметров для отключения протоколов SChannel в Windows. Подробные сведения см. в статье [How to restrict the use of certain cryptographic algorithms and protocols in Schannel.dll](https://support.microsoft.com/help/245030/how-to-restrict-the-use-of-certain-cryptographic-algorithms-and-protoc) (Как ограничить использование определенных алгоритмов шифрования и протоколов в Schannel.dll).

## <a name="ensure-that-tls-12-is-enabled-as-a-protocol-for-schannel-at-the-operating-system-level"></a><a name="bkmk_protocol"></a> Убедитесь, что TLS 1.2 включен в качестве протокола для SChannel на уровне операционной системы

[!INCLUDE [Enable TLS 1.2 protocol as a security provider](includes/enable-tls-1-2-protocol-security-provider.md)]

## <a name="update-and-configure-the-net-framework-to-support-tls-12"></a><a name="bkmk_net"></a> Обновите и настройте .NET Framework для поддержки TLS 1.2

[!INCLUDE [Update and configure the .NET framework to support TLS 1.2](includes/update-net-framework-to-support-tls-1-2.md)]


## <a name="next-steps"></a>Дальнейшие шаги

- [Включение TLS 1.2 на серверах сайта и удаленных системах сайта](enable-tls-1-2-server.md)
- [Распространенные проблемы при включении TLS 1.2](enable-tls-1-2-troubleshoot.md)

