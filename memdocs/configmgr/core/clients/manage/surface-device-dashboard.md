---
title: Панель мониторинга устройств Surface
titleSuffix: Configuration Manager
description: Просмотрите сведения об управлении устройствами Surface с помощью панели мониторинга.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 7397fc17-3ae8-4525-8386-aea8a9cffa06
ms.openlocfilehash: f9b9c49bde16754b7a60112905f14da2cd5e48eb
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906290"
---
# <a name="surface-device-dashboard-in-configuration-manager"></a>Панель мониторинга устройств Surface в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Начиная с версии 1802 в панели мониторинга устройств Surface все сведения об устройствах Surface, обнаруженных в вашей среде, отображаются в одном удобном представлении. <!--1355788-->

## <a name="open-the-surface-device-dashboard"></a>Переход к панели мониторинга устройств Surface

Чтобы открыть панель мониторинга устройств Surface, выполните следующие действия. 

1. Откройте консоль Configuration Manager. 
2. Щелкните узел **Мониторинг**. 
3. Чтобы загрузить панель мониторинга, щелкните **Устройства Surface**.

**Панель мониторинга устройств Surface**
![Панель мониторинга устройств Surface](media/Surface-device-dashboard.PNG)



## <a name="reviewing-information-in-the-surface-device-dashboard"></a>Просмотр сведений на панели мониторинга устройств Surface

На панели мониторинга устройства Surface отображаются три диаграммы для вашей среды. 

- **Percent of Surface devices** (Доля устройств Surface) — сведения о доле устройств Surface в вашей среде.

    ![Диаграмма "Доля устройств Surface"](media/Percent-Surface-Devices.PNG)
- **Surface Models** (Модели Surface) — количество устройств на каждую модель Surface. 
  - При наведении указателя мыши на раздел диаграммы выводится доля устройств Surface в выбранной модели. 

       ![Диаграмма "Модели Surface"](media/Surface-Models-Hover.PNG)
  - Чтобы перейти к списку устройств для модели, щелкните раздел диаграммы. 
      ![Список устройств в модели Surface](media/Surface-Model-Device-List.PNG)

- **Top five firmware versions** (Пять ведущих версий встроенного ПО) — диаграмма с основными пятью моделями встроенного ПО в вашей среде. 
  - При наведении указателя мыши на раздел диаграммы выводится число устройств Surface с выбранной версией встроенного ПО. Начиная с Configuration Manager версии 1806 при щелчке раздела диаграммы отображается список соответствующих устройств. <!--1358654-->
     ![Список устройств в модели Surface](media/Surface-Firmware-Hover.PNG)


## <a name="more-information"></a>Дополнительные сведения

Дополнительные сведения об устройствах Surface см. на веб-сайте [Surface](https://www.microsoft.com/surface).

Дополнительные сведения о развертывании обновлений встроенного ПО Surface в Configuration Manager см. в статье [Управление обновлениями драйверов Surface](https://support.microsoft.com/help/4098906).




