---
title: Выпуски Technical Preview
titleSuffix: Configuration Manager
description: Сведения о ветви Technical Preview, которая позволяет протестировать новые функции и возможности в Configuration Manager.
ms.date: 05/29/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e4c0842a3e23eb8503c945073a4be35db5173086
ms.sourcegitcommit: 0d2f6132428b5fa994e5b770ab1d2bf7d78ac179
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/30/2020
ms.locfileid: "84226257"
---
# <a name="technical-preview-for-configuration-manager"></a>Technical Preview для Configuration Manager

*Область применения: Configuration Manager (ветвь Technical Preview)*

В этой статье содержатся сведения о ежемесячных выпусках ветви Technical Preview для Configuration Manager. В версии Technical Preview представлены новые функции, над которыми работает команда Майкрософт. В ней представлены новые функции, которые еще не включены в ветвь Current Branch для Configuration Manager. Эти функции в конечном итоге могут появиться в обновление для ветви Current Branch. Прежде чем будут выпущены окончательные версии функций, мы хотим, чтобы вы опробовали их и поделились с нами своими впечатлениями.

Так как это ознакомительная техническая версия, сведения и функции могут быть изменены.

Эти сведения относятся ко всем версиям ветви Technical Preview для Configuration Manager. В этой статье перечислены все новые функции с указанием версий Technical Preview, в которых они впервые появились. Например, версия **2001** за январь (`01`) 2020 года (`20`). Каждой версии Preview посвящена отдельная статья с подробными сведениями о каждой функции.

Сведения о новых возможностях в ветви *Current Branch* для Configuration Manager см. в статье [Новые возможности в добавочных версиях System Center Configuration Manager](../plan-design/changes/whats-new-incremental-versions.md).

> [!Tip]
> Чтобы получать уведомления при обновлении этой страницы, скопируйте и вставьте следующий URL-адрес в средство чтения веб-канала RSS: `https://docs.microsoft.com/api/search/rss?search=%22technical+preview+releases+-+Configuration+Manager%22&locale=en-us`.

## <a name="requirements-and-limitations"></a><a name="bkmk_reqs"></a> Требования и ограничения

> [!IMPORTANT]
> Версия Technical Preview лицензирована только для работы в лабораторной среде. Корпорация Майкрософт может не предоставлять услуги поддержки, и некоторые функции могут быть недоступны в технических версиях. Кроме того, в технической версии могут использоваться урезанные или отличающиеся от коммерческой версии программного обеспечения стандарты безопасности, конфиденциальности, специальных возможностей и надежности.

Сведения о большинстве предварительных требований для продукта см. в статье [Поддерживаемые конфигурации для System Center Configuration Manager](../plan-design/configs/supported-configurations.md). Для ветви Technical Preview действуют следующие ограничения:

- Каждая установка активна в течение 90 дней, по истечении которых она становится неактивной.

- Поддерживается только английский язык.

- В командной строке программы установки поддерживаются только такие параметры:

  - `/silent`
  - `/testdbupgrade`

- При установке для точки подключения службы задается оперативный режим. Она не поддерживает работу в автономном режиме.

- Статьи по каждой отдельной версии Technical Preview содержат дополнительные ограничения или требования при их наличии.

- В ветви Technical Preview не поддерживаются следующие функции.

  - [Переход](../migration/migrate-data-between-hierarchies.md) на эту предварительную ветвь или с нее.

  - [Обновление](../servers/deploy/install/upgrade-to-configuration-manager.md) до этой предварительной ветви.

  - [Восстановление сайта](../servers/manage/recover-sites.md) из папки cd.latest.<!--507106-->

