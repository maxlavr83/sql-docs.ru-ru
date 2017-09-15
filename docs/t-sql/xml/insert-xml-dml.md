---
title: "INSERT (XML DML) | Документы Microsoft"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- XML DML [SQL Server]
- inserting nodes
- insert keyword [XML DML]
- insert XML DML statement
ms.assetid: 0c95c2b3-5cc2-4c38-9e25-86493096c442
caps.latest.revision: 38
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9f995a0dcd0b91c0835c4121a7a2072c2a586f35
ms.contentlocale: ru-ru
ms.lasthandoff: 09/01/2017

---
# <a name="insert-xml-dml"></a>insert (XML DML)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Вставляет один или несколько узлов, идентифицируемых по *Expression1* как дочерних узлов или одноуровневых объектов узла, идентифицируемого выражением *Expression2*.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
insert   
      Expression1 (  
                 {as first | as last} into | after | before  
                                    Expression2  
                )  
```  
  
## <a name="arguments"></a>Аргументы  
 *Expression1*  
 Идентифицирует один или несколько вставляемых узлов. Это может быть постоянный экземпляр XML; ссылку на типизированный экземпляр типа данных XML той же коллекции XML-схемы, в которой применяется метод изменения; нетипизированный XML экземпляр типа данных с помощью изолированного **SQL: column()**/**SQL: variable()** функции; или выражение XQuery. Результатом выражения может быть узел, в том числе текстовый, или упорядоченная последовательность узлов. Корневой узел (/) не может быть результатом выражения. Если результатом выражения является значение или последовательность значений, то такие значения вставляются в качестве одиночного текстового узла, в котором все значения разделены пробелами. Если несколько узлов указаны как постоянные, они заключаются в скобки и разделяются запятыми. Разнородные последовательности, например, последовательность элементов, атрибутов или значений, вставлять нельзя. Если *Expression1* разрешается в пустую последовательность, вставка не выполняется и ошибки не возвращаются.  
  
 into  
 Узлы, идентифицируемые выражением *Expression1* , вставляются в качестве прямых потомков (дочерних узлов) узла, идентифицируемого выражением *Expression2*. Если узел в *Expression2* уже есть один или несколько дочерних узлов, необходимо использовать либо **как первый** или **согласно последнему** можно указать, где добавить новый узел. Они означают, соответственно, добавление в начало или в конец списка потомков. **Как первый** и **согласно последнему** при вставке атрибутов игнорируются ключевые слова.  
  
 after  
 Узлы, идентифицируемые выражением *Expression1* , вставляются в качестве элементов с общим родителем непосредственно после узла, идентифицируемого выражением *Expression2*. **После** ключевое слово не может использоваться для вставки атрибутов. Например, его нельзя использовать для вставки конструктора атрибута или для возвращения атрибута из запроса XQuery.  
  
 before  
 Узлы, идентифицируемые выражением *Expression1* , вставляются в качестве элементов с общим родителем непосредственно перед узлом, идентифицируемым по *Expression2*. **Перед** при вставке атрибутов ключевое слово не может использоваться. Например, его нельзя использовать для вставки конструктора атрибута или для возвращения атрибута из запроса XQuery.  
  
 *Expression2*  
 Идентифицирует узел. Узлов, заданных в *Expression1* вставляются относительно узла, идентифицируемого выражением *Expression2*. Это может быть выражение XQuery, возвращающее ссылку на узел, существующий в документе, к которому в данный момент производится обращение. Если возвращается более одного узла, то операция вставки завершается неудачно. Если *Expression2* возвращает пустую последовательность, вставка не произойдет и никакие ошибки не возвращаются. Если *Expression2* статически не является одноэлементным множеством, возвращается статическая ошибка. *Expression2* не может быть инструкция по обработке, комментарий или атрибут. Обратите внимание, что *Expression2* должен представлять собой ссылку на существующий узел в документе, а не на конструируемый узел.  
  
## <a name="examples"></a>Примеры  
  
### <a name="a-inserting-element-nodes-into-the-document"></a>A. Вставка узлов элементов в документ  
 В следующем примере показана вставка элементов в документ. Во-первых, XML-документ присваивается переменной **xml** типа. Затем с помощью нескольких **вставить** XML DML-инструкций показано, как вставка узлов элементов в документе. После каждой операции вставки с помощью инструкции SELECT отображается результат.  
  
```  
USE AdventureWorks;  
GO  
DECLARE @myDoc xml;         
SET @myDoc = '<Root>         
    <ProductDescription ProductID="1" ProductName="Road Bike">         
        <Features>         
        </Features>         
    </ProductDescription>         
