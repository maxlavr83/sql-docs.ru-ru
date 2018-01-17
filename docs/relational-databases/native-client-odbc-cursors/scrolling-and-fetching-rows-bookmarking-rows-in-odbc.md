---
title: "Создание закладок строк в ODBC | Документы Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-cursors
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- cursors [ODBC], fetching rows
- ODBC cursors, fetching rows
- cursors [ODBC], scrolling rows
- ODBC cursors, scrolling rows
- bookmarks [ODBC]
ms.assetid: 9cfcd243-c9d4-4c2a-abc4-399dbabe5f6b
caps.latest.revision: "31"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ecae2c00d4e8b1ca66382aeabf2b29171db7031c
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/08/2018
---
# <a name="scrolling-and-fetching-rows---bookmarking-rows-in-odbc"></a>Прокрутка и выборка строки - закладок строк в ODBC
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Закладка представляет собой значение, используемое для идентификации строки данных. Содержание значения закладки понятно только драйверу или источнику данных. Например, оно может быть простым (номером строки) или сложным (адрес на диске). В ODBC приложение запрашивает закладку для конкретной строки, сохраняет ее и передает обратно курсору для возврата к строке.  
  
 При выборке строк через [SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md), приложение может использовать закладку в качестве основы для выборки начальной строки. Такой способ представляет собой форму абсолютной адресации, поскольку не зависит от текущей позиции курсора. Для прокрутки в строке с закладкой, приложение вызывает **SQLFetchScroll** с *FetchOrientation* из SQL_FETCH_BOOKMARK. Эта операция использует закладку, на которую указывает атрибут параметра SQL_ATTR_FETCH_BOOKMARK_PTR. Она возвращает набор строк, начинающийся со строки, определяемой закладкой. Приложение может указать смещение для этой операции в *FetchOffset* аргумент при вызове для **SQLFetchScroll**. При указании смещения первая строка возвращаемого набора строк определяется сложением числа в аргументе FetchOffset с номером строки, определяемой закладкой. Поставщик OLE DB для собственного клиента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] поддерживает только закладки в статических курсорах и курсорах, управляемых набором ключей. Если при включенных закладках запрошен динамический курсор, то вместо него открывается курсор, управляемый набором ключей.  
  
 Закладки могут также использоваться с **SQLBulkOperations** функцию для выполнения операций над набором строк, начиная с закладки.  
  
## <a name="see-also"></a>См. также:  
 [Прокрутка и выборка строк](../../relational-databases/native-client-odbc-cursors/scrolling-and-fetching-rows.md)  
  
  