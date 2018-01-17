---
title: "sys.server_audits (Transact-SQL) | Документы Microsoft"
ms.custom: 
ms.date: 04/05/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- server_audits_TSQL
- sys.server_audits_TSQL
- sys.server_audits
- server_audits
dev_langs: TSQL
helpviewer_keywords: sys.server_audits catalog view
ms.assetid: c2c4a000-1127-46a8-b1e9-947fd1136e1e
caps.latest.revision: "19"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: afd66281887431849c7e1c1983299c6736ff878b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/21/2017
---
# <a name="sysserveraudits-transact-sql"></a>sys.server_audits (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Содержит по одной строке для каждого аудита [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] в экземпляре сервера. Дополнительные сведения см. в статье [Подсистема аудита SQL Server (компонент Database Engine)](../../relational-databases/security/auditing/sql-server-audit-database-engine.md).  
  
|Имя столбца|Тип данных|Description|  
|-----------------|---------------|-----------------|  
|**audit_id**|**int**|Идентификатор аудита.|  
|**name**|**sysname**|Имя аудита.|  
|**audit_guid**|**uniqueidentifier**|Идентификатор GUID аудита, который используется для перечисления аудитов со член Server &#124; подсоединения спецификации аудита базы данных во время запуска сервера и базы данных.|  
|**create_date**|**datetime**|Дата и время создания аудита в формате UTC.|  
|**modify_date**|**datetime**|Дата и время последнего изменения аудита в формате UTC.|  
|**principal_id**|**int**|Идентификатор владельца аудита, зарегистрированного на сервере.|  
|**type**|**char(2)**|Тип аудита:<br /><br /> SL — журнал событий безопасности NT<br /><br /> AL — журнал событий приложений NT<br /><br /> FL — файл в файловой системе|  
|**type_desc**|**nvarchar(60)**|ЖУРНАЛ БЕЗОПАСНОСТИ<br /><br /> ЖУРНАЛ ПРИЛОЖЕНИЙ<br /><br /> FILE|  
|**ON_FAILURE**|**tinyint**|В случае ошибки записи данных о действии:<br /><br /> 0 — продолжить;<br /><br /> 1 — завершить работу экземпляра сервера;<br /><br /> 2 — ошибка операции.|  
|**on_failure_desc**|**nvarchar(60)**|В случае ошибки записи данных о действии:<br /><br /> CONTINUE<br /><br /> SHUTDOWN SERVER INSTANCE<br /><br /> FAIL_OPERATION|  
|**is_state_enabled**|**tinyint**|0 — отключено;<br /><br /> 1 — включено.|  
|**queue_delay**|**int**|Максимальное время ожидания перед записью на диск, в миллисекундах. Если 0, то аудит гарантирует запись, прежде чем событие может быть продолжено.|  
|**предикат**|**nvarchar(3000)**|Выражение предиката, применяемое к событию.|  
  
## <a name="permissions"></a>Permissions  
 Участники **ALTER ANY SERVER AUDIT** или **VIEW ANY DEFINITION** разрешение имеют доступ к этому представлению каталога. Кроме того, участник не должно быть запрещено **VIEW ANY DEFINITION** разрешение.  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Дополнительные сведения см. в разделе [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>См. также:  
 [Создание АУДИТА сервера &#40; Transact-SQL &#41;](../../t-sql/statements/create-server-audit-transact-sql.md)   
 [ALTER SERVER AUDIT &#40; Transact-SQL &#41;](../../t-sql/statements/alter-server-audit-transact-sql.md)   
 [DROP SERVER AUDIT &#40; Transact-SQL &#41;](../../t-sql/statements/drop-server-audit-transact-sql.md)   
 [Создание СПЕЦИФИКАЦИИ АУДИТА сервера &#40; Transact-SQL &#41;](../../t-sql/statements/create-server-audit-specification-transact-sql.md)   
 [ALTER SERVER AUDIT SPECIFICATION &#40; Transact-SQL &#41;](../../t-sql/statements/alter-server-audit-specification-transact-sql.md)   
 [DROP SERVER AUDIT SPECIFICATION &#40; Transact-SQL &#41;](../../t-sql/statements/drop-server-audit-specification-transact-sql.md)   
 [СОЗДАТЬ СПЕЦИФИКАЦИЮ АУДИТА базы данных &#40; Transact-SQL &#41;](../../t-sql/statements/create-database-audit-specification-transact-sql.md)   
 [ALTER DATABASE AUDIT SPECIFICATION &#40; Transact-SQL &#41;](../../t-sql/statements/alter-database-audit-specification-transact-sql.md)   
 [УДАЛИТЬ СПЕЦИФИКАЦИЮ АУДИТА базы данных &#40; Transact-SQL &#41;](../../t-sql/statements/drop-database-audit-specification-transact-sql.md)   
 [ALTER AUTHORIZATION &#40; Transact-SQL &#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [sys.fn_get_audit_file &#40; Transact-SQL &#41;](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md)   
 [sys.server_file_audits &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)   
 [sys.server_audit_specifications &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)   
 [sys.server_audit_specification_details &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)   
 [sys.database_audit_specifications &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)   
 [sys.database_audit_specification_details &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)   
 [sys.dm_server_audit_status &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)   
 [sys.dm_audit_actions &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)   
 [sys.dm_audit_class_type_map &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)   
 [Создание аудита сервера и спецификации аудита сервера](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  