</Root>'  ;       
SELECT @myDoc;     
-- insert first feature child (no need to specify as first or as last)         
SET @myDoc.modify('         
insert <Maintenance>3 year parts and labor extended maintenance is available</Maintenance>   
into (/Root/ProductDescription/Features)[1]') ;  
SELECT @myDoc ;        
-- insert second feature. We want this to be the first in sequence so use 'as first'         
set @myDoc.modify('         
insert <Warranty>1 year parts and labor</Warranty>          
as first         
into (/Root/ProductDescription/Features)[1]         
')  ;       
SELECT @myDoc  ;       
-- insert third feature child. This one is the last child of <Features> so use 'as last'         
SELECT @myDoc         
SET @myDoc.modify('         
insert <Material>Aluminium</Material>          
as last         
into (/Root/ProductDescription/Features)[1]         
')         
SELECT @myDoc ;        
-- Add fourth feature - this time as a sibling (and not a child)         
-- 'after' keyword is used (instead of as first or as last child)         
SELECT @myDoc  ;       
set @myDoc.modify('         
insert <BikeFrame>Strong long lasting</BikeFrame>   
after (/Root/ProductDescription/Features/Material)[1]         
')  ;       
SELECT @myDoc;  
GO  
```  
  
 Заметьте, что в разнообразных выражениях путей в данном примере в качестве требования к статическому вводу указывается «[1]». Это позволяет гарантированно указать отдельный целевой узел.  
  
### <a name="b-inserting-multiple-elements-into-the-document"></a>Б. Вставка нескольких элементов в документ  
 В следующем примере документ сначала присваивается переменной **xml** типа. Затем последовательность из двух элементов, представляющих функции продукта, присваивается второй переменной типа **xml** типа. Эта последовательность затем вставляется в первую переменную.  
  
```  
USE AdventureWorks;  
GO  
DECLARE @myDoc xml;  
SET @myDoc = N'<Root>             
<ProductDescription ProductID="1" ProductName="Road Bike">             
    <Features> </Features>             
</ProductDescription>             
</Root>';  
DECLARE @newFeatures xml;  
SET @newFeatures = N'<Warranty>1 year parts and labor</Warranty>            
<Maintenance>3 year parts and labor extended maintenance is available</Maintenance>';           
-- insert new features from specified variable            
SET @myDoc.modify('             
insert sql:variable("@newFeatures")             
into (/Root/ProductDescription/Features)[1] ')             
SELECT @myDoc;  
GO  
```  
  
### <a name="c-inserting-attributes-into-a-document"></a>В. Вставка атрибутов в документ  
 В следующем примере показано, как выполняется вставка атрибутов в документ. Сначала документ присваивается **xml** переменной типа. Затем используется серия **вставить** инструкций XML DML служит для вставки атрибутов в документ. После каждой операции вставки с помощью инструкции SELECT отображается результат.  
  
```  
USE AdventureWorks;  
GO  
DECLARE @myDoc xml ;            
SET @myDoc =   
'<Root>             
    <Location LocationID="10" >             
        <step>Manufacturing step 1 at this work center</step>             
        <step>Manufacturing step 2 at this work center</step>             
    </Location>             
</Root>' ;  
SELECT @myDoc  ;          
-- insert LaborHours attribute             
SET @myDoc.modify('             
insert attribute LaborHours {".5" }             
into (/Root/Location[@LocationID=10])[1] ') ;           
SELECT @myDoc  ;          
-- insert MachineHours attribute but its value is retrived from a sql variable @Hrs             
DECLARE @Hrs float ;            
SET @Hrs =.2   ;          
SET @myDoc.modify('             
insert attribute MachineHours {sql:variable("@Hrs") }             
into   (/Root/Location[@LocationID=10])[1] ');            
SELECT @myDoc;             
-- insert sequence of attribute nodes (note the use of ',' and ()              
-- around the attributes.             
SET @myDoc.modify('             
insert (              
           attribute SetupHours {".5" },             
           attribute SomeOtherAtt {".2"}             
        )             
into (/Root/Location[@LocationID=10])[1] ');             
SELECT @myDoc;  
GO  
```  
  
### <a name="d-inserting-a-comment-node"></a>Г. Вставка узла с комментарием  
 В этом запросе XML-документ сначала присваивается переменной **xml** типа. Затем для вставки узла с комментарием после первого элемента <`step`> используется язык XML DML.  
  
```  
USE AdventureWorks;  
GO  
DECLARE @myDoc xml;             
SET @myDoc =   
'<Root>             
    <Location LocationID="10" >             
        <step>Manufacturing step 1 at this work center</step>             
        <step>Manufacturing step 2 at this work center</step>             
    </Location>             
</Root>' ;           
SELECT @myDoc;             
SET @myDoc.modify('             
insert <!-- some comment -->             
after (/Root/Location[@LocationID=10]/step[1])[1] ');            
SELECT @myDoc;  
GO  
```  
  
### <a name="e-inserting-a-processing-instruction"></a>Д. Вставка инструкции по обработке  
 В следующем запросе XML-документ сначала присваивается переменной **xml** типа. Затем используется ключевое слово языка XML DML для вставки инструкции по обработке в начало документа.  
  
```  
USE AdventureWorks;  
GO  
DECLARE @myDoc xml;  
SET @myDoc =   
'<Root>   
    <Location LocationID="10" >   
        <step>Manufacturing step 1 at this work center</step>   
        <step>Manufacturing step 2 at this work center</step>   
    </Location>   
</Root>' ;  
SELECT @myDoc ;  
SET @myDoc.modify('   
insert <?Program = "Instructions.exe" ?>   
before (/Root)[1] ') ;  
SELECT @myDoc ;  
GO  
```  
  
### <a name="f-inserting-data-using-a-cdata-section"></a>Е. Вставка данных с помощью раздела CDATA  
 При вставке текста, содержащего недопустимые в XML символы, например, < или >, можно использовать разделы CDATA для вставки данных, как показано в следующем запросе. В запросе указывается раздел CDATA, но добавляется он в качестве текстового узла, в котором недопустимые символы преобразуются в сущности. Например ' <' сохраняется как &lt;.  
  
```  
USE AdventureWorks;  
GO  
DECLARE @myDoc xml;             
SET @myDoc =   
'<Root>             
    <ProductDescription ProductID="1" ProductName="Road Bike">             
        <Features> </Features>             
    </ProductDescription>             
</Root>' ;            
SELECT @myDoc ;            
SET @myDoc.modify('             
insert <![CDATA[ <notxml> as text </notxml> or cdata ]]>   
into  (/Root/ProductDescription/Features)[1] ') ;   
SELECT @myDoc ;  
GO  
```  
  
 Запрос выполняет вставку текстового узла в элемент <`Features`>:  
  
```  
<Root>  
<ProductDescription ProductID="1" ProductName="Road Bike">  
<Features> <notxml> as text </notxml> or cdata </Features>  
</ProductDescription>  
</Root>       
```  
  
### <a name="g-inserting-text-node"></a>Ж. Вставка текстового узла  
 В этом запросе XML-документ сначала присваивается переменной **xml** типа. Затем для вставки текстового узла в качестве первого дочернего узла элемента <`Root`> используется язык XML DML. Для указания текста используется текстовый конструктор.  
  
```  
USE AdventureWorks;  
GO  
DECLARE @myDoc xml;  
SET @myDoc = '<Root>  
<ProductDescription ProductID="1" ProductName="Road Bike">  
<Features>  
  
</Features>  
</ProductDescription>  
</Root>'  
SELECT @myDoc;  
set @myDoc.modify('  
 insert text{"Product Catalog Description"}   
 as first into (/Root)[1]  
');  
SELECT @myDoc;  
```  
  
### <a name="h-inserting-a-new-element-into-an-untyped-xml-column"></a>З. Вставка нового элемента в нетипизированный XML-столбец  
 В следующем примере применяется XML DML для обновления экземпляра XML хранится в **xml** столбец типа:  
  
```  
USE AdventureWorks;  
GO  
CREATE TABLE T (i int, x xml);  
go  
INSERT INTO T VALUES(1,'<Root>  
    <ProductDescription ProductID="1" ProductName="Road Bike">  
        <Features>  
            <Warranty>1 year parts and labor</Warranty>  
            <Maintenance>3 year parts and labor extended maintenance is available</Maintenance>  
        </Features>  
    </ProductDescription>  
</Root>');  
go  
-- insert a new element  
UPDATE T  
SET x.modify('insert <Material>Aluminium</Material> as first  
  into   (/Root/ProductDescription/Features)[1]  
');  
GO  
```  
  
 Опять же, при вставке узла элемента <`Material`> результат выражения пути должен возвращать одну цель. Это указывается явно путем добавления [1] в конце выражения.  
  
```  
-- check the update  
SELECT x.query(' //ProductDescription/Features')  
FROM T;  
GO  
```  
  
### <a name="i-inserting-based-on-an-if-condition-statement"></a>И. Вставка на основе инструкции с условием  
 В следующем примере указывается условие IF в рамках Expression1 в **вставить** XML DML-инструкции. Если условие возвращает значение True, атрибут добавляется в элемент <`WorkCenter`>.  
  
```  
USE AdventureWorks;  
GO  
DECLARE @myDoc xml;  
SET @myDoc =   
'<Root>  
    <Location LocationID="10" LaborHours="1.2" >  
        <step>Manufacturing step 1 at this work center</step>  
    <step>Manufacturing step 2 at this work center</step>  
    </Location>  
</Root>';  
SELECT @myDoc  
SET @myDoc.modify('  
insert  
if (/Root/Location[@LocationID=10])  
then attribute MachineHours {".5"}  
else ()  
    as first into   (/Root/Location[@LocationID=10])[1] ');  
SELECT @myDoc;  
GO  
```  
  
 Ниже приведен похожий пример, за исключением того, **вставить** инструкции XML DML вставляет элемент в документе, если условие имеет значение True. То есть в случае, если элемент <`WorkCenter`> содержит два или менее дочерних элементов <`step`>.  
  
```  
USE AdventureWorks;  
GO  
DECLARE @myDoc xml;  
SET @myDoc =   
'<Root>  
    <Location LocationID="10" LaborHours="1.2" >  
        <step>Manufacturing step 1 at this work center</step>  
        <step>Manufacturing step 2 at this work center</step>  
    </Location>  
</Root>';  
SELECT @myDoc;  
SET @myDoc.modify('  
insert  
if (count(/Root/Location/step) <= 2)  
then element step { "This is a new step" }  
else ()  
    as last into   (/Root/Location[@LocationID=10])[1] ');  
SELECT @myDoc;  
GO  
```  
  
 Результат:  
  
```  
<Root>  
 <WorkCenter WorkCenterID="10" LaborHours="1.2">  
  <step>Manufacturing step 1 at this work center</step>  
  <step>Manufacturing step 2 at this work center</step>  
  <step>This is a new step</step>  
 </WorkCenter>  
```  
  
### <a name="j-inserting-nodes-in-a-typed-xml-column"></a>К. Вставка узлов в типизированный XML-столбец  
 В этом примере выполняется вставка элемента и атрибута в производственные инструкции, хранимые в типизированном XML **xml** столбца.  
  
 В примере сначала создается таблица (T) с типизированным **xml** столбца в базе данных AdventureWorks. Затем копируются производственные инструкции экземпляра XML из столбца Instructions в таблице ProductModel в таблицу T. После этого вставленные данные применяются к XML в таблице T.  
  
```  
USE AdventureWorks;  
GO            
DROP TABLE T;  
GO             
CREATE TABLE T(ProductModelID int primary key,    
Instructions xml (Production.ManuInstructionsSchemaCollection));  
GO  
INSERT T              
    SELECT ProductModelID, Instructions             
    FROM Production.ProductModel             
    WHERE ProductModelID=7;  
GO             
SELECT Instructions             
FROM T;  
-- now insertion begins             
--1) insert a new manu. Location. The <Root> specified as              
-- expression 2 in the insert() must be singleton.      
UPDATE T   
set Instructions.modify('   
declare namespace MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";   
insert <MI:Location LocationID="1000" >   
           <MI:step>New instructions go here</MI:step>   
         </MI:Location>   
as first   
into   (/MI:root)[1]   
') ;  
  
SELECT Instructions             
FROM T ;  
-- 2) insert attributes in the new <Location>             
UPDATE T             
SET Instructions.modify('             
declare namespace MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";             
insert attribute LaborHours { "1000" }             
into (/MI:root/MI:Location[@LocationID=1000])[1] ');   
GO             
SELECT Instructions             
FROM T ;  
GO             
--cleanup             
DROP TABLE T ;  
GO             
```  
  
## <a name="see-also"></a>См. также:  
 [Сравнение типизированного и нетипизированного XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [Создание экземпляров XML-данных](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [методов типа данных xml](../../t-sql/xml/xml-data-type-methods.md)   
 [Язык модификации XML-данных &#40; Язык XML DML &#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
