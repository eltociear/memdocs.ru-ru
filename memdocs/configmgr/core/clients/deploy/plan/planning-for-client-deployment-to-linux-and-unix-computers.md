---
title: Планирование развертывания клиентов на компьютерах Linux и UNIX
titleSuffix: Configuration Manager
description: Планируйте развертывание клиентов на компьютерах Linux и UNIX в Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 44153689-70e8-42ad-9ae8-17ae35f6a2e3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: dfede7594224ff48af2a1e4066e69d551c3c576e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693732"
---
# <a name="planning-for-client-deployment-to-linux-and-unix-computers-in-configuration-manager"></a>Планирование развертывания клиентов на компьютерах Linux и UNIX в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

> [!Important]  
> Начиная с версии 1902, Configuration Manager не поддерживает клиенты Linux и UNIX. 
> 
> Вы можете управлять серверами Linux с помощью портала управления Microsoft Azure. Решения Azure располагают расширенной поддержкой Linux, которая в большинстве случаев превышает функциональные возможности Configuration Manager, включая полное управление исправлениями для Linux.

Вы можете установить клиент Configuration Manager на компьютерах с Linux или UNIX. Этот клиент разработан для серверов, работающих как компьютер рабочей группы, при этом клиент не поддерживает взаимодействие с вошедшими в систему пользователями. После установки клиентского программного обеспечения и подключения клиента к сайту Configuration Manager вы управляете клиентом с помощью консоли Configuration Manager и отчетов.  

> [!NOTE]
>  Клиент Configuration Manager для Linux и UNIX не поддерживает следующие функции управления:  
> 
> - Принудительная установка клиента  
>   -   Развертывание операционной системы  
>   -   Развертывание приложений; вместо этого развертывайте ПО с помощью пакетов и программ.  
>   -   Инвентаризация программного обеспечения  
>   -   Обновления программного обеспечения  
>   -   Параметры соответствия  
>   -   Удаленное управление  
>   -   Исключение брандмауэра Windows для прокси-сервера пробуждения  
>   -   Проверка и исправление состояния клиента  
>   -   Управление клиентами через Интернет  

 Дополнительные сведения о поддерживаемых дистрибутивах Linux и UNIX и оборудовании, требуемом для поддержки клиента для Linux и UNIX, см. в статье [Рекомендуемое оборудование для Configuration Manager](../../../../core/plan-design/configs/recommended-hardware.md).  

 Используйте сведения этой статьи при планировании развертывания клиента Configuration Manager для Linux и UNIX.  

##  <a name="prerequisites-for-client-deployment-to-linux-and-unix-servers"></a><a name="BKMK_ClientDeployPrereqforLnU"></a> Необходимые условия для развертывания клиента на серверах UNIX и Linux  
 Используйте следующие сведения для определения необходимых компонентов, вы должны быть выполнены для успешно установить клиент для Linux и UNIX.  

###  <a name="dependencies-external-to-configuration-manager"></a><a name="BKMK_ClientDeployExternalforLnU"></a> Внешние зависимости Configuration Manager  
 В следующих таблицах описываются требуемые версии операционных систем UNIX и Linux и зависимости пакетов.  

 **Red Hat Enterprise Linux Server, выпуск 5.1 (Tikanga)**  

|Требуемый пакет|Описание:|Минимальная версия|  
|----------------------|-----------------|---------------------|  
|glibc|Стандартные библиотеки C|2.5-12|  
|Openssl|Библиотеки OpenSSL; протокол защищенной связи|0.9.8b-8.3.el5|  
|PAM|Подключаемые модули проверки подлинности|0.99.6.2-3.14.el5|  

 **Red Hat Enterprise Linux Server, выпуск 6**  

|Требуемый пакет|Описание:|Минимальная версия|  
|----------------------|-----------------|---------------------|  
|glibc|Стандартные библиотеки C|2.12-1.7|  
|Openssl|Библиотеки OpenSSL; протокол защищенной связи|1.0.0-4|  
|PAM|Подключаемые модули проверки подлинности|1.1.1-4|  

 **Red Hat Enterprise Linux Server, выпуск 7**  

|Требуемый пакет|Описание:|Минимальная версия|  
|----------------------|-----------------|---------------------|  
|glibc|Стандартные библиотеки C|2.17|  
|Openssl|Библиотеки OpenSSL; протокол защищенной связи|1.0.1|  
|PAM|Подключаемые модули проверки подлинности|1.1.1-4|  

 **Solaris 10 для SPARC**  

