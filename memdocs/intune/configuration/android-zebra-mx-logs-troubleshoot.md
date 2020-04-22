---
title: Использование журналов StageNow на устройствах Android Zebra в Microsoft Intune в Azure | Документация Майкрософт
description: См. раздел со сведениями о распространенных проблемах и способах их устранения при использовании StageNow на устройствах Android с Microsoft Intune. Также узнайте, как получить журналы, и ознакомьтесь с примерами того, как считать сведения об успешном выполнении или ошибках из журнала.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/26/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: ''
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 607e2303cbec9ec7fc069db602d51684b71e6575
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "80083848"
---
# <a name="troubleshoot-and-see-potential-issues-on-android-zebra-devices-in-microsoft-intune"></a>Устранение неполадок и просмотр потенциальных проблем на устройствах Android Zebra в Microsoft Intune



В Microsoft Intune можно использовать [Zebra Mobility Extensions (MX) для управления устройствами Android Zebra](android-zebra-mx-overview.md). При использовании устройств Zebra необходимо создать профили в StageNow для управления параметрами и их отправки в Intune. Intune использует приложение StageNow для применения параметров на устройствах. Приложение StageNow также создает подробный файл журнала на устройстве, который используется для устранения неполадок.

Данная функция применяется к:

- Android

Например, вы создаете профиль в StageNow для настройки устройства. При создании профиля StageNow на последнем шаге создается файл для проверки профиля. Затем этот файл используется приложением StageNow на устройстве.

В другом примере вы создаете профиль в StageNow для его проверки. В Intune вы добавляете профиль StageNow, а затем назначаете его устройствам Zebra. При проверке состояния назначенного профиля в профиле отображается высокоуровневый статус.

В обоих случаях можно получить дополнительные сведения из файла журнала StageNow, который сохраняется на устройстве каждый раз при применении профиля StageNow.

Некоторые проблемы не связаны с содержимым профиля StageNow и не отражаются в журналах.

В этой статье показано, как прочитать журналы StageNow, а также перечислены другие потенциальные проблемы с устройствами Zebra, которые могут не отражаться в журналах.

Дополнительные сведения об этой функции см. в разделе [Использование устройств Zebra с Zebra Mobility Extensions и управление ими](android-zebra-mx-overview.md).

## <a name="get-the-logs"></a>Получение журналов

