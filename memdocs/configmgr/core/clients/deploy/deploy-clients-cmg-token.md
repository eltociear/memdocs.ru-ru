---
title: Маркеры проверки подлинности в шлюзе управления облачными клиентами
titleSuffix: Configuration Manager
description: Зарегистрируйте клиент во внутренней сети для получения уникального маркера или создайте маркер групповой регистрации для интернет-устройств.
ms.date: 04/29/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: f0703475-85a4-450d-a4e8-7a18a01e2c47
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3a05c10d1f73fa0817febdd591190f6bc2ff0a0e
ms.sourcegitcommit: b7e5b053dfa260e7383a9744558d50245f2bccdc
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/29/2020
ms.locfileid: "82587277"
---
# <a name="token-based-authentication-for-cloud-management-gateway"></a>Проверка подлинности на основе маркеров для шлюза управления облачными клиентами

*Область применения: Configuration Manager (Current Branch)*

<!--5686290-->

Шлюз управления облачными клиентами (CMG) поддерживает многие типы клиентов, но даже при использовании [расширенного HTTP](../../plan-design/hierarchy/enhanced-http.md) этим клиентам требуется [сертификат проверки подлинности клиента](../manage/cmg/certificates-for-cloud-management-gateway.md#for-internet-based-clients-communicating-with-the-cloud-management-gateway). Такое требование к наличию сертификата может оказаться сложно обеспечить для интернет-клиентов, которые не так часто подключаются к внутренней сети, не могут присоединяться к Azure Active Directory (Azure AD) и для которых не предусмотрен метод установки сертификата, выданного PKI.

Начиная с версии 2002, Configuration Manager расширяет поддержку устройств с помощью следующих методов.

- Регистрация во внутренней сети для уникального маркера

- Создание маркера групповой регистрации для интернет-устройств

Чтобы воспользоваться преимуществами этих новых функций, после обновления сайта нужно также обновить клиенты до последней версии. Полный сценарий не работает, пока для клиента также не установлена последняя версия. При необходимости [повысьте уровень версии клиента до рабочей](../manage/upgrade/test-client-upgrades.md#to-promote-the-new-client-to-production).

Клиент Configuration Manager вместе с точкой управления управляют этим маркером, поэтому зависимости от версии ОС нет. Эта функция доступна для любой [поддерживаемой клиентами версии ОС](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md).

> [!NOTE]
> Эти методы поддерживают только сценарии управления, ориентированные на устройства.
>
> Корпорация Майкрософт рекомендует присоединить устройства к Azure AD. Интернет-устройства могут использовать Azure AD для проверки подлинности в Configuration Manager. Кроме того, это позволяет выполнять сценарии как с устройствами, так и с пользователями, когда устройство подключено к Интернету или внутренней сети. Дополнительные сведения см. в разделе [Установка и регистрация клиента с помощью удостоверений Azure AD](deploy-clients-cmg-azure.md#install-and-register-the-client-using-azure-ad-identity).

## <a name="register-on-the-internal-network"></a>Регистрация во внутренней сети

Для использования этого метода требуется, чтобы клиент сначала зарегистрировался в точке управления во внутренней сети. Регистрация клиента обычно происходит сразу после установки. Точка управления предоставляет клиенту уникальный маркер, в котором указано, что он использует самозаверяющий сертификат. Когда клиент переключается в Интернет, для взаимодействия с CMG он связывает свой самозаверяющий сертификат с маркером, выданным точкой управления. Клиент обновляет маркер раз в месяц; срок его действия составляет 90 дней.

Такое поведение сайта является поведением по умолчанию.

## <a name="create-a-bulk-registration-token"></a>Создание маркера групповой регистрации

Если не удается установить и зарегистрировать клиенты во внутренней сети, создайте маркер групповой регистрации. Используйте этот маркер при установке клиента на интернет-устройство и регистрации через CMG. Срок действия маркера групповой регистрации достаточно короткий, и он не хранится на клиенте или на сайте. Он позволяет клиенту сгенерировать уникальный маркер, который связан с его самозаверяющим сертификатом, что позволяет выполнить проверку подлинности с помощью CMG.

1. Войдите на сервер сайта верхнего уровня в иерархии с правами локального администратора.

1. Откройте командную строку как администратор.

1. Запустите инструмент из папки `\bin\X64` каталога установки Configuration Manager на сервере сайта: `BulkRegistrationTokenTool.exe`. Создайте новый маркер с параметром `/new`. Например, `BulkRegistrationTokenTool.exe /new`. Дополнительные сведения см. в разделе [Использование средства маркера групповой регистрации](#bulk-registration-token-tool-usage).

1. Скопируйте маркер и сохраните его в безопасном месте.

1. Установите клиент Configuration Manager на интернет-устройство. Добавьте параметр установки клиента: [ **/regtoken**](about-client-installation-properties.md#regtoken). В следующем примере в командной строке имеются другие обязательные параметры и свойства установки:

    `ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC SMSMP=https://mp1.contoso.com /regtoken:eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik9Tbzh2Tmd5VldRUjlDYVh5T2lacHFlMDlXNCJ9.eyJTQ0NNVG9rZW5DYXRlZ29yeSI6IlN7Q01QcmVBdXRoVG9rZW4iLCJBdXRob3JpdHkiOiJTQ0NNIiwiTGljZW5zZSI6IlNDQ00iLCJUeXBlIjoiQnVsa1JlZ2lzdHJhdGlvbiIsIlRlbmFudElkIjoiQ0RDQzVFOTEtMEFERi00QTI0LTgyRDAtMTk2NjY3RjFDMDgxIiwiVW5pcXVlSWQiOiJkYjU5MWUzMy1wNmZkLTRjNWItODJmMy1iZjY3M2U1YmQwYTIiLCJpc3MiOiJ1cm46c2NjbTpvYXV0aDI6Y2RjYzVlOTEtMGFkZi00YTI0LTgyZDAtMTk2NjY3ZjFjMDgxIiwiYXVkIjoidXJuOnNjY206c2VydmljZSIsImV4cCI6MTU4MDQxNbUwNSwibmJmIjoxNTgwMTU2MzA1fQ.ZUJkxCX6lxHUZhMH_WhYXFm_tbXenEdpgnbIqI1h8hYIJw7xDk3wv625SCfNfsqxhAwRwJByfkXdVGgIpAcFshzArXUVPPvmiUGaxlbB83etUTQjrLIk-gvQQZiE5NSgJ63LCp5KtqFCZe8vlZxnOloErFIrebjFikxqAgwOO4i5ukJdl3KQ07YPRhwpuXmwxRf1vsiawXBvTMhy40SOeZ3mAyCRypQpQNa7NM3adCBwUtYKwHqiX3r1jQU0y57LvU_brBfLUL6JUpk3ri-LSpwPFarRXzZPJUu4-mQFIgrMmKCYbFk3AaEvvrJienfWSvFYLpIYA7lg-6EVYRcCAA`

    > [!TIP]
    > Дополнительные сведения об этой командной строке см. в разделе [Установка и регистрация клиента с помощью удостоверений Azure AD](deploy-clients-cmg-azure.md#install-and-register-the-client-using-azure-ad-identity). Этот процесс аналогичен указанному в разделе за тем исключением, что в нем не используются свойства Azure AD.

### <a name="known-issues"></a>Известные проблемы

Невозможно создать маркер групповой регистрации на сайте с сервером сайта в пассивном режиме.<!-- 6399087 -->

### <a name="bulk-registration-token-tool-usage"></a>Использование средства маркера групповой регистрации

Средство `BulkRegistrationTokenTool.exe` находится в папке `\bin\X64` каталога установки Configuration Manager на сервере сайта. Войдите на сервер сайта и запустите его от имени администратора. В командной строке поддерживаются следующие параметры.

- `/?`
- `/new`
- `/lifetime`

#### <a name=""></a>/?

Отображает сведения об использовании.

Пример: `BulkRegistrationTokenTool.exe /?`

#### <a name="new"></a>/new

Создание нового маркера групповой регистрации.

Пример: `BulkRegistrationTokenTool.exe /new`

Это средство отображает следующие сведения:
  
- Идентификатор GUID, используемый сайтом для отслеживания выданных маркеров
- Период действия маркера по умолчанию — три дня.
- Маркер групповой регистрации.

Маркер не хранится на клиенте или на сайте. Не забудьте скопировать маркер из командной строки и сохранить его в безопасном месте.

#### <a name="lifetime"></a>/lifetime

Используйте с параметром `/new`, чтобы указать срок действия маркера. Укажите целочисленное значение в минутах. Значение по умолчанию — 4320 (три дня). Максимальное значение — 10 080 (семь дней).

Пример: `BulkRegistrationTokenTool.exe /lifetime:4320`

## <a name="see-also"></a>См. также

- [Планирование шлюза управления облачными клиентами](../manage/cmg/plan-cloud-management-gateway.md)

- [Установка и назначение клиентов Configuration Manager для Windows 10 с проверкой подлинности при помощи Azure AD](deploy-clients-cmg-azure.md)
