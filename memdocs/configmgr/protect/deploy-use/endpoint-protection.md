---
title: Endpoint Protection
titleSuffix: Configuration Manager
description: Узнайте, как управлять политиками защиты от вредоносных программ и параметрами безопасности брандмауэра Windows для клиентов.
ms.date: 03/18/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 76c90f64-d729-456b-8304-01852cd66fb6
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: b74a8c1daff31a8ffca8a38e6449aeeef1bb9b2d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697182"
---
# <a name="endpoint-protection"></a>Endpoint Protection

*Область применения: Configuration Manager (Current Branch)*

Endpoint Protection управляет политиками защиты от вредоносных программ и параметрами безопасности брандмауэра Windows для клиентских компьютеров в иерархии Configuration Manager.  

> [!IMPORTANT]  
>  Чтобы использовать Endpoint Protection для управления клиентами в иерархии Configuration Manager, необходима лицензия.  

 Совместное использование Endpoint Protection и Configuration Manager обеспечивает следующие преимущества:  

-   Настройка политик защиты от вредоносных программ, параметров брандмауэра Windows и управление службой "Расширенная защита от угроз" (ATP) в Microsoft Defender для выбранных групп компьютеров.  
-   Использование обновлений программного обеспечения Configuration Manager для загрузки актуальных файлов определений вредоносных программ на клиентские компьютеры.  
-   Отправка уведомлений по электронной почте, использование средств мониторинга в консоли и просмотр отчетов. Эти действия позволяют информировать пользователей с правами администратора об обнаружении вредоносных программ на клиентских компьютерах.  

На компьютерах под управлением ОС начиная с Windows 10 и Windows Server 2016 Защитник Windows уже установлен. В этих операционных системах клиент управления для Защитника Windows устанавливается при установке клиента Configuration Manager. На компьютерах под управлением Windows 8.1 и более ранних версий вместе с клиентом Configuration Manager также устанавливается клиент Endpoint Protection. Возможности клиентов Защитника Windows и Endpoint Protection:  

-   обнаружение и исправление вредоносных программ и шпионского программного обеспечения;  
-   обнаружение и исправление пакетов программ rootkit;  
-   оценка критических уязвимостей и автоматическое обновление определений и антивирусного модуля;  
-   обнаружение уязвимости сети с помощью системы проверки сети;  
-   интеграция со службой Cloud Protection Service для передачи сведений о вредоносных программах в Майкрософт. При подключении этой службы клиент Endpoint Protection или Защитник Windows, обнаружив на компьютере неопознанную вредоносную программу, скачивает новейшие определения из Центра по защите от вредоносных программ.  

> [!NOTE]  
>  Клиент Endpoint Protection можно установить на сервере под управлением Hyper-V и на гостевых виртуальных машинах с поддерживаемыми операционными системами. Во избежание чрезмерного использования ресурсов ЦП действия Endpoint Protection имеют встроенную случайную задержку, чтобы службы защиты не запускались одновременно.  

 Кроме того, Endpoint Protection используется для управления параметрами брандмауэра Windows в консоли Configuration Manager.  

 [Пример сценария. Использование System Center Endpoint Protection для защиты компьютеров от вредоносных программ](scenarios-endpoint-protection.md) Endpoint Protection и брандмауэр Windows.  


## <a name="managing-malware-with-endpoint-protection"></a>Защита от вредоносных программ с помощью Endpoint Protection  
 Endpoint Protection в Configuration Manager позволяет создавать политики защиты от вредоносных программ, содержащие параметры для конфигураций клиента Endpoint Protection. Созданные политики защиты от вредоносных программ можно развертывать на клиентских компьютерах. Их применение отслеживается в узле **Состояние Endpoint Protection** в разделе **Безопасность** рабочей области **Наблюдение**. Кроме того, в узле **Отчеты** можно использовать отчеты Endpoint Protection.  

 Дополнительные сведения:  

-   [Создание и развертывание политик защиты от вредоносных программ для Endpoint Protection](endpoint-antimalware-policies.md). Сведения о создании, развертывании и мониторинге политик защиты от вредоносных программ со списком параметров, которые можно настраивать  

-   [Мониторинг Endpoint Protection](monitor-endpoint-protection.md) — отчеты о действиях мониторинга, сведения о зараженных клиентских компьютерах и другие возможности.  

-   [Управление политиками защиты от вредоносных программ и параметрами брандмауэра для Endpoint Protection](endpoint-antimalware-firewall.md) — сведения об устранении вредоносных программ, найденных на клиентских компьютерах.  

