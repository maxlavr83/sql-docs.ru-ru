---
title: "&gt;= (Больше или равно) (расширения интеллектуального анализа данных) | Документы Microsoft"
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
dev_langs:
- DMX
helpviewer_keywords:
- '>= (greater than or equal to operator)'
- greater than or equal to (>=)
ms.assetid: a96b7e9c-72dc-4df1-aa41-85aad933df96
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 736cf2361101a9722aa3723c64a04f98fde04b0c
ms.contentlocale: ru-ru
ms.lasthandoff: 08/02/2017

---
# <a name="gt-greater-than-or-equal-to-dmx"></a>&gt;= (Больше или равно) (расширения интеллектуального анализа данных)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Выполняет операцию сравнения с целью определения, является ли одно выражение больше второго выражения расширений интеллектуального анализа данных или равным ему.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
DMX_Expression >= DMX_Expression  
```  
  
#### <a name="parameters"></a>Параметры  
 *DMX_Expression*  
 Допустимое выражение расширений интеллектуального анализа данных.  
  
## <a name="return-value"></a>Возвращаемое значение  
 Логическое значение равно TRUE в случае, если оба аргумента не равны NULL, и значение первого аргумента больше значения второго аргумента или равно ему. Логическое значение равно FALSE, если оба аргумента не равны NULL, и первый аргумент имеет значение меньшее, чем второй. Логическое значение равно NULL, если один или оба аргумента имеют значение NULL.  
  
## <a name="see-also"></a>См. также:  
 [Операторы сравнения &#40; расширений интеллектуального анализа данных &#41;](../dmx/operators-comparison.md)   
 [Расширения интеллектуального анализа данных &#40; расширений интеллектуального анализа данных &#41; Справочник по операторам](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Операторы &#40; расширений интеллектуального анализа данных &#41;](../dmx/operators-dmx.md)  
  
  
