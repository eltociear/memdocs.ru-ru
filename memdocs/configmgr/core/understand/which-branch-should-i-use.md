---
title: Какую ветвь следует использовать
titleSuffix: Configuration Manager
description: В этой статье описаны различия между доступными ветвями Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a3be4f8f-3d44-4e3c-9fa1-e85f30a36e72
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c7a505296fe51aae996d429fe7da2033d3a787ff
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706672"
---
# <a name="which-branch-of-configuration-manager-should-i-use"></a>Какую ветвь Configuration Manager следует использовать?

*Область применения: Configuration Manager (Current Branch и Technical Preview Branch) и System Center Configuration Manager (Long-Term Servicing Branch)*

Доступны три ветви Configuration Manager:

- Current Branch
- Long Term Servicing Branch
- Ветвь Technical Preview

Эта статья поможет вам выбрать наиболее подходящую ветвь.

> [!TIP]  
> На всех сайтах в иерархии должна использоваться одна ветвь. Иерархия с различными ветвями на разных сайтах не поддерживается.

## <a name="current-branch"></a>Current Branch

Эта ветвь лицензирована для использования в рабочей среде. Она предоставляет доступ к новейшим компонентам и функциям. Эту ветвь можно использовать при наличии одной из следующих лицензий:  

- System Center Datacenter
- System Center Standard
- System Center Configuration Manager
- Эквивалентные права по подписке  

Дополнительные сведения о программе Software Assurance и вариантах лицензирования см. в разделах [Лицензирование и ветви в Configuration Manager](learn-more-editions.md) и [Вопросы и ответы о ветвях и лицензировании Configuration Manager](product-and-licensing-faq.md).

Корпорация Майкрософт планирует выпускать обновления версии Current Branch для Configuration Manager несколько раз в год. Каждая версия обновления будет поддерживаться в течение 18 месяцев с даты выпуска общедоступной версии. Техническая поддержка доступна в течение всего периода поддержки. Однако структура поддержки стала динамической и состоит из двух отдельных этапов обслуживания, которые зависят от доступности последней версии Current Branch. Дополнительные сведения см. в статье [Поддержка версий Current Branch Configuration Manager](../servers/manage/current-branch-versions-supported.md). Обновления до новых версий доступны как обновления в консоли.

