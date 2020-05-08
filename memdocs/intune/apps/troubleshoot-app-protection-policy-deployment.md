---
title: Устранение неполадок при развертывании политики защиты приложений Intune
description: Описываются способы устранения неполадок, которые могут возникать при развертывании политик защиты приложений Intune.
author: simonxjx
manager: dcscontentpm
localization_priority: Normal
search.appverid:
- MET150
audience: ITPro
ms.date: 4/17/2020
ms.service: microsoft-intune
ms.topic: conceptual
ms.author: v-six
ms.custom: CSSTroubleshoot
appliesto:
- Intune
ms.openlocfilehash: 3b4c02e366f4778e65b4fe4c853ed147fcdb1df3
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2020
ms.locfileid: "82072758"
---
# <a name="troubleshooting-app-protection-policy-deployment-in-intune"></a>Устранение неполадок при развертывании политики защиты приложений в Intune

## <a name="introduction"></a>Введение

Эта статья поможет вам в выявлении и устранении проблем при применении политик защиты приложений в Microsoft Intune. Обратитесь к разделам, которые относятся к вашей ситуации.

## <a name="basic-steps"></a>Основные шаги

### <a name="collect-initial-data"></a>Сбор начальных данных

Перед тем как приступить к устранению неполадок, следует собрать базовые сведения, чтобы лучше понять проблему и сократить время на поиск решения.

Соберите следующие сведения:

- Какой параметр политики не был применен? Была ли применена хотя бы одна политика?
- Что происходит на стороне пользователей? Установили и запустили ли пользователи целевое приложение?
- Когда появилась проблема? Работала или защита приложений вообще?
- На какой платформе возникает проблема (Android или iOS)?
- Сколько пользователей затронуто? Затронуты ли все устройства или только некоторые из них?
- Сколько затронуто устройств? Затронуты ли все устройства или только некоторые из них?
- Хотя политика защиты приложений Intune не требует наличия службы управления мобильными устройствами (MDM), используют ли затронутые пользователи Intune или стороннее решение EMM?
- Затронуты ли все управляемые приложения или только некоторые из них? Например, могут быть затронуты бизнес-приложения с [Intune App SDK](../developer/app-sdk-get-started.md), но не приложения магазина.

Теперь можно начать устранение неполадок на основе ответов на эти вопросы.

### <a name="verify-prerequisites"></a>Проверка необходимых условий

Следующий шаг — проверка выполнения всех необходимых условий.

Хотя политики защиты приложений Intune можно использовать независимо от любого решения MDM, должны выполняться указанные ниже предварительные требования.

