---
title: Способы реализации курсоров | Документация Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, cursors
- ODBC cursors, about ODBC cursors
- ODBC applications, cursors
- cursors [ODBC], about ODBC cursors
ms.assetid: 2b1d7dd4-08a4-43fc-b3eb-70c183d0941f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4c92391b1d8874da3a8901ccc5c6245e48334241
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/02/2018
ms.locfileid: "48155724"
---
# <a name="how-cursors-are-implemented"></a>Способы реализации курсоров
  Приложения ODBC управляют поведением курсора путем задания одного или нескольких атрибутов инструкции перед выполнением инструкции SQL. ODBC может указывать характеристики курсора двумя разными способами.  
  
-   Тип курсора  
  
     Типы курсора задаются при помощи атрибута SQL_ATTR_CURSOR_TYPE [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md). Типы курсора ODBC бывают с последовательным доступом, статические, управляемые набором ключей, смешанные и динамические. Изначально метод указания курсоров в ODBC заключался в задании типа курсора.  
  
-   Режим работы курсоров  
  
     Режим работы курсоров задается с помощью атрибутов SQL_ATTR_CURSOR_SCROLLABLE и SQL_ATTR_CURSOR_SENSITIVITY **SQLSetStmtAttr**. Эти атрибуты смоделированы на ключевых словах SCROLL и SENSITIVE, которые в стандартах ISO определены для инструкции DECLARE CURSOR. Два этих параметра ISO появились в ODBC версии 3.0.  
  
 Характеристики курсора ODBC следует указывать с помощью одного из этих методов; при этом предпочтительнее использовать типы курсоров ODBC.  
  
 Помимо установки типа курсора приложения ODBC также задают и другие параметры, например число строк, возвращаемое при каждом извлечении, параметры параллелизма, а также уровни изоляции транзакции. Эти параметры можно задавать для курсоров в стиле ODBC (с последовательным доступом, статических, управляемых набором ключей, смешанных и динамических) или курсоров в стиле ISO (прокручиваемость и чувствительность).  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Драйвер ODBC для собственного клиента поддерживает несколько способов физической реализации курсоров различных типов. Некоторые типы курсоров драйвер реализует с помощью результирующего набора [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] по умолчанию; другие курсоры реализуются им как серверные курсоры либо при помощи библиотеки курсоров ODBC.  
  
## <a name="in-this-section"></a>в этом разделе  
  
-   [Использование результирующих наборов по умолчанию в SQL Server](using-sql-server-default-result-sets.md)  
  
-   [Использование серверных курсоров](using-server-cursors.md)  
  
-   [Библиотека курсоров ODBC](odbc-cursor-library.md)  
  
## <a name="see-also"></a>См. также  
 [Использование курсоров &#40;ODBC&#41;](../using-cursors-odbc.md)  
  
  
