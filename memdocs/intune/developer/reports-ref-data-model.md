---
title: Модель данных для хранилища данных
titleSuffix: Microsoft Intune
description: Хранилище данных Microsoft Intune ежедневно производит выборку данных, чтобы предоставить историческое представление для вашей постоянно изменяющейся мобильной среды.
keywords: Хранилище данных Intune
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 05/28/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 4D04D3D9-4B6C-41CD-AAF8-466AF8FA6032
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: db6feb746aa7177f56ff6e87565d67e207d4d9ef
ms.sourcegitcommit: 118587ddb31ce26b27801839db9b3b59f1177f0f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/29/2020
ms.locfileid: "84165453"
---
# <a name="microsoft-intune-data-warehouse-data-model"></a>Модель данных для хранилища данных Microsoft Intune

Хранилище данных Intune ежедневно производит выборку данных, чтобы предоставить историческое представление для вашей постоянно изменяющейся среды мобильных устройств. Представление состоит из связанных сущностей во времени.

## <a name="entities-entity-sets"></a>Сущности: наборы сущностей

Хранилище предоставляет данные в следующих высокоуровневых областях:

- Меры защиты, охватывающие приложения и их использование
- Зарегистрированные устройства, свойства и инвентаризация
- Инвентаризация приложений и программного обеспечения
- Политики конфигурации и соответствия для устройств

Эти области содержат сущности, важные в вашей среде Intune. Сведения о наборах сущностей см. в следующих статьях:

- [Приложения](reports-ref-application.md)
- [Дата](reports-ref-date.md)
- [Устройства](reports-ref-devices.md)
- [Справочник по расширению управления Intune](reports-ref-intunemanagementextension.md)
- [Политика](reports-ref-policy.md)
- [Управление мобильными приложениями (MAM)](../apps/app-management.md)
- [Пользователь](reports-ref-user.md)
- [Сопоставление пользователя и устройства](reports-ref-user-device.md)

## <a name="relationships-star-schema-model"></a>Связи: модель по схеме типа "звезда"

Хранилище упорядочивает сущности по связям, значимым для типа задаваемых вопросов. Например, вы можете просмотреть количество установок приложения Android собственной разработки. Структура хранилища данных позволяет получить ценные сведения о мобильной среде. В свою очередь аналитические средства, такие как Microsoft Power BI, могут использовать модель данных хранилища для создания визуализаций и динамических панелей мониторинга.

Сущности и связи используют модель по схеме типа "звезда". Такая схема сопоставляет факты по измерению времени. *Факт* в контексте модели представляет собой количественное измерение, например число устройств или приложений либо время регистрации. В хранилище таблиц фактов содержится большой объем данных. Их размер может значительно увеличиваться, поэтому в хранилище обычно собираются данные за 30 дней. *Измерение* предоставляет контекст фактам. Факт анализирует произошедшую ситуацию, а измерения указывают, с кем это случилось. Таблицы измерения, такие как таблица **Пользователи**, меньше и могут хранить данные в течение более длинного времени, чем таблицы фактов.

Модель по схеме типа "звезда" оптимизирована для гибкой работы и анализа данных, чтобы вы могли создавать отчеты и получить представление о своей развивающейся мобильной среде.

## <a name="time-daily-snapshots"></a>Время: ежедневные моментальные снимки

Хранилище распределяет данные из Intune в нисходящем направлении. Intune ежедневно в полночь (в формате UTC) создает моментальные снимки и сохраняет их в хранилище. Длительность удержания моментальных снимков зависит от таблицы фактов. Некоторые могут храниться семь дней, другие — 30 дней, а некоторые даже еще дольше.

## <a name="next-steps"></a>Дальнейшие действия

- Дополнительные сведения о том, как хранилище данных отслеживает время существования пользователей в Intune, см. в статье [Представление времени существования пользователя в хранилище данных Microsoft Intune](reports-ref-user-timeline.md).
- Дополнительные сведения о работе с хранилищами данных см. [здесь](https://www.codeproject.com/Articles/652108/Create-First-Data-WareHouse).
- Дополнительные сведения о работе с Power BI и хранилищем данных см. в статье [Создание отчета Power BI путем импорта набора данных](https://powerbi.microsoft.com/documentation/powerbi-service-create-a-new-report/). 