- Пользователю должна быть назначена лицензия Intune.
- Пользователь должен быть включен в группу безопасности, на которую распространяется политика защиты приложений. Эта же политика защиты приложений должна распространяться и на определенное используемое приложение.
- На устройствах Android для применения политик защиты приложений требуется приложение "Корпоративный портал".
- При использовании приложения [Word, Excel или PowerPoint](https://products.office.com/business/office) должны выполняться указанные ниже дополнительные требования.
    - У пользователя должна быть лицензия на [Microsoft 365 для бизнеса или предприятий](https://products.office.com/business/compare-more-office-365-for-business-plans), связанная с его учетной записью Azure Active Directory (Azure AD). Подписка должна включать приложения Office на мобильных устройствах и может включать облачную учетную запись хранения с поддержкой [OneDrive для бизнеса](https://onedrive.live.com/about/business/). Лицензии Office 365 можно назначить в [Центре администрирования Microsoft 365](https://admin.microsoft.com), следуя [этим инструкциям](https://support.office.com/article/Assign-or-remove-licenses-for-Office-365-for-business-997596b5-4173-4627-b915-36abac6786dc).
    - У пользователя должно быть управляемое расположение, настроенное с помощью функции **Сохранить как**. Эта команда находится в параметре политики защиты приложений **Сохранение копий корпоративных данных**. Например, если управляемое расположение — [OneDrive](https://onedrive.live.com/about/), приложение OneDrive должно быть настроено в приложении Word, Excel или PowerPoint пользователя.
    - Если управляемое расположение — OneDrive, на приложение должна распространяться политика защиты, развернутая для пользователя.

  > [!NOTE]
  > Мобильные приложения Office в настоящее время поддерживают только SharePoint Online, но не локальное приложение SharePoint.

- Если вы используете политики защиты приложений Intune вместе с локальными ресурсами (Microsoft Skype для бизнеса и Microsoft Exchange Server), необходимо включить [гибридную современную проверку подлинности (HMA) для Skype для бизнеса и Exchange](https://docs.microsoft.com/office365/enterprise/hybrid-modern-auth-overview).

Политики защиты приложений Intune требуют соответствия удостоверений пользователя в приложении и в [Intune App SDK](../developer/app-sdk-get-started.md). Единственный способ обеспечить такое соответствие — использовать современную проверку подлинности. Есть сценарии, в которых приложения могут работать в локальной конфигурации без современной проверки подлинности. Однако результат не гарантируется и может отличаться от ожидаемого.

Дополнительные сведения о включении HMA для гибридных и локальных конфигураций Skype для бизнеса см. в следующих статьях:

- **Гибридная**<br>
[Выход общедоступной версии гибридной современной проверки подлинности для Skype для бизнеса и Exchange](https://techcommunity.microsoft.com/t5/Skype-for-Business-Blog/Hybrid-Modern-Auth-for-SfB-and-Exchange-goes-GA/ba-p/134756)

- **Локальная**<br>
[Современная проверка подлинности для локальной версии Skype для бизнеса с AAD](https://techcommunity.microsoft.com/t5/Skype-for-Business-Blog/Modern-Auth-for-SfB-OnPrem-with-AAD/ba-p/180910)

### <a name="check-app-protection-policy-status"></a>Проверка состояния политики защиты приложений

Чтобы проверить состояние защиты приложений, выполните указанные ниже действия.

1. Войдите в [Центр администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Выберите **Приложения** > **Монитор** > **Состояние защиты приложений** и щелкните плитку **Назначенные пользователи**.
3. На странице **Отчеты по приложению** выберите **Выбрать пользователя**, чтобы вывести список пользователей и групп.
4. Найдите и выберите в списке одного из затронутых пользователей, а затем нажмите **Выбрать пользователя**. В верхней части области "Отчеты по приложению" отображаются сведения о том, есть ли у пользователя лицензия на защиту приложений и лицензия на Office 365. Можно также просмотреть состояние приложения для всех устройств пользователя.
5. Запишите такие важные сведения, как целевые приложения, типы устройств, политики, состояние синхронизации устройств и время последней синхронизации.

> [!NOTE]
> Политики защиты приложений применяются только в том случае, если приложения используются в рабочем контексте, например, когда пользователь получает доступ к приложениям с помощью рабочей учетной записи.

Дополнительные сведения см. в статье [Проверка настройки политики защиты приложений в Microsoft Intune](../apps/app-protection-policies-validate.md).

### <a name="verify-that-user-identity-is-consistent-between-app-and-intune-app-sdk"></a>Проверка согласованности удостоверений пользователя в приложении и Intune App SDK

В большинстве случаев пользователи входят в свои учетные записи с помощью имени субъекта-пользователя. Однако в некоторых средах (например, в локальных) пользователи могут использовать для входа другую форму учетных данных. В таких случаях имя субъекта-пользователя, используемое в приложении, может отличаться от объекта имени субъекта-пользователя в Azure AD. При возникновении этой проблемы политики защиты приложений применяются не так, как ожидается.

Корпорация Майкрософт рекомендует сопоставлять имя субъекта-пользователя с основным SMTP-адресом. Эта практика позволяет пользователям входить в управляемые приложения, систему защиты приложений Intune и другие ресурсы Azure AD, используя одно и то же удостоверение. Дополнительные сведения см. в статье [Указание атрибута UserPrincipalName в Azure AD](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-userprincipalname).

Если в среде требуются альтернативные методы входа, см. статью [Настройка альтернативного идентификатора входа](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/configuring-alternate-login-id), в частности раздел [Гибридная современная проверка подлинности с альтернативным идентификатором](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/configuring-alternate-login-id#hybrid-modern-authentication-with-alternate-id).

### <a name="verify-that-the-user-is-targeted"></a>Проверка применения политик к пользователю

Политики защиты приложений Intune должны применяться к пользователям. Если не назначить политику защиты приложений пользователю или группе пользователей, политика не применяется.

Чтобы проверить, применяется ли политика к целевому пользователю, выполните указанные ниже действия.

1. Войдите в [Центр администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Выберите **Приложения** > **Монитор** > **Состояние защиты приложений**, а затем выберите плитку **Состояние пользователя** (в зависимости от платформы ОС устройства).
В открывшейся области **Отчеты по приложению** выберите пункт **Выбрать пользователя** для поиска пользователя.
3. Выберите пользователя в списке. Отобразятся подробные сведения для этого пользователя.

Если политика назначена группе пользователей, убедитесь в том, что пользователь входит в эту группу. Для этого выполните следующие действия.

1. Войдите в [Центр администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Выберите **Группы > Все группы**, а затем найдите и выберите группу, используемую для назначения политики защиты приложений.
3. В разделе **Управление** выберите **Участники**.
4. Если затронутого пользователя нет в списке, ознакомьтесь со статьей [Управление доступом к приложениям и ресурсам с помощью групп Azure Active Directory](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-manage-groups) и правилами членства в группах. Убедитесь в том, что затронутый пользователь входит в группу.
5. Убедитесь в том, что затронутый пользователь не входит ни в одну из исключенных из политики групп.

> [!IMPORTANT]
> - Политика защиты приложений Intune должна назначаться группам пользователей, а не группам устройств.
> - Если на затронутом устройстве используется Программа регистрации устройств Apple (DEP), убедитесь в том, что включено **сопоставление пользователей**. Сопоставление пользователей необходимо для всех приложений, требующих проверку подлинности пользователей в рамках DEP.
> - Если на затронутом устройстве используется Android Enterprise, политики защиты приложений будут поддерживаться только рабочими профилями.


### <a name="verify-that-the-managed-app-is-targeted"></a>Проверка применения политик к управляемому приложению

При настройке политик защиты приложений Intune целевые приложения должны использовать [Intune App SDK](../developer/app-sdk-get-started.md). В противном случае политики могут работать неправильно.

Убедитесь в том, что целевое приложение имеется в списке [защищенных приложений Microsoft Intune](../apps/apps-supported-intune-apps.md). Бизнес-приложения и пользовательские приложения должны использовать последнюю версию [Intune App SDK](../developer/app-sdk-get-started.md). Обратите внимание на следующее.

Для iOS это очень важно, так как каждая версия содержит исправления, которые влияют на применение этих политик и их функционирование. Дополнительные сведения см. на странице [выпусков пакета Intune App SDK для iOS](https://github.com/msintuneappsdk/ms-intune-app-sdk-ios/releases).
Для Android это не так важно. Однако у пользователей должна быть установлена последняя версия приложения "Корпоративный портал", так как оно выступает в роли агента брокера политик.

> [!NOTE]
> Начиная с сентября 2019 г. Intune переходит на поддержку приложений для iOS с пакетом Intune App SDK 8.1.1 и более поздних версий. Приложения, созданные с использованием версий пакета SDK до версии 8.1.1, больше не поддерживаются. 

## <a name="more-information"></a>Дополнительные сведения

### <a name="special-requirements-for-intune-mdm-managed-devices"></a>Особые требования для устройств под управлением Intune MDM

При создании политики защиты приложений ее можно назначить всем типам приложений или приложениям следующих типов:

- приложения на неуправляемых устройствах;
- приложения на управляемых устройствах Intune;
- приложения в рабочем профиле Android.

> [!NOTE] 
> Чтобы указать типы приложений, задайте для параметра **Предназначены для всех типов приложений** значение **Нет**, а затем выберите типы в списке **Типы приложений**.

Для iOS требуются следующие дополнительные [параметры конфигурации приложений](../apps/app-configuration-policies-use-ios.md) для применения параметров политики защиты приложений (APP) к приложениям на устройствах, зарегистрированных в Intune:

- Для всех приложений, управляемых MDM (Intune или сторонним решением EMM), необходимо настроить **IntuneMAMUPN**. Дополнительные сведения см. в статье "Настройка пользовательского параметра имени участника-пользователя для Microsoft Intune или стороннего решения EMM".
- Для всех сторонних приложений и бизнес-приложений, управляемых MDM, необходимо настроить **IntuneMAMDeviceID**.
- Параметру **IntuneMAMDeviceID** необходимо присвоить маркер идентификатора устройства. Пример: key=IntuneMAMDeviceID, value={{deviceID}}. См. сведения о [добавлении политик конфигурации приложений для управляемых устройств iOS](../apps/app-configuration-policies-use-ios.md).
- Если настроить только значение **IntuneMAMDeviceID**, Intune APP будет распознавать устройство как неуправляемое.

### <a name="scenario-policy-changes-are-not-working"></a>Сценарий: изменения политики не работают
[Intune App SDK](../developer/app-sdk-get-started.md) регулярно проверяет изменения политик. Однако этот процесс может быть отложен по одной из следующих причин:

- Приложение не синхронизировалось со службой.
- Приложение "Корпоративный портал" было удалено с устройства.

Политика защиты приложений Intune использует удостоверение пользователя. Поэтому требуются допустимое имя входа в приложение, использующее рабочую или учебную учетную запись, и соответствующее подключение к службе. Если пользователь не выполнил вход в приложение или приложение "Корпоративный портал" было удалено с устройства, обновления политик не применяются.

Кроме того, применение изменений и обновлений политики защиты приложений может занять до 8 часов. Закрытие всех приложений и перезапуск устройства обычно ускоряют применение обновлений политики.

Чтобы проверить состояние защиты приложений, выполните указанные ниже действия.

1. Войдите в [Центр администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Выберите **Приложения** > **Монитор** > **Состояние защиты приложений** и щелкните плитку **Назначенные пользователи**.
3. На странице "Отчеты по приложению" нажмите **Выбрать пользователя**, чтобы вывести список пользователей и групп.
4. Найдите и выберите в списке одного из затронутых пользователей, а затем нажмите **Выбрать пользователя**.
5. Проверьте примененные политики, включая состояние и время последней синхронизации.
6. Если состояние — **Не записано после изменений** или указано, что синхронизация в последнее время не проводилась, проверьте, есть ли у пользователя соответствующее сетевое подключение. В случае с Android проверьте, установлена ли у пользователей последняя версия приложения "Корпоративный портал".

> [!IMPORTANT]
> [Intune App SDK](../developer/app-sdk-get-started.md) проверяет выборочную очистку каждые 30 минут. Однако изменения существующей политики для пользователей, которые уже выполнили вход, могут не отображаться до 8 часов. Чтобы ускорить этот процесс, попросите пользователей выйти из приложения, а затем снова войти или перезапустить устройства.

Политика защиты приложений Intune поддерживает множественные удостоверения. Intune может применять политики защиты приложений только к рабочей или учебной учетной записи, с которой был выполнен вход в приложение. Однако на каждое устройство поддерживается только одна рабочая или учебная учетная запись.

### <a name="scenario-the-policy-is-applied-but-ios-users-can-still-transfer-work-files-to-unmanaged-apps"></a>Сценарий: политика применяется, но пользователи iOS по-прежнему могут передавать рабочие файлы в неуправляемые приложения
Функция **управления открытием в других приложениях** (![кнопка "Открыть в..."](media/troubleshoot-app-protection/troubleshoot-app-protection.jpg)) для устройств iOS позволяет ограничить передачу файлов между приложениями, которые развернуты через канал MDM. Пользователь может иметь возможность передавать рабочие файлы из управляемых расположений, таких как OneDrive и Exchange, в неуправляемые приложения или расположения в зависимости от конфигурации. Функция **управления открытием в других приложениях** в iOS работает независимо от других методов передачи данных. Поэтому на нее не влияют параметры **Сохранить как** и параметры **копирования и вставки**.

Политики защиты приложений Intune можно использовать вместе с функцией **управления открытием в других приложениях** в iOS, чтобы защитить данные компании указанным ниже образом.

- **Принадлежащие пользователям устройства, которыми не управляет решение MDM**. Вы можете задать параметры политики защиты приложений, выбрав параметр **Разрешить приложению передавать данные другим приложениям: только приложения, управляемые политикой**. Настроенная таким образом функция **Открыть в** в управляемом политикой приложении будет предоставлять возможность выбрать только другие управляемые политикой приложения. Например, если пользователь попытается отправить защищенный файл в виде вложения из OneDrive в собственном почтовом приложении, этот файл будет недоступен для чтения.

- **Устройства под управлением решения MDM**. У устройств, зарегистрированных в Intune или сторонних решениях MDM, обмен данными между приложениями, к которым применяются политики защиты приложений, и другими управляемыми приложениями iOS, развернутыми с помощью MDM, регулируется политиками защиты приложений Intune и функцией **управления открытием в других приложениях** iOS.<br/><br/>
Чтобы связать приложения, развертываемые с помощью решения MDM, с политиками защиты приложений Intune, необходимо настроить параметр UPN пользователя, как описано в разделе [Настройка параметра имени участника-пользователя](../apps/data-transfer-between-apps-manage-ios.md#configure-user-upn-setting-for-microsoft-intune-or-third-party-emm).<br/><br/>Чтобы указать, как данные должны передаваться другим приложениям, включите параметр **Отправка корпоративных данных другим приложениям** и выберите нужный уровень общего доступа.<br/><br/>Чтобы указать, как приложение может получать данные от других приложений, включите параметр **Получать данные из других приложений** и выберите нужный уровень получения данных.

Дополнительные сведения о получении и передаче данных приложения см. в разделе [Параметры перемещения данных](../apps/app-protection-policy-settings-ios.md#data-protection).

Дополнительные сведения см. в разделе [Как управлять передачей данных между приложениями iOS в Microsoft Intune](../apps/data-transfer-between-apps-manage-ios.md).

## <a name="references"></a>Ссылок

Если вы не решили возникшую проблему или вам нужны дополнительные сведения об Intune, опубликуйте вопрос на [форуме Microsoft Intune](https://social.technet.microsoft.com/Forums/en-US/home?category=microsoftintune&filter=alltypes&sort=lastpostdesc). Этот форум посещают многие специалисты службы поддержки, специалисты MVP и участники нашей группы разработчиков. Весьма вероятно, что кто-то предоставит вам необходимую информацию.

Сведения о том, как отправить запрос на поддержку в службу технической поддержки Microsoft Intune, см. в статье [Получение поддержки для Microsoft Intune](../fundamentals/get-support.md).

Дополнительные сведения о политике защиты приложений Intune см. в следующих статьях.

- [Устранение неполадок управления мобильными приложениями](../apps/troubleshoot-mam.md)
- [Часто задаваемые вопросы об управлении мобильными приложениями (MAM) и защите приложений](../apps/mam-faq.md)
- [Совет службы поддержки: устранение неполадок, связанных с политикой защиты приложений Intune, с помощью файлов журналов на локальных устройствах](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Troubleshooting-Intune-app-protection-policy-using/ba-p/330372)

Последние новости, сведения и технические советы можно найти в официальных блогах:

- [Блог службы поддержки Microsoft Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/bg-p/IntuneCustomerSuccess)
- [Блог разработчиков Microsoft Enterprise Mobility and Security](https://cloudblogs.microsoft.com/enterprisemobility)

## <a name="next-steps"></a>Дальнейшие шаги

- Дополнительные сведения об устранении неполадок в службе Intune см. в руководстве по [использованию портала диагностики для оказания помощи пользователям в вашей компании](../fundamentals/help-desk-operators.md). 
- Вы можете узнать об известных проблемах в Microsoft Intune. Дополнительные сведения см. в [блоге Intune об успехах клиентов](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/bg-p/IntuneCustomerSuccess).
- Нужна дополнительная помощь? См. [ Получение поддержки для Microsoft Intune](../fundamentals/get-support.md).