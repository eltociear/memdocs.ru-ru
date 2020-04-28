---
title: Дополнительные сведения о безопасности сценариев PowerShell
titleSuffix: Configuration Manager
description: Ресурсы и ссылки на дополнительные сведения о безопасности сценариев PowerShell
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: a0bd093d-67a5-4f74-bf79-dd604889f5ba
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6b519d60be094bb7c39f738d04322009b36a409f
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075869"
---
# <a name="learn-more-about-powershell-script-security"></a>Дополнительные сведения о безопасности сценариев PowerShell

*Область применения: Configuration Manager (Current Branch)*

В обязанности администратора входит проверка предложенных скриптов и параметров PowerShell для использования в своей среде. Ниже приведены некоторые полезные ресурсы, рассказывающие администраторам о возможностях PowerShell и потенциальных уязвимостях. Их рекомендуется изучить с целью сокращения потенциальных рисков и использования безопасных сценариев.

## <a name="powershell-script-security"></a>Безопасность сценариев PowerShell
Встраивание в сценарии запуска — это функция визуальной проверки и утверждения сценариев, выполнение которых запрашивается в среде. Администраторам следует иметь в виду, что сценарии PowerShell могут иметь структуру, затрудняющую понимание: некоторые вредоносные сценарии бывает сложно обнаружить путем визуальной проверки во время процесса утверждения. Поэтому мы рекомендуем использовать определенные средства проверки помимо визуального анализа сценариев PowerShell. Это поможет выявить подозрительные сценарии. Эти средства не всегда могут определить цели создателя скрипта PowerShell, однако они привлекут ваше внимание к подозрительным аспектам. Не смотря на это, именно администратор должен будет принять решение о том, является ли синтаксис сценария вредоносным и целенаправленным.

## <a name="recommendations"></a>Рекомендации
- Ознакомьтесь с рекомендациями по обеспечению безопасности PowerShell, ссылки на которые представлены ниже.
- **Подписывайте свои сценарии**. Хороший способ обеспечения безопасности сценариев — их тщательная проверка и подписание перед импортом для использования.
- Не храните секреты (например, пароли) в скриптах PowerShell и всегда следуйте рекомендациям по обращению с секретами.


## <a name="general-information-about-powershell-security-best-practices"></a>Общие сведения о рекомендациях по безопасности PowerShell

Эта коллекция ссылок подобрана для администраторов Configuration Manager в качестве отправной точки для изучения рекомендаций по обеспечению безопасности сценариев PowerShell.  

[Introduction to PowerShell Security Best Practices](https://blogs.msdn.microsoft.com/powershell/2013/12/16/powershell-security-best-practices/ ) (Введение в рекомендации по безопасности PowerShell)

[Рекомендации по безопасности PowerShell (презентация PowerPoint)](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/74/metablogapi/1055.PowerShell-Security-Best-Practices_3CA24C32.pptx)

<iframe src="https://channel9.msdn.com/Events/Blue-Hat-Security-Briefings/BlueHat-Security-Briefings-Fall-2013-Sessions/PowerShell-Best-Practices/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>

[Блог группы разработчиков PowerShell, посвященный защите от атак PowerShell](https://blogs.msdn.microsoft.com/powershell/2017/10/23/defending-against-powershell-attacks/)

[Лента в Twitter, посвященная защите от атак PowerShell, от эксперта Майкрософт по безопасности и PowerShell Ли Холмса (Lee Holmes)](https://twitter.com/Lee_Holmes/status/922462821081694208)

[Protecting Against Malicious Code Injection](https://blogs.msdn.microsoft.com/powershell/2006/11/22/protecting-against-malicious-code-injection/) (Защита от внедрения вредоносного кода)

["Синяя команда" PowerShell обсуждает подробную регистрацию блоков сценариев, защищенное ведение журнала событий, интерфейс поиска защиты от вредоносных программ и API создания безопасного кода](https://blogs.msdn.microsoft.com/powershell/2015/06/09/powershell-the-blue-team/) (на англ. языке)

[Для Windows 10 разработан API для интерфейса поиска защиты от вредоносных программ](https://cloudblogs.microsoft.com/microsoftsecure/2015/06/09/windows-10-to-offer-application-developers-new-malware-defenses/?source=mmpc)

## <a name="powershell-parameters-security"></a>Безопасность параметров PowerShell
Передача параметров обеспечивает дополнительную гибкость при работе со сценариями и возможность отложить решения до времени выполнения. При этом она также повышает уровень риска. Рекомендации по предотвращению внедрения вредоносных параметров или сценариев приведены ниже.

- Разрешайте использование только предварительно определенных параметров.
- Используйте функции регулярных выражений для проверки разрешенных параметров.
    - Пример: если допускается только определенный диапазон значений, используйте регулярное выражение для проверки применения только тех символов или значений, которые входят в диапазон.
    - Проверка параметров может помешать пользователям использовать определенные символы, которые можно экранировать, например кавычки. Имейте в виду, что типов кавычек может быть несколько, поэтому использовать регулярные выражения для проверки разрешенных символов бывает гораздо проще, чем определить все недопустимые входные данные.
- Используйте модуль PowerShell [InjectionHunter](https://www.powershellgallery.com/packages/InjectionHunter/1.0.0) из коллекции PowerShell.
    - Возможны ложные срабатывания, поэтому в случае обнаружения подозрительных элементов проверяйте их соответствие целям сценария, чтобы определить, представляют ли они фактическую опасность. 
- Microsoft Visual Studio включает анализатор сценариев, который может помочь при проверке синтаксиса PowerShell.
- В этом видео под названием "DEF CON 25 — Lee Holmes — Get $pwnd: Attacking Battle Hardened Windows Server" приводится обзор типов проблем, от которых можно защититься (обратите особое внимание на часть с 12:20 по 17:50):     <iframe width="560" height="315" src="https://www.youtube.com/embed/ahxMOAAani8" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

## <a name="environment-recommendations"></a>Рекомендации по среде
Общие рекомендации для администраторов PowerShell.
1. Развертывайте последнюю версию PowerShell, например версию 5 или более позднюю, встроенную в Windows 10. Кроме того, можно развернуть [Windows Management Framework](https://www.microsoft.com/download/details.aspx?id=54616). 
2. Включите и собирайте данные журналов PowerShell, в том числе защищенное ведение журнала событий (при необходимости). Включите эти журналы в рабочие процессы подписания, поиска и реагирования на нарушения безопасности.
3. Реализуйте технологию Just Enough Administration (JEA) для важнейших систем для устранения или сокращения неограниченного административного доступа к этим системам.
4. Выполните развертывание политик управления приложениями в Защитнике Windows, чтобы разрешить предварительно утвержденным административным задачам использовать все возможности языка PowerShell и ограничить возможности интерактивного и неутвержденного использования для заданного ряда сценариев PowerShell.
5. Выполните развертывание Windows 10, чтобы предоставить поставщику антивирусной защиты полный доступ ко всему содержимому (включая содержимое, создаваемое или раскрываемое во времени выполнения), обрабатываемому узлами сценариев Windows, включая PowerShell.
