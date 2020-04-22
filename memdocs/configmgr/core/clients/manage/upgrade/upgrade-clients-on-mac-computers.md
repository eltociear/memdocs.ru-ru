---
title: Обновление клиентов macOS
titleSuffix: Configuration Manager
description: Обновление клиента Configuration Manager на компьютерах Mac.
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 74c60941-5eae-4905-9e58-252bdb39df96
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f34d0c9233b4f7384dfc2280dc92334450a785ed
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696262"
---
# <a name="how-to-upgrade-clients-on-mac-computers-in-configuration-manager"></a>Обновление клиентов на компьютерах Mac в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Ниже приведены общие инструкции по обновлению клиента для компьютеров Mac с помощью приложения Configuration Manager. Можно также скачать файл установки клиента Mac, скопировать его в общую сетевую или локальную папку на компьютере Mac, а затем поручить пользователям выполнить установку вручную.  

> [!NOTE]  
> Прежде чем приступить к выполнению этих действий, убедитесь, что компьютер Mac соответствует необходимым условиям. См. раздел [Поддерживаемые операционные системы для серверов системы сайта](../../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#mac-computers).  

## <a name="download-the-latest-mac-client"></a>Скачайте последнюю версию клиента для Mac.

Клиент Mac для Configuration Manager отсутствует на установочном носителе Configuration Manager. Скачайте [клиент Microsoft Endpoint Configuration Manager для macOS (64-разрядная версия)](https://www.microsoft.com/download/details.aspx?id=100850) в Центре загрузки Майкрософт. Установочные файлы клиента Mac содержатся в файле установщика Windows с именем **ConfigmgrMacClient.msi**.  

## <a name="create-the-mac-client-installation-file"></a>Создание файла установки клиента для Mac

Запустите файл **ConfigmgrMacClient.msi** на компьютере под управлением Windows. Этот установщик распакует файл установки клиента для Mac с именем **Macclient.dmg**. Этот файл по умолчанию можно найти здесь: **C:\Program Files\Microsoft\System Center Configuration Manager for Mac client**.  

## <a name="extract-the-client-installation-files"></a>Извлечение файлов установки клиента

Скопируйте файл **Macclient.dmg** на компьютер Mac. Подключите его в macOS, а затем скопируйте его содержимое в папку на компьютере Mac.  

## <a name="create-a-cmmac-file"></a>Создание CMMAC-файла

1. Откройте папку **Tools** в файлах установки клиента Mac. Используйте средство **CMAppUtil** для создания CMMAC-файла из пакета установки клиента. Этот файл будет использоваться для создания приложения Configuration Manager.  

2. Скопируйте новый файл **CMClient.pkg.cmmac** в сетевую папку, которая доступна для компьютера с консолью Configuration Manager.  

    Дополнительные сведения см. в разделе [Дополнительные процедуры для создания и развертывания приложений для компьютеров Mac](../../../../apps/get-started/creating-mac-computer-applications.md#supplemental-procedures-to-create-and-deploy-applications-for-mac-computers).  

## <a name="create-and-deploy-the-app"></a>Создание и развертывание приложения

1. В консоли Configuration Manager [создайте приложение](../../../../apps/get-started/creating-mac-computer-applications.md) из файла **CMClient.pkg.cmmac**.  

2. [Разверните это приложение](../../../../apps/deploy-use/deploy-applications.md) на компьютерах Mac в своей иерархии.  

## <a name="install-the-updated-client"></a>Установка обновленного клиента

Существующий клиент Configuration Manager на компьютерах Mac сообщит пользователю, что обновление доступно для установки. После установки клиента пользователям необходимо перезапустить свои компьютеры Mac.  

После перезапуска компьютера автоматически запустится мастер **регистрации компьютеров**, чтобы запросить новый сертификат пользователя.

Если вы не используете регистрацию в Configuration Manager и устанавливаете сертификат клиента независимо от Configuration Manager, см. раздел [Настройка клиентов для использования существующего сертификата](#BKMK_UpgradingClient_MachineEnrollment).  

## <a name="configure-clients-to-use-an-existing-certificate"></a><a name="BKMK_UpgradingClient_MachineEnrollment"></a> Настройка клиентов для использования существующего сертификата

Используйте эту процедуру для предотвращения запуска мастера регистрации компьютеров и настройки обновленного клиента на использование существующего сертификата клиента.  

1. В консоли Configuration Manager [создайте элемент конфигурации](../../../../compliance/deploy-use/create-configuration-items-for-mac-os-x-devices-managed-with-the-client.md) с типом **Mac OS X**.  

1. Добавьте к этому элементу конфигурации параметр с типом **Сценарий**.  

1. Добавьте следующий сценарий настройки:  

  ``` Shell
  #!/bin/sh  
  echo "Starting script\n"  
  echo "Changing directory to MAC Client\n"  
  cd /Users/Administrator/Desktop/'MAC Client'/  
  echo "Import root cert\n"  
  /usr/bin/sudo /usr/bin/security import /Users/Administrator/Desktop/'MAC Client'/Root.pfx -A -k /Library/Keychains/System.Keychain -P ROOT  
  echo "Using openssl to convert pfx to a crt\n"  
  /usr/bin/sudo openssl pkcs12 -in /Users/Administrator/Desktop/'MAC Client'/Root.pfx -out Root1.crt -nokeys -clcerts -passin pass:ROOT  
  echo "Adding trust to root cert\n"  
  /usr/bin/sudo /usr/bin/security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.Keychain Root1.crt  
  echo "Import client cert\n"  
  /usr/bin/sudo /usr/bin/security import /Users/Administrator/Desktop/'MAC Client'/MacClient.pfx -A -k /Library/Keychains/System.Keychain -P MAC  
  echo "Executing ccmclient with MP\n"  
  sudo ./ccmsetup -MP https://SCCM34387.SCCM34387DOM.NET/omadm/cimhandler.ashx  
  echo "Editing Plist file\n"  
  sudo /usr/libexec/Plistbuddy -c 'Add:SubjectName string CMMAC003L' /Library/'Application Support'/Microsoft/CCM/ccmclient.plist  
  echo "Changing directory to CCM\n"  
  cd /Library/'Application Support'/Microsoft/CCM/  
  echo "Making connection to the server\n"  
  sudo open ./CCMClient  
  echo "Ending Script\n"  
  exit  
  ```  

1. Добавьте элемент конфигурации в [шаблон базовой конфигурации](../../../../compliance/deploy-use/create-configuration-baselines.md). Затем [разверните его](../../../../compliance/deploy-use/deploy-configuration-baselines.md) на всех компьютерах Mac, на которых установлен сертификат, независимо от Configuration Manager.  