|Требуемый пакет|Описание:|Минимальная версия|  
|----------------------|-----------------|---------------------|  
|Обновление операционной системы|Утечка памяти в PAM|117463-05|  
|SUNWlibC|Sun Workshop Compilers Bundled libC (sparc)|5.10, REV=2004.12.22|  
|SUNWlibms|Math & Microtasking Libraries (Usr) (sparc)|5.10, REV=2004.11.23|  
|SUNWlibmsr|Math & Microtasking Libraries (Root) (sparc)|5.10, REV=2004.11.23|  
|SUNWcslr|Основные библиотеки Solaris (Root) (sparc)|11.10.0, REV=2005.01.21.15.53|  
|SUNWcsl|Основные библиотеки Solaris (Root) (sparc)|11.10.0, REV=2005.01.21.15.53|  
|Openssl|SUNopenssl-librararies (Usr)<br /><br /> Компания Sun предоставляет библиотеки OpenSSL для Solaris 10 SPARC. Они поставляются в пакете с операционной системой.|11.10.0, REV=2005.01.21.15.53|  
|PAM|Подключаемые модули проверки подлинности<br /><br /> SUNWcsr, Core Solaris, (Root) (sparc)|11.10.0, REV=2005.01.21.15.53|  

 **Solaris 10 для x86**  

|Требуемый пакет|Описание:|Минимальная версия|  
|----------------------|-----------------|---------------------|  
|Обновление операционной системы|Утечка памяти в PAM|117464-04|  
|SUNWlibC|Упакованные компиляторов Sun семинар libC (i386)|5.10, REV=2004.12.20|  
|SUNWlibmsr|Math & Microtasking Libraries (Root) (i386)|5.10, REV=2004.12.18|  
|SUNWcsl|Основы Solaris (общей библиотеки) (i386)|11.10.0, REV=2005.01.21.16.34|  
|SUNWcslr|Основные библиотеки Solaris (Root) (i386)|11.10.0, REV=2005.01.21.16.34|  
|Openssl|Библиотеки sunwopenssl; Библиотеки OpenSSL (Usr) (i386)|11.10.0, REV=2005.01.21.16.34|  
|PAM|Подключаемые модули проверки подлинности<br /><br /> SUNWcsr ядра Solaris, (Root)(i386)|11.10.0, REV=2005.01.21.16.34|  

 **Solaris 11 для SPARC**  

|Требуемый пакет|Описание:|Минимальная версия|  
|----------------------|-----------------|---------------------|  
|SUNWlibC|Sun Workshop Compilers Bundled libC|5.11, REV=2011.04.11|  
|SUNWlibmsr|Math & Microtasking Libraries (Root)|5.11, REV=2011.04.11|  
|SUNWcslr|Core Solaris Libraries (Root)|11.11, REV=2009.11.11|  
|SUNWcsl|Core Solaris, (Shared Libs)|11.11, REV=2009.11.11|  
|SUNWcsr|Core Solaris, (Root)|11.11, REV=2009.11.11|  
|Библиотеки SUNWopenssl|Библиотеки OpenSSL (Usr)|11.11.0, REV=2010.05.25.01.00|  

 **Solaris 11 для x86**  

|Требуемый пакет|Описание:|Минимальная версия|  
|----------------|-----------|---------------|  
|SUNWlibC|Sun Workshop Compilers Bundled libC|5.11, REV=2011.04.11|  
|SUNWlibmsr|Math & Microtasking Libraries (Root)|5.11, REV=2011.04.11|  
|SUNWcslr|Core Solaris Libraries (Root)|11.11, REV=2009.11.11|  
|SUNWcsl|Core Solaris, (Shared Libs)|11.11, REV=2009.11.11|  
|SUNWcsr|Core Solaris, (Root)|11.11, REV=2009.11.11|  
|Библиотеки SUNWopenssl|Библиотеки OpenSSL (Usr)|11.11.0, REV=2010.05.25.01.00|  


 **SUSE Linux Enterprise Server 10 SP1 (i586)**  

