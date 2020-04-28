---
title: Требования для доступа к Интернету
titleSuffix: Configuration Manager
description: Узнайте о конечных точках Интернета, чтобы обеспечить полную функциональность Configuration Manager.
ms.date: 04/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b34fe701-5d05-42be-b965-e3dccc9363ca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 58afaf564a8afaba4569755575fcc7c1757c5529
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110140"
---
# <a name="internet-access-requirements"></a>Требования для доступа к Интернету

Некоторые функции Configuration Manager зависят от подключения к Интернету. Если ваша организация ограничивает сетевое взаимодействие с Интернетом с помощью брандмауэра или прокси-сервера, убедитесь, что эти конечные точки разрешены.

<!-- SCCMDocs-pr #3403 -->

## <a name="service-connection-point"></a><a name="bkmk_scp"></a> Точка подключения службы

Эти конфигурации применяются к компьютеру, на котором размещена точка подключения службы, и ко всем брандмауэрам между этим компьютером и Интернетом. И компьютер, и брандмауэры должны поддерживать передачу данных на указанные ниже расположения в Интернете через исходящий порт **TCP 443** для HTTPS и исходящий порт **TCP 80** для HTTP.

Точка подключения службы поддерживает веб-прокси (с проверкой подлинности или без нее) для использования этих расположений. Дополнительные сведения см. в статье [Поддержка прокси-сервера](proxy-server-support.md).

Дополнительные сведения о точке подключения службы см. в [этой статье](../../servers/deploy/configure/about-the-service-connection-point.md).

Другим функциям Configuration Manager могут потребоваться дополнительные конечные точки из точки подключения службы. См. сведения в других разделах этой статьи.

