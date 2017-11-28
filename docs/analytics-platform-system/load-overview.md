---
title: "Загрузить"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.suite: sql
ms.custom: 
ms.technology: mpp-data-warehouse
description: "Можно загрузить или вставки данных в SQL Server Parallel данных хранилища (PDW) с помощью служб Integration Services, программа bcp, dwloader или инструкцию SQL INSERT."
ms.date: 10/20/2016
ms.topic: article
ms.assetid: c7292108-4a48-409e-b0f4-e4ba84dce26f
caps.latest.revision: "22"
ms.openlocfilehash: bef6cf70573aaac642665b9f1e847f4b251e39e9
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/17/2017
---
# <a name="load-sql-server-pdw"></a>Загрузка (SQL Server PDW)
Можно загрузить или вставки данных в SQL Server Parallel данных хранилища (PDW) с помощью служб Integration Services [программа bcp](../tools/bcp-utility.md), **dwloader** загрузчика командной строки или инструкции SQL INSERT.  

## <a name="loading-environment"></a>Среда загрузки  
Чтобы загрузить данные, требуется один или несколько серверов загрузки. Можно использовать собственные существующих ETL или других серверах, или можно приобрести новые серверы. Дополнительные сведения см. в разделе [приобретать и настраивать сервер загрузки](acquire-and-configure-loading-server.md). Эти инструкции включают [загрузке листа планирования емкости сервера](loading-server-capacity-planning-worksheet.md) при планировании подходящее решение для загрузки.  
  
## <a name="load-with-dwloader"></a>Загрузка с помощью dwloader  
С помощью [dwloader командной строки загрузчика](dwloader.md) является самым быстрым способом загрузить данные в PDW.  
  
![Процесс загрузки](media/loading-process.png "процесс загрузки")  
  
dwloader загружает данные непосредственно в вычислительные узлы без передачи данных через узел элемента управления. Чтобы загрузить данные, сначала dwloader взаимодействует с узла управления для получения контактных данных для вычислительных узлов. dwloader настраивает канал связи с каждым узлом вычислений, а затем отправляет фрагменты 256 КБ данных вычислительных узлов в циклического перебора.  
  
На каждом вычислительном узле службы перемещения данных (DMS) получает и обрабатывает фрагменты данных. Обработка данных включает в себя преобразование каждой строки в собственном формате SQL Server и вычисления хэша распространения для определения вычислительных узлов, к которой принадлежит каждая строка.  
  
После обработки строк, DMS использует перемещения в случайном порядке для передачи каждой строки на правильный вычислительного узла и экземпляра SQL Server. Как SQL Server получает строки, включающий их согласно **-b** установите параметр размера пакета в dwloader, а затем выполняет массовую загрузку пакета.  

## <a name="load-with-prepared-statements"></a>Загрузка с помощью подготовленных инструкций

Подготовленные инструкции можно использовать для загрузки данных в распределенных и реплицированной таблицы. Если входные данные не соответствует в целевой тип данных, выполняется неявное преобразование. Неявные преобразования, поддерживаемые PDW подготовленных инструкций являются подмножеством преобразования, поддерживаемые SQL Server. То есть поддерживаются только подмножество преобразования, но также поддерживаемое преобразование соответствует неявные преобразования в SQL Server. Независимо от того, определен ли целевой таблицы для загрузки как распределенные или реплицированной таблицы неявных преобразований (при необходимости) для всех столбцов, которые существуют в целевой таблице. 

<!-- MISSING LINK
For more information, see [Prepared statements](prepared-statements.md).
-->
  
## <a name="related-tasks"></a>Связанные задачи  
  
|Задача|Description|  
|--------|---------------|  
|Создание промежуточной базы данных.|[Создание промежуточной базы данных](staging-database.md)|  
|Загрузить со службами Integration Services.|[Загрузка с помощью служб Integration Services](load-with-ssis.md)|  
|Понимать преобразования типов для dwloader.|[Правила преобразования типов данных для dwloader](dwloader-data-type-conversion-rules.md)|  
|Загрузка данных с dwloader.|[dwloader загрузчика командной строки](dwloader.md)|  
|Понимать преобразования типов для вставки.|[Загрузка данных с помощью INSERT](load-with-insert.md)|  
 
<!-- MISSING LINKS
## See Also  
[Grant permissions to load data](grant-permissions-to-load-data.md)  
[Common metadata query examles](metadata-query-examples.md)  
  
-->