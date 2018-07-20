---
title: Задание цветов диаграммы с помощью палитры (построитель отчетов и службы SSRS) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d95efc22-5a32-43d4-9bd2-12753e7fd395
caps.latest.revision: 6
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 306f73588ed837771bbb5852d9107e44c28f1f0d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2018
ms.locfileid: "37276070"
---
# <a name="define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs"></a>Задание цветов диаграммы с помощью палитры (построитель отчетов и службы SSRS)
  Цветовую палитру диаграммы можно изменить, выбрав существующую палитру или определив свою. Пользовательские палитры зависят для конкретного отчета.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-change-the-colors-on-the-chart-using-a-built-in-color-palette"></a>Изменение цветов диаграммы с помощью встроенной цветовой палитры  
  
1.  Откройте панель «Свойства».  
  
2.  Щелкните диаграмму в области конструктора. На панели «Свойства» отображаются свойства объекта диаграммы.  
  
     В раскрывающемся списке в верхней части панели свойств появляется имя объекта (по умолчанию —**Диаграмма1** ).  
  
3.  На вкладке **Диаграмма** в свойстве Palette выберите из раскрывающегося списка новую палитру.  
  
    > [!NOTE]  
    >  Изменить цвета или их порядок во встроенной палитре нельзя.  
  
### <a name="to-define-your-own-colors-on-the-chart-using-a-custom-color-palette"></a>Определение пользовательских цветов диаграммы с помощью пользовательской цветовой палитры  
  
1.  Откройте панель «Свойства».  
  
2.  Щелкните диаграмму в области конструктора. На панели «Свойства» отображаются свойства объекта диаграммы.  
  
3.  В **диаграммы** разделе для `Palette` выберите **Custom**.  
  
4.  В области свойства CustomPaletteColors нажмите кнопку изменения коллекции (**…**). Будет открыто окно **Редактор коллекции ReportColorExpression** .  
  
5.  Чтобы добавить цвет, нажмите кнопку **Добавить** . Выберите цвет из раскрывающегося списка или выберите выражение и укажите шестнадцатеричное значение конкретного цвета — например, ff6600 для оранжевого цвета.  
  
     Дополнительные сведения о шестнадцатеричных значениях см. в разделе [Таблица цветов](http://go.microsoft.com/fwlink/?linkid=9258) в MSDN.  
  
6.  Нажмите кнопку **Добавить** , чтобы добавить в палитру еще один цвет.  
  
7.  По завершении нажмите кнопку **ОК**.  
  
 В пользовательской палитре можно менять порядок цветов, чтобы изменить цвета разных рядов диаграммы.  
  
## <a name="see-also"></a>См. также  
 [Форматирование цветов для рядов на диаграмме (построитель отчетов и службы SSRS)](formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)   
 [Диаграммы (построитель отчетов и службы SSRS)](charts-report-builder-and-ssrs.md)   
 [Указание согласованных цветов для нескольких фигурных диаграмм (построитель отчетов и службы SSRS)](shape-charts-report-builder-and-ssrs.md)  
  
  