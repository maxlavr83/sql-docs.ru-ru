---
title: dbo.syscategories (Transact-SQL) | Документация Майкрософт
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.syscategories_TSQL
- syscategories
- syscategories_TSQL
- dbo.syscategories
dev_langs:
- TSQL
helpviewer_keywords:
- syscategories system table
ms.assetid: eb2cb75c-dc58-4a5b-b329-664e9fe20ce0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0ee0509469f7a9bddca066a6e05416a13685ad9e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/01/2018
ms.locfileid: "47703522"
---
# <a name="dbosyscategories-transact-sql"></a>dbo.syscategories (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Содержит категории, используемые средой [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] для организации заданий, предупреждений и операторов. Эта таблица хранится в **msdb** базы данных.  
  
|Имя столбца|Тип данных|Описание|  
|-----------------|---------------|-----------------|  
|**category_id**|**int**|Идентификатор категории|  
|**category_class**|**int**|Тип элемента в категории:<br /><br /> **1** = задание<br /><br /> **2** = предупреждение<br /><br /> **3** =-оператор|  
|**category_type**|**tinyint**|Тип категории:<br /><br /> **1** = local<br /><br /> **2** = Многосерверная<br /><br /> **3** = нет|  
|**name**|**sysname**|Имя категории|  
  
  
