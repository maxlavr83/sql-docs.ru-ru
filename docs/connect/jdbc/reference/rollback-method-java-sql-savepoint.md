---
title: "Метод Rollback (java.sql.Savepoint) | Документы Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerConnection.rollback (java.sql.Savepoint)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d5dbd9ef-194f-4130-bfcc-7901a4fa8ded
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0b774454bdd981decb1a2f40be43550b2bdd3272
ms.contentlocale: ru-ru
ms.lasthandoff: 09/09/2017

---
# <a name="rollback-method-javasqlsavepoint"></a>Метод rollback (java.sql.Savepoint)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Отменяет все изменения, внесенные после заданного [SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md) был установлен объект.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
public void rollback(java.sql.Savepoint s)  
```  
  
#### <a name="parameters"></a>Параметры  
 *s*  
  
 Объект точки сохранения для отката.  
  
## <a name="exceptions"></a>Исключения  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Замечания  
 Этот метод rollBack указывается с помощью отката метода в интерфейсе java.sql.Connection.  
  
 Этот метод следует использовать, только если отключен режим автоматической фиксации.  
  
## <a name="see-also"></a>См. также:  
 [Метод Rollback &#40; SQLServerConnection &#41;](../../../connect/jdbc/reference/rollback-method-sqlserverconnection.md)   
 [Элементы SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Класс SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  