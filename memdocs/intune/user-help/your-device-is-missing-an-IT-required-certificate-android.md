---
title: На устройстве отсутствует сертификат | Документация Майкрософт
description: ''
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 07/29/2019
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: f0ba4cbb-ef0a-4335-86bf-f1d006867fa2
searchScope:
- User help
ROBOTS: ''
ms.reviewer: arnab
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 1cd3309ebe05d48fd2b28988ffc09702901c470a
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/27/2020
ms.locfileid: "83881063"
---
# <a name="install-missing-certificate-required-by-your-organization"></a>Установка отсутствующего сертификата, необходимого для вашей организации  

Если устройство не зарегистрировано в Intune и на нем отсутствует требуемый сертификат, вы не сможете войти в приложение "Корпоративный портал". При попытке войти вы увидите следующее сообщение:

![screenshot-error-message-about-missing-certificate](./media/andr-cert_install-1-cert_missing.png)

Существует два варианта, которыми можно воспользоваться для загрузки необходимого сертификата и регистрации устройства. 

- Включите доступ в браузере в приложении корпоративного портала.
- Определите отсутствующий сертификат, просмотрев сертификаты на компьютере компании или учебном компьютере. Затем выполните поиск в Интернете, чтобы скачать необходимый сертификат. 

Сначала выполните действия по включению доступа в браузере. После этого, если по-прежнему не удается зарегистрировать устройство, выполните действия по его поиску в Интернете. 

## <a name="enable-browser-access"></a>Разрешение доступа в браузере
Выполните следующие действия, чтобы включить доступ в браузере. После включения доступа корпоративный портал установит соответствующий сертификат и продолжит регистрацию.    

1. Выберите меню в правом углу в приложении корпоративного портала.  
2. Выберите **Параметры**.  
3. Рядом с пунктом **Включить доступ в браузере** выберите **Включить**.  
4. На экране "Администратор устройства" выберите **АКТИВИРОВАТЬ**. 

## <a name="identify-and-download-the-missing-certificate-through-web-search"></a>Обнаружение и скачивание отсутствующего сертификата с помощью поиска в Интернете
Выполните следующие действия, чтобы вручную найти и установить сертификат на устройство.  

1. На компьютере откройте Internet Explorer. Если у вас нет компьютера, обратитесь в службу поддержки вашей компании. Контактные данные службы поддержки доступны на [веб-сайте корпоративного портала](https://go.microsoft.com/fwlink/?linkid=2010980).

2. Перейдите на [веб-сайт корпоративного портала](https://go.microsoft.com/fwlink/?linkid=2010980) и войдите на портал, используя рабочие или учебные учетные данные.

3. Справа от адресной строки браузера щелкните символ в виде замка, как показано на снимке экрана ниже.

    ![screenshot-internet-explorer-address-bar-padlock-symbol](./media/andr-missing-cert-ie-padlock-symbol.png)

    Если вы не видите его, остановитесь и обратитесь в службу поддержки вашей компании. Символ в виде замка означает, что выполнен безопасный вход. Поэтому не следует продолжать работу, если он не отображается.

4. Щелкните **Просмотр сертификатов**.

    ![screenshot-internet-explorer-view-certificates-button-on-website-identification-dialog](./media/andr-missg-cert-ie-view-cert-button.png)

5. Перейдите на вкладку **Путь сертификации** и укажите сертификат, который необходимо получить из Интернета. Имя нужного сертификата будет находиться там же, где находится выделенное имя на примере снимка экрана выше.

6. Найдите имя отсутствующего сертификата, определенного в предыдущем разделе, используя поисковую систему, например Bing или Google. У сертификата могут быть различные расширения, например CRT, PEM и т. п.

7. Скачайте корневой сертификат с веб-сайта.

8. После скачивания сертификата перетяните верхнюю панель вниз, чтобы открыть уведомления, а затем выберите имя сертификата в списке уведомлений.

4. В диалоговом окне **Имя сертификата**, показанном на снимке экрана ниже, примите имя сертификата по умолчанию.

5. Убедитесь, что для параметра **Credential Use** (Использование учетных данных) задано значение **Used for VPN and apps** (Использовать для VPN и приложений), и нажмите кнопку **ОК**.

    ![screenshot-certificate-name-dialog-showing-certificate-name](./media/andr-missing-cert-cert-name.png)

6. Закройте приложение корпоративного портала.

7. Снова откройте приложение корпоративного портала. Теперь вы сможете войти в приложение корпоративного портала. Если вам нужна помощь, обратитесь в службу поддержки вашей компании.

Если вы видите сообщение об отсутствующем сертификате, которое показано выше, но уже выполнили описанную здесь процедуру, вероятно, необходим другой сертификат, для установки которого нужна помощь службы поддержки вашей компании. Если вам нужна помощь, обратитесь в службу поддержки вашей компании, используя контактные данные на [веб-сайте корпоративного портала](https://go.microsoft.com/fwlink/?linkid=2010980).

## <a name="next-steps"></a>Дальнейшие шаги  

По-прежнему нужна помощь? Обратитесь в службу поддержки вашей компании. Его контактные данные доступны на [веб-сайте корпоративного портала](https://go.microsoft.com/fwlink/?linkid=2010980).  
