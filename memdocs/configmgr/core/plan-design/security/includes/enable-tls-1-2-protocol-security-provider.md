---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/13/2019
ms.openlocfilehash: 08cebf6ef844e1854daa9444462f4c4470319186
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704082"
---
<!--## Enable Transport layer security (TLS) 1.2 protocol as a security provider Note: the heading in in the 2 articles (enable-tls-1-2-client & enable-tls-1-2-server) to better facilitate linking. -->

Протокол TLS 1.2 включен по умолчанию, поэтому менять эти разделы не нужно. Вы можете внести изменения в `Protocols`, чтобы отключить протоколы TLS 1.0 и TLS 1.1 после того, как выполнили все другие инструкции в этой статье и убедились, что в среде работает только TLS 1.2.

Проверьте параметр подраздела реестра `\SecurityProviders\SCHANNEL\Protocols`, как описано в разделе [Настройка безопасности в реестре Windows](https://docs.microsoft.com/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry).

