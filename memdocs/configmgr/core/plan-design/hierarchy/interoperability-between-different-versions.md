---
title: Взаимодействие между версиями
titleSuffix: Configuration Manager
description: Узнайте, как избежать конфликтов между несколькими иерархиями в одной сети Configuration Manager.
ms.date: 05/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9b0a7859-747f-4495-a2f4-13fd5991f897
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d8d5eeeeafa775514bb46fa0906f22572343611d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693522"
---
# <a name="interoperability-between-different-versions-of-configuration-manager"></a>Взаимодействие различных версий Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Возможна установка и эксплуатация сразу нескольких независимых иерархий Configuration Manager в одной сети. Но, так как разные иерархии Configuration Manager не взаимодействуют вне процесса миграции, для каждой иерархии необходимо создать конфигурации, предотвращающие конфликты между ними. Кроме того, можно создать разные конфигурации, чтобы облегчить взаимодействие управляемых вами ресурсов с системами сайтов из правильной иерархии.  

## <a name="interoperability-between-current-branch-and-earlier-versions"></a><a name="BKMK_SupConfigInterop"></a> Взаимодействие между текущей ветвью и более ранними версиями  

В одной и той же иерархии Configuration Manager не могут сосуществовать сайты разных версий. Допускаются исключения только при обработке следующих сценариев обновления:

- Обновление System Center 2012 Configuration Manager до Configuration Manager (Current Branch)
- Обновление Configuration Manager до текущей ветви с использованием обновлений в консоли

Сайт Configuration Manager (Current Branch) можно развернуть параллельно с существующей иерархией или сайтом System Center 2012 Configuration Manager. Необходимо предотвратить попытки клиентов любой из версий присоединиться к сайту другой версии.

