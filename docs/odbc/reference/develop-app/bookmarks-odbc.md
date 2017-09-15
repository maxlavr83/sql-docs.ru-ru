---
title: "Закладки (ODBC) | Документы Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- result sets [ODBC], bookmarks
- bookmarks [ODBC]
ms.assetid: 1d7cccc5-f847-4321-b240-28570854ee5c
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 791350c93e2570ad8615e5b378e9979870e02acf
ms.contentlocale: ru-ru
ms.lasthandoff: 09/09/2017

---
# <a name="bookmarks-odbc"></a>Закладки (ODBC)
Закладка представляет собой значение, используемое для идентификации строки данных. Содержание значения закладки понятно только драйверу или источнику данных. Например, оно может быть простым (номером строки) или сложным (адрес на диске). Закладки в ODBC, немного отличаются от закладки в реальном книг. В реальной книги средство чтения помещает закладки на конкретной странице, а затем поиск эту закладку, чтобы вернуться на страницу. В ODBC приложение запрашивает закладку для конкретной строки, сохраняет ее и передает обратно курсору для возврата к строке. Таким образом закладки в ODBC аналогичны чтения, записывая номера страницы запоминание его, а затем выполните поиск страницы.  
  
 Чтобы определить драйверы закладок, приложение вызывает **SQLGetInfo** с параметром SQL_BOOKMARK_PERSISTENCE. Биты в это значение описывают, какие операции закладки сохранятся после сборки, например закладки, по-прежнему действительны ли после закрытия курсора.  
  
 Этот раздел содержит следующие подразделы.  
  
-   [Типы закладки](../../../odbc/reference/develop-app/bookmark-types.md)  
  
-   [Извлечение закладки](../../../odbc/reference/develop-app/retrieving-bookmarks.md)  
  
-   [Прокрутка по закладке](../../../odbc/reference/develop-app/scrolling-by-bookmark.md)  
  
-   [Обновление, удаление или выборка по закладке](../../../odbc/reference/develop-app/updating-deleting-or-fetching-by-bookmark.md)  
  
-   [Сравнение закладки](../../../odbc/reference/develop-app/comparing-bookmarks.md)