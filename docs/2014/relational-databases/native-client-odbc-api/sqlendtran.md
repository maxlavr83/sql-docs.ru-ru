---
title: SQLEndTran | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLEndTran function
ms.assetid: 95cff841-c2d5-4e1e-a18d-f3d4696a5b85
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f5425fdc189febd23e9fc61765f4ad56fe484111
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/13/2018
ms.locfileid: "53364156"
---
# <a name="sqlendtran"></a>SQLEndTran
  По умолчанию драйвер ODBC для собственного клиента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] закрывает связанный с инструкцией курсор в момент фиксации или отката транзакции функцией **SQLEndTran** . Серверные курсоры закрываются, если они не являются статическими. Когда **SQLEndTran** производит фиксацию или откат операции, поведение курсора, связанного с инструкцией, определяется значением определяемого драйвером соединения ODBC атрибута SQL_COPT_SS_PRESERVE_CURSORS, установленного при помощи функции [SQLSetConnectAttr](sqlsetconnectattr.md).  
  
## <a name="see-also"></a>См. также  
 [Сведения о реализации API ODBC](odbc-api-implementation-details.md)   
 [Функция SQLEndTran](https://go.microsoft.com/fwlink/?LinkId=59342)  
  
  
