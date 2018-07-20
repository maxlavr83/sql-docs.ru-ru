---
title: Добавление атрибутов к измерениям | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 80551dad-97ac-40d0-90af-b810780321ce
caps.latest.revision: 15
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 19fdf91a124a02da60e91c28a6f6be42fd5f2e42
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2018
ms.locfileid: "37198494"
---
# <a name="adding-attributes-to-dimensions"></a>Добавление атрибутов к измерениям
  Теперь после определения измерений можно наполнить их атрибутами, которые представляют все элементы данных в измерении. Атрибуты обычно основаны на полях из представления источников данных. При добавлении атрибутов в измерение можно включить поля из любой таблицы в представлении источника данных.  
  
 В этой задаче с помощью конструктора измерений в измерения «Заказчик» и «Продукт» будут добавлены атрибуты. Измерение «Заказчик» будет включать атрибуты, основанные на полях из таблиц как «Заказчик», так и «География».  
  
## <a name="adding-attributes-to-the-customer-dimension"></a>Добавление атрибутов в измерение «Заказчик»  
  
#### <a name="to-add-attributes"></a>Добавление атрибутов  
  
1.  Откройте в конструкторе измерений измерение «Заказчик». Для этого дважды щелкните измерение **Заказчик** в узле **Измерения** обозревателя решений.  
  
2.  На панели **Атрибуты** обратите внимание на атрибуты «Customer Key» и «Geography Key», созданные мастером кубов.  
  
3.  На панели инструментов вкладки **Структура измерения** щелкните значок «Масштаб», чтобы просмотреть таблицы области **Представление источника данных** в масштабе 100 %.  
  
4.  Перетащите следующие столбцы из таблицы **Customer** в области **Представление источника данных** в область **Атрибуты** .  
  
    -   **BirthDate**  
  
    -   **MaritalStatus**  
  
    -   **Gender**  
  
    -   **EmailAddress**  
  
    -   **YearlyIncome**  
  
    -   **TotalChildren**  
  
    -   **NumberChildrenAtHome**  
  
    -   **EnglishEducation**  
  
    -   **EnglishOccupation**  
  
    -   **HouseOwnerFlag**  
  
    -   **NumberCarsOwned**  
  
    -   **Phone**  
  
    -   **DateFirstPurchase**  
  
    -   **CommuteDistance**  
  
5.  Перетащите следующие столбцы из таблицы **Geography** в области **Представление источника данных** в область **Атрибуты** .  
  
    -   **Город**  
  
    -   **StateProvinceName**  
  
    -   **EnglishCountryRegionName**  
  
    -   **PostalCode**  
  
6.  В меню «Файл» выберите команду **Сохранить все**.  
  
## <a name="adding-attributes-to-the-product-dimension"></a>Добавление атрибутов в измерение «Продукт»  
  
#### <a name="to-add-attributes"></a>Добавление атрибутов  
  
1.  Откройте в конструкторе измерений измерение «Продукт». Дважды щелкните измерение **Продукт** в обозревателе решений.  
  
2.  На панели **Атрибуты** обратите внимание на атрибут «Ключ продукта», созданный мастером кубов.  
  
3.  На панели инструментов вкладки **Структура измерения** щелкните значок «Масштаб», чтобы просмотреть таблицы области **Представление источника данных** в масштабе 100 %.  
  
4.  Перетащите следующие столбцы из таблицы **Продукт** в области **Представление источника данных** в область **Атрибуты** .  
  
    -   **StandardCost**  
  
    -   **Color**  
  
    -   **SafetyStockLevel**  
  
    -   **ReorderPoint**  
  
    -   **ListPrice**  
  
    -   **Размер**  
  
    -   **SizeRange**  
  
    -   **Weight**  
  
    -   **DaysToManufacture**  
  
    -   **ProductLine**  
  
    -   **DealerPrice**  
  
    -   **Class**  
  
    -   **Style**  
  
    -   **ModelName**  
  
    -   **StartDate**  
  
    -   **EndDate**  
  
    -   **Состояние**  
  
5.  В меню «Файл» выберите команду **Сохранить все**.  
  
## <a name="next-task-in-lesson"></a>Следующая задача занятия  
 [Просмотр свойств куба и измерения](lesson-2-4-reviewing-cube-and-dimension-properties.md)  
  
## <a name="see-also"></a>См. также  
 [Справочник по свойствам атрибута измерения](multidimensional-models/dimension-attribute-properties-reference.md)  
  
  