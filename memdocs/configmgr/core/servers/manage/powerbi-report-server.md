---
title: Интеграция с Сервером отчетов Power BI
titleSuffix: Configuration Manager
description: Интегрируйте сервер отчетов Power BI с отчетами Configuration Manager для создания современных визуализаций и повышения производительности.
ms.date: 04/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 315e2613-dc71-46b1-80cb-26161d08103a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0c596ba410adc979b92a000c28d815e89695a9b0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694352"
---
# <a name="integrate-with-power-bi-report-server"></a>Интеграция с Сервером отчетов Power BI

*Область применения: Configuration Manager (Current Branch)*

<!--3721603-->

Начиная с версии 2002, можно интегрировать [Сервер отчетов Power BI](https://docs.microsoft.com/power-bi/report-server/get-started) с отчетами Configuration Manager. Эта интеграция обеспечивает современные возможности визуализации и улучшает производительность. Она добавляет поддержку консоли для отчетов Power BI, аналогично тому, что уже существует в SQL Server Reporting Services.

Сохраните файлы отчетов Power BI Desktop (PBIX) и разверните их на сервере отчетов Power BI. Этот процесс аналогичен работе с файлами отчетов SQL Server Reporting Services (RDL). Кроме того, отчеты можно запускать в браузере непосредственно из консоли Configuration Manager.

## <a name="prerequisites"></a>Предварительные условия

- Лицензия сервера отчетов Power BI. Дополнительные сведения см. в статье [Лицензирование сервера отчетов Power BI](https://docs.microsoft.com/power-bi/report-server/get-started#licensing-power-bi-report-server).

- Скачайте [сервер отчетов Microsoft Power BI за сентябрь 2019 г.](https://www.microsoft.com/download/details.aspx?id=57270) или более поздний выпуск.

    > [!NOTE]
    > Не устанавливайте сервер отчетов Power BI сразу. Сведения о правильном процессе в зависимости от среды см. в разделе [Настройка точки служб отчетов](#configure-the-reporting-services-point).

- Скачайте [Microsoft Power BI Desktop (оптимизировано для сервера отчетов Power BI за сентябрь 2019 г.)](https://www.microsoft.com/download/details.aspx?id=57271) или более поздний выпуск.

    > [!IMPORTANT]
    > - Используйте только версии Power BI Desktop из [Центра загрузки Майкрософт](https://www.microsoft.com/download/). Не используйте версию из Microsoft Store.
    > - Используйте только версию [Power BI Desktop с пометкой **Оптимизировано для сервера отчетов Power BI**](https://docs.microsoft.com/power-bi/report-server/install-powerbi-desktop).

- Интеграция Power BI использует одно и то же администрирование на основе ролей для создания отчетов.

## <a name="configure-the-reporting-services-point"></a>Настройка точки служб отчетов

Этот процесс зависит от того, есть ли у вас уже эта роль на сайте.

### <a name="you-have-a-reporting-services-point"></a>У вас есть точка служб отчетов

Используйте этот процесс только в том случае, если на сайте уже есть точка служб отчетов. Выполните все шаги этого процесса на том же сервере:

1. В **Configuration Manager сервера отчетов** сделайте резервную копию **ключей шифрования**. Дополнительные сведения см. в статье [Ключи шифрования служб SSRS — резервное копирование и восстановление ключей шифрования](https://docs.microsoft.com/sql/reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys).

    > [!WARNING]
    > Если пропустить этот шаг, доступ к пользовательским отчетам в SQL Server Reporting Services будет потерян.

1. Удалите роль точки служб отчетов с сайта.

1. Удалите службы отчетов SQL Server, но сохраните базу данных.

1. Установите сервер отчетов Power BI.

1. Настройка сервера отчетов Power BI

    1. Используйте базу данных предыдущего сервера отчетов.

    1. Используйте **Configuration Manager сервера отчетов**, чтобы восстановить **ключи шифрования**.

1. Добавьте роль точки служб отчетов в Configuration Manager.

### <a name="you-dont-have-a-reporting-services-point"></a>У вас нет точки служб отчетов

Используйте этот процесс только в том случае, если на сайте еще нет точки служб отчетов. Выполните все шаги этого процесса на том же сервере:

1. Установите сервер отчетов Power BI.

2. Добавьте роль точки служб отчетов в Configuration Manager. Дополнительные сведения см. в статье о [настройке отчетов](configuring-reporting.md).

## <a name="configure-the-configuration-manager-console"></a>Настройка консоли Configuration Manager

1. На компьютере, на котором выполняется консоль Configuration Manager, обновите ее до последней версии.

1. Установите Power BI Desktop. Убедитесь, что язык совпадает.

1. После установки запустите Power BI Desktop по крайней мере один раз, прежде чем открыть консоль Configuration Manager.

## <a name="create-power-bi-reports"></a>Создание отчетов Power BI

1. В консоли Configuration Manager перейдите к рабочей области **Наблюдение**, разверните пункт **Отчеты** и выберите узел **Отчеты Power BI**.

1. На ленте выберите **Создать отчет**. Это действие открывает Power BI Desktop.

1. Создайте отчет в Power BI Desktop.

    - В Power BI Desktop при подключении к источнику данных выберите **DirectQuery** для параметров подключения.

    - Используйте в этих отчетах только поддерживаемые представления SQL. Дополнительные сведения см. в разделе [Создание пользовательских отчетов с помощью представлений SQL Server в Configuration Manager](../../../develop/core/understand/sqlviews/create-custom-reports-using-sql-server-views.md).

1. Когда отчет будет готов к сохранению, перейдите в меню **Файл**, выберите пункт **Сохранить как**, а затем выберите пункт **Сервер отчетов Power BI**.

1. В окне **Выбор сервера отчетов Power BI** введите URL-адрес точки служб отчетов в качестве значения параметра **Новый адрес сервера отчетов**. Например, `https://rsp.contoso.com/Reports`.

В консоли Configuration Manager в списке отчетов Power BI появится новый отчет.

## <a name="next-steps"></a>Дальнейшие шаги

После создания отчета в консоли Configuration Manager можно выполнить следующие действия:

- **Запустить в браузере**. Открывает отчет Power BI в веб-браузере. Отправьте этот URL-адрес другим пользователям, например: `https://rsp.contoso.com/Reports/POWERBI/ConfigMgr_ABC/Windows%2010/Windows10%20Dashboard?rs:embed=true`

    > [!TIP]
    > Эти отчеты можно просматривать только в веб-браузере.

- **Изменить**. Внесите изменения в отчет в Power BI Desktop. Для существующего отчета используйте параметр **Сохранить**, чтобы сохранить изменения на сервере отчетов.

Дополнительные сведения о файлах журналов, используемых для создания отчетов, см. в разделе [Справочник по файлам журналов — отчеты](../../plan-design/hierarchy/log-files.md#BKMK_ReportLog).
