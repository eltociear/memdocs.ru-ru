---
title: Синхронизация обновлений Office 365 без подключения к Интернету
titleSuffix: Configuration Manager
description: Вы можете выполнять синхронизацию обновлений Office 365 в точке обновления ПО верхнего уровня, отключенной от Интернета.
ms.date: 04/21/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: a8fa7e7a-bf55-42de-b0c2-c56777dc1508
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: 3627d2f7772b7b9e133d742b0ee4f94dba6e457a
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110361"
---
# <a name="synchronize-office-365-updates-from-a-disconnected-software-update-point"></a><a name="bkmk_O365"></a> Синхронизация обновлений Office 365 с отключенной точки обновления программного обеспечения

*Область применения: Configuration Manager (Current Branch)*
<!--4065163-->
Начиная с Configuration Manager версии 2002, вы можете использовать средство для импорта обновлений Office 365 с подключенного к Интернету сервера WSUS в отключенную среду Configuration Manager. Ранее при экспорте и импорте метаданных для программного обеспечения, обновленного в отключенных средах, не удавалось выполнить развертывание обновлений Office 365. Для обновлений Office 365 требуются дополнительные метаданные, скачанные из API Office и CDN Office, что невозможно для отключенных сред.

> [!Note]
> Начиная с 21 апреля 2020 г. Office 365 профессиональный плюс переименовывается в **Приложения Microsoft 365 для предприятия**. Дополнительные сведения см. в статье [Изменение названия Office 365 профессиональный плюс](https://docs.microsoft.com/deployoffice/name-change). Пока консоль Configuration Manager обновляется, в ней и в сопутствующей документации может встречаться старое название.

## <a name="prerequisites"></a>Предварительные условия

- Сервер WSUS, подключенный к Интернету и работающий на Windows Server версии не ниже 2012.
- Для сервера WSUS требуется подключение к следующим двум конечным точкам в Интернете:
   - `officecdn.microsoft.com`
   - `config.office.com`
- Скопируйте средство OfflineUpdateExporter и его зависимости на подключенный к Интернету сервер WSUS.
  - Средство и его зависимости находятся в каталоге **&lt;ConfigMgrInstallDir>/tools/OfflineUpdateExporter**.
- Пользователь, запускающий средство, должен быть участником группы **Администраторы WSUS**.
- Каталог, созданный для хранения метаданных и содержимого обновления Office, должен иметь соответствующие списки управления доступом (ACL) для защиты файлов.
    - Кроме того, этот каталог должен быть пустым.
- Перемещение данных с онлайн сервера WSUS в отключенную среду следует выполнять в безопасном режиме.

> [!IMPORTANT]
> Будет скачиваться содержимое для всех языков Office 365. Каждое обновление может иметь приблизительно 10 ГБ содержимого.

## <a name="synchronize-then-decline-unneeded-office-365-updates"></a>Синхронизация и последующее отклонение ненужных обновлений Office 365

1. Из подключенных к Интернету служб WSUS откройте консоль WSUS.
1. Выберите меню **Параметры**, а затем щелкните элемент **Продукты и классификация**.
1. На вкладке **Продукты** выберите **клиент Office 365**, а затем **Обновления** на вкладке **Классификации**. [![Продукты и классификации для обновлений Office 365 в WSUS](./media/4065163-o365-updates-product-classification.png)](./media/4065163-o365-updates-product-classification.png#lightbox)
1. Перейдите в раздел **Синхронизация** и выберите **Синхронизировать сейчас**, чтобы получить обновления Office 365 в WSUS.
1. После завершения синхронизации отклоните все обновления Office 365, которые не нужно развертывать с помощью Configuration Manager. Подтверждение скачивания обновлений Office 365 не требуется.  
   - Отклонение нежелательных обновлений Office 365 в WSUS не приводит к отмене их экспорта во время экспорта WsusUtil.exe, но не дает инструменту OfflineUpdateExporter скачивать для них содержимое.
   - Инструмент OfflineUpdateExporter выполняет скачивание обновлений Office 365 за вас. Скачивание других продуктов все равно следует подтверждать, если вы экспортируете для них обновления.
    - Создайте [новое представление обновления в WSUS](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/manage/viewing-and-managing-updates#to-create-a-new-update-view-on-wsus), чтобы легко обнаруживать и отклонять ненужные обновления Office 365 в WSUS.
1. Если вы одобряете скачивание и экспорт других обновлений продуктов, дождитесь завершения скачивания содержимого, прежде чем запустить экспорт WsusUtil.exe и копировать содержимое папки WSUSContent. Дополнительные сведения см. в статье [Synchronize software updates from a disconnected software update point](synchronize-software-updates-disconnected.md) (Синхронизация обновлений программного обеспечения из отсоединенной точки обновления программного обеспечения)

## <a name="exporting-the-office-365-updates"></a>Экспорт обновлений Office 365

1. Скопируйте папку OfflineUpdateExporter из Configuration Manager на сервер WSUS, подключенный к Интернету.
    - Средство и его зависимости находятся в каталоге **&lt;ConfigMgrInstallDir>/tools/OfflineUpdateExporter**.
1. Из командной строки на сервере WSUS, подключенном к Интернету, запустите инструмент со следующими параметрами потребления: **OfflineUpdateExporter.exe -O -D &lt;путь_назначения>**

   |Параметр OfflineUpdateExporter|Описание:|
   |---|---|
   |**-O**|  **-Office**. Определяет продукт для экспорта обновлений Office 365.|
   |**-D**|**-Destination**. Назначение (Destination) —это необходимый параметр. Также требуется полный путь к целевой папке.|

   - Инструмент **OfflineUpdateExporter** выполняет такие действия:
      - подключается к WSUS;
      - считывает метаданные обновления Office 365 в WSUS;
      - скачивает содержимое и любые дополнительные метаданные, необходимые для обновлений Office 365, в папку назначения.

1. В командной строке на сервере WSUS, подключенном к Интернету, перейдите в папку, содержащую файл WsusUtil.exe. По умолчанию средство находится в каталоге %*ProgramFiles*%\Update Services\Tools. Например, если средство находится в расположении по умолчанию, введите **cd %ProgramFiles%\Update Services\Tools**.
   - Если вы используете Windows Server 2012, убедитесь, что на серверах WSUS установлено исправление [KB2819484](https://support.microsoft.com/help/2819484/cab-file-that-is-exported-by-using-the-wsusutil-exe-command-is-display).
   - Пользователь, работающий со средством WsusUtil, должен быть участником локальной группы "Администраторы" на сервере.

1. Чтобы экспортировать метаданные обновлений программного обеспечения в GZIP-файл, введите:  

    **WsusUtil.exe export**  *имя_пакета*  *файл_журнала*  

    Пример.  

    **WsusUtil.exe export export.xml.gz export.log**

1. Скопируйте файл **export.xml.gz** на сервер WSUS верхнего уровня при отключенной сети.
1. Если вы одобрили обновления для других продуктов, скопируйте содержимое папки WSUSContent в папку WSUSContent отключенного сервера WSUS верхнего уровня.
1. Скопируйте папку назначения, используемую для **OfflineUpdateExporter**, на сервер сайта верхнего уровня Configuration Manager при отключенной сети.

## <a name="import-the-office-365-updates"></a>Импорт обновлений Office 365

1. На отключенном сервере WSUS верхнего уровня импортируйте метаданные обновления с **export.xml.gz**, сгенерированные на сервере WSUS, подключенном к Интернету.
   
    Пример.  

    **WsusUtil.exe import export.xml.gz import.log**
    
    По умолчанию средство WsusUtil.exe находится в каталоге %*ProgramFiles*%\Update Services\Tools.

1. После завершения импорта вам нужно будет настроить свойство управления сайтом на отключенном сервере сайта Configuration Manager верхнего уровня. Это изменение конфигурации указывает на то, что Configuration Manager относится к содержимому Office 365. Чтобы изменить конфигурацию свойства, выполните приведенные ниже действия.
   1. Скопируйте сценарий [O365OflBaseUrlConfigured PowerShell](#bkmk_o365_script) на сервер сайта Configuration Manager верхнего уровня, отключенный от сети.
   1. Измените `"D:\Office365updates\content"` на полный путь скопированного каталога, содержащего содержимое и метаданные Office, созданные OfflineUpdateExporter.
      > [!IMPORTANT]
      > Для свойства O365OflBaseUrlConfigured работают только локальные пути.
   1. Сохраните скрипт как `O365OflBaseUrlConfigured.ps1`
   1. Из всплывающего окна PowerShell на отключенном сервере сайта Configuration Manager верхнего уровня запустите `.\O365OflBaseUrlConfigured.ps1`.
   1. Перезапустите службу **SMS_Executive** на сервере сайта.
1. В консоли **Configuration Manager** последовательно выберите **Администрирование** > **Конфигурация сайта** > **Сайты**.
1. Щелкните правой кнопкой мыши сайт верхнего уровня и последовательно выберите **Настройка компонентов сайта** > **Точка обновления программного обеспечения**.
1. На вкладке **Классификации** выберите *Обновления*. Во вкладке **Продукты** выберите *клиента Office 365*.
1. [Синхронизация обновлений программного обеспечения](synchronize-software-updates.md#manually-start-software-updates-synchronization) для Configuration Manager
1. После завершения синхронизации используйте для развертывания обновлений Office 365 обычный процесс.

## <a name="proxy-configuration"></a><a name="bkmk_O365_ki"></a> Конфигурация прокси-сервера

- Конфигурация прокси не встроена в инструмент. Если на сервере, где запущен инструмент, прокси-сервер установлен в пункте "Свойства браузера", то теоретически будет использоваться именно этот прокси-сервер, следовательно он должен правильно функционировать.
   - Запустите `netsh winhttp show proxy` из командной строки, чтобы увидеть настроенный прокси.



## <a name="modify-o365oflbaseurlconfigured-property"></a><a name="bkmk_o365_script"></a> Изменение свойства O365OflBaseUrlConfigured

```powershell
# Name: O365OflBaseUrlConfigured.ps1
#
# Description: This sample sets the O365OflBaseUrlConfigured property for the SMS_WSUS_CONFIGURATION_MANAGER component on the top-level site.
# This script must be run on the disconnected top-level Configuration Manager site server
#
# Replace "D:\Office365updates\content" with the full path to the copied directory containing all the Office metadata and content generated by the OfflineUpdateExporter tool.
# Only local paths work for the O365OflBaseUrlConfigured property.

$PropertyValue = "D:\Office365updates\content"

# Don't change any of the lines below
$PropertyName = "O365OflBaseUrlConfigured"

# Get provider instance
$providerMachine = Get-WmiObject -namespace "root\sms" -class "SMS_ProviderLocation"

if($providerMachine -is [system.array])
{
    $providerMachine=$providerMachine[0]
}

$SiteCode = $providerMachine.SiteCode

$component = gwmi -ComputerName $providerMachine.Machine -namespace root\sms\site_$SiteCode -query 'select comp.* from sms_sci_component comp join SMS_SCI_SiteDefinition sdef on sdef.SiteCode=comp.SiteCode where sdef.ParentSiteCode="" and comp.componentname="SMS_WSUS_CONFIGURATION_MANAGER"'
$properties = $component.props

Write-host "Updating $PropertyName property for site " $SiteCode

foreach ($property in $properties)
{
  if ($property.propertyname -eq $PropertyName) 
  {
    Write-host "Current value for $PropertyName is $($property.value2)"
    $property.value2 = $PropertyValue
    Write-host "Updating value for $PropertyName to $($property.value2)"
    break
  }
}

$component.props = $properties
$component.put()
```

## <a name="next-steps"></a>Дальнейшие шаги

[Добавление обновлений программного обеспечения в группу обновлений](../deploy-use/add-software-updates-to-an-update-group.md)