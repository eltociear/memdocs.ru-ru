---
title: Регистрация корпоративных устройств macOS в службе управления | Документы Майкрософт
description: Описывает, как зарегистрировать устройство macOS в Intune, если оно приобретено и предоставлено вашей организацией.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/29/2018
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: japoehlm
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 4a20e1b26df1d07a80d8919f8e59e0d9117f891d
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/27/2020
ms.locfileid: "83880264"
---
# <a name="enroll-your-organization-provided-macos-device-in-management"></a>Регистрация корпоративных устройств macOS в службе управления

Узнайте, как настроить управление устройством macOS в Intune.  

Устройства, предоставленные вашей организацией, часто предварительно настроены еще до их получения вами. Ваша организация отправляет предварительно настроенные параметры на устройство после того, как вы включаете его и впервые выполняете вход. После завершения настройки устройства вы получите доступ к рабочим или учебным ресурсам.

Чтобы приступить к настройке управления, войдите, используя рабочую или учебную учетную запись. В оставшейся части этой статьи описываются действия и экраны помощника по настройке.

## <a name="what-is-apple-dep"></a>Что такое Программа регистрации устройств Apple?

Возможно, организация приобрела устройства по так называемой *Программе регистрации устройств Apple* (DEP). Некоторые организации покупают большое количество устройств с iOS или macOS через Apple DEP. Организации могут настраивать устройства и управлять ими с помощью любого поставщика управления мобильными устройствами, например Intune. Если вы являетесь администратором и хотите больше узнать об DEP, см. раздел [Автоматическая регистрация устройств macOS с помощью программы регистрации устройств от Apple](https://docs.microsoft.com/intune/enrollment/device-enrollment-program-enroll-macos).  

## <a name="get-your-device-managed"></a>Включение управления устройством

Выполните следующие действия, чтобы зарегистрировать устройство macOS в службе управления. Если вы используете личное, а не корпоративное устройство, следуйте указаниям для [личных устройств, использующихся в работе](enroll-your-device-in-intune-macos-cp.md).  

1. Включите устройства macOS.
2. Выберите страну или регион и нажмите кнопку **Продолжить**.  

   ![Снимок экрана — экран приветствия помощника по настройке устройства macOS со списком доступных языков.](./media/macos-dep-welcome-1808.png)
3. Выберите раскладку клавиатуры. В списке отображается один или несколько параметров в зависимости от выбранной страны или региона. Чтобы просмотреть все варианты раскладок независимо от страны или региона, щелкните **Показать все**. По завершении нажмите кнопку **Продолжить**.  

   ![Снимок экрана — экран раскладки клавиатуры в помощнике по настройке устройства macOS со списком языков клавиатуры для выбора, без флажка "Показать все" и с кнопками "Назад" и "Продолжить".](./media/macos-dep-keyboard-1808.png)  
4. Выберите сеть Wi-Fi. Необходимо иметь подключение к Интернету, чтобы продолжить установку. Если вы не видите сеть или хотите подключиться по проводной сети, нажмите **Другие параметры сети**. По завершении нажмите кнопку **Продолжить**.  

   ![Снимок экрана — экран выбора сети Wi-Fi в помощнике по настройке устройства macOS со списком доступных сетей на выбор. Также отображаются кнопки "Другие параметры сети", "Назад" и "Продолжить".](./media/macos-dep-wifi-1808.png)  
5. После подключения к сети Wi-Fi откроется экран **Удаленное управление**. Удаленное управление позволяет администратору вашей организации удаленно настраивать на устройстве необходимые учетные записи, параметры, приложения и сети. Чтобы понять принцип управления устройством, прочтите об удаленном управлении. Затем нажмите кнопку **Продолжить**.  

   ![Снимок экрана — экран удаленного управления в помощнике по настройке устройства macOS с описанием удаленного управления и ссылкой на документацию с дополнительными сведениями. Также показаны кнопки "Назад" и "Продолжить".](./media/macos-dep-remote-management-1-1808.png)  
6. При появлении запроса войдите в рабочую или учебную учетную запись. После проверки подлинности устройство установит профиль управления. Профиль настраивает и включает доступ к ресурсам вашей организации.  
7. Прочитайте о значке данных и конфиденциальности Apple, чтобы распознавать сбор персональных данных. Затем нажмите кнопку **Продолжить**.  

   ![Снимок экрана — экран данных и конфиденциальности в помощнике по настройке устройства macOS с изображением двух человек, пожимающих друг другу руки, и описанием использования Apple персональных данных. Также показаны кнопки "Назад" и "Продолжить".](./media/macos-dep-apple-data-privacy-1808.png)  
8. После регистрации устройства могут потребоваться дополнительные действия. Эти действия зависят от того, какой процесс настройки существует в вашей организации. Возможно, вам потребуется:
    * Войти в учетную запись Apple.
    * Принять условия.
    * Создать учетную запись компьютера.
    * Выполнить экспресс-настройку.
    * Настроить Mac.

## <a name="get-the-company-portal-app"></a>Получение приложения корпоративного портала

Скачайте приложение корпоративного портала Intune для macOS на свое устройство. Это приложение позволяет отслеживать, синхронизировать, добавлять и удалять устройства из службы управления, а также устанавливать приложения. Эти действия также предназначены для регистрации устройства на корпоративном портале.

1. На устройстве macOS перейдите по адресу [https://portal.manage.microsoft.com/EnrollmentRedirect.aspx](https://portal.manage.microsoft.com/EnrollmentRedirect.aspx).
2. Войдите на корпоративный портал, используя рабочую или учебную учетную запись. 
3. Нажмите кнопку **Get the App** (Получить приложение), чтобы скачать установщик корпоративного портала для macOS.
4. При появлении запроса откройте PKG-файл и выполните действия по установке.
5. Откройте приложение "Корпоративный портал" и выполните вход с рабочей или учебной учетной записью.
6. Найдите устройство и щелкните **Зарегистрировать**.
7. Последовательно нажмите кнопки **Продолжить** > **Готово**. Устройство должно появиться в приложении корпоративного портала как корпоративное и соответствующее.

По-прежнему нужна помощь? Обратитесь в службу поддержки вашей компании. Его контактные данные доступны на [веб-сайте корпоративного портала](https://go.microsoft.com/fwlink/?linkid=2010980).
