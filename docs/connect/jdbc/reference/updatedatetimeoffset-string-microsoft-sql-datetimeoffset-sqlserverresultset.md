---
title: "updateDateTimeOffset(string) (SQLServerResultSet) | Документы Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 952947ce-7c6e-4364-b035-46cb7fe621b2
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ee7ddcee503aff8481b5c996fcb59f7e1ac50e2a
ms.contentlocale: ru-ru
ms.lasthandoff: 09/09/2017

---
# <a name="updatedatetimeoffsetstring-microsoftsqldatetimeoffset-sqlserverresultset"></a>updateDateTimeOffset(string, microsoft.sql.DateTimeOffset) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Этот метод добавлен в [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] версии 3.0 драйвера JDBC.  
  
 Обновляет значение указанного столбца [класс DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md) значение с заданным именем столбца.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
public void updateDateTimeOffset(String columnName, microsoft.sql.DateTimeOffset x)  
```  
  
#### <a name="parameters"></a>Параметры  
 *columnName*  
  
 Имя столбца.  
  
 *x*  
  
 Объект [класс DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md) объекта.  
  
## <a name="exceptions"></a>Исключения  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Замечания  
 Вы можете получить [класс DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md) значение с [SQLServerResultSet.getDateTimeOffset](../../../connect/jdbc/reference/getdatetimeoffset-sqlserverresultset.md).  
  
## <a name="see-also"></a>См. также:  
 [метод updateDateTimeOffset &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/updatedatetimeoffset-sqlserverresultset.md)   
 [Элементы SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Класс SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  