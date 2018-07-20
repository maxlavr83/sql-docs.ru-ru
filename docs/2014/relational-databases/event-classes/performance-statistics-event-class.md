---
title: Класс событий Performance Statistics | Документация Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Performance Statistics event class
ms.assetid: da9cd2c4-6fdd-4ada-b74f-105e3541393c
caps.latest.revision: 32
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4d0191085ac2a294d1dce8a30b9292a1cd7cf8ab
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2018
ms.locfileid: "37171175"
---
# <a name="performance-statistics-event-class"></a>Performance Statistics, класс событий
  Класс событий Performance Statistics можно использовать для наблюдения за производительностью выполняемых запросов, хранимых процедур и триггеров. Каждый из шести подклассов событий обозначает событие, относящееся ко времени существования запросов, хранимых процедур и триггеров в системе. Сочетая эти подклассы событий и связанные с ними динамические административные представления sys.dm_exec_query_stats, sys.dm_exec_procedure_stats и sys.dm_exec_trigger_stats, можно восстановить историю производительности любого заданного запроса, хранимой процедуры или триггера.  
  
## <a name="performance-statistics-event-class-data-columns"></a>Столбцы данных класса событий Performance Statistics  
 Следующие таблицы описывают столбцы данных класса событий, связанные с каждым из следующих подклассов событий: EventSubClass 0, EventSubClass 1,EventSubClass 2,EventSubClass 3, EventSubClass 4 и EventSubClass 5.  
  
### <a name="eventsubclass-0"></a>EventSubClass 0  
  
