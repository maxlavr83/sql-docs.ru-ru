---
title: "Элемент Ordinal (ASSL) | Документы Microsoft"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Ordinal Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Ordinal
helpviewer_keywords:
- Ordinal element
ms.assetid: 64e68ad5-439c-4c1d-9df4-ee90c56761b4
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f82b14a571fad0753e3b8835a3e0829a4975c583
ms.contentlocale: ru-ru
ms.lasthandoff: 09/01/2017

---
# <a name="ordinal-element-assl"></a>Элемент Ordinal (ASSL)
  Определяет порядковый номер, к которому следует выполнять привязку в таких коллекциях, как коллекции ключей и переводов.  
  
## <a name="syntax"></a>Синтаксис  
  
```xml  
  
<AttributeBinding> <!-- or CubeAttributeBinding -->  
   ...  
   <Ordinal>...</Ordinal>  
   ...  
</AttributeBinding>  
```  
  
## <a name="element-characteristics"></a>Характеристики элемента  
  
|Характеристика|Описание|  
|--------------------|-----------------|  
|Тип данных и длина|Целочисленный|  
|Значение по умолчанию|**0**|  
|Количество элементов|0—1: необязательный элемент, который может появляться только один раз.|  
  
## <a name="element-relationships"></a>Связи элемента  
  
|Связь|Элемент|  
|------------------|-------------|  
|Родительские элементы|[AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md), [CubeAttributeBinding](../../../analysis-services/scripting/data-type/cubeattributebinding-data-type-assl.md)|  
|Дочерние элементы|None|  
  
## <a name="remarks"></a>Замечания  
 **AttributeBinding** и **CubeAttributeBinding** элементов, в который [тип](../../../analysis-services/scripting/properties/type-element-binding-assl.md) свойство может принимать значение *ключ* или *перевода*  могут быть привязаны к атрибуту, который в свою очередь привязан к коллекции столбцов в представлении источника данных. Значение элемента **Ordinal** определяет, к какому столбцу в этой коллекции относятся элементы **AttributeBinding** или **CubeAttributeBinding** .  
  
 Элементы, соответствующие родителям элемента **порядковый номер** в модели объектов Analysis Management объекты AMO — <xref:Microsoft.AnalysisServices.AttributeBinding> и <xref:Microsoft.AnalysisServices.CubeAttributeBinding>.  
  
## <a name="see-also"></a>См. также:  
 [Свойства &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  