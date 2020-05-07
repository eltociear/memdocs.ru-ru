---
title: Шифрование данных восстановления
titleSuffix: Configuration Manager
description: Зашифруйте ключи восстановления BitLocker, пакеты восстановления и хэши паролей TPM по сети и в базе данных Configuration Manager.
ms.date: 04/15/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 1ee6541a-e243-43ea-be16-d0349f7f0c6e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 79f50cf4b0d241df2fc8d12dc46c833af278bd5a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709352"
---
# <a name="encrypt-recovery-data"></a>Шифрование данных восстановления

*Область применения: Configuration Manager (Current Branch)*

<!--3601034-->

При создании политики управления BitLocker Configuration Manager развертывает службу восстановления на точке управления. На странице **Управление клиентами** политики управления BitLocker при **настройке служб управления BitLocker** клиент создает резервную копию ключевых данных восстановления в базе данных сайта. Эти сведения включают ключи восстановления BitLocker, пакеты восстановления и хэши паролей доверенного платформенного модуля. Когда доступ пользователей к защищенным устройствам блокируется, эти сведения можно использовать для восстановления доступа к устройству.

Учитывая конфиденциальную природу этих сведений, необходимо защитить их в следующих случаях.

- Для Configuration Manager требуется подключение по протоколу HTTPS между клиентом и службой восстановления для шифрования передаваемых данных по сети. Существует два варианта.

  - Предоставьте HTTPS-подключение для веб-сайта IIS в точке управления, в которой размещена служба восстановления, а не для всей роли точки управления. Применимо только к Configuration Manager версии 2002.<!-- 5925660 -->

  - Настройте точку управления для HTTPS. В свойствах точки управления параметр **Подключения клиента** должен иметь значение **HTTPS**. Применимо к Configuration Manager версии 1910 или 2002.

    > [!NOTE]
    > Улучшенный протокол HTTP в настоящее время не поддерживается.

- Также рекомендуется шифровать эти данные при хранении в базе данных сайта. Вы можете использовать шифрование на уровне ячеек SQL Server с собственным сертификатом.

    Если вы не хотите создавать сертификат шифрования управления BitLocker, выберите хранилище данных восстановления в виде обычного текста. При создании политики управления BitLocker включите параметр, позволяющий **Сохранять данные восстановления в виде обычного текста**.

    > [!NOTE]
    > Еще один уровень безопасности — шифрование всей базы данных сайта. Если включить шифрование для базы данных, в Configuration Manager не будет никаких функциональных проблем.
    >
    > Шифрование следует использовать с осторожностью, особенно в крупномасштабных средах. В зависимости от того, какие таблицы шифруются и какая версия SQL используется, вы можете заметить снижение производительности на 25 %. Обновите планы резервного копирования и восстановления, чтобы можно было успешно восстановить зашифрованные данные.

## <a name="certificate-requirements"></a>Требования к сертификатам

### <a name="https-server-authentication-certificate"></a>Сертификат проверки подлинности сервера HTTPS

<!--5925660-->

В Configuration Manager текущей версии ветви 1910 для интеграции службы восстановления BitLocker требовалась точка управления с поддержкой HTTPS. HTTPS-подключение необходимо для шифрования ключей восстановления по сети от клиента Configuration Manager до точки управления. Настройка точки управления и всех клиентов для HTTPS может быть непростой задачей для многих клиентов.

Начиная с версии 2002, требование HTTPS предназначено для веб-сайта IIS, на котором размещена служба восстановления, а не для всей роли точки управления. Это изменение ослабляет требования к сертификатам, но ключи восстановления по-прежнему шифруются при передаче.

Теперь свойство **Клиентские подключения** точки управления может быть **HTTP** или **HTTPS**. Если точка управления настроена для **HTTP**, для поддержки службы восстановления BitLocker:

1. Получите сертификат проверки подлинности сервера. Привяжите сертификат к веб-сайту IIS в точке управления, в которой размещена служба восстановления BitLocker.

