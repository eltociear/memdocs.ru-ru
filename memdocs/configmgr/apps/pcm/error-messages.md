---
title: Сообщения об ошибках
titleSuffix: Configuration Manager
description: Дополнительные сведения о сообщениях об ошибках из диспетчера преобразования пакетов.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 0d3cf6e1-b295-4b05-821d-e9f57c74ca14
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4d4a2fa66dc1c4a8af3b3f7f16c67d58edebb5fa
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688972"
---
# <a name="technical-reference-for-package-conversion-manager-error-messages"></a>Технический справочник по сообщениям об ошибках диспетчера преобразования пакетов

*Область применения: Configuration Manager (Current Branch)*

<!--1357861-->

В этой статье описываются сообщения об ошибках, отображаемые диспетчером преобразования пакетов. В нее также включены возможные причины ошибок и методы их исправления. Диспетчер преобразования пакетов регистрирует сообщения об ошибках в **PCMTrace.log**. Дополнительные сведения, в том числе о том, как контролировать уровень детализации, см. в разделе [Файлы журнала](troubleshoot-pcm.md#log-files).


#### <a name="application-creation-failed-with-the-following-exception"></a>Сбой создания приложения со следующим исключением

Указанное исключение произошло во время отправки объекта приложения на сервер Configuration Manager.

Проверьте свои разрешения в Configuration Manager и возможности подключения, а затем повторите попытку. Если эти действия не устранят проблему, проверьте файл **PCMtrace.log**  (уровень детализации 4) и **SMSProv.log**.


#### <a name="conversion-error--applies-to-a-package-transform-status"></a>Ошибка преобразования: ПРИМЕНЯЕТСЯ К СОСТОЯНИЮ ПРЕОБРАЗОВАНИЯ ПАКЕТА

Общее исключение произошло во время преобразования пакета. Изучите файл **PCMtrace.log** (уровень детализации 4).

Проверьте разрешения пользователя для сетевой папки (источника данных пакета), проверьте подключение, а затем повторите попытку. Если эти действия не устранят проблему, проверьте файл **PCMtrace.log**  (уровень детализации 4).


#### <a name="did-not-find-a-converted-package-and-its-resultant-application-in-the-workflow-outputs"></a>Преобразованный пакет и его итоговые приложения в выходных данных рабочего процесса не найдены
Приложение (преобразованный пакет или программа) было удалено.

Измените соответствующий пакет или программу, чтобы убедиться, что соответствующий пакет или программа существует.


#### <a name="objects-were-not-created-successfully"></a>Объекты не были успешно созданы
Существует несколько возможных причин.

Проверьте свои разрешения в Configuration Manager и возможности подключения, а затем повторите попытку. Если эти действия не устранят проблему, проверьте файл **PCMtrace.log**  (уровень детализации 4) и файл **SMSProv.log**.


#### <a name="please-close-the-wizard-and-resolve-any-issues-with-the-selected-package-see-pcmtracelog-for-more-details"></a>Закройте мастер и устраните все проблемы с выбранным пакетом. Дополнительные сведения см. в разделе "PCMTrace.Log"
Существует несколько возможных причин.

Проверьте свои разрешения в Configuration Manager и возможности подключения, а затем повторите попытку. Если эти действия не устранят проблему, проверьте файл **PCMtrace.log**  (уровень детализации 4) и файл **SMSProv.log**.


#### <a name="some-deployment-types-are-missing-detection-methods-all-deployment-types-must-have-detection-methods"></a>У некоторых типов развертывания отсутствуют методы обнаружения. Все типы развертывания должны иметь методы обнаружения
Методы обнаружения отсутствуют в программе.

Добавьте один или несколько методов обнаружения во время процесса **исправления и преобразования**.


#### <a name="there-was-an-error-preparing-the-package-for-conversion"></a>Ошибка при подготовке пакета к преобразованию
Существует несколько возможных причин.

Проверьте свои разрешения в Configuration Manager и возможности подключения, а затем повторите попытку. Если эти действия не устранят проблему, проверьте файл **PCMtrace.log**  (уровень детализации 4) и файл **SMSProv.log**.


