---
title: Удаление CAS
titleSuffix: Configuration Manager
description: Удаление CAS сводит инфраструктуру Configuration Manager к одному автономному первичному сайту.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 16975644-8dfa-4f22-b45a-c54a9250dbd2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6704075d707306f55a50a937185c9bdd28b18cc5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700622"
---
# <a name="remove-the-central-administration-site"></a>Удаление сайта центра администрирования

*Область применения: Configuration Manager (Current Branch)*

<!-- 3607277 -->

Начиная с версии 2002, если иерархия состоит из сайта центра администрирования (CAS) и одного дочернего первичного сайта, можно удалить CAS. Это действие сводит инфраструктуру Configuration Manager к одному автономному первичному сайту. Это позволяет устранить сложность репликации типа "сеть — сеть" и разместить задачи управления на одном сайте.

> [!IMPORTANT]
> В этой версии Configuration Manager эта функция предварительной версии не включена по умолчанию. В настоящее время она доступна для клиентов Microsoft Premier.
>
> Чтобы включить эту функцию, обратитесь к менеджеру по технической поддержке:
>
> - Ваш технический консультант откроет консультационное обращение, в котором будут использоваться часы Microsoft Premier.
> - Невозможно изменить уровень серьезности обращения.
> - Служба поддержки Майкрософт работает над такими обращениями в рабочее время в будни.

## <a name="plan"></a>План