2. Настройте клиенты, чтобы они доверяли сертификату проверки подлинности сервера. Создать доверие можно двумя способами.

    - Использовать сертификат от общедоступного и доверенного в глобальном масштабе поставщика сертификатов. Такими поставщиками могут быть, помимо прочего, DigiCert, Thawte или VeriSign. Клиенты Windows включают доверенные корневые центры сертификации (ЦС) от этих поставщиков. Используя сертификат проверки подлинности сервера, выданный одним из этих поставщиков, клиенты автоматически устанавливают с ним отношение доверия.

    - Используйте сертификат, выданный центром сертификации из инфраструктуры открытых ключей (PKI) вашей организации. Большинство реализаций PKI добавляют доверенные корневые ЦС в клиенты Windows. Например, использование служб сертификатов Active Directory с групповой политикой. Если сертификат проверки подлинности выдается из ЦС, с которым у ваших клиентов нет автоматического отношения доверия, добавьте доверенный корневой сертификат ЦС для клиентов.

> [!TIP]
> Единственными клиентами, которым требуется взаимодействовать со службой восстановления, являются клиенты, которые вы планируете использовать с политикой управления BitLocker и правилом **Управление клиентами**.

Чтобы устранить неполадки подключения, на клиенте используйте **BitLockerManagementHandler.log**. Для подключения к службе восстановления в журнале отображается URL-адрес, который используется клиентом. Найдите запись, которая начинается с `Checking for Recovery Service at`.

> [!NOTE]
> Если сайт имеет более одной точки управления, включите протокол HTTPS во всех точках управления на сайте, с которыми может взаимодействовать клиент, управляемый BitLocker. Если точка управления HTTPS окажется недоступна, клиент может выполнить отработку отказа в точку управления HTTP, после чего не сможет депонировать свой ключ восстановления.
>
> Эта рекомендация относится к обоим вариантам: включению HTTPS для точки управления или включению веб-сайта IIS, на котором размещена служба восстановления, в точке управления.

### <a name="sql-encryption-certificate"></a>Сертификат шифрования SQL

Используйте этот сертификат, чтобы включить шифрование SQL Server для данных восстановления BitLocker на уровне ячеек. Вы можете использовать собственный процесс для создания и развертывания сертификата шифрования управления BitLocker, если он соответствует следующим требованиям.

- Имя сертификата шифрования управления BitLocker должно быть `BitLockerManagement_CERT`.

- Этот сертификат должен быть зашифрован с помощью главного ключа базы данных.

- Следующие пользователи SQL должны иметь разрешения **Контроль** для сертификата:
  - RecoveryAndHardwareCore
  - RecoveryAndHardwareRead
  - RecoveryAndHardwareWrite

- Разверните одинаковый сертификат в каждой базе данных сайта в иерархии.

- Создайте сертификат с последней версией SQL Server в вашей среде. Пример.
  - Сертификаты, созданные с помощью SQL Server 2016 или более поздней версии, совместимы с SQL Server 2014 или более ранней версии.
  - Сертификаты, созданные с помощью SQL Server 2014 или более ранней версии, несовместимы с SQL Server 2016 или более поздней версии.

## <a name="example-scripts"></a>Примеры сценариев

Эти скрипты SQL являются примерами для создания и развертывания сертификата шифрования управления BitLocker в базе данных сайта Configuration Manager.

### <a name="create-certificate"></a>Создание сертификата

Этот пример скрипта выполняет следующие действия:

- Создает сертификат
- Задает разрешения.
- Создает главный ключ базы данных

Прежде чем использовать этот скрипт в рабочей среде, измените следующие значения:

- Имя базы данных сайта (`CM_ABC`)
- Пароль для создания главного ключа (`MyMasterKeyPassword`)
- Дата истечения срока действия сертификата (`20391022`)

``` SQL
USE CM_ABC
IF NOT EXISTS (SELECT name FROM sys.symmetric_keys WHERE name = '##MS_DatabaseMasterKey##')
BEGIN
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'MyMasterKeyPassword'
END

IF NOT EXISTS (SELECT name from sys.certificates WHERE name = 'BitLockerManagement_CERT')
BEGIN
    CREATE CERTIFICATE BitLockerManagement_CERT AUTHORIZATION RecoveryAndHardwareCore
    WITH SUBJECT = 'BitLocker Management',
    EXPIRY_DATE = '20391022'

    GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareRead
    GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareWrite
END
```

