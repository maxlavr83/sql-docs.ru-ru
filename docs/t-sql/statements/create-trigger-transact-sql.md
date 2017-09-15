---
title: "CREATE TRIGGER (Transact-SQL) | Документы Microsoft"
ms.custom:
- SQL2016_New_Updated
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE TRIGGER
- TRIGGER
- CREATE_TRIGGER_TSQL
- TRIGGER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- recursive DML triggers [SQL Server]
- CREATE TRIGGER statement
- multiple triggers
- deferred name resolution, DML triggers
- DML triggers, creating
- nested triggers
- server-scoped triggers
- DDL triggers, creating
- triggers [SQL Server], creating
- database-scoped triggers [SQL Server]
ms.assetid: edeced03-decd-44c3-8c74-2c02f801d3e7
caps.latest.revision: 140
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 56011e892d5fbc5862f3d7c279bc297c3d0ac04c
ms.contentlocale: ru-ru
ms.lasthandoff: 09/01/2017

---
# <a name="create-trigger-transact-sql"></a>CREATE TRIGGER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Создает триггер языка обработки данных, DDL или входа. Триггер — это особая разновидность хранимой процедуры, выполняемая автоматически при возникновении события на сервере базы данных. Триггеры языка обработки данных выполняются по событиям, вызванным попыткой пользователя изменить данные с помощью языка обработки данных. Событиями DML являются процедуры INSERT, UPDATE или DELETE, применяемые к таблице или представлению. Эти триггеры срабатывают при запуске любого допустимого события независимо от того, влияет ли оно на какие-либо строки таблицы. Дополнительные сведения см. в разделе [DML Triggers](../../relational-databases/triggers/dml-triggers.md).  
  
 Триггеры DDL срабатывают в ответ на ряд событий языка описания данных (DDL). Эти события прежде всего соответствуют инструкциям [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE, ALTER, DROP и некоторым системным хранимым процедурам, которые выполняют схожие с DDL операции. Триггеры входа могут срабатывать в ответ на событие LOGON, возникающее при установке пользовательских сеансов. Триггеры могут быть созданы непосредственно из [!INCLUDE[tsql](../../includes/tsql-md.md)] инструкций или методов сборок, созданных в [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] общеязыковая среда выполнения (CLR) и их передачи в экземпляр [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] позволяет создавать несколько триггеров для любой инструкции.  
  
> [!IMPORTANT]  
>  Вредоносный программный код внутри триггеров может быть запущен с расширенными правами доступа. Дополнительные сведения о том, как устранить эту угрозу см. в разделе [Управление безопасностью триггеров](../../relational-databases/triggers/manage-trigger-security.md).  
  
> [!NOTE]  
>  В этом разделе рассматривается интеграция со средой CLR .NET Framework в SQL Server. Интеграция со средой CLR не применяется к базе данных SQL Azure.  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
-- SQL Server Syntax  
-- Trigger on an INSERT, UPDATE, or DELETE statement to a table or view (DML Trigger)  
  
CREATE [ OR ALTER ] TRIGGER [ schema_name . ]trigger_name   
ON { table | view }   
[ WITH <dml_trigger_option> [ ,...n ] ]  
{ FOR | AFTER | INSTEAD OF }   
{ [ INSERT ] [ , ] [ UPDATE ] [ , ] [ DELETE ] }   
[ WITH APPEND ]  
[ NOT FOR REPLICATION ]   
AS { sql_statement  [ ; ] [ ,...n ] | EXTERNAL NAME <method specifier [ ; ] > }  
  
<dml_trigger_option> ::=  
    [ ENCRYPTION ]  
    [ EXECUTE AS Clause ]  
  
<method_specifier> ::=  
    assembly_name.class_name.method_name  
  
```  
  
```  
-- SQL Server Syntax  
-- Trigger on an INSERT, UPDATE, or DELETE statement to a 
-- table (DML Trigger on memory-optimized tables)  
  
CREATE [ OR ALTER ] TRIGGER [ schema_name . ]trigger_name   
ON { table }   
[ WITH <dml_trigger_option> [ ,...n ] ]  
{ FOR | AFTER }   
{ [ INSERT ] [ , ] [ UPDATE ] [ , ] [ DELETE ] }   
AS { sql_statement  [ ; ] [ ,...n ] }  
  
<dml_trigger_option> ::=  
    [ NATIVE_COMPILATION ]  
    [ SCHEMABINDING ]  
    [ EXECUTE AS Clause ]  
  
```  
  
```  
-- Trigger on a CREATE, ALTER, DROP, GRANT, DENY, 
-- REVOKE or UPDATE statement (DDL Trigger)  
  
CREATE [ OR ALTER ] TRIGGER trigger_name   
ON { ALL SERVER | DATABASE }   
[ WITH <ddl_trigger_option> [ ,...n ] ]  
{ FOR | AFTER } { event_type | event_group } [ ,...n ]  
AS { sql_statement  [ ; ] [ ,...n ] | EXTERNAL NAME < method specifier >  [ ; ] }  
  
<ddl_trigger_option> ::=  
    [ ENCRYPTION ]  
    [ EXECUTE AS Clause ]  
  
```  
  
```  
-- Trigger on a LOGON event (Logon Trigger)  
  
CREATE [ OR ALTER ] TRIGGER trigger_name   
ON ALL SERVER   
[ WITH <logon_trigger_option> [ ,...n ] ]  
{ FOR| AFTER } LOGON    
AS { sql_statement  [ ; ] [ ,...n ] | EXTERNAL NAME < method specifier >  [ ; ] }  
  
<logon_trigger_option> ::=  
    [ ENCRYPTION ]  
    [ EXECUTE AS Clause ]  
  
```  
  
## <a name="syntax"></a>Синтаксис  
  
```  
-- Windows Azure SQL Database Syntax   
-- Trigger on an INSERT, UPDATE, or DELETE statement to a table or view (DML Trigger)  
  
CREATE [ OR ALTER ] TRIGGER [ schema_name . ]trigger_name   
ON { table | view }   
 [ WITH <dml_trigger_option> [ ,...n ] ]   
{ FOR | AFTER | INSTEAD OF }   
{ [ INSERT ] [ , ] [ UPDATE ] [ , ] [ DELETE ] }   
  AS { sql_statement  [ ; ] [ ,...n ] [ ; ] > }  
  
<dml_trigger_option> ::=   
        [ EXECUTE AS Clause ]  
  
```  
  
```  
-- Windows Azure SQL Database Syntax  
-- Trigger on a CREATE, ALTER, DROP, GRANT, DENY, 
-- REVOKE, or UPDATE STATISTICS statement (DDL Trigger)   
  
CREATE [ OR ALTER ] TRIGGER trigger_name   
ON { DATABASE }   
 [ WITH <ddl_trigger_option> [ ,...n ] ]   
{ FOR | AFTER } { event_type | event_group } [ ,...n ]   
AS { sql_statement  [ ; ] [ ,...n ]  [ ; ] }  
  
<ddl_trigger_option> ::=   
    [ EXECUTE AS Clause ]  
```  
  
## <a name="arguments"></a>Аргументы
ИЛИ ALTER  
 **Применяется к**: Azure [!INCLUDE[ssSDS](../../includes/sssds-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (начиная с [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1). 
  
 Условно изменяет триггер только в том случае, если он уже существует. 
  
 *schema_name*  
 Имя схемы, которой принадлежит триггер DML. Действие триггеров DML ограничивается областью схемы таблицы или представления, для которых они созданы. *schema_name* не может быть указан для триггеров DDL или входа.  
  
 *имя_триггера*  
 Имя триггера. Объект *имя_триггера* должны соответствовать правилам для [идентификаторы](../../relational-databases/databases/database-identifiers.md), за исключением того, что *имя_триггера* не может начинаться с символов # или ##.  
  
 *Таблица* | *представление*  
 Таблица или представление, в которых выполняется триггер DML, иногда указывается как таблица триггера или представление триггера. Указание уточненного имени таблицы или представления не является обязательным. На представление может ссылаться только триггер INSTEAD OF. Триггеры DML не могут быть описаны в локальной или глобальной временных таблицах.  
  
 DATABASE  
 Применяет область действия триггера DDL к текущей базе данных. Если указано, триггер срабатывает всякий раз, когда *event_type* или *event_group* происходит в текущей базе данных.  
  
 ALL SERVER  
 **Область применения**: начиная с [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] до [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Применяет область действия триггера DDL или триггера входа к текущему серверу. Если указано, триггер срабатывает всякий раз, когда *event_type* или *event_group* возникновении в любом месте на текущем сервере.  
  
 WITH ENCRYPTION  
 **Область применения**: начиная с [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] до [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Затемняет текст инструкции CREATE TRIGGER. Использование параметра WITH ENCRYPTION не позволяет публиковать триггер как часть репликации [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Параметр WITH ENCRYPTION не может быть указан для триггеров CLR.  
  
 EXECUTE AS  
 Указывает контекст безопасности, в котором выполняется триггер. Позволяет управлять учетной записью пользователя, используемой экземпляром [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] для проверки разрешений на любые объекты базы данных, ссылаемые триггером.  
  
 Этот параметр является обязательным для триггеров в таблицах, оптимизированных для памяти.  
  
 Дополнительные сведения см. в разделе[предложение EXECUTE AS &#40; Transact-SQL &#41; ](../../t-sql/statements/execute-as-clause-transact-sql.md).  
  
 NATIVE_COMPILATION  
 Указывает, что триггер скомпилирован в собственном коде.  
  
 Этот параметр является обязательным для триггеров в таблицах, оптимизированных для памяти.  
  
 SCHEMABINDING  
 Гарантирует, что таблицы, на которые ссылается триггер не может удалить или изменить.  
  
 Этот параметр является обязательным для триггеров в таблицах, оптимизированных для памяти и не поддерживается для триггеров в обычных таблицах.  
  
 FOR | AFTER  
 Тип AFTER указывает, что триггер DML срабатывает только после успешного выполнения всех операций в инструкции SQL, запускаемой триггером. Все каскадные действия и проверки ограничений, на которые имеется ссылка, должны быть успешно завершены, прежде чем триггер сработает.  
  
 Если единственным заданным ключевым словом является FOR, аргумент AFTER используется по умолчанию.  
  
 Триггеры AFTER не могут быть определены на представлениях.  
  
 INSTEAD OF  
 Указывает, что триггер DML выполняется *вместо* запуска инструкции SQL, поэтому, переопределение действия запускающих инструкций. Аргумент INSTEAD OF не может быть указан для триггеров DDL или триггеров входа.  
  
 На каждую инструкцию INSERT, UPDATE или DELETE в таблице или представлении может быть определено не более одного триггера INSTEAD OF. Однако можно определить представления на представлениях, где у каждого представления есть собственный триггер INSTEAD OF.  
  
 Использование триггеров INSTEAD OF не допускается в поддерживающих обновление представлениях, которые используют параметр WITH CHECK OPTION. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] вызывает ошибку, если триггер INSTEAD OF добавляется к поддерживающему обновление представлению с параметром WITH CHECK OPTION. Пользователь должен удалить этот параметр при помощи инструкции ALTER VIEW перед определением триггера INSTEAD OF.  
  
 { [ DELETE ] [ , ] [ INSERT ] [ , ] [ UPDATE ] }  
 Определяет инструкции изменения данных, по которым срабатывает триггер DML, если он применяется к таблице или представлению. Необходимо указать как минимум одну инструкцию. В определении триггера разрешены любые их сочетания в любом порядке.  
  
 Для триггеров INSTEAD OF параметр DELETE не разрешен в таблицах, имеющих ссылочную связь с указанием каскадного действия ON DELETE. Аналогично параметр UPDATE не разрешен в таблицах, у которых есть ссылочная связь с указанием каскадного действия ON UPDATE.  
  
 WITH APPEND  
 **Область применения**: начиная с [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] до [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].  
  
 Указывает, что требуется добавить триггер существующего типа. Аргумент WITH APPEND не может быть использован для триггеров INSTEAD OF или при явном указании триггера AFTER. Аргумент WITH APPEND может использоваться только при указании параметра FOR без INSTEAD OF или AFTER из соображений поддержки обратной совместимости. Аргумент WITH APPEND не может быть указан, если указан параметр EXTERNAL NAME (в случае триггера CLR).  
  
 *event_type*  
 Имя языкового события [!INCLUDE[tsql](../../includes/tsql-md.md)], которое после выполнения вызывает срабатывание триггера DDL. Список событий триггеров DDL, перечислены в [DDL-события](../../relational-databases/triggers/ddl-events.md).  
  
 *event_group*  
 Имя стандартной группы событий языка [!INCLUDE[tsql](../../includes/tsql-md.md)]. Триггер DDL срабатывает после любого [!INCLUDE[tsql](../../includes/tsql-md.md)] событий языка, к которому принадлежит *event_group*. Список групп событий для триггеров DDL, перечислены в [группы DDL-событий](../../relational-databases/triggers/ddl-event-groups.md).  
  
 После завершения работы, инструкции CREATE TRIGGER *event_group* также функционирует в качестве макроса, добавляя события соответствующих типов его представление каталога sys.trigger_events.  
  
 NOT FOR REPLICATION  
 **Область применения**: начиная с [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] до [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Указывает, что триггер не может быть выполнен, если агент репликации изменяет таблицу, используемую триггером.  
  
 *sql_statement*  
 Условия и действия триггера. Условия триггера указывают дополнительные критерии, определяющие, какие события — DML, DDL или событие входа — вызывают срабатывание триггера.  
  
 Действия триггера, указанные в инструкциях языка [!INCLUDE[tsql](../../includes/tsql-md.md)], вступают в силу после попытки использования операции.  
  
 Триггеры могут содержать любое количество инструкций языка [!INCLUDE[tsql](../../includes/tsql-md.md)] любого типа, за некоторыми исключениями. Дополнительные сведения см. в подразделе «Примечания». Триггеры разработаны для контроля или изменения данных на основании инструкций модификации или определения данных; они не возвращают пользователю никаких данных. [!INCLUDE[tsql](../../includes/tsql-md.md)] Инструкций в триггере часто включают в себя [языка управления потоком](~/t-sql/language-elements/control-of-flow.md).  
  
 Триггеры DML используют логические (концептуальные) таблицы deleted и inserted. По своей структуре они подобны таблице, на которой определен триггер, то есть таблице, к которой применяется действие пользователя. В таблицах deleted и inserted содержатся старые или новые значения строк, которые могут быть изменены действиями пользователя. Например, для запроса всех значений таблицы `deleted` можно использовать инструкцию:  
  
```  
SELECT * FROM deleted;  
```  
  
 Дополнительные сведения см. в разделе [использование таблиц inserted и deleted](../../relational-databases/triggers/use-the-inserted-and-deleted-tables.md).  
  
 Триггеры DDL и logon записи сведений о событиях, запускаемых с помощью [EVENTDATA &#40; Transact-SQL &#41; ](../../t-sql/functions/eventdata-transact-sql.md) функции. Дополнительные сведения см. в разделе [использование функции EVENTDATA](../../relational-databases/triggers/use-the-eventdata-function.md).  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]поддерживает обновление от **текст**, **ntext**, или **изображения** триггера столбцов с помощью INSTEAD OF для таблиц или представлений.  
  
> [!IMPORTANT]  
>  **ntext**, **текст**, и **изображения** типов данных будет удалена в будущей версии [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Следует избегать использования этих типов данных при новой разработке и запланировать изменение приложений, использующих их в настоящий момент. Вместо них следует использовать типы данных [nvarchar(max)](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md), [varchar(max)](../../t-sql/data-types/char-and-varchar-transact-sql.md)и [varbinary(max)](../../t-sql/data-types/binary-and-varbinary-transact-sql.md) . Триггеры AFTER и INSTEAD OF поддержки **varchar(MAX)**, **nvarchar(MAX)**, и **varbinary(MAX)** данные в таблицах inserted и deleted.  
  
 Для триггеров в таблицах, оптимизированных для памяти единственным *sql_statement* разрешено на верхнем уровне-блок ATOMIC. T-SQL, допускается внутри блока ATOMIC ограничивается разрешалось использовать в собственном коде T-SQL.  
  
 \<method_specifier > **применяется к**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] через [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Указывает метод сборки для связывания с CLR-триггером. Этот метод не должен принимать аргументы и возвращать значения void. *class_name* должен быть допустимым [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] идентификатором и существовать как класс в сборке с видимостью сборки. Если класс имеет имя, содержащее точки (.) для разделения частей пространства имен, имя класса должно быть заключено в квадратные скобки ([ ]) или двойные кавычки (" "). Класс не может быть вложенным.  
  
> [!NOTE]  
>  По умолчанию возможность [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] запускать код CLR отключена. Можно создавать, изменять и удалять объекты базы данных, которые ссылаются на модули управляемого кода, но эти ссылки не будут выполнены в экземпляре [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Если [параметр clr enabled](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md) включен с помощью [sp_ Настройка](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
## <a name="remarks-dml-triggers"></a>Триггеры DML примечания  
 Триггеры DML часто используются для применения бизнес-правил и обеспечения целостности данных. В [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] декларативное ограничение ссылочной целостности обеспечивается инструкциями ALTER TABLE и CREATE TABLE. Однако декларативное ограничение ссылочной целостности не обеспечивает ссылочную целостность между базами данных. Ограничение ссылочной целостности подразумевает выполнение правил связи между первичными и внешними ключами таблиц. Для обеспечения ограничений ссылочной целостности используйте в инструкциях ALTER TABLE и CREATE TABLE ограничения PRIMARY KEY и FOREIGN KEY. Если ограничения распространяются на таблицу триггера, они проверяются после срабатывания триггера INSTEAD OF и до выполнения триггера AFTER. В случае нарушения ограничения выполняется откат действий триггера INSTEAD OF, и триггер AFTER не срабатывает.  
  
 Первые и последние триггеры AFTER, которые будут выполнены в таблице, могут быть определены с использованием процедуры sp_settriggerorder. Для таблицы можно определить только один первый и один последний триггер для каждой из операций INSERT, UPDATE и DELETE. Если в таблице есть другие триггеры AFTER, они будут выполняться случайным образом.  
  
 Если инструкция ALTER TRIGGER меняет первый или последний триггер, первый или последний набор атрибутов измененного триггера удаляется, а порядок сортировки должен быть установлен заново с помощью процедуры sp_settriggerorder.  
  
 Триггер AFTER выполняется только после того, как вызывающая срабатывание триггера инструкция SQL была успешно выполнена. Успешное выполнение также подразумевает завершение всех ссылочных каскадных действий и проверки ограничений, связанных с измененными или удаленными объектами. Триггер AFTER не вызывает рекурсивное срабатывание триггера INSTEAD OF в одной и той же таблице.  
  
 Если триггер INSTEAD OF, определенный для таблицы, выполняет по отношению к таблице какую-либо инструкцию, которая бы снова вызвала срабатывание триггера INSTEAD OF, триггер рекурсивно не вызывается. Вместо этого инструкция обрабатывается так, как если бы у таблицы отсутствовал триггер INSTEAD OF, и начинается применение последовательности ограничений и выполнение триггера AFTER. Например, если триггер определен в виде триггера INSTEAD OF INSERT для таблицы и выполняет инструкцию INSERT для этой же таблицы, инструкция INSERT не вызывает нового срабатывания триггера. Команда INSERT, выполняемая триггером, начинает процесс применения ограничений и взвода всех триггеров AFTER INSERT, определенных для данной таблицы.  
  
 Если триггер INSTEAD OF, определенный для представления, выполняет по отношению к представлению какую-либо инструкцию, которая бы снова вызвала срабатывание триггера INSTEAD OF, триггер рекурсивно не вызывается. Вместо этого инструкция выполняет изменение базовых таблиц, на которых основано представление. В данном случае определение представления должно удовлетворять всем ограничениям, установленным для обновляемых представлений. Определение обновляемых представлений см. в разделе [изменение данных через представление](../../relational-databases/views/modify-data-through-a-view.md).  
  
 Например, если триггер определен как INSTEAD OF UPDATE для представления и выполняет инструкцию UPDATE для этого же представления, инструкция UPDATE, выполняемая триггером, не вызывает нового срабатывания триггера. Инструкция UPDATE, выполняемая в триггере, обрабатывает представление так, как если бы у представления не имелось триггера INSTEAD OF. Столбцы, измененные с помощью инструкции UPDATE, должны принадлежать одной базовой таблице. Каждая модификация базовой таблицы вызывает применение последовательности ограничений и взвод триггеров AFTER, определенных для данной таблицы.  
  
### <a name="testing-for-update-or-insert-actions-to-specific-columns"></a>Проверка действий инструкций UPDATE или INSERT на указанные столбцы  
 Триггер языка [!INCLUDE[tsql](../../includes/tsql-md.md)] можно сконструировать для выполнения конкретных действий, основанных на изменении определенных столбцов с помощью инструкций UPDATE или INSERT. Используйте [UPDATE()](../../t-sql/functions/update-trigger-functions-transact-sql.md) или [COLUMNS_UPDATED](../../t-sql/functions/columns-updated-transact-sql.md) в теле триггера для этой цели. Конструкция UPDATE() проверяет действие инструкций UPDATE или INSERT на одном столбце. С помощью конструкции COLUMNS_UPDATED проверяются действия инструкций UPDATE или INSERT, проводимых на нескольких столбцах, и возвращается битовый шаблон, показывающий, какие столбцы были вставлены или обновлены.  
  
### <a name="trigger-limitations"></a>Ограничения триггеров  
 Инструкция CREATE TRIGGER должна быть первой инструкцией в пакете и может применяться только к одной таблице.  
  
 Триггер создается только в текущей базе данных, но может, тем не менее, содержать ссылки на объекты за пределами текущей базы данных.  
  
 Если для уточнения триггера указано имя схемы, имя таблицы необходимо уточнить таким же образом.  
  
 Одно и то же действие триггера может быть определено более чем для одного действия пользователя (например, INSERT и UPDATE) в одной и той же инструкции CREATE TRIGGER.  
  
 Триггеры INSTEAD OF DELETE/UPDATE нельзя определить для таблицы, у которой есть внешний ключ, определенный для каскадного выполнения операции DELETE/UPDATE.  
  
 Внутри триггера может быть использована любая инструкция SET. Выбранный параметр SET остается в силе во время выполнения триггера, после чего настройки возвращаются в предыдущее состояние.  
  
 Во время срабатывания триггера результаты возвращаются вызывающему приложению так же, как и в случае с хранимыми процедурами. Чтобы предотвратить вызванное срабатыванием триггера возвращение результатов приложению, не следует включать инструкции SELECT, возвращающие результат, или инструкции, которые выполняют в триггере присвоение переменных. Триггер, содержащий либо инструкции SELECT, которые возвращают результаты пользователю, либо инструкции, выполняющие присвоение переменных, требует особого обращения; эти возвращаемые результаты должны быть перезаписаны во все приложения, в которых разрешены изменения таблицы триггера. Если в триггере происходит присвоение переменной, следует использовать инструкцию SET NOCOUNT в начале триггера, чтобы предотвратить возвращение каких-либо результирующих наборов.  
  
 Хотя инструкция TRUNCATE TABLE по своей сути является инструкцией DELETE, она не активирует триггер, поскольку операция не записывает удаление отдельных строк. Однако беспокоиться о случайном обходе триггера DELETE таким образом нужно только пользователям с разрешениями на выполнение инструкции TRUNCATE TABLE.  
  
 Инструкция WRITETEXT (с ведением журнала и без него) не запускает триггеры.  
  
 Следующие инструкции языка [!INCLUDE[tsql](../../includes/tsql-md.md)] не разрешены в триггерах DML:  
  
||||  
|-|-|-|  
|ALTER DATABASE|CREATE DATABASE|DROP DATABASE|  
|RESTORE DATABASE|RESTORE LOG|RECONFIGURE|  
  
 Кроме того, использование следующих инструкций [!INCLUDE[tsql](../../includes/tsql-md.md)] в тексте триггера DML не допускается, если он применяется к таблице или представлению, которые являются целью действий триггера.  
  
||||  
|-|-|-|  
|CREATE INDEX (в т.ч CREATE SPATIAL INDEX и CREATE XML INDEX)|ALTER INDEX|DROP INDEX|  
|DBCC DBREINDEX|ALTER PARTITION FUNCTION|DROP TABLE|  
|ALTER TABLE, если используется в следующих целях:<br /><br /> Добавление, изменение или удаление столбцов.<br /><br /> Переключение секций.<br /><br /> Добавление или удаление ограничений PRIMARY KEY и UNIQUE.|||  
  
> [!NOTE]  
>  Поскольку [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] не поддерживает пользовательских триггеров в системных таблицах, рекомендуется не создавать пользовательские триггеры для системных таблиц.  
  
## <a name="remarks-ddl-triggers"></a>Триггеры DDL примечания  
 Триггеры DDL, как и стандартные триггеры, выполняют хранимые процедуры в ответ на какое-либо событие. В отличие от стандартных триггеров, они не срабатывают в ответ на выполнение инструкций UPDATE, INSERT или DELETE по отношению к таблице или представлению. Вместо этого триггеры срабатывают в первую очередь в ответ на инструкции языка определения данных (DDL). Это инструкции CREATE, ALTER, DROP, GRANT, DENY, REVOKE и UPDATE STATISTICS. Системные хранимые процедуры, выполняющие операции, подобные операциям DDL, также могут запускать триггеры DDL.  
  
> [!IMPORTANT]  
>  Протестируйте триггеры DDL, чтобы получить ответ на выполнение системных хранимых процедур. Например, инструкция CREATE TYPE и хранимые процедуры sp_addtype и sp_rename вызовут срабатывание триггера DDL, созданного для события CREATE_TYPE.  
  
 Дополнительные сведения о триггерах DDL см. в разделе [триггеры DDL](../../relational-databases/triggers/ddl-triggers.md).  
  
 Триггеры DDL не срабатывают в ответ на события, влияющие на локальные или глобальные временные таблицы и хранимые процедуры.  
  
 В отличие от триггеров DML, триггеры DDL не ограничены областью схемы. Поэтому для запроса метаданных о триггерах DDL нельзя воспользоваться такими функциями как OBJECT_ID, OBJECT_NAME, OBJECTPROPERTY и OBJECTPROPERTYEX. Используйте вместо них представления каталога. Дополнительные сведения см. в разделе [получить сведения о триггерах DDL](../../relational-databases/triggers/get-information-about-ddl-triggers.md).  
  
> [!NOTE]  
>  Триггеры DDL сервера появляются в [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] обозревателя объектов в **триггеры** папки. Эта папка находится под папкой **Объекты сервера** . Триггеры DDL уровня базы данных находятся в **триггеры базы данных** папки. Эта папка находится в папке **Программирование** соответствующей базы данных.  
  
## <a name="logon-triggers"></a>Триггеры входа  
 Триггеры входа выполняют хранимые процедуры в ответ на событие LOGON. Это событие вызывается при установке пользовательского сеанса с экземпляром [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Триггеры входа срабатывают после завершения этапа проверки подлинности при входе, но перед тем, как пользовательский сеанс реально устанавливается. Следовательно, все сообщения, которые возникают внутри триггера и обычно достигают пользователя, такие как сообщения об ошибках и сообщения от инструкции PRINT, перенаправляются в журнал ошибок [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Дополнительные сведения см. в разделе [триггеры входа](../../relational-databases/triggers/logon-triggers.md).  
  
 Если проверка подлинности завершается сбоем, триггеры входа не срабатывают.  
  
 В триггерах входа не поддерживаются распределенные транзакции. Если срабатывает триггер входа, содержащий распределенную транзакцию, возвращается ошибка 3969.  
  
### <a name="disabling-a-logon-trigger"></a>Отключение триггера входа  
 Триггер входа может эффективно запрещать подключения к службам [!INCLUDE[ssDE](../../includes/ssde-md.md)] для всех пользователей, в том числе членов предопределенной роли сервера **sysadmin** . Если триггер входа запрещает соединения, члены предопределенной роли сервера **sysadmin** могут подключаться с помощью выделенного административного соединения или путем вызова [!INCLUDE[ssDE](../../includes/ssde-md.md)] в режиме минимальной конфигурации (-f). Дополнительные сведения см. в разделе [Параметры запуска службы Database Engine](../../database-engine/configure-windows/database-engine-service-startup-options.md).  
  
## <a name="general-trigger-considerations"></a>Общие соглашения о триггерах  
  
### <a name="returning-results"></a>Возвращаемые результаты  
 Возможность возвращать результаты из триггеров будет исключена из следующей версии SQL Server. Триггеры, возвращающие результирующие наборы, могут привести к непредвиденному поведению приложений, не предназначенных для работы с ними. Не используйте в разрабатываемых приложениях триггеры, возвращающие результирующие наборы, и запланируйте изменение приложений, которые используют их в настоящее время. Чтобы триггеры не возвращали результирующие наборы, установите [disallow results from triggers параметр](../../database-engine/configure-windows/disallow-results-from-triggers-server-configuration-option.md) значение 1.  
  
 Триггеры входа всегда запрещают возврат результирующих наборов, и данное поведение нельзя настроить. Если триггер входа формирует результирующий набор, то триггер не выполняется и попытка входа, вызванная триггером, запрещается.  
  
### <a name="multiple-triggers"></a>Несколько триггеров  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] позволяет создавать несколько триггеров для каждого события DML, DDL и LOGON. Например, если инструкция CREATE TRIGGER FOR UPDATE выполняется в таблице, уже имеющей триггер UPDATE, дополнительно создается триггер обновления. В более ранних версиях [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] был разрешен только один триггер в каждой таблице для каждого события изменения данных INSERT, UPDATE или DELETE.  
  
### <a name="recursive-triggers"></a>Рекурсивные триггеры  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] разрешает рекурсивный вызов триггеров, если с помощью инструкции ALTER DATABASE включена настройка RECURSIVE_TRIGGERS.  
  
 В рекурсивных триггерах могут возникать следующие типы рекурсии:  
  
-   Косвенная рекурсия  
  
     При косвенной рекурсии приложение обновляет таблицу T1. Это событие вызывает срабатывание триггера TR1, обновляющего таблицу T2. Это вызывает срабатывание триггера T2 и обновление таблицы T1.  
  
-   Прямая рекурсия  
  
     При прямой рекурсии приложение обновляет таблицу T1. Это событие вызывает срабатывание триггера TR1, обновляющего таблицу T1. Поскольку таблица T1 уже была обновлена, триггер TR1 срабатывает снова и т. д.  
  
 В следующем примере используются оба типа рекурсий: прямая и косвенная. Допустим, для таблицы T1 определены два триггера: TR1 и TR2. Триггер TR1 рекурсивно обновляет таблицу T1. Инструкция UPDATE выполняет каждый из триггеров TR1 и TR2 один раз. В дополнение к этому срабатывание триггера TR1 вызывает выполнение триггеров TR1 (рекурсивно) и TR2. В таблицах inserted и deleted триггера содержатся строки, которые относятся только к инструкции UPDATE, вызвавшей срабатывание триггера.  
  
> [!NOTE]  
>  Описанная ситуация имеет место только в том случае, если настройка RECURSIVE_TRIGGERS включена с помощью инструкции ALTER DATABASE. Определенного порядка выполнения нескольких триггеров, заданных для какого-либо конкретного события, не существует. Каждый триггер должен быть самодостаточным.  
  
 Отключение настройки RECURSIVE_TRIGGERS предотвращает выполнение только прямых рекурсий. Чтобы отключить косвенную рекурсию, с помощью хранимой процедуры sp_configure присвойте параметру сервера nested triggers значение 0.  
  
 Если один из триггеров выполняет инструкцию ROLLBACK TRANSACTION, никакие другие триггеры, вне зависимости от уровня вложенности, не срабатывают.  
  
### <a name="nested-triggers"></a>Вложенные триггеры  
 Вложенность триггеров может достигать максимум 32 уровня. Если триггер изменяет таблицу, для которой определен другой триггер, то запускается второй триггер, вызывающий срабатывание третьего и т.д. Если любой из триггеров в цепочке отключает бесконечный цикл, то уровень вложенности превышает допустимый предел, и срабатывание триггера отменяется. Если триггер на языке [!INCLUDE[tsql](../../includes/tsql-md.md)] выполняет управляемый код с помощью ссылки на метод, тип или статистическую функцию среды CLR, эта ссылка считается одним из допустимых 32 уровней вложенности. Методы, вызываемые из управляемого кода, под это ограничение не подпадают.  
  
 Чтобы отменить вложенные триггеры, присвойте значение 0 параметру nested triggers хранимой процедуры sp_configure. В конфигурации по умолчанию вложенные триггеры разрешены. Если вложенные триггеры отключены, рекурсивные триггеры тоже будут отключены, вне зависимости от настройки RECURSIVE_TRIGGERS, установленной с помощью инструкции ALTER DATABASE.  
  
 Первый триггер AFTER, вложенный в INSTEAD OF, триггер срабатывает, даже если **вложенные триггеры** параметр конфигурации сервера задано значение 0. Однако при таком значении параметра последующие триггеры AFTER не срабатывают. Рекомендуется проверить приложения на наличие вложенных триггеров определить, соответствуют ли приложения бизнес-правилам в случае если **вложенные триггеры** параметр конфигурации сервера задано значение 0, и внесите соответствующие изменения.  
  
### <a name="deferred-name-resolution"></a>Отложенная интерпретация имен  
 В [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] разрешены хранимые процедуры, триггеры и пакеты на языке [!INCLUDE[tsql](../../includes/tsql-md.md)], которые содержат ссылки на таблицы, не существующие в момент компиляции. Такая возможность называется отложенной интерпретацией имен.  
  
## <a name="permissions"></a>Permissions  
 Для создания триггера DML требуется разрешение ALTER на таблицу или представление, в которых создается триггер.  
  
 Для создания триггера DDL с областью действия в пределах сервера (ON ALL SERVER) или триггера входа требуется разрешение CONTROL SERVER на сервер. Для создания триггера DDL с областью видимости в пределах базы данных (ON DATABASE) требуется разрешение ALTER ANY DATABASE DDL TRIGGER на текущую базу данных.  
  
## <a name="examples"></a>Примеры  
  
### <a name="a-using-a-dml-trigger-with-a-reminder-message"></a>A. Использование триггера DML с предупреждающим сообщением  
 Следующий триггер DML отправляет клиенту сообщение, когда кто-то пытается добавить или изменить данные в таблице `Customer` в базе данных [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
CREATE TRIGGER reminder1  
ON Sales.Customer  
AFTER INSERT, UPDATE   
AS RAISERROR ('Notify Customer Relations', 16, 10);  
GO  
```  
  
### <a name="b-using-a-dml-trigger-with-a-reminder-e-mail-message"></a>Б. Использование триггера DML с предупреждающим сообщением, отправляемым по электронной почте  
 В следующем примере указанному пользователю (`MaryM`) по электронной почте отправляется сообщение при изменении таблицы `Customer`.  
  
```  
CREATE TRIGGER reminder2  
ON Sales.Customer  
AFTER INSERT, UPDATE, DELETE   
AS  
   EXEC msdb.dbo.sp_send_dbmail  
        @profile_name = 'AdventureWorks2012 Administrator',  
        @recipients = 'danw@Adventure-Works.com',  
        @body = 'Don''t forget to print a report for the sales force.',  
        @subject = 'Reminder';  
GO  
```  
  
### <a name="c-using-a-dml-after-trigger-to-enforce-a-business-rule-between-the-purchaseorderheader-and-vendor-tables"></a>В. Использование триггера DML AFTER для принудительного применения бизнес-правил между таблицами PurchaseOrderHeader и Vendor  
 Поскольку ограничение CHECK может содержать ссылки только на столбцы, для которых определены ограничения на уровне столбцов или таблицы, любые межтабличные ограничения (в данном случае бизнес-правила) должны быть заданы в виде триггеров.  
  
 В следующем примере создается триггер DML в базе данных AdventureWorks 2012. Этот триггер проверяет уровень кредитоспособности для поставщика (а не 5) при попытке вставить новый заказ на покупку в `PurchaseOrderHeader` таблицы. Для получения сведений о кредитоспособности поставщика требуется ссылка на таблицу `Vendor`. В случае слишком низкой кредитоспособности выводится соответствующее сообщение и вставка не выполняется.  
  
```  
-- This trigger prevents a row from being inserted in the Purchasing.PurchaseOrderHeader 
-- table when the credit rating of the specified vendor is set to 5 (below average).  
  
CREATE TRIGGER Purchasing.LowCredit ON Purchasing.PurchaseOrderHeader  
AFTER INSERT  
AS  
IF EXISTS (SELECT *  
           FROM Purchasing.PurchaseOrderHeader AS p   
           JOIN inserted AS i   
           ON p.PurchaseOrderID = i.PurchaseOrderID   
           JOIN Purchasing.Vendor AS v   
           ON v.BusinessEntityID = p.VendorID  
           WHERE v.CreditRating = 5  
          )  
BEGIN  
RAISERROR ('A vendor''s credit rating is too low to accept new  
purchase orders.', 16, 1);  
ROLLBACK TRANSACTION;  
RETURN   
END;  
GO  
  
-- This statement attempts to insert a row into the PurchaseOrderHeader table  
-- for a vendor that has a below average credit rating.  
-- The AFTER INSERT trigger is fired and the INSERT transaction is rolled back.  
  
INSERT INTO Purchasing.PurchaseOrderHeader (RevisionNumber, Status, EmployeeID,  
VendorID, ShipMethodID, OrderDate, ShipDate, SubTotal, TaxAmt, Freight)  
VALUES (  
2  
,3  
,261  
,1652  
,4  
,GETDATE()  
,GETDATE()  
,44594.55  
,3567.564  
,1114.8638 );  
GO  
  
```  
  
### <a name="d-using-a-database-scoped-ddl-trigger"></a>Г. Использование триггера DDL уровня базы данных  
 В следующем примере триггер DDL используется для предотвращения удаления синонимов в базе данных.  
  
```  
CREATE TRIGGER safety   
ON DATABASE   
FOR DROP_SYNONYM  
AS   
   RAISERROR ('You must disable Trigger "safety" to drop synonyms!',10, 1)  
   ROLLBACK  
GO  
DROP TRIGGER safety  
ON DATABASE;  
GO  
```  
  
### <a name="e-using-a-server-scoped-ddl-trigger"></a>Д. Использование триггера DDL уровня сервера  
 В следующем примере триггер DDL используется для вывода сообщения при возникновении на данном экземпляре сервера любого из событий CREATE DATABASE, а функция `EVENTDATA` используется для получения текста соответствующей инструкции на языке [!INCLUDE[tsql](../../includes/tsql-md.md)]. Дополнительные примеры использования функции EVENTDATA в триггерах DDL см. в разделе [использование функции EVENTDATA](../../relational-databases/triggers/use-the-eventdata-function.md).  
  
**Область применения**: начиная с [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] до [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
CREATE TRIGGER ddl_trig_database   
ON ALL SERVER   
FOR CREATE_DATABASE   
AS   
    PRINT 'Database Created.'  
    SELECT EVENTDATA().value('(/EVENT_INSTANCE/TSQLCommand/CommandText)[1]','nvarchar(max)')  
GO  
DROP TRIGGER ddl_trig_database  
ON ALL SERVER;  
GO  
```  
  
### <a name="f-using-a-logon-trigger"></a>Е. Использование триггера входа  
 В следующем примере триггер входа запрещает попытки входа для [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] членом *login_test* входа, если уже есть три пользовательских сеанса под этой учетной записью.  
  
**Область применения**: начиная с [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] до [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
USE master;  
GO  
CREATE LOGIN login_test WITH PASSWORD = '3KHJ6dhx(0xVYsdf' MUST_CHANGE,  
    CHECK_EXPIRATION = ON;  
GO  
GRANT VIEW SERVER STATE TO login_test;  
GO  
CREATE TRIGGER connection_limit_trigger  
ON ALL SERVER WITH EXECUTE AS 'login_test'  
FOR LOGON  
AS  
BEGIN  
IF ORIGINAL_LOGIN()= 'login_test' AND  
    (SELECT COUNT(*) FROM sys.dm_exec_sessions  
            WHERE is_user_process = 1 AND  
                original_login_name = 'login_test') > 3  
    ROLLBACK;  
END;  
  
```  
  
### <a name="g-viewing-the-events-that-cause-a-trigger-to-fire"></a>Ж. Просмотр событий, вызвавших срабатывание триггера  
 В следующем примере выполняются запросы к представлениям каталога `sys.triggers` и `sys.trigger_events` с целью определения, какие события языка [!INCLUDE[tsql](../../includes/tsql-md.md)] вызывали срабатывание триггера `safety`. Создание триггера `safety` показано в предыдущем примере.  
  
```  
SELECT TE.*  
FROM sys.trigger_events AS TE  
JOIN sys.triggers AS T ON T.object_id = TE.object_id  
WHERE T.parent_class = 0 AND T.name = 'safety';  
GO  
```  
  
## <a name="see-also"></a>См. также:  
 [ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md)   
 [ALTER TRIGGER (Transact-SQL)](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [Функция COLUMNS_UPDATED &#40; Transact-SQL &#41;](../../t-sql/functions/columns-updated-transact-sql.md)   
 [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)   
 [DROP TRIGGER (Transact-SQL)](../../t-sql/statements/drop-trigger-transact-sql.md)   
 [ENABLE TRIGGER (Transact-SQL)](../../t-sql/statements/enable-trigger-transact-sql.md)   
 [DISABLE TRIGGER (Transact-SQL)](../../t-sql/statements/disable-trigger-transact-sql.md)   
 [Функция TRIGGER_NESTLEVEL &#40; Transact-SQL &#41;](../../t-sql/functions/trigger-nestlevel-transact-sql.md)   
 [EVENTDATA (Transact-SQL)](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.dm_sql_referenced_entities (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)   
 [sys.dm_sql_referencing_entities (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)   
 [Представление каталога sys.sql_expression_dependencies (Transact-SQL)](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)   
 [sp_help (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sp_helptrigger (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helptrigger-transact-sql.md)   
 [sp_helptext (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [sp_rename (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)   
 [sp_settriggerorder &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-settriggerorder-transact-sql.md)   
 [Обновление &#40; &#41; &#40; Transact-SQL &#41;](../../t-sql/functions/update-trigger-functions-transact-sql.md)   
 [Получение сведений о триггерах DML](../../relational-databases/triggers/get-information-about-dml-triggers.md)   
 [Получение сведений о триггерах DDL](../../relational-databases/triggers/get-information-about-ddl-triggers.md)   
 [sys.triggers (Transact-SQL)](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md)   
 [sys.trigger_events (Transact-SQL)](../../relational-databases/system-catalog-views/sys-trigger-events-transact-sql.md)   
 [sys.sql_modules (Transact-SQL)](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.assembly_modules (Transact-SQL)](../../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md)   
 [sys.server_triggers (Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-triggers-transact-sql.md)   
 [sys.server_trigger_events (Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-trigger-events-transact-sql.md)   
 [sys.server_sql_modules (Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-sql-modules-transact-sql.md)   
 [sys.server_assembly_modules (Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-assembly-modules-transact-sql.md)  
  
  


