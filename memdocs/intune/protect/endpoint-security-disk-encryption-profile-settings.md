---
title: Параметры политики шифрования дисков для обеспечения безопасности конечных точек Intune | Документация Майкрософт
description: Параметры политики шифрования дисков для обеспечения безопасности конечных точек для BitLocker и FileVault в Microsoft Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: db23ee1742934e8545c03c529d6a05c13cc59f1a
ms.sourcegitcommit: 6ca5e75ed7a6fd2186fbe51c177960004d5ec81f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2020
ms.locfileid: "83633286"
---
# <a name="disk-encryption-policy-settings-for-endpoint-security-in-intune"></a>Параметры политики шифрования дисков для обеспечения безопасности конечных точек в Intune

Просмотрите параметры, которые можно настроить в профилях для политики *Шифрование дисков* в узле безопасности конечных точек в Intune в рамках [политики безопасности конечных точек](../protect/endpoint-security-policy.md).

Поддерживаемые платформы и профили

- **macOS**:
  - Профиль: **FileVault**
- **Windows 10 и более поздних версий**
  - Профиль: **BitLocker**

## <a name="filevault"></a>FileVault

### <a name="encryption"></a>Encryption

**Включить FileVault**  
- **Не настроено** (*по умолчанию*)
- **Да** — включить полное шифрование диска с помощью XTS-AES 128 с FileVault на устройствах под управлением macOS 10.13 и более поздних версий. FileVault включается, когда пользователь выходит с устройства.

  Если задано значение *Да*, можно настроить дополнительные параметры для FileVault.

  - Для устройств создаются ключи восстановления **Тип ключа восстановления**
    *Личный ключ*. Настройте следующие параметры для личного ключа.

    - **Смена личного ключа восстановления**  
      Укажите частоту смены личного ключа восстановления для устройства. Можно выбрать значение по умолчанию **Не настроено** или значение от **1** до **12** месяцев.
    - **Описание расположения персонального криптоключа восстановления**  
      Введите короткое сообщение для пользователя, в котором объясняется, как можно получить личный ключ восстановления. Это сообщение пользователь видит на экране входа в систему при появлении запроса на ввод личного ключа восстановления в случае, если пароль забыт.

  - **Число разрешенных пропусков**  
    Задайте, сколько раз пользователь может игнорировать запросы о включении FileVault, прежде чем оно станет обязательным для входа.
    - **Не настроено** (*по умолчанию*) — на устройстве требуется включить шифрование, прежде чем будет разрешен следующий вход в систему.
    - От **1** до **10** — пользователь может игнорировать запрос от 1 до 10 раз, прежде чем требовать шифрования на устройстве.
    - **Без ограничения, всегда запрашивать** — выводится запрос на включение FileVault, но шифрование никогда не требуется.

  - **Возможность отсрочки до выхода**  
    - **Не настроено** (*по умолчанию*)
    - **Да** — отложить запрос на включение FileVault, пока пользователь не выйдет из системы.  

  - **Отключить запрос при выходе**  
    Запрет вывода запроса на включение FileVault при выходе пользователя из системы. Если задано значение "Отключено", запрос при выходе будет отключен, и будет выводиться запрос при входе в систему.
    - **Не настроено** (*по умолчанию*)
    - **Да** — отключить запрос на включение FileVault, который появляется при выходе.

## <a name="bitlocker"></a>BitLocker

### <a name="bitlocker--base-settings"></a>Базовые параметры BitLocker

