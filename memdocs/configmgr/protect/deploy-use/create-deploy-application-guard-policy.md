---
title: Управление политиками Application Guard
titleSuffix: Configuration Manager
description: Узнайте, как создавать и развертывать политики Application Guard в Защитнике Windows.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 33a6c1d9-4dd8-411c-a748-693a5bd2ea5a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 241e7ed9a2195e178cc1aac2ee2a146eea60b093
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705752"
---
# <a name="create-and-deploy-windows-defender-application-guard-policy"></a>Создание и развертывание политики Application Guard в Защитнике Windows

*Область применения: Configuration Manager (Current Branch)*
<!-- 1351960 -->  
Вы можете создать и развернуть [политики Application Guard в Защитнике Windows (Application Guard)](https://docs.microsoft.com/windows/threat-protection/windows-defender-application-guard/wd-app-guard-overview), используя защиту конечных точек Configuration Manager. Эти политики помогают защитить пользователей, открывая ненадежные веб-сайты в безопасном изолированном контейнере, который никак не взаимодействует с другими частями операционной системы.

## <a name="prerequisites"></a>Предварительные условия

Чтобы создать и развернуть политику Application Guard в Защитнике Windows, требуется использовать Windows 10 Fall Creators Update (1709). Для устройств Windows 10, на которых вы развертываете эту политику, нужно настроить политику сетевой изоляции. Дополнительные сведения см. в статье [Обзор Application Guard в Защитнике Windows](https://docs.microsoft.com/windows/threat-protection/windows-defender-application-guard/wd-app-guard-overview).

## <a name="create-a-policy-and-to-browse-the-available-settings"></a>Создание политики и просмотр доступных параметров

1. В консоли Configuration Manager щелкните элемент **Активы и соответствие**.
2. В рабочей области **Активы и соответствие** выберите пункты **Обзор** > **Endpoint Protection** > **Application Guard в Защитнике Windows**.
3. На вкладке **Главная** в группе **Создать** щелкните **Создать политику Application Guard в Защитнике Windows**.
4. Вы можете просмотреть и настроить доступные параметры, используя эту [статью](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/configure-wd-app-guard) в качестве инструкции. Configuration Manager позволяет задавать некоторые параметры политики:
   - [Параметры взаимодействия с узлом](#bkmk_HIS)
   - [Поведение приложения](#bkmk_ABS)
   - [Управление файлами](#bkmk_FM)
5. На странице **Определение сети** нужно указать удостоверение организации и задать границу корпоративной сети.

    > [!NOTE]
    > Компьютеры с ОС Windows 10 хранят только один список сетевой изоляции в клиенте. Вы можете создать два типа списков сетевой изоляции и развернуть их на клиенте:
    >
    >  - один из Windows Information Protection;
    >  - один из Application Guard в Защитнике Windows.
    >
    > При развертывании обеих политик эти списки сетевой изоляции должны совпадать. Если вы развернете несовпадающие списки на одном клиенте, произойдет сбой развертывания. Дополнительные сведения см. в [документации по Windows Information Protection](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/create-wip-policy-using-configmgr).

6. Когда вы закончите настройку, завершите работу мастера и разверните политику на одном или нескольких устройствах Windows 10 1709.

### <a name="host-interaction-settings"></a><a name="bkmk_HIS"></a> Параметры взаимодействия с узлом

Настройка взаимодействия между устройствами узлов и контейнером Application Guard. До выпуска Configuration Manager версии 1802 поведение приложения и взаимодействие с узлом определялись на вкладке **Параметры**.

- **Буфер обмена** — в разделе "Параметры" до Configuration Manager версии 1802
  - Допустимый тип содержимого
    - text
    - Образы
- **Печать:**
  - Разрешить печать в XPS
  - Разрешить печать в PDF
  - Разрешить печать на локальных принтерах
  - Разрешить печать на сетевых принтерах
- **Графика** (начиная с Configuration Manager версии 1802)
  - Доступ к виртуальному графическому процессору
- **Файлы** (начиная с Configuration Manager версии 1802)
  - Сохранение загруженных файлов на узле

### <a name="application-behavior-settings"></a><a name="bkmk_ABS"></a> Параметры поведения приложений

Настройка поведения приложений внутри сеанса Application Guard. До выпуска Configuration Manager версии 1802 поведение приложения и взаимодействие с узлом определялись на вкладке **Параметры**.

- **Содержимое**
  - Корпоративные сайты могут загружать содержимое, не связанное с организацией, например сторонние подключаемые модули.
- **Прочее:**
  - Сохранение созданных пользователем данных браузера.
  - Вести аудит событий безопасности в изолированном сеансе Application Guard

### <a name="file-management"></a><a name="bkmk_FM"></a> Управление файлами
<!--3555858-->
Начиная с версии Configuration Manager 1906 появился параметр политики, с помощью которого пользователи могут доверять файлам, которые обычно открываются в Application Guard. После успешного завершения файлы будут открываться на устройстве узла, а не в Application Guard. Дополнительные сведения о политиках Application Guard см. в статье [Configure Windows Defender Application Guard policy settings](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/configure-wd-app-guard) (Настройка параметров политик Application Guard в Защитнике Windows).

- **Разрешить пользователям доверять файлам, открытым в Application Guard в Защитнике Windows** — разрешите пользователю помечать файлы как доверенные. Если файл является доверенным, он открывается на узле, а не в Application Guard. Применимо к клиентам Windows 10 версии 1809 или более поздней.
  - **Запрещено**. Запретить пользователям помечать файлы как доверенные (по умолчанию).
  - **Файлы, проверенные антивирусом**. Разрешить пользователям помечать файлы как доверенные после антивирусной проверки.
  - **Все файлы**. Разрешить пользователям помечать любые файлы как доверенные.

При включении управления файлами в файле DCMReporting.log клиента могут иметься зарегистрированные ошибки. Приведенные ниже ошибки обычно не влияют на функциональность. <!--4619457-->

- На совместимых устройствах:
  - Условие FileTrustCriteria не найдено
- На несовместимых устройствах:
  - Условие FileTrustCriteria не найдено
  - FileTrustCriteria_condition не удалось найти в сопоставлении.
  - Условие FileTrustCriteria не найдено в дайджесте

Чтобы изменить параметры Application Guard, в рабочей области **Активы и соответствие** разверните узел **Endpoint Protection** и щелкните **Application Guard в Защитнике Windows**. Щелкните правой кнопкой мыши политику, которую требуется изменить, а затем выберите **Свойства**.

## <a name="next-steps"></a>Дальнейшие шаги

Дополнительные сведения об Application Guard в Защитнике Windows: [Windows Defender Application Guard Overview](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/wd-app-guard-overview) (Обзор Application Guard в Защитнике Windows).
[Часто задаваемые вопросы об Application Guard в Защитнике Windows](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/faq-wd-app-guard)
