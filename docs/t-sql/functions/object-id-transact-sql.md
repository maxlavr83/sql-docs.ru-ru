---
title: "Object_id (Transact-SQL) | Документы Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OBJECT_ID
- OBJECT_ID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- objects [SQL Server], IDs
- identification numbers [SQL Server], database objects
- checking object exists
- IDs [SQL Server], database objects
- OBJECT_ID function
- database objects [SQL Server], IDs
- displaying object IDs
- viewing object IDs
- verifying object exists
ms.assetid: f89286db-440f-4218-a828-30881ce3077a
caps.latest.revision: 63
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a612928c3a30b48d3dc8e1dedd4375ca564555d8
ms.contentlocale: ru-ru
ms.lasthandoff: 09/01/2017

---
# <a name="objectid-transact-sql"></a>OBJECT_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Возвращает идентификационный номер объекта базы данных для объекта области схемы.  
  
> [!IMPORTANT]  
>  Запросы на объекты, не относящиеся к области схемы, например триггеры DDL, не могут выполняться с использованием OBJECT_ID. Для объектов, которые не представлены в [sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) представления каталога, следует получить идентификационные номера объектов с помощью запроса соответствующих представлений каталогов. Например, чтобы вернуть идентификационный номер триггера DDL, используйте `SELECT OBJECT_ID FROM sys.triggers WHERE name = 'DatabaseTriggerLog``'`.  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
OBJECT_ID ( '[ database_name . [ schema_name ] . | schema_name . ]   
  object_name' [ ,'object_type' ] )  
```  
  
## <a name="arguments"></a>Аргументы  
 **"** *object_name* **"**  
 Объект, который должен использоваться. *object_name* либо **varchar** или **nvarchar**. Если *object_name* — **varchar**, оно неявно преобразуется в **nvarchar**. Не обязательно указывать имена базы данных и схемы.  
  
 **"** *object_type* **"**  
 Объект области схемы. *object_type* либо **varchar** или **nvarchar**. Если *object_type* — **varchar**, оно неявно преобразуется в **nvarchar**. Список типов объектов см. в разделе **тип** столбца в [sys.objects &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).  
  
## <a name="return-types"></a>Типы возвращаемых значений  
 **int**  
  
## <a name="exceptions"></a>Исключения  
 Для пространственного индекса функция OBJECT_ID возвращает значение NULL.  
  
 В случае ошибки возвращает значение NULL.  
  
 Пользователь может просматривать только метаданные защищаемых объектов, которыми он владеет или на которые пользователю были предоставлены разрешения. Это означает, что встроенные функции, создающие метаданные, такие как OBJECT_ID, могут вернуть значение NULL в случае, если пользователь не имеет разрешений на объект. Дополнительные сведения см. в разделе [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="remarks"></a>Замечания  
 Если параметр системной функции является необязательным, то предполагаются текущие база данных, главный компьютер, пользователь сервера или пользователь базы данных. За встроенными функциями всегда должны следовать круглые скобки.  
  
 Если указано имя временной таблицы, имя базы данных должно идти перед именем временной таблицы, если текущая база данных **tempdb**. Например: `SELECT OBJECT_ID('tempdb..#mytemptable')`.  
  
 Системные функции можно использовать в списке выбора, в предложении WHERE и в любом месте, где разрешается использование выражений. Дополнительные сведения см. в разделе [выражения &#40; Transact-SQL &#41; ](../../t-sql/language-elements/expressions-transact-sql.md) и [ГДЕ &#40; Transact-SQL &#41; ](../../t-sql/queries/where-transact-sql.md).  
  
## <a name="examples"></a>Примеры  
  
### <a name="a-returning-the-object-id-for-a-specified-object"></a>A. Получение идентификатора указанного объекта  
 Следующий пример возвращает идентификатор объекта для таблицы `Production.WorkOrder` в базе данных [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
USE master;  
GO  
SELECT OBJECT_ID(N'AdventureWorks2012.Production.WorkOrder') AS 'Object ID';  
GO  
```  
  
### <a name="b-verifying-that-an-object-exists"></a>Б. Проверка существования объекта  
 Следующий пример проверяет существование указанной таблицы, проверяя наличие у таблицы идентификатора объекта. Если таблица существует, то она удаляется. Если таблица не существует, то инструкция `DROP TABLE` не выполняется.  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID (N'dbo.AWBuildVersion', N'U') IS NOT NULL  
DROP TABLE dbo.AWBuildVersion;  
GO  
```  
  
### <a name="c-using-objectid-to-specify-the-value-of-a-system-function-parameter"></a>В. Использование функции OBJECT_ID для указания параметра системной функции  
 Следующий пример возвращает сведения для всех индексов и секций `Person.Address` в таблицу [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] базы данных с помощью [sys.dm_db_index_operational_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md) функции.  
  
> [!IMPORTANT]  
>  При использовании для возврата значений параметров функций DB_ID и OBJECT_ID языка [!INCLUDE[tsql](../../includes/tsql-md.md)] необходимо убедиться в допустимости возвращаемого идентификатора. Если имя базы данных или объекта не может быть найдено, например если база данных или объект не существуют или неправильно записаны, то обе функции возвратят значение NULL. **Sys.dm_db_index_operational_stats** функция интерпретирует NULL как значение шаблона, указывающего все базы данных или всех объектов. Так как эта операция может быть непреднамеренной, примеры в этом разделе демонстрируют безопасный способ определения идентификаторов базы данных и объекта.  
  
```  
DECLARE @db_id int;  
DECLARE @object_id int;  
SET @db_id = DB_ID(N'AdventureWorks2012');  
SET @object_id = OBJECT_ID(N'AdventureWorks2012.Person.Address');  
IF @db_id IS NULL   
  BEGIN;  
    PRINT N'Invalid database';  
  END;  
ELSE IF @object_id IS NULL  
  BEGIN;  
    PRINT N'Invalid object';  
  END;  
ELSE  
  BEGIN;  
    SELECT * FROM sys.dm_db_index_operational_stats(@db_id, @object_id, NULL, NULL);  
  END;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Примеры: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] и[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-returning-the-object-id-for-a-specified-object"></a>D: идентификатор объекта для заданного объекта, возвращая  
 Следующий пример возвращает идентификатор объекта для таблицы `FactFinance` в базе данных [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)].  
  
```  
SELECT OBJECT_ID(AdventureWorksPDW2012.dbo.FactFinance') AS 'Object ID';  
```  
  
## <a name="see-also"></a>См. также:  
 [Функции метаданных &#40; Transact-SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sys.Objects &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.dm_db_index_operational_stats &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)   
 [OBJECT_DEFINITION (Transact-SQL)](../../t-sql/functions/object-definition-transact-sql.md)   
 [Object_name &#40; Transact-SQL &#41;](../../t-sql/functions/object-name-transact-sql.md)  
  
  

