---
title: "Функция SQLGetDiagField | Документы Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLGetDiagField
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetDiagField
helpviewer_keywords:
- SQLGetDiagField function [ODBC]
ms.assetid: 1dbc4398-97a8-4585-bb77-1f7ea75e24c4
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0cd8f64eb18fc6e1fb456b03ef65ef2dc33cc140
ms.contentlocale: ru-ru
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgetdiagfield-function"></a>Функция SQLGetDiagField
**Соответствия**  
 Появился в версии: ODBC 3.0 нормативных требований: ISO-92  
  
 **Сводка**  
 **SQLGetDiagField** возвращает текущее значение поля записи диагностических данных структуры (связанной с указанным дескриптором), содержащий сведения об ошибках, предупреждения и состояние.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
SQLRETURN SQLGetDiagField(  
     SQLSMALLINT     HandleType,  
     SQLHANDLE       Handle,  
     SQLSMALLINT     RecNumber,  
     SQLSMALLINT     DiagIdentifier,  
     SQLPOINTER      DiagInfoPtr,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   StringLengthPtr);  
```  
  
## <a name="arguments"></a>Аргументы  
 *HandleType*  
 [Вход] Идентификатор типа дескриптора, описывающий тип дескриптора, для которого требуются диагностики. Должна быть одной из следующих:  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   ЗНАЧЕНИЕ SQL_HANDLE_STMT  
  
 Дескриптор SQL_HANDLE_DBC_INFO_TOKEN используется только для диспетчера драйверов и драйверов. Приложения не должны использовать этот тип дескриптора. Дополнительные сведения о SQL_HANDLE_DBC_INFO_TOKEN см. в разделе [разработке пула соединений, поддерживающие драйвер ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).  
  
 *Дескриптор*  
 [Вход] Дескриптор для структуры диагностических данных, тип, указанный *HandleType*. Если *HandleType* — SQL_HANDLE_ENV, *обработки* может быть общим или дескриптор среды с монопольным доступом.  
  
 *RecNumber*  
 [Вход] Указывает состояние записи, из которой приложение ищет сведения. Состояние записи нумеруются от 1. Если *DiagIdentifier* аргумент указывает любое поле заголовка диагностики *RecNumber* учитывается. В противном случае он должен быть больше 0.  
  
 *DiagIdentifier*  
 [Вход] Указывает поле, значение которого является возвращаемых диагностики. Дополнительные сведения см. в разделе «*DiagIdentifier* аргумент» раздела «Примечания».  
  
 *DiagInfoPtr*  
 [Выход] Указатель на буфер, в котором для возвращения диагностических сведений. Тип данных зависит от значения *DiagIdentifier*. Если *DiagInfoPtr* имеет тип integer, приложения должны использовать буфер SQLULEN и инициализации, значение 0, перед вызовом этой функции, как некоторые драйверы могут только записи в нижнем 32-разрядной или 16-разрядное буфера и оставить высшего порядка бит без изменений.  
  
 Если *DiagInfoPtr* имеет значение NULL, *StringLengthPtr* по-прежнему возвращает общее количество байтов (за исключением знака конечное значение null для символьных данных) для возврата в буфере, на который указывает * DiagInfoPtr*.  
  
 *BufferLength*  
 [Вход] Если *DiagIdentifier* является диагностики, определенных для ODBC и *DiagInfoPtr* указывает на строку символов или двоичных буфера, данный аргумент должен иметь длину \* *DiagInfoPtr *. Если *DiagIdentifier* представляет собой поле, определенных для ODBC и \* *DiagInfoPtr* является целым числом, *BufferLength* учитывается. Если значение в * \*DiagInfoPtr* строка в Юникоде (при вызове **SQLGetDiagFieldW**), *BufferLength* аргумент должен быть четным числом.  
  
 Если *DiagIdentifier* является полем, определяемым драйвером, приложение сможет определить природу поля для диспетчера драйверов, задав *BufferLength* аргумент. *BufferLength* может иметь следующие значения:  
  
-   Если *DiagInfoPtr* — это указатель на строку знаков *BufferLength* длина строки или SQL_NTS.  
  
-   Если *DiagInfoPtr* является указатель на буфер двоичных разрядов приложения результатом SQL_LEN_BINARY_ATTR (*длина*) макрос в *BufferLength*. В этом случае отрицательное значение в *BufferLength*.  
  
-   Если *DiagInfoPtr* — это указатель на значение, отличное от строки символов или двоичная строка *BufferLength* должно иметь значение SQL_IS_POINTER.  
  
-   Если * \*DiagInfoPtr* содержит тип данных фиксированной длины, *BufferLength* — SQL_IS_INTEGER, SQL_IS_UINTEGER, SQL_IS_SMALLINT или SQL_IS_USMALLINT, соответствующим образом.  
  
 *StringLengthPtr*  
 [Выход] Указатель на буфер, в который возвращается общее количество байтов (за исключением число байтов, необходимых для знака завершения null) для возврата в \* *DiagInfoPtr*, для символьных данных. Если количество байтов, доступных для возврата больше или равно *BufferLength*, текст в \* *DiagInfoPtr* усекается до *BufferLength* минус Длина символа конечное значение null.  
  
## <a name="returns"></a>Возвращает  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE или значение SQL_NO_DATA.  
  
## <a name="diagnostics"></a>Диагностика  
 **SQLGetDiagField** не публикует диагностические записи для себя. Он использует следующие возвращаемые значения для оповещения результат собственный выполнения:  
  
-   SQL_SUCCESS: Функция успешно возвращен диагностические сведения.  
  
-   SQL_SUCCESS_WITH_INFO: \* *DiagInfoPtr* слишком мал для хранения запрошенного диагностические поля. Таким образом данные в поле диагностики были усечены. Чтобы определить, что возникло усечение, приложение необходимо сравнить *BufferLength* фактическое число доступных байтов, записываемые в **StringLengthPtr*.  
  
-   SQL_INVALID_HANDLE: Дескриптор обозначается *HandleType* и *обработки* не является допустимым дескриптором.  
  
-   Значение SQL_ERROR: Произошло одно из следующих:  
  
    -   *DiagIdentifier* аргумент не является одним из допустимых значений.  
  
    -   *DiagIdentifier* аргумент был SQL_DIAG_CURSOR_ROW_COUNT, SQL_DIAG_DYNAMIC_FUNCTION, SQL_DIAG_DYNAMIC_FUNCTION_CODE или SQL_DIAG_ROW_COUNT, но *обработки* не дескриптора инструкции. (Диспетчер драйверов возвращает это диагностики.)  
  
    -   *RecNumber* аргумент был меньше или равно 0 при *DiagIdentifier* указано поле из диагностическую запись. *RecNumber* учитывается для поля заголовка.  
  
    -   Значения, запрошенного был строку символов и *BufferLength* меньше нуля.  
  
    -   При использовании асинхронного уведомления, асинхронные операции для дескриптора не завершена.  
  
-   Значение SQL_NO_DATA: *RecNumber* превышает количество диагностических записей, которые существовали для дескриптор, указанный в *обработки.* Функция также возвращает значение SQL_NO_DATA любой положительные *RecNumber* Если нет диагностических записей для *обработки*.  
  
## <a name="comments"></a>Комментарии  
 Приложение обычно вызывает **SQLGetDiagField** для выполнения одной из трех целей:  
  
1.  Чтобы получить конкретную ошибку или предупреждение при вызове функции вернул значение SQL_ERROR или SQL_SUCCESS_WITH_INFO (или SQL_NEED_DATA для **SQLBrowseConnect** функции).  
  
2.  Чтобы определить количество строк в источнике данных, затронутых при операции обновления, удаления или вставки были выполнены с помощью вызова **SQLExecute**, **SQLExecDirect**, ** SQLBulkOperations**, или **SQLSetPos** (из SQL_DIAG_ROW_COUNT поле заголовка), или требуется определить количество строк, которые существуют в текущем открытого курсора, если драйвер может предоставить эти сведения (из Поле заголовка SQL_DIAG_CURSOR_ROW_COUNT).  
  
3.  Чтобы определить, какая функция была выполнена с помощью вызова **SQLExecDirect** или **SQLExecute** (из поля заголовка SQL_DIAG_DYNAMIC_FUNCTION и SQL_DIAG_DYNAMIC_FUNCTION_CODE).  
  
 Любая функция ODBC можно разместить ноль или более записей диагностики каждый раз, что он вызывается, поэтому приложение может вызвать **SQLGetDiagField** после любого вызова функции ODBC. Не ограничено число диагностических записях, которые могут храниться в любой момент времени. **SQLGetDiagField** получает диагностические сведения, недавно связанные со структурой диагностических данных, указанной в *обработки* аргумент. Если приложение вызывает функцию ODBC, отличных от **SQLGetDiagField** или **SQLGetDiagRec**, теряются все диагностические сведения из предыдущего вызова с тем же дескриптором.  
  
 Приложение может сканировать все диагностические записи путем увеличения или уменьшения *RecNumber*, при условии, что **SQLGetDiagField** возвращает SQL_SUCCESS. Число записей состояния отображается в поле заголовка SQL_DIAG_NUMBER. Вызовы **SQLGetDiagField** являются обратимыми полей заголовка и записи. Приложение может вызвать **SQLGetDiagField** попытку позднее, для извлечения полей из записи, до тех пор, пока не был вызван до этого времени будет разместить записей на тот же дескриптор функции, отличные от диагностических функций.  
  
 Приложение может вызвать **SQLGetDiagField** для возврата любого диагностические поля в любое время, за исключением SQL_DIAG_CURSOR_ROW_COUNT или SQL_DIAG_ROW_COUNT, который вернет значение SQL_ERROR, если *обработки* не Дескриптор инструкции. Если другие диагностические поля не определен, вызов **SQLGetDiagField** возвращает SQL_SUCCESS (при условии других Диагностика не обнаруживается) и в поле возвращается неопределенное значение.  
  
 Дополнительные сведения см. в разделе [с помощью SQLGetDiagRec и SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md) и [реализации SQLGetDiagRec и SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md).  
  
 Вызов API-Интерфейс, отличном от того, которое выполняется асинхронно создаст HY010 «Функция ошибка последовательности». Однако не удалось получить запись об ошибке, до завершения асинхронной операции.  
  
## <a name="handletype-argument"></a>Аргумент HandleType  
 Каждый тип дескриптора может иметь диагностические сведения, связанные с ним. *HandleType* аргумент указывает тип дескриптора *обработки*.  
  
 Некоторые поля заголовка и записи не может быть предоставлен среды, подключения, инструкции и дескриптора дескрипторов. Эти дескрипторы, для которых поле не применимо, отображаются в следующих разделах «Заголовок полей» и «запись».  
  
 Если *HandleType* — SQL_HANDLE_ENV, *обработки* может быть маркер общего или отменен общий доступ к среде.  
  
 Нет заголовок специфические для драйвера диагностические поля должен быть связан с дескриптор среды.  
  
 Поля только для диагностики заголовка, которые определены для дескриптора: SQL_DIAG_NUMBER и SQL_DIAG_RETURNCODE.  
  
## <a name="diagidentifier-argument"></a>Аргумент DiagIdentifier  
 Этот аргумент указывает идентификатор поля, необходимые в структуре диагностических данных. Если *RecNumber* больше или равно 1, данные в поле Описание диагностических сведений, возвращаемых функцией. Если *RecNumber* равно 0, поле находится в заголовке структуры диагностических данных и поэтому содержит данные, относящиеся к вызову функции, возвращены диагностических сведений, не определенные сведения.  
  
 Драйверы можно определить заголовок драйвера и поля записей в структуре диагностических данных.  
  
 ODBC 3*.x* приложения, работа с ODBC 2*.x* драйвер будет вызывать **SQLGetDiagField** только с *DiagIdentifier* Аргумент SQL_DIAG_CLASS_ORIGIN, SQL_DIAG_CLASS_SUBCLASS_ORIGIN, SQL_DIAG_CONNECTION_NAME, SQL_DIAG_MESSAGE_TEXT, SQL_DIAG_NATIVE, SQL_DIAG_NUMBER, SQL_DIAG_RETURNCODE, SQL_DIAG_SERVER_NAME или SQL_DIAG_SQLSTATE. Все диагностические поля вернет значение SQL_ERROR.  
  
## <a name="header-fields"></a>Поля заголовка  
 Поля заголовка, перечисленные в следующей таблице может быть включено в *DiagIdentifier* аргумент.  
  
|DiagIdentifier|Возвращаемый тип|Возвращает|  
|--------------------|-----------------|-------------|  
|SQL_DIAG_CURSOR_ROW_COUNT|SQLLEN|Это поле содержит количество строк в курсоре. Его семантика зависит от **SQLGetInfo** типы информации, SQL_DYNAMIC_CURSOR_ATTRIBUTES2, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2, SQL_KEYSET_CURSOR_ATTRIBUTES2 и SQL_STATIC_CURSOR_ATTRIBUTES2, которые указывают, что количество строк, доступны для каждого типа курсора (в битах SQL_CA2_CRC_EXACT и SQL_CA2_CRC_APPROXIMATE).<br /><br /> Содержимое этого поля определяется только для дескриптора инструкции и только после **SQLExecute**, **SQLExecDirect**, или **SQLMoreResults** был вызван. Вызов **SQLGetDiagField** с *DiagIdentifier* из SQL_DIAG_CURSOR_ROW_COUNT на отличный от инструкции дескриптор вернет значение SQL_ERROR.|  
|SQL_DIAG_DYNAMIC_FUNCTION|SQLCHAR *|Это строка, описывающая инструкции SQL, которая выполняется базовой функции. (Для определенных значений см. в «Значения полей динамической функции» далее в этом разделе.) Содержимое этого поля определяется только для дескриптора инструкции и только после вызова **SQLExecute**, **SQLExecDirect**, или **SQLMoreResults**. Вызов **SQLGetDiagField** с *DiagIdentifier* из SQL_DIAG_DYNAMIC_FUNCTION на отличный от инструкции дескриптор вернет значение SQL_ERROR. Значение этого поля не определено до вызова **SQLExecute** или **SQLExecDirect**.|  
|SQL_DIAG_DYNAMIC_FUNCTION_CODE|SQLINTEGER|Это числовой код, описывающий инструкции SQL, которая была выполнена с помощью базовой функции. (Для конкретного значения см. в «Значения из динамических функция Fields,» далее в этом разделе.) Содержимое этого поля определяется только для дескриптора инструкции и только после вызова **SQLExecute**, **SQLExecDirect**, или **SQLMoreResults**. Вызов **SQLGetDiagField** с *DiagIdentifier* из SQL_DIAG_DYNAMIC_FUNCTION_CODE на отличный от инструкции дескриптор вернет значение SQL_ERROR. Значение этого поля не определено до вызова **SQLExecute** или **SQLExecDirect**.|  
|SQL_DIAG_NUMBER|SQLINTEGER|Число записей состояния, доступные для указанного дескриптора.|  
|SQL_DIAG_RETURNCODE|SQLRETURN|Код возврата, возвращаемых функцией. Список кодов возврата см. в разделе [коды возврата](../../../odbc/reference/develop-app/return-codes-odbc.md). Драйвер не должен реализовывать SQL_DIAG_RETURNCODE; он всегда реализуется с помощью диспетчера драйверов. Если ни одна из функций еще был вызван для *обработки*, для SQL_DIAG_RETURNCODE возвращается значение SQL_SUCCESS.|  
|SQL_DIAG_ROW_COUNT|SQLLEN|Число строк, затронутых инструкцией insert, delete или update, выполненных **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, или **SQLSetPos**. , Определяемым драйвером после *курсора спецификации* был выполнен. Содержимое этого поля определяется только для дескриптора инструкции. Вызов **SQLGetDiagField** с *DiagIdentifier* из SQL_DIAG_ROW_COUNT на отличный от инструкции дескриптор вернет значение SQL_ERROR. Данные в это поле также возвращается в *RowCountPtr* аргумент **SQLRowCount**. Данные в этом поле сбрасывается после каждого вызова функции nondiagnostic, в то время как возвращаемый счетчик строк **SQLRowCount** остается неизменным, пока инструкция снова установить значение состояния подготовленный и выделенный.|  
  
## <a name="record-fields"></a>Поля записей  
 Поля записей, перечисленных в следующей таблице может быть включено в *DiagIdentifier* аргумент.  
  
|DiagIdentifier|Возвращаемый тип|Возвращает|  
|--------------------|-----------------|-------------|  
|SQL_DIAG_CLASS_ORIGIN|SQLCHAR *|Строка, указывающая документ, который определяет класс часть значение SQLSTATE в этой записи. Его значение равно «ISO 9075» для всех SQLSTATE определяется Open Group и интерфейс уровня вызова ISO. Для конкретного ODBC SQLSTATE (все языки, класс которого SQLSTATE — «Обмена мгновенными Сообщениями»), его значение равно «ODBC 3.0".|  
|SQL_DIAG_COLUMN_NUMBER|SQLINTEGER|Если поле SQL_DIAG_ROW_NUMBER число допустимую строку в набор строк или набор параметров, это поле содержит значение, представляющее номер столбца в результирующем наборе или номер параметра в набор параметров. Номера всегда начинаются с 1; столбец результирующего набора Если эта запись состояния относится столбца закладки, это поле может быть нулевой. Параметр нумерация начинается с 1. Он имеет значение SQL_NO_COLUMN_NUMBER, если запись состояния не связан с номер столбца или параметра с номером. Если драйвер не может определить номер столбца или параметра номер, связанный с этой записью, это поле имеет значение SQL_COLUMN_NUMBER_UNKNOWN.<br /><br /> Содержимое этого поля определяется только для дескриптора инструкции.|  
|SQL_DIAG_CONNECTION_NAME|SQLCHAR *|Строка, указывающая имя соединения, который связывает диагностическая запись с. Это поле доступно, определяемым драйвером. Структуры диагностических данных, связанной с дескриптором среды и диагностические сведения, не связаны с любого соединения это поле является строка нулевой длины.|  
|SQL_DIAG_MESSAGE_TEXT|SQLCHAR *|Информационное сообщение в случае ошибки или предупреждения. Это поле имеет формат, как описано в [диагностические сообщения](../../../odbc/reference/develop-app/diagnostic-messages.md). Нет без ограничения длины текста диагностические сообщения.|  
|SQL_DIAG_NATIVE|SQLINTEGER|Драйвер или данные, определяемые источником машинный код ошибки. Если нет машинный код ошибки, драйвер возвращает 0.|  
|SQL_DIAG_ROW_NUMBER|SQLLEN|Это поле содержит номер строки в наборе строк, или номер параметра в наборе параметров, с которыми связана запись состояния. Номера строк и номера параметров начинаются с 1. Это поле имеет значение SQL_NO_ROW_NUMBER, если эта запись состояния не связан с номер строки или номер параметра. Если драйвер не может определить количество строк или параметр с номером, с которой связана эта запись, это поле имеет значение SQL_ROW_NUMBER_UNKNOWN.<br /><br /> Содержимое этого поля определяется только для дескриптора инструкции.|  
|SQL_DIAG_SERVER_NAME|SQLCHAR *|Строка, указывающая имя сервера, к которому относится диагностической записью. Это то же, что значение, возвращаемое при вызове **SQLGetInfo** с параметром SQL_DATA_SOURCE_NAME. Для структур диагностических данных, связанной с дескриптором среды и диагностики, которые связаны с любого сервера это поле является строка нулевой длины.|  
|SQL_DIAG_SQLSTATE|SQLCHAR *|Код диагностики Пятисимвольный SQLSTATE. Дополнительные сведения см. в разделе [SQLSTATE](../../../odbc/reference/develop-app/sqlstates.md).|  
|SQL_DIAG_SUBCLASS_ORIGIN|SQLCHAR *|Строка с такой же формат и допустимые значения как SQL_DIAG_CLASS_ORIGIN, обозначающее определение часть подкласс части код SQLSTATE. Следующие атрибуты конкретного ODBC SQLSTATE, для которых возвращается «ODBC 3.0».<br /><br /> 01S00 01S01, 01S02, 01S06, 01S07, 07S01, 08S01, 21S01, 21S02, 25S01, 25S02, 25S03, 42S01, 42S02, 42S11, 42S12, 42S21, 42S22, HY095, HY097, HY098, HY099, HY100, HY101, HY105, HY107, HY109, HY110, HY111, HYT00, HYT01, IM001, IM002, IM003, IM004, IM005, IM006, IM007, IM008, IM010, IM011, IM012.|  
  
## <a name="values-of-the-dynamic-function-fields"></a>Значения полей динамической функции  
 В следующей таблице описаны значения SQL_DIAG_DYNAMIC_FUNCTION и SQL_DIAG_DYNAMIC_FUNCTION_CODE, применяемые к каждому типу выполняемой инструкции SQL с помощью вызова **SQLExecute** или **SQLExecDirect**. Драйвер можно добавлять определяемые драйвером значений в них.  
  
|Инструкция SQL<br /><br /> выполняется|Значение<br /><br /> SQL_DIAG_DYNAMIC_FUNCTION|Значение<br /><br /> SQL_DIAG_DYNAMIC_FUNCTION_CODE|  
|--------------------------------|-----------------------------------------------|-----------------------------------------------------|  
|*ALTER домена оператор*|«ALTER ДОМЕНА»|SQL_DIAG_ALTER_DOMAIN|  
|*Таблица инструкции ALTER*|«ALTER TABLE»|SQL_DIAG_ALTER_TABLE|  
|*Определение проверочного утверждения*|«СОЗДАНИЕ УТВЕРЖДЕНИЯ»|SQL_DIAG_CREATE_ASSERTION|  
|*Определение для набора символов*|«СОЗДАНИЕ НАБОРА СИМВОЛОВ»|SQL_DIAG_CREATE_CHARACTER_SET|  
|*Определение параметров сортировки*|«СОЗДАНИЕ ПАРАМЕТРОВ СОРТИРОВКИ»|SQL_DIAG_CREATE_COLLATION|  
|*Создание индекса оператор-*|«СОЗДАНИЕ ИНДЕКСА»|SQL_DIAG_CREATE_INDEX|  
|*Инструкция CREATE table*|«СОЗДАНИЕ ТАБЛИЦЫ»|SQL_DIAG_CREATE_TABLE|  
|*Создание представление оператор*|«СОЗДАНИЕ ПРЕДСТАВЛЕНИЯ»|SQL_DIAG_CREATE_VIEW|  
|*спецификацией курсора*|«SELECT КУРСОРА»|SQL_DIAG_SELECT_CURSOR|  
|*положение инструкции DELETE*|«DELETE ДИНАМИЧЕСКОГО КУРСОРА»|SQL_DIAG_DYNAMIC_DELETE_CURSOR|  
|*Поиск DELETE оператор*|«DELETE WHERE»|SQL_DIAG_DELETE_WHERE|  
n-определение *|«СОЗДАНИЕ ДОМЕНА»|SQL_DIAG_CREATE_DOMAIN|  
|*инструкции DROP утверждения*|«DROP УТВЕРЖДЕНИЯ»|SQL_DIAG_DROP_ASSERTION|  
|*DROP символ набор stmt*|«DROP КОДИРОВКА»|SQL_DIAG_DROP_CHARACTER_SET|  
|*инструкции DROP — параметры сортировки*|«DROP ПАРАМЕТРЫ СОРТИРОВКИ»|SQL_DIAG_DROP_COLLATION|  
|*инструкции DROP домена*|«DROP ДОМЕНА»|SQL_DIAG_DROP_DOMAIN|  
|*инструкции DROP индекс*|«DROP INDEX»|SQL_DIAG_DROP_INDEX|  
|*инструкции DROP схемы*|«DROP SCHEMA»|SQL_DIAG_DROP_SCHEMA|  
|*инструкции DROP таблица*|«DROP TABLE»|SQL_DIAG_DROP_TABLE|  
|*инструкции DROP преобразования*|«DROP ПРЕОБРАЗОВАНИЯ»|SQL_DIAG_DROP_TRANSLATION|  
|*инструкции DROP представление*|«DROP VIEW»|SQL_DIAG_DROP_VIEW|  
— оператор *|«GRANT»|SQL_DIAG_GRANT|  
|*инструкции INSERT*|«ВСТАВКА»|SQL_DIAG_INSERT|  
|*Модуль ODBC-процедуры*|«CALL»|ВЫЗОВ SQL_DIAG_|  
|*Инструкция REVOKE*|«ОТМЕНЫ»|SQL_DIAG_REVOKE|  
|*Определение схемы*|«СОЗДАНИЕ СХЕМЫ»|SQL_DIAG_CREATE_SCHEMA|  
|*определения перевода*|«СОЗДАНИЕ ПРЕОБРАЗОВАНИЯ»|SQL_DIAG_CREATE_TRANSLATION|  
|*Обновление располагается инструкции*|«ДИНАМИЧЕСКОЕ ОБНОВЛЕНИЕ КУРСОРА»|SQL_DIAG_DYNAMIC_UPDATE_CURSOR|  
|*Поиск обновления оператор*|«ОБНОВЛЕНИЕ WHERE»|SQL_DIAG_UPDATE_WHERE|  
|Неизвестно|*пустая строка*|SQL_DIAG_UNKNOWN_STATEMENT|  
  
## <a name="sequence-of-status-records"></a>Последовательность записей состояния  
 Состояние записи располагаются в последовательности, на основе номера строки и тип диагностики. Диспетчер драйверов определяет окончательный порядок, в котором для возвращения состояния записи, которые создает. Драйвер определяет окончательный порядок, в котором для возвращения состояния записи, которые создает.  
  
 Если диагностические записи учитываются, диспетчер драйверов и драйвер, диспетчер драйверов отвечает за их упорядочивание.  
  
 Если две или более записей состояния, последовательность записей сначала определяется по номеру строки. Для определения последовательности диагностических записей по строкам применяются следующие правила:  
  
-   Записи, которые не соответствуют любой строке отображаться перед записей, которые соответствуют конкретной строки, поскольку SQL_NO_ROW_NUMBER определен равным – 1.  
  
-   Записи, для которых имеет неизвестный номер строки отображаться перед других записей, так как SQL_ROW_NUMBER_UNKNOWN определяется как – 2.  
  
-   Для всех записей, которые относятся к определенной строки записи сортируются по значению в поле SQL_DIAG_ROW_NUMBER. Перечислены все ошибки и предупреждения из первой строки, затронутой и затем все ошибки и предупреждения следующей строки затронутых и т. д.  
  
> [!NOTE]  
>  ODBC 3*.x* диспетчер драйверов не упорядочивает записи состояния в очереди диагностики при SQLSTATE 01S01 (ошибка в строке) возвращается ODBC 2*.x* драйвера или если SQLSTATE 01S01 (ошибка в строке), возвращенный ODBC 3*.x* драйвера при **SQLExtendedFetch** вызывается или **SQLSetPos** будет вызван на курсор, расположенных с **SQLExtendedFetch **.  
  
 В каждой строке, а также тех записей, которые не соответствуют в строку или для которого неизвестен номер строки или для всех этих записей с номером строки, равное SQL_NO_ROW_NUMBER первая запись в списке, определяется с помощью набора правила сортировки. После первой записи не определен порядок записей, влияющих на строки. Приложение нельзя предполагать, что ошибки предшествовать предупреждения после первой записи. Приложения следует проверить структуры завершения диагностических данных для получения полной информации о неудачного вызова функции.  
  
 Следующие правила используются для определения первой записи в строке. Запись с высшего ранга является первой записью. Источник записи (диспетчера драйверов, драйвер, шлюза и т. д.) не учитываются при ранжирование записей.  
  
-   **Ошибки** состояние записи, описывающие ошибки имеют высшего ранга. Для сортировки ошибок применяются следующие правила:  
  
    -   Записи, которые указывают на сбой транзакции или ошибка возможные транзакции outrank все записи.  
  
    -   Если две или более записей описать аналогичное условие ошибки, SQLSTATE, определенных в спецификации Open CLI группы (классы 03 через ГЦ) outrank SQLSTATE, определяемые ODBC и драйвером.  
  
-   **Значения данных нет определенных реализацией** состояние записи, которые описывают значения определяемые драйвером нет данных (класс 02) имеют второй высшего ранга.  
  
-   **Предупреждения** низким рангом имеют состояние записи, описывающие предупреждения (класс 01). Если же условие предупреждения, затем предупреждение SQLSTATE, определенных в спецификации Open CLI группы описаны две или более записей outrank SQLSTATE, определенных для ODBC и определяемым драйвером.  
  
## <a name="related-functions"></a>Связанные функции  
  
|Сведения о|См.|  
|---------------------------|---------|  
|Получение нескольких полей структуры диагностических данных|[Функция SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|  
  
## <a name="see-also"></a>См. также:  
 [Справочник по API-интерфейса ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Файлы заголовков ODBC](../../../odbc/reference/install/odbc-header-files.md)