---
title: Инвентаризация программного обеспечения
titleSuffix: Configuration Manager
description: Общие сведения об инвентаризации программного обеспечения в Configuration Manager.
ms.date: 04/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 79eb49da-cd2b-4ffc-b355-b595aeba3aea
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 07b6f0108125c97128ddc88b663b0af4dabadbe7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695392"
---
# <a name="introduction-to-software-inventory-in-configuration-manager"></a>Общие сведения об инвентаризации программного обеспечения в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Используйте инвентаризацию программного обеспечения для сбора сведений о файлах на клиентских устройствах. Кроме того, функция инвентаризации ПО может собирать файлы с клиентских устройств и сохранять их на сервере сайта. Данные инвентаризации программного обеспечения собираются, если в клиентских параметрах включен параметр **Включить инвентаризацию программного обеспечения для клиентов**. Можно также запланировать операцию в параметрах клиента.  

После включения функции инвентаризации программного обеспечения и ее запуска клиентами данные инвентаризации отправляются в точку управления на сайте клиента. Затем точка управления передает данные инвентаризации на сервер сайта Configuration Manager, сохраняющий их в базе данных сайта.

 Ниже приведены способы просмотра данных инвентаризации программного обеспечения.  

- [Создание запросов](../../../../core/servers/manage/create-queries.md), которые возвращают устройства с указанными файлами.   

- Создание [коллекций на основе запросов](../../../../core/clients/manage/collections/introduction-to-collections.md), которые включают в себя устройства с указанными файлами.   

- [Запуск отчетов](../../../servers/manage/introduction-to-reporting.md), содержащих сведения о файлах на устройствах.

- Использование [обозревателя ресурсов](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md) для изучения подробной информации о файлах, включенных в инвентарную опись и собранных на клиентских устройствах.   

 При выполнении на клиентском устройстве инвентаризации ПО первый отчет содержит полную инвентаризацию. Последующие отчеты содержат только сведения об изменении данных инвентаризации. Сервер сайта обрабатывает изменившиеся данные в порядке их поступления. Если изменившиеся данные для клиента отсутствуют, сервер сайта отклоняет дополнительные изменившиеся данные инвентаризации и указывает клиенту выполнить полную инвентаризацию.  

 Configuration Manager может обнаруживать компьютеры с двойной загрузкой, но возвращает сведения об инвентаризации только из операционной системы, активной на момент выполнения инвентаризации.  