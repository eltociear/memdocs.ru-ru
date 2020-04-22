---
title: Безопасность и конфиденциальность управления питанием
titleSuffix: Configuration Manager
description: Сведения о безопасности и конфиденциальности управления питанием в Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 469ff35f-59a1-484d-902b-107dd6070baf
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: c019faee1ffa035bde626778bb15b8f5feabc243
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696512"
---
# <a name="security-and-privacy-for-power-management-in-configuration-manager"></a>Обеспечение безопасности и конфиденциальности управления питанием в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

В этом разделе приводятся сведения о безопасности и конфиденциальности управления питанием в Configuration Manager.  

## <a name="security-best-practices-for-power-management"></a>Рекомендации по обеспечению безопасности для управления питанием  
 Для функции управления питанием нет каких-то специальных рекомендаций по обеспечению безопасности.  

## <a name="privacy-information-for-power-management"></a>Сведения о конфиденциальности управления питанием  
 Управление питанием использует возможности, которые встроены в Windows для отслеживания энергопотребления и применения параметров питания к компьютерам в рабочее и нерабочее время. Configuration Manager собирает с компьютеров данные по энергопотреблению, включая сведения о периодах использования компьютера пользователем. Хотя Configuration Manager отслеживает энергопотребление для коллекции, а не для отдельных компьютеров, можно создать коллекцию, содержащую только один компьютер. Управление питанием не включено по умолчанию и должно быть настроено администратором.  

 Сведения об энергопотреблении сохраняются в базе данных Configuration Manager и не отправляются в Майкрософт. Подробные сведения хранятся в базе данных 31 день, сводные данные — 13 месяцев. Интервал удаления изменить нельзя.  

 Перед настройкой параметров управления питанием учтите требования к конфиденциальности.  
