---
title: "sp_help (Transact-SQL) | Документы Microsoft"
ms.custom: 
ms.date: 10/24/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_help
- sp_help_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_help
ms.assetid: 913cd5d4-39a3-4a4b-a926-75ed32878884
caps.latest.revision: "60"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 4df2325ef2da29b60ca4f1e7109dd73ff9530ea2
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/21/2017
---
# <a name="sphelp-transact-sql"></a>sp_help (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Сообщает сведения об объекте базы данных (любой объект из списка **sys.sysobjects** Просмотр в режиме совместимости), тип данных или определяемый пользователем тип.  
  
 
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
sp_help [ [ @objname = ] 'name' ]  
```  
  
## <a name="arguments"></a>Аргументы  
 [  **@objname=**] **"***имя***"**  
 — Это имя любого объекта в **sysobjects** или любого определяемого пользователем типа данных в **systypes** таблицы. *имя* — **nvarchar (**776**)**, значение по умолчанию NULL. Имена баз данных неприемлемы.  Имена двух или трех частей должен иметь разделители, например «Person.AddressType» или [Person.AddressType].   
   
  
## <a name="return-code-values"></a>Значения кода возврата  
 0 (успешное завершение) или 1 (неуспешное завершение)  
  
## <a name="result-sets"></a>Результирующие наборы  
 Результирующие наборы, возвращаемые зависят ли *имя* будет указано, когда он указан, и это какой объект базы данных.  
  
1.  Если **sp_help** выполняется без аргументов, возвращаются общие сведения об объектах всех типов, которые существуют в текущей базе данных.  
  
    |Имя столбца|Тип данных|Description|  
    |-----------------|---------------|-----------------|  
    |**Название**|**nvarchar (**128**)**|Имя объекта|  
    |**Владелец**|**nvarchar (**128**)**|Владелец объекта (участник базы данных, владеющий объектом, по умолчанию совпадает с владельцем схемы, содержащей объект).|  
    |**Object_type**|**nvarchar (**31**)**|Тип объекта|  
  
2.  Если *имя* — [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] типа данных или определяемый пользователем тип, **sp_help** возвращает следующий результирующий набор.  
  
    |Имя столбца|Тип данных|Description|  
    |-----------------|---------------|-----------------|  
    |**Функция Type_name**|**nvarchar (**128**)**|Имя типа данных.|  
    |**Storage_type**|**nvarchar (**128**)**|Имя типа данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
    |**Длина**|**smallint**|Физическая длина типа данных (в байтах).|  
    |**Prec**|**int**|Точность (общее количество знаков).|  
    |**Масштаб**|**int**|Количество знаков справа от десятичной запятой.|  
    |**Допускает значения NULL**|**varchar (**35**)**|Указывает, допускаются ли значения NULL: Yes или No.|  
    |**Default_name**|**nvarchar (**128**)**|Имя значения по умолчанию, привязанного к этому типу.<br /><br /> NULL = нет привязанного правила по умолчанию.|  
    |**Rule_name**|**nvarchar (**128**)**|Имя правила, привязанного к этому типу.<br /><br /> NULL = нет привязанного правила по умолчанию.|  
    |**Параметры сортировки**|**sysname**|Параметры сортировки для типа данных. Имеет значение NULL для несимвольных типов данных.|  
  
3.  Если *имя* — это любой объект базы данных, кроме типа данных, **sp_help** возвращает этот результирующий задано, а также дополнительные результирующие наборы, в зависимости от типа указанного объекта.  
  
    |Имя столбца|Тип данных|Description|  
    |-----------------|---------------|-----------------|  
    |**Название**|**nvarchar (**128**)**|Имя таблицы|  
    |**Владелец**|**nvarchar (**128**)**|Владелец таблицы|  
    |**Тип**|**nvarchar (**31**)**|Тип таблицы|  
    |**Created_datetime**|**datetime**|Дата создания таблицы|  
  
     В зависимости от объекта базы данных **sp_help** возвращает дополнительные результирующие наборы.  
  
     Если *имя* системной таблице, пользовательской таблицы или представления, **sp_help** возвращает следующие результирующие наборы. Однако результирующий набор, описывающий место расположения файла данных внутри файловой группы, для представления не возвращается.  
  
    -   Дополнительный результирующий набор, возвращаемый для объектов столбца:  
  
        |Имя столбца|Тип данных|Description|  
        |-----------------|---------------|-----------------|  
        |**Column_name**|**nvarchar (**128**)**|Имя столбца.|  
        |**Тип**|**nvarchar (**128**)**|Тип данных столбца.|  
        |**Вычисляемый**|**varchar (**35**)**|Указывает, вычисляются ли значения в столбце: Yes или No.|  
        |**Длина**|**int**|Длина столбца в байтах.<br /><br /> Примечание: Если тип данных столбца является типом больших значений (**varchar(max)**, **nvarchar(max)**, **varbinary(max)**, или **xml**), значение будет отображено значение -1.|  
        |**Prec**|**char (**5**)**|Точность столбца.|  
        |**Масштаб**|**char (**5**)**|Масштаб столбца.|  
        |**Допускает значения NULL**|**varchar (**35**)**|Указывает, допускаются ли значения NULL в столбце: Yes или No.|  
        |**TrimTrailingBlanks**|**varchar (**35**)**|Указывает, усекать ли завершающие пробелы или нет. Возвращает значение Yes или No.|  
        |**FixedLenNullInSource**|**varchar (**35**)**|Только для обратной совместимости.|  
        |**Параметры сортировки**|**sysname**|Параметры сортировки столбца. Имеет значение NULL для несимвольных типов данных.|  
  
    -   Дополнительный результирующий набор, возвращаемый для столбцов идентификаторов:  
  
        |Имя столбца|Тип данных|Description|  
        |-----------------|---------------|-----------------|  
        |**Идентификатор**|**nvarchar (**128**)**|Имя столбца, чей тип данных объявлен удостоверением.|  
        |**Начальное значение**|**numeric**|Стартовое значение для столбца идентификаторов.|  
        |**Приращение**|**numeric**|Шаг прироста, который следует использовать для значений в этом столбце.|  
        |**Не для репликации**|**int**|Свойство IDENTITY не применяется, когда имя входа репликации, таких как **sqlrepl**, вставляет данные в таблицу:<br /><br /> 1 = True<br /><br /> 0 = False.|  
  
    -   Дополнительный результирующий набор, возвращаемый для столбцов:  
  
        |Имя столбца|Тип данных|Description|  
        |-----------------|---------------|-----------------|  
        |**RowGuidCol**|**sysname**|Имя столбца глобального уникального идентификатора.|  
  
    -   Дополнительный результирующий набор, возвращаемый для файловых групп:  
  
        |Имя столбца|Тип данных|Description|  
        |-----------------|---------------|-----------------|  
        |**Data_located_on_filegroup**|**nvarchar (**128**)**|Файловая группа, в которой хранятся данные: основной, дополнительный или журнала транзакций.|  
  
    -   Дополнительный результирующий набор, возвращаемый для индексов:  
  
        |Имя столбца|Тип данных|Description|  
        |-----------------|---------------|-----------------|  
        |**index_name**|**sysname**|Имя индекса.|  
        |**Index_description**|**varchar (**210**)**|Описание индекса.|  
        |**index_keys**|**nvarchar (**2078**)**|Имена столбцов, на основе которых построен индекс. Возвращает значение NULL для оптимизированных для памяти xVelocity индексов columnstore.|  
  
    -   Дополнительный результирующий набор, возвращаемый для ограничений:  
  
        |Имя столбца|Тип данных|Description|  
        |-----------------|---------------|-----------------|  
        |**тип_ограничения**|**nvarchar (**146**)**|Тип ограничения.|  
        |**constraint_name**|**nvarchar (**128**)**|Имя ограничения.|  
        |**delete_action**|**nvarchar (**9**)**|Указывает, является ли действие DELETE: NO_ACTION, CASCADE, SET_NULL, SET_DEFAULT или N/A.<br /><br /> Применимо только для ограничений FOREIGN KEY.|  
        |**update_action**|**nvarchar (**9**)**|Указывает, является ли действие UPDATE: NO_ACTION, CASCADE, SET_NULL, SET_DEFAULT или N/A.<br /><br /> Применимо только для ограничений FOREIGN KEY.|  
        |**status_enabled**|**varchar (**8**)**|Указывает, включено ли ограничение: включено, отключено или н/д.<br /><br /> Применимо только для ограничений CHECK и FOREIGN KEY.|  
        |**status_for_replication**|**varchar (**19**)**|Указывает, предназначено ли ограничение для репликации.<br /><br /> Применимо только для ограничений CHECK и FOREIGN KEY.|  
        |**constraint_keys**|**nvarchar (**2078**)**|Имена столбцов, составляющих ограничение, или, в случае со значениями по умолчанию и правилами, текст, определяющий значение по умолчанию или правило.|  
  
    -   Дополнительный результирующий набор, возвращаемый для ссылочных объектов:  
  
        |Имя столбца|Тип данных|Description|  
        |-----------------|---------------|-----------------|  
        |**Таблицу ссылается**|**nvarchar (**516**)**|Указывает другие объекты базы данных, которые ссылаются на таблицу.|  
  
    -   Дополнительный результирующий набор, возвращаемый для хранимых процедур, функций или расширенных хранимых процедур.  
  
        |Имя столбца|Тип данных|Description|  
        |-----------------|---------------|-----------------|  
        |**Имя_параметра**|**nvarchar (**128**)**|Имя аргумента хранимой процедуры.|  
        |**Тип**|**nvarchar (**128**)**|Тип данных аргумента хранимой процедуры.|  
        |**Длина**|**smallint**|Максимальная физическая длина хранилища, в байтах.|  
        |**Prec**|**int**|Точность или общее количество знаков.|  
        |**Масштаб**|**int**|Число цифр справа от десятичной запятой.|  
        |**Param_order**|**smallint**|Порядок аргумента.|  
  
## <a name="remarks"></a>Замечания  
 **Sp_help** процедура ищет объект только текущей базы данных.  
  
 Когда *имя* не указан, **sp_help** списки имена объектов, владельцев и типы объектов для всех объектов в текущей базе данных. **sp_helptrigger** предоставляет сведения о триггерах.  
  
 **sp_help** предоставляет доступ только к упорядочиваемым столбцам индекса; поэтому она не предоставляет сведения об XML-индексы или Пространственные индексы.  
  
## <a name="permissions"></a>Permissions  
 Необходимо быть членом роли **public** . Пользователь должен иметь по крайней мере одно разрешение *objname*. Чтобы просмотреть ключи, значения по умолчанию или правила ограничения для столбца, необходимо обладать разрешением VIEW DEFINITION для этой таблицы.  
  
## <a name="examples"></a>Примеры  
  
### <a name="a-returning-information-about-all-objects"></a>A. Возвращение сведений обо всех объектах  
 В нижеследующем примере приводится информация о каждом объекте в базе данных `master`.  
  
```  
USE master;  
GO  
EXEC sp_help;  
GO  
```  
  
### <a name="b-returning-information-about-a-single-object"></a>Б. Возвращение сведений об отдельном объекте  
 В нижеследующем примере отображаются сведения о таблице `Person`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_help 'Person.Person';  
GO  
```  
  
## <a name="see-also"></a>См. также:  
 [Компонент Database Engine хранимой процедуры &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sp_helpindex &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpindex-transact-sql.md)   
 [sp_helprotect &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helprotect-transact-sql.md)   
 [sp_helpserver (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [sp_helptrigger (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helptrigger-transact-sql.md)   
 [sp_helpuser &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)   
 [Системные хранимые процедуры (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.sysobjects &#40; Transact-SQL &#41;](../../relational-databases/system-compatibility-views/sys-sysobjects-transact-sql.md)  
  
  