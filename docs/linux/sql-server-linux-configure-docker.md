---
title: "Параметры конфигурации для 2017 г. SQL Server на Docker | Документы Microsoft"
description: "Возможность использования различных способов использования и взаимодействия с образами контейнеров 2017 г. SQL Server в Docker. Это включает сохранение, копирование файлов и устранения неполадок."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 07/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 82737f18-f5d6-4dce-a255-688889fdde69
ms.custom: H1Hack27Feb2017
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: f87c28e4d2ba7689d422ccf2f1a903765a39f27a
ms.contentlocale: ru-ru
ms.lasthandoff: 08/02/2017

---
# <a name="configure-sql-server-2017-container-images-on-docker"></a>Настройка образов контейнеров 2017 г. SQL Server на Docker

В этом разделе объясняется, как настроить и использовать [образ контейнера mssql-server-linux](https://hub.docker.com/r/microsoft/mssql-server-linux/) с помощью Docker. Этот образ состоит из SQL Server на основании Ubuntu 16.04 Linux. Он может использоваться с подсистемой Dосker 1.8 + на Linux или Docker для Mac и Windows.

> [!NOTE]
> В этом разделе особое внимание уделяется с помощью образа mssql-server-linux. Непокрытые образа Windows, но Дополнительные сведения о нем на [Docker Hub страница windows для сервера mssql](https://hub.docker.com/r/microsoft/mssql-server-windows/).

## <a name="pull-and-run-the-container-image"></a>По запросу, а затем запускать образ контейнера

Для извлечения и запустить образ контейнера Docker для 2017 г. SQL Server, выполните необходимые условия и действия в следующем краткого руководства.

- [Запускать образ контейнера 2017 г. SQL Server с помощью Docker](quickstart-install-connect-docker.md)

В этом разделе конфигурации предоставляет дополнительное подключение и сценарии использования в следующих разделах.

## <a name="connect-and-query"></a>Подключения и запроса

Можно подключиться и запросов SQL Server в контейнере с либо вне контейнера или в контейнере. В следующих разделах объясняется оба сценария. 

### <a name="tools-outside-the-container"></a>Средства вне контейнера

Можно соединиться с экземпляром SQL Server на компьютере Docker с помощью любого внешнего средства macOS, Windows или Linux, поддерживающее подключения SQL. Некоторые общие средства включают:

- [программа sqlcmd](sql-server-linux-setup-tools.md)
- [Код Visual Studio](sql-server-linux-develop-use-vscode.md)
- [SQL Server Management Studio (SSMS) в Windows](sql-server-linux-develop-use-ssms.md)

В следующем примере используется **sqlcmd** для подключения к SQL Server, запущенный в контейнер Docker. IP-адреса в строке подключения является IP-адрес компьютера, на котором выполняется контейнера.

```bash
sqlcmd -S 10.3.2.4 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4 -U SA -P "<YourPassword>"
```

Порт узла, который не был по умолчанию был сопоставлен **1433**, добавьте этот порт в строке подключения. Например, если вы указали `-p 1400:1433` в вашей `docker run` команды, а затем соедините с явным образом указать порт 1400.

```bash
sqlcmd -S 10.3.2.4,1400 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4,1400 -U SA -P "<YourPassword>"
```

### <a name="tools-inside-the-container"></a>Средства внутри контейнера

Начиная с SQL Server 2017 г CTP 2.0 [средства командной строки SQL Server](sql-server-linux-setup-tools.md) включаются в образе контейнера. При присоединении к образу с интерактивной командной строки средства можно выполнять локально.

1. Используйте `docker exec -it` команду, чтобы запустить интерактивный bash оболочки внутри вашей запущенного контейнера. В следующем примере `e69e056c702d` — это идентификатор контейнера.

    ```bash
    docker exec -it e69e056c702d "bash"
    ```

    > [!TIP]
    > Не всегда необходимо указывать идентификатор весь контейнер. Необходимо указать достаточно символов, для его однозначной идентификации. Поэтому в этом примере может быть достаточно, чтобы использовать `e6` или `e69` вместо полного идентификатора.

2. Один раз внутри контейнера, подключите локально с помощью sqlcmd. Обратите внимание, что sqlcmd не в пути по умолчанию, поэтому необходимо указать полный путь.

    ```bash
    /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P '<YourPassword>'
    ```

3. После завершения работы с sqlcmd, введите `exit`.

4. После завершения работы с интерактивной командной строки, введите `exit`. Контейнер продолжается после выхода из оболочки интерактивный bash.

## <a name="run-multiple-sql-server-containers"></a>Запустите несколько контейнеров SQL Server

Docker обеспечивает возможность запуска несколько контейнеров SQL Server на том же компьютере узла. Этот подход для сценариев, требующих несколько экземпляров SQL Server на том же узле. Каждый контейнер должен предоставлять сам на другой порт.

В следующем примере создаются два контейнера SQL Server и сопоставляет их с порты **1401** и **1402** на хост-компьютере.

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' --cap-add SYS_PTRACE -p 1401:1433 -d microsoft/mssql-server-linux
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' --cap-add SYS_PTRACE -p 1402:1433 -d microsoft/mssql-server-linux
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" --cap-add SYS_PTRACE -p 1401:1433 -d microsoft/mssql-server-linux
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" --cap-add SYS_PTRACE -p 1402:1433 -d microsoft/mssql-server-linux
```

Теперь имеются два экземпляра SQL Server, запущенный в отдельные контейнеры. Клиенты могут подключаться к каждому экземпляру SQL Server с помощью IP-адрес узла Docker и номер порта для контейнера.

```bash
sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
sqlcmd -S 10.3.2.4,1402 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
sqlcmd -S 10.3.2.4,1402 -U SA -P "<YourPassword>"
```

## <a id="persist"></a>Сохранить данные

Изменения конфигурации SQL Server и файлы базы данных сохраняются в контейнере даже при перезагрузке контейнер с `docker stop` и `docker start`. Однако если удалить контейнер с `docker rm`, все данные в контейнере удаляются, включая SQL Server и баз данных. Следующий раздел объясняет, как использовать **тома данных** для сохранения файла базы данных, даже если удалены связанные контейнеры.

> [!IMPORTANT]
> Для SQL Server очень важно понимать сохранение данных в Docker. Помимо обсуждения в этом разделе, в документации Docker на [управление данными в контейнерах Docker](https://docs.docker.com/engine/tutorials/dockervolumes/).

### <a name="mount-a-host-directory-as-data-volume"></a>Подключить узел каталога в качестве тома данных

Первый параметр — подключение к каталогу на узле в качестве тома данных в контейнере. Чтобы сделать это, используйте `docker run` с `-v <host directory>:/var/opt/mssql` флаг. Это позволяет данные для восстановления между выполнениями контейнера.

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' --cap-add SYS_PTRACE -p 1433:1433 -v <host directory>:/var/opt/mssql -d microsoft/mssql-server-linux
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" --cap-add SYS_PTRACE -p 1433:1433 -v <host directory>:/var/opt/mssql -d microsoft/mssql-server-linux
```

Этот метод дает возможность совместного использования и просматривать файлы на узле за пределами Docker.

> [!IMPORTANT]
> Сопоставление тома узла для Docker на Mac с SQL Server на образе Linux в настоящее время не поддерживается. Вместо этого используйте контейнеры томов данных. Это ограничение относится только к `/var/opt/msql` каталога. Чтение из подключенного каталога работает нормально. Например можно подключить узла каталога, с ключом-v на Mac и восстановление резервной копии из BAK-файл, который находится на узле.

### <a name="use-data-volume-containers"></a>Используйте контейнеры томов данных

Второй вариант — использовать контейнер томов данных. Можно создать контейнер томов данных, указав имя тома вместо каталог узла с `-v` параметра. В следующем примере создается общего тома данных с именем **sqlvolume**.

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' --cap-add SYS_PTRACE -p 1433:1433 -v sqlvolume:/var/opt/mssql -d microsoft/mssql-server-linux
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" --cap-add SYS_PTRACE -p 1433:1433 -v sqlvolume:/var/opt/mssql -d microsoft/mssql-server-linux
```

> [!NOTE]
> Этот метод для выполнения команды неявно создания тома данных не работает с более ранними версиями Docker. В этом случае использовать явную шаги, описанные в документации Docker [Создание и подключение контейнера томов данных](https://docs.docker.com/engine/tutorials/dockervolumes/#creating-and-mounting-a-data-volume-container).

Даже в том случае, если остановить и удалить этот контейнер, тома данных не будет устранена. Вы можете просмотреть ее с `docker volume ls` команды.

```bash
docker volume ls
```

При создании другой контейнер с тем же именем тома новый контейнер использует те же данные SQL Server, находящиеся на томе.

Чтобы удалить контейнер томов данных, используйте `docker volume rm` команды.

> [!WARNING]
> При удалении контейнера томов данных, все данные SQL Server, в контейнере, *окончательно* удалены.

### <a name="backup-and-restore"></a>Резервное копирование и восстановление
Помимо этих методов контейнера можно также использовать стандартные резервного копирования SQL Server и восстановить методы. Файлы резервных копий можно использовать для защиты данных или перемещения данных на другой экземпляр SQL Server. Дополнительные сведения см. в разделе [резервное копирование и восстановление баз данных SQL Server в Linux](sql-server-linux-backup-and-restore-database.md).

> [!WARNING]
> При создании резервных копий, убедитесь, что для создания или копирования файлов резервной копии вне контейнера. В противном случае при удалении контейнера также удаляются файлы резервной копии.

## <a name="execute-commands-in-a-container"></a>Выполнение команд в контейнер

При наличии запущенного контейнера из узла терминалов позволяет выполнять команды в контейнере.

Чтобы получить идентификатор контейнера запуска:

```bash
docker ps
```

Чтобы запустить bash, терминалов в контейнере запуска:

```bash
docker exec -ti <Container ID> /bin/bash
```

Теперь можно выполнить команды, как если бы, если вы используете их терминалов внутри контейнера. По завершении введите `exit`. Это завершает работу во время сеанса интерактивной командой, но продолжает выполняться контейнера.

## <a name="copy-files-from-a-container"></a>Скопируйте файлы из контейнера

Чтобы скопировать файл из контейнера, используйте следующую команду:

```bash
docker cp <Container ID>:<Container path> <host path>
```

**Пример:**

```bash
docker cp d6b75213ef80:/var/opt/mssql/log/errorlog /tmp/errorlog
```

```PowerShell
docker cp d6b75213ef80:/var/opt/mssql/log/errorlog C:\Temp\errorlog
```

Чтобы скопировать файл в контейнер, используйте следующую команду:

```bash
docker cp <Host path> <Container ID>:<Container path>
```

**Пример:**

```bash
docker cp /tmp/mydb.mdf d6b75213ef80:/var/opt/mssql/data
```

```PowerShell
docker cp C:\Temp\mydb.mdf d6b75213ef80:/var/opt/mssql/data
```

## <a name="upgrade-sql-server-in-containers"></a>Обновление SQL Server в контейнерах

Чтобы обновить образ контейнера с помощью Docker, извлечь последнюю версию из реестра. Используйте `docker pull` команды:

```bash
docker pull microsoft/mssql-server-linux:latest
```

Это обновляет образ SQL Server для любой новые контейнеры, создаваемые вами, но не обновляет SQL Server в все запущенные контейнеры. Для этого необходимо создать новый контейнер в образе контейнера последнюю SQL Server и перенести данные в этот новый контейнер.

1. Во-первых, убедитесь, что вы используете один из [методы сохраняемости данных](#persist) для существующего контейнера SQL Server.

2. Остановка SQL Server контейнер с `docker stop` команды.

3. Создать новый контейнер SQL Server с `docker run` и указать каталог сопоставленных узла или контейнер томов данных. Новый контейнер теперь использует новую версию SQL Server с помощью существующих данных SQL Server.

4. Проверка баз данных и данных в новый контейнер.

5. При необходимости удалите старый контейнер с `docker rm`.

## <a id="troubleshooting"></a>Устранение неполадок

В следующих разделах содержатся сведения об устранении неполадок для запуска SQL Server в контейнерах.

### <a name="docker-command-errors"></a>Ошибки команды docker

Если возникли ошибки для любой `docker` команды, убедитесь, что запущена служба docker и попробуйте выполнить с повышенными разрешениями.

Например, в Linux, может появиться следующая ошибка при выполнении `docker` команды:

```
Cannot connect to the Docker daemon. Is the docker daemon running on this host?
```

Если эта ошибка появляется в Linux, попытайтесь выполнить те же команды, предваряемые фразой `sudo`. В случае неудачи, проверьте, запущена служба docker и запустить его при необходимости.

```bash
sudo systemctl status docker
sudo systemctl start docker
```

В Windows убедитесь, что вы выполняете запуск PowerShell или в командной строке с правами администратора.

### <a name="sql-server-container-startup-errors"></a>Ошибки при запуске контейнера SQL Server

Если контейнер SQL Server не запускается, выполните следующие проверки.

- Если появляется сообщение об ошибке, таких как **"не удалось создать конечную точку CONTAINER_NAME сетевой мост. Ошибка при запуске прокси-сервера: привязка 0.0.0.0:1433 прослушивания tcp: адрес уже используется. "** , а затем пытаетесь сопоставление контейнера порта 1433 порт, который уже используется. Это может произойти, если вы используете SQL Server локально на хост-компьютере. Он также может произойти, если запустить два контейнера SQL Server и сопоставьте их оба на один и тот же порт узла. В этом случае используйте `-p` параметр для сопоставления портов другой узел контейнера порт 1433. Например: 

    ```bash
    docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' --cap-add SYS_PTRACE -p 1400:1433 -d microsoft/mssql-server-linux`.
    ```

    ```PowerShell
    docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" --cap-add SYS_PTRACE -p 1400:1433 -d microsoft/mssql-server-linux`.
    ```

- Проверьте, есть ли сообщения об ошибках из контейнера.

    ```bash
    docker logs e69e056c702d
    ```

- Убедитесь, что выполняются минимальные требования памяти и диска, указанное в [требования](#requirements) этого раздела.

- Если вы используете программное обеспечение управления контейнера, убедитесь, что он поддерживает контейнера процессы, выполняющиеся как корневой. Процесс sqlservr в контейнере работает как корень.

- Просмотрите [SQL Server программа установки и журналы ошибок](#errorlogs).

### <a name="sql-server-connection-failures"></a>Сбоев соединений SQL Server

Если не удается подключиться к экземпляру SQL Server, запускается в контейнере, выполните следующие проверки.

- Убедитесь, что контейнер SQL Server запущена, просмотрев **состояние** столбец `docker ps -a` выходных данных. В противном случае используйте `docker start <Container ID>` для его запуска.

- При сопоставлении узла нестандартный порт (не 1433), убедитесь, что порт указываются в строке подключения. Вы увидите сопоставление порта на **ПОРТЫ** столбец `docker ps -a` выходных данных. Например следующая команда выполняет подключение sqlcmd в контейнер, который прослушивает порт 1401:

    ```bash
    sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
    ```

    ```PowerShell
    sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
    ```

- Если вы использовали `docker run` с существующие тома сопоставленных данных или контейнер томов данных, SQL Server игнорирует значение `MSSQL_SA_PASSWORD`. Вместо этого используется предварительно настроенный пароль пользователя SA, из данных SQL Server в том или данных контейнера томов данных. Убедитесь, что вы используете пароль SA, связанные с данными, которые вы присоединения.

- Просмотрите [SQL Server программа установки и журналы ошибок](#errorlogs).

### <a name="sql-server-availability-groups"></a>Группы доступности SQL Server

При использовании Docker с группами доступности SQL Server существует два дополнительных требований.

- Сопоставление порта, который используется для связи реплика (по умолчанию 5022). Например, указать `-p 5022:5022` как часть вашего `docker run` команды.

- Явно задать имя узла контейнера с `-h YOURHOSTNAME` параметр `docker run` команды. Это имя узла используется при настройке группы доступности. Если не указать его с `-h`, по умолчанию используется идентификатор контейнера.

### <a id="errorlogs"></a>SQL Server программа установки и журналы ошибок

Вы можете просмотреть программы установки SQL Server и журналы ошибок **/var/opt/mssql/log**. Если контейнер не запущена, сначала запустите контейнер. Затем используйте интерактивной командной строки, чтобы просмотреть журналы.

```bash
docker start e69e056c702d
docker exec -it e69e056c702d "bash"
```

Из сеанса bash внутри контейнера выполните следующие команды:

```bash
cd /var/opt/mssql/log
cat setup*.log
cat errorlog
```

> [!TIP]
> Если подключить каталога сервера **/var/opt/mssql** при создании контейнера, вместо этого можно осуществлять **журнала** подкаталог на сопоставленном путь на узле.

## <a name="next-steps"></a>Следующие шаги

Начало работы с образами контейнеров 2017 г. SQL Server на Docker через [краткого руководства](quickstart-install-connect-docker.md).

См. также, [mssql docker репозитории GitHub](https://github.com/Microsoft/mssql-docker) ресурсы, отзывы и известные проблемы.
