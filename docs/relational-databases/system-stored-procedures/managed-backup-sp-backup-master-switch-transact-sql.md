---
title: "managed_backup.sp_ backup_master_switch (Transact-SQL) | Документы Microsoft"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_ backup_master_switch
- smart_admin.sp_ backup_master_switch
- sp_ backup_master_switch_TSQL
- smart_admin.sp_ backup_master_switch_TSQL
dev_langs: TSQL
helpviewer_keywords:
- sp_ backup_master_switch
- smart_admin.sp_ backup_master_switch
ms.assetid: 1ed2b2b2-c897-41cc-bed5-1c6bc47b9dd2
caps.latest.revision: "12"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 84955e0805abf954d23159cbd0bd1e5b32d1f508
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/02/2018
---
# <a name="managedbackupsp-backupmasterswitch-transact-sql"></a>managed_backup.sp_ backup_master_switch (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Приостанавливает или возобновляет компонент [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].  
  
 Эта хранимая процедура используется для приостановки и возобновления компонента [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. Она обеспечивает сохранность всех параметров конфигурации и их применение при возобновлении работы компонента. При приостановке компонента [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] срок хранения не действует. Это означает отсутствие проверки для определения, следует ли удалять файлы из хранилища, имеются ли поврежденные файлы резервной копии или разрывы в цепочке журналов.  
  

  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```sql  
EXEC managed_backup.sp_backup_master_switch   
                     [@state = ] { 0 | 1}  
```  
  
##  <a name="Arguments"></a> Аргументы  
 @state  
 Задает состояние [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. @state Параметр **бит**. При установке в значение 0 работа приостанавливается, а при установке в значение 1 — возобновляется.  
  
## <a name="return-code-value"></a>Значения кодов возврата  
 0 (успешное завершение) или 1 (неуспешное завершение)  
  
## <a name="security"></a>безопасность  
 Описаны проблемы безопасности, связанные с разрешениями statement.Include как подраздела (заголовок H3). Рассмотрите включение других подразделов для цепочки владения и аудита, если потребуется.  
  
### <a name="permissions"></a>Разрешения  
 Требуется членство в **db_backupoperator** роли базы данных с **ALTER ANY CREDENTIAL** разрешения, и **EXECUTE** разрешения на **sp_delete_ backuphistory**хранимой процедуры.  
  
## <a name="examples"></a>Примеры  
 В следующем примере [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] приостанавливается в том экземпляре, в котором выполняется пример.  
  
```  
Use msdb;  
GO  
EXEC managed_backup.sp_master_switch @state=0;  
Go  
  
```  
  
 В следующем примере [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] возобновляется.  
  
```  
Use msdb;  
GO  
EXEC managed_backup.sp_master_switch @state=1;  
Go  
  
```  
  
## <a name="see-also"></a>См. также:  
 [Управляемое резервное копирование SQL Server в Microsoft Azure](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)  
  
  