### <a name="back-up-certificate"></a>Резервное копирование сертификата

Этот пример скрипта создает резервную копию сертификата. При сохранении сертификата в файл его можно [восстановить](#restore-certificate) в другие базы данных сайта в иерархии.

Прежде чем использовать этот скрипт в рабочей среде, измените следующие значения:

- Имя базы данных сайта (`CM_ABC`)
- Имя и путь к файлу (`C:\BitLockerManagement_CERT_KEY`)
- Пароль ключа экспорта (`MyExportKeyPassword`)

``` SQL
USE CM_ABC
BACKUP CERTIFICATE BitLockerManagement_CERT TO FILE = 'C:\BitLockerManagement_CERT'
    WITH PRIVATE KEY ( FILE = 'C:\BitLockerManagement_CERT_KEY',
        ENCRYPTION BY PASSWORD = 'MyExportKeyPassword')
```

> [!IMPORTANT]
> Сохраните экспортированный файл сертификата и связанный с ним пароль в безопасном месте.

### <a name="restore-certificate"></a>Восстановление сертификата

Этот пример скрипта восстанавливает сертификат из файла. Используйте этот процесс для развертывания сертификата, созданного в другой базе данных сайта.

Прежде чем использовать этот скрипт в рабочей среде, измените следующие значения:

- Имя базы данных сайта (`CM_ABC`)
- Пароль главного ключа (`MyMasterKeyPassword`)
- Имя и путь к файлу (`C:\BitLockerManagement_CERT_KEY`)
- Пароль ключа экспорта (`MyExportKeyPassword`)

``` SQL
USE CM_ABC
IF NOT EXISTS (SELECT name FROM sys.symmetric_keys WHERE name = '##MS_DatabaseMasterKey##')
BEGIN
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'MyMasterKeyPassword'
END

IF NOT EXISTS (SELECT name from sys.certificates WHERE name = 'BitLockerManagement_CERT')
BEGIN

CREATE CERTIFICATE BitLockerManagement_CERT AUTHORIZATION RecoveryAndHardwareCore
FROM FILE  = 'C:\BitLockerManagement_CERT'
    WITH PRIVATE KEY ( FILE = 'C:\BitLockerManagement_CERT_KEY',
        DECRYPTION BY PASSWORD = 'MyExportKeyPassword')

GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareRead
GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareWrite
END
```

### <a name="verify-certificate"></a>Проверка сертификата

Используйте этот скрипт SQL, чтобы убедиться, что SQL успешно создал сертификат с необходимыми разрешениями.

``` SQL
USE CM_ABC
declare @count int
select @count = count(distinct u.name) from sys.database_principals u
join sys.database_permissions p on p.grantee_principal_id = u.principal_id or p.grantor_principal_id = u.principal_id
join sys.certificates c on c.certificate_id = p.major_id
where u.name in('RecoveryAndHardwareCore', 'RecoveryAndHardwareRead', 'RecoveryAndHardwareWrite') and
c.name = 'BitLockerManagement_CERT' and p.permission_name like 'CONTROL'
if(@count >= 3) select 1
else select 0
```

Если сертификат действителен, скрипт возвращает значение `1`.

## <a name="see-also"></a>См. также

Дополнительные сведения об этих командах SQL см. в следующих статьях:

- [SQL Server и ключи шифрования базы данных](https://docs.microsoft.com/sql/relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine)
- [Создание сертификата](https://docs.microsoft.com/sql/t-sql/statements/create-certificate-transact-sql)
- [Резервное копирование сертификата](https://docs.microsoft.com/sql/t-sql/statements/backup-certificate-transact-sql)
- [Создание главного ключа](https://docs.microsoft.com/sql/t-sql/statements/create-master-key-transact-sql)
- [Резервное копирование главного ключа](https://docs.microsoft.com/sql/t-sql/statements/backup-master-key-transact-sql)
- [Предоставление разрешений сертификатов](https://docs.microsoft.com/sql/t-sql/statements/grant-certificate-permissions-transact-sql)
