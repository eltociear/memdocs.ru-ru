---
title: Развертывание обновлений программного обеспечения
titleSuffix: Configuration Manager
description: Узнайте, как в консоли Configuration Manager вручную запустить процесс развертывания или развернуть обновления автоматически.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 11/27/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 04536d51-3bf7-45e5-b4af-36ceed10583d
ms.openlocfilehash: 8104bbab04e2c8741bfbbc9c6fb61039033941c9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696142"
---
# <a name="deploy-software-updates"></a>Развертывание обновлений программного обеспечения  

*Область применения: Configuration Manager (Current Branch)*

Этап развертывания обновления программного обеспечения — это процесс развертывания обновлений. Независимо от того, как вы развертываете обновления программного обеспечения, сайт выполняет следующие действия:
- добавляет обновления в группу обновлений программного обеспечения;
- распространяет содержимое обновления в точки распространения;
- развертывает группу обновлений на клиентах.  

После создания развертывания сайт отправляет соответствующую политику обновления программного обеспечения на целевые клиенты. Клиенты загружают файлы содержимого обновления программного обеспечения из источника содержимого в свой локальный кэш. Клиенты в Интернете всегда скачивают содержимое из облачной службы Центра обновления Майкрософт. Затем обновления программного обеспечения становятся доступными для установки.   

> [!Tip]  
>  Клиент в интрасети может загружать обновления программного обеспечения из Центра обновления Майкрософт, даже если точка распространения недоступна.  

> [!NOTE]  
>  В отличие от других типов развертывания все обновления программного обеспечения скачиваются в кэш клиента. На это никак не влияет максимальный размер кэша на клиентском компьютере. Дополнительные сведения о параметрах кэша клиента см. в разделе [Настройка кэша клиента для клиентов Configuration Manager](../../core/clients/manage/manage-clients.md#BKMK_ClientCache).  

В случае настройки обязательного развертывания обновлений ПО эти обновления автоматически устанавливаются при наступлении запланированного крайнего срока. Пользователь клиентского компьютера также может запланировать или инициировать установку обновлений ПО перед наступлением крайнего срока. Когда попытка установки ПО завершается, клиенты отправляют на сервер сайта сообщения об успешной или неудавшейся установке обновления ПО, которое может быть успешно завершено или прерваться в результате сбоя. Дополнительные сведения о развертываниях обновлений программного обеспечения см. в разделе [Рабочие процессы развертывания обновлений программного обеспечения](../understand/software-updates-introduction.md#BKMK_DeploymentWorkflows).  

Существует три основных сценария развертывания обновлений программного обеспечения: 
- [Ручное развертывание](#BKMK_ManualDeployment)  
- [Автоматическое развертывание](#bkmk_auto)  
- [Поэтапное развертывание](#bkmk_phased)  

Как правило, обновления программного обеспечения сначала развертываются вручную с целью создания базы для клиентов, а затем с помощью автоматического или поэтапного развертывания осуществляется управление установкой обновлений на клиенты.  

> [!Note]  
> Невозможно использовать правила автоматического развертывания при поэтапном развертывании.



## <a name="manually-deploy-software-updates"></a><a name="BKMK_ManualDeployment"></a> Развертывание обновлений программного обеспечения вручную
Выберите обновления программного обеспечения в консоли Configuration Manager и вручную запустите процесс развертывания. Этот способ развертывания обычно используется для выполнения следующих задач:  

- обновление клиентов с помощью обновлений программного обеспечения перед созданием правил автоматического развертывания для управления ежемесячными развертываниями;  

- развертывание внештатных обновлений программного обеспечения.  


В следующем списке приводится описание общего процесса ручного развертывания обновлений программного обеспечения.  

1. Фильтр для обновлений программного обеспечения, использующих определенные требования. Например, создайте условие, обеспечивающее получение всех обновлений безопасности или других важных обновлений, необходимых для более чем 50 клиентов.  

2. Создайте группу обновления программного обеспечения, которая содержит обновления программного обеспечения.  

3. Загрузите содержимое обновлений программного обеспечения в группе обновлений программного обеспечения.  

4. Вручную разверните группу обновления программного обеспечения.  

Дополнительные сведения и подробные инструкции см. в статье [Развертывание обновлений программного обеспечения вручную](manually-deploy-software-updates.md).

> [!Tip]  
> При развертывании обновлений для клиента Office 365 вручную найдите их в узле **Обновления Office 365** в разделе **Управление клиентом Office 365** рабочей области **Библиотека программного обеспечения**.  



## <a name="automatically-deploy-software-updates"></a><a name="bkmk_auto"></a> Автоматическое развертывание обновлений программного обеспечения

Автоматическое развертывание обновлений настраивается с помощью правила автоматического развертывания (ADR). Это общепринятый способ развертывания ежемесячных обновлений ПО (известный как "Вторник установки исправлений") и управления обновлениями определений. Чтобы автоматизировать процесс развертывания, необходимо задать условия для правил автоматического развертывания. В списке ниже приводится описание общего процесса автоматического развертывания обновлений ПО.  

1.  Создается правило автоматического развертывания, определяющее параметры развертывания.  

2.  Сайт добавляет обновления программного обеспечения в группу обновлений программного обеспечения.  

3.  Сайт развертывает группу обновлений программного обеспечения на клиентах в целевой коллекции.  

Сначала определите стратегию автоматического развертывания обновлений программного обеспечения. Например, создайте правило автоматического развертывания и укажите в качестве изначальной цели коллекцию тестовых клиентов. После успешной установки обновлений программного обеспечения в тестовой группе добавьте в правило новое развертывание. Можно также изменить целевую коллекцию в существующем развертывании, указав ту, которая содержит больший набор клиентов. Принимая решение относительно используемой стратегии, учтите следующие моменты.  

- Вы можете изменять свойства объектов обновления программного обеспечения, создаваемых правилами автоматического развертывания.   

- Правила автоматического развертывания автоматически развертывают обновления программного обеспечения на клиентах при их добавлении в целевую коллекцию.  

- Когда вы или правило автоматического развертывания добавляете обновления программного обеспечения в группу обновлений, сайт автоматически развертывает их на клиентах в целевой коллекции.  

- Развертывания для правила автоматического развертывания можно включать и отключать в любое время.  


После создания правила автоматического развертывания к нему можно добавить дополнительные развертывания. Это позволяет управлять сложным процессом развертывания различных обновлений для разных коллекций. Каждое новое развертывание имеет полный набор функций и средств мониторинга развертывания.  

Каждое новое добавляемое развертывание:  

- использует те же группу и пакет обновлений, создаваемый ADR при первом запуске;  
- может быть предназначено для другой коллекции;  
- поддерживает уникальные свойства развертывания, в том числе:  
  -   время активации;  
  -   Крайний срок  
  -   Взаимодействие с пользователем  
  -   отдельные предупреждения для этого развертывания.  


Дополнительные сведения и подробные инструкции см. в статье [Автоматическое развертывание обновлений программного обеспечения](automatically-deploy-software-updates.md).



## <a name="deploy-software-updates-in-phases"></a><a name="bkmk_phased"></a> Поэтапное развертывание обновлений программного обеспечения

<!--1358146-->
Начиная с версии 1810 можно создавать поэтапные развертывания для обновлений программного обеспечения. Поэтапные развертывания позволяют организовать согласованное, последовательное развертывание программного обеспечения на основе настраиваемых условий и групп.

Подробные сведения см. в статье [Создание поэтапных развертываний с помощью Configuration Manager](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md?toc=/sccm/sum/toc.json&bc=/sccm/sum/breadcrumb/toc.json).
