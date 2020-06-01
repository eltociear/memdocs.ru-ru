---
title: XML-параметры конфигурации подключаемого модуля
titleSuffix: Configuration Manager
description: Технический справочник по XML-элементам подключаемого модуля диспетчера преобразования пакетов.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 940cc075-4066-44d5-972a-927c0b0a1143
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 9178b595ba67723c623979b4c29290e42fe5f6ac
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/27/2020
ms.locfileid: "83877749"
---
# <a name="technical-reference-for-the-package-conversion-manager-plug-in-configuration-xml"></a>Технический справочник по XML-параметрам конфигурации подключаемого модуля диспетчера преобразования пакетов

*Область применения: Configuration Manager (Current Branch)*

<!--1357861-->

В этой статье описываются XML-элементы в файле конфигурации Configuration Manager (Microsoft.ConfigurationManagement.exe.config), которые управляют операциями подключаемого модуля диспетчера преобразования пакетов. Дополнительные сведения о том, как использовать подключаемый модуль, см. в разделе [Применение подключаемого модуля диспетчера преобразования пакетов](how-to-use-plug-in.md).



## <a name="xml-configuration-elements"></a>XML-элементы конфигурации

В приведенной ниже таблице описаны XML-элементы в файле конфигурации Configuration Manager, которые относятся к подключаемому модулю "Диспетчер преобразования пакетов".

|Элемент  |Type  |Описание:  |
|---------|---------|---------|
|**PcmPlugIn**|Строка|Имя сценария или исполняемого файла для использования в качестве подключаемого модуля диспетчера преобразования пакетов.|
|**PcmPlugInTimeoutMilliseconds**|Целое число|Максимальное время (в миллисекундах) ожидания выполнения обработки пакета сценарием подключаемого модуля диспетчера преобразования пакетов или исполняемым файлом.|
|**PcmPluginExitCode**|Целое число|Код выхода, ожидаемый от процесса подключаемого модуля. Это значение указывает на успешное завершение. Все другие коды считаются ошибками.|
|**ForceRequirementsExtraction**|Логическое значение|Разрешить автоматическое преобразование для требований коллекции, связанных с пакетом. Для этого параметра значение "True" должно быть выбрано только при работе с подключаемым модулем диспетчера преобразования пакетов, предназначенным для принятия решений о том, какие требования использовать.|



## <a name="sample-configuration-xml"></a>Пример XML-элементов конфигурации

В этом разделе приводится пример XML-элементов конфигурации диспетчера преобразования пакетов в файле конфигурации Configuration Manager **Microsoft.ConfigurationManagement.exe.config**. По умолчанию этот файл расположен по следующему пути.  
`C:\Program Files (x86)\Microsoft Endpoint Manager\AdminConsole\bin\Microsoft.ConfigurationManagement.exe.config`

> [!IMPORTANT]
> Начиная с версии 1910, этот путь изменился и ведет в папку `Microsoft Endpoint Manager`. Убедитесь, что вы не используете файл старой версии, расположенный в другой папке. 

В этом примере элементы, относящиеся к диспетчеру преобразования пакетов, находятся внутри следующего элемента: `Microsoft.ConfigurationManagement.UserCentric.Workflow.Properties.Settings`

``` XML
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
...
    </Microsoft.ConfigurationManagement.AdminConsole.Properties.Settings>
    <Microsoft.ConfigurationManagement.UserCentric.Workflow.Properties.Settings>
      <setting name="DecisionVerbosity" serializeAs="String">
        <value>2</value>
      </setting>
      <setting name="PcmPlugIn" serializeAs="String">
        <value>pcmplugin.vbs</value>
      </setting>
      <setting name="PcmPlugInTimeoutMilliseconds" serializeAs="String">
        <value>10000</value>
      </setting>
      <setting name="PcmPluginExitCode" serializeAs="String">
        <value>0</value>
      </setting>
      <setting name="ForceRequirementsExtraction" serializeAs="String">
        <value>True</value >
      </setting>
    </Microsoft.ConfigurationManagement.UserCentric.Workflow.Properties.Settings>
  </applicationSettings>
...
```

