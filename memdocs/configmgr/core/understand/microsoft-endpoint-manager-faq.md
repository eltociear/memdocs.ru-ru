---
title: Вопросы и ответы по Microsoft Endpoint Configuration Manager
titleSuffix: Configuration Manager
description: Часто задаваемые вопросы о программе Microsoft Endpoint Configuration Manager
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: be276b34-e283-4386-8b45-5629e431c50d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 05aeca86071ea823d3ebc3cf493bea4d418bad27
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706852"
---
# <a name="microsoft-endpoint-configuration-manager-faq"></a>Вопросы и ответы по Microsoft Endpoint Configuration Manager

*Область применения: Configuration Manager (Current Branch, Technical Preview)*

Начиная с версии 1910 Configuration Manager входит в состав Microsoft Endpoint Manager. Эта статья содержит ответы на часто задаваемые вопросы.

## <a name="summary"></a>Сводка

Вы можете начать с просмотра двухминутного видеролика от Бреда Андерсона (Brad Anderson), корпоративного вице-президента по Microsoft 365:

> [!VIDEO https://www.youtube.com/embed/GS7oNPInFuw]

## <a name="faqs"></a>Частые вопросы

### <a name="what-is-microsoft-endpoint-manager"></a>Что такое Microsoft Endpoint Manager?

Microsoft Endpoint Manager — это интегрированное решение для управления всеми устройствами. Корпорация Майкрософт объединяет Configuration Manager и Intune с упрощенной лицензией. Продолжайте пользоваться имеющимися вложениями в Configuration Manager, используя преимущества Microsoft Cloud в своем темпе.

Следующие решения по управлению Майкрософт теперь являются частью торговой марки **Microsoft Endpoint Manager**:

- [Configuration Manager](https://docs.microsoft.com/configmgr)
- [Intune](https://docs.microsoft.com/intune)
- [Аналитика компьютеров](../../desktop-analytics/overview.md)
- [AutoPilot](https://docs.microsoft.com/intune/enrollment/enrollment-autopilot);
- другие функции в [консоли администратора управления устройствами](https://go.microsoft.com/fwlink/?linkid=2109094).

Дополнительные сведения см. в следующих сообщениях от Бреда Андерсона (Brad Anderson), вице-президента корпорации Майкрософт 365:

- [запись блога с объявлением](https://aka.ms/cmannounce);
- [документ с данными о видении](https://aka.ms/MEMVisionPaper);

### <a name="what-things-change-in-configuration-manager-with-microsoft-endpoint-manager"></a>Что изменилось в Configuration Manager с появлением Microsoft Endpoint Manager?

В версии 1910, кроме изменения названия, Configuration Manager функционирует аналогичным образом.

Особенно важно, что изменились имена папок меню "Пуск" для общих компонентов, таких как [консоль Configuration Manager](../servers/manage/admin-console.md#bkmk_open) и [центр программного обеспечения](software-center.md#bkmk_open).

### <a name="how-do-we-refer-to-the-product-now"></a>Как мы теперь будем ссылаться на этот продукт?

- При ссылке на все решение, включающее все компоненты: **Microsoft Endpoint Manager**

- При ссылке на локальный компонент:
  - При первой ссылке используется полное фирменное наименование: **Microsoft Endpoint Configuration Manager**
  - Для общего использования: **Configuration Manager**
  - В условиях ограниченного пространства: **ConfigMgr**, но только в экземплярах, где обычное имя не помещается

### <a name="are-there-any-licensing-changes"></a>Имеются ли какие-либо изменения в лицензировании?

Да. Как было объявлено на Microsoft Ignite 2019, если у вас есть лицензия на Configuration Manager, то вы также получаете лицензию на Intune для [совместного управления](../../comanage/overview.md) компьютерами на базе Windows. См. [вопросы и ответы о продуктах и лицензировании](product-and-licensing-faq.md#bkmk_mem).

### <a name="why-do-i-still-see-system-center-configuration-manager-some-places"></a>Почему в некоторых местах все еще указано название "System Center Configuration Manager"?

Для внесения изменений во все продукты, службы и вспомогательные материалы, такие как документация, требуется время.

Также существуют некоторые фундаментальные компоненты, которые не могут изменяться. Основной службой Windows на серверах сайта по-прежнему является **SMS_Executive**. Репозиторий GitHub, который поддерживает эту документацию, останется **SCCMDocs**.

## <a name="next-steps"></a>Дальнейшие шаги

См. статью [Новые возможности в добавочных версиях Configuration Manager](../plan-design/changes/whats-new-incremental-versions.md).
