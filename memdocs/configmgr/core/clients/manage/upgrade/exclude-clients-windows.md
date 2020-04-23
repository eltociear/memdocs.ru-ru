---
title: Исключение обновлений клиента для Windows
titleSuffix: Configuration Manager
description: Узнайте, как исключить клиенты Windows из обновления в Configuration Manager.
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4cd6031f-8844-4d0b-8166-b24d6528a94e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 58a7741bb628a0c8fb346c8f61b446301b138d80
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696852"
---
# <a name="how-to-exclude-clients-from-upgrade-in-configuration-manager"></a>Как исключить клиенты из обновления в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Вы можете исключить ряд клиентов из автоматической установки обновленных версий клиентов. Это можно использовать для коллекции компьютеров, которым требуется особое внимание при обновлении клиента. Клиент, который находится в исключенной коллекции, игнорирует запросы на установку обновленного клиентского программного обеспечения.

Это исключение применяется к следующим методам:

- автоматическое обновление;
- обновление путем установки обновления программного обеспечения;
- Сценарии входа
- Групповая политика

> [!NOTE]
> Хотя в пользовательском интерфейсе указывается, что клиенты не будут обновлены с помощью какого-либо метода, существует два способа, которые можно использовать для переопределения этих параметров. Для переопределения этой конфигурации используйте принудительную установку клиента и установку клиента вручную. Дополнительные сведения см. в разделе [Обновление исключенного клиента](#bkmk_override).

## <a name="configure-exclusion"></a><a name="bkmk_exclude"></a> Настройка исключения

1. В консоли Configuration Manager перейдите к рабочей области **Администрирование**. Разверните **Конфигурация сайта**, выберите узел **Сайты**, а затем щелкните **Параметры иерархии** на ленте.

2. Перейдите на вкладку **Обновление клиента**.

3. Выберите параметр **Исключить указанные клиенты из обновления**. Затем выберите **коллекцию исключений**, которую необходимо исключить. Можно выбрать только одну коллекцию для исключения.

4. Нажмите кнопку **ОК**, чтобы закрыть окно и сохранить конфигурацию.

![Параметры для исключения из автоматического обновления](media/automatic_upgrade_exclusion.png)

После того как клиенты будут добавлены в политику обновления с исключенной коллекцией, они не будут устанавливать обновления автоматически. Дополнительные сведения см. в разделе [Обновление клиентов для компьютеров Windows](upgrade-clients-for-windows-computers.md).

> [!NOTE]
> Исключенные клиенты по-прежнему будут скачивать и запускать Ccmsetup, но обновляться не будут.

После удаления клиента из коллекции исключений он не будет обновляться автоматически до следующего цикла автоматического обновления.

## <a name="how-to-upgrade-an-excluded-client"></a><a name="bkmk_override"></a> Обновление исключенного клиента

Если устройство является членом коллекции, исключенной из обновления, вы можете обновить клиент с помощью одного из следующих методов:

- **Принудительная установка клиента**. Ccmsetup позволяет принудительно установить клиент, так как это ваше прямое намерение. Этот метод позволяет обновить клиент, не удаляя его из коллекции или не удаляя всю коллекцию из исключения.

- **Установка клиента вручную**. Обновите исключенный клиент вручную, используя следующий параметр командной строки Ccmsetup: **/IgnoreSkipUpgrade**.

    Если вы пытаетесь вручную обновить клиент, который является членом исключенной коллекции, и не используете этот параметр, то клиент не будет обновлен. Дополнительные сведения см. в статье [Установка клиентов Configuration Manager вручную](../../deploy/deploy-clients-to-windows-computers.md#BKMK_Manual).

## <a name="see-also"></a>См. также

- [Обновление клиентов](upgrade-clients.md)

- [Развертывание клиентов на компьютерах Windows](../../deploy/deploy-clients-to-windows-computers.md)

- [Клиент для длительного взаимодействия](../../../understand/interoperability-client.md)