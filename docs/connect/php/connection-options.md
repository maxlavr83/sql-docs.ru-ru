---
title: "Параметры соединения | Документы Microsoft"
ms.custom: 
ms.date: 07/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6d1ea295-8e34-438e-8468-4bbc0f76192c
caps.latest.revision: 37
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: aadb44954096cbbcb520850a54d4cc2c41911f08
ms.contentlocale: ru-ru
ms.lasthandoff: 09/09/2017

---
# <a name="connection-options"></a>Параметры соединения
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

В этом разделе перечислены параметры, которые допускаются в ассоциативном массиве (при использовании [sqlsrv_connect](../../connect/php/sqlsrv-connect.md) в драйвере SQLSRV) и ключевые слова, которые допускаются в имени источника данных (dsn) (при использовании [PDO::__construct ](../../connect/php/pdo-construct.md) в драйвере PDO_SQLSRV).  

|Key|Значение|Описание|По умолчанию|  
|-------|---------|---------------|-----------|  
|APP|Строковые значения|Указывает имя приложения, используемое для трассировки.|Значение не задано.|  
|ApplicationIntent|Строковые значения|Объявляет тип рабочей нагрузки приложения при соединении с сервером. Возможными значениями являются ReadOnly и ReadWrite.<br /><br />Дополнительные сведения о поддержке [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] для [!INCLUDE[ssHADR](../../includes/sshadr_md.md)]см. в статье [Поддержка высокой доступности и аварийного восстановления в драйвере PHP для SQL Server](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).|ReadWrite|  
|AttachDBFileName|Строковые значения|Указывает, какой файл базы данных сервер должен присоединить.|Значение не задано.|  
|Проверка подлинности|Одна из следующих строк:<br /><br />«SqlPassword»<br /><br />«ActiveDirectoryPassword»|Указывает режим проверки подлинности.|Не задано.|  
|CharacterSet<br /><br />(не поддерживается в драйвере PDO_SQLSRV)|Строковые значения|Задает кодировку, используемую для отправки данных на сервер.<br /><br />Возможными значениями являются SQLSRV_ENC_CHAR и UTF-8. Дополнительные сведения см. в статье [How to: Send and Retrieve UTF-8 Data Using Built-In UTF-8 Support](../../connect/php/how-to-send-and-retrieve-utf-8-data-using-built-in-utf-8-support.md).|SQLSRV_ENC_CHAR|  
|ConnectionPooling|1 или **true** для включения организации пулов соединений.<br /><br />0 или **false** для отключения организации пулов соединений.|Указывает, назначено ли соединение из пула соединений (1 или **true**) или нет (0 или **false**).<sup> 1</sup>|**значение true,** (1)|  
|База данных|Строковые значения|Указывает имя базы данных, используемое для устанавливаемого соединения<sup>2</sup>.|База данных по умолчанию для используемого имени входа.|  
|Шифрование|1 или **true** для включения шифрования.<br /><br />0 или **false** для отключения шифрования.|Указывает, выполняется ли шифрование обмена данными с SQL Server (1 или **true**) или нет (0 или **false**)<sup>3</sup>.|**false** (0)|  
|Failover_Partner|Строковые значения|Указывает сервер и экземпляр зеркала базы данных (если они включены и настроены), используемые при недоступности сервера-источника.<br /><br />На использование Failover_Partner с MultiSubnetFailover налагаются определенные ограничения. Дополнительные сведения см. в статье [Поддержка высокой доступности и аварийного восстановления в драйвере PHP для SQL Server](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).|Значение не задано.|  
|LoginTimeout|Целое число (драйвер SQLSRV)<br /><br />Строка (драйвер PDO_SQLSRV)|Указывает количество секунд ожидания перед неудачным завершением соединения.|Время ожидания отсутствует.|  
|MultipleActiveResultSets|1 или **true** для использования множественных активных результирующих наборов.<br /><br />0 или **false** для отключения множественных активных результирующих наборов.|Отключает или явным образом включает поддержку множественных активных результирующих наборов (MARS).<br /><br />Дополнительные сведения см. в разделе [как: отключение множественных активных результирующих наборов &#40; Режим MARS &#41; ](../../connect/php/how-to-disable-multiple-active-resultsets-mars.md).|true (1)|  
|MultiSubnetFailover|Строковые значения|Всегда указывайте **multiSubnetFailover = yes** при подключении к прослушивателю группы доступности из [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] группы доступности или [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] экземпляра отказоустойчивого кластера. **multiSubnetFailover = yes** настраивает [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] для обеспечения более быстрое обнаружение и подключение к серверу (активного). Возможными значениями являются Yes и No.<br /><br />Дополнительные сведения о поддержке [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] для [!INCLUDE[ssHADR](../../includes/sshadr_md.md)]см. в статье [Поддержка высокой доступности и аварийного восстановления в драйвере PHP для SQL Server](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).|Нет|  
|PWD<br /><br />(не поддерживается в драйвере PDO_SQLSRV)|Строковые значения|Указывает пароль, связанный с Идентификатором пользователя, который будет использоваться при подключении с проверкой подлинности SQL Server<sup>4</sup>.|Значение не задано.|  
|QuotedId|1 или **true** для использования правил SQL-92.<br /><br />0 или **false** для использования устаревших правил.|Указывает, следует ли использовать правила SQL-92 для нестандартных идентификаторов (1 или **true**) или использовать устаревшие правила Transact-SQL (0 или **false**).|**значение true,** (1)|  
|ReturnDatesAsStrings<br /><br />(не поддерживается в драйвере PDO_SQLSRV)|1 или **true** для возврата типов даты и времени в виде строк.<br /><br />0 или **false** для возврата типов даты и времени в виде типов **DateTime** PHP.|Извлекает типы даты и времени (datetime, date, time, datetime2 и datetimeoffset) в виде строк или типов PHP. При использовании драйвера PDO_SQLSRV даты возвращается в виде строк. Драйвер PDO_SQLSRV не содержит **datetime** типа.<br /><br />Дополнительные сведения см. в статье [Практическое руководство. Получение типа даты и времени в виде строк с помощью драйвера SQLSRV](../../connect/php/how-to-retrieve-date-and-time-type-as-strings-using-the-sqlsrv-driver.md).|**false**|  
|Прокручиваемые курсоры|Строковые значения|"Буферизовано" означает, что требуется клиентский (буферизированный) курсор, который позволяет кэшировать весь результирующий набор в памяти. Дополнительные сведения см. в разделе [типы курсоров &#40; Драйвер SQLSRV &#41; ](../../connect/php/cursor-types-sqlsrv-driver.md).|Курсор последовательного доступа|  
|Server<br /><br />(не поддерживается в драйвере SQLSRV)|Строковые значения|Экземпляр [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] для соединения.<br /><br />Вы также можете указать имя виртуальной сети для подключения к группе доступности AlwaysOn. Дополнительные сведения о поддержке [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] для [!INCLUDE[ssHADR](../../includes/sshadr_md.md)]см. в статье [Поддержка высокой доступности и аварийного восстановления в драйвере PHP для SQL Server](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).|Server является обязательным ключевым словом (хотя оно не обязательно должно стоять на первом месте в строке подключения). Если имя сервера не передается в ключевое слово, будет предпринята попытка подключения к локальному экземпляру.<br /><br />Значением, передаваемым в ключевое слово Server, может быть имя экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] или IP-адрес экземпляра. При необходимости можно указать номер порта (например, `sqlsrv:server=(local),1033`).<br /><br />Начиная с версии 3.0 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] , можно также указать экземпляр LocalDB с `server=(localdb)\instancename`. Дополнительные сведения см. в статье [PHP Driver for SQL Server Support for LocalDB](../../connect/php/php-driver-for-sql-server-support-for-localdb.md).|  
|TraceFile|Строковые значения|Указывает путь для файла, используемый для трассировки данных.|Значение не задано.|  
|TraceOn|1 или **true** для включения трассировки.<br /><br />0 или **false** для отключения трассировки.|Указывает, включена ли трассировка ODBC (1 или **true**) или выключен (0 или **false**) для устанавливаемого соединения.|**false** (0)|  
|TransactionIsolation|Драйвер SQLSRV использует следующие значения:<br /><br />SQLSRV_TXN_READ_UNCOMMITTED<br /><br />SQLSRV_TXN_READ_COMMITTED<br /><br />SQLSRV_TXN_REPEATABLE_READ<br /><br />SQLSRV_TXN_SNAPSHOT<br /><br />SQLSRV_TXN_SERIALIZABLE<br /><br />Драйвер PDO_SQLSRV использует следующие значения:<br /><br />PDO::SQLSRV_TXN_READ_UNCOMMITTED<br /><br />PDO::SQLSRV_TXN_READ_COMMITTED<br /><br />PDO::SQLSRV_TXN_REPEATABLE_READ<br /><br />PDO::SQLSRV_TXN_SNAPSHOT<br /><br />PDO::SQLSRV_TXN_SERIALIZABLE|Указывает уровень изоляции транзакции.<br /><br />Дополнительные сведения об изоляции транзакций см. в статье [SET TRANSACTION ISOLATION LEVEL](http://go.microsoft.com/fwlink/?LinkID=191497) в документации по SQL Server.|SQLSRV_TXN_READ_COMMITTED<br /><br />либо<br /><br />PDO::SQLSRV_TXN_READ_COMMITTED|  
|TransparentNetworkIPResolution|**Включить** или **отключено**|Влияет на последовательность соединения при разрешении первый IP-адрес имени узла не отвечает и имеется несколько IP-адресов, связанных с имя узла.<br /><br />Он взаимодействует с MultiSubnetFailover для предоставления другого подключения последовательностей. Дополнительные сведения см. в разделе [с помощью прозрачного разрешение IP-адресов сети](https://docs.microsoft.com/en-us/sql/connect/odbc/using-transparent-network-ip-resolution).|Включено|
|TrustServerCertificate|1 или **true** , чтобы доверять сертификату.<br /><br />0 или **false** , чтобы не доверять сертификату.|Указывает, следует ли клиенту доверять (1 или **true**) или отклонения (0 или **false**) самозаверяющий сертификат сервера.|**false** (0)|  
|UID<br /><br />(не поддерживается в драйвере PDO_SQLSRV)|Строковые значения|Указывает идентификатор пользователя, который будет использоваться при подключении с проверкой подлинности SQL Server<sup>4</sup>.|Значение не задано.|  
|WSID|Строковые значения|Задает имя компьютера для выполнения трассировки.|Значение не задано.|  

1. `ConnectionPooling` Атрибут не может использоваться для включения или отключения организации пулов соединений в Linux и Mac. В разделе [(драйверы Майкрософт для PHP для SQL Server) организации пулов соединений](../../connect/php/connection-pooling-microsoft-drivers-for-php-for-sql-server.md).

2. Все запросы, выполняемые в рамках установленного подключения вносятся в базу данных, который задается параметром *базы данных* атрибута. Тем не менее если пользователь имеет необходимые разрешения, данные в других базах данных может осуществляться с помощью полного имени. Например если *master* база данных настроена с *базы данных* атрибут соединения, существует возможность выполнения запроса Transact-SQL, который обращается к * AdventureWorks.HumanResources.Employee* таблицы, используя полное доменное имя.  

3. Включение *Encryption* может негативно повлиять на производительность некоторых приложений из-за необходимости выполнять дополнительные вычисления для шифрования данных.  

4. Экземпляр *UID* и *PWD* должны быть заданы при соединении с использованием проверки подлинности [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] .  

Многие поддерживаемые ключи являются атрибутами строк подключения ODBC. Дополнительные сведения о строках подключения ODBC см. в статье [Использование ключевых слов строки подключения с SQL Native Client](http://go.microsoft.com/fwlink/?LinkId=105504).  

## <a name="see-also"></a>См. также:  
[Подключение к серверу](../../connect/php/connecting-to-the-server.md)  
