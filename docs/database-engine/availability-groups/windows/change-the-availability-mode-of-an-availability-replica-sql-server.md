---
title: Смена режима доступности для реплики доступности (SQL Server) | Документы Майкрософт
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], deploying
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], availability modes
ms.assetid: c4da8f25-fb1b-45a4-8bf2-195df6df634c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6afbefc04c2495c3f7a08cc0c6d73a4d1ba28880
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/01/2018
ms.locfileid: "47610162"
---
# <a name="change-the-availability-mode-of-an-availability-replica-sql-server"></a>Смена режима доступности для реплики доступности (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  В этом разделе описывается изменение режима доступности для реплики доступности в группе доступности AlwaysOn в [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] с помощью среды [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]или PowerShell. Режим доступности — это свойство реплики, которое определяет, происходит в ней синхронная или асинхронная фиксация. *Режим асинхронной фиксации* увеличивает производительность за счет средств высокого уровня доступности и поддерживает только принудительный переход на другой ресурс вручную (с возможной потерей данных), который обычно называется *принудительной отработкой отказа*. *Режим синхронной фиксации* обеспечивает высокий уровень доступности за счет производительности и после завершения синхронизации вторичной реплики поддерживает как автоматическую отработку отказа, так и отработку отказа вручную.  
  
-   **Перед началом работы**  
  
     [Предварительные требования](#Prerequisites)  
  
     [безопасность](#Security)  
  
-   **Смена режима доступности для реплики доступности с помощью следующего:**  
  
     [Среда SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
##  <a name="BeforeYouBegin"></a> Перед началом  
  
###  <a name="Prerequisites"></a> Предварительные требования  
  
-   Необходимо подключиться к экземпляру сервера, на котором размещена первичная реплика.  
  
###  <a name="Security"></a> безопасность  
  
####  <a name="Permissions"></a> Permissions  
 Необходимо разрешение ALTER AVAILABILITY GROUP для группы доступности, разрешение CONTROL AVAILABILITY GROUP, разрешение ALTER ANY AVAILABILITY GROUP или разрешение CONTROL SERVER.  
  
##  <a name="SSMSProcedure"></a> Использование среды SQL Server Management Studio  
 **Изменение режима доступности для группы доступности**  
  
1.  В обозревателе объектов подключитесь к экземпляру сервера, на котором размещена первичная реплика, и разверните дерево сервера.  
  
2.  Разверните узел **Высокий уровень доступности AlwaysOn** и узел **Группы доступности** .  
  
3.  Щелкните группу доступности, реплику которой нужно изменить.  
  
4.  Щелкните правой кнопкой мыши реплику и выберите пункт **Свойства**.  
  
5.  В диалоговом окне **Свойства реплики доступности** измените режим доступности для этой реплики с помощью раскрывающегося списка **Режим доступности** .  
  
##  <a name="TsqlProcedure"></a> Использование Transact-SQL  
 **Изменение режима доступности для группы доступности**  
  
1.  Подключитесь к экземпляру сервера, на котором находится первичная реплика.  
  
2.  Инструкция [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md) используется следующим образом:  
  
     ALTER AVAILABILITY GROUP *имя_группы* MODIFY REPLICA ON '*имя_сервера*'  
  
     WITH ( {  
  
     AVAILABILITY_MODE = { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT }  
  
     | FAILOVER_MODE = { AUTOMATIC | MANUAL }  
  
     } )  
  
     где *имя_группы* — это имя группы доступности, а *имя_сервера* — это имя экземпляра сервера, на котором размещена реплика, которую требуется изменить.  
  
    > [!NOTE]  
    >  FAILOVER_MODE = AUTOMATIC поддерживается, только если указан параметр AVAILABILITY_MODE = SYNCHRONOUS_COMMIT.  
  
     В следующем примере, введенном на первичной реплике группы доступности `AccountsAG` , выполняется изменение режимов доступности и отработки отказа на синхронную фиксацию и автоматический переход на другой ресурс соответственно для реплики, размещенной на экземпляре сервера `INSTANCE09` .  
  
    ```  
  
    ALTER AVAILABILITY GROUP AccountsAG MODIFY REPLICA ON 'INSTANCE09'  
       WITH (AVAILABILITY_MODE = SYNCHRONOUS_COMMIT);  
    ALTER AVAILABILITY GROUP AccountsAG MODIFY REPLICA ON 'INSTANCE09'  
       WITH (FAILOVER_MODE = AUTOMATIC);  
    ```  
  
##  <a name="PowerShellProcedure"></a> Использование PowerShell  
 **Изменение режима доступности для группы доступности**  
  
1.  Перейдите в каталог (**cd**) экземпляра сервера, в котором находится первичная реплика.  
  
2.  Используйте командлет **Set-SqlAvailabilityReplica** с параметром **AvailabilityMode** и при необходимости параметром **FailoverMode** .  
  
     Например, следующая команда изменяет реплику `MyReplica` в группе доступности `MyAg` , устанавливая использование режима доступности с синхронной фиксацией и поддержку автоматического перехода на другой ресурс.  
  
    ```  
    Set-SqlAvailabilityReplica -AvailabilityMode "SynchronousCommit" -FailoverMode "Automatic" `   
    -Path SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAg\AvailabilityReplicas\MyReplica  
    ```  
  
    > [!NOTE]  
    >  Чтобы просмотреть синтаксис командлета, воспользуйтесь командлетом **Get-Help** в среде PowerShell [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Дополнительные сведения см. в разделе [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md).  
  
 **Настройка и использование поставщика SQL Server PowerShell**  
  
-   [Поставщик SQL Server PowerShell](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
## <a name="see-also"></a>См. также:  
 [Обзор групп доступности AlwaysOn (SQL Server)](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Режимы доступности (группы доступности AlwaysOn)](../../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md)   
 [Отработка отказа и режимы отработки отказа (группы доступности AlwaysOn)](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)  
  
  
