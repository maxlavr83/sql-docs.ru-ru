---
title: 'Активные вторичные реплики: Резервное копирование во вторичных репликах (группы доступности AlwaysOn) | Документация Майкрософт'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- backup priority
- backup on secondary replicas
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], backup on secondary replicas
- active secondary replicas [SQL Server], backup on
- automated backup preference
- Availability Groups [SQL Server], active secondary replicas
ms.assetid: 82afe51b-71d1-4d5b-b20a-b57afc002405
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a94db154042f2cc6314459b6af4b52a43c2c9966
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/02/2018
ms.locfileid: "48186974"
---
# <a name="active-secondaries-backup-on-secondary-replicas-always-on-availability-groups"></a>Активные вторичные реплики, резервное копирование во вторичных репликах (группы доступности AlwaysOn)
  Функции [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] по поддержке вторичных реплик обеспечивают выполнение операций резервного копирования для вторичных реплик. Операции резервного копирования могут оказывать значительную нагрузку на систему ввода-вывода и ЦП (при использовании сжатия резервных копий). Перенос резервного копирования в синхронизированную или синхронизирующуюся вторичную реплику позволяет использовать ресурсы на экземпляре сервера, где размещается первичная реплика, для рабочей нагрузки первого уровня.  
  
> [!NOTE]  
>  Инструкция RESTORE недопустима для базы данных-источника или базы данных-получателя группы доступности.  
  
  
  
##  <a name="SupportedBuTypes"></a> Поддерживаемые типы резервного копирования на вторичных репликах  
  
-   `BACKUP DATABASE` поддерживает только полные, доступные только для копирования резервные копии баз данных, файлов и файловых групп, которые выполняются во вторичных репликах. Обратите внимание, что резервные копии, доступные только для копирования, не влияют на цепочку журналов и не очищают битовую карту разностного резервного копирования.  
  
-   Разностные резервные копии не поддерживаются во вторичных репликах.  
  
-   **BACKUP LOG** поддерживает только обычное резервное копирование журналов (параметр COPY_ONLY не поддерживается для резервных копий журналов во вторичных репликах).  
  
     Обеспечивается последовательная цепочка журналов по всем резервным копиям журналов в любой реплике (первичной или вторичной) независимо от их режима доступности (синхронной или асинхронной фиксации).  
  
-   Для резервного копирования базы данных-получателя, необходимо иметь возможность взаимодействовать с первичной репликой вторичной репликой и должен быть `SYNCHRONIZED` или `SYNCHRONIZING`.  
  
##  <a name="WhereBuJobsRun"></a> Настройка места выполнения заданий резервного копирования  
 Выполнение резервного копирования во вторичной реплике для снятия рабочей нагрузки резервного копирования с основного рабочего сервера обеспечивает значительные преимущества. Однако выполнение резервного копирования на вторичных репликах создает значительные сложности в процессе определения, где должны запускаться задания резервного копирования. Для решения этой проблемы настройте расположение запуска заданий резервного копирования, как описано далее.  
  
1.  Настройте группу доступности, чтобы указать, на каких репликах доступности предпочтительно проведение резервного копирования. Дополнительные сведения см. в описании параметров *AUTOMATED_BACKUP_PREFERENCE* и *BACKUP_PRIORITY* в разделе [CREATE AVAILABILITY GROUP (Transact-SQL)](/sql/t-sql/statements/create-availability-group-transact-sql) или [ALTER AVAILABILITY GROUP (Transact-SQL)](/sql/t-sql/statements/alter-availability-group-transact-sql).  
  
2.  Создайте скрипты заданий резервного копирования для каждой из баз данных доступности на каждом экземпляре сервера, на котором размещается реплика доступности, потенциально используемая для выполнения резервного копирования. Дополнительные сведения см. в подразделе "Дальнейшие действия. После настройки резервного копирования во вторичных репликах" раздела [Настройка резервного копирования в репликах доступности (SQL Server)](configure-backup-on-availability-replicas-sql-server.md).  
  
##  <a name="RelatedTasks"></a> Связанные задачи  
 **Настройка резервного копирования во вторичных репликах**  
  
-   [Настройка резервного копирования в репликах доступности (SQL Server)](configure-backup-on-availability-replicas-sql-server.md)  
  
 **Определение, является ли текущая реплика предпочитаемой репликой резервного копирования**  
  
-   [sys.fn_hadr_backup_is_preferred_replica](/sql/relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql)  
  
 **Создание задания резервного копирования**  
  
-   [Использование мастера планов обслуживания](../../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md)  
  
-   [Реализация заданий](../../../ssms/agent/implement-jobs.md)  
  
  
## <a name="see-also"></a>См. также  
 [Обзор групп доступности AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Резервные копии только для копирования (SQL Server)](../../../relational-databases/backup-restore/copy-only-backups-sql-server.md)   
 [CREATE AVAILABILITY GROUP (Transact-SQL)](/sql/t-sql/statements/create-availability-group-transact-sql)   
 [ALTER AVAILABILITY GROUP (Transact-SQL)](/sql/t-sql/statements/alter-availability-group-transact-sql)  
  
  
