---
title: Лицензирование и ветви
titleSuffix: Configuration Manager
description: Узнайте о требованиях к лицензированию для доступных в Configuration Manager вариантов установки
ms.date: 06/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 495b87ae-41a4-49ba-abe2-d4f7d22ac0d4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f18ed2180f1d526e2afa4872e8fa9018c7e18721
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706882"
---
# <a name="licensing-and-branches-for-configuration-manager"></a>Лицензирование и ветви в Configuration Manager

*Область применения: Configuration Manager (Current Branch) и System Center Configuration Manager (Long-Term Servicing Branch)*

Из этой статьи вы узнаете о требованиях к лицензированию для доступных в Configuration Manager вариантов установки. Такие варианты установки включают приведенные ниже ветви.

- Current Branch
- Long-term servicing branch (LTSB)
- Ознакомительная установка Current Branch
- Ветвь Technical Preview

## <a name="licensing-overview"></a>Общие сведения о лицензировании

Клиенты с действующим соглашением Software Assurance (SA) для лицензий Configuration Manager или с эквивалентными правами по подписке с 1 октября 2016 г. имеют право на использование выпуска Configuration Manager версии 1606 за октябрь 2016 г. Клиенты с правами на Configuration Manager, действительными на 1 октября 2016 г. или после этой даты, могут выбрать один из двух вариантов лицензирования после установки: Current Branch и Long-Term Servicing Branch (LTSB).

