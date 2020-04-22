---
title: Сценарии развертывания операционных систем предприятия
titleSuffix: Configuration Manager
description: Ознакомьтесь с несколькими сценариями развертывания операционных систем предприятия с помощью Configuration Manager.
ms.date: 02/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: f74fdb86-c7c2-447f-91f6-b42df6370d7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 07e8623928cbfe0bcd562d3d6efdf3a9ceee85ae
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708392"
---
# <a name="scenarios-to-deploy-enterprise-operating-systems-with-configuration-manager"></a>Сценарии развертывания операционных систем предприятия с помощью Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

В Configuration Manager доступны следующие сценарии развертывания операционной системы:  

#### <a name="upgrade-windows-to-the-latest-version"></a>Обновление Windows до последней версии
В этом сценарии обновляется операционная система на компьютерах, работающих под управлением Windows 7, Windows 8.1 или Windows 10. При обновлении приложения, параметры и данные пользователей сохраняются на компьютере. Процесс характеризуется отсутствием внешних зависимостей, таких как Windows ADK, а также более высокой скоростью и надежностью по сравнению с традиционным развертыванием ОС.  

Дополнительные сведения см. в статье [Обновление Windows до последней версии](upgrade-windows-to-the-latest-version.md).


#### <a name="windows-autopilot-for-existing-devices"></a>Windows Autopilot для имеющихся устройств
<!--3607717, fka 1358333-->
Начиная с версии 1810, Windows Autopilot для существующих устройств теперь предоставляется в Windows 10 версии 1809 или более поздней. Эта функция позволяет пересоздавать образ и подготавливать устройство Windows 7 к режиму Windows Autopilot с управлением пользователем с помощью одной последовательности задач Configuration Manager.

Дополнительные сведения см. в статье [Windows Autopilot for existing devices](windows-autopilot-for-existing-devices.md) (Windows Autopilot для существующих устройств).


#### <a name="refresh-an-existing-computer-with-a-new-version-of-windows"></a>Обновление существующего компьютера до новой версии Windows
В этом сценарии существующий компьютер секционируется и форматируется (очищается). Затем на нем устанавливается новая операционная система. После установки операционной системы можно перенести параметры и данные пользователя.  

Дополнительные сведения см. в статье об [обновлении существующего компьютера до новой версии Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md).


#### <a name="install-a-new-version-of-windows-on-a-new-computer-bare-metal"></a>Установка новой версии Windows на новом компьютере (без операционной системы)
В этом сценарии операционная система устанавливается на новом компьютере. Это новая установка, которая не включает в себя перенос каких-либо параметров или данных пользователя.  

Дополнительные сведения см. в статье об [установке новой версии Windows на новом компьютере (без операционной системы)](install-new-windows-version-new-computer-bare-metal.md).


#### <a name="replace-an-existing-computer-and-transfer-settings"></a>Замена существующего компьютера и перенос параметров
В этом сценарии операционная система устанавливается на новом компьютере. При необходимости можно перенести параметры и данные пользователя со старого компьютера на новый.  

Дополнительные сведения см. в статье [Замена существующего компьютера и перенос параметров](replace-an-existing-computer-and-transfer-settings.md).


