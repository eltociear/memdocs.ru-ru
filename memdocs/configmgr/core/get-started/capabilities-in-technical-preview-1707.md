---
title: Техническая версия 1707
titleSuffix: Configuration Manager
description: Сведения о функциях, доступных в Technical Preview для Configuration Manager, версия 1707.
ms.date: 08/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: cb405ba0-8792-4ab7-988b-2f835f3a9550
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 4ddae3e4c4cf31cb05376bfa437d722f16652fad
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705142"
---
# <a name="capabilities-in-technical-preview-1707-for-configuration-manager"></a>Возможности в Technical Preview 1707 для Configuration Manager

*Область применения: Configuration Manager (ветвь Technical Preview)*

В этой статье содержатся сведения о функциях, доступных в версии 1707 Technical Preview для Configuration Manager. Этот выпуск можно установить для обновления и добавления новых возможностей в ознакомительную техническую версию сайта Configuration Manager. Перед установкой этой версии прочтите статью [Technical Preview для Configuration Manager](../../core/get-started/technical-preview.md). В ней приведены общие требования и ограничения на использование ознакомительной технической версии, а также сведения о том, как выполнять обновления и оставлять отзывы о функциях этого выпуска.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->

**Известные проблемы в этой версии Technical Preview:**
- **Если сервер сайта находится в пассивном режиме, происходит сбой обновления до предварительной версии 1707**. Если вы запустили предварительную версию 1706 и [сервер первичного сайта находится в пассивном режиме](capabilities-in-technical-preview-1706.md#site-server-role-high-availability), удалите сервер сайта в пассивном режиме, чтобы обновить сайт предварительной версии до версии 1707. Вы можете повторно установить сервер сайта в пассивном режиме, после того как на сайте заработает версия 1707.

  Удаление сервера сайта в пассивном режиме
  1. Откройте консоль и выберите **Администрирование** > **Обзор** > **Конфигурация сайта** > **Серверы и роли системы сайта**. Затем выберите сервер сайта в пассивном режиме.
  2. На панели **Системные роли сайта** щелкните правой кнопкой мыши роль **Сервер сайта** и нажмите кнопку **Удалить роль**.
  3. Щелкните правой кнопкой мыши сервер сайта в пассивном режиме, а затем выберите **Удалить**.
  4. Удалив сервер сайта на активном сервере первичного сайта, перезапустите службу **CONFIGURATION_MANAGER_UPDATE**.



**Ниже перечислены новые возможности, доступные в этой версии.**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="client-peer-cache-support-for-express-installation-files-for-windows-10-and-office-365"></a>Одноранговый кэш клиента поддерживает файлы экспресс-установки для Windows 10 и Office 365
<!-- 1352486 -->
Начиная с этого выпуска, одноранговый кэш поддерживает использование файлов экспресс-установки содержимого для Windows 10 и файлов обновления для Office 365. Дополнительные настройки не требуются.

## <a name="surface-device-dashboard"></a>Панель мониторинга устройств Surface
<!--1355788-->
Эта панель мониторинга позволяет получать сведения об устройствах Surface в вашем окружении. Перейдите в консоли к пункту **Мониторинг** > **Устройства Surface**. Вы можете просмотреть следующее:
- процент устройств Surface;
- процент моделей Surface;
- пять самых часто встречающихся версий операционных систем.

Щелкните раздел диаграммы **Модели Surface**, чтобы получить полный список устройств.  

## <a name="configure-and-deploy-windows-defender-application-guard-policies"></a>Настройка и развертывание политик Application Guard в Защитнике Windows
<!-- 1351960 -->

[Application Guard в Защитнике Windows](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97) — это новая функция Windows, которая помогает защитить пользователей, открывая ненадежные веб-узлы в безопасном изолированном контейнере, который никак не взаимодействует с другими частями операционной системы. В этом выпуске Technical Preview мы добавили возможность настроить эту функцию с помощью параметров соответствия Configuration Manager. Вы можете настроить их и развернуть в коллекции. Эта функция будет выпущена в предварительной версии для 64-разрядной версии Windows 10 Fall Creator (кодовое имя RS3). Чтобы проверить ее в работе, необходимо использовать предварительную версию этого обновления.

### <a name="before-you-start"></a>Перед началом работы

Чтобы создавать и развертывать политики Application Guard в Защитнике Windows, для соответствующих устройств Windows 10 должны быть настроены политики сетевой изоляции. Дополнительные сведения см. в [этой записи блога](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97). Эта возможность поддерживается только в текущих сборках Windows 10 Insider. Чтобы проверить ее работу, на клиентах должна быть запущена последняя сборка Windows 10 Insider.

### <a name="try-it-out"></a>Попробуйте!

#### <a name="to-create-a-policy-and-to-browse-the-available-settings"></a>Чтобы создать политику и просмотреть доступные параметры, сделайте следующее.

1. В консоли Configuration Manager щелкните элемент **Активы и соответствие**.
2. В рабочей области **Активы и соответствие** выберите пункты **Обзор** > **Endpoint Protection** > **Application Guard в Защитнике Windows**.
3. На вкладке **Главная** в группе **Создать** щелкните **Создать политику Application Guard в Защитнике Windows**.
4. Вы можете просмотреть и настроить доступные параметры, а также испытать функцию в работе, используя запись блога в качестве инструкции.
5. В этом выпуске мы добавили в мастер новую страницу **Определение сети**. На этой странице нужно указать удостоверение организации и задать границу корпоративной сети.<br>Компьютеры с ОС Windows 10 хранят только один список сетевой изоляции в клиенте. В этом выпуске вы можете создать два разных типа списков сетевой изоляции (один — из Windows Information Protection, а другой — из Application Guard в Защитнике Windows) и развернуть их в клиенте. При развертывании обеих политик эти списки сетевой изоляции должны совпадать. Если вы развернете несовпадающие списки на одном клиенте, произойдет сбой развертывания.
Дополнительные сведения о том, как указать определения сети, см. в [документации по Windows Information Protection](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/create-wip-policy-using-configmgr).

6. Когда вы закончите настройку, завершите работу мастера и разверните политику на одном или нескольких устройствах Windows 10.

### <a name="further-reading"></a>Дополнительные сведения
Дополнительные сведения об Application Guard в Защитника Windows см. в [этой записи блога](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97). Кроме того, в [этой записи блога](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903) см. дополнительные сведения об изолированном режиме Application Guard в Защитнике Windows.

## <a name="add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager"></a>Добавление параметров при развертывании сценариев PowerShell из Configuration Manager

<!-- 1236459 --->

В последней версии Technical Preview появилась новая возможность [создавать и запускать сценарии PowerShell из консоли Configuration Manager](capabilities-in-technical-preview-1706.md#create-and-run-powershell-scripts-from-the-configuration-manager-console).
В этой версии Technical Preview эта возможность была усовершенствована. Configuration Manager теперь считывает сценарий PowerShell и отображает доступные параметры в мастере создания сценариев. Вы можете указать в мастере значение параметра, которое будет использоваться при запуске сценария. Вы также можете оставить параметр пустым. В этом случае значение параметра потребуется указать в момент запуска сценария.
В этой версии Technical Preview необходимо указать все параметры, необходимые для сценария. В следующем выпуске настройка параметров сценария будет необязательной.

### <a name="try-it-out"></a>Попробуйте!

1. Выполните следующие указания, чтобы научиться [создавать и запускать сценарии PowerShell из консоли Configuration Manager](capabilities-in-technical-preview-1706.md#create-and-run-powershell-scripts-from-the-configuration-manager-console).
2. На новой странице **Параметры сценариев** **мастера создания сценариев** выберите параметр и щелкните **Изменить**.
3. Укажите значение для выбранного параметра и нажмите кнопку **ОК**.
4. Завершите работу мастера.

При запуске сценарий будет использовать настроенные вами значения параметров.