Все условия в отношении продуктов, приобретаемых в рамках программ корпоративного лицензирования Майкрософт, можно найти [здесь](https://go.microsoft.com/fwlink/?LinkId=800052).


## <a name="licensed-branches"></a>Лицензированные ветви

Эта статья ссылается на соглашение Software Assurance или эквивалентные права по подписке. Это лицензионное соглашение Майкрософт предоставляет права на установку и использование Configuration Manager.

### <a name="current-branch"></a>Current Branch

Current Branch требует наличия действующего соглашения Software Assurance (или эквивалентные права) для Configuration Manager. Подробные сведения см. в подразделе [Software Assurance и Current Branch](#software-assurance-and-the-current-branch).

Эта ветвь поддерживается для использования в рабочих средах, в которых необходимо регулярно получать исправления и обновления компонентов от корпорации Майкрософт. Она предоставляет доступ ко всем возможностям и улучшениям.

Начиная с версии 1710 каждая версия обновления поддерживается в течение 18 месяцев с даты выпуска общедоступной версии. Дополнительные сведения см. в статье [Поддержка версий Current Branch Configuration Manager](../servers/manage/current-branch-versions-supported.md).

### <a name="long-term-servicing-branch-ltsb"></a>Long-term servicing branch (LTSB)

LTSB требует наличия действующего соглашения Software Assurance с корпорацией Майкрософт (по состоянию на 1 октября 2016 г.). Подробные сведения см. в разделе [Software Assurance и LTSB](#software-assurance-and-the-ltsb).

Эта ветвь поддерживается для использования в рабочих средах. Она предназначена для клиентов, срок действия соглашения Software Assurance или эквивалентных прав по подписке которых для Configuration Manager истек после 1 октября 2016 г. Возможности этой ветви ограничены по сравнению с Current Branch.

Она позволяет получать критические обновления для системы безопасности Configuration Manager, но новые возможности недоступны.

### <a name="evaluation-installation-of-the-current-branch"></a>Ознакомительная установка Current Branch

Ознакомительная версия не требует наличия соглашения Software Assurance с корпорацией Майкрософт. [Ознакомительные установки](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection) могут принадлежать только ветви Current Branch, и их можно использовать в течение 180 дней.

Вы можете обновить ознакомительную установку до полной установки Current Branch. Обновить ознакомительную установку до Long-Term Servicing Branch нельзя.

### <a name="technical-preview-branch"></a>Ветвь Technical Preview

Доступна также [ветвь Technical Preview](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview). Это ограниченная сборка Configuration Manager, которая позволяет испытать новые возможности. Для установки Technical Preview и лицензированных версий используются разные носители. Подробные сведения см. в статье [Technical Preview для Configuration Manager](../get-started/technical-preview.md).


## <a name="software-assurance-agreements"></a>Соглашения Software Assurance

Состояние Software Assurance или эквивалентных прав по подписке для лицензий Configuration Manager на 1 октября 2016 г. или после этой даты определяет то, какую ветвь вы можете установить и использовать.

### <a name="software-assurance-and-the-current-branch"></a>Software Assurance и Current Branch

Права на использование Configuration Manager (Current Branch) могут предоставляться из следующих источников:

- **System Center**: клиенты с активными соглашениями SA для лицензий System Center Standard или Datacenter могут установить и использовать Configuration Manager (Current Branch).

- **System Center Configuration Manager**: Клиенты с действующим соглашением SA для лицензий Configuration Manager или с эквивалентными правами по подписке могут установить и использовать Configuration Manager (Current Branch).

При наличии действующего соглашения SA для лицензий Configuration Manager (или эквивалентных прав по подписке) по состоянию на 1 октября 2016 г. или после этой даты:

- Вы можете установить и использовать Current Branch.
- Если срок действия соглашения SA или подписки истечет, Current Branch необходимо будет удалить.

### <a name="software-assurance-and-the-ltsb"></a>Software Assurance и LTSB

При наличии действующего соглашения SA для лицензий Configuration Manager (или эквивалентных прав по подписке) по состоянию на 1 октября 2016 г. или после этой даты:

- Вы можете установить и использовать LTSB. Клиенты, имеющие бессрочные права на Configuration Manager либо соглашение SA или подписку с истекшим сроком действия, могут установить версию Configuration Manager LTSB, которая является текущей на момент истечения срока действия соглашения.

Ветвь LTSB основана на версии Current Branch 1606 и имеет следующие ограничения:

- Преобразование Current Branch в LTSB не поддерживается. При наличии сайта Current Branch необходимо установить LTSB в качестве нового сайта.  

- LTSB поддерживает не все возможности Current Branch. Подробные сведения см. в статье [Общие сведения о версии System Center Configuration Manager (Long-Term Servicing Branch)](introduction-to-the-ltsb.md). К ограничениям относятся ограниченный набор возможностей, ограниченные варианты обновления и отдельный жизненный цикл поддержки продукта.  

### <a name="software-assurance-expiration-date"></a>Дата истечения срока действия Software Assurance

Начиная с выпуска версии 1606 базового носителя для Configuration Manager в октябре 2016 г. вы можете указывать дату окончания срока действия соглашения Software Assurance. **Дата истечения срока действия Software Assurance** — это необязательное значение, которое можно указать в качестве напоминания. Добавьте его в консоли Configuration Manager при запуске установки Configuration Manager или после этого.

> [!NOTE]
> Майкрософт не проверяет указанную дату окончания срока действия и не будет использовать ее для проверки лицензии. Вы можете использовать ее как напоминание об окончании срока действия. Это значение может оказаться полезным в тех ситуациях, когда Configuration Manager периодически проверяет наличие обновлений программного обеспечения, предлагаемых через Интернет. Лицензия Software Assurance должна быть действующей, чтобы вы могли воспользоваться такими дополнительными обновлениями.

#### <a name="to-specify-the-software-assurance-expiration-date"></a>Указание даты истечения срока действия для Software Assurance

- Вы можете указать это значение на странице **Ключ продукта** мастера установки при запуске программы установки с носителя Configuration Manager.

- Эту дату также можно указать на вкладке **Лицензирование** диалогового окна **Параметры иерархии** в консоли Configuration Manager.


## <a name="licensing-resources"></a>Ресурсы по лицензированию

Чтобы узнать больше о лицензировании продуктов, воспользуйтесь приведенными ниже ресурсами.

### <a name="microsoft-volume-licensing-service-center-vlsc"></a>Microsoft Volume Licensing Service Center (VLSC)

- [Обзор VLSC](https://www.microsoft.com/Licensing/existing-customer/vlsc-training-and-resources.aspx)

- [Условия использования продукта с корпоративным лицензированием Microsoft](https://go.microsoft.com/fwlink/?LinkId=800052)

- Клиенты программы корпоративного лицензирования могут получить сводку по лицензиям на веб-сайте [Volume Licensing Service Center](https://www.microsoft.com/Licensing/servicecenter/default.aspx). Перейдите в меню **Лицензии** и выберите пункт **Licenses Summary** (Сводка по лицензиям).

### <a name="vlsc-videos"></a>Видеоролики, посвященные VLSC

- Учебные видеоматериалы по работе VLSC можно найти на странице [Учебные материалы и ресурсы по работе с веб-сайтом Microsoft Volume Licensing Service Center](https://www.microsoft.com/licensing/existing-customer/vlsc-training-and-resources) в разделе **Видеоруководства**.

- Видео [Where to look up your active Software Assurance agreement](https://www.microsoft.com/showcase/video.aspx?uuid=fe1846cb-1d26-49fc-b064-57b25dcc31a0) (Где найти действующее соглашение Software Assurance) с 43-й секунды  

- [Как получить разрешения для VLSC](https://www.microsoft.com/showcase/video.aspx?uuid=ac4ed1ca-d0a9-43cd-89fa-74ccb555dec4). Вы можете предоставлять разрешения на чтение и запись данных в VLSC другим сотрудникам своей организации.
