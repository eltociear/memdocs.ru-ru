---
title: Безопасность и конфиденциальность запросов
titleSuffix: Configuration Manager
description: Рекомендации по обеспечению безопасности и конфиденциальности при запросе информации из базы данных сайта.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 30080620-20d3-4c38-b8dd-db5516e1acae
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 882eedd1be029d5824fbd5d26a3f08d8f8f0021d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695702"
---
# <a name="security-and-privacy-for-queries-in-configuration-manager"></a>Безопасность и конфиденциальность запросов в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Запросы в Configuration Manager позволяют получать сведения из базы данных сайта с учетом заданных условий. Configuration Manager собирает сведения базы данных сайта во время стандартных операций. Например, используя сведения, собранные в ходе обнаружения или инвентаризации, можно настроить запрос для определения устройств, которые соответствуют определенным условиям.  

 Дополнительные сведения о запросах см. в статье [Общие сведения о запросах в System Center Configuration Manager](../../../core/servers/manage/introduction-to-queries.md). См. подробнее об [обеспечении в Configuration Manager безопасности и конфиденциальности во время операций по сбору данных, извлекаемых с помощью запросов](../../../core/plan-design/security/security-and-privacy.md).  

## <a name="security-best-practices-for-queries"></a>Рекомендации по обеспечению безопасности для запросов

 Учитывайте следующие рекомендации по обеспечению безопасности при выполнении запросов.  

|Рекомендация по безопасности|Дополнительные сведения|  
|----------------------------|----------------------|  
|При импорте и экспорте запроса, сохраненного в сетевой папке, обеспечьте безопасность расположения и сетевого канала.|Ограничьте доступ пользователей к сетевой папке.<br /><br /> Используйте подписывание SMB или протокол IPsec при обмене данными между сетевой папкой и сервером сайта, чтобы предотвратить изменение данных запроса злоумышленником до их импорта.|  

## <a name="next-steps"></a>Дальнейшие шаги
  
[Безопасность и конфиденциальность Configuration Manager](../../../core/plan-design/security/security-and-privacy.md)
