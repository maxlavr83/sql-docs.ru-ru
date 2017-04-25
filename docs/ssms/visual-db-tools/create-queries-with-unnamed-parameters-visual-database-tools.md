---
title: "Создание запросов с неименованными параметрами (визуальные инструменты для баз данных) | Документация Майкрософт"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- unnamed parameters
- parameters [SQL Server], unnamed
ms.assetid: 5f4b664b-3d3d-4d07-a0e7-791d78743504
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: cf0454412324ef88c645854dab9563eeee531b64
ms.lasthandoff: 04/11/2017

---
# <a name="create-queries-with-unnamed-parameters-visual-database-tools"></a>Создание запросов с неименованными параметрами (визуальные инструменты для баз данных)
Запросы с неименованными параметрами создаются с указанием вопросительного знака (?) в качестве заполнителя литерала. Конструктор запросов и представлений присваивает такому параметру временное имя. В запросе можно указать любое число неименованных параметров.  
  
При запуске запроса в конструкторе запросов и представлений в диалоговом окне параметров запроса отображается временное имя.  
  
### <a name="to-specify-an-unnamed-parameter"></a>Указание неименованного параметра  
  
1.  Добавьте столбцы или выражения, для которых нужно произвести поиск, на [панель критериев](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md). Если столбцы или выражения поиска не нужно включать в результат запроса, их необходимо удалить из списка выходных столбцов.  
  
2.  Укажите строку, в которой содержится столбец данных или выражение для поиска, и в столбце сетки **Фильтр** введите вопросительный знак (?).  
  
    По умолчанию конструктор запросов и представлений добавляет оператор «=». Однако можно отредактировать ячейку и заменить его на оператор «>», «<» или любой другой оператор сравнения языка SQL.  
  
## <a name="see-also"></a>См. также:  
[Запрос с параметрами (визуальные инструменты для баз данных)](../../ssms/visual-db-tools/query-with-parameters-visual-database-tools.md)  
  
