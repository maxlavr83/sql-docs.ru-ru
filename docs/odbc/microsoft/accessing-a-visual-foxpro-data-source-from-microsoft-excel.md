---
title: "Доступ к источникам данных Visual FoxPro из Microsoft Excel | Документы Microsoft"
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
- FoxPro ODBC driver [ODBC], Excel
- Visual FoxPro data [ODBC], Excel
- Visual FoxPro data [ODBC], accessing
- Visual FoxPro ODBC driver [ODBC], Excel
ms.assetid: 2c143020-0403-4592-80e0-84229f3d40be
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 085ab9bd928d7a25bd5d9e1d75f3355bdad0fd8e
ms.contentlocale: ru-ru
ms.lasthandoff: 09/09/2017

---
# <a name="accessing-a-visual-foxpro-data-source-from-microsoft-excel"></a>Доступ к источникам данных Visual FoxPro из Microsoft Excel
Если у вас установлен Microsoft Query, можно создать источник данных в Microsoft Excel, который подключается к данным Visual FoxPro.  
  
### <a name="to-access-visual-foxpro-data-from-microsoft-excel"></a>Доступ к данным Visual FoxPro из Microsoft Excel  
  
1.  Откройте электронную таблицу Microsoft Excel.  
  
2.  В меню Данные выберите внешние данные. Откроется Microsoft Query.  
  
3.  В диалоговом окне Выбор источника данных выберите другой.  
  
4.  В диалоговом окне Источники данных ODBC нажмите кнопку "Создать".  
  
5.  В диалоговом окне Добавить источник данных выберите в поле со списком установить драйверы ODBC драйвера Microsoft Visual FoxPro и нажмите кнопку ОК.  
  
6.  В [диалоговое окно установки Visual FoxPro ODBC](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md), введите имя источника данных, выберите тип базы данных, введите путь к базе данных или каталог и нажмите кнопку ОК.  
  
     Имя источника данных отображается в текстовом поле введите источник данных диалогового окна "Источники данных ODBC".  
  
7.  Нажмите кнопку «ОК».  
  
     Имя источника данных выбран в текстовом поле доступные источники данных с помощью диалогового окна Выбор источника данных.  
  
8.  Вариант.  
  
 Теперь можно добавить таблицы, чтобы открыть запрос. Дополнительные сведения о построении запроса см. в разделе [импорта данных в Microsoft Excel из базы данных Visual FoxPro](../../odbc/microsoft/importing-data-into-microsoft-excel-from-a-visual-foxpro-database.md).