---
title: Удаленная поддержка мобильных устройств под управлением Intune
description: На выбор предлагается четыре разных варианта удаленной поддержки пользователей с мобильными устройствами.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/20/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 34f88d4e7aefe9a32238bb6d14203de0defd65ef
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988262"
---
# <a name="remotely-assist-mobile-devices-managed-by-microsoft-endpoint-manager"></a>Удаленная поддержка мобильных устройств под управлением Microsoft Endpoint Manager

На выбор предлагается четыре варианта удаленного администрирования устройств под управлением Microsoft Endpoint Manager.

- [Microsoft Teams](https://products.office.com/microsoft-teams/) — это центр для совместной работы, где вы можете общаться, проводить собрания и работать вместе, где бы вы ни были.
- [Быстрая поддержка](https://support.microsoft.com/help/4027243/windows-10-solve-pc-problems-with-quick-assist) — это приложение Windows 10, которое позволяет двум людям совместно использовать устройство через удаленное подключение.
- [TeamViewer](https://www.teamviewer.com/) — это программа стороннего производителя, которая приобретается отдельно. Она предоставляет исчерпывающий набор возможностей для удаленного доступа и поддержки. [Интеграция Intune и TeamViewer](teamviewer-support.md) обеспечивает удаленную поддержку с помощью TeamViewer, а управление соединителем осуществляется непосредственно в Intune.
- [Удаленное управление](https://docs.microsoft.com/configmgr/core/clients/manage/remote-control/introduction-to-remote-control) включено в состав Microsoft Endpoint Configuration Manager. Оно используется для удаленного администрирования, поддержки или просмотра любого компьютера рабочей группы и компьютера, присоединенного к домену.

| Функции, платформы, лицензии | **Teams** | Быстрая поддержка | TeamViewer (Intune) | Удаленное управление (ConfigMgr) |
|:---:|:---:|:---:|:---:|:---:|
| Удаленные просмотр и управление |![Флажок](../enrollment/media/enrollment-method-capab/checkmark.png)|![Флажок](../enrollment/media/enrollment-method-capab/checkmark.png)|![Флажок](../enrollment/media/enrollment-method-capab/checkmark.png)|![Флажок](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Чат |![Флажок](../enrollment/media/enrollment-method-capab/checkmark.png)||![Флажок](../enrollment/media/enrollment-method-capab/checkmark.png)||
| Передача файлов |![Флажок](../enrollment/media/enrollment-method-capab/checkmark.png)|![Флажок](../enrollment/media/enrollment-method-capab/checkmark.png)|![Флажок](../enrollment/media/enrollment-method-capab/checkmark.png)|![Флажок](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Административный доступ с повышенными правами |||![Флажок](../enrollment/media/enrollment-method-capab/checkmark.png)|![Флажок](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Автоматический доступ |||![Флажок](../enrollment/media/enrollment-method-capab/checkmark.png)|![Флажок](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Одновременное удаленное управление |![Флажок](../enrollment/media/enrollment-method-capab/checkmark.png)|![Флажок](../enrollment/media/enrollment-method-capab/checkmark.png)|||
| Поддержка нескольких пользователей |||![Флажок](../enrollment/media/enrollment-method-capab/checkmark.png)|![Флажок](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Удаленные действия ||![Флажок](../enrollment/media/enrollment-method-capab/checkmark.png)|![Флажок](../enrollment/media/enrollment-method-capab/checkmark.png)|![Флажок](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Поддержка через Интернет |![Флажок](../enrollment/media/enrollment-method-capab/checkmark.png)|![Флажок](../enrollment/media/enrollment-method-capab/checkmark.png)|![Флажок](../enrollment/media/enrollment-method-capab/checkmark.png)||
| Отчетность по результатам аудита |![Флажок](../enrollment/media/enrollment-method-capab/checkmark.png)||![Флажок](../enrollment/media/enrollment-method-capab/checkmark.png)|![Флажок](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Поддержка всех платформ (Windows, iOS, Android, macOS) |![Флажок](../enrollment/media/enrollment-method-capab/checkmark.png)||![Флажок](../enrollment/media/enrollment-method-capab/checkmark.png)||
| Интеграция с Windows 10: дополнительное приложение не требуется ||![Флажок](../enrollment/media/enrollment-method-capab/checkmark.png)|||
| Требуется устройство, которое будет находиться под совместным управлением Configuration Manager и Intune ||||![Флажок](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Требуется дополнительная лицензия\* |![Флажок](../enrollment/media/enrollment-method-capab/checkmark.png)||![Флажок](../enrollment/media/enrollment-method-capab/checkmark.png)|![Флажок](../enrollment/media/enrollment-method-capab/checkmark.png)|

\* Для Teams требуется лицензия на O365 или M365. Для использования TeamViewer и Intune требуются лицензии на эти продукты. Удаленное управление — это функция Configuration Manager, поэтому для него требуется лицензия на Configuration Manager.
