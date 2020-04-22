---
title: Предоставление общего доступа к приложениям в центре программного обеспечения
titleSuffix: Configuration Manager
description: Предоставьте общий доступ к ссылке на приложение в центре программного обеспечения в Configuration Manager.
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2629c376-ec43-4f0e-a78b-4223cc9302bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: be2e930e3f59bc5a4d7db9e27ce2f875814fd358
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689242"
---
# <a name="share-an-application-from-software-center"></a>Предоставление общего доступа к приложению из центра программного обеспечения

*Область применения: Configuration Manager (Current Branch)* <!-- 1706 -->

Гиперссылку на приложение можно скопировать в центре программного обеспечения с помощью кнопки ![Поделиться](media/share15.png); кнопку **Поделиться** можно найти в представлении сведений о приложении. Вы можете предоставлять общий доступ только к гиперссылкам на приложения. Если приложение становится недоступным, гиперссылка открывает окно с сообщением о том, что приложение недоступно.

1. Выберите элемент **Приложения**, а затем выберите приложение.
2. Выберите ![Поделиться](media/share15.png), нажав кнопку **Поделиться**.
3. Нажмите в окне кнопку **Копировать**.
4. Вставьте URL-адрес в сообщение электронной почты, чтобы предоставить общий доступ к приложению.  

> [!TIP]  
>  Чтобы создать ссылку в сообщении электронной почты Outlook, нажмите клавиши **CTRL** + **K** и вставьте URL-адрес.  
>  
> По умолчанию в Outlook отображается оповещение системы безопасности для протокола центра программного обеспечения, когда получатель переходит по ссылке. Вы можете запретить это поведение в своей среде, добавив в реестр ключ доверенного протокола. Например, `HKCU\Software\Policies\Microsoft\Office\16.0\Common\Security\Trusted Protocols\All Applications\softwarecenter:`  