|Имя столбца данных|Тип данных|Описание|Идентификатор столбца|Фильтруемый|  
|----------------------|---------------|-----------------|---------------|----------------|  
|BigintData1|`bigint`|NULL|52|Да|  
|BinaryData|`image`|NULL|2|Да|  
|DatabaseID|`int`|Идентификатор базы данных, указанной в инструкции USE *database* , или базы данных по умолчанию, если для данного экземпляра инструкция USE *database* не выполнялась. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] отображает имя базы данных, если столбец данных ServerName захвачен при трассировке и сервер доступен. Определите значение для базы данных, используя функцию DB_ID.|3|Да|  
|EventSequence|`int`|Последовательность данного события в запросе.|51|Нет|  
|EventSubClass|`int`|Тип подкласса события.<br /><br /> 0 = Новый текст пакета SQL, который пока отсутствует в кэше.<br /><br /> Следующие типы EventSubClass создаются в трассировке для нерегламентированных пакетов.<br /><br /> Для нерегламентированных пакетов, состоящих из *n* запросов.<br /><br /> 1 типа 0|21|Да|  
|IntegerData2|`int`|NULL|55|Да|  
|ObjectID|`int`|NULL|22|Да|  
|Offset|`int`|NULL|61|Да|  
|PlanHandle|`Image`|NULL|65|Да|  
|SessionLoginName|`nvarchar`|Имя входа пользователя, создавшего этот сеанс. Например, при соединении с [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] под именем Login1 и при выполнении инструкции под именем Login2 SessionLoginName будет содержать значение Login1, а LoginName — значение Login2. В этом столбце отображаются как имена входа [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , так и имена входа Windows.|64|Да|  
|SPID|`int`|Идентификатор сеанса, в котором произошло событие.|12|Да|  
|SqlHandle|`image`|Дескриптор SQL, который можно использовать для получения текста SQL пакета с помощью динамического административного представления sys.dm_exec_sql_text.|63|Да|  
|StartTime|`datetime`|Время начала события, если оно известно.|14|Да|  
|TextData|`ntext`|Текст пакета SQL.|1|Да|  
  
### <a name="eventsubclass-1"></a>EventSubClass 1  
  
|Имя столбца данных|Тип данных|Описание|Идентификатор столбца|Фильтруемый|  
|----------------------|---------------|-----------------|---------------|----------------|  
|BigintData1|`bigint`|Совокупное количество повторных компиляций данного плана.|52|Да|  
|BinaryData|`image`|Двоичный XML скомпилированного плана.|2|Да|  
|DatabaseID|`int`|Идентификатор базы данных, указанной в инструкции USE *database* , или базы данных по умолчанию, если для данного экземпляра инструкция USE *database* не выполнялась. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] отображает имя базы данных, если столбец данных ServerName захвачен при трассировке и сервер доступен. Определите значение для базы данных, используя функцию DB_ID.|3|Да|  
|EventSequence|`int`|Последовательность данного события в запросе.|51|Нет|  
|SessionLoginName|`nvarchar`|Имя входа пользователя, создавшего этот сеанс. Например, при соединении с [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] под именем Login1 и при выполнении инструкции под именем Login2 SessionLoginName будет содержать значение Login1, а LoginName — значение Login2. В этом столбце отображаются как имена входа [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , так и имена входа Windows.|64|Да|  
|EventSubClass|`int`|Тип подкласса события.<br /><br /> 1 = Скомпилированы запросы в хранимой процедуре.<br /><br /> Следующие типы EventSubClass создаются в трассировке для хранимых процедур.<br /><br /> Для хранимых процедур, состоящих из *n* запросов.<br /><br /> *n* типа 1|21|Да|  
|IntegerData2|`int`|Конечное смещение инструкции в хранимой процедуре:<br /><br /> -1 для конечного смещения хранимой процедуры.|55|Да|  
|ObjectID|`int`|Идентификатор объекта, назначенный системой.|22|Да|  
|Offset|`int`|Начальное смещение инструкции в пределах хранимой процедуры или пакета.|61|Да|  
|SPID|`int`|Идентификатор сеанса, в котором произошло событие.|12|Да|  
|SqlHandle|`image`|Дескриптор SQL, который можно использовать для получения текста SQL хранимой процедуры с помощью динамического административного представления dm_exec_sql_text.|63|Да|  
|StartTime|`datetime`|Время начала события, если оно известно.|14|Да|  
|TextData|`ntext`|NULL|1|Да|  
|PlanHandle|`image`|Дескриптор скомпилированного плана для хранимой процедуры. Может быть использован для получения плана XML с помощью динамического административного представления sys.dm_exec_query_plan.|65|Да|  
|ObjectType|`int`|Значение, представляющее тип объекта, связанного с событием.<br /><br /> 8272 = хранимая процедура|28|Да|  
|BigintData2|`bigint`|Общий объем памяти в килобайтах, используемой во время компиляции.|53|Да|  
|ЦП|`int`|Общее процессорное время в миллисекундах, затраченное на компиляцию.|18|Да|  
|Продолжительность|`int`|Общее время в микросекундах, затраченное на компиляцию.|13|Да|  
|IntegerData|`int`|Размер скомпилированного плана в килобайтах.|25|Да|  
  
### <a name="eventsubclass-2"></a>EventSubClass 2  
  
|Имя столбца данных|Тип данных|Описание|Идентификатор столбца|Фильтруемый|  
|----------------------|---------------|-----------------|---------------|----------------|  
|BigintData1|`bigint`|Совокупное количество повторных компиляций данного плана.|52|Да|  
|BinaryData|`image`|Двоичный XML скомпилированного плана.|2|Да|  
|DatabaseID|`int`|Идентификатор базы данных, указанной в инструкции USE *database* , или базы данных по умолчанию, если для данного экземпляра инструкция USE *database* не выполнялась. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] отображает имя базы данных, если столбец данных ServerName захвачен при трассировке и сервер доступен. Определите значение для базы данных, используя функцию DB_ID.|3|Да|  
|EventSequence|`int`|Последовательность данного события в запросе.|51|Нет|  
|SessionLoginName|`nvarchar`|Имя входа пользователя, создавшего этот сеанс. Например, при соединении с [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] под именем Login1 и при выполнении инструкции под именем Login2 SessionLoginName будет содержать значение Login1, а LoginName — значение Login2. В этом столбце отображаются как имена входа [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , так и имена входа Windows.|64|Да|  
|EventSubClass|`int`|Тип подкласса события.<br /><br /> 2 = Скомпилированы запросы в нерегламентированной инструкции SQL.<br /><br /> Следующие типы EventSubClass создаются в трассировке для нерегламентированных пакетов.<br /><br /> Для нерегламентированных пакетов, состоящих из *n* запросов.<br /><br /> *n* типа 2|21|Да|  
|IntegerData2|`int`|Конечное смещение инструкции в пакете:<br /><br /> -1 для конечного смещения пакета.|55|Да|  
|ObjectID|`int`|Недоступно|22|Да|  
|Offset|`int`|Начальное смещение инструкции в пределах пакета.<br /><br /> 0 для начального смещения пакета.|61|Да|  
|SPID|`int`|Идентификатор сеанса, в котором произошло событие.|12|Да|  
|SqlHandle|`image`|Дескриптор SQL. Может быть использован для получения текста SQL пакета с помощью динамического административного представления dm_exec_sql_text.|63|Да|  
|StartTime|`datetime`|Время начала события, если оно известно.|14|Да|  
|TextData|`ntext`|NULL|1|Да|  
|PlanHandle|`image`|Дескриптор скомпилированного плана для пакета. Может быть использован для получения плана XML пакета с помощью динамического административного представления dm_exec_query_plan.|65|Да|  
|BigintData2|`bigint`|Общий объем памяти в килобайтах, используемой во время компиляции.|53|Да|  
|ЦП|`int`|Общее время ЦП в микросекундах, затраченное на компиляцию.|18|Да|  
|Duration|`int`|Общее время в миллисекундах, затраченное на компиляцию.|13|Да|  
|IntegerData|`int`|Размер скомпилированного плана в килобайтах.|25|Да|  
  
### <a name="eventsubclass-3"></a>EventSubClass 3  
  
|Имя столбца данных|Тип данных|Описание|Идентификатор столбца|Фильтруемый|  
|----------------------|---------------|-----------------|---------------|----------------|  
|BigintData1|`bigint`|Совокупное количество повторных компиляций данного плана.|52|Да|  
|BinaryData|`image`|NULL|2|Да|  
|DatabaseID|`int`|Идентификатор базы данных, указанной в инструкции USE *database* , или базы данных по умолчанию, если для данного экземпляра инструкция USE *database* не выполнялась. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] отображает имя базы данных, если столбец данных ServerName захвачен при трассировке и сервер доступен. Определите значение для базы данных, используя функцию DB_ID.|3|Да|  
|EventSequence|`int`|Последовательность данного события в запросе.|51|Нет|  
|SessionLoginName|`nvarchar`|Имя входа пользователя, создавшего этот сеанс. Например, при соединении с [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] под именем Login1 и при выполнении инструкции под именем Login2 SessionLoginName будет содержать значение Login1, а LoginName — значение Login2. В этом столбце отображаются как имена входа [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , так и имена входа Windows.|64|Да|  
|EventSubClass|`int`|Тип подкласса события.<br /><br /> 3 = Запрос удален из кэша, и данные предыстории производительности этого плана тоже будут уничтожены.<br /><br /> Следующие типы EventSubClass формируются при трассировке.<br /><br /> Для нерегламентированных пакетов, состоящих из *n* запросов.<br /><br /> 1 типа 3, когда запрос сброшен из кэша.<br /><br /> Для хранимых процедур, состоящих из *n* запросов.<br />1 типа 3, когда запрос сброшен из кэша.|21|Да|  
|IntegerData2|`int`|Конечное смещение инструкции в хранимой процедуре или пакете:<br /><br /> -1 для конечного смещения хранимой процедуры или пакета.|55|Да|  
|ObjectID|`int`|NULL|22|Да|  
|Offset|`int`|Начальное смещение инструкции в пределах хранимой процедуры или пакета.<br /><br /> 0 для начального смещения хранимой процедуры или пакета.|61|Да|  
|SPID|`int`|Идентификатор сеанса, в котором произошло событие.|12|Да|  
|SqlHandle|`image`|Дескриптор SQL, который можно использовать для получения текста SQL хранимой процедуры или пакета с помощью динамического административного представления dm_exec_sql_text.|63|Да|  
|StartTime|`datetime`|Время начала события, если оно известно.|14|Да|  
|TextData|`ntext`|QueryExecutionStats|1|Да|  
|PlanHandle|`image`|Дескриптор скомпилированного плана для хранимой процедуры или пакета. Может быть использован для получения плана XML с помощью динамического административного представления dm_exec_query_plan.|65|Да|  
|GroupID|`int`|Идентификатор группы рабочей нагрузки, в которой запускается событие трассировки SQL.|66|Да|  
  
### <a name="eventsubclass-4"></a>EventSubClass 4  
  
|Имя столбца данных|Тип данных|Описание|Идентификатор столбца|Фильтруемый|  
|----------------------|---------------|-----------------|---------------|----------------|  
|BigintData1|`bigint`|NULL|52|Да|  
|BinaryData|`image`|NULL|2|Да|  
|DatabaseID|`int`|Идентификатор базы данных, в которой располагается заданная хранимая процедура.|3|Да|  
|EventSequence|`int`|Последовательность данного события в запросе.|51|Нет|  
|SessionLoginName|`nvarchar`|Имя входа пользователя, создавшего этот сеанс. Например, при соединении с [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] под именем Login1 и при выполнении инструкции под именем Login2 SessionLoginName будет содержать значение Login1, а LoginName — значение Login2. В этом столбце отображаются как имена входа [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , так и имена входа Windows.|64|Да|  
|EventSubClass|`int`|Тип подкласса события.<br /><br /> 4 = Кэшированная хранимая процедура удалена из кэша, и связанные с ней данные об истории производительности будут уничтожены.|21|Да|  
|IntegerData2|`int`|NULL|55|Да|  
|ObjectID|`int`|Идентификатор хранимой процедуры. Соответствует столбцу object_id в представлении sys.procedures.|22|Да|  
|Offset|`int`|NULL|61|Да|  
|SPID|`int`|Идентификатор сеанса, в котором произошло событие.|12|Да|  
|SqlHandle|`image`|Дескриптор SQL, который можно использовать для получения текста SQL хранимой процедуры, выполненной с помощью динамического административного представления dm_exec_sql_text.|63|Да|  
|StartTime|`datetime`|Время начала события, если оно известно.|14|Да|  
|TextData|`ntext`|ProcedureExecutionStats|1|Да|  
|PlanHandle|`image`|Дескриптор скомпилированного плана для хранимой процедуры. Может быть использован для получения плана XML с помощью динамического административного представления dm_exec_query_plan.|65|Да|  
|GroupID|`int`|Идентификатор группы рабочей нагрузки, в которой запускается событие трассировки SQL.|66|Да|  
  
### <a name="eventsubclass-5"></a>EventSubClass 5  
  
|Имя столбца данных|Тип данных|Описание|Идентификатор столбца|Фильтруемый|  
|----------------------|---------------|-----------------|---------------|----------------|  
|BigintData1|`bigint`|NULL|52|Да|  
|BinaryData|`image`|NULL|2|Да|  
|DatabaseID|`int`|Идентификатор базы данных, в которой располагается заданный триггер.|3|Да|  
|EventSequence|`int`|Последовательность данного события в запросе.|51|Нет|  
|SessionLoginName|`nvarchar`|Имя входа пользователя, создавшего этот сеанс. Например, при соединении с [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] под именем Login1 и при выполнении инструкции под именем Login2 SessionLoginName будет содержать значение Login1, а LoginName — значение Login2. В этом столбце отображаются как имена входа [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , так и имена входа Windows.|64|Да|  
|EventSubClass|`int`|Тип подкласса события.<br /><br /> 5 = Кэшированный триггер удален из кэша, и связанные с ним данные об истории производительности будут уничтожены.|21|Да|  
|IntegerData2|`int`|NULL|55|Да|  
|ObjectID|`int`|Идентификатор триггера. Соответствует столбцу object_id в представлениях каталогов sys.triggers/sys.server_triggers.|22|Да|  
|Offset|`int`|NULL|61|Да|  
|SPID|`int`|Идентификатор сеанса, в котором произошло событие.|12|Да|  
|SqlHandle|`image`|Дескриптор SQL, который можно использовать для получения текста SQL триггера с помощью динамического административного представления dm_exec_sql_text.|63|Да|  
|StartTime|`datetime`|Время начала события, если оно известно.|14|Да|  
|TextData|`ntext`|TriggerExecutionStats|1|Да|  
|PlanHandle|`image`|Дескриптор скомпилированного плана для триггера. Может быть использован для получения плана XML с помощью динамического административного представления dm_exec_query_plan.|65|Да|  
|GroupID|`int`|Идентификатор группы рабочей нагрузки, в которой запускается событие трассировки SQL.|66|Да|  
  
## <a name="see-also"></a>См. также  
 [Расширенные события](../extended-events/extended-events.md)   
 [Хранимая процедура sp_trace_setevent (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [Класс событий Showplan XML for Query Compile](showplan-xml-for-query-compile-event-class.md)   
 [Динамические административные представления и функции (Transact-SQL)](../views/views.md)  
  
  