---
title: "MSSQLSERVER_17887 | Документация Майкрософт"
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 17887 (Database Engine error)
ms.assetid: ad0806e6-3296-4c32-b103-fccf0f8a8d3d
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 6aef26c0ef39217ea990f433e84751d87ca31345
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver17887"></a>MSSQLSERVER_17887
  
## <a name="details"></a>Сведения  
  
|||  
|-|-|  
|Название продукта|SQL Server|  
|Идентификатор события|17887|  
|Источник события|MSSQLSERVER|  
|Компонент|SQLEngine|  
|Символическое имя|SRV_IO_COMP_LISTENER_NONYIELDING|  
|Текст сообщения|Прослушиватель завершения операций ввода-вывода (0x%lx) исполнитель 0x%p, по-видимому, не возвращает управление узлу %ld. Примерная загрузка ЦП: ядро %I64d мс, пользователь %I64d мс, интервал: %I64d.|  
  
## <a name="explanation"></a>Объяснение  
Указывает на возможную проблему прослушивателя порта завершения операций ввода-вывода на указанном узле при выполнении подпрограммы завершения ввода-вывода для сетевого события чтения или записи. Эта ошибка исчезнет, когда прослушиватель порта завершения операций ввода-вывода на указанном узле вернет управление после выполнения подпрограммы завершения ввода-вывода.  
  
## <a name="user-action"></a>Действие пользователя  
Обратитесь в службу поддержки пользователей Майкрософт.  
  
