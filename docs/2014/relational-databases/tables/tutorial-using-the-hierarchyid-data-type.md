---
title: Учебник. Использование типа данных hierarchyid | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- tutorials [hierarchyid]
- hierarchyid [Database Engine], tutorial
ms.assetid: 5a7f7cfd-7faf-439f-8085-8fd6bf7db355
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e3718b45b69870969dae85b4eb1ad2e9e80adc85
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/03/2018
ms.locfileid: "52788773"
---
# <a name="tutorial-using-the-hierarchyid-data-type"></a>Учебник. Использование типа данных hierarchyid
  Этот учебник предназначен для пользователей, имеющих опыт работы с [!INCLUDE[tsql](../../includes/tsql-md.md)], но незнакомых с типом данных `hierarchyid`.  
  
## <a name="what-you-will-learn"></a>Обзор учебника  
 Учебник разделен на два занятия.  
  
 [Занятие 1. Преобразование таблицы в иерархическую структуру](lesson-1-converting-a-table-to-a-hierarchical-structure.md)  
 На этом занятии возьмем существующую таблицу сотрудников, структурированную по иерархии «родители-потомки», и переместим данные в новую таблицу, представляющую иерархию с помощью типа данных `hierarchyid`. Для этого занятия требуется образец базы данных [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
 [Занятие 2. Создание и управление данными в иерархической таблице](lesson-2-creating-and-managing-data-in-a-hierarchical-table.md)  
 На этом занятии создается таблица, используя тип данных `hierarchyid` для представления структуры иерархии. Затем создаются запросы и производится управление данными с помощью иерархических методов.  
  
## <a name="requirements"></a>Требования  
 В системе должно быть установлено следующее.  
  
-   Любой выпуск [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] или более поздней версии.  
  
-   Среда [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] или [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] Express.  
  
-   Internet Explorer 6 или более поздней версии.  
  
## <a name="see-also"></a>См. также  
 [Учебник. Начало работы с ядром СУБД](../tutorial-getting-started-with-the-database-engine.md)   
 [Учебник. Написание инструкций Transact-SQL](../../t-sql/tutorial-writing-transact-sql-statements.md)   
 [Справочник по методам типа данных hierarchyid](/sql/t-sql/data-types/hierarchyid-data-type-method-reference)   
 [Иерархические данные &#40;SQL Server&#41;](../hierarchical-data-sql-server.md)   
 [hierarchyid (Transact-SQL)](/sql/t-sql/data-types/hierarchyid-data-type-method-reference)  
  
  