-   [Файлы журналов для Endpoint Protection](../../core/plan-design/hierarchy/log-files.md#BKMK_EPLog)  


## <a name="managing-windows-firewall-with-endpoint-protection"></a>Управление брандмауэром Windows с помощью Endpoint Protection  
 Endpoint Protection в Configuration Manager позволяет управлять основными параметрами брандмауэра Windows на клиентских компьютерах. Для каждого сетевого профиля можно настроить следующие параметры:  

-   включение и отключение брандмауэра Windows;  

-   блокирование входящих подключений, включая указанные в списке разрешенных программ;  

-   уведомление пользователя о блокировании брандмауэром Windows новой программы.  

> [!NOTE]  
>  Endpoint Protection поддерживает управление только брандмауэром Windows.  


 Дополнительные сведения см. в статье [Создание и развертывание политик брандмауэра Windows для Endpoint Protection в System Center Configuration Manager](create-windows-firewall-policies.md).  


## <a name="microsoft-defender-advanced-threat-protection"></a>Advanced Threat Protection в Microsoft Defender

Endpoint Protection отслеживает службу "Расширенная защита от угроз (ATP) в Microsoft Defender" (прежнее название — ATP в Защитнике Windows) и управляет ею. С помощью службы Microsoft Defender ATP предприятия могут обнаруживать, исследовать атаки повышенной сложности и реагировать на них в своих сетях. Подробные сведения см. в статье [Microsoft Defender Advanced Threat Protection](windows-defender-advanced-threat-protection.md) (Расширенная защита от угроз в Microsoft Defender).

## <a name="endpoint-protection-workflow"></a>Рабочий процесс Endpoint Protection  
 Приведенная ниже схема поможет вам понять рабочий процесс для внедрения Endpoint Protection в вашей иерархии Configuration Manager.  

 ![Рабочий процесс Endpoint Protection](../media/Endpoint-Protection-Workflow.gif)  



## <a name="endpoint-protection-client-for-mac-computers-and-linux-servers"></a>Клиент Endpoint Protection для компьютеров Mac и серверов Linux  

> [!Important]  
> Поддержка System Center Endpoint Protection (SCEP) для Mac и Linux (все версии) заканчивается 31 декабря 2018 г. По окончании срока поддержки новые определения вирусов для SCEP для Mac и Linux могут быть недоступны. Дополнительные сведения см. в [записи блога об окончании срока поддержки](https://go.microsoft.com/fwlink/?linkid=870182).  

 System Center Endpoint Protection включает в себя клиент Endpoint Protection для компьютеров Linux и Mac. Эти клиенты не поставляются с Configuration Manager. Загрузите следующие продукты с сайта [Microsoft Volume Licensing Service Center](https://www.microsoft.com/licensing/servicecenter/default.aspx).  

-   System Center Endpoint Protection для Mac  

-   System Center Endpoint Protection для Linux  


> [!Note]  
>  Для загрузки файлов установки Endpoint Protection для Linux и Mac вы должны быть клиентом корпоративного лицензирования Майкрософт.  

 Этими продуктами невозможно управлять из консоли Configuration Manager. Пакет управления System Center Operations Manager поставляется с файлами установки, что позволяет управлять клиентом для Linux.  

### <a name="how-to-get-the-endpoint-protection-client-for-mac-computers-and-linux-servers"></a>Как получить клиент Endpoint Protection для компьютеров Mac и серверов Linux

Используйте следующие действия, чтобы скачать файл образа, содержащий клиентское программное обеспечение Endpoint Protection и документацию для компьютеров Mac и серверов Linux.
1. Войдите на веб-сайт [Microsoft Volume Licensing Service Center](https://www.microsoft.com/licensing/servicecenter/default.aspx).
2. В верхней части веб-сайта перейдите на вкладку **Downloads and Keys** (Загрузки и ключи).
3. Используйте фильтр по продукту **System Center Endpoint Protection (текущая ветвь)** .
4. Щелкните ссылку **Download** (Скачать).
5. Нажмите кнопку **Continue**(Продолжить). Вы увидите несколько файлов, включая один с именем: **System Center Endpoint Protection (current branch — version 1606) for Linux OS and Macintosh OS Multilanguage 32/64 bit 1878 MB ISO**.
6. Щелкните значок стрелки, чтобы скачать файл. Имя файла — **SW_DVD5_Sys_Ctr_Endpnt_Prtctn_1606_MultiLang_-3_EptProt_Lin_Mac_MLF_X21-67050.ISO**.

Это обновление за январь 2018 года (X21-67050) включает следующие версии:

- System Center Endpoint Protection для Mac 4.5.32.0 (поддержка для macOS 10.13 High Sierra);
- System Center Endpoint Protection для Linux 4.5.20.0. 

  Дополнительные сведения о том, как устанавливать клиенты Endpoint Protection для Linux и компьютеров Mac и управлять ими, см. в документации, поставляемой с этими продуктами. Она находится в папке **Documentation** в ISO-файле.