|Требуемый пакет|Описание:|Минимальная версия|  
|----------------------|-----------------|---------------------|  
|glibc-2,4-31,30|Стандартная общая библиотека C|2.4-31.30|  
|Openssl|Библиотеки OpenSSL; протокол защищенной связи|0.9.8a-18.15|  
|PAM|Подключаемые модули проверки подлинности|0.99.6.3-28.8|  

 **SUSE Linux Enterprise Server 11 (i586)**  

|Требуемый пакет|Описание:|Минимальная версия|  
|----------------------|-----------------|---------------------|  
|glibc-2.9-13.2|Стандартная общая библиотека C|2.9-13.2|  
|PAM|Подключаемые модули проверки подлинности|pam-1.0.2-20.1|  

 **Универсальная операционная система Linux Debian (пакет Debian), сервер Ubuntu**  

|Требуемый пакет|Описание:|Минимальная версия|  
|----------------------|-----------------|---------------------|  
|libc6|Стандартная общая библиотека C|2.3.6|  
|Openssl|Библиотеки OpenSSL; протокол защищенной связи|0.9.8 или 1.0|  
|PAM|Подключаемые модули проверки подлинности|0.79-3|  

 **Универсальная операционная система Linux CentOS (пакет RPM), Oracle Linux**  

|Требуемый пакет|Описание:|Минимальная версия|  
|----------------------|-----------------|---------------------|  
|glibc|Стандартная общая библиотека C|2.5-12|  
|Openssl|Библиотеки OpenSSL; протокол защищенной связи|0.9.8 или 1.0|  
|PAM|Подключаемые модули проверки подлинности|0.99.6.2-3.14|  


 **IBM AIX 6.1**  

|Требуемый пакет|Описание:|Минимальная версия|  
|----------------------|-----------------|---------------------|  
|Версия ОС|Версия операционной системы|AIX 6.1: любой уровень технологии и пакет обновления|  
|xlC.rte|Среда выполнения XL C/C++|9.0.0.5|  
|OpenSSL/openssl.base|Библиотеки OpenSSL; протокол защищенной связи|0.9.8.4|  

 **IBM AIX 7.1 (Power)**  

|Требуемый пакет|Описание:|Минимальная версия|  
|----------------------|-----------------|---------------------|  
|Версия ОС|Версия операционной системы|AIX 7.1: любой уровень технологии и пакет обновления|  
|xlC.rte|Среда выполнения XL C/C++||  
|OpenSSL/openssl.base|Библиотеки OpenSSL; протокол защищенной связи||  


 **HP-UX 11i v3 IA64**  

|Требуемый пакет|Описание:|Минимальная версия|  
|----------------------|-----------------|---------------------|  
|HPUX11i-OE|Операционная среда HP-UX Foundation|B.11.31.0709|  
|OS-Core.MinimumRuntime.CORE-SHLIBS|Библиотеки разработки, относящиеся к IA|B.11.31|  
|SysMgmtMin|Минимальный набор средств для развертывания ПО|B.11.31.0709|  
|SysMgmtMin.openssl|Библиотеки OpenSSL; протокол защищенной связи|A.00.09.08d.002|  
|PAM|Подключаемые модули проверки подлинности|В HP-UX модуль PAM входит в число основных компонентов операционной системы. Других зависимостей нет.|  

 **Зависимости Configuration Manager**. В следующей таблице перечислены роли системы сайта, поддерживающие клиенты Linux и UNIX. Дополнительные сведения об этих ролях системы сайта см. в статье [Определение ролей систем сайта для клиентов Configuration Manager](../../../../core/clients/deploy/plan/determine-the-site-system-roles-for-clients.md).  

