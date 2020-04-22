---
title: Защита данных и инфраструктуры сайтов
titleSuffix: Configuration Manager
description: Узнайте, как защитить ресурсы организации от раскрытия или вредоносных атак с помощью Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 2117f786-d521-4790-9e8d-ec096c63c9d7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 381f9d190b1d73bbbab6142fd9587e881d0870ce
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708602"
---
# <a name="protect-data-and-site-infrastructure"></a>Защита данных и инфраструктуры сайтов

*Область применения: Configuration Manager (Current Branch)*

Вы хотите, чтобы пользователи могли безопасно получать доступ к ресурсам Организации. Защитите инфраструктуру и данные от уязвимостей или вредоносной атаки. Используйте Configuration Manager для обеспечения доступа и защиты ресурсов организации.  

- [Endpoint Protection](../deploy-use/endpoint-protection.md) позволяет управлять следующими политиками защитника Майкрософт для клиентских компьютеров:

  - Антивредоносная программа в Microsoft Defender
  - Брандмауэр в Microsoft Defender
  - Advanced Threat Protection в Microsoft Defender
  - Exploit Guard в Microsoft Defender
  - Application Guard в Microsoft Defender
  - Управление приложениями в Microsoft Defender

  > [!TIP]
  > Для управления защитой конечных точек на совместно управляемых устройствах Windows 10 с помощью облачной службы Microsoft Endpoint Manager переключите [рабочую нагрузку **Endpoint Protection**](../../comanage/workloads.md#endpoint-protection) на Intune. Дополнительные сведения см. в статье [Защита конечных точек для Microsoft Intune](https://docs.microsoft.com/intune/endpoint-protection-windows-10).

- Защита данных, хранящихся на локальных клиентах Windows, с помощью шифрования диска BitLocker (BDE). Configuration Manager обеспечивает полное управление жизненным циклом BitLocker, которое может заменить администрирование и мониторинг Microsoft BitLocker (MBAM). Дополнительные сведения см. в статье [Планирование управления BitLocker](../plan-design/bitlocker-management.md).

- Вместо традиционных паролей включите альтернативные методы входа на устройствах Windows 10 с помощью Windows Hello для бизнеса. Дополнительные сведения см. в статье [Параметры Windows Hello для бизнеса в System Center Configuration Manager](../deploy-use/windows-hello-for-business-settings.md).

- Сведите к минимуму усилия пользователей для подключения к ресурсам, включив VPN-подключение с использованием профилей VPN. Дополнительные сведения см. в статье [Профили VPN](../deploy-use/vpn-profiles.md).  

- Профили Wi-Fi предоставляют набор средств и ресурсов, помогающих управлять параметрами беспроводной сети на устройствах в организации. Развертывание этих параметров упрощает подключение пользователей к беспроводным сетям. Подробные сведения см. в статье [Create Wi-Fi profiles](../deploy-use/create-wifi-profiles.md) (Создание профилей Wi-Fi).  

- Подготавливайте устройства с помощью сертификатов, необходимых пользователям для подключения к ресурсам. Дополнительные сведения см. в разделе [Профили сертификатов](../deploy-use/introduction-to-certificate-profiles.md).  
