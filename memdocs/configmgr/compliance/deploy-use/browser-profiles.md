---
title: Настройка параметров Microsoft Edge
titleSuffix: Configuration Manager
description: Настройка параметров для веб-браузера Microsoft Edge на клиентских устройствах Windows 10
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.assetid: 76477b4d-df41-4b25-8318-7d18d46ca2c6
ms.openlocfilehash: 91c11e133c74cd3b55db09e8bf80fd6c4df7774d
ms.sourcegitcommit: f94cdca69981627d6a3471b04ac6f0f5ee8f554f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2020
ms.locfileid: "82210100"
---
# <a name="configure-microsoft-edge-settings-in-configuration-manager"></a>Настройка параметров Microsoft Edge в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

<!-- 1357310 -->
Начиная с версии 1802 пользователи, которые используют веб-браузер [Microsoft Edge](https://technet.microsoft.com/microsoft-edge/bb265256) на клиентских устройствах Windows 10, могут создавать политику параметров соответствия Configuration Manager, чтобы настроить несколько параметров Microsoft Edge. 

Эта политика применяется только к клиентам с ОС Windows 10 версии 1703 или более поздней. <!--511552-->


## <a name="policy-settings"></a>Параметры политики
В настоящее время эта политика включает следующие параметры:
- **Set Microsoft Edge browser as default**. (Установить браузер Microsoft Edge по умолчанию). Настраивает параметр приложения по умолчанию Windows 10 для веб-браузера как Microsoft Edge
- **Включить раскрывающийся список в адресной строке**. Требуется Windows 10, версия 1703 или более поздняя. Дополнительные сведения см. в разделе [Browser/AllowAddressBarDropdown](/windows/client-management/mdm/policy-csp-browser#browser-allowaddressbardropdown).
- **Включить синхронизацию избранного между браузерами Майкрософт**. Требуется Windows 10, версия 1703 или более поздняя. Дополнительные сведения см. в разделе [Browser/SyncFavoritesBetweenIEAndMicrosoftEdge](/windows/client-management/mdm/policy-csp-browser#browser-syncfavoritesbetweenieandmicrosoftedge).
- **Разрешить очистку данных браузера при выходе**. Требуется Windows 10, версия 1703 или более поздняя. Дополнительные сведения см. в разделе [Browser/ClearBrowsingDataOnExit](/windows/client-management/mdm/policy-csp-browser#browser-clearbrowsingdataonexit).
- **Разрешить не отслеживать заголовки**. Дополнительные сведения см. в разделе [Политика браузера AllowDoNotTrack](/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack).
- **Разрешить автозаполнение**. Дополнительные сведения см. в разделе [Политика браузера AllowAutofill](/windows/client-management/mdm/policy-csp-browser#browser-allowautofill).
- **Разрешить файлы cookie**. Дополнительные сведения см. в разделе [Политика браузера AllowCookies](/windows/client-management/mdm/policy-csp-browser#browser-allowcookies).
- **Разрешить блокирование всплывающих окон**. Дополнительные сведения см. в разделе [Политика браузера AllowPopups](/windows/client-management/mdm/policy-csp-browser#browser-allowpopups).
- **Разрешить варианты поиска в адресной строке**. Дополнительные сведения см. в разделе [Политика браузера AllowSearchSuggestionsinAddressBar](/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar).
- **Разрешить отправку трафика интрасети в Internet Explorer**. Дополнительные сведения см. в разделе [Политика браузера SendIntranetTraffictoInternetExplorer](/windows/client-management/mdm/policy-csp-browser#browser-sendintranettraffictointernetexplorer).
- **Разрешить диспетчер паролей**. Дополнительные сведения см. в разделе [Политика браузера AllowPasswordManager](/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager).
- **Разрешить средства для разработчиков**. Дополнительные сведения см. в разделе [Политика браузера AllowDeveloperTools](/windows/client-management/mdm/policy-csp-browser#browser-allowdevelopertools).
- **Разрешить расширения**. Дополнительные сведения см. в разделе [Политика браузера AllowExtensions](/windows/client-management/mdm/policy-csp-browser#browser-allowextensions).


### <a name="configure-windows-defender-smartscreen-settings-for-microsoft-edge"></a>Настройка параметров SmartScreen Защитника Windows для Microsoft Edge
<!--1353701-->
Начиная с версии 1806, эта политика добавляет три параметра для [SmartScreen Защитника Windows](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-smartscreen/microsoft-defender-smartscreen-overview). На странице **Параметры SmartScreen** политики теперь имеются указанные ниже дополнительные параметры.

- **Разрешить SmartScreen**. Указывает, разрешено ли использовать функцию SmartScreen Защитника Windows. Дополнительные сведения см. в описании [политики браузера AllowSmartScreen](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen).
- **Пользователи могут переопределять запрос SmartScreen для сайтов**. Указывает, могут ли пользователи переопределить предупреждения фильтра SmartScreen Защитника Windows о потенциально вредоносных веб-сайтах. Дополнительные сведения см. в описании [политики браузера PreventSmartScreenPromptOverride](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride).
- **Пользователи могут переопределять запрос SmartScreen для файлов**. Указывает, могут ли пользователи переопределить предупреждения фильтра SmartScreen Защитника Windows о скачивании непроверенных файлов. Дополнительные сведения см. в описании [политики браузера PreventSmartScreenPromptOverrideForFiles](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles).



## <a name="create-the-microsoft-edge-browser-profile"></a>Создание профиля браузера Microsoft Edge

1. В консоли Configuration Manager перейдите в рабочую область **Активы и соответствие**. Разверните **Параметры соответствия** и выберите узел **Профили браузера Microsoft Edge**. На ленте выберите **Создать профиль браузера Microsoft Edge**.
2. Укажите **имя** политики, при необходимости введите **описание**, а затем щелкните **Далее**.
3. На странице **Общие параметры** измените значение на **Настроено** для параметров, которые необходимо включить в политику, а затем нажмите кнопку **Далее**. Чтобы продолжить, выберите параметр **Set Microsoft Edge Browser as default** (Задать браузер Microsoft Edge в качестве браузера по умолчанию).
4. В версии 1806 и более поздних версиях настройте параметры на странице **Параметры SmartScreen**, а затем нажмите кнопку **Далее**. 
5. На странице **Поддерживаемые платформы** выберите версии и архитектуры операционной системы, к которым применяется политика, а затем нажмите кнопку **Далее**. 
6. Завершите работу мастера.



## <a name="deploy-the-policy"></a>Развертывание политики

1. Выберите политику и щелкните вариант ленты **Развернуть**.
2. Щелкните **Обзор**, чтобы выбрать коллекцию, в которую требуется развернуть политику. 
3. При необходимости выберите дополнительные параметры.  
     a. Создайте предупреждения, если политика не соответствует требованиям.  
     b. Задайте расписание, по которому клиент будет оценивать соответствие устройства политике. 
4. Щелкните **ОК**, чтобы создать развертывание.



## <a name="next-steps"></a>Дальнейшие шаги

Как и все политики параметров соответствия клиент устраняет ошибки параметров по указанному расписанию. [Отслеживайте и сообщайте о соответствии устройства](monitor-compliance-settings.md) в консоли Configuration Manager.
