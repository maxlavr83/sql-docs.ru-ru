---
title: Остановка системного управления версиями в темпоральной таблице с системным управлением версиями | Документация Майкрософт
ms.custom: ''
ms.date: 10/11/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: dddd707e-bfb1-44ff-937b-a84c5e5d1a94
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 37fe6d7b3dfe92e2cdf53e7a7b26ab363a567510
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/27/2018
ms.locfileid: "52409170"
---
# <a name="stopping-system-versioning-on-a-system-versioned-temporal-table"></a>Остановка системного управления версиями в темпоральной таблице с системным управлением версиями
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Возможно, вам временно или навсегда понадобится остановить управление версиями в темпоральной таблице.   
Для этого нужно задать для предложения **SYSTEM_VERSIONING** значение **OFF**.  
  
## <a name="setting-systemversioning--off"></a>Установка для предложения SYSTEM_VERSIONING значения OFF  
 Остановите системное управление версиями, если в темпоральной таблице нужно провести определенные операции обслуживания или таблица с управлением версиями больше не нужна. В результате этой операции вы получите две отдельные таблицы:  
  
-   текущую таблицу с определением периода;  
  
-   прежнюю таблицу в качестве обычной таблицы.  
  
### <a name="important-remarks"></a>Важные замечания  
  
-   Если задать значение  **SYSTEM_VERSIONING = OFF** или удалить период **SYSTEM_TIME** , это не приведет к потере данных.  
  
-   Если задать **SYSTEM_VERSIONING = OFF** и не исключить удаление периода **SYSTEM_TIME** , система продолжит обновлять столбцы периода при каждой операции вставки и обновления. Элементы, удаленные из текущей таблицы, не подлежат восстановлению.  
  
-   Удалите период **SYSTEM_TIME** , чтобы полностью удалить столбцы периода.  
  
-   Если задать **SYSTEM_VERSIONING = OFF**, все пользователи с необходимыми разрешениями смогут изменять схему и содержимое прежней таблицы или даже окончательно удалить ее.  
  
### <a name="permanently-remove-systemversioning"></a>Окончательное удаление SYSTEM_VERSIONING  
 В этом примере окончательно удаляется параметр SYSTEM_VERSIONING и полностью удаляются столбцы периода. Удалять столбцы периода необязательно.  
  
```  
ALTER TABLE dbo.Department SET (SYSTEM_VERSIONING = OFF);   
/*Optionally, DROP PERIOD if you want to revert temporal table to a non-temporal*/   
ALTER TABLE dbo.Department   
DROP PERIOD FOR SYSTEM_TIME;  
  
```  
  
### <a name="temporarily-remove-systemversioning"></a>Временное удаление SYSTEM_VERSIONING  
 Это список операций, которые требуют, чтобы для системного управления версиями было задано значение **OFF**:  
  
-   удаление ненужных данных из журнала (**DELETE** или **TRUNCATE**);  
  
-   удаление данных из текущей таблицы без управления версиями (**DELETE**, **TRUNCATE**);  
  
-   секционирование **SWITCH OUT** из текущей таблицы;  
  
-   секционирование **SWITCH IN** в прежнюю таблицу.  
  
 В этом примере действие SYSTEM_VERSIONING временно прекращается для выполнения определенных операций обслуживания. Если необходимо временно остановить управление версиями для обслуживания таблицы, настоятельно рекомендуем делать это в ходе транзакции, чтобы обеспечить согласованность данных.  
  
```  
BEGIN TRAN   
ALTER TABLE dbo.Department SET (SYSTEM_VERSIONING = OFF);   
TRUNCATE TABLE [History].[DepartmentHistory]   
WITH (PARTITIONS (1,2))   
ALTER TABLE dbo.Department SET    
(   
SYSTEM_VERSIONING = ON (HISTORY_TABLE = History.DepartmentHistory)   
);   
COMMIT ;  
  
```  
  
## <a name="see-also"></a>См. также:  
 [Темпоральные таблицы](../../relational-databases/tables/temporal-tables.md)   
 [Приступая к работе c темпоральными таблицами с системным управлением версиями](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)   
 [Управление хранением данных журнала в темпоральных таблицах с системным управлением версиями](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [Темпоральные таблицы с системным управлением версиями и таблицы, оптимизированные для памяти](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [Создание темпоральной таблицы с системным управлением версиями](../../relational-databases/tables/creating-a-system-versioned-temporal-table.md)   
 [Изменение данных в темпоральной таблице с системным управлением версиями](../../relational-databases/tables/modifying-data-in-a-system-versioned-temporal-table.md)   
 [Запрос данных в темпоральной таблице с системным управлением версиями](../../relational-databases/tables/querying-data-in-a-system-versioned-temporal-table.md)   
 [Изменение схемы темпоральной таблицы с системным управлением версиями](../../relational-databases/tables/changing-the-schema-of-a-system-versioned-temporal-table.md)  
  
  
