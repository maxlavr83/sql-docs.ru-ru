---
title: Определение упорядочивания для измерения | Документы Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6f2e9dfce4abc66e9fa77a7d429c3cdd9a306c69
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/10/2018
ms.locfileid: "34022251"
---
# <a name="bi-wizard---define-the-ordering-for-a-dimension"></a>Мастер бизнес-Аналитики — определение упорядочивания для измерения
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Добавьте расширение упорядочивания атрибутов к кубу или измерению, чтобы указать, как упорядочиваются элементы атрибута. Элементы можно упорядочивать по имени или ключу атрибута, либо по имени или ключу другого атрибута (основанному на связи атрибута). По умолчанию элементы упорядочиваются по имени. Это расширение изменяет настройки свойств **OrderBy** и **OrderByAttributeID** для атрибутов в измерении.  
  
 Чтобы добавить упорядочивание атрибутов, используйте мастер бизнес-аналитики и выберите параметр **Задать сортировку атрибута** на странице **Выбор расширения** . После этого мастер отобразит шаги, позволяющие выбрать измерение, к которому необходимо применить упорядочивание атрибутов, и указать способ упорядочивания атрибутов для выбранного измерения.  
  
## <a name="selecting-a-dimension"></a>Выбор измерения  
 На первой странице **Определение порядка атрибутов** мастера указывается измерение, к которому необходимо применить упорядочивание атрибутов. Добавление расширения упорядочивания атрибутов к этому выбранному измерению приведет к изменению измерения. Эти изменения будут наследоваться всеми кубами, включающими выбранное измерение.  
  
## <a name="specifying-ordering"></a>Указание упорядочивания  
 На второй странице **Определение порядка атрибутов** мастера указывается, как будут упорядочиваться все атрибуты в измерении.  
  
 В столбце **Атрибут сортировки** можно изменить атрибут, используемый для выполнения упорядочивания. Если атрибут, который вы хотите использовать для упорядочивания элементов не находится в списке, прокрутите список вниз, а затем выберите  **\<создать атрибут... >** Открытие **выберите столбец** диалоговое окно, где это возможно Выберите столбец в таблице измерения. При выборе столбца с использованием диалогового окна **Выбор столбца** создается дополнительный атрибут, с помощью которого необходимо упорядочивать элементы атрибута.  
  
 В столбце **Критерии** после этого можно выбрать, необходимо ли упорядочивать элементы атрибута по **Key** или **Name**.  
  
  
