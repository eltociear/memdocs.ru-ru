---
title: Журналы событий клиента
titleSuffix: Configuration Manager
description: Технический справочник по возможным записям клиента BitLocker (MBAM) в журнале событий Windows
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: c38b6963-cb1f-40ed-a888-e19d401ec3fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4043af4aa30942a5e8e1f7d2a3d1017c1e72d89f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705972"
---
# <a name="client-event-logs"></a>Журналы событий клиента

*Область применения: Configuration Manager (Current Branch)*

<!--3601034-->

Журналы событий клиента BitLocker можно просматривать с помощью средства просмотра событий Windows в клиенте Configuration Manager, на котором развертывается политика управления BitLocker. Перейдите в раздел **Журналы приложений и служб**, **Microsoft**, **Windows**, **MBAM**, где находятся [Административные](#admin) и [Рабочие](#operational) журналы событий.

## <a name="admin"></a>Администратор

### <a name="2-volumeenactmentfailed"></a>2\. VolumeEnactmentFailed

Произошла ошибка при применении политик MBAM.

#### <a name="error-code--2144272219"></a>Код ошибки: 2144272219

Подробные сведения: Функция шифрования дисков BitLocker поддерживает шифрование только используемого пространства лишь в хранилище с тонкой подготовкой.

Эта ошибка возникает при попытке использовать BitLocker для шифрования виртуальной машины под управлением Windows 10 версии 1803 или более ранней. Более ранние версии Windows 10 не поддерживают полное шифрование диска. Политики управления BitLocker применяют полное шифрование диска.

#### <a name="error-code--2147024774"></a>Код ошибки: 2147024774

Подробные сведения: Область данных, переданная системному вызову, слишком мала.

Чтобы устранить эту проблему, перезапустите компьютер.

### <a name="4-transferstatusdatafailed"></a>4\. TransferStatusDataFailed

Произошла ошибка при отправке данных о состоянии шифрования.

### <a name="8-systemvolumenotfound"></a>8: SystemVolumeNotFound

Системный том отсутствует. Для шифрования диска операционной системы необходимо значение SystemVolume.

### <a name="9-tpmnotfound"></a>9: TPMNotFound

Оборудование доверенного платформенного модуля отсутствует. Для шифрования диска операционной системы необходим доверенный платформенный модуль с системой защиты доверенного платформенного модуля.

### <a name="10-machinehwexempted"></a>10: MachineHWExempted

Компьютер исключен из шифрования. Состояние оборудования компьютера: Исключено

### <a name="11-machinehwunknown"></a>11: MachineHWUnknown

Компьютер исключен из шифрования. Состояние оборудования компьютера: Неизвестно

### <a name="12-hwcheckfailed"></a>12: HWCheckFailed

Сбой проверки исключения оборудования.

### <a name="13-userisexempted"></a>13: UserIsExempted

Пользователь исключен из шифрования.

### <a name="14-useriswaiting"></a>14: UserIsWaiting

Пользователь запросил исключение.

### <a name="15-userexemptioncheckfailed"></a>15: UserExemptionCheckFailed

Сбой проверки исключения пользователя.

### <a name="16-userpostponed"></a>16: UserPostponed

Пользователь отложил процесс шифрования.

### <a name="17-tpminitializationfailed"></a>17: TPMInitializationFailed

Сбой инициализации доверенного платформенного модуля. Пользователь отклонил изменения в BIOS.

### <a name="18-coreservicedown"></a>18: CoreServiceDown

Не удалось подключиться к службе восстановления и оборудования MBAM.

#### <a name="error-code--2147024809"></a>Код ошибки: 2147024809

Подробные сведения: неверный параметр.

Эта ошибка возникает, если веб-сайт не является HTTPS или у клиента нет сертификата PKI.

### <a name="20-policymismatch"></a>20: PolicyMismatch

Политика управления BitLocker конфликтует или повреждена.

### <a name="21-conflictingosvolumepolicies"></a>21: ConflictingOSVolumePolicies

Обнаруженные политики шифрования тома операционной системы конфликтуют. Проверьте политики BitLocker, связанные с системой защиты дисков операционной системы.

### <a name="22-conflictingfddvolumepolicies"></a>22: ConflictingFDDVolumePolicies

Обнаруженные политики шифрования тома фиксированного диска с данными конфликтуют. Проверьте политики BitLocker, связанные с системой защиты фиксированных дисков с данными.

### <a name="27-encryptionfailednodra"></a>27: EncryptionFailedNoDra

Произошла ошибка во время шифрования. В режиме FIPS до загрузки Windows 8.1 требуется система защиты агента восстановления данных.

### <a name="34-tpmlockoutresetfailed"></a>34: TpmLockOutResetFailed

Не удалось сбросить блокировку доверенного платформенного модуля.

### <a name="36-tpmownerauthretrievalfailed"></a>36: TpmOwnerAuthRetrievalFailed

Не удалось получить OwnerAuth доверенного платформенного модуля из служб MBAM.

### <a name="37-wmiproviderdllsearchpathupdatefailed"></a>37: WmiProviderDllSearchPathUpdateFailed

Не удалось обновить пути поиска DLL для поставщика WMI.

### <a name="38-timedoutwaitingforwmiprovider"></a>38: TimedOutWaitingForWmiProvider

Остановка агента. Истекло время ожидания ответа от экземпляра поставщика WMI MBAM.

## <a name="operational"></a>Оперативный

### <a name="1-volumeenactmentsuccessful"></a>1: VolumeEnactmentSuccessful

Политики управления BitLocker применены.

### <a name="3-transferstatusdatasuccessful"></a>3\. TransferStatusDataSuccessful

Данные о состоянии шифрования успешно отправлены.

### <a name="19-coreserviceup"></a>19: CoreServiceUp

Успешное подключение к службе восстановления и оборудования MBAM.

### <a name="28-tpmownerauthescrowed"></a>28: TpmOwnerAuthEscrowed

OwnerAuth доверенного платформенного модуля депонирован.

### <a name="29-recoverykeyescrowed"></a>29: RecoveryKeyEscrowed

Ключ восстановления BitLocker для тома депонирован.

### <a name="30-recoverykeyreset"></a>30: RecoveryKeyReset

Ключ восстановления BitLocker для тома обновлен.

### <a name="31-enforcepolicydateset"></a>31: EnforcePolicyDateSet

Для тома установлена дата применения политики.

### <a name="32-enforcepolicydatecleared"></a>32: EnforcePolicyDateCleared

Для тома удалена дата применения политики.

### <a name="33-tpmlockoutresetsucceeded"></a>33: TpmLockOutResetSucceeded

Блокировка доверенного платформенного модуля сброшена.

### <a name="35-tpmownerauthretrievalsucceeded"></a>35: TpmOwnerAuthRetrievalSucceeded

OwnerAuth доверенного платформенного модуля из служб MBAM получен.

### <a name="39-removabledrivemounted"></a>39: RemovableDriveMounted

Съемный диск подключен.

### <a name="40-removabledrivedismounted"></a>40: RemovableDriveDismounted

Съемный диск отключен.

### <a name="41-failedtoenactendpointunreachable"></a>41: FailedToEnactEndpointUnreachable

Не удалось применить политики управления BitLocker к тому из-за сбоя подключения к службе "Восстановление и оборудование" MBAM.

### <a name="42-failedtoenactlockedvolume"></a>42: FailedToEnactLockedVolume

Состояние заблокированного тома не позволило применить политики управления BitLocker к тому.

### <a name="43-transferstatusdatafailedendpointunreachable"></a>43: TransferStatusDataFailedEndpointUnreachable

Не удалось передать данные о состоянии шифрования из-за сбоя подключения к службе "Соответствие и состояние" MBAM.

## <a name="see-also"></a>См. также

Дополнительные сведения об использовании этих журналов см. в статье [Журналы событий BitLocker](about-event-logs.md).

Дополнительные сведения об устранении неполадок см. в разделе [Устранение неполадок BitLocker](troubleshoot.md).
