---
title: Настройка центра поддержки
titleSuffix: Configuration Manager
description: Настройка файла конфигурации центра поддержки.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a6f7f6b7-9ef3-4ffa-a3cf-d877ac55983b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1436f40dc989202725d7b83d551d318b970f9b5d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707442"
---
# <a name="customize-support-center"></a>Настройка центра поддержки

*Область применения: Configuration Manager (Current Branch)*

Средство [Центр поддержки](support-center.md) включает файл конфигурации, который можно настраивать. По умолчанию при установке центра поддержки этот файл расположен по следующему пути: `C:\Program Files (x86)\Configuration Manager Support Center\ConfigMgrSupportCenter.exe.config`. Файл конфигурации изменяет поведение программы:

- [Настройка сбора данных](#bkmk_datacoll). Вы можете изменять наборы разделов реестра и пространств имен WMI, доступных для включения во время сбора данных.  

- [Настройка групп журналов](#bkmk_loggroups). Вы можете определять новые группы файлов журналов с помощью регулярных выражений. Также можно добавить другие файлы журналов в группы журналов.  

- [Сбор дополнительных файлов журналов с использованием подстановочных знаков](#bkmk_wildcards). Вы можете использовать поиск с подстановочными знаками для сбора дополнительных файлов журналов.  

Для внесения этих изменений вам потребуются права администратора на клиентском компьютере, где установлен центр поддержки. Эти настройки производятся в текстовом редакторе или редакторе XML, таком как Блокнот или Visual Studio.

> [!Important]  
> Файл конфигурации центра поддержки — это файл формата XML. Он очень важен для работы центра поддержки. Рекомендуется изменять этот файл только пользователям, знакомым с XML и регулярными выражениями.  

Перед настройкой файла конфигурации центра поддержки сохраните резервную копию исходного файла. Это позволит восстановить исходную функциональность центра поддержки, если вы сделаете ошибки при редактировании этого файла. Если не создавать резервную копию, а центр поддержки начнет работать правильно, после внесения изменений в файле конфигурации следует повторно установить центр поддержки. Также можно скопировать файл конфигурации из другой установки центра поддержки.



## <a name="customize-data-collection"></a><a name="bkmk_datacoll"></a> Настройка сбора данных

Для настройки сбора данных на клиенте можно изменять файл конфигурации центра поддержки с помощью XML-элементов, содержащихся в элементе `<dataCollectorSettings>`.


### <a name="wmi-data-collection"></a>Сбор данных WMI

Элемент `<CcmWmiDataCollector>` содержит элемент `<collectionScopes>`. Этот элемент используется для изменения пространств имен WMI, из которых центр поддержки собирает данные. Он также включает элемент `<ignoreScopes>`. Он позволяет вам отфильтровывать коллекцию данных из частей пространств имен, заданных в элементе `<collectionScopes>`.  
    
#### <a name="example"></a>Пример
Файл конфигурации по умолчанию собирает данные из пространства имен `root\ccm`. Он включает этот путь в элемент `<add/>` в `<collectionScopes>`. 

Он также игнорирует все данные в путях `\cimodels`, `\invagt`,  `\events` и `\policy` для этого пространства имен. Он включает эти пути в элементы `<add/>` внутри `<ignoreScopes>`.

```XML
<CcmWmiDataCollector>
  <collectionScopes>
    <!-- Collect these namespaces (ignoring the sub-scopes in the ignoreScopes block) -->
    <add key="root\ccm"/>
    <add key="root\cimv2\sms"/>
  </collectionScopes>
  <ignoreScopes>
    <!-- Collecting these namespaces is known to be problematic/unnecessary -->
    <add key="root\ccm\cimodels"/>
    <add key="root\ccm\invagt"/>
    <add key="root\ccm\events"/>
    <!-- Do not collect policy, there's already a separate policy collector.-->
    <add key="root\ccm\policy"/>
  </ignoreScopes>
</CcmWmiDataCollector>
```


### <a name="registry-data-collection"></a>Сбор данных реестра

Элемент `<RegistryDataCollector>` содержит элемент `<registryKeys>`. Используйте этот элемент для изменения разделов и подразделов реестра, которые центр поддержки собирает в пути `HKEY_LOCAL_MACHINE`. Центр поддержки не поддерживает сбор данных реестра из других корневых путей реестра.

#### <a name="example"></a>Пример
Для сбора разделов реестра для классической программы, установленной на устройстве, добавьте следующий элемент `<add/>` в элемент `<registryKeys>`: `<add key="software\\microsoft\\windows\\currentversion\\uninstall"/>`

```XML
<RegistryDataCollector>
  <registryKeys>
    <!-- Registry keys (and all subkeys) to collect -->
    <add key="software\\microsoft\\ccm"/>
    <add key="software\\microsoft\\sms"/>
    <add key="software\\microsoft\\ccmsetup"/>
    <add key="software\\microsoft\\windows\\currentversion\\uninstall"/>
  </registryKeys>
</RegistryDataCollector>
```



## <a name="customize-log-file-groups"></a><a name="bkmk_loggroups"></a> Настройка групп файлов журналов

Для настройки того, какие файлы журналов центр поддержки собирает и как он представляет их в списке **Группы журналов**, используйте элементы в элементе `<logGroups>`. Когда вы запускаете центр поддержки, он проверяет этот раздел файла конфигурации. Затем он создает группу для списка **Группы журналов** для каждого уникального значения ключа атрибута среди элементов `<add/>`, содержащихся в элементе `<logGroups>`.

- **Компонентная группа журналов**: элемент `<componentLogGroup>` использует ключевой атрибут, чтобы определить имя группы журналов, которое отображается в списке. Он также использует значение атрибута, которое содержит регулярное выражение (regex). Это регулярное выражение используется для сбора набора сопутствующих файлов журналов.  

- **Статическая группа журналов**: элемент `<staticLogGroup>` использует ключевой атрибут, чтобы определить имя группы журналов, которое отображается в списке. Он также использует значение атрибута, определяющее имя файла журнала.  

Если одно и то же значение ключевого атрибута используется в элементе `<add/>` внутри элементов `<componentLogGroup>` и `<staticLogGroup>`, центр поддержки создаст одну группу. Эта группа включает файлы журнала, определенные в обоих элементах, которые используют один и тот же ключ.

#### <a name="example"></a>Пример
```XML
<logGroups>
  <componentLogGroup>
    <add key="Application Management" value="^(app.*|ci.*|contentaccess|contenttransfermanager|datatransferservice|dcm.*|execmgr.*|UserAffinity.*|.*Handler$|.*Provider$)"/>
    <add key="Client Registration" value="^(clientregistration|locationservices|ccmmessaging|ccmexec)"/>
    <add key="Inventory" value="^(ccmmessaging|inventoryagent|mtrmgr|swmtrreportgen|virtualapp|mtr.*|filesystemfile)"/>
    <add key="Policy" value="^(ccmmessaging|policyagent_.*|policyevaluator_.*)"/>
    <add key="Software Updates" value="^(ci.*|contentaccess|contenttransfermanager|datatransferservice|dcm.*|update.*|wuahandler|xmlstore|scanagent)"/>
    <add key="Software Distribution" value="^(datatransferservice|execmgr.*|contenttransfermanager|locationservices|contentaccess|filebits)"/>
    <add key="Desired Configuration Management" value="^(ci.*|dcm.*)"/>
    <add key="Operating System Deployment" value="^(ts.*)"/>
  </componentLogGroup>
  <staticLogGroup>
    <add key="Application Management" value="ccmsdkprovider.log"/>
    <add key="Desired Configuration Management" value="ccmsdkprovider.log"/>
    <add key="Software Updates" value="ccmsdkprovider.log"/>
  </staticLogGroup>
</logGroups>
```



## <a name="collecting-additional-log-files-using-wildcards"></a><a name="bkmk_wildcards"></a> Сбор дополнительных файлов журналов с использованием подстановочных знаков

Чтобы собрать дополнительные файлы журнала, используйте подстановочные знаки в пути к файлу или имени файла. Эти подстановочные знаки включают переменные среды уровня системы, такие как `%WINDIR%`, но исключают переменные среды уровня пользователя, такие как `%USERPROFILE%`. Чтобы собрать дополнительные файлы журналов с помощью такого нерекурсивного поиска файлов журналов, используйте элемент `<add/>` в элементе `<additionalLogFiles>`. 

Эти примеры показывают, как центр поддержки использует эту функцию в файле конфигурации по умолчанию.

#### <a name="example-1-collect-all-windows-update-log-files-in-the-windows-directory"></a>Пример 1. Сбор всех файлов журналов Центра обновления Windows в каталоге Windows
Следующий элемент будет собирать все файлы с именем `WindowsUpdate.log`, находящиеся в каталоге Windows: 

`<add key="%WINDIR%\WindowsUpdate.log" />`

#### <a name="example-2-collect-all-log-files-in-the-windows-logs-directory"></a>Пример 2: Сбор всех файлов журналов в каталоге журналов Windows
Следующий элемент будет собирать все файлы с `.log` в конце имени, находящиеся в каталоге журналов Windows: 

`<add key="%WINDIR%\logs\*.log" />`

#### <a name="full-example-xml"></a>Полный пример XML
```XML
<CcmLogDataCollector>
  <additionalLogFiles>
    <!-- Collect these additional log files. Can pass in a wildcard for the filename. System variables are also supported. -->
    <!--
    <add key="%WINDIR%\WindowsUpdate.log" />
    <add key="%WINDIR%\logs\*.log" />
    -->
  </additionalLogFiles>
</CcmLogDataCollector>
```