> [!TIP]  
> При подключении к `go.microsoft.com` или `manage.microsoft.com` точка подключения службы использует службу Microsoft Intune. Существует известная проблема, когда соединителю Intune не удается установить подключение, если корневой сертификат Baltimore CyberTrust не установлен, истек срок его действия или сертификат поврежден в точке подключения службы. Дополнительные сведения см. в статье базы знаний [KB 3187516. Configuration Manager Service Connection Point doesn't download updates](https://support.microsoft.com/help/3187516) (Точка подключения службы диспетчера конфигурации не загружает обновления).  

Начиная с версии 2002, если серверу сайта Configuration Manager не удается подключиться к необходимым конечным точкам для облачной службы, создается сообщение о критическом состоянии с идентификатором 11488. Если ему не удается подключиться к службе, состояние компонента SMS_SERVICE_CONNECTOR изменяется на критическое. Более подробные сведения о состоянии см.в узле [Состояние компонента](../../servers/manage/use-alerts-and-the-status-system.md#BKMK_MonitorSystemStatus) консоли Configuration Manager.<!-- 5566763 -->

### <a name="updates-and-servicing"></a><a name="bkmk_scp-updates"/> Обновления и обслуживание

Дополнительные сведения об этой функции см. в статье [Обновления и обслуживание для Configuration Manager](../../servers/manage/updates.md).

> [!Tip]  
> Включите эти конечные точки для правила [аналитики управления](../../servers/manage/management-insights.md). **Подключите сайт к облаку Майкрософт для получения обновлений Configuration Manager**.

- `*.akamaiedge.net`  

- `*.akamaitechnologies.com`  

- `*.manage.microsoft.com`  

- `go.microsoft.com`  

- `*.blob.core.windows.net`  

- `download.microsoft.com`  

- `download.windowsupdate.com`  

- `sccmconnected-a01.cloudapp.net`  

- `configmgrbits.azureedge.net`  

### <a name="windows-10-servicing"></a>Обслуживание Windows 10

Дополнительные сведения об этой функции см. в статье [Manage Windows as a service using System Center Configuration Manager](../../../osd/deploy-use/manage-windows-as-a-service.md) (Управление Windows как службой с помощью System Center Configuration Manager).

- `download.microsoft.com`  

- `https://go.microsoft.com/fwlink/?LinkID=619849`  

- `dl.delivery.mp.microsoft.com`  

### <a name="azure-services"></a>Службы Azure

Дополнительные сведения об этой функции см. в статье [Configure Azure services for use with Configuration Manager](../../servers/deploy/configure/azure-services-wizard.md) (Настройка служб Azure для использования с Configuration Manager).

- `management.azure.com`  

## <a name="co-management"></a>Совместное управление

Если вы регистрируете устройства Windows 10 в Microsoft Intune для совместного управления, убедитесь, что эти устройства могут получить доступ к конечным точкам, требуемым Intune. Дополнительные сведения см. в статье [Network endpoints for Microsoft Intune](https://docs.microsoft.com/intune/intune-endpoints) (Конечные точки сети для Microsoft Intune).

## <a name="microsoft-store-for-business"></a>Microsoft Store для бизнеса

При интеграции Configuration Manager с [Microsoft Store для бизнеса](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md) убедитесь, что точка подключения службы и целевые устройства имеют доступ к облачной службе. См. сведения о [конфигурации прокси-сервера Microsoft Store для бизнеса](https://docs.microsoft.com/microsoft-store/prerequisites-microsoft-store-for-business#proxy-configuration).

## <a name="cloud-services"></a><a name="bkmk_cloud"></a> Облачные службы

<!-- SCCMDocs-pr #3402 -->

Сведения в этом разделе охватывают следующие функции:

- шлюз управления облачными клиентами (CMG);
- облачная точка распространения (CDP);
- интеграция с Azure Active Directory (Azure AD);
- обнаружение на основе Azure AD.

Для развертывания службы CMG/CDP **точке подключения службы** требуется доступ к:

- В каждой среде некоторые конечные точки Azure имеют ряд отличий в зависимости от конфигурации. Configuration Manager сохраняет эти конечные точки в базе данных сайта. Чтобы получить список конечных точек Azure, следует запросить таблицу **AzureEnvironments** в SQL Server.  

Для **точки подключения CMG** требуется доступ к следующим конечным точкам службы:

- Конечная точка управления службами: `https://management.core.windows.net/`  

- Конечная точка хранилища: `<name>.blob.core.windows.net` и `<name>.table.core.windows.net`

    Здесь `<name>` — это имя облачной службы CMG или CDP. Например, если CMG — `GraniteFalls.CloudApp.Net`, то первая конечная точка хранилища, которую нужно разрешить, — `GraniteFalls.blob.core.windows.net`.<!-- SCCMDocs#2288 -->

Для извлечения маркера Azure AD с помощью **консоли** и **клиента Configuration Manager**:

- ActiveDirectoryEndpoint (`https://login.microsoftonline.com/`).  

Для обнаружения пользователей Azure AD **точке подключения служб** требуется доступ к:

- версия 1810 и прежние версии: конечной точке AAD Graph (`https://graph.windows.net/`);  

- версия 1902 и более поздние версии: конечной точке Microsoft Graph (`https://graph.microsoft.com/`).

Система сайта точки подключения шлюза управления облачными клиентами (CMG) поддерживает использование веб-прокси. Дополнительные сведения о настройке этой роли для прокси-сервера см. в статье [Поддержка прокси-сервера](proxy-server-support.md#configure-the-proxy-for-a-site-system-server). Точка подключения CMG должна подключаться только к конечным точкам службы CMG. Ей не требуется доступ к другим конечным точкам Azure.

Дополнительные сведения о CMG см. в статье [Планирование работы шлюза управления облачными клиентами в Configuration Manager](../../clients/manage/cmg/plan-cloud-management-gateway.md).

## <a name="software-updates"></a><a name="bkmk_sum"></a> Обновления программного обеспечения

Разрешите активной точке обновления программного обеспечения доступ к следующим конечным точкам, чтобы WSUS и автоматические обновления могли взаимодействовать с облачной службой Центра обновления Майкрософт:  

- `http://windowsupdate.microsoft.com`  

- `http://*.windowsupdate.microsoft.com`  

- `https://*.windowsupdate.microsoft.com`  

- `http://*.update.microsoft.com`  

- `https://*.update.microsoft.com`  

- `http://*.windowsupdate.com`  

- `http://download.windowsupdate.com`  

- `http://download.microsoft.com`  

- `http://*.download.windowsupdate.com`  

- `http://test.stats.update.microsoft.com`  

- `http://ntservicepack.microsoft.com`  

Дополнительные сведения см. в статье [Plan for software updates in Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md) (Планирование обновлений программного обеспечения в Configuration Manager).

### <a name="intranet-firewall"></a>Брандмауэр интрасети

Вам может потребоваться добавить конечные точки в брандмауэр, который находится между двумя системами сайта, в следующих случаях:

- наличие точки обновления программного обеспечения на дочерних сайтах;
- если на сайте присутствует удаленная активная точка обновления программного обеспечения интернет-клиентов.

#### <a name="software-update-point-on-the-child-site"></a>Точка обновления программного обеспечения на дочернем сайте

- `http://<FQDN for software update point on child site>`  

- `https://<FQDN for software update point on child site>`  

- `http://<FQDN for software update point on parent site>`  

- `https://<FQDN for software update point on parent site>`  

## <a name="manage-office-365"></a>Управление Office 365

> [!NOTE]
> Начиная с 21 апреля 2020 г. Office 365 профессиональный плюс переименовывается в **Приложения Microsoft 365 для предприятия**. Дополнительные сведения см. в статье [Изменение названия Office 365 профессиональный плюс](https://docs.microsoft.com/deployoffice/name-change). Пока консоль Configuration Manager обновляется, в ней и в сопутствующей документации может встречаться старое название.

Если вы используете Configuration Manager для развертывания и обновления Приложений Microsoft 365 для предприятия, разрешите доступ к следующим конечным точкам:

<!-- SCCMDocs#929 -->

- `officecdn.microsoft.com` для синхронизации точки обновления программного обеспечения для обновлений клиента Приложений Microsoft 365 для предприятия;

- `config.office.com` для создания пользовательских конфигураций для развертываний Приложений Microsoft 365 для предприятия.

## <a name="configuration-manager-console"></a>Консоль Configuration Manager

Компьютерам с консолью Configuration Manager для определенных функций требуется доступ к следующим конечным точкам Интернета:

### <a name="in-console-feedback"></a>Обратная связь в консоли

- `http://petrol.office.microsoft.com`

Дополнительные сведения об обратной связи по продукту см. в [этом разделе](../../understand/find-help.md#product-feedback).

### <a name="community-workspace-documentation-node"></a>Рабочая область "Сообщество", узел документации

- `https://aka.ms`

- `https://raw.githubusercontent.com`

Дополнительные сведения см. в статье [Использование консоли Configuration Manager](../../servers/manage/admin-console.md).

<!-- 
Community Hub
when in current branch, get details from SCCMDocs-pr #3403 
 -->

### <a name="monitoring-workspace-site-hierarchy-node"></a>Рабочая область "Наблюдение", узел иерархии сайтов

Если вы используете **географическое представление**, разрешите доступ к следующей конечной точке:

- `http://maps.bing.com`

## <a name="desktop-analytics"></a>Аналитика компьютеров

Дополнительные сведения о необходимых конечных точках для облачной службы Аналитики компьютеров см. в статье [Enable data sharing for Desktop Analytics](../../../desktop-analytics/enable-data-sharing.md#endpoints) (Обеспечение обмена данными для Desktop Analytics).

## <a name="microsoft-public-ip-addresses"></a>Общедоступные IP-адреса Майкрософт

Дополнительные сведения об общедоступных диапазонах IP-адресов Майкрософт см. в [этом документе](https://www.microsoft.com/download/details.aspx?id=53602). Эти адреса регулярно обновляются. Там нет детализации по службам, и любой IP-адрес в этих диапазонах может быть использован.

## <a name="see-also"></a>См. также

- [Порты, используемые в Configuration Manager](../hierarchy/ports.md)

- [Поддержка прокси-сервера в Configuration Manager](proxy-server-support.md)
