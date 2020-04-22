---
title: Настройка Endpoint Protection
titleSuffix: Configuration Manager
description: Узнайте, как настроить Configuration Manager для обновления и распространения определений вредоносных программ для Защитника Windows.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e48f20dd56f445a10faa485b8bb7e86dbb05f75a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704522"
---
# <a name="configure-endpoint-protection"></a>Настройка Endpoint Protection

*Область применения: Configuration Manager (Current Branch)*

Прежде чем приступить к использованию Endpoint Protection для управления системой безопасности и защиты от вредоносных программ на клиентских компьютерах Configuration Manager, необходимо выполнить этапы настройки, описанные в этой статье.  

## <a name="how-to-configure-endpoint-protection-in-configuration-manager"></a>Настройка Endpoint Protection в Configuration Manager  
 Endpoint Protection в Configuration Manager имеет внешние зависимости и зависимости в пределах продукта.  

### <a name="steps-to-configure-endpoint-protection-in-configuration-manager"></a>Этапы настройки Endpoint Protection в Configuration Manager  
 Следующая таблица содержит этапы, подробности и дополнительные сведения о настройке Endpoint Protection.  

> [!IMPORTANT]  
>  Если управление Endpoint Protection осуществляется для компьютеров Windows 10, необходимо настроить Configuration Manager для обновления и распространения определений вредоносных программ для Защитника Windows. Защитник Windows входит в состав Windows 10, но по-прежнему требуется устанавливать SCEPInstall и задавать настраиваемые параметры клиентов для Endpoint Protection (**шаг 5**). </br> </br>
> Начиная с версии Configuration Manager 1802 на устройствах Windows 10 не требуется устанавливать агент Endpoint Protection (SCEPInstall). Если он уже установлен на устройствах Windows 10, Configuration Manager не удалит его. Администраторы могут удалять агент Endpoint Protection на устройствах Windows 10 с версией клиента не ранее 1802. SCEPInstall.exe может по-прежнему присутствовать в папке C:\Windows\ccmsetup на некоторых компьютерах, но не нужно загружать его для новых клиентов. Настраиваемые параметры клиентов для Endpoint Protection (**шаг 5**) по-прежнему необходимо указывать. <!--503654-->

|Шаги|Сведения|  
|-----------|-------------|  
|**Шаг 1.** [Создание роли системы сайта для точки Endpoint Protection](endpoint-protection-site-role.md)|Прежде чем использовать Endpoint Protection, устанавливается роль системы сайта точки Endpoint Protection. Ее следует устанавливать только на одном сервере системы сайта (на верхнем уровне иерархии сайта центра администрирования или автономного первичного сайта). |  
|**Шаг 2.** [Настройка оповещений для Endpoint Protection](endpoint-configure-alerts.md)|Оповещения информируют администратора при возникновении определенных событий, например при заражении компьютера вредоносными программами. Оповещения отображаются в узле **Оповещения** рабочей области **Мониторинг** или дополнительно могут быть отправлены указанным пользователям по электронной почте. |  
|**Шаг 3.** [Настройка источников обновления определений для клиентов Endpoint Protection](endpoint-definition-updates.md)|Endpoint Protection можно настроить для использования различных источников для скачивания обновлений определений. |  
|**Шаг 4.** [Настройка политики защиты от вредоносных программ по умолчанию и создание настраиваемых политик защиты от вредоносных программ](endpoint-antimalware-policies.md)|Политика защиты от вредоносных программ, используемая по умолчанию, применяется при установке клиента Endpoint Protection. Любые развернутые настраиваемые политики применяются по умолчанию в течение 60 минут процесса развертывания клиента. Перед тем как развернуть клиент Endpoint Protection, убедитесь, что политики защиты от вредоносных программ настроены. |  
|**Шаг 5**. [Задание значений настраиваемых параметров клиентов для Endpoint Protection](endpoint-protection-configure-client.md)|Используйте настраиваемые параметры клиентов, чтобы задать значения параметров Endpoint Protection для коллекций компьютеров в иерархии.<br /><br /> Примечание. Не следует изменять значения параметров клиентов Endpoint Protection, используемые по умолчанию, кроме случаев, когда вы уверенны, что их нужно применить на всех компьютерах в иерархии. |  
