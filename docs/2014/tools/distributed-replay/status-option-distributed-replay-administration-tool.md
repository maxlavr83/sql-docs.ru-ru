---
title: Параметр состояния (средство администрирования распределенного воспроизведения) | Документы Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: ea89386e-1598-4412-8b37-680d14b2a5b6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 42e06144f35ab2db8f124dddff74fb836b6d9c4c
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/03/2018
ms.locfileid: "52761016"
---
# <a name="status-option-distributed-replay-administration-tool"></a>Параметр состояния (средство администрирования распределенного воспроизведения)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Средство администрирования распределенного воспроизведения `DReplay.exe`, это средство командной строки, которое можно использовать для взаимодействия с контроллером распределенного воспроизведения. В этой статье описан параметр командной строки **status** и соответствующий синтаксис.  
  
 Параметр **status** опрашивает контроллер и отображает его текущее состояние.  
  
 ![Topic link icon](../../database-engine/media/topic-link.gif "Значок ссылки на раздел") Дополнительные сведения о синтаксических обозначениях, используемых в синтаксисе средства администрирования, см. в разделе [Синтаксические обозначения в Transact-SQL (Transact-SQL)](/sql/t-sql/language-elements/transact-sql-syntax-conventions-transact-sql).  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
dreplay status [-mcontroller] [-fstatus_interval]  
```  
  
#### <a name="parameters"></a>Параметры  
 **-m** *controller*  
 Задает имя компьютера для контроллера. Локальный компьютер можно указать как «`localhost`» или «`.`».  
  
 Если параметр **-m** не задан, то используется локальный компьютер.  
  
 **-f** *status_interval*  
 Указывает частоту (в секундах) отображения состояния.  
  
 Если параметр **-f** не задан, то интервал по умолчанию составляет 30 секунд.  
  
## <a name="examples"></a>Примеры  
 В следующем примере текущий статус отображается каждые 60 секунд. Значение `localhost` указывает, что служба контроллера запущена на том же компьютере, что и средство администрирования.  
  
```  
dreplay status -m localhost -f 60  
```  
  
## <a name="permissions"></a>Разрешения  
 Средство администрирования должно запускаться как интерактивный пользователь, с учетной записью локального пользователя или пользователя домена. Для использования учетной записи локального пользователя средство администрирования и контроллер должны быть запущены на одном компьютере.  
  
 Дополнительные сведения см. в статье [Distributed Replay Security](distributed-replay-security.md).  
  
## <a name="see-also"></a>См. также  
 [Распределенное воспроизведение SQL Server](sql-server-distributed-replay.md)   
 [Отладчик Transact-SQL](../../relational-databases/scripting/transact-sql-debugger.md)  
  
  
