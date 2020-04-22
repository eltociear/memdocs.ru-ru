---
title: Поддержка Windows 10
titleSuffix: Configuration Manager
description: Сведения о том, какие версии Windows 10 можно развернуть с помощью Configuration Manager и использовать в качестве клиентов
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a1626a65-da22-49e0-9564-d2f752ea3f4b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7241db0220bf4adf9b55341514afb03de33c2589
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688602"
---
# <a name="support-for-windows-10-in-configuration-manager"></a>Поддержка Windows 10 в Configuration Manager  

*Область применения: Configuration Manager (Current Branch)*

Дополнительные сведения о версиях Windows 10, которые поддерживает Configuration Manager, включая:

- [Windows 10 как клиент Configuration Manager](#windows-10-as-a-client)
- [Комплект средств для развертывания и оценки Windows (ADK) для Windows 10](#windows-10-adk)

> [!Tip]
> Сборки Windows Server в качестве клиента поддерживаются так же, как соответствующая версия Windows 10. Например, у Windows Server 2016 та же версия сборки, что и у Windows 10 2016 с долгосрочным обслуживанием, а версия Windows Server 1803 совпадает с версией сборки Windows 10 версии 1803.
>
> Дополнительные сведения о Windows Server как системе сайта см. в статье [Поддерживаемые операционные системы для серверов системы сайта Configuration Manager](supported-operating-systems-for-site-system-servers.md#bkmk_core).

## <a name="windows-10-as-a-client"></a>Windows 10 в качестве клиента

Мы стараемся реализовывать в Configuration Manager клиентскую поддержку каждой новой версии Windows 10 как можно скорее после ее выпуска. Так как графики разработки и выпуска этих продуктов не совпадают, обеспечиваемая в Configuration Manager поддержка зависит от времени выпуска версий и ветвей каждого продукта.

Та или иная версия Configuration Manager будет удалена из схемы, когда завершится период [поддержки соответствующей версии](../../servers/manage/current-branch-versions-supported.md). Точно так же поддержка версий Windows 10, например Корпоративная 2015 с долгосрочным обслуживанием или 1511, будет удалена из схемы, когда эти версии перестанут поддерживаться.

- Последняя версия Configuration Manager Current Branch получает обновления для системы безопасности и критические обновления, в которые могут входить исправления проблем, касающиеся версий Windows 10. Когда корпорация Майкрософт выпустит новую версию Configuration Manager Current Branch, более ранние версии будут получать только обновления для системы безопасности. Дополнительные сведения см. в статье [Поддержка версий Current Branch Configuration Manager](../../servers/manage/current-branch-versions-supported.md).  

    > [!Note]  
    > Лучшим способом поддержки актуальности Windows 10 является использование Configuration Manager. Дополнительные сведения см. в статье [Configuration Manager и Windows как услуга](../../understand/configuration-manager-and-windows-as-service.md).  

- Приведенные здесь сведения дополняют то, что изложено в статье [Поддерживаемые операционные системы для клиентов и устройств](supported-operating-systems-for-clients-and-devices.md).  

- Если вы используете ветвь Long-Term Servicing Branch системы Configuration Manager, см. раздел [Поддерживаемые конфигурации для Long-Term Servicing Branch](../../understand/supported-configurations-for-ltsb.md).  

В таблице ниже перечислены версии Windows 10, которые можно использовать в качестве клиента, и соответствующие им версии Configuration Manager.

| Версия Windows 10 | Configuration Manager 1810 | Configuration Manager 1902 | Configuration Manager 1906 | Configuration Manager 1910 | Configuration Manager 2002 |
|---------------------|-----|-----|-----|-----|-----|
| **Корпоративная 2015 с долгосрочным обслуживанием** <!--10/14/2025-->   | ![Поддерживается](media/green_check.png) | ![Поддерживается](media/green_check.png) | ![Поддерживается](media/green_check.png) | ![Поддерживается](media/green_check.png) | ![Поддерживается](media/green_check.png) |
| **Корпоративная 2016 с долгосрочным обслуживанием** <!--10/13/2026-->   | ![Поддерживается](media/green_check.png) | ![Поддерживается](media/green_check.png) | ![Поддерживается](media/green_check.png) | ![Поддерживается](media/green_check.png) | ![Поддерживается](media/green_check.png) |
| **Корпоративная LTSC 2019** <!--01/09/2029-->   | ![Поддерживается](media/green_check.png) | ![Поддерживается](media/green_check.png) | ![Поддерживается](media/green_check.png) | ![Поддерживается](media/green_check.png) | ![Поддерживается](media/green_check.png) |
| **1709**<br>(10.0.16299)   <!--04/14/2020-->   | ![Поддерживается](media/green_check.png) | ![Поддерживается](media/green_check.png) | ![Поддерживается](media/green_check.png) | ![Поддерживается](media/green_check.png) | ![Поддерживается](media/green_check.png) |
| **1803**<br>(10.0.17134)   <!--11/10/2020-->   | ![Поддерживается](media/green_check.png) | ![Поддерживается](media/green_check.png) | ![Поддерживается](media/green_check.png) | ![Поддерживается](media/green_check.png) | ![Поддерживается](media/green_check.png) |
| **1809**<br>(10.0.17763)   <!--05/11/2021-->   | ![Поддерживается](media/green_check.png) | ![Поддерживается](media/green_check.png) | ![Поддерживается](media/green_check.png) | ![Поддерживается](media/green_check.png) | ![Поддерживается](media/green_check.png) |
| **1903**<br>(10.0.18362)   <!--12/08/2020-->   | ![Не поддерживается](media/Red_X.png) | ![Поддерживается](media/green_check.png) | ![Поддерживается](media/green_check.png) | ![Поддерживается](media/green_check.png) | ![Поддерживается](media/green_check.png) |
| **1909**<br>(10.0.18363)   <!--05/11/2021-->   | ![Не поддерживается](media/Red_X.png) | ![Не поддерживается](media/Red_X.png) | ![Поддерживается](media/green_check.png) | ![Поддерживается](media/green_check.png) | ![Поддерживается](media/green_check.png) |

<!-- lifecycle reference: https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet -->

Дополнительные сведения о жизненном цикле Windows см. в [справочнике по жизненному циклу Windows](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet).

| Key |
|--|
| ![Поддерживается](media/green_check.png) = **Поддерживается**  |
| ![Не поддерживается](media/Red_X.png) = **Не поддерживается** |

### <a name="windows-10-client-support-notes"></a><a name="bkmk_win10-notes"></a> Примечания о поддержке клиента Windows 10

- Поддержка версий Windows 10, выходящих в рамках Semi-Annual Channel, распространяется на следующие выпуски: Корпоративная, Pro, для образовательных учреждений и Pro для образовательных учреждений.  

- Начиная с версии 1906, Configuration Manager поддерживает Windows 10 Pro для рабочей станции.

- Для Windows 10 версии 1909 носитель развертывания ОС показывает версию 10.0.18362.418.

### <a name="windows-10-on-arm64"></a><a name="bkmk_arm64"></a> Windows 10 в ARM64

Configuration Manager поддерживает клиенты на устройствах ARM64 с Windows 10. Развертывание ОС не поддерживается.<!-- 1353704 -->

Начиная с версии 2002,<!--5954175--> платформа **Все устройства Windows 10 (ARM64)** доступна в списке поддерживаемых версий ОС для объектов с правилами требований или списками применимости.

> [!NOTE]
> Если ранее вы выбрали платформу верхнего уровня **Windows 10**, это действие автоматически выбирает **Все устройства Windows 10 (64-разрядная)** и **Все устройства Windows 10 (32-разрядная)** . Эта новая платформа не выбирается автоматически. Если вы хотите добавить **Все устройства Windows 10 (ARM64)** , вручную выберите ее в списке.

### <a name="support-for-windows-insider"></a><a name="bkmk_WIfB-support"></a> Поддержка программы предварительной оценки Windows

Начиная с Configuration Manager версии 1906, можно [обновлять и обслуживать сборки программы предварительной оценки Windows](../../../sum/get-started/configure-classifications-and-products.md#bkmk_WIfB). Эта возможность предоставляется для удобства наших клиентов. Хотя эта функция должна работать, ее поддержка является наилучшим решением. Configuration Manager может не выдать исправление для этой функции, если она прекращает работать.  

Отправить отзыв о программе предварительной оценки Windows можно в [концентраторе обратной связи](https://docs.microsoft.com/windows-insider/at-work-pro/wip-4-biz-feedback).

## <a name="windows-10-adk"></a>Windows 10 ADK

Если вы развертываете операционную систему с помощью Configuration Manager, Windows ADK является обязательной внешней зависимостью. Дополнительные сведения см. в следующих статьях:

- [Требования к инфраструктуре для развертывания ОС](../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md#windows-adk-for-windows-10)

- [Скачивание Windows ADK для Windows 10](https://docs.microsoft.com/windows-hardware/get-started/adk-install)

    > [!IMPORTANT]
    > Начиная с Windows 10 версии 1809 для установки среды Windows PE используется отдельный установщик. Другие функции не отличаются.
    >
    > Обязательно загрузите **Windows ADK для Windows 10** и **надстройку Windows PE для ADK**.

В таблице ниже перечислены версии Windows 10 ADK и соответствующие им версии Configuration Manager.

| Версия Windows 10 ADK  | Configuration Manager 1810 | Configuration Manager 1902 | Configuration Manager 1906 | Configuration Manager 1910 | Configuration Manager 2002 |
|--------------------|-----|-----|-----|-----|-----|
| **1709**<br>(10.1.16299) | ![Не поддерживается](media/Red_X.png)   | ![Не поддерживается](media/Red_X.png) | ![Не поддерживается](media/Red_X.png) | ![Не поддерживается](media/Red_X.png) | ![Не поддерживается](media/Red_X.png) |
| **1803**<br>(10.1.17134) | ![Обратная совместимость](media/blue_compat.png) | ![Обратная совместимость](media/blue_compat.png) | ![Не поддерживается](media/Red_X.png) | ![Не поддерживается](media/Red_X.png) | ![Не поддерживается](media/Red_X.png) |
| **1809**<br>(10.1.17763) | ![Поддерживается](media/green_check.png) | ![Поддерживается](media/green_check.png) | ![Обратная совместимость](media/blue_compat.png) | ![Обратная совместимость](media/blue_compat.png) | ![Не поддерживается](media/Red_X.png) |
| **1903**<br>(10.1.18362) | ![Не поддерживается](media/Red_X.png) | ![Поддерживается](media/green_check.png) | ![Поддерживается](media/green_check.png) | ![Поддерживается](media/green_check.png) | ![Поддерживается](media/green_check.png) |

|Key|
|--|
| ![Поддерживается](media/green_check.png) = **Поддерживается** <br/> В этой таблице показана только поддержка Windows ADK относительно версии Configuration Manager. Корпорация Майкрософт рекомендует использовать ту версию Windows ADK, которая соответствует развертываемой версии Windows. Используйте последнюю версию Windows ADK при развертывании последней версии Windows 10. Последняя версия Windows ADK может поддерживать развертывание более ранних версий ОС, таких как Windows 8.1.<!-- SCCMDocs issue 1229 --> Дополнительные сведения о поддержке компонента Windows ADK см. в разделе [Поддерживаемые DISM платформы](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-supported-platforms) и [Требования USMT](https://docs.microsoft.com/windows/deployment/usmt/usmt-requirements#bkmk-1). |
| ![Обратная совместимость](media/blue_compat.png)  = **Обратная совместимость** <br/> Это сочетание не протестировано, но должно работать. Мы будем документировать известные проблемы и предупреждения. |
| ![Не поддерживается](media/Red_X.png) = **Не поддерживается** |

### <a name="windows-10-adk-support-notes"></a><a name="bkmk_adk-notes"></a> Примечания о поддержке Windows 10 ADK

- Configuration Manager поддерживает только компоненты x86 и amd64 Windows 10 ADK. Сейчас он не поддерживает компоненты ARM и ARM64.

- В сборках Windows Server предъявляются те же требования к ADK, что и в соответствующей версии Windows 10. Например, в Windows Server 2016 используется та же версия сборки, что и в Windows 10 LTSB 2016.
