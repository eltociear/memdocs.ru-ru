---
title: Скачивание определений из Центра обновления Майкрософт
titleSuffix: Configuration Manager
description: Узнайте, как обеспечить скачивание определений вредоносных программ Endpoint Protection из Центра обновления Майкрософт для Configuration Manager.
ms.date: 11/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: ab7626ae-d4bf-4ca6-ab25-c61f96800a02
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1f0d8ac635d514e750584126458bfde6b5fc24ee
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697242"
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-microsoft-updates"></a>Включение скачивания определений вредоносных программ Endpoint Protection из Центра обновления Майкрософт

*Область применения: Configuration Manager (Current Branch)*

При скачивании обновлений определений из Центра обновления Майкрософт клиенты будут проверять веб-сайт Центра обновления Майкрософт через интервал, указанный в разделе **Обновления для механизма обнаружения угроз** диалогового окна политики защиты от вредоносных программ.

 Этот метод может быть полезен, когда у клиента отсутствует подключение к сайту Configuration Manager или если требуется, чтобы пользователи могли инициировать обновления определений.

> [!IMPORTANT]
> - Чтобы использовать этот метод для загрузки обновлений определений, клиенты должны иметь доступ к Центру обновления Майкрософт через Интернет.
> - Начиная с Configuration Manager версии 1902 раздел **Обновления определений** переименован в **Обновления аналитики безопасности**.

## <a name="using-the-microsoft-malware-protection-center-to-download-definitions"></a>Использование Центра Майкрософт по защите от вредоносных программ для загрузки определений
 Вы можете настроить клиенты для загрузки обновлений из Центра Майкрософт по защите от вредоносных программ. Клиенты Endpoint Protection применяют эту возможность для скачивания обновлений определений, если они не смогли загрузить обновления из другого источника. Этот метод обновления может быть полезен, если в вашей инфраструктуре Configuration Manager существует проблема, препятствующая доставке обновлений.

> [!IMPORTANT]
>  Чтобы использовать этот метод для загрузки обновлений определений, клиенты должны иметь доступ к Центру обновления Майкрософт через Интернет.
> 
> 
> [!div class="button"]
> [Следующий этап >](endpoint-antimalware-policies.md)
> 
> [!div class="button"]
> [Назад >](endpoint-configure-alerts.md)