Например, если две или более иерархии Configuration Manager имеют [перекрывающиеся границы](../../servers/deploy/configure/boundary-groups.md#overlapping-boundaries), которые включают одни и те же сетевые расположения, лучше назначить каждый новый клиент конкретному сайту, а не использовать автоматическое назначение сайта. Дополнительные сведения см. в статье [Назначение клиентов сайту в System Center Configuration Manager](../../clients/deploy/assign-clients-to-a-site.md).  

Кроме того, нельзя установить клиент из System Center 2012 Configuration Manager на компьютере, где размещена роль системы сайта из Configuration Manager (Current Branch). Также нельзя установить клиент Configuration Manager (Current Branch) на компьютере, где размещена роль системы сайта из System Center 2012 Configuration Manager.  

Не поддерживаются следующие клиенты и подключения:  

- Все версии компьютерных клиентов не старше System Center 2012 Configuration Manager.  

- Все версии System Center 2012 Configuration Manager или более ранняя версия клиента управления устройством.  

- Клиент управления устройством Windows CE Platform Builder (любая версия).  

- VPN-подключение диспетчера мобильных устройств System Center.  

### <a name="client-site-assignment-considerations"></a><a name="BKMK_SupConfigSiteAssignment"></a> Рекомендации по назначению сайта клиента  

Клиенты Configuration Manager могут назначаться только одному первичному сайту. Фактическое назначение сайта клиента невозможно спрогнозировать, если выполняются все следующие условия:

- Для назначения клиентов сайтам при установке клиента используется автоматическое назначение сайта.
- Несколько групп содержат одну и ту же границу.
- Группам границ назначены разные сайты.

Если границы перекрываются в нескольких сайтах и иерархиях Configuration Manager, клиенты могут быть неправильно назначены сайту или вообще не получить назначение.  

Клиенты Configuration Manager (Current Branch) проверяют версию сайта, прежде чем завершить его назначение. Если границы сайтов перекрываются, нельзя назначить клиенты сайту с предыдущей версией. Но клиенты более ранней версии System Center 2012 Configuration Manager могут быть неправильно назначены сайту Configuration Manager (Current Branch) более поздней версии.  

Чтобы предотвратить случайное назначение клиентов сайту при наличии перекрывающихся границ двух иерархий, параметры установки клиента следует настроить для назначения клиентам конкретного сайта.  

## <a name="configuration-manager-limitations-in-a-mixed-version-hierarchy"></a><a name="bkmk_mixed"></a> Ограничения возможностей Configuration Manager в иерархии со смешанными версиями  

При обновлении иерархии Configuration Manager (Current Branch) разные сайты могут находиться в различных версиях. Например, вы сначала обновили сайт центра администрирования. Но из-за периодов обслуживания сайта вы не обновляли первичные сайты до определенных даты и времени.  

Когда разные сайты в одной иерархии имеют разные версии, некоторые функции становятся недоступными. Это может влиять на управление объектами Configuration Manager в консоли Configuration Manager и на доступные клиентам функциональные возможности. Обычно функциональные возможности более новой версии Configuration Manager недоступны на сайтах или в клиентах с более ранними версиями пакетов обновления.  

### <a name="network-access-account"></a>Учетная запись доступа к сети

Обновите сайт центра администрирования до Configuration Manager (Current Branch). Просмотрите сведения об учетной записи для доступа к сети в консоли Configuration Manager, подключенной к этому обновленному сайту. Сведения об учетной записи не отображаются на сайтах под управлением System Center 2012 Configuration Manager.

После обновления первичного сайта до той же версии, что и у сайта центра администрирования, учетные данные будут отображаться в консоли.

То же происходит и при обновлении версии Configuration Manager.

### <a name="boot-images-for-os-deployment"></a>Образы загрузки для развертывания операционной системы

#### <a name="when-upgrading-from-system-center-2012-configuration-manager-to-configuration-manager-current-branch"></a>При обновлении System Center 2012 Configuration Manager до Configuration Manager (Current Branch)

Когда сайт верхнего уровня в иерархии обновляется до Configuration Manager (Current Branch), образы загрузки по умолчанию автоматически обновляются для использования комплекта средств для развертывания и оценки Windows (Windows ADK) версии 10. Используйте эти образы загрузки только для развертываний в клиентах на сайтах Configuration Manager (Current Branch). Дополнительные сведения см. в статье [Планирование взаимодействия для развертывания операционных систем в System Center Configuration Manager](../../../osd/plan-design/planning-for-operating-system-deployment-interoperability.md).

#### <a name="when-upgrading-between-configuration-manager-current-branch-versions"></a>При обновлении между версиями Configuration Manager (Current Branch)

До появления новых версий Configuration Manager не обновляйте используемую версию Windows ADK: это не повлияет на образы загрузки.

### <a name="new-task-sequence-steps"></a>Новые шаги последовательности задач

При создании последовательности задач, содержащей шаг, представленный в одной версии Configuration Manager, но недоступный в более ранней версии, могут возникнуть перечисленные ниже проблемы.

- При попытке изменить последовательность задач с сайта под управлением предыдущей версии Configuration Manager происходит ошибка.

- Последовательность задач не будет выполняться на компьютере, на котором запущена предыдущая версия клиента Configuration Manager.

### <a name="client-to-down-level-management-point-communications"></a>Обмен данными между клиентом и точкой управления нижнего уровня

Клиент Configuration Manager, который обменивается данными с точкой управления на сайте с версией пакета обновления ниже, чем версия пакета обновления на клиенте, может использовать только функциональные возможности, поддерживаемые этой более низкой версией Configuration Manager. Например, при развертывании содержимого с недавно обновленного сайта Configuration Manager (Current Branch) на клиенте, который обменивается данными с точкой управления, которая еще не была обновлена до этой версии, этот клиент не может использовать новые функциональные возможности последней версии.

### <a name="package-and-task-sequence-deployments-to-legacy-clients"></a>Развертывание пакетов и последовательности задач в клиентах устаревших версий

<!-- SCCMDocs-pr issue #3493 -->

Начиная с версии 1902 больше нельзя развернуть пакет или последовательность задач в версии клиента 5.7730 или более ранней версии. Чтобы обойти это ограничение, обновите клиент до более поздней версии.

## <a name="software-updates"></a>Обновления программного обеспечения

### <a name="orchestration-groups"></a>Группы оркестрации

Группы оркестрации, представленные в версии 2002, нельзя использовать в иерархии со смешанными версиями. <!--SCCMDocs-pr issue ##5056, 6389000-->

## <a name="interoperability-for-the-configuration-manager-console"></a><a name="BKMK_ConsoleInterop"></a> Взаимодействие с консолью Configuration Manager  

В этом разделе приводятся сведения об использовании консоли Configuration Manager в среде с различными версиями Configuration Manager.  

### <a name="an-environment-with-both-system-center-2012-configuration-manager-and-configuration-manager-current-branch"></a>Среда, в которой используются обе версии: System Center 2012 Configuration Manager и Configuration Manager (Current Branch)

Для управления сайтом Configuration Manager как консоль, так и сайт, к которому подключается консоль, должны использовать одну и ту же версию Configuration Manager. Например, с помощью консоли System Center 2012 Configuration Manager нельзя управлять сайтом Configuration Manager (Current Branch), и наоборот.

Установка консоли System Center 2012 Configuration Manager и консоли Configuration Manager (Current Branch) на одном компьютере не поддерживается.

### <a name="an-environment-with-multiple-versions-of-configuration-manager"></a>Среда, в которой используются несколько версий Configuration Manager

Configuration Manager (Current Branch) не поддерживает установку нескольких консолей Configuration Manager на одном компьютере. Чтобы использовать несколько консолей для разных версий Configuration Manager, разные консоли необходимо установить на отдельных компьютерах.

В процессе обновления сайтов в иерархии до новой версии можно подключить консоль к сайту, на котором запущена более новая версия, и ознакомиться с информацией о других сайтах в конкретной иерархии. Тем не менее эта конфигурация не рекомендуется. Вполне возможно, что различия между версией консоли и версией сайта Configuration Manager могут привести к проблемам с данными. Некоторые функции, доступные в последней версии продукта, не будут доступны в консоли.

Управление сайтом с консоли, версия которой не совпадает с версией сайта, не поддерживается. Если так делать, можно потерять данные и поставить сайт под угрозу. Например, использовать консоль версии 1610 для управления сайтом версии 1606 не следует. Такая схема использования не поддерживается.
