---
title: "Удаление расширенной хранимой процедуры из SQL Server | Документы Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: extended-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- deleting extended stored procedures
- removing extended stored procedures
- extended stored procedures [SQL Server], removing
- dropping extended stored procedures
ms.assetid: 7827e574-3f59-4279-9a9b-532582e041cb
caps.latest.revision: "37"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 147091aee873f0c9b15c3b9934b8daf6c3acbe8a
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/08/2018
---
# <a name="removing-an-extended-stored-procedure-from-sql-server"></a>Удаление расширенной хранимой процедуры из SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Пользуйтесь вместо этого интеграцией со средой CLR.  
  
 Чтобы удалить каждую функцию расширенной хранимой процедуры в пользовательской расширенной хранимой процедуры библиотеки DLL, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] системный администратор должен выполнить **sp_dropextendedproc** системную хранимую процедуру, указав имя функции и имя библиотеки DLL, в которой размещается функция. Например, эта команда удаляет функцию **xp_hello**, расположенную в DLL-Библиотеки xp_hello.dll из [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
```  
sp_dropextendedproc 'xp_hello'  
```  
  
 Начиная с версии [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], **sp_dropextendedproc** не удаляет Системные расширенные хранимые процедуры. Вместо этого системный администратор должен запретить разрешение EXECUTE на расширенную хранимую процедуру, чтобы **открытый** роли.  
  
## <a name="see-also"></a>См. также:  
 [sp_dropextendedproc &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)  
  
  