### <a name="use-the-stagenow-app-on-the-device"></a>Использование приложения StageNow на устройстве
При тестировании профиля непосредственно с помощью StageNow на компьютере вместо того, чтобы использовать [Intune для развертывания профиля](android-zebra-mx-overview.md#step-4-create-a-device-management-profile-in-stagenow), приложение StageNow на устройстве сохраняет журналы из теста. Чтобы получить файл журнала, используйте параметр **Еще (...)** в приложении StageNow на устройстве.

### <a name="get-logs-using-android-debug-bridge"></a>Получение журналов с помощью Android Debug Bridge
Чтобы получить журналы после развертывания профиля с помощью Intune, подключите устройство к компьютеру с [Android Debug Bridge (ADB)](https://developer.android.com/studio/command-line/adb) (откроется веб-сайт Android).

На устройстве журналы хранятся в папке `/sdcard/Android/data/com.microsoft.windowsintune.companyportal/files`

### <a name="get-logs-from-email"></a>Получение журналов по электронной почте
Чтобы получить журналы после развертывания профиля с помощью Intune, конечные пользователи могут отправить журналы по электронной почте с помощью почтового приложения на устройстве. На устройстве Zebra откройте приложение корпоративного портала и [отправьте журналы](https://docs.microsoft.com/mem/intune/user-help/send-logs-to-your-it-admin-by-email-android). При использовании функции отправки журналов также создается идентификатор инцидента PowerLift, на который можно сослаться при обращении в службу поддержки Майкрософт.

## <a name="read-the-logs"></a>Чтение журналов

При просмотре журналов возникает ошибка при появлении тега `<characteristic-error>`. Сведения об ошибке записываются в тег `<parm-error>` > свойство `desc`.

## <a name="error-types"></a>Типы ошибок

Устройства Zebra включают различные уровни отчетов об ошибках:

- На устройстве не поддерживается CSP. Например, устройство не является мобильным и не имеет диспетчера сотовой сети.
- Несоответствие версии MX или OSX. Каждый CSP имеет версию. Полную таблицу поддержки см. в [документации по Zebra](http://techdocs.zebra.com/mx/) (на веб-сайте Zebra).
- Устройство сообщает о возникновении другой проблемы или ошибки.

## <a name="examples"></a>Примеры

Например, у вас есть следующий входной профиль:

```xml
<wap-provisioningdoc>
    <characteristic type="Clock">
        <parm name="AutoTime" value="false"/>
        <parm name="TimeZone" value="GMT-5"/>
        <parm name="Date" value="2014-12-03"/>
        <parm name="Time" value="11:11:11"/>
    </characteristic>
</wap-provisioningdoc>
```

В журнале XML-код идентичен входным данным. Эти выходные данные указывают на то, что профиль успешно применен к устройству без ошибок:

```xml
<wap-provisioningdoc>
    <characteristic type="Clock" version="6.0">
        <parm name="AutoTime" value="false"/>
        <parm name="TimeZone" value="GMT-5"/>
        <parm name="Date" value="2014-12-03"/>
        <parm name="Time" value="11:11:11"/>
    </characteristic>
</wap-provisioningdoc>
```

В другом примере имеются следующие входные данные:

```xml
<wap-provisioningdoc>
    <characteristic type="XmlMgr" version="4.2" >
        <parm name="ProcessingMode" value="1"/>
    </characteristic>
    <characteristic type="AppMgr" version="4.2" >
        <parm name="Action" value="Install"/>
        <parm name="APK" value="/sdcard/test.apk"/>
    </characteristic>
</wap-provisioningdoc>
```

В журнале отображается ошибка, так как она содержит тег `<characteristic-error>`. В этом сценарии профиль попытался установить пакет Android (APK), который не существует по указанному пути:

```xml
<wap-provisioningdoc>
    <characteristic type="XmlMgr" version="4.2">
        <parm name="ProcessingMode" value="1"/>
    </characteristic>
    <characteristic-error type="AppMgr" version="5.1" desc="missing">
        <parm-error name="Action" value="Install" desc="apk doesnot exist in the path"/>
        <parm name="APK" value="/sdcard/test.apk"/>
    </characteristic-error>
</wap-provisioningdoc>
```

## <a name="other-potential-issues-with-zebra-devices"></a>Другие потенциальные проблемы с устройствами Zebra

В этом разделе перечислены другие возможные проблемы, с которыми можно столкнуться при использовании устройств Zebra с администратором устройств. Эти проблемы не отображаются в журналах StageNow.

### <a name="android-system-webview-is-out-of-date"></a>Android System WebView устарела

При входе со старых устройств с помощью приложения корпоративного портала для пользователей может отображаться сообщение о том, что компонент System WebView устарел и нуждается в обновлении. Если на устройстве установлен Google Play, подключите его к Интернету и проверьте наличие обновлений. Если на устройстве не установлен Google Play, получите обновленную версию компонента и примените ее к устройствам. Или обновите ОС устройства до актуальной версией, выпущенной Zebra.

### <a name="management-actions-take-a-long-time"></a>Действия по управлению занимают много времени

Если службы Google Play недоступны, выполнение некоторых задач занимает до 8 часов. Статья [Ограничения приложения корпоративного портала Intune для Android](https://support.microsoft.com/help/3211588/limitations-of-intune-company-portal-app-for-android-in-china) (переход на другой веб-сайт Майкрософт) может оказаться полезным ресурсом при поиске соответствующей информации.

### <a name="device-spoofing-suspected-shows-in-intune"></a>В Intune отображается сообщение о подозрении на спуфинг устройства

Эта ошибка означает, что Intune подозревает, что устройство, которое не является устройством Android Zebra, сообщает о своей модели и изготовителе как об устройстве Zebra.

### <a name="company-portal-app-is-older-than-minimum-required-version"></a>Приложение корпоративного портала старше минимальной требуемой версии

Intune может обновить минимальную требуемую версию приложения корпоративного портала. Если на устройстве не установлен Google Play, приложение корпоративного портала не обновляется автоматически. Если минимальная требуемая версия новее установленной версии, приложение корпоративного портала перестает работать. Обновите приложение корпоративного портала до актуальной версии, используя [передачу данных корпоративного портала на устройства Zebra](android-zebra-mx-overview.md#sideload-the-company-portal-app).

## <a name="next-steps"></a>Дальнейшие действия

[Доски обсуждений Zebra](https://developer.zebra.com/community/home/discussions) (на веб-сайте Zebra)

[Использование устройств Zebra с Zebra Mobility Extensions и управление ими в Intune](android-zebra-mx-overview.md)
