---
title: Профили VPN
titleSuffix: Configuration Manager
description: Узнайте, как использовать профили VPN в Configuration Manager, чтобы развернуть параметры VPN для пользователей в вашей организации.
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: c0f094f1-852e-4606-91db-97846d8f0772
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9463d857599e676da6267313df575c8881436f93
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706252"
---
# <a name="vpn-profiles-in-configuration-manager"></a>Профили VPN в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

<!--1283610-->
Чтобы развернуть параметры VPN для пользователей в вашей организации, используйте профили VPN в Configuration Manager. Развертывание этих параметров упрощает для конечного пользователя подключение к ресурсам в локальной сети.  

Например, представим, что вам нужно настроить параметры для подключения к общей папке во внутренней сети на всех устройствах с Windows 10. Создайте профиль VPN с параметрами, которые необходимы для подключения ко внутренней сети. Затем разверните этот профиль для всех пользователей, у которых есть устройства с Windows 10. Эти пользователи увидят VPN-подключение в списке доступных сетей и смогут с легкостью использовать его.

При создании профиля Wi-Fi можно указать большое число параметров безопасности. Они включают сертификаты для проверки сервера и проверки подлинности клиента, подготовленные с помощью профилей сертификатов в Configuration Manager. Дополнительные сведения см. в разделе [Профили сертификатов](introduction-to-certificate-profiles.md).

> [!Note]
> По умолчанию в Configuration Manager эта дополнительная функция отключена. Перед использованием ее необходимо включить. Дополнительные сведения см. в разделе [Включение дополнительных функций из обновлений](../../core/servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  

## <a name="supported-platforms"></a>Поддерживаемые платформы

В приведенной ниже таблице описываются профили VPN, которые можно настроить для различных платформ устройств.

|Тип подключения|Windows 8.1|Windows RT|Windows RT 8.1|быть под управлением ОС Windows 10;|
|---------------|-----------|----------|--------------|----------|
|**Pulse Secure**|Да|Нет|Да|Да|
|**F5 Edge Client**|Да|Нет|Да|Да|
|**Dell SonicWALL Mobile Connect**|Да|Нет|Да|Да|
|**Check Point Mobile VPN**|Да|Нет|Да|Да|
|**Microsoft SSL (SSTP)**|Да|Да|Да|Нет|
|**Microsoft Automatic**|Да|Да|Да|Нет|
|**IKEv2**|Да|Да|Да|Нет|
|**PPTP**|Да|Да|Да|Нет|
|**L2TP**|Да|Да|Да|Нет|

## <a name="next-step"></a>Дальнейшие действия

> [!div class="nextstepaction"]
> [Создание профилей VPN](create-vpn-profiles.md)

## <a name="see-also"></a>См. также

- [Необходимые условия для профилей VPN](../plan-design/prerequisites-for-wifi-vpn-profiles.md)

- [Безопасность и конфиденциальность профилей VPN](../plan-design/security-and-privacy-for-wifi-vpn-profiles.md)