Для установки ветви Current Branch в качестве нового сайта можно использовать [базовый носитель](../servers/manage/updates.md#bkmk_Baselines). Кроме того, базовый носитель можно использовать для обновления System Center 2012 Configuration Manager с пакетом обновления 2 (SP2) или System Center 2012 R2 Configuration Manager с пакетом обновления 1 (SP1). Доступ к носителю зависит от способа лицензирования Configuration Manager в организации.

Базовый носитель также можно использовать для установки нового сайта в качестве ознакомительной версии Current Branch. Для ознакомительной версии лицензия не требуется. Ознакомительная версия предоставляется на 180 дней. Она поддерживает обновление до лицензионной версии Current Branch. Чтобы установить только ознакомительную версию, получите ее на веб-сайте [центра оценки TechNet](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection).

> [!NOTE]
> Базовый носитель используется только для установки сайтов для новой иерархии Configuration Manager. Если вы ранее установили базовую версию, для обновления сайтов до новой версии воспользуйтесь обновлениями в консоли.  
>
> При обновлении сайтов с помощью обновлений в консоли создаются сайты, эквивалентные новому сайту, установленному с помощью базового носителя.
>
> Дополнительные сведения см. в статье [Обновления для Configuration Manager](../servers/manage/updates.md).  

### <a name="features-of-the-current-branch"></a>Возможности Current Branch

- Принимает [обновления в консоли](../servers/manage/install-in-console-updates.md), предоставляющие доступ к новым функциям.
- Принимает обновления в консоли, обеспечивающие исправления безопасности и качества для существующих компонентов.
- Поддерживает обновление по внештатному каналу при необходимости. Дополнительные сведения см. в разделах [Использование инструмента регистрации обновлений](../servers/manage/use-the-update-registration-tool-to-import-hotfixes.md) и [Использование установщика исправлений](../servers/manage/use-the-hotfix-installer-to-install-updates.md).
- Интегрируется с облачными службами.
- Поддерживает [миграцию данных](../migration/migrate-data-between-hierarchies.md) в другие установки Configuration Manager и из них.
- Поддерживает обновление с предыдущих версий Configuration Manager.
- Поддерживает установку в качестве ознакомительного выпуска с последующим обновлением до полностью лицензированной версии.

Специалисты Майкрософт рекомендуют выполнять обновление до последней версии вскоре после ее выпуска. Перед обновлением до более актуальной версии можно работать с текущей версией в течение 18 месяцев. Также можно пропустить обновление для установки самой последней доступной версии. Так как каждая версия является накопительной, даже если вы пропустите одно обновление и установите последнюю версию, вы все равно получите доступ ко всем функциям и усовершенствованиям предыдущих версий.

Дополнительные сведения см. в разделе [Поддержка версий Current Branch](../servers/manage/current-branch-versions-supported.md).

### <a name="current-branch-update-options"></a>Варианты обновления Current Branch

- При наличии действующего соглашения Software Assurance можно установить обновления в консоли для версий Current Branch.  
- Преобразовать Current Branch в Technical Preview невозможно. Ветви Technical Preview — это отдельные установки, которым не нужна лицензия.
- Кроме того, нет возможности преобразовать Current Branch в ветвь Long-Term Servicing Branch (LTSB). Нужно удалить Current Branch, а затем установить LTSB в рамках новой установки.

## <a name="long-term-servicing-branch"></a>Long Term Servicing Branch

Эта ветвь лицензирована для использования в рабочей среде Configuration Manager для клиентов, использующих Current Branch и согласившихся, что срок действия их участия в программе Configuration Manager Software Assurance (SA) или эквивалентных прав по подписке истекает после 1 октября 2016 г. Дополнительные сведения о программе Software Assurance и вариантах лицензирования см. в разделах [Лицензирование и ветви в Configuration Manager](learn-more-editions.md) и [Вопросы и ответы о ветвях и лицензировании Configuration Manager](product-and-licensing-faq.md).

В основе ветви LTSB лежит версия 1606. Эта ветвь не получает обновления в консоли, предоставляющие новые возможности или обновляющие существующие компоненты. Тем не менее важные исправления безопасности предоставляются. Чтобы установить LTSB, нужно использовать [базовый носитель](../servers/manage/updates.md#bkmk_Baselines) с версией 1606, который поставляется вместе с System Center 2016. Более поздние базовые версии не поддерживают установку LTSB.

Для установки LTSB в качестве нового сайта или обновления с поддерживаемого сайта System Center 2012 Configuration Manager используйте [базовый носитель](../servers/manage/updates.md#bkmk_Baselines) версии 1606, предоставляемый вместе с System Center 2016. Базовый носитель можно использовать для установки нового сайта под управлением версии 1606 ветви Current Branch или нового сайта под управлением ветви Long-Term Servicing Branch.

> [!TIP]  
> Дополнительные сведения о System Center 2016 см. в [документации по System Center 2016](https://docs.microsoft.com/system-center/index). Эта документация также определяет способ получения System Center 2016, для чего требуется лицензионное соглашение с Майкрософт или аналогичные права.  
>  
> Чтобы найти Configuration Manager версии 1606 в Volume Licensing Service Center (VLSC), перейдите на вкладку **Downloads and Keys** (Файлы для скачивания и ключи) сайта [VLSC](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx), выполните поиск по запросу `System Center 2016`, а затем выберите **System Center 2016 Datacenter** или **System Center 2016 Standard**.  
>  
> Ознакомительную версию System Center 2016 также можно скачать в [Центре оценки TechNet](https://www.microsoft.com/evalcenter/evaluate-system-center-technical-preview).  

### <a name="features-of-the-ltsb"></a>Возможности LTSB

- Принимает обновления в консоли, обеспечивающие важные исправления безопасности.
- Предоставляет возможность установки, если истек срок действия соглашения SA или эквивалентных прав на Configuration Manager.
- Поддерживает обновление (преобразование) в Current Branch после получения действующего соглашения SA или эквивалентных прав на Configuration Manager.

### <a name="ltsb-limitations"></a>Ограничения LTSB

Ветвь LTSB основана на версии Current Branch 1606 и имеет следующие ограничения:

- Ветвь LTSB поддерживается в течение 10 лет после выпуска общедоступной версии (октябрь 2016 г.). В течение этого срока предоставляются важные обновления безопасности, но через 10 лет поддержка этой ветви заканчивается. Дополнительные сведения о жизненном цикле поддержки см. в разделе [Политика жизненного цикла поддержки Майкрософт](https://support.microsoft.com/lifecycle).
- Поддерживает ограниченный набор серверных и клиентских операционных систем и связанных технологий, таких как версии SQL Server. Дополнительные сведения см. в статье [Поддерживаемые конфигурации для Long-Term Servicing Branch](supported-configurations-for-ltsb.md).
- Не получает обновления, предоставляющие новые функции.
- Не поддерживает следующие возможности:
  - Подключенные к облаку функции, такие как совместное управление или Аналитика компьютеров
  - локальное управление мобильными устройствами (MDM).
  - Панель мониторинга обслуживания Windows 10, планы обслуживания или Semi-Annual Channel для Windows 10
  - Будущие выпуски Windows 10 LTSB и Windows Server.
  - Аналитика активов.
  - Любые функции предварительной версии.

### <a name="ltsb-update-options"></a>Варианты обновления LTSB

- Установку LTSB можно преобразовать в установку Current Branch. Преобразование в ветвь Current Branch поддерживается до или после истечения срока действия поддержки для LTSB.

  Для преобразования необходимо действующее соглашение Software Assurance с Майкрософт. Дополнительные сведения см. в следующих статьях:

  - [Обновление Long-Term Servicing Branch до Current Branch](convert-to-current-branch.md)
  - [Лицензирование и ветви в Configuration Manager](learn-more-editions.md)
  - [Базовые и обновленные версии](../servers/manage/updates.md#bkmk_Baselines)

- Преобразовать LTSB в Technical Preview невозможно. Ветви Technical Preview — это отдельные установки, которым не нужна лицензия.

- Ознакомительную версию Current Branch невозможно обновить до установки LTSB.

## <a name="technical-preview-branch"></a>Ветвь Technical Preview

Ветвь Technical Preview предназначена для применения в лабораторной среде. Благодаря этому вы можете изучать и апробировать новейшие возможности, разрабатываемые для Configuration Manager. Она не поддерживается в рабочей среде и не требует наличия лицензионного соглашения Software Assurance.

Чтобы установить новый сайт под управлением Technical Preview, используйте последнюю версию [базового носителя для ветви Technical Preview](../get-started/technical-preview.md#bkmk_install). После установки ветви Technical Preview новые версии доступны как ежемесячные обновления в консоли.

### <a name="features-of-the-technical-preview-branch"></a>Возможности ветви Technical Preview

- Основана на последних базовых версиях Current Branch.
- Принимает обновления в консоли для обновления до последней версии Technical Preview.
- Включает новые разрабатываемые компоненты, по которым корпорация Майкрософт хочет получить ваши отзывы.
- Принимает обновления, которые применяются только к ветви Technical Preview.

### <a name="technical-preview-limitations"></a>Ограничения Technical Preview

- [Поддержка ограничена](../get-started/technical-preview.md#bkmk_reqs), включая только один первичный сайт и до 10 клиентов.  
- Невозможно выполнить обновление или миграцию в Current Branch или установку LTSB.
- Не поддерживает следующие возможности:
  - Использование миграции для импорта или экспорта данных в другую установку Configuration Manager
  - Обновление с предыдущих версий Configuration Manager.
  - Установка в качестве ознакомительной версии

Функции, которые впервые были представлены в Technical Preview, часто добавляются в Current Branch при последующем обновлении. Каждая новая версия Technical Preview включает функции из предыдущих выпусков Technical Preview даже после того, как эти функции были добавлены в выпуск Current Branch.

Дополнительные сведения см. в статье [Technical Preview для Configuration Manager](../get-started/technical-preview.md)

### <a name="technical-preview-update-options"></a>Варианты обновления Technical Preview

- Можно установить любые обновления в консоли для новой версии Technical Preview.

- Преобразовать Technical Preview в Current Branch или LTSB невозможно.

## <a name="identify-your-version-and-branch"></a>Определение версии и ветви

### <a name="version"></a>Версия

Чтобы проверить версию сайта, в левом верхнем углу консоли перейдите к элементу **О Configuration Manager**. В этом диалоговом окне отображается **Версия сайта**. Список версий сайта см. в статье [Базовые и обновленные версии](../servers/manage/updates.md#bkmk_Baselines).

### <a name="branch"></a>Ветвь

Чтобы узнать ветвь сайта, в консоли перейдите в раздел **Администрирование** > **Конфигурация сайта** > **Сайты** и откройте **Параметры иерархии**. Если имеется активная возможность преобразования в Current Branch, на сайте выполняется версия LTSB. Если на сайте выполняется Current Branch, консоль отключает эту возможность.

Дополнительные сведения о различных версиях Configuration Manager см. в разделе [Базовые и обновленные версии](../servers/manage/updates.md#bkmk_Baselines).
