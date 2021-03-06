---
title: Возможности технической версии 1704
titleSuffix: Configuration Manager
description: Сведения о функциях, доступных в Technical Preview для Configuration Manager, версия 1704.
ms.date: 04/21/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e318e705-20f2-417d-8cde-7dfe661b2fa7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: c24b9a6e4f6f123e0456b9f1337a7c3b19ab6962
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705272"
---
# <a name="capabilities-in-technical-preview-1704-for-configuration-manager"></a>Возможности в Technical Preview 1704 для Configuration Manager

*Область применения: Configuration Manager (ветвь Technical Preview)*

В этой статье содержатся сведения о функциях, доступных в версии 1704 Technical Preview для Configuration Manager. Этот выпуск можно установить для обновления и добавления новых возможностей в ознакомительную техническую версию сайта Configuration Manager. Перед установкой этой версии прочтите вводную статью [Technical Preview для Configuration Manager](../../core/get-started/technical-preview.md), чтобы ознакомиться с общими требованиями и ограничениями на использование ознакомительной технической версии, а также узнать, как выполнять обновления и оставлять отзывы о возможностях этого выпуска.    


**Ниже перечислены новые возможности, доступные в этой версии.**  

## <a name="configure-android-apps-with-app-configuration-policies"></a>Настройка приложений Android с помощью политик конфигурации приложений
Вы можете использовать политики конфигурации приложений в Configuration Manager для распространения параметров, которые могут быть необходимы, когда пользователь работает с приложением на устройствах под управлением Android for Work. Политики конфигурации Android приложения доступны только на устройствах под управлением Android for Work. Они применимы к утвержденным приложениям из хранилища Play for Work.

### <a name="try-it-out"></a>Попробуйте!                 

В консоли Configuration Manager последовательно выберите **Библиотека программного обеспечения** > **Управление приложениями** > **Политики конфигурации приложений** и **Создать политику конфигурации приложений**. На странице **Общие** мастера теперь можно **выбрать тип политики конфигурации**. Укажите платформу для политики конфигурации приложения: **Политика конфигурации для приложений Android for Work**. После этого можно **указать пары "имя — значение"** или **перейти к файлу JSON списка свойств**. Новая политика конфигурации приложений отображается в узле **Политики конфигурации приложений** рабочей области **Библиотека программного обеспечения**. Чтобы связать политику конфигурации приложений с развертыванием приложения Android for Work, разверните приложение обычным образом, как описано в разделе [Развертывание приложений](../../apps/deploy-use/deploy-applications.md).

## <a name="hardware-inventory-collects-secure-boot-information"></a>Функция инвентаризации оборудования собирает сведения о безопасной загрузке
Функция инвентаризации оборудования теперь собирает сведения о включении безопасной загрузки на клиентах. Эти сведения хранятся в классе **SMS_Firmware** (представлено в версии 1702 и включено в функции инвентаризации оборудования по умолчанию). См. дополнительные сведения о [настройке инвентаризации оборудования](../clients/manage/inventory/configure-hardware-inventory.md).

## <a name="add-child-task-sequences-to-a-task-sequence"></a>Добавление дочерней последовательности задач в последовательность задач
В этой версии вы можете добавить новый шаг последовательности задач, который управляет другой последовательностью задач, что, в свою очередь, создает иерархическое отношение между последовательностями задач. Это позволяет создать дополнительные модульные последовательности задач, которые можно повторно использовать.  

При добавлении в последовательность задач дочерней последовательности задач учитывайте следующее:

- Родительская и дочерняя последовательности задач эффективно объединяются в одну политику, выполняемой на клиенте.
- Вы не можете добавить дочернюю последовательность задач, которая является родительской для другой последовательности задач.
- Среда является глобальной. Например, если переменная определена родительской последовательностью задач, а затем изменена дочерней, переменная останется измененной. Аналогичным образом, если дочерняя последовательность задач создает переменную, такая переменная будет доступной для соответствующих действий в родительской последовательности задач.
- Сообщения о состоянии отправляются для отдельной операции последовательности задач как обычно.
- Последовательности задач регистрируют записи в файл журнала smsts.log так, чтобы было понятно, когда начинается дочерняя последовательность задач.
- Если в Technical Preview для Configuration Manager, версия 1704, последовательности дочерних задач ссылаются на любой пакет, а вы запускаете родительскую последовательность задач из центра программного обеспечения, клиент не сможет найти содержимое пакета при запуске дочерней последовательности задач. В этом сценарии необходимо запустить последовательность задач с носителя (загрузочного носителя, PXE и пр.).  

    Если дочерняя последовательность задач использует такие действия, как **Выполнить из командной строки** (без ссылки на пакет), **Форматировать**, **BitLocker** и пр., она будет успешно запущена из центра программного обеспечения.

### <a name="to-add-a-child-task-sequence-to-a-task-sequence"></a>Добавление дочерней последовательности задач в последовательность задач
1. В редакторе последовательности задач щелкните **Добавить**, **Общие** и **Запустить последовательность задач**.
2. Щелкните **Обзор**, чтобы выбрать дочернюю последовательность задач.  

## <a name="reload-boot-images-with-current-windows-pe-version"></a>Перезагрузка загрузочных образов с использованием текущей версии Windows РЕ
Запуская **обновление точек распространения** на выбранном загрузочном образе, вы теперь можете повторно загрузить в загрузочный образ последнюю версию Windows PE (из каталога установки Windows ADK). На странице **Общие** мастера предоставлены сведения о версии Windows ADK, установленной на сервере сайта, и версии Windows ADK, из которой в загрузочном образе использовался экземпляр Windows PE, а также о версии клиента Configuration Manager. Эти сведения помогут вам решить, следует ли повторно использовать загрузочный образ. Кроме того, добавлен новый столбец (**Версия клиента**), доступный при просмотре загрузочных образов на узле **Загрузочные образы** и отображающий версию клиента Configuration Manager, используемую для каждого загрузочного образа.

### <a name="to-reload-a-boot-image-with-the-current-windows-pe-version"></a>Перезагрузка загрузочного образа с использованием текущей версии Windows PE

1. В консоли Configuration Manager последовательно выберите **Библиотека программного обеспечения** > **Операционные системы** > **Загрузочные образы**.
2. Выберите образ загрузки и щелкните **Обновить точки распространения**.
3. На странице **Общие** мастера выберите **перезагрузку загрузочного образа с использованием текущей версии среды Windows PE из установленной версии Windows ADK**.

## <a name="improvements-to-operating-system-deployment"></a>Усовершенствования развертывания операционной системы
Мы оптимизировали процедуру развертывания операционной системы во многом на основе ваших отзывов.

- [Новый столбец **Версия ОС** для образов операционных систем](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/17558407-add-a-column-to-the-operating-system-images-node-f): мы добавили новый столбец **Версия ОС**, в котором отображается версия операционной системы для образа при просмотре сведений в узлах **Образы операционной системы** и **Пакеты обновления операционной системы**. Отображается только версия первого индекса в WIM-файле. На вкладке **Сведения** для образа можно просмотреть версии операционной системы для других индексов.

- [Более эффективное ведение журналов в Smsts.log](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/16791919-stop-filling-smsts-log-with-useless): начиная с этой версии мы больше не записываем сведения CCM_CIVersionInfo.PolicyID в файл журнала smsts.log. Раньше эти сведения содержались во многих записях, что затрудняло поиск более важной информации в файле журнала.
