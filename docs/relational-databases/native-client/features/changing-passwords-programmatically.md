---
title: "Смена пароля программным способом | Документы Microsoft"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client|features
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- data access [SQL Server Native Client], password expiration
- SQL Server Native Client ODBC driver, passwords
- SQL Server Native Client OLE DB provider, passwords
- passwords [SQL Server], expiration
- SQLNCLI, password expiration
- expiration [SQL Server Native Client]
- passwords [SQL Server], modifying
- expired passwords [SQL Server Native Client]
- SQL Server Native Client, password expiration
- modifying passwords
ms.assetid: 624ad949-5fed-4ce5-b319-878549f9487b
caps.latest.revision: "36"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5907fb8f99e17de6396adac479213ae9a87cf4d4
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/08/2018
---
# <a name="changing-passwords-programmatically"></a>Смена пароля программным способом
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  В версиях, предшествующих [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], при истечении пароля пользователя переустановить его мог только администратор. Начиная с версии [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client поддерживает обработку истечения срока действия пароля программным способом с помощью обоих [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] поставщика OLE DB для собственного клиента и [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] драйвер ODBC собственного клиента и через изменения в **Имени входа SQL Server** диалоговым окнам.  
  
> [!NOTE]  
>  По возможности следует предлагать пользователям вводить свои учетные данные во время выполнения, избегая их сохранения. Если необходимо сохранить учетные данные, зашифруйте их с помощью [API-интерфейса шифрования Win32](http://go.microsoft.com/fwlink/?LinkId=64532). Дополнительные сведения об использовании паролей см. в разделе [Strong Passwords](../../../relational-databases/security/strong-passwords.md).  
  
## <a name="sql-server-login-error-codes"></a>Коды ошибок имени входа SQL Server  
 Если соединение нельзя установить из-за проблем проверки подлинности, то для диагностики и восстановления приложению будет доступен один из существующих кодов ошибок SQL Server.  
  
|Код ошибки SQL Server|Сообщение об ошибке|  
|---------------------------|-------------------|  
|15113|Ошибка входа пользователя "%. * ls. Причина: не удалось проверить пароль. Учетная запись заблокирована.|  
|18463|Ошибка входа пользователя «%.*ls». Причина: Не удалось изменить пароль. В данный момент этот пароль не может быть использован.|  
|18464|Ошибка входа пользователя «%.*ls». Причина: Не удалось изменить пароль. Пароль слишком короткий и не отвечает требованиям политики.|  
|18465|Ошибка входа пользователя «%.*ls». Причина: Не удалось изменить пароль. Пароль слишком длинный и не отвечает требованиям политики.|  
|18466|Ошибка входа пользователя «%.*ls». Причина: Не удалось изменить пароль. Пароль недостаточно сложный и не отвечает требованиям политики.|  
|18467|Ошибка входа пользователя «%.*ls». Причина: Не удалось изменить пароль. Пароль не отвечает требованиям динамической библиотеки фильтрации паролей.|  
|18468|Ошибка входа пользователя «%.*ls». Причина: Не удалось изменить пароль. В процессе проверки пароля произошла непредвиденная ошибка.|  
|18487|Ошибка входа пользователя «%.*ls». Причина: Пароль учетной записи, истек.|  
|18488|Ошибка входа пользователя «%.*ls». Причина: Необходимо изменить пароль учетной записи.|  
  
## <a name="sql-server-native-client-ole-db-provider"></a>Поставщик OLE DB для собственного клиента SQL Server  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Поставщика OLE DB для собственного клиента поддерживает истечение срока действия пароля, то пользовательский интерфейс и программно.  
  
### <a name="ole-db-user-interface-password-expiration"></a>Пользовательский интерфейс OLE DB для истечения срока действия пароля  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Поставщик OLE DB для собственного клиента поддерживает истечение срока действия пароля через изменения в **имени входа SQL Server** диалоговым окнам. Если свойство DBPROP_INIT_PROMPT установлено в значение DBPROMPT_NOPROMPT, то в случае истечения срока действия пароля попытка начального соединения завершится с ошибкой.  
  
 Если свойство DBPROP_INIT_PROMPT задано любое другое значение, пользователь видит **имени входа SQL Server** диалога, независимо от того, является ли пароля истек. Пользователь может щелкнуть **параметры** кнопку и проверьте **Смена пароля** для изменения пароля.  
  
 Если пользователь нажимает кнопку ОК, и срок действия пароля, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] предлагает пользователю ввести и подтвердить новый пароль с помощью **изменить пароль SQL Server** диалогового окна.  
  
#### <a name="ole-db-prompt-behavior-and-locked-accounts"></a>Поведение подсказки OLE DB и заблокированные учетные записи  
 Попытки соединения могут окончиться неудачей, если учетная запись заблокирована. В этом случае вслед за выводом **имени входа SQL Server** диалоговое окно, для пользователя отображается сообщение об ошибке сервера и попытка соединения отменяется. Оно также может произойти после отображения **изменить пароль SQL Server** диалоговое окно, если пользователь неправильно ввел старый пароль. В этом случае будет выведено то же сообщение об ошибке, а попытка соединения отменяется.  
  
#### <a name="ole-db-connection-pooling-password-expiration-and-locked-accounts"></a>Пул соединений OLE DB, истечение срока действия пароля и заблокированные учетные записи  
 Учетная запись может оказаться заблокированной или может истечь срок действия пароля, в то время как соединение останется активным в пуле соединений. Сервер проверяет наличие паролей с истекшим сроком действия и заблокированных учетных записей в двух случаях. Во-первых, при первоначальном создании соединения. Во-вторых, после восстановления соединения, при получении соединения из пула.  
  
 Если попытка восстановления завершилась неудачно, то соединение удаляется из пула и возвращается ошибка.  
  
### <a name="ole-db-programmatic-password-expiration"></a>Программное истечение срока действия пароля OLE DB  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Поддерживает истечение срока действия пароля через свойства SSPROP_AUTH_OLD_PASSWORD (типа VT_BSTR), который был добавлен в набор свойств DBPROPSET_SQLSERVERDBINIT поставщик OLE DB для собственного клиента.  
  
 Существующее свойство «Password» ссылается на свойство DBPROP_AUTH_PASSWORD и используется для хранения нового пароля.  
  
> [!NOTE]  
>  В строке подключения свойство «Old Password» устанавливает значение свойства SSPROP_AUTH_OLD_PASSWORD, являющееся текущим паролем (возможно, с истекшим сроком действия), недоступным через свойство строки поставщика.  
  
 Поставщик не сохраняет значение этого свойства. Когда это свойство установлено, при первом соединении поставщик не использует пул соединений, поскольку это вызовет новое соединение. Если пароль успешно изменен, текущее соединение нельзя использовать повторно, поскольку оно все еще содержит старый пароль, который будет недопустимым после изменения пароля. Кроме того, при успешном входе поставщик очистит данное свойство. Дальнейшие попытки получения старого пароля вернут значение VT_EMPTY.  
  
> [!NOTE]  
>  Свойство SSPROP_AUTH_OLD_PASSWORD не нужно сохранять, поскольку оно используется только при истечении срока действия пароля.  
  
 Обратите внимание, что при установке свойства «Old Password» поставщик предполагает, что была сделана попытка изменить пароль, если не была также указана проверка подлинности Windows, имеющая приоритет.  
  
 Если используется проверка подлинности Windows, указав старый пароль приведет к DB_E_ERRORSOCCURRED или DB_S_ERRORSOCCURRED в зависимости от того старый пароль был указан как REQUIRED или OPTIONAL соответственно, а значение состояния DBPROPSTATUS_ CONFLICTINGBADVALUE возвращается в *dwStatus*. Это определяется при **IDBInitialize::Initialize** вызывается.  
  
 Если попытка смены пароля завершилась непредвиденной ошибкой, то сервер возвращает код ошибки 18468. Попытка соединения возвращает стандартный код ошибки OLEDB.  
  
 Дополнительные сведения о наборе свойств dbpropset_sqlserverdbinit см. в разделе [свойства инициализации и авторизации](../../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md).  
  
## <a name="sql-server-native-client-odbc-driver"></a>Драйвер ODBC для собственного клиента SQL Server  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Поставщика OLE DB для собственного клиента поддерживает истечение срока действия пароля, то пользовательский интерфейс и программно.  
  
### <a name="odbc-user-interface-password-expiration"></a>Пользовательский интерфейс ODBC истечения срока действия пароля  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Драйвер ODBC для собственного клиента поддерживает истечение срока действия пароля через изменения в **имени входа SQL Server** диалоговым окнам.  
  
 Если [SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md) вызывается и значение **DriverCompletion** имеет значение SQL_DRIVER_NOPROMPT, происходит сбой попытки первоначального соединения, если срок действия пароля. Последующими вызовами возвращаются значение 28000 свойства SQLSTATE и собственное значение кода ошибки 18487 **SQLError** или **SQLGetDiagRec**.  
  
 Если **DriverCompletion** ему было присвоено любое другое значение пользователь видит **имени входа SQL Server** диалога, независимо от того, является ли пароля истек. Пользователь может щелкнуть **параметры** кнопку и проверьте **Смена пароля** для изменения пароля.  
  
 Если пользователь нажимает кнопку ОК, и срок действия пароля, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] предлагает ему ввести и подтвердить новый пароль с помощью **изменить пароль SQL Server** диалогового окна.  
  
