---
title: Сетевая инфраструктура
titleSuffix: Configuration Manager
description: Настройка брандмауэров, портов и доменов для подготовки к взаимодействию с Configuration Manager.
ms.date: 06/19/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d6993bba-f6bd-4639-adbf-efc1c638b2f3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 816b48f7dac3703c1d45fdbc0bf8ad7dc9528caa
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703092"
---
# <a name="network-infrastructure-considerations-for-configuration-manager"></a>Рекомендации по сетевой инфраструктуре для Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Чтобы подготовить сеть к поддержке Configuration Manager, вам может потребоваться настроить некоторые компоненты инфраструктуры. Например, открыть порты брандмауэра для передачи данных, используемых Configuration Manager.  

## <a name="ports-and-protocols"></a>Порты и протоколы

Различные функции Configuration Manager используют разные сетевые порты. Некоторые порты обязательны, а некоторые вы можете настроить.

Большинство функций взаимодействия Configuration Manager использует общие порты, например порт 80 для HTTP и порт 443 для HTTPS. Некоторые роли системы сайта поддерживают использование настраиваемых веб-сайтов и портов. Дополнительные сведения см. в статье [Веб-сайты для серверов системы сайта в System Center Configuration Manager](websites-for-site-system-servers.md).

Перед развертыванием Configuration Manager определите порты, которые планируется использовать, и соответствующим образом настройте брандмауэры.

После установки Configuration Manager, если вам нужно изменить порт, не забудьте обновить брандмауэры на устройствах и в сети. Измените также конфигурацию порта в Configuration Manager.

Дополнительные сведения см. в следующих статьях:

- [Настройка портов связи для клиентов](../../clients/deploy/configure-client-communication-ports.md)
- [Порты, используемые в Configuration Manager](../hierarchy/ports.md)


## <a name="internet-access-requirements"></a>Требования для доступа к Интернету

Некоторые функции Configuration Manager зависят от подключения к Интернету. Если ваша организация ограничивает сетевое взаимодействие с Интернетом с помощью брандмауэра или прокси сервера, убедитесь, что требуемые конечные точки разрешены.

Дополнительные сведения о требованиях для доступа к Интернету см. в [этой статье](internet-endpoints.md).


## <a name="proxy-servers"></a>Прокси-серверы

Вы можете указать разные прокси-серверы для отдельных клиентов и серверов системы сайта. Эти настройки выполняются при установке роли системы сайта или клиента и при необходимости меняются позже.

Дополнительные сведения см. в статье [Поддержка прокси-сервера](proxy-server-support.md).
