---
title: dbo.sysdac_instances (Transact-SQL) | Документация Майкрософт
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysdac_instances_TSQL
- sysdac_instances
- sysdac_instances_TSQL
- dbo.sysdac_instances
dev_langs:
- TSQL
helpviewer_keywords:
- dbo.sysdac_instances
- sysdac_instances
ms.assetid: 28285f3d-3889-439f-8b24-3bdef08e46b4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 049f3d0201957cfee5d7bc88301c6af97c0b6dcb
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2018
ms.locfileid: "51660684"
---
# <a name="data-tier-application-views---dbosysdacinstances"></a>Представления приложения уровня данных — dbo.sysdac_instances
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Отображает по одной строке для каждого экземпляра приложения уровня данных (DAC), развернутого на экземпляре [!INCLUDE[ssDE](../../includes/ssde-md.md)]. sysdac_instances принадлежит схеме dbo в базе данных msdb. Следующая таблица описывает столбцы в представлении sysdac_instances.  
  
|Имя столбца|Тип данных|Описание|  
|-----------------|---------------|-----------------|  
|instance_id|**uniqueidentifier**|Идентификатор экземпляра DAC.|  
|имя_экземпляра|**sysname**|Имя экземпляра приложения уровня данных, указанное при развертывании DAC.|  
|type_name|**sysname**|Имя DAC, указанное при создании пакета DAC.|  
|type_version|**Nvarchar(64)**|Версия DAC, указанная при создании пакета DAC.|  
|description|**nvarchar(4000)**|Описание DAC, записанное при создании пакета DAC.|  
|type_stream|**varbinary(max)**|Битовый поток, который содержит закодированное представление логических объектов, таких как таблицы и представления, содержащихся в DAC.|  
|date_created|**datetime**|Дата и время создания экземпляра DAC.|  
|created_by|**sysname**|Имя входа, создавшее экземпляр DAC.|  
|database_name|**sysname**|Имя базы данных, созданной для экземпляра DAC.|  
  
## <a name="remarks"></a>Примечания  
 DAC включает тип DAC, который представляет собой определение логических объектов уровня данных, используемых приложением, таких как таблицы и представления. Пакет DAC представляет собой файл, используемый для развертывания DAC. Пакет DAC содержит представление всех логических объектов, содержащихся в типе DAC. Пакет DAC может использоваться для развертывания одной или нескольких копий или экземпляров DAC на экземпляре компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Каждый экземпляр DAC, развернутый одним и тем же пакетом DAC, имеет одинаковый с другими экземплярами тип, но ему присваиваются уникальные имя и идентификатор экземпляра.  
  
## <a name="permissions"></a>Разрешения  
 Требует членства в предопределенной роли сервера sysadmin для просмотра всех столбцов. Члены роли public могут просматривать столбцы instance_name, description и type_version.  
  
## <a name="see-also"></a>См. также  
 [Приложения уровня данных](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [Представления приложения уровня данных &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/0de01328-d7a6-4677-b7a0-dcd3098c23d4)  
  
  