- Иерархия должна состоять из сайта CAS и одного дочернего первичного сайта. Первичный сайт может иметь вторичные сайты. Чтобы удалить другие дочерние первичные сайты из иерархии, ознакомьтесь с этапами планирования и предварительными требованиями для [удаления первичного сайта](uninstall-sites-and-hierarchies.md#bkmk_primary).

- Убедитесь, что дочерний первичный сайт соответствует требованиям к размеру и масштабированию для [автономного первичного сайта](../../../plan-design/configs/size-and-scale-numbers.md#bkmk_pri).

- Переместить или вывести из эксплуатации любые роли сайта на CAS, кроме точки подключения службы и точки обновления программного обеспечения. Программа установки Configuration Manager обрабатывает эти две роли при удалении CAS.

  Следующие роли наиболее распространены на сайтах центра администрирования, и их необходимо вывести из использования или перенести на первичный сайт:

  - Точка синхронизации аналитики активов
  - Точка Endpoint Protection
  - Точка служб отчетов
  - Точка обслуживания хранилища данных
  - шлюз управления облачными клиентами (CMG);

    > [!NOTE]
    > Если вы включили CMG для содержимого, запланируйте повторное распространение содержимого после повторного создания CMG на первичном сайте.<!-- 6608659 -->

- Отключение распределенных представлений

- Configuration Manager автоматически обрабатывает расположения источников для встроенных пакетов, таких как клиент Configuration Manager. Проверьте все остальные расположения источников содержимого, чтобы убедиться, что они не используют общую папку на CAS.

- Завершите все активные задания миграции и удалите все конфигурации миграции. Дополнительные сведения см. в разделе [Остановка активной миграции из другой иерархии](prerequisites-for-installing-sites.md#stop-active-migration-from-another-hierarchy).

- Если вы используете правила автоматического развертывания для обновлений программного обеспечения, воссоздайте их на дочернем первичном сайте.

- Если вы используете Configuration Manager или System Center Updates Publisher для управления [сторонними обновлениями программного обеспечения](../../../../sum/deploy-use/third-party-software-updates.md), экспортируйте сертификат для подписи WSUS из точки обновления программного обеспечения на CAS.

  - Перед удалением CAS дождитесь, когда истекут сроки всех необходимых развертываний сторонних обновлений программного обеспечения. Клиенты предварительно скачивают содержимое для обязательных развертываний, и при изменении точки обновления хэш содержимого изменяется вместе с *локальной публикацией* обновлений программного обеспечения. (Это поведение не влияет на другие типы содержимого, затрагивая только локальную публикацию сторонних обновлений программного обеспечения.) Если удалить CAS, когда эти обязательные развертывания не закончены, на клиентах произойдут ошибки из-за несовпадения хэшей.

- Проверьте все стороннее программное обеспечение, которое может иметь зависимости от CAS.

## <a name="prerequisites"></a>Предварительные условия

- Убедитесь, что пользователь-администратор, запускающий программу установки Configuration Manager, имеет следующие права безопасности:

  - права локального **администратора** на сервере CAS;

  - если сервер базы данных CAS находится на удалении от сервера сайта — права локального **администратора** на удаленном сервере базы данных сайта для CAS;

  - права **системного администратора** базы данных сайта CAS;

  - права **локального администратора** на сервере первичного сайта;

  - если сервер базы данных первичного сайта находится на удалении от сервера первичного сайта — права локального **администратора** на удаленном сервере базы данных сайта для первичного сайта;

  - права **системного администратора** базы данных первичного сайта;

  - роль **администратора инфраструктуры** или **полного администратора** на CAS и первичном сайте;

- только один дочерний первичный сайт в иерархии. Дополнительные сведения см. в разделе [Удаление первичного сайта](uninstall-sites-and-hierarchies.md#bkmk_primary).

## <a name="process"></a>Процесс

1. Запустите программу установки Configuration Manager на сервере CAS одним из следующих способов.

    - В меню **Пуск** выберите пункт **Установка Configuration Manager**.

    - В каталоге *установочного носителя* Configuration Manager откройте `\SMSSETUP\BIN\X64\setup.exe`. Убедитесь, что эта версия совпадает с версией сайта.

    - В каталоге, где *установлен* Configuration Manager, откройте `\BIN\X64\setup.exe`.

1. Прочтите информацию на странице **Перед началом работы**.

1. На странице **Приступая к работе** выберите **Выполнить обслуживание или сброс параметров этого сайта**.

1. На странице **Обслуживание сайта** выберите **Удаление сайта центра администрирования**. <!-- or is it still "delete"? -->

1. На странице **Повторная настройка существующих ролей системы сайта**:

    - **Точка подключения службы**. Введите полное доменное имя системы сайта на первичном сайте для размещения этой требуемой роли. Дополнительные сведения см. в статье [Точки подключения службы](../configure/about-the-service-connection-point.md).

    - **Точка обновления программного обеспечения**. Выберите существующую точку обновления программного обеспечения на первичном сайте. Программа установки настраивает эту точку обновления программного обеспечения на синхронизацию с конфигурацией CAS.

    Программа установки проверяет, соответствуют ли указанные серверы предварительным требованиям. Выберите **Начать установку**, когда будете готовы продолжить.

Если программа установки обнаружит проблему, используйте мастер, чтобы повторить процесс.

После завершения установки он сбрасывает первичный сайт. См. сведения о [сбросе сайта](../../manage/modify-your-infrastructure.md#bkmk_reset).

## <a name="monitor-and-verify"></a>Мониторинг и проверка

Во время установки проверьте следующие журналы:

- `C:\ConfigMgrSetup.log` на сервере CAS;

- **hman.log** в каталоге журналов Configuration Manager на сервере первичного сайта.

Используйте узел **Иерархия сайтов** в рабочей области **Мониторинг**, чтобы визуализировать изменения в иерархии. Например, на следующем рисунке показано сравнение CAS **SHY**, первичного сайта **HAW** и вторичного сайта **VWT**.

| До  | После   |
|---------|---------|
|![Пример представления иерархии сайтов для CAS, первичного сайта и вторичного сайта](media/3607277-cas-primary-secondary.png)|![Пример представления иерархии сайтов для первичного сайта и вторичного сайта](media/3607277-primary-secondary.png)|

## <a name="post-setup-tasks"></a>Задачи, выполняемые после установки

После удаления CAS ознакомьтесь с приведенными ниже шагами в меру их применимости к вашей среде.

- Вручную удалите учетную запись компьютера сервера CAS из локальных групп первичного сайта.

- Доверенный корневой ключ будет изменен, что может потребовать дополнительных действий.

  - Обновите загрузочные образы развертывания ОС, чтобы включить последние двоичные файлы Configuration Manager.

  - Заново создайте [Носитель развертывания ОС](../../../../osd/deploy-use/create-task-sequence-media.md).

- При подключении Configuration Manager к [Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm?context=configmgr/core/context/core-context) необходимо сбросить подключение. Первый шаг к устранению проблем заключается в том, чтобы [обновить секретный ключ](../configure/azure-services-wizard.md#bkmk_renew). Если это не устранит проблему, создайте подключение заново.<!-- 5584635 -->

- В версии 2002 при включении синхронизации драйверов Surface перенастройте эту функцию после удаления CAS. Дополнительные сведения см. в разделе [Включить обновление драйверов и встроенного ПО Microsoft Surface](../../../../sum/get-started/configure-classifications-and-products.md#bkmk_Surface).<!-- 5728727 -->

- При наличии обновления программного обеспечения сторонних поставщиков сделайте следующее.

  1. Экспортируйте сертификат для подписи WSUS из точки обновления программного обеспечения на CAS, если вы этого еще не сделали.

  1. Перед созданием новых развертываний удалите обновление из всех существующих развертываний и пакетов обновлений программного обеспечения.

  1. Чтобы восстановить метаданные обновления программного обеспечения в пригодном для использования состоянии, повторно синхронизируйте подписанные каталоги. Можно также подождать, пока Configuration Manager автоматически повторно синхронизируется.

  1. Произведите запуск или дождитесь начала процесса синхронизации обновлений программного обеспечения для обновления Configuration Manager с добавлением текущего состояния служб WSUS. При необходимости используйте командлеты PowerShell SCUP или WSUS для удаления и чтения обновлений.

  1. Повторно опубликуйте содержимое тех обновлений, которые необходимо развернуть.