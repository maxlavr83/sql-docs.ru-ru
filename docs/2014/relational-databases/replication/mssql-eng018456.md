---
title: MSSQL_ENG018456 | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG018456 error
ms.assetid: 3daa8144-d81f-445a-b6c3-4bb3e9fd1526
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ff5d5a983bda1dd5efa68c282373f37ab8fda571
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/03/2018
ms.locfileid: "52750316"
---
# <a name="mssqleng018456"></a>MSSQL_ENG018456
    
## <a name="message-details"></a>Сведения о сообщении  
  
|||  
|-|-|  
|Название продукта|SQL Server|  
|Идентификатор события|18456|  
|Источник события|MSSQLSERVER|  
|Компонент|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Символическое имя||  
|Текст сообщения|Ошибка входа пользователя '%.*ls'.%.\*ls|  
  
## <a name="explanation"></a>Объяснение  
 Ошибка MSSQL_ENG018456 возникает при неудачной попытке входа в систему. Если сообщение об ошибке включает учетную запись **distributor_admin** (Ошибка входа пользователя 'distributor_admin'.), проблема заключается в учетной записи, которая используется репликацией. Репликация создает удаленный сервер **repl_distributor**, предоставляющий возможность обмена данными между распространителем и издателем. Имя входа **distributor_admin** связано с этим удаленным сервером и должно иметь правильный пароль.  
  
## <a name="user-action"></a>Действие пользователя  
 Убедитесь в том, что для учетной записи указан пароль. Дополнительные сведения см. в разделе [Организация безопасности распространителя](security/secure-the-distributor.md).  
  
## <a name="see-also"></a>См. также  
 [Справочник по ошибкам и событиям (репликация)](errors-and-events-reference-replication.md)  
  
  
