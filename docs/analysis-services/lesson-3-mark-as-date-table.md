---
title: "Урок 4: Пометить как таблицу дат | Документы Microsoft"
ms.custom: 
ms.date: 03/27/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: c32cc336-b7d8-4122-9d62-4936344d2315
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5bef08da2c79aa1b17241300d1b9b31e7b977781
ms.contentlocale: ru-ru
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-3-mark-as-date-table"></a>Занятие 3: Пометить как таблицу дат
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

На занятии 2: Добавление данных, вы импортировали таблицу измерения с именем DimDate. Хотя в модели эта таблица называется DimDate, он также может называться как *таблицу дат*, они содержат данные даты и времени.  
  
Всякий раз при использовании функции логики операций со временем DAX в вычислениях, как будет выполняться при создании мер немного позже, необходимо указать свойства таблицы даты, включающие *таблицу дат* и уникальный идентификатор *даты столбец* в этой таблице.
  
На этом занятии вы пометить таблицы DimDate как *таблицу дат* и столбец даты (в таблице дат) в качестве *столбец даты* (идентификатор).  

Прежде чем мы пометить таблицы дат и столбец дат, нам нужно немного обслуживания, чтобы лучше понять нашей модели. Вы заметите таблицы DimDate столбец с именем **FullDateAlternateKey**. Он содержит по одной строке на каждый день каждого календарного года, включается в таблицу. Мы будем использовать этот столбец много формулы мер и в отчетах. Но FullDateAlternateKey не очень хорошо идентификатора для этого столбца. Мы будем переименуйте его в **Дата**, упрощая процесс идентификации и включать в формулы. Когда это возможно, рекомендуется переименовать объекты, такие как таблицы и столбцы, чтобы упростить их идентификацию в клиентские приложения, такие как Power BI и Excel. 
  
Предполагаемое время выполнения данного занятия: **3 минуты**  
  
## <a name="prerequisites"></a>Предварительные требования  
Этот раздел является частью учебника по табличному моделированию, который необходимо изучать по порядку. Перед выполнением задач этого занятия, необходимо завершить предыдущее занятие: [Lesson 2: Добавление данных](../analysis-services/lesson-2-add-data.md). 

### <a name="to-rename-the-fulldatealternatekey-column"></a>Переименование столбца FullDateAlternateKey

1.  В конструкторе моделей щелкните **DimDate** таблицы.

2.  Дважды щелкните заголовок для **FullDateAlternateKey** столбца и переименуйте его в **даты**.

  
### <a name="to-set-mark-as-date-table"></a>Параметр «Пометить как таблицу данных» (Mark as Date Table)  
  
1.  Выберите столбец **Дата** , а затем убедитесь, что в окне **Свойства** в разделе **Тип данных**выбран тип  **Дата** .  
  
2.  Откройте меню **Таблица** , выберите пункт **Дата**, а затем пункт **Пометить как таблицу дат**.  
  
3.  В диалоговом окне **Пометить как таблицу дат** в списке **Дата** выберите столбец **Дата** в качестве уникального идентификатора. Оно обычно выбирается по умолчанию. Нажмите кнопку **ОК**. 

    ![как табличные lesson3-Дата таблицы](../analysis-services/media/as-tabular-lesson3-date-table.png)
  

## <a name="whats-next"></a>Дальнейшие действия
Перейдите к следующему занятию: [занятия 4: Создание связей](../analysis-services/lesson-4-create-relationships.md).
  
