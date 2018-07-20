---
title: Настройка количества попаданий | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- vs.debug.breakpt.hitcount
helpviewer_keywords:
- Transact-SQL debugger, breakpoint hit count
ms.assetid: 24836939-94ed-4e57-aa85-5d6938d859e4
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c6d859190ee6ca3767ce0ab28a9feb0bb5e96a21
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2018
ms.locfileid: "37228744"
---
# <a name="specify-a-hit-count"></a>Настройка счетчика числа попаданий
  Счетчик числа попаданий точки останова увеличивается отладчиком [!INCLUDE[tsql](../../includes/tsql-md.md)] каждый раз при достижении точки останова. Если достигнуто указанное число попаданий или удовлетворяется любое из указанных условий для точки останова, то отладчик выполняет действие, заданное для точки останова.  
  
## <a name="hit-count-considerations"></a>Соображения в отношении счетчика числа попаданий  
 По умолчанию выполнение прерывается каждый раз, когда достигается точка останова. Можно выбрать один из следующих параметров:  
  
-   Останавливать всегда (по умолчанию).  
  
-   Останавливать, если счетчик равен определенному значению.  
  
-   Останавливать, если счетчик равен кратному числу заданного значения.  
  
-   Останавливать, если счетчик превышает заданное значение или равен ему.  
  
 Счетчики числа попаданий точек останова увеличиваются в рамках сеанса отладки. Все счетчики числа попаданий обнуляются в начале каждого сеанса отладки.  
  
 Если необходимо отслеживать, сколько раз достигается точка останова, без выполнения остановки, задайте очень большое значение счетчика числа попаданий, чтобы точка останова никогда не была достигнута.  
  
 Действие для точки останова по умолчанию — прекращение выполнения, если достигнуто число попаданий и удовлетворяется условие для точки останова. Сведения об указании других действий см. в разделе [Задание действия в точке останова](specify-a-breakpoint-action.md).  
  
#### <a name="to-specify-a-hit-count"></a>Настройка счетчика числа попаданий  
  
1.  В окне редактора щелкните глиф точки останова правой кнопкой мыши и выберите в контекстном меню пункт **Число попаданий** .  
  
     -или-  
  
     В окне **Точки останова** щелкните глиф точки останова правой кнопкой мыши и выберите в контекстном меню пункт **Число попаданий** .  
  
2.  В диалоговом окне **Счетчик числа попаданий точки останова** выберите нужное поведение в поле **При попадании в точку останова** .  
  
     При выборе параметров, отличных от **Останавливать всегда**, с правой стороны от списка появится текстовое поле. Введите целое число в текстовое поле, чтобы задать нужное количество попаданий.  
  
3.  Нажмите кнопку **ОК** , чтобы внести изменения, либо кнопку **Отмена** , чтобы выйти без их применения.  
  
#### <a name="to-view-or-reset-the-current-hit-count"></a>Просмотр или сброс текущего счетчика числа попаданий  
  
1.  В окне редактора щелкните глиф точки останова правой кнопкой мыши и выберите в контекстном меню пункт **Число попаданий** .  
  
     -или-  
  
     В окне **Точки останова** щелкните глиф точки останова правой кнопкой мыши и выберите в контекстном меню пункт **Число попаданий** .  
  
2.  В диалоговом окне **Счетчик точек останова** пункт **Текущее число попаданий** отображается сразу над кнопкой **Сброс** .  
  
3.  Нажмите кнопку **Сброс** , если нужно обнулить текущий счетчик числа попаданий.  
  
4.  Нажмите кнопку **ОК** или **Отмена** для выхода из диалогового окна.  
  
## <a name="see-also"></a>См. также  
 [Задание условия точки останова](specify-a-breakpoint-condition.md)  
  
  