|Система сайта Configuration Manager|Дополнительные сведения|  
|---------------------------------------|----------------------|  
|Точка управления|Хотя точка управления не требуется для установки клиента Configuration Manager для Linux и UNIX, она необходима для передачи информации между клиентскими компьютерами и серверами Configuration Manager. Без точки управления управлять клиентскими компьютерами невозможно.|  
|Точка распространения|Точка распространения не требуется для установки клиента Configuration Manager в Linux и UNIX. Однако роль системы сайта не требуется, если развертывание программного обеспечения на серверах Linux и UNIX.<br /><br /> Так как клиент Configuration Manager для Linux и UNIX не поддерживает передачу данных по протоколу SMB, используемые с этим клиентом точки распространения должны поддерживать передачу данных по протоколу HTTP или HTTPS.|  
|Резервная точка состояния|Резервная точка состояния не требуется для установки клиента Configuration Manager для Linux и UNIX. Но резервная точка состояния позволяет компьютерам на сайте Configuration Manager отправлять сообщения о состоянии, когда они не могут установить связь с точкой управления. Клиент может отправить резервная точка состояния состоянием их установки.|  

 **Требования к брандмауэрам**. Убедитесь, что брандмауэры не блокируют обмен данными через порты, указанные в качестве портов запросов клиентов. Клиент для Linux и UNIX напрямую взаимодействует с точками управления, точками распространения и резервными точками состояния.  

 Сведения о портах для взаимодействия и запросов клиентов см. в статье [Настройка клиента для Linux и UNIX для поиска точек управления](../../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md#BKMK_ConfigClientMP).  

##  <a name="planning-for-communication-across-forest-trusts-for-linux-and-unix-servers"></a><a name="BKMK_PlanningforCommunicationsforLnU"></a> Планирование обмена данными в пределах доверий леса для серверов Linux и UNIX  
 Серверы Linux и UNIX, которыми вы управляете с помощью Configuration Manager, выступают в качестве клиентов рабочих групп и требуют аналогичной настройки, как и клиенты на базе Windows, входящие в состав рабочей группы. Сведения о том, как осуществляется обмен данными между компьютерами в рабочих группах, см. в разделе [Обмен данными между лесами Active Directory](../../../plan-design/hierarchy/communications-between-endpoints.md#Plan_Com_X-Forest).  

###  <a name="service-location-by-the-client-for-linux-and-unix"></a><a name="BKMK_ServiceLocationforLnU"></a> Обнаружение службы клиентом для Linux и UNIX  
 Задача обнаружения сервера системы сайта, который предоставляет клиентам службы называется расположение службы. В отличие от клиента на основе Windows, клиент для Linux и UNIX не использует Active Directory для обнаружения служб. Кроме того, клиент Configuration Manager для Linux и UNIX не поддерживает свойство клиента, указывающее суффикс домена для точки управления. Вместо этого клиент узнает о дополнительные серверы системы сайта, обслуживающим клиентов из точки управления известных, назначаемые при установке клиентского программного обеспечения.  

 Дополнительные сведения см. в разделе [Обнаружение службы и определение клиентами назначенной им точки управления](../../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#BKMK_Plan_Service_Location).  

##  <a name="planning-for-security-and-certificates-for-linux-and-unix-servers"></a><a name="BKMK_SecurityforLnU"></a> Планирование безопасности и сертификаты для серверов Linux и UNIX  
 Для обеспечения безопасной связи с сайтами Configuration Manager и соответствующей проверки подлинности клиент Configuration Manager для Linux и UNIX использует ту же модель взаимодействия, что и клиент Configuration Manager для Windows.  

 При установке клиента Linux и UNIX можно назначить ему PKI-сертификат, который позволяет использовать протокол HTTPS для связи с сайтами Configuration Manager. Если не назначить PKI-сертификат, клиент создает самозаверяющий сертификат и передает данные только по протоколу HTTP.  

 Клиенты, предоставляемые сертификат PKI при установке использовать HTTPS для связи с точками управления. Когда клиенту не удалось найти точку управления, который поддерживает протокол HTTPS, он вернется на использование протокола HTTP с предоставленным PKI-сертификат.  

 Если клиент UNIX или Linux использует PKI-сертификат, вам не нужно утверждать их. Если клиент использует самозаверяющий сертификат, проверьте параметры иерархии для утверждения клиента в консоли Configuration Manager. Если метод утверждения клиента не **автоматически утвердить все компьютеры (не рекомендуется)** , необходимо утвердить клиента вручную.  

 Дополнительные сведения об утверждении клиентов вручную см. в разделе [Управление клиентами из узла "Устройства"](../../manage/manage-clients.md#BKMK_ManagingClients_DevicesNode).  

 Сведения о том, как использовать сертификаты в Configuration Manager, см. в статье [Требования к PKI-сертификатам для System Center Configuration Manager](../../../plan-design/network/pki-certificate-requirements.md).  

###  <a name="about-certificates-for-use-by-linux-and-unix-servers"></a><a name="BKMK_AboutCertsforLnU"></a> Сведения о сертификатах, используемых серверами Linux и UNIX  
 Клиент Configuration Manager для Linux и UNIX использует самозаверяющий сертификат или PKI-сертификат X.509 точно так же, как и клиенты на базе Windows. При управлении клиентами Linux и UNIX требования к PKI для систем сайта Configuration Manager ничем не отличаются.  

 Этот сертификат, используемый для клиентов Linux и UNIX, которые взаимодействуют с системами сайта Configuration Manager, должен иметь формат PKCS#12, а чтобы его можно было указывать клиенту при задании PKI-сертификата, необходимо знать пароль.  

 Клиент Configuration Manager для Linux и UNIX поддерживает использование только одного PKI-сертификата. Поэтому критерии выбора сертификатов, настроенные для сайта Configuration Manager, не применяются.  

###  <a name="configuring-certificates-for-linux-and-unix-servers"></a><a name="BKMK_ConfigCertsforLnU"></a> Настройка сертификатов для серверов Linux и UNIX  
 Чтобы настроить клиент Configuration Manager для серверов Linux и UNIX так, чтобы он применял связь по протоколу HTTPS, необходимо настроить для него использование PKI-сертификата во время установки клиента. Вы не можете подготовить сертификат до установки клиентского программного обеспечения.  

 При установке клиента, который использует PKI-сертификат, используйте параметр командной строки `-UsePKICert`, чтобы указать расположение и имя файла PKCS#12, содержащего PKI-сертификат. Кроме того, вам необходимо использовать параметр командной строки `-certpw`, чтобы указать пароль для сертификата.  

 Если вы не укажете параметр `-UsePKICert`, клиент создаст самозаверяющий сертификат и будет пытаться связаться с серверами системы сайта только по протоколу HTTP.  

##  <a name="versions-that-dont-support-sha-256"></a><a name="BKMK_NoSHA-256"></a> Версии, которые не поддерживают SHA-256  
 Следующие операционные системы Linux и UNIX, поддерживаемые в качестве клиентов для Configuration Manager, были выпущены с версиями OpenSSL, которые не поддерживают SHA-256:  

-   Solaris версии 10 (SPARC/x86)  


 Для управления этими операционными системами с помощью Configuration Manager необходимо установить клиент Configuration Manager для Linux и UNIX с использованием параметра командной строки, который позволяет клиенту пропустить проверку SHA-256. Клиенты Configuration Manager, выполняемые в этих версиях операционных систем, работают в менее безопасном режиме по сравнению с клиентами, поддерживающими SHA-256. Это менее безопасный режим имеет следующие особенности:  

-   Клиенты не проверяют подпись сервера сайта, связанную с политикой, которую они запрашивают из точки управления.  

-   Клиенты не проверяют хэш для пакетов, скачанных из точки распространения.  

> [!IMPORTANT]  
>  Параметр `ignoreSHA256validation` позволяет запустить клиент для компьютеров Linux и UNIX в режиме сниженной безопасности. Оно предназначено для использования в более старых платформ, которые не включать поддержку SHA-256. Это является переопределения безопасности и не рекомендуется корпорацией Майкрософт, но поддерживается для использования в среде надежную и безопасную центра обработки данных.  

 При установке клиента Configuration Manager для Linux и UNIX скрипт установки проверяет версию операционной системы. По умолчанию, если определяется версия операционной системы, не имеющая версии OpenSSL с поддержкой SHA-256, установка клиента Configuration Manager завершается сбоем.  

 Чтобы установить клиент Configuration Manager в операционной системе Linux или UNIX, в которой отсутствует версия OpenSSL с поддержкой SHA-256, необходимо использовать параметр командной строки `ignoreSHA256validation`. При использовании этого параметра командной строки в соответствующей операционной системе Linux или UNIX клиент Configuration Manager пропускает проверку SHA-256, а после установки не использует SHA-256 для подписи данных, передаваемых системам сайта по протоколу HTTP. Сведения о настройке клиентов Linux и UNIX на использование сертификатов см. в разделе [Планирование безопасности и сертификаты для Linux и UNIX](#BKMK_SecurityforLnU). Дополнительные сведения об обязательном использовании SHA-256 см. в разделе [Настройка подписывания и шифрования](../../../plan-design/security/configure-security.md#BKMK_ConfigureSigningEncryption).  

> [!NOTE]  
>  Параметр командной строки `ignoreSHA256validation` игнорируется на компьютерах, работающих под управлением Linux и UNIX с версией OpenSSL, поддерживающей SHA-256.  
