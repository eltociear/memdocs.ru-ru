---
title: Конечные точки сети для развертываний в государственных организациях США — Microsoft Intune
titleSuffix: ''
description: Просмотрите конечные точки для государственных организаций США для Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/30/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 5f6682cb-5fcd-4018-b7f7-71768ad3152e
ms.reviewer: kerimh
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: d1574e07ca58debaef5bbc134a86d76aa21778a3
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347268"
---
# <a name="us-government-endpoints-for-microsoft-intune"></a>Конечные точки для государственных организаций США для Microsoft Intune

На этой странице перечислены конечные точки для государственных организаций США, необходимые для параметров прокси-сервера в развертываниях Intune.

Для управления устройствами, защищенными брандмауэрами и прокси-серверами, нужно включить возможность обмена данными с Intune.

- Прокси-сервер должен поддерживать протоколы **HTTP (80)** и **HTTPS (443)** , так как клиенты Intune используют оба этих протокола.
- Для некоторых задач (например, скачивание программного обеспечения и обновлений) Intune требуется доступ к manage.microsoft.com через прокси-сервер без проверки подлинности.

Параметры прокси-сервера можно изменить на отдельных клиентских компьютерах. Кроме того, с помощью параметров групповой политики можно изменить параметры для всех клиентских компьютеров, защищенных указанным прокси-сервером.

Управляемые устройства должны иметь конфигурации с выбранным параметром **Все пользователи**, чтобы все пользователи могли получать доступ к службам через брандмауэры.

Дополнительные сведения об автоматической регистрации и регистрации устройств Windows 10 для государственных организаций США см. в статье о [настройке регистрации для устройств с Windows](../enrollment/windows-enroll.md#windows-10-auto-enrollment-and-device-registration).

В приведенной ниже таблице перечислены порты и службы, к которым обращается клиент Intune.

|**Конечная точка**|**IP-адрес**|
|---------------------|-----------|
|*.manage.microsoft.us | 52.243.26.209 <br> 52.247.173.11 <br> 52.227.183.12 <br>52.227.180.205 <br> 52.227.178.107 <br> 13.72.185.168 <br> 52.227.173.179 <br> 52.227.175.242 <br> 13.72.39.209 <br> 52.243.26.209 <br> 52.247.173.11 |
| enterpriseregistration.microsoftonline.us | 13.72.188.239 <br> 13.72.55.179 |

## <a name="us-government-customer-designated-endpoints"></a>Конечные точки для государственных организаций США, назначенные клиентом:
- Портал Azure: https:\//portal.azure.us/ 
- Office 365: https:\//portal.office365.us/ 
- Корпоративный портал Intune: https:\//portal.manage.microsoft.us/ 
- Центр администрирования Microsoft Endpoint Manager: https:\//endpoint.microsoft.us/

## <a name="partner-service-endpoints-that-intune-depends-on"></a>Конечные точки служб-партнеров, от которых зависит Intune:
- Службы синхронизации Microsoft Azure Active Directory: https:\//syncservice.gov.us.microsoftonline.com/DirectoryService.svc
- Evo STS: https:\//login.microsoftonline.us
- Прокси-сервер каталога: https:\//directoryproxy.microsoftazure.us/DirectoryProxy.svc
- AAD Graph: https:\//directory.microsoftazure.us and https:\//graph.microsoftazure.us
- MS Graph: https:\//graph.microsoft.us
- ADRS: https:\//enterpriseregistration.microsoftonline.us

[!INCLUDE [Intune notices](../includes/windows-push-notification-services.md)]

[!INCLUDE [Intune notices](../includes/apple-device-network-information.md)]

## <a name="next-steps"></a>Дальнейшие шаги
[Конечные точки сети для Microsoft Intune](intune-endpoints.md)

