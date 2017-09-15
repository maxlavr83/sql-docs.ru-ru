---
title: "SUM (Transact-SQL) | Документы Microsoft"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SUM
- SUM_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- values [SQL Server], sum of all
- SUM function [Transact-SQL]
- values [SQL Server]
- summation [SQL Server]
- expressions [SQL Server], sum of all values
- DISTINCT keyword
- totals [SQL Server], SUM
- summary values [SQL Server]
ms.assetid: 9af94d0f-55d4-428f-a840-ec530160f379
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2bfa411dc054ea6996a8d8eb6b2ed53c6253d1b9
ms.contentlocale: ru-ru
ms.lasthandoff: 09/01/2017

---
# <a name="sum-transact-sql"></a>SUM (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Возвращает сумму всех, либо только уникальных, значений в выражении. Функция SUM может быть использована только для числовых столбцов. Значения NULL пропускаются.  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
SUM ( [ ALL | DISTINCT ] expression )  
   OVER ( [ partition_by_clause ] order_by_clause )    
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
SUM ( [ ALL | DISTINCT ] expression )  
```  
  
## <a name="arguments"></a>Аргументы  
 ALL  
 Применяет агрегатную функцию ко всем значениям. ALL является параметром по умолчанию.  
  
 DISTINCT  
 Указывает, что функция SUM возвращает сумму только уникальных значений.  
  
 *expression*  
 Может быть константой, столбцом или функцией, а также любым сочетанием арифметических, побитовых и строковых операторов. *выражение* является выражением категории типа точных числовых или приблизительных числовых данных, за исключением **бит** тип данных. Агрегатные функции и вложенные запросы не допускаются. Дополнительные сведения см. в разделе [Выражения (Transact-SQL)](../../t-sql/language-elements/expressions-transact-sql.md).  
  
 НАД **(** [ *partition_by_clause* ] *order_by_clause***)**  
 *partition_by_clause* Делит результирующий набор, полученный с помощью предложения FROM, на секции, к которым применяется функция. Если этот параметр не указан, функция обрабатывает все строки результирующего набора запроса как отдельные группы. *order_by_clause* , определяет логический порядок, в котором выполняется операция. *order_by_clause* является обязательным. Дополнительные сведения см. в разделе [предложение OVER &#40; Transact-SQL &#41; ](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
## <a name="return-types"></a>Типы возвращаемых значений  
 Возвращает сумму всех *выражение* значения в наиболее точном *выражение* тип данных.  
  
|Результат выражения|Возвращаемый тип|  
|-----------------------|-----------------|  
|**tinyint**|**int**|  
|**smallint**|**int**|  
|**ssNoversion**|**int**|  
|**bigint**|**bigint**|  
|**десятичное число** категории (p, s)|**Decimal (38, s)**|  
|**Money** и **smallmoney** категории|**money**|  
|**число с плавающей запятой** и **реальные** категории|**float**|  
  
## <a name="remarks"></a>Замечания  
 SUM — это детерминированная функция, если она используется без предложений OVER и ORDER BY. Она не детерминирована при использовании с предложениями OVER и ORDER BY. Дополнительные сведения см. в разделе [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
## <a name="examples"></a>Примеры  
  
### <a name="a-using-sum-to-return-summary-data"></a>A. Использование SUM для возвращения сводных данных  
 В следующих примерах показано использование функции SUM для возвращения данных в базе данных [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
SELECT Color, SUM(ListPrice), SUM(StandardCost)  
FROM Production.Product  
WHERE Color IS NOT NULL   
    AND ListPrice != 0.00   
    AND Name LIKE 'Mountain%'  
GROUP BY Color  
ORDER BY Color;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Color`  
  
 `--------------- --------------------- ---------------------`  
  
 `Black           27404.84              5214.9616`  
  
 `Silver          26462.84              14665.6792`  
  
 `White           19.00                 6.7926`  
  
 `(3 row(s) affected)`  
  
