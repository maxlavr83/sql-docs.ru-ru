---
title: Последовательность и QNames (XQuery) | Документация Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- sequence [XQuery]
- XQuery, sequence
- QName [XQuery]
- predefined namespaces [XML in SQL Server]
ms.assetid: 3593ac26-dd78-4bf0-bb87-64fbcac5f026
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 470543f0016a01d10f6fff06383216ff984649fb
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2018
ms.locfileid: "51656294"
---
# <a name="sequence-and-qnames-xquery"></a>Последовательность и QNames (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  В этом разделе описаны следующие основные понятия XQuery.  
  
-   Последовательность  
  
-   QNames и стандартные пространства имен.  
  
## <a name="sequence"></a>Последовательность  
 Результат выражения в XQuery является последовательностью XML-узлов и экземпляров атомарных типов XSD. Отдельная запись последовательности называется элементом. Элемент последовательности может быть одним из следующих объектов.  
  
-   Такой узел, как элемент, атрибут, текст, инструкция по обработке, комментарий или документ.  
  
-   Такое атомарное значение, как экземпляр простого типа XSD.  
  
 Например, следующий запрос создает последовательность из двух элементов-узлов:  
  
```  
SELECT Instructions.query('  
     <step1> Step 1 description goes here</step1>,  
     <step2> Step 2 description goes here </step2>  
') AS Result  
FROM Production.ProductModel  
WHERE ProductModelID=7;  
  
```  
  
 Результат:  
  
```  
<step1> Step 1 description goes here </step1>  
<step2> Step 2 description goes here </step2>   
```  
  
 В предыдущем запросе запятая (`,`) в конце конструкции `<step1>` выполняет роль конструктора последовательности и является обязательной. Пробелы в результате добавлены только для иллюстрации и включены во все примеры результатов в документации.  
  
 Ниже приведены дополнительные сведения о последовательностях, которые следует иметь в виду.  
  
-   Если результат запроса представляет собой последовательность, которая содержит другую последовательность, то эта внутренняя последовательность упрощается до последовательности-контейнера. Например, последовательность ((1,2, (3,4,5)),6) упрощается в (1, 2, 3, 4, 5, 6).  
  
    ```  
    DECLARE @x xml;  
    SET @x = '';  
    SELECT @x.query('(1,2, (3,4,5)),6');  
    ```  
  
-   Пустой последовательностью называется та, которая не содержит элементов. Она записывается как «()».  
  
-   Последовательность, состоящую из единственного элемента, можно использовать как атомарное значение, и наоборот. То есть (1) = 1.  
  
 В такой реализации последовательность должна быть однородной. То есть последовательность состоит либо из атомарных значений, либо из узлов. Например, ниже приведены допустимые последовательности.  
  
```  
DECLARE @x xml;  
SET @x = '';  
-- Expression returns a sequence of 1 text node (singleton).  
SELECT @x.query('1');  
-- Expression returns a sequence of 2 text nodes  
SELECT @x.query('"abc", "xyz"');  
-- Expression returns a sequence of one atomic value. data() returns  
-- typed value of the node.  
SELECT @x.query('data(1)');  
-- Expression returns a sequence of one element node.   
-- In the expression XML construction is used to construct an element.  
SELECT @x.query('<x> {1+2} </x>');  
```  
  
 Следующий запрос вернет ошибку, поскольку разнородные последовательности не поддерживаются.  
  
```  
SELECT @x.query('<x>11</x>, 22');  
```  
  
## <a name="qname"></a>QName  
 Любой идентификатор в XQuery является именем QName. Имя QName состоит из префикса пространства имен и локального имени. В этой реализации имена переменных в XQuery являются именами QName и не могут иметь префиксов.  
  
 Рассмотрим следующий пример, в котором указывается запрос к нетипизированной **xml** переменной:  
  
```  
DECLARE @x xml;  
SET @x = '<Root><a>111</a></Root>';  
SELECT @x.query('/Root/a');  
```  
  
 В выражении (`/Root/a`) `Root` и `a` являются именами QName.  
  
 В следующем примере запрос производится к типизированному **xml** столбца. Запрос перебирает все \<шаг > элементы в расположении первого рабочего центра.  
  
```  
SELECT Instructions.query('  
   declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $Step in /AWMI:root/AWMI:Location[1]/AWMI:step  
      return  
           string($Step)   
') AS Result  
FROM Production.ProductModel  
WHERE ProductModelID=7;  
```  
  
 На панели запросов отметьте следующее.  
  
-   `AWMI root`, `AWMI:Location`, `AWMI:step` и `$Step` относятся к типу данных QNames. `AWMI` является префиксом, а `root`, `Location` и `Step` — локальными именами.  
  
-   Переменная `$step` — это имя QName, у нее нет префикса.  
  
 Ниже приведены пространства имен, стандартные в [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] для использования с поддержкой XQuery.  
  
|Prefix|URI|  
|------------|---------|  
|xs|https://www.w3.org/2001/XMLSchema|  
|xsi|https://www.w3.org/2001/XMLSchema-instance|  
|xdt|https://www.w3.org/2004/07/xpath-datatypes|  
|fn|https://www.w3.org/2004/07/xpath-functions|  
|(без префикса)|`urn:schemas-microsoft-com:xml-sql`|  
|sqltypes|https://schemas.microsoft.com/sqlserver/2004/sqltypes|  
|xml|`https://www.w3.org/XML/1998/namespace`|  
|(без префикса)|`https://schemas.microsoft.com/sqlserver/2004/SOAP`|  
  
 У всех создаваемых баз данных **sys** коллекции XML-схем. Эти схемы зарезервированы, поэтому к ним можно обратиться из любой пользовательской коллекции XML-схем.  
  
> [!NOTE]  
>  Эта реализация не поддерживает `local` префикса, как описано в спецификации XQuery на https://www.w3.org/2004/07/xquery-local-functions.  
  
## <a name="see-also"></a>См. также  
 [Основы XQuery](../xquery/xquery-basics.md)  
  
  
