---
title: Начало работы с SQL Server (на платформе Linux) в облаке
titleSuffix: SQL Server
description: В этом кратком руководстве показано, как SQL Server под управлением Linux в облаке по своему усмотрению.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 10/25/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux, seodec18
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: 3c64c2ab3927c111b29f0bafa6745fbab2f7fd13
ms.sourcegitcommit: de8ef246a74c935c5098713f14e9dd06c4733713
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2018
ms.locfileid: "53160542"
---
# <a name="quickstart-run-sql-server-in-the-cloud"></a>Краткое руководство. Запуск SQL Server в облаке

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

В этом кратком руководстве вы установите SQL Server на Red Hat Enterprise Linux (RHEL), SUSE Linux Enterprise Server (SLES) или Ubuntu в облаке по своему усмотрению. Запуск SQL Server на Linux в Azure описан здесь: [Подготовка виртуальной машины SQL Server на базе Linux на портале Azure](https://docs.microsoft.com/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json).

> [!NOTE]
> Если вы решили запустить платный выпуск SQL Server, необходимо использовать собственную лицензию (BYOL).

## <a name="amazon-web-services"></a>Amazon Web Services
1.  Создание Linux AMI с помощью по крайней мере 2 ГБ памяти, из marketplace 
    * [RHEL 7.3 +](https://aws.amazon.com/marketplace/pp/B00KWBZVK6)
    * [SLES версии 12 с пакетом обновления 2](https://aws.amazon.com/marketplace/pp/B00PMM99PI)
    * [Ubuntu 16.04](https://aws.amazon.com/marketplace/pp/B01JBL2M0O)
1.  Подключение к AMI с ssh
1.  Выполните быстрый запуск для выбранного дистрибутива Linux. 
    * [RHEL](quickstart-install-connect-red-hat.md)
    * [SLES](quickstart-install-connect-suse.md)
    * [Ubuntu](quickstart-install-connect-ubuntu.md)
1.  Настройка удаленных подключений: 
    * Откройте [консоли Amazon EC2]( https://console.aws.amazon.com/ec2/)
    * В области навигации выберите **группы безопасности**. 
    * Выберите **входящим трафиком, Правка, добавить правило**
    * Добавьте правило входящего трафика, разрешающее прохождение трафика через порт, на котором SQL Server ожидает передачи данных (по умолчанию порт TCP 1433)

    
## <a name="digital-ocean"></a>Digital Ocean
1. Войдите в [панели управления](https://cloud.digitalocean.com/login) и нажмите кнопку Создать дроплет
1. Выберите по крайней мере 2 ГБ памяти дроплет Ubuntu 16.04
1. Подключение к дроплет с ssh
1. Выполните [Ubuntu быстрого запуска](quickstart-install-connect-ubuntu.md)
1. Настройка удаленных подключений:
    * В верхней части панели управления, выполните **сети** ссылку, а затем выберите **брандмауэры**
    * Добавьте правило входящего трафика, разрешающее прохождение трафика через порт, на котором SQL Server ожидает передачи данных (по умолчанию порт TCP 1433)
    
## <a name="google-cloud-platform"></a>Google Cloud Platform
1.  Создание образа Linux с помощью по крайней мере 2 ГБ памяти из средства запуска Cloud 
    * [RHEL 7.3 +](https://console.cloud.google.com/launcher/details/rhel-cloud/rhel-7)
    * [SLES версии 12 с пакетом обновления 2](https://console.cloud.google.com/launcher/details/suse-cloud/sles-12)
    * [Ubuntu 16.04](https://console.cloud.google.com/launcher/details/ubuntu-os-cloud/ubuntu-xenial)
1.  Подключение к образу с помощью ssh
1.  Выполните быстрый запуск для выбранного дистрибутива Linux. 
    * [RHEL](quickstart-install-connect-red-hat.md)
    * [SLES](quickstart-install-connect-suse.md)
    * [Ubuntu](quickstart-install-connect-ubuntu.md)
1.  Настройка удаленных подключений: 
    * Перейдите к [правила брандмауэра](https://console.cloud.google.com/networking/firewalls)
    * Добавьте правило входящего трафика, разрешающее прохождение трафика через порт, прослушиваемый SQL Server (по умолчанию tcp: 1433)
