---
title: Configuration Manager и Windows как услуга
titleSuffix: Configuration Manager
description: Основные сведения о том, как внедрить Configuration Manager Current Branch для поддержки модели Windows как услуга.
ms.date: 06/15/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c8534a1e-57b8-4688-b6e6-299d82cfcec9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e92a39a91c60734f212c7d1e99e266d0ec9a4008
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701252"
---
# <a name="configuration-manager-and-windows-as-a-service"></a>Configuration Manager и Windows как услуга

*Область применения: Configuration Manager (Current Branch)*

Configuration Manager обеспечивает комплексное управление обновлениями компонентов для Windows 10. Для полноценного внедрения модели Windows как услуга требуется также внедрить модель Configuration Manager Current Branch. Для обеспечения актуальности Windows 10 следует поддерживать в актуальном состоянии и Configuration Manager. Чтобы воспользоваться всеми преимуществами новых корпоративных возможностей для Windows 10, нужны новые версии Configuration Manager. Эта статья является материал целевой страницей для ключевых материалов по внедрению модели Configuration Manager Current Branch. Эта модель прокладывает вам путь к модели Windows как услуга.

## <a name="key-articles-about-adopting-configuration-manager-current-branch"></a>Ключевые материалы по внедрению модели Configuration Manager Current Branch

| Статья        | Описание:          | 
| ------------- |-------------|
|[Обзор Configuration Manager Current Branch](../plan-design/changes/whats-new-incremental-versions.md)|Содержит краткий обзор ключевых аспектов новой модели обслуживания для Configuration Manager (Current Branch).|
|[Жизненный цикл поддержки](../servers/manage/current-branch-versions-supported.md)|Содержит пояснения для новой модели поддержки и обслуживания.|
|[Удаленные и устаревшие компоненты](../plan-design/changes/deprecated/removed-and-deprecated.md)|Позволяет заранее узнать о будущих изменениях, которые могут повлиять на использование Configuration Manager.|
|[Обновления для Configuration Manager Current Branch](../servers/manage/updates.md)|Содержит описание удобного способа для применения обновлений компонентов к Configuration Manager в консоли.|
|[Получение доступных обновлений](../servers/manage/install-in-console-updates.md#get-available-updates)|Описание двух режимов для получения обновлений компонентов Configuration Manager.|
|[Контрольный список обновления](../servers/manage/install-in-console-updates.md#bkmk_beforeinstall)|Содержит контрольные списки обновления для конкретных версий, если это необходимо.| 
|[Установка обновлений компонентов Configuration Manager](../servers/manage/install-in-console-updates.md#bkmk_install)|Описывает простую установку обновлений компонентов.|
|[Поддержка Windows 10](../plan-design/configs/support-for-windows-10.md)|Содержит схему поддержки для версий Windows 10 (и ADK).|
|[Версии Technical Preview для Configuration Manager](../get-started/technical-preview.md)|Содержит сведения о программе Technical Preview для Configuration Manager.|


## <a name="key-articles-about-adopting-windows-as-a-service"></a>Ключевые материалы по внедрению модели Windows как услуга

| Статья        | Описание:          |
| ------------- |-------------|
|[Управление Windows как службой](../../osd/deploy-use/manage-windows-as-a-service.md)|Содержит сведения об использовании планов обслуживания для развертывания обновлений компонентов Windows 10.|
|[Обновление Windows 10 с помощью последовательности задач](../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md)|Сведения о создании последовательности задач для обновления Windows 10 с дополнительными рекомендациями.|
|[Поэтапные развертывания](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md)|Поэтапные развертывания автоматизируют согласованное и последовательное развертывание последовательности задач в нескольких коллекциях.|  
|[Оптимизация доставки обновлений Windows 10](../../sum/deploy-use/optimize-windows-10-update-delivery.md)|Использование Configuration Manager для управления содержимым обновления, чтобы поддерживать актуальность Windows 10.|
|[Использование Аналитики компьютеров](../../desktop-analytics/overview.md)|Аналитика компьютеров позволяет оценить и проанализировать готовность устройств в вашей среде к обновлению до Windows 10.|
|[Интеграция с Центром обновления Windows для бизнеса (дополнительно)](../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md)|Содержит сведения о том, как определять и развертывать обновления политики Центра обновления Windows для бизнеса с помощью Configuration Manager.|
|[Использование совместного управления с помощью Microsoft Intune и Центра обновления Windows для бизнеса (дополнительно)](../../comanage/overview.md)|Содержит общие сведения о совместном управлении.|


## <a name="related-articles"></a>Похожие статьи

- [Поддерживается обновление System Center 2012 Configuration Manager до Configuration Manager (Current Branch) на месте](../servers/deploy/install/upgrade-to-configuration-manager.md)
- [Планирование миграции на Configuration Manager (Current Branch)](../migration/planning-for-migration.md)