- **Включить полное шифрование диска для ОС и фиксированных дисков данных**  
  CSP: [RequireDeviceEncryption](https://go.microsoft.com/fwlink/?linkid=872523)

  Если диск был зашифрован до применения политики, дополнительные действия не предпринимаются. Если метод шифрования и параметры соответствуют настройкам политики, конфигурация должна сообщить об успешной установке. Если параметр конфигурации BitLocker не соответствует этой политике, то конфигурация, скорее всего, вернет ошибку.
  
  Чтобы применить эту политику к уже зашифрованному диску, расшифруйте диск и повторно примените политику MDM. По умолчанию Windows не требует шифрование диска BitLocker. Однако в случае присоединения к Azure AD и при регистрации учетной записи Майкрософт (MSA) или входе в систему с ее помощью автоматическое шифрование может применяться для BitLocker со 128-битным шифрованием XTS-AES.

  - **Не настроено** (*по умолчанию*) — принудительное применение BitLocker не выполняется.
  - **Да** — принудительное использование BitLocker.

- **Требовать шифрование карт памяти (только для мобильных устройств)**  
  CSP: [RequireStorageCardEncryption](https://go.microsoft.com/fwlink/?linkid=872524)

  Этот параметр применяется только к устройствам SKU Windows Mobile и Mobile Enterprise.
  - **Не настроено** (*по умолчанию*) — параметр возвращается к значению ОС по умолчанию, то есть шифрование карты памяти не требуется.
  - **Да** — для мобильных устройств требуется шифрование на картах памяти.

- **Скрыть запрос о продукте шифрования стороннего разработчика**  
  CSP: [AllowWarningForOtherDiskEncryption](https://go.microsoft.com/fwlink/?linkid=872525)

  Если BitLocker включен в системе, которая уже зашифрована с помощью стороннего продукта шифрования, такое устройство может стать непригодным для использования. Могут возникнуть потери данных, и вам может потребоваться переустановить Windows. Настоятельно рекомендуется никогда не включать BitLocker на устройстве с установленным или включенным продуктом шифрования стороннего разработчика.

  По умолчанию мастер установки BitLocker запрашивает у пользователей подтверждение того, что продукт шифрования стороннего разработчика отсутствует.

  - **Не настроено** (*по умолчанию*) — мастер установки BitLocker выводит предупреждение и предлагает пользователям подтвердить отсутствие продукта шифрования стороннего разработчика.
  - **Да** — запросы мастеров установки BitLocker скрываются от пользователей.

  Если требуются функции автоматического включения BitLocker, предупреждение о продукте шифрования стороннего разработчика должно быть скрыто, так как любые запросы нарушают работу автоматических процессов.

  Если задано значение *Да*, можно настроить следующий параметр.

  - **Разрешить обычным пользователям включать шифрование для сценариев Autopilot**  
    CSP: [AllowStandardUserEncryption](https://go.microsoft.com/fwlink/?linkid=2114200)
    - **Не настроено** (*по умолчанию*) — во время сценариев автоматического включения присоединения к Azure Active Directory (AADJ) пользователям не нужно быть локальными администраторами для включения BitLocker.
    - **Да** — этот параметр оставлен в качестве значения по умолчанию для клиента, которое подразумевает обязательное наличие доступа локального администратора для включения BitLocker.

    Для сценариев, отличных от автоматического включения, и сценариев Autopilot пользователь должен быть локальным администратором для завершения процедуры в мастере установки BitLocker.

- **Включить управляемую клиентом смену пароля восстановления**  
  CSP: [ConfigureRecoveryPasswordRotation](https://go.microsoft.com/fwlink/?linkid=2114201)

  Устройства добавления рабочей учетной записи (AWS, формально присоединенные к рабочей области) не поддерживаются для смены ключа.
  - **Не настроено** (*умолчанию*) — клиент не будет сменять ключи восстановления BitLocker.
  - **Отключено**
  - **Устройства, присоединенные к Azure AD**.
  - **Устройства с присоединением к Azure AD и гибридным присоединением**

### <a name="bitlocker---fixed-drive-settings"></a>Параметры жестких дисков в BitLocker

- **Политика BitLocker в отношении жестких дисков**  
  [Параметры групповой политики BitLocker](https://go.microsoft.com/fwlink/?linkid=2067018)

  - **Восстановление несъемных дисков**  
    CSP: [FixedDrivesRecoveryOptions](https://go.microsoft.com/fwlink/?linkid=872538)

    Управление восстановлением жестких дисков данных, защищенных с помощью BitLocker, при отсутствии необходимых сведений о ключах запуска.

    - **Не настроено** (*по умолчанию*) — поддерживаются параметры восстановления по умолчанию, включая агент восстановления данных (DRA). Конечный пользователь может указать параметры восстановления, а сведения о восстановлении не архивируются в Azure Active Directory.
    - **Настроить** — разрешение доступа для настройки различных методов восстановления диска.

    Если задано значение *Настроить*, доступны следующие параметры.

    - **Создание пользователем ключа восстановления**  
      - **Заблокировано** (*по умолчанию*)
      - **Обязательное**
      - **Допускается**

    - **Настройка пакета восстановления BitLocker**
      - **Пароль и ключ** (*по умолчанию*) — включение пароля восстановления BitLocker, применяемого администраторами и пользователями для разблокировки защищенных дисков, и пакетов ключей восстановления, используемых администраторами для восстановления данных, в Active Directory.
      - **Только пароль** — пакеты ключей восстановления могут быть недоступны, когда в них возникает необходимость.

    - **Требовать от устройства архивировать сведения о восстановлении в Azure AD**
      - **Не настроено** (*по умолчанию*) — включение BitLocker будет завершено, даже если архивация ключей восстановления в Azure AD завершается сбоем. Это может привести к тому, что никакие сведения о восстановлении во внешней среде храниться не будут.
      - **Да** — BitLocker не завершает включение, пока ключи восстановления не будут успешно сохранены в Azure Active Directory.

    - **Создание пользователем пароля восстановления**  
      - **Заблокировано** (*по умолчанию*)
      - **Обязательное**
      - **Допускается**

    - **Скрытие параметров восстановления во время установки BitLocker**
      - **Не настроено** (*по умолчанию*) — предоставляет пользователю доступ к дополнительным параметрам восстановления.
      - **Да** — запрещает пользователю выбирать дополнительные параметры восстановления, такие как печать ключей восстановления, во время работы мастера установки BitLocker.

    - **Включение BitLocker после сохранения данных восстановления**
      - **Не настроено** (*по умолчанию*)  
      - **Да**

    - **Блокировка использования агента восстановления данных (DRA) на основе сертификатов**
      - **Не настроено** (*по умолчанию*) — разрешает настройку агента восстановления данных. Для настройки агента восстановления данных требуется корпоративный PKI и объекты групповой политики для развертывания агента DRA и сертификатов.
      - **Да** — блокирует возможность использования агента восстановления данных (DRA) для восстановления дисков с поддержкой BitLocker.

  - **Блокировка доступа на запись к фиксированным дискам с данными, не защищенным BitLocker**  
    CSP: [FixedDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872534)  
    Этот параметр доступен, если *Политика фиксированного диска BitLocker* имеет значение *Настроить*.

    - **Не настроено** (*по умолчанию*) — данные могут записываться на незашифрованные фиксированные диски.
    - **Да** — Windows не будет разрешать запись данных на фиксированные диски, не защищенные с помощью BitLocker. Если фиксированный диск не зашифрован, пользователю потребуется завершить работу мастера установки BitLocker для диска, прежде чем ему будет предоставлен доступ на запись.

  - **Настроить метод шифрования для фиксированных дисков с данными**  
    CSP: [EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)  

    Настройте метод шифрования и стойкость шифра для фиксированных дисков с данными. *XTS-AES, 128 бит* — это метод шифрования Windows по умолчанию и рекомендуемое значение.

    - **Не настроено** (*по умолчанию*)
    - **AES CBC, 128 бит**
    - **AES CBC, 256 бит**
    - **AES XTS, 128 бит**
    - **AES XTS, 256 бит**

### <a name="bitlocker---os-drive-settings"></a>Параметры дисков ОС в BitLocker

- **Политика BitLocker в отношении системных дисков**  
  CSP: [Параметры групповой политики BitLocker](https://go.microsoft.com/fwlink/?linkid=2067025)

  - **Настроить** (*по умолчанию*)  
  - **Не настроено**.

  Если задано значение *Настроить*, можно настроить следующие параметры.

  - **Требуется проверка подлинности при запуске**  
    CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

    - **Не настроено** (*по умолчанию*)
    - **Да** — позволяет настраивать дополнительные требования к проверке подлинности при запуске системы, в том числе использование доверенного платформенного модуля (TPM) или требования к ПИН-коду запуска.

    Если задано значение *Да*, можно настроить указанные ниже параметры.

    - **Запуск совместимого доверенного платформенного модуля**  
      CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      Рекомендуется запрашивать доверенный платформенный модуль для BitLocker. Этот параметр применяется только при первом включении BitLocker и не действует, если BitLocker уже включен.

      - **Заблокировано** (*по умолчанию*) — BitLocker не использует доверенный платформенный модуль.
      - **Обязательно** — BitLocker включается только в том случае, если доверенный платформенный модуль присутствует и пригоден для использования.
      - **Разрешено** — BitLocker использует доверенный платформенный модуль, если он есть.

    - **ПИН-код запуска совместимого доверенного платформенного модуля**  
      CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      - **Заблокировано** (*по умолчанию*) — блокирует использование ПИН-кода.
      - **Обязательно** — требует наличия ПИН-кода и доверенного платформенного модуля для включения BitLocker.
      - **Разрешено** — BitLocker использует доверенный платформенный модуль, если он есть, и позволяет пользователю настроить ПИН-код запуска.

      Для сценариев автоматического включения необходимо задать для этого параметра значение *Заблокировано*. Сценарии автоматического включения (включая Autopilot) не будут работать, если требуется вмешательство пользователя.

    - **Ключ запуска совместимого доверенного платформенного модуля**  
      CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      - **Заблокировано** (*по умолчанию*) — блокирует использование ключей запуска.
      - **Обязательно** — требует наличия ключа запуска и доверенного платформенного модуля для включения BitLocker.
      - **Разрешено** — BitLocker использует доверенный платформенный модуль, если он есть, и позволяет использовать ключ запуска (например, USB-накопитель) для разблокировки дисков.

      Для сценариев автоматического включения необходимо задать для этого параметра значение *Заблокировано*. Сценарии автоматического включения (включая Autopilot) не будут работать, если требуется вмешательство пользователя.

    - **Ключ и ПИН-код запуска совместимого доверенного платформенного модуля**  
      CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      - **Заблокировано** (*по умолчанию*) — блокирует использование комбинации ключа запуска и ПИН-кода.
      - **Обязательно** — требует наличие ключа запуска и ПИН-кода для включения BitLocker.
      - **Разрешено** — BitLocker использует доверенный платформенный модуль, если он есть, и позволяет использовать комбинацию ключа запуска и ПИН-кода.

      Для сценариев автоматического включения необходимо задать для этого параметра значение *Заблокировано*. Сценарии автоматического включения (включая Autopilot) не будут работать, если требуется вмешательство пользователя.

    - **Отключить BitLocker на устройствах с несовместимым доверенным платформенным модулем**  
    CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      Если доверенный платформенный модуль отсутствует, для запуска BitLocker требуется пароль или USB-накопитель.

      Этот параметр применяется только при первом включении BitLocker и не действует, если BitLocker уже включен.

      - **Не настроено** (*по умолчанию*)
      - **Да** — блокирует настройку BitLocker без совместимой микросхемы доверенного платформенного модуля.

    - **Включить сообщение и URL-адрес предзагрузочного восстановления**  
      CSP: [SystemDrivesRecoveryMessage](https://go.microsoft.com/fwlink/?linkid=872530)configure

      - **Не настроено** (*по умолчанию*) — использовать сведения о предзагрузочном восстановлении BitLocker по умолчанию.
      - **Да** — включить конфигурацию настраиваемого сообщения и URL-адреса предзагрузочного восстановления, чтобы помочь пользователям понять, как найти пароль восстановления. Сообщение и URL-адрес предзагрузочного восстановления отображаются для пользователей, когда они заблокировали свой компьютер в режиме восстановления.

      Если задано значение *Да*, можно настроить указанные ниже параметры.

      - **Сообщение предзагрузочного восстановления**  
        Укажите настраиваемое сообщение предзагрузочного восстановления.

      - **URL-адрес предзагрузочного восстановления**  
        Укажите настраиваемый URL-адрес предзагрузочного восстановления.

    - **Восстановление системных дисков**  
      CSP: [SystemDrivesRecoveryOptions](https://go.microsoft.com/fwlink/?linkid=872529)

      - **Не настроено** (*по умолчанию*)  
      - **Настроить** — включение конфигурации с дополнительными параметрами.

      Если задано значение *Настроить*, доступны следующие параметры.

      - **Создание пользователем ключа восстановления**  
        - **Заблокировано** (*по умолчанию*)
        - **Обязательное**
        - **Допускается**

      - **Настройка пакета восстановления BitLocker**
        - **Пароль и ключ** (*по умолчанию*) — включение пароля восстановления BitLocker, применяемого администраторами и пользователями для разблокировки защищенных дисков, и пакетов ключей восстановления, используемых администраторами для восстановления данных, в Active Directory.
        - **Только пароль** — пакеты ключей восстановления могут быть недоступны, когда в них возникает необходимость.

      - **Требовать от устройства архивировать сведения о восстановлении в Azure AD**
        - **Не настроено** (*по умолчанию*) — включение BitLocker будет завершено, даже если архивация ключей восстановления в Azure AD завершается сбоем. Это может привести к тому, что никакие сведения о восстановлении во внешней среде храниться не будут.
        - **Да** — BitLocker не завершает включение, пока ключи восстановления не будут успешно сохранены в Azure Active Directory.

      - **Создание пользователем пароля восстановления**  
        - **Заблокировано** (*по умолчанию*)
        - **Обязательное**
        - **Допускается**

      - **Скрытие параметров восстановления во время установки BitLocker**
        - **Не настроено** (*по умолчанию*) — предоставляет пользователю доступ к дополнительным параметрам восстановления.
        - **Да** — запрещает пользователю выбирать дополнительные параметры восстановления, такие как печать ключей восстановления, во время работы мастера установки BitLocker.

      - **Включение BitLocker после сохранения данных восстановления**
        - **Не настроено** (*по умолчанию*)  
        - **Да**

      - **Блокировка использования агента восстановления данных (DRA) на основе сертификатов**
        - **Не настроено** (*по умолчанию*) — разрешает настройку агента восстановления данных. Для настройки агента восстановления данных требуется корпоративный PKI и объекты групповой политики для развертывания агента DRA и сертификатов.
        - **Да** — блокирует возможность использования агента восстановления данных (DRA) для восстановления дисков с поддержкой BitLocker.

    - **Минимальная длина PIN-кода**  
      CSP: [SystemDrivesMinimumPINLength](https://go.microsoft.com/fwlink/?linkid=872528)

      Укажите минимальную длину ПИН-кода запуска, если при включении BitLocker требуется сочетание доверенного платформенного модуля и ПИН-кода. Длина ПИН-кода должна составлять от 4 до 20 цифр.

      Если этот параметр не настроен, пользователи могут настроить ПИН-код запуска любой длины (в диапазоне от 4 до 20 цифр).

      Этот параметр применяется только при первом включении BitLocker и не действует, если BitLocker уже включен.

  - **Настройка метода шифрования для дисков операционной системы**  
   CSP: [EncryptionMethodByDriveType]( https://go.microsoft.com/fwlink/?linkid=872526)

    Настройте метод шифрования и стойкость шифра для дисков операционной системы. *XTS-AES, 128 бит* — это метод шифрования Windows по умолчанию и рекомендуемое значение.

    - **Не настроено** (*по умолчанию*)
    - **AES CBC, 128 бит**
    - **AES CBC, 256 бит**
    - **AES XTS, 128 бит**
    - **AES XTS, 256 бит**

### <a name="bitlocker---removable-drive-settings"></a>Параметры съемных носителей в BitLocker

- **Настройка метода шифрования для дисков операционной системы**  
  CSP: [Параметры групповой политики BitLocker](https://go.microsoft.com/fwlink/?linkid=2067140)

  - **Не настроено** (*по умолчанию*)  
  - **Настройте**

  Если задано значение *Настроить*, можно настроить следующие параметры.

  - **Настройка метода шифрования для съемных дисков с данными**  
    CSP: [EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)

    Выберите нужный метод шифрования для съемных дисков с данными.

    - **Не настроено** (*по умолчанию*)
    - **AES CBC, 128 бит**
    - **AES CBC, 256 бит**
    - **AES XTS, 128 бит**
    - **AES XTS, 256 бит**

  - **Блокировка доступа на запись к съемным дискам с данными, не защищенным BitLocker**  
    CSP: [RemovableDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872540)

    - **Не настроено** (*по умолчанию*) — данные могут записываться на незашифрованные съемные диски.
    - **Да** — Windows не разрешает запись данных на съемные носители, не защищенные с помощью BitLocker. Если вставленный съемный носитель не зашифрован, пользователю необходимо завершить работу мастера установки BitLocker для диска, прежде чем будет предоставлен доступ на запись к этому носителю.

    - **Блокировка доступа на запись к съемным дискам с данными, не защищенным BitLocker**  
      CSP: [RemovableDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872540)

      - **Не настроено** (*по умолчанию*) — можно использовать любой диск, зашифрованный BitLocker.
      - **Да** — блокирует доступ к съемным носителям, если они не были зашифрованы на компьютере, принадлежащем вашей организации.

## <a name="next-steps"></a>Дальнейшие шаги

[Политика безопасности конечной точки для шифрования дисков](../protect/endpoint-security-disk-encryption-policy.md)