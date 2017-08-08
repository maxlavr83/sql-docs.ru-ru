---
title: "IsTestCase (расширения интеллектуального анализа данных) | Документы Microsoft"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- IsTestCase
dev_langs:
- DMX
helpviewer_keywords:
- IsTestCase function
ms.assetid: 7ff4b895-9bb4-4e26-ab1b-c9049cfc2291
caps.latest.revision: 10
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 0880841c201e9f25eb4685d0e6368abbb5bca885
ms.contentlocale: ru-ru
ms.lasthandoff: 08/02/2017

---
# <a name="istestcase-dmx"></a>IsTestCase (расширения интеллектуального анализа данных)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Указывает, используется ли вариант в качестве проверочного для конкретной модели или структуры интеллектуального анализа данных.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
IsTestCase()  
```  
  
## <a name="result-type"></a>Тип результата  
 Возвращает **true** Если регистр входит в набор проверочных данных; в противном случае **false**.  
  
## <a name="remarks"></a>Замечания  
 Если создание структуры интеллектуального анализа данных и соответствующей модели интеллектуального анализа производится при помощи мастера интеллектуального анализа данных, то по умолчанию 30% вариантов резервируются для использования в качестве проверочного набора данных. Оставшиеся варианты используются для обучения модели интеллектуального анализа данных. Один и тот же проверочный набор данных можно использовать со всеми моделями, созданными на основе этой структуры. Однако если для создания модели интеллектуального анализа данных использовались расширения интеллектуального анализа данных, то по умолчанию все данные используются для обучения модели и проверочный набор не создается. Чтобы разрешить создание проверочного набора данных, нужно задать значение параметров предложения WITH HOLDOUT.  
  
 Узнать, создавался ли для конкретной структуры интеллектуального анализа данных проверочный набор, можно, посмотрев значение свойств <xref:Microsoft.AnalysisServices.MiningStructure.HoldoutMaxCases%2A> и <xref:Microsoft.AnalysisServices.MiningStructure.HoldoutMaxPercent%2A>.  
  
> [!NOTE]  
>  Необходимо включить детализацию на модели, если вы хотите использовать функции IsTrainingCase или IsTestCase для получения сведений о вариантах в конкретной модели. Дополнительные сведения см. в разделе [Включение детализации для модели интеллектуального анализа данных](../analysis-services/data-mining/enable-drillthrough-for-a-mining-model.md).  
  
 Чтобы вернуть варианты, которые являются частью набора данных для обучения, используйте функцию [IsTrainingCase &#40; расширений интеллектуального анализа данных &#41;](../dmx/istrainingcase-dmx.md).  
  
## <a name="examples"></a>Примеры  
 В следующем примере используется `Targeted Mailing` структуры интеллектуального анализа данных, созданную в [Basic Data Mining Tutorial](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c). Запрос возвращает все варианты структуры, используемые для проверки.  
  
```  
SELECT *  
FROM [Targeted Mailing].CASES  
WHERE IsTestCase()  
```  
  
 Дополнительные сведения о запросах к вариантам, используемым для интеллектуального анализа данных см. в разделе [SELECT FROM &#60; модели &#62;. ВАРИАНТЫ &#40; расширений интеллектуального анализа данных &#41; ](../dmx/select-from-model-cases-dmx.md) и [SELECT FROM &#60; структура &#62;. СЛУЧАИ](../dmx/select-from-structure-cases.md).  
  
## <a name="see-also"></a>См. также:  
 [Функции &#40; расширений интеллектуального анализа данных &#41;](../dmx/functions-dmx.md)   
 [Запросы интеллектуального анализа данных](../analysis-services/data-mining/data-mining-queries.md)   
 [Обучающие и проверочные наборы данных](../analysis-services/data-mining/training-and-testing-data-sets.md)  
  
  
