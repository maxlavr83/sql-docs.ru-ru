---
title: sp_help_agent_default (Transact-SQL) | Документация Майкрософт
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_help_agent_default
- sp_help_agent_default_TSQL
helpviewer_keywords:
- sp_help_agent_default
ms.assetid: 7ba55e39-05dd-43c7-b5da-b268ed8426dd
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9ee9596b578396786da8562f2ecf73c3b85f0241
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/18/2018
ms.locfileid: "53588038"
---
# <a name="sphelpagentdefault-transact-sql"></a>sp_help_agent_default (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Извлекает идентификатор конфигурации по умолчанию для типа агента, переданного в качестве аргумента. Эта хранимая процедура выполняется на распространителе в любой базе данных.  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
sp_help_agent_default [ @profile_id= ] profile_id OUTPUT   
        , [ @agent_type = ] agent_type  
```  
  
## <a name="arguments"></a>Аргументы  
 [  **@profile_id=**] _profile_id_**выходных данных**  
 Идентификатор конфигурации по умолчанию для типа агента. *profile_id* — **int**, не имеет значения по умолчанию. *profile_id* также является параметром OUTPUT и возвращает идентификатор конфигурации по умолчанию для типа агента.  
  
 [  **@agent_type=**] **"**_agent_type_**"**  
 Тип агента. *agent_type* — **int**, по умолчанию и может принимать одно из следующих значений.  
  
|Значение|Описание|  
|-----------|-----------------|  
|**1**|Агент моментальных снимков.|  
|**2**|Агент чтения журнала.|  
|**3**|Агент распространителя.|  
|**4**|Агент слияния.|  
|**9**|Агент чтения очереди.|  
  
## <a name="return-code-values"></a>Значения кода возврата  
 **0** (успешное завершение) или **1** (неуспешное завершение)  
  
## <a name="remarks"></a>Примечания  
 **sp_help_agent_default** используется во всех типах репликации.  
  
## <a name="permissions"></a>Разрешения  
 Только члены **sysadmin** предопределенной роли сервера или **replmonitor** предопределенной роли базы данных могут выполнять процедуру **sp_help_agent_default**.  
  
## <a name="see-also"></a>См. также  
 [Системные хранимые процедуры (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
