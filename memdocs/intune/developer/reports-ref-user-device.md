---
title: Сопоставление пользователя и устройства — хранилище данных Intune
titleSuffix: Microsoft Intune
description: Сущность UserDeviceAssociation содержит сопоставления пользователей и устройств в вашей организации.
keywords: Хранилище данных Intune
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 12/04/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 777484A7-09CE-4409-987F-76B3F87DFE93
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6127b365a04ad48a9cbaa98bdef821c4d1334181
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/13/2020
ms.locfileid: "79339895"
---
# <a name="reference-for-user-device-association-entity"></a>Справочник по сущности сопоставления пользователя и устройства

Сущность **userDeviceAssociation** содержит сопоставления пользователей и устройств в вашей организации.

## <a name="userdeviceassociations"></a>userDeviceAssociations


|        Имя        |                                           Описание:                                            |        Пример         |
|--------------------|--------------------------------------------------------------------------------------------------|------------------------|
|      userKey       |              Уникальный идентификатор пользователя в хранилище данных. (Суррогатный ключ).               |          123           |
|     deviceKey      |                      Уникальный идентификатор устройства в хранилище данных.                      |          123           |
| createdDateTimeUTC |           Дата и время создания сопоставления пользователя и устройства. Используется формат UTC.           | 23/11/2016 12:00:00 |
|     isDeleted      | Указывает, что пользователь отменил регистрацию этого устройства и что сопоставление больше не действительно. |       Истина/ложь       |
|  endedDateTimeUTC  |              Дата и время (в формате UTC), когда значение IsDeleted изменилось на <strong>True</strong>.               | 23/06/2017 12:00:00 |

## <a name="next-steps"></a>Дальнейшие шаги

- Дополнительные сведения см. в статье [Использование хранилища данных Intune](reports-nav-create-intune-reports.md).