### <a name="b-using-the-over-clause"></a>Б. Использование предложения OVER  
 В следующем примере показано использование функции SUM с предложением OVER для представления суммарного объема годовых продаж на каждой территории в таблице `Sales.SalesPerson` в базе данных [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. Данные секционируются по `TerritoryID` и логически сортируются по `SalesYTD`. Это означает, что функция SUM вычисляется для каждой территории на основании продаж за год. Обратите внимание, что в `TerritoryID` 1 для продаж за 2005 год используются две строки, в которых представлены два менеджера по продажам с показателями за этот год. После расчета суммарного значения продаж для двух данных строк в вычисление включается третья строка, представляющая продажи за 2006 год.  
  
```  
SELECT BusinessEntityID, TerritoryID   
   ,DATEPART(yy,ModifiedDate) AS SalesYear  
   ,CONVERT(varchar(20),SalesYTD,1) AS  SalesYTD  
   ,CONVERT(varchar(20),AVG(SalesYTD) OVER (PARTITION BY TerritoryID   
                                            ORDER BY DATEPART(yy,ModifiedDate)   
                                           ),1) AS MovingAvg  
   ,CONVERT(varchar(20),SUM(SalesYTD) OVER (PARTITION BY TerritoryID   
                                            ORDER BY DATEPART(yy,ModifiedDate)   
                                            ),1) AS CumulativeTotal  
FROM Sales.SalesPerson  
WHERE TerritoryID IS NULL OR TerritoryID < 5  
ORDER BY TerritoryID,SalesYear;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
BusinessEntityID TerritoryID SalesYear   SalesYTD             MovingAvg            CumulativeTotal  
---------------- ----------- ----------- -------------------- -------------------- --------------------  
274              NULL        2005        559,697.56           559,697.56           559,697.56  
287              NULL        2006        519,905.93           539,801.75           1,079,603.50  
285              NULL        2007        172,524.45           417,375.98           1,252,127.95  
283              1           2005        1,573,012.94         1,462,795.04         2,925,590.07  
280              1           2005        1,352,577.13         1,462,795.04         2,925,590.07  
284              1           2006        1,576,562.20         1,500,717.42         4,502,152.27  
275              2           2005        3,763,178.18         3,763,178.18         3,763,178.18  
277              3           2005        3,189,418.37         3,189,418.37         3,189,418.37  
276              4           2005        4,251,368.55         3,354,952.08         6,709,904.17  
281              4           2005        2,458,535.62         3,354,952.08         6,709,904.17  
  
(10 row(s) affected)  
  
```  
  
 В этом примере предложение OVER не включает в себя предложение PARTITION BY. Это означает, что функция будет применяться для всех строк, возвращаемых запросом. Предложение ORDER BY, указанное в предложении OVER, определяет логический порядок применения функции SUM. Запрос возвращает суммарное общее значение продаж за год для всех территорий, указанных в предложении WHERE. Предложение ORDER BY, указанное в инструкции SELECT, определяет порядок отображения строк запроса.  
  
```  
SELECT BusinessEntityID, TerritoryID   
   ,DATEPART(yy,ModifiedDate) AS SalesYear  
   ,CONVERT(varchar(20),SalesYTD,1) AS  SalesYTD  
   ,CONVERT(varchar(20),AVG(SalesYTD) OVER (ORDER BY DATEPART(yy,ModifiedDate)   
                                            ),1) AS MovingAvg  
   ,CONVERT(varchar(20),SUM(SalesYTD) OVER (ORDER BY DATEPART(yy,ModifiedDate)   
                                            ),1) AS CumulativeTotal  
FROM Sales.SalesPerson  
WHERE TerritoryID IS NULL OR TerritoryID < 5  
ORDER BY SalesYear;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
BusinessEntityID TerritoryID SalesYear   SalesYTD             MovingAvg            CumulativeTotal  
---------------- ----------- ----------- -------------------- -------------------- --------------------  
274              NULL        2005        559,697.56           2,449,684.05         17,147,788.35  
275              2           2005        3,763,178.18         2,449,684.05         17,147,788.35  
276              4           2005        4,251,368.55         2,449,684.05         17,147,788.35  
277              3           2005        3,189,418.37         2,449,684.05         17,147,788.35  
280              1           2005        1,352,577.13         2,449,684.05         17,147,788.35  
281              4           2005        2,458,535.62         2,449,684.05         17,147,788.35  
283              1           2005        1,573,012.94         2,449,684.05         17,147,788.35  
284              1           2006        1,576,562.20         2,138,250.72         19,244,256.47  
287              NULL        2006        519,905.93           2,138,250.72         19,244,256.47  
285              NULL        2007        172,524.45           1,941,678.09         19,416,780.93  
(10 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Примеры: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] и[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-a-simple-sum-example"></a>В. Простой пример SUM  
 Следующий пример возвращает общее количество каждый продукт, проданный в 2003 году.  
  
```  
-- Uses AdventureWorks  
  
SELECT ProductKey, SUM(SalesAmount) AS TotalPerProduct  
FROM dbo.FactInternetSales  
WHERE OrderDateKey >= '20030101'   
      AND OrderDateKey < '20040101'  
GROUP BY ProductKey  
ORDER BY ProductKey;  
  
```  
  
 Здесь приводится частичный результирующий набор.  
  
 `ProductKey  TotalPerProduct`  
  
 `----------  ---------------`  
  
 `214         31421.0200`  
  
 `217         31176.0900`  
  
 `222         29986.4300`  
  
 `225          7956.1500`  
  
### <a name="d-calculating-group-totals-with-more-than-one-column"></a>Г. Вычисление общей суммы значений с более чем один столбец  
 В следующем примере производится вычисление суммы значений столбцов `ListPrice` и `StandardCost` для каждого из значений цвета, указанных в таблице `Product`.  
  
```  
-- Uses AdventureWorks  
  
SELECT Color, SUM(ListPrice)AS TotalList,   
       SUM(StandardCost) AS TotalCost  
FROM dbo.DimProduct  
GROUP BY Color  
ORDER BY Color;  
```  
  
 Первая часть результирующего набора, показано ниже:  
  
 `Color       TotalList      TotalCost`  
  
 `----------  -------------  --------------`  
  
 `Black       101295.7191    57490.5378`  
  
 `Blue         24082.9484    14772.0524`  
  
 `Grey           125.0000       51.5625`  
  
 `Multi          880.7468      526.4095`  
  
 `NA            3162.3564     1360.6185`  
  
## <a name="see-also"></a>См. также:  
 [Агрегатные функции &#40; Transact-SQL &#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)   
 [ЧЕРЕЗ предложение &#40; Transact-SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md)  
  
  

