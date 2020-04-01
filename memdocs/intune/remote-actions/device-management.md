---
title: Управление устройствами с помощью Microsoft Intune в Azure | Документы Майкрософт
description: Просмотр устройств, управляемых с помощью Microsoft Intune, включая экспорт списка устройств в CSV-формат, просмотр устройств, присоединенных к Azure Active Directory, просмотр журнала изменений выполняемых действий на устройстве, использование TeamViewer Connector для удаленного устранения неполадок на устройствах Android ИТ-администраторами и просмотр всех действий, которые можно выполнять на устройствах.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 11/14/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: d2412418-d91a-4767-a3d6-bc88bb29caa2
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 98451e7ffd6aef9e5fb298af96b91074f39c383e
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/27/2020
ms.locfileid: "80325271"
---
# <a name="what-is-microsoft-intune-device-management"></a>Что такое управление устройствами с помощью Microsoft Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

ИТ-администратор должен сделать так, чтобы управляемые устройства предоставляли ресурсы, необходимые пользователям для выполнения работы, с одновременной защитой этих данных от риска.

Рабочая нагрузка **Устройства** позволяет получить сведения об управляемых устройствах и активировать удаленные задачи на этих устройствах.

## <a name="get-to-your-devices"></a>Доступ к устройствам

1. Войдите в [Центр администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
3. Выберите **Устройства**. В этом представлении отображаются подробные сведения об отдельных устройствах, а также выполняемые на них действия.

   - В разделе **Общие сведения** приведены снимок зарегистрированных устройств, количество устройств, использующих различные платформы, и другие сведения.
   - В разделе **Все устройства** отображается список зарегистрированных управляемых устройств.

     Функция **Экспорт** позволяет создать ZIP-список всех устройств с шагом 10 000 (Internet Explorer) или 30 000 (Microsoft Edge, Chrome).

     Выберите любое устройство, чтобы [просмотреть дополнительные сведения об этом устройстве](device-inventory.md), такие как сведения об оборудовании, установленные приложения, политики и др.

   - В разделе **Устройства Azure AD** отображается список устройств, зарегистрированных или присоединенных к Azure Active Directory (Azure AD). Дополнительные сведения об [управлении устройствами Azure AD](https://docs.microsoft.com/azure/active-directory/device-management-introduction).
   - **Действия устройства** — журнал удаленных действий, выполненных на разных устройствах, включая действие, его состояние, пользователя, который инициировал действие, и время.

     ![Снимок экрана: мониторинг действий устройств](./media/device-management/monitor-device-actions.png)

   - В **журналы аудита** записываются действия, которые генерируют изменения в Intune. В [журналах аудита](../fundamentals/monitor-audit-logs.md) содержатся более подробные сведения.
   - **TeamViewer Connector** — это служба, которая позволяет пользователям устройств Android, управляемым Intune, получать удаленную помощь от ИТ-администраторов. Дополнительные сведения о [TeamViewer](teamviewer-support.md).
   - В разделе **Справка и поддержка** находится ярлык на советы по устранению неполадок, обращению в службу поддержки или проверке состояния Intune.

## <a name="available-device-actions"></a>Доступные действия на устройствах
Доступные действия зависят от платформы и конфигурации устройства.

- [Просмотр данных по инвентаризации устройств](device-inventory.md)
- Выполнение действий удаленного устройства
  - [Сброс Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot-reset#reset-devices-with-remote-windows-autopilot-reset)
  - [Смена ключа BitLocker](../protect/encrypt-devices.md#rotate-bitlocker-recovery-keys) (только в Windows)
  - [Удалить](devices-wipe.md#delete-devices-from-the-intune-portal)
  - [Отключение блокировки активации](device-activation-lock-disable.md) (только iOS)
  - [Новый запуск](device-fresh-start.md) (только Windows)
  - [Полная проверка](../configuration/device-restrictions-windows-10.md#microsoft-defender-antivirus) (только Windows 10)
  - [Найти устройство](device-locate.md) (только iOS)
  - [Режим пропажи](device-lost-mode.md) (только iOS)
  - [Быстрая проверка](../configuration/device-restrictions-windows-10.md#microsoft-defender-antivirus) (только Windows 10)
  - [Удаленное управление устройством Android](teamviewer-support.md)
  - [Удаленная блокировка](device-remote-lock.md).
  - [Переименование устройства](device-rename.md)
  - [Сбросить секретный код](device-passcode-reset.md)
  - [Перезапуск](device-restart.md) (только Windows)
  - [Прекратить использование](devices-wipe.md#retire)
  - [Обновление аналитики безопасности Защитника Windows](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-antivirus/manage-protection-updates-windows-defender-antivirus)
  - [Сброс ПИН-кода для Windows 10](device-windows-pin-reset.md)
  - [Очистка](devices-wipe.md#wipe)
  - [Отправка пользовательских уведомлений](custom-notifications.md#send-a-custom-notification-to-a-single-device) (Android, iOS, iPadOS)
  - [Синхронизация устройств](device-sync.md)
- [Массовые действия устройств](bulk-device-actions.md)

## <a name="next-steps"></a>Дальнейшие шаги

- В разделе **Все устройства** выберите устройство, чтобы просмотреть о нем дополнительные сведения.
- Выберите **Действия устройства** для просмотра состояния действий, выполняемых на управляемых устройствах.