#### <a name="odbc-prompt-behavior-and-locked-accounts"></a>Поведение подсказки ODBC и заблокированные учетные записи  
 Попытки соединения могут окончиться неудачей, если учетная запись заблокирована. В этом случае вслед за выводом **имени входа SQL Server** диалоговое окно, для пользователя отображается сообщение об ошибке сервера и попытка соединения отменяется. Оно также может произойти после отображения **изменить пароль SQL Server** диалоговое окно, если пользователь неправильно ввел старый пароль. В этом случае будет выведено то же сообщение об ошибке, а попытка соединения отменяется.  
  
#### <a name="odbc-connection-pooling-password-expiry-and-locked-accounts"></a>Пул соединений ODBC, истечение срока действия пароля и заблокированные учетные записи  
 Учетная запись может оказаться заблокированной или может истечь срок действия пароля, в то время как соединение останется активным в пуле соединений. Сервер проверяет наличие паролей с истекшим сроком действия и заблокированных учетных записей в двух случаях. Во-первых, при первоначальном создании соединения. Во-вторых, после восстановления соединения, при получении соединения из пула.  
  
 Если попытка восстановления завершилась неудачно, то соединение удаляется из пула и возвращается ошибка.  
  
### <a name="odbc-programmatic-password-expiration"></a>Программное истечение срока действия пароля ODBC  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Драйвер ODBC для собственного клиента поддерживает истечение срока действия пароля через Добавление атрибута SQL_COPT_SS_OLDPWD, который устанавливается перед соединением с сервером с использованием [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) функции.  
  
 Атрибут SQL_COPT_SS_OLDPWD дескриптора соединения ссылается на пароль с истекшим сроком действия. Для этого атрибута не существует атрибута строки соединения, поскольку это может повлиять на пул соединений. При успешном входе драйвер очищает этот атрибут.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Драйвер ODBC собственного клиента возвращает SQL_ERROR в четырех случаях для этого компонента: срок действия пароля, конфликт политик пароля, блокировка учетной записи, и установка свойства старого пароля при использовании проверки подлинности Windows. Драйвер возвращает пользователю соответствующие сообщения об ошибках при [SQLGetDiagField](../../../relational-databases/native-client-odbc-api/sqlgetdiagfield.md) вызывается.  
  
## <a name="see-also"></a>См. также:  
 [Компоненты SQL Server Native Client](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  