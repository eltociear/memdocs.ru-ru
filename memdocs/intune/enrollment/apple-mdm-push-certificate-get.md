---
title: Получение сертификата Apple MDM Push Сertificate для Intune
titleSuffix: ''
description: Узнайте, как получить Apple MDM Push Certificate для управления устройствами iOS и iPadOS с помощью Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/08/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 6f67fcd2-5682-4f9c-8d74-d4ab69dc978c
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: a66171d678ffd19e424fb399633c3fed3db9a588
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/27/2020
ms.locfileid: "83987009"
---
# <a name="get-an-apple-mdm-push-certificate"></a>Получение сертификата MDM Push Certificate

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Для управления устройствами с iOS, iPadOS и macOS с помощью Intune требуется Apple MDM Push Certificate. После добавления сертификата в Intune пользователи смогут регистрировать свои устройства с помощью:

- приложения корпоративного портала;

- способов массовой регистрации Apple, таких как программа регистрации устройств, Apple School Manager или Apple Configurator.

См. сведения о [вариантах регистрации устройств iOS и iPadOS](ios-enroll.md).

Сертификат Push Certificate с истекшим сроком действия необходимо обновить. При обновлении следует использовать тот же идентификатор Apple ID, который применялся при создании сертификата Push Certificate.


## <a name="steps-to-get-your-certificate"></a>Порядок получения сертификата
Войдите в [Центр администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), выберите **Устройства** > **Регистрация устройств** > **Регистрация Apple** > **Apple MDM Push Certificate**, а затем выполните следующие действия.

### <a name="step-1-grant-microsoft-permission-to-send-user-and-device-information-to-apple"></a>Шаг 1. Предоставление корпорации Майкрософт разрешения на отправку сведения о пользователях и устройствах в Apple
Выберите **Даю согласие**, чтобы разрешить корпорации Майкрософт отправлять данные в Apple.

![Экран настройки сертификата MDM Push Certificate без настройки MDM Push.](./media/apple-mdm-push-certificate-get/create-mdm-push-certificate.png)

### <a name="step-2-download-the-intune-certificate-signing-request-required-to-create-an-apple-mdm-push-certificate"></a>Шаг 2. Скачивание запроса на подписание сертификата Intune, необходимого для создания сертификата Apple MDM Push Certificate
Выберите **Скачать CSR**, чтобы скачать CSR-файл и сохранить его локально. Файл используется для запроса сертификата отношений доверия с портала сертификатов Apple Push.

### <a name="step-3-create-an-apple-mdm-push-certificate"></a>Шаг 3. Создание сертификата Apple MDM Push Certificate
Выберите **Создать собственный сертификат MDM Push Certificate**, чтобы перейти на портал сертификатов Apple Push. Войдите с помощью идентификатора Apple ID компании и нажмите кнопку **Создать сертификат**. Щелкните **Выбрать файл**, перейдите к файлу запроса подписи сертификата, а затем выберите **Отправить**. На странице подтверждения нажмите кнопку **Скачать**, чтобы скачать файл сертификата (PEM) и сохранить его локально.

> [!NOTE]
> Сертификат связан с идентификатором Apple ID, который использовался при его создании. Рекомендуется использовать корпоративный идентификатор Apple для выполнения задач управления. Также следует убедиться в том, что почтовый ящик просматривается несколькими пользователями, как и список рассылки. Никогда не используйте личный идентификатор Apple ID.

### <a name="step-4-enter-the-apple-id-used-to-create-your-apple-mdm-push-certificate"></a>Шаг 4. Ввод идентификатора Apple ID, который использовался для создания сертификата Apple MDM Push Certificate
Запишите этот идентификатор как напоминание о времени, когда его потребуется обновить.

### <a name="step-5-browse-to-your-apple-mdm-push-certificate-to-upload"></a>Шаг 5. Переход к сертификату Apple MDM Push Certificate для отправки
Перейдите к файлу сертификата (PEM) и щелкните **Открыть**, а затем выберите **Передать**. С помощью push-сертификата Intune может регистрировать устройства Apple и управлять ими.

## <a name="renew-apple-mdm-push-certificate"></a>Продлите сертификат Apple MDM Push Certificate.
Сертификат Apple MDM Push Certificate действителен в течение одного года. Чтобы иметь возможность и дальше управлять устройствами iOS, iPadOS и macOS, этот сертификат необходимо продлевать ежегодно. После истечения срока действия сертификата вы не сможете связаться с зарегистрированными устройствами Apple.

Сертификат связан с идентификатором Apple ID, который использовался при его создании. Продлите сертификат MDM Push Certificate с тем же идентификатором Apple ID, который использовался для создания сертификата.

1. Войдите в [Центр администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), выберите **Устройства** > **Регистрация устройств** > **Регистрация Apple** > **Apple MDM Push Certificate**.
2. Выберите **Скачать CSR**, чтобы скачать CSR-файл и сохранить его локально. Файл используется для запроса сертификата отношений доверия с портала сертификатов Apple Push.
3. Выберите **Создать собственный сертификат MDM Push Certificate**, чтобы перейти на портал сертификатов Apple Push. Найдите сертификат, который требуется продлить, и выберите **Продлить**.
4. На экране **Продление сертификата Push Certificate** укажите сведения для идентификации сертификата в будущем, затем нажмите кнопку **Выбрать файл**, выберите новый файл запроса, который был загружен, и нажмите кнопку **Отправить**.
   > [!TIP]
   > Сертификат можно определить по идентификатору пользователя. Чтобы определить часть идентификатора пользователя, представляющую собой идентификатор GUID, просмотрите запись **Идентификатор темы** в сведениях о сертификате. На зарегистрированном устройстве iOS или iPadOS щелкните **Настройки** > **Общие** > **Управление** **устройством** > **Профиль управления** > **Подробнее** > **Профиль управления**. Во второй строке (**Раздел**) содержится уникальный идентификатор GUID, который можно сопоставить с сертификатом на портале сертификатов Apple Push.
 
6. В окне **Подтверждение** нажмите кнопку **Скачать** и сохраните PEM-файл локально.
7. В [Intune](https://go.microsoft.com/fwlink/?linkid=2090973) щелкните значок **Сертификат Apple MDM Push Certificate**, выберите PEM-файл, полученный от Apple, и нажмите кнопку **Отправить**.

Состояние сертификата Apple MDM Push Certificate изменится на **Активный**, а до истечения срока его действия останется 365 дней.
