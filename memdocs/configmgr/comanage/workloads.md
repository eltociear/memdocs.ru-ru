---
title: Рабочие нагрузки совместного управления
titleSuffix: Configuration Manager
description: Сведения о рабочих нагрузках, которые можно переключить из Configuration Manager в Microsoft Intune.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 04/15/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.assetid: 4c90befe-9c4e-4c27-a947-625887e15052
ms.openlocfilehash: 8c91ba1c2b4b5ef7072c030eddd9b97dd69933e5
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075716"
---
# <a name="co-management-workloads"></a>Рабочие нагрузки совместного управления

Вам не придется переключать рабочие нагрузки, или вы можете настроить их по отдельности, когда будете готовы. Configuration Manager будет и далее управлять всеми остальными рабочими нагрузками, в том числе всеми не переключенными на Intune рабочими нагрузками и всеми функциями Configuration Manager, для которых не поддерживается совместное управление.

Если вы переключите рабочую нагрузку в Intune, но позднее измените свое решение, вы можете снова переключиться на Configuration Manager.

Совместное управление поддерживает следующие рабочие нагрузки:

- [Политики соответствия требованиям](#compliance-policies)  

- [Политики Центра обновления Windows](#windows-update-policies)  

- [Политики доступа к ресурсам](#resource-access-policies)  

- [Endpoint Protection](#endpoint-protection)  

- [Конфигурация устройств](#device-configuration)  

- [Приложения Office "нажми и работай"](#office-click-to-run-apps)  

- [Клиентские приложения](#client-apps)  

## <a name="compliance-policies"></a>Политики соответствия требованиям

Политики соответствия требованиям определяют правила и параметры, которым должно соответствовать устройство, чтобы политики условного доступа расценивали его как совместимое. Политики соответствия также можно использовать для отслеживания и устранения проблем совместимости у устройств, независимо от условного доступа. Начиная с Configuration Manager версии 1910 вы можете добавлять оценку настраиваемых конфигурационных баз в качестве правила оценки политики соответствия. Дополнительные сведения см. в статье [Включение настраиваемых конфигурационных баз в оценку политики соответствия](../compliance/deploy-use/create-configuration-baselines.md#bkmk_CAbaselines).

Дополнительные сведения об этой функции Intune см. в статье [Начало работы с политиками соответствия устройств в Intune](https://docs.microsoft.com/intune/device-compliance-get-started).  

## <a name="windows-update-policies"></a>Политики Центра обновления Windows

Политики Цента обновления Windows для бизнеса позволяют настраивать политики отсрочки обновлений компонентов Windows 10 или исправлений для устройств Windows 10, управляемых непосредственно с помощью Центра обновления Windows для бизнеса.

Дополнительные сведения об этой функции Intune см. в статье [Управление обновлениями программного обеспечения в Intune](https://docs.microsoft.com/intune/windows-update-for-business-configure).  

## <a name="resource-access-policies"></a>Политики доступа к ресурсам

Политики доступа к ресурсам настраивают параметры VPN, Wi-Fi, электронной почты и сертификатов на устройствах.

Дополнительные сведения об этой функции Intune см. в статье [Применение параметров функций на устройствах с помощью профилей устройств в Microsoft Intune](https://docs.microsoft.com/intune/device-profiles).

> [!Note]  
> Рабочая нагрузка доступа к ресурсам также включена в конфигурацию устройства. Intune управляет этими политиками, когда вы переключаете рабочую нагрузку [конфигурации устройства](#device-configuration).

## <a name="endpoint-protection"></a>Endpoint Protection

<!--1357365-->

Рабочая нагрузка Endpoint Protection включает в себя пакет Защитника Windows с набором функций защиты от вредоносных программ.

- Антивирусная программа "Защитник Windows"
- Служба защиты приложений Защитника Windows  
- Брандмауэр Защитника Windows  
- SmartScreen Защитника Windows  
- Шифрование Windows
- Exploit Guard в Защитнике Windows  
- Управление приложениями в Защитнике Windows  
- Центр безопасности Защитника Windows  
- Advanced Threat Protection в Защитнике Windows (сейчас называется Advanced Threat Protection в Microsoft Defender)
- Windows Information Protection  

Дополнительные сведения об этой функции Intune см. в статье [Параметры Windows 10 (и более поздних версий) для защиты устройств с помощью Intune](https://docs.microsoft.com/intune/endpoint-protection-windows-10).

> [!Note]  
> При переключении этой рабочей нагрузки политики Configuration Manager используются на устройстве, пока не будут заменены политиками Intune. Такое поведение гарантирует, что политики будут использоваться на устройстве во время перехода.
>
> Рабочая нагрузка Endpoint Protection также включена в конфигурацию устройства. Это же поведение политики применяется, когда вы переключаете рабочую нагрузку [конфигурации устройства](#device-configuration).<!-- SCCMDocs.nl-nl issue #4 -->
>
> На параметры антивирусной программы в Microsoft Defender, которые относятся к типу профиля ограничений устройства для конфигурации устройств Intune, ползунок Endpoint Protection не действует. Чтобы управлять параметрами антивирусной программы в Microsoft Defender для совместно управляемых устройств с включенным ползунком Endpoint Protection, воспользуйтесь новыми политиками антивирусной защиты в **центре администрирования Microsoft Endpoint Manager** > **Безопасность конечной точки** > **Антивирус**. Эта политика нового типа содержит новые и улучшенные параметры, а также поддерживает все параметры, доступные в профиле ограничений устройства. <!--6609171-->
>
> Функция шифрования Windows включает в себя управление BitLocker. Дополнительные сведения о работе этой функции с совместным управлением см. в статье [Развертывание управления BitLocker](../protect/deploy-use/bitlocker/deploy-management-agent.md#co-management-and-intune).<!-- SCCMDocs#2321 -->

## <a name="device-configuration"></a>Конфигурация устройства

<!--1357903-->

Рабочая нагрузка конфигурации устройств включает параметры для управления устройствами в организации. Переключение этой рабочей нагрузки приводит к переносу рабочих нагрузок **Доступ к ресурсам** и **Endpoint Protection**.

Вы по-прежнему сможете развертывать из Configuration Manager параметры в совместно управляемые устройства, даже если Intune является центром конфигурации устройств. Такое исключение допускается для настройки параметров, которые нужны для вашей организации, но пока не доступны в Intune. Укажите это исключение в [конфигурационной базе Configuration Manager](../compliance/deploy-use/create-configuration-baselines.md). Включите параметр **Всегда применять эти базовые показатели даже для совместно управляемых клиентов** при создании базовой конфигурации. Вы сможете позднее изменить этот параметр на вкладке **Общие**, где собраны свойства существующей базовой конфигурации.  

Дополнительные сведения об этой функции Intune см. в статье [Создайте профиль устройства в Microsoft Intune](https://docs.microsoft.com/intune/device-profile-create).  

## <a name="office-click-to-run-apps"></a>Приложения Office "нажми и работай"

<!--1357841-->

Эта рабочая нагрузка управляет приложениями Office 365 на совместно управляемых устройствах.

- После перемещения рабочей нагрузки приложение отображается в **Корпоративном портале** на устройстве.  

- Отображение обновлений Office на клиенте может занять около 24 часов, если устройства не были перезапущены.  

- Имеется новое глобальное условие — **Приложения Office 365 управляются службой Intune на устройстве**. Оно добавляется по умолчанию в качестве требования к новым приложениям Office 365. При переносе этой рабочей нагрузки совместно управляемые клиенты не отвечают требованию приложения. Затем они не устанавливают приложение Office 365, развертываемое через Configuration Manager.  

Дополнительные сведения об этой функции Intune см. в статье [Назначение приложений Office 365 устройствам на базе Windows 10 с помощью Microsoft Intune](https://docs.microsoft.com/intune/apps-add-office365).

## <a name="client-apps"></a>Клиентские приложения

<!--1357892-->

Вы можете использовать Intune для управления клиентскими приложениями и сценариями PowerShell на совместно управляемых устройствах Windows 10. После переноса рабочей нагрузки все доступные приложения, развернутые через Intune, становятся доступными на корпоративном портале. Приложения, которые вы развертывали через Configuration Manager, доступны в Центре программного обеспечения.

Дополнительные сведения об этой функции Intune см. в статье [Что такое управление приложениями с помощью Microsoft Intune](https://docs.microsoft.com/intune/app-management).

> [!Tip]  
> Эта функция появилась в версии 1806 [на стадии предварительного выпуска](../core/servers/manage/pre-release-features.md). Начиная с версии 2002, эта функция больше не считается функцией предварительной версии.  
>
> Эта функция может отображаться в списке функций как **Мобильные приложения для совместно управляемых устройств**.<!-- 5849669 -->

Начиная с версии 1910 при включении подключенного кэша Майкрософт в точках распространения Configuration Manager они могут обслуживать приложения Microsoft Intune Win32 для совместно управляемых клиентов. Дополнительные сведения см. в разделе [Подключенный кэш Майкрософт в Configuration Manager](../core/plan-design/hierarchy/microsoft-connected-cache.md#bkmk_intune).

## <a name="diagram-for-app-workloads"></a>Схема рабочих нагрузок приложений

![Схема рабочих нагрузок приложений для совместного управления](media/co-management-apps.svg)

[Просмотреть схему в полном размере](media/co-management-apps.svg)

## <a name="known-issues"></a>Известные проблемы

Когда рабочая нагрузка Endpoint Protection переносится в Intune, клиент может по-прежнему учитывать политики, заданные в Configuration Manager и Microsoft Defender. <!--5024559-->

Чтобы решить эту проблему, примените файл CleanUpPolicy.xml с помощью программы ConfigSecurityPolicy.exe после получения политик Intune клиентом, выполнив указанные ниже действия.

1. Скопируйте и сохраните приведенный ниже текст как `CleanUpPolicy.xml`.

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <SecurityPolicy xmlns="http://forefront.microsoft.com/FEP/2010/01/PolicyData" Name="FEP clean-up policy"><PolicySection Name="FEP.AmPolicy"><LocalGroupPolicySettings><IgnoreKey Name="SOFTWARE\Policies\Microsoft\Microsoft Antimalware"/><IgnoreKey Name="SOFTWARE\Policies\Microsoft\Windows Defender"/></LocalGroupPolicySettings></PolicySection></SecurityPolicy>
   ```
1. Откройте командную строку с повышенными привилегиями и запустите программу `ConfigSecurityPolicy.exe`. Обычно этот исполняемый файл находится в одном из следующих каталогов:
   - C:\Program Files\Windows Defender
   - C:\Program Files\Microsoft Security Client
1. В командной строке передайте XML-файл для очистки политики. Например, `ConfigSecurityPolicy.exe C:\temp\CleanUpPolicy.xml`.  

## <a name="next-steps"></a>Дальнейшие шаги

[How to switch Configuration Manager workloads to Intune](how-to-switch-workloads.md) (Переключение рабочих нагрузок Configuration Manager в Intune)  