- Обновление этой предварительной ветви до ветви Current Branch не поддерживается.

    > [!Note]
    > Когда для предварительной версии доступны обновления, их по прежнему можно найти на узле **Обновления и обслуживание** консоли Configuration Manager и установить из него. Процесс обновления в консоли см. в видеоролике [на сайте youtube.com](https://www.youtube.com/embed/KBd_EGFbUT8).

- Предварительная ветвь поддерживает только автономный первичный сайт. Сайт центра администрирования и несколько первичных или вторичных сайтов не поддерживаются.

Ветвь Technical Preview для Configuration Manager поддерживает описанные ниже продукты и технологии.

- Если не указано иное, ветвь Technical Preview поддерживает те же версии SQL Server, что и Current Branch. Дополнительные сведения см. в разделе [Поддерживаемые версии SQL Server](../plan-design/configs/support-for-sql-server-versions.md).

- Сайт поддерживает до 10 клиентов, которые могут работать под управлением любой [поддерживаемой версии клиентской операционной системы](../plan-design/configs/supported-operating-systems-for-clients-and-devices.md).<!-- SCCMDocs#1656 -->

> [!Note]
> Перечисление этих версий здесь не означает расширение их поддержки за пределами индивидуальных жизненных циклов поддержки. Configuration Manager не поддерживает продукты, жизненный цикл поддержки которых уже завершился. Дополнительные сведения см. в статье [Политика жизненного цикла поддержки Майкрософт](https://support.microsoft.com/lifecycle).

## <a name="install-and-update"></a><a name="bkmk_install"></a> Установка и обновление

Ветвь Technical Preview для Configuration Manager, предназначенная для тестового использования, отличается от ветви Current Branch для Configuration Manager, предназначенной для использования в рабочей среде.

Сначала установите базовую версию ветви Technical Preview. После установки базовой версии воспользуйтесь функцией обновления в консоли, чтобы установить все обновления для актуальной предварительной версии. Обычно новые версии Technical Preview выходят каждый месяц.

Майкрософт поддерживает каждую версию Technical Preview, пока не выйдут три последующие версии. Например, с выпуском версии 1908 прекращается поддержка версии 1904, а версии 1905, 1906 и 1907 продолжают поддерживаться. Когда поддержка базовой версии прекращается, она все еще поддерживается для установки нового сайта Technical Preview, так как предполагается, что вы сразу же обновите ее до поддерживаемой версии. Старая базовая версия поддерживается до выхода новой базовой версии. Обновите базовую версию до последней доступной версии, а затем повторяйте процесс обновления, пока не будет установлена актуальная версия Technical Preview.

> [!TIP]
> При установке обновления для Technical Preview предварительная установка обновляется до этой новой версии Technical Preview. Версию Technical Preview невозможно обновить до версии Current Branch. Кроме того, предварительная версия никогда не получает обновления из ветви Current Branch.
>
> Несколько раз на протяжении года выпускаются версии ветвей Technical Preview и Current Branch с одинаковым номером версии. Например, наряду с версией 1910 из ветви Technical Preview существует версия 1910 из ветви Current Branch.

### <a name="active-baseline-versions"></a>Активные базовые версии

Базовую версию можно установить на один год с момента ее выпуска. Используйте последнюю базовую версию при установке нового технического сайта предварительной версии.

- **Техническая предварительная версия 2002**. Техническая предварительная версия Configuration Manager 2002 доступна как через обновление в консоли, так и в качестве новой базовой версии.

Вы можете скачать базовые версии на странице [Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).

## <a name="providing-feedback"></a><a name="BKMK_TPFeedback"></a> Обратная связь

Мы будем рады узнать ваше мнение о новых функциях в версии Technical Preview. Дополнительные сведения см. в статье [Отзыв о продукте](../understand/find-help.md#product-feedback).

Если у вас есть какие-либо идеи о новых возможностях, которые могут быть вам полезны, сообщите нам о них. Вы можете делиться своими идеями и голосовать за идеи, предложенные другими: [Configuration Manager UserVoice](https://configurationmanager.uservoice.com).

<!--
## <a name="bdmk_tpknownissues"></a> General changes introduced in technical preview branch

<!-- (explanatory comment)
Enable this section if needed to include any broad change to the tech preview branch
-->

## <a name="features-in-the-most-recent-version"></a><a name="bkmk_tpCaps"></a> Функции, доступные в новой версии

<!-- (explanatory comment)
This is the full list of new features in the latest TP release

bullet format:
<!-- - [title](2020/technical-preview-2005.md) <!--ID-->

Ниже приведены функции, представленные в последней версии Technical Preview для Configuration Manager.

### <a name="technical-preview-version-2005"></a>Technical Preview версии 2005

- [Присоединение арендатора: Временная шкала устройства в Центре администрирования](2020/technical-preview-2005.md#bkmk_timeline) <!--7141381-->
- [Присоединение арендатора: установка приложения из Центра администрирования](2020/technical-preview-2005.md#bkmk_apps) <!--6024389-->
- [Присоединение арендатора: CMPivot из Центра администрирования](2020/technical-preview-2005.md#bkmk_cmpivot) <!--6024392-->
- [Присоединение арендатора: запуск сценариев из Центра администрирования](2020/technical-preview-2005.md#bkmk_scripts) <!--6234688-->
- [Тип границы VPN](2020/technical-preview-2005.md#bkmk_vpn) <!--7020519-->
- [Проверка подлинности Azure AD в Центре программного обеспечения](2020/technical-preview-2005.md#bkmk_availapp) <!--6935376-->
- [Установка и обновление клиента с лимитным подключением](2020/technical-preview-2005.md#bkmk_meter) <!--6976145-->
- [Поддержка носителей последовательности задач для облачного содержимого](2020/technical-preview-2005.md#bkmk_tsmedia) <!--6209223-->
- [Улучшения командлетов шлюза управления облачными клиентами](2020/technical-preview-2005.md#bkmk_pwshcmg) <!--6978300-->
- [Центр сообщества и GitHub](2020/technical-preview-2005.md#community-hub-and-github) <!--3555935-->
- [Приложения Microsoft 365 для предприятия](2020/technical-preview-2005.md#bkmk_365_apps) <!--6298093-->
- [Сбои при установке и обновлении отчетов в корпорацию Майкрософт](2020/technical-preview-2005.md#report-setup-and-upgrade-failures-to-microsoft) <!--5622909-->
- [Уведомление об истечении срока действия секретного ключа приложения Azure AD](2020/technical-preview-2005.md#bkmk_alertkey) <!--6386392-->
- [Улучшения этапов последовательности задач BitLocker](2020/technical-preview-2005.md#bkmk_tsbitlocker) <!--6995601-->
- [Улучшения средства очистки библиотеки содержимого](2020/technical-preview-2005.md#bkmk_content) <!--6887878-->
- [Удаление командной строки во время обновления Windows 10 на месте](2020/technical-preview-2005.md#bkmk_ipucmd) <!--2837795-->

> [!NOTE]
> Функции, которые были доступны в предыдущей версии Technical Preview, остаются доступными в последующих версиях. Таким же образом функции, добавленные в ветвь Current Branch для Configuration Manager, остаются доступными в ветви Technical Preview.

## <a name="features-in-recent-technical-previews"></a>Функции в последних версиях Technical Preview

<!-- (explanatory comment)
This is the full list of new features in the past TP releases since the last CB release.
Each month, add features from the list above to a new H3 section at the top of this section.
When there's a new CB, add any features not in that CB to the table in H2 "Features in previous technical previews"
-->

Следующие функции были выпущены в прошлых версиях Configuration Manager ветви Technical Preview с момента выхода выпуска Current Branch версии 2002.

> [!TIP]
> При выходе новой версии Current Branch доступные в ней функции приводятся в актуальном выпуске статьи *Новые возможности*. Дополнительные сведения: [Новые возможности в добавочных версиях](../plan-design/changes/whats-new-incremental-versions.md#supported-versions).

### <a name="technical-preview-version-2004"></a>Technical Preview версии 2004

- [Подключение арендатора Microsoft Endpoint Manager: сведения о клиенте ConfigMgr](2020/technical-preview-2004.md#bkmk_mem) <!--6374854-->
- [Уведомления от Майкрософт](2020/technical-preview-2004.md#notifications-from-microsoft) <!--3953121-->
- [Копирование данных обнаружения из консоли](2020/technical-preview-2004.md#bkmk_copydisco) <!--6890051-->
- [Улучшения CMPivot](2020/technical-preview-2004.md#improvements-to-cmpivot) <!--6518631-->
- [Поддержка PowerShell версии 7](2020/technical-preview-2004.md#bkmk_pwsh7) <!--6023299-->
- [Улучшение этапа последовательности задач "Отформатировать диск и создать разделы"](2020/technical-preview-2004.md#bkmk_osdpart) <!--6610288-->
- [Правила аналитики управления для развертывания ОС](2020/technical-preview-2004.md#bkmk_osdmi) <!--6982275-->
- [Командлеты PowerShell для типов развертывания последовательности задач](2020/technical-preview-2004.md#bkmk_osdpwsh) <!--7019342-->

### <a name="technical-preview-version-2003"></a>Техническая предварительная версия 2003

- [Подключение клиентов Configuration Manager к ATP в Microsoft Defender через центр администрирования Microsoft Endpoint Manager](2020/technical-preview-2003.md#bkmk_atp) <!--5691658-->
- [Отслеживание исправлений элементов конфигурации](2020/technical-preview-2003.md#bkmk_track) <!--4261411 in 2002-->
- [Отображение групп границ для устройств](2020/technical-preview-2003.md#bkmk_boundary) <!--6521835 in 2002-->
- [Новый мастер отзывов](2020/technical-preview-2003.md#bkmk_feedback) <!--3180826-->
- [Улучшения в панели мониторинга "Управление Microsoft Edge"](2020/technical-preview-2003.md#bkmk_edge) <!--5907383-->
- [Улучшения CMPivot](2020/technical-preview-2003.md#bkmk_cmpivot) <!--6518631-->
- [Запрос об отзывах, отправленный в Майкрософт](2020/technical-preview-2003.md#bkmk_smile) <!--6488450-->
- [Новый метод пакета SDK для выполнения последовательности задач](2020/technical-preview-2003.md#bkmk_tsapi) <!--6448458-->
- [Улучшение развертывания операционной системы](2020/technical-preview-2003.md#bkmk_osd) <!--6452769-->

## <a name="features-in-previous-technical-previews"></a>Функции в предыдущих версиях Technical Preview

<!-- (explanatory comment)
This is the list of individual features that are still in TP (not in CB). 
Copy from the lists above any individual features that are still in TP and add to the top of this list
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

Ниже приведены функции, представленные в предыдущих версиях ветви Technical Preview для Configuration Manager. Эти функции останутся доступными в следующих версиях, но они пока еще недоступны в ветви Current Branch.

| Компонент        | Версия Technical Preview |
|----------------|---------------------------|
| Прикрепление файлов к отзыву <!--3556011--> | [Technical Preview 1910](2019/technical-preview-1910.md#attach-files-to-feedback) |
| Улучшения точек распространения с поддержкой многоадресной рассылки <!--3785535--> | [Technical Preview 1908.2](2019/technical-preview-1908-2.md#bkmk_multicast) |
| Шаблоны поэтапного развертывания <!--4961086--> | [Technical Preview 1908](2019/technical-preview-1908.md#phased-deployment-templates) |
| Удаленное управление в любом месте с помощью шлюза управления облаком <!--4575930--> | [Technical Preview 1906](2019/technical-preview-1906.md#remote-control-anywhere-using-cloud-management-gateway) |
| Улучшения Центра сообщества <!--3555935--> | [Technical Preview 1906](2019/technical-preview-1906.md#bkmk_hub) |
| Улучшения Центра сообщества <!--4224401--> | [Technical Preview 1905](2019/technical-preview-1905.md#bkmk_hub) |
| Центр сообщества и GitHub <!--3555935--> | [Technical Preview 1904](2019/technical-preview-1904.md#community-hub-and-github) |
| Калькулятор стоимости облачных служб <!--3555774--> | [Улучшение при создании носителей для последовательности задач](2019/technical-preview-1903.md#bkmk_cmg) |
| Скачивание отчетов из Центра сообщества <!--3555936--> | [Technical Preview 1812](capabilities-in-technical-preview-1812.md#bkmk_hub) |
| Центр сообщества <!--3556020, fka 1357766--> | [Technical Preview 1807](capabilities-in-technical-preview-1807.md#bkmk_hub) |
| Служба ответчика PXE на основе клиента <!--3556018, fka 1357148--> | [Technical Preview 1712](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) |
| Поддержка сетевой загрузки PXE для IPv6 <!--3601254, fka 1269793--> |[Technical Preview 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
| Использование Azure Active Directory <!--3607315, fka 1322145--> | [Technical Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
| Усовершенствования для аналитики активов <!--3601024, fka 1307390--> | [Technical Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence) |

## <a name="see-also"></a>См. также

Дополнительные сведения см. в следующих статьях:

- [Оценка Configuration Manager в лабораторной среде](evaluate-with-lab-environment.md)
- [Новые возможности в добавочных версиях System Center Configuration Manager](../plan-design/changes/whats-new-incremental-versions.md)
- [Общие сведения о Configuration Manager](../understand/introduction.md)

> [!Tip]
> Дополнительные сведения о компонентах, на включение которых требуется согласие, см. в статье [Функции предварительной версии в System Center Configuration Manager](../servers/manage/pre-release-features.md).
>
> Дополнительные сведения о функциях, которые необходимо включить в первую очередь, см. в разделе [Включение дополнительных функций из обновлений](../servers/manage/install-in-console-updates.md#bkmk_options).
