---
title: "Перенос данных Access в SQL Server — базы данных Azure SQL (AccessToSQL) | Документы Microsoft"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- bulk loading data
- data, loading into SQL Azure
- data, loading into SQL Server
- migrating databases, loading data
- migrating databases, options
- options, migrating data
- SQL Azure, migrating data into
- SQL Server, migrating data into
ms.assetid: f3b18af7-1af0-499d-a00d-a0af94895625
caps.latest.revision: 17
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: f6d51cc33d972fc49352ccbf382f6b0193195d9e
ms.contentlocale: ru-ru
ms.lasthandoff: 08/02/2017

---
# <a name="migrating-access-data-into-sql-server---azure-sql-db-accesstosql"></a>Перенос данных Access в SQL Server — базы данных Azure SQL (AccessToSQL)
После успешного создания объектов базы данных в [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], можно перенести данные с доступом к [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] или SQL Azure.  
  
## <a name="setting-migration-options"></a>Настройка параметров миграции  
Прежде чем переносить данные в [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] или SQL Azure, проверьте параметры миграции проекта в **параметры проекта** диалоговое окно. В этом диалоговом окне можно задать размер пакета миграции, блокировка таблицы, ограничения проверки, выполнения, удостоверений и обработке, значение null триггеров вставки и как обрабатывать даты из [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] диапазона. Дополнительные сведения см. в разделе [параметры проекта (миграция)](http://msdn.microsoft.com/en-us/4caebc9c-8680-4b99-a8fa-89c43161c95d).  
  
## <a name="migrating-data"></a>Перенос данных  
Миграция данных является операцией массовой загрузки, которая перемещает строки данных в [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] или SQL Azure в транзакциях. Число строк, загружаемых в [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] или SQL Azure в одной транзакции, настроенным в параметрах проекта.  
  
Для просмотра сообщений о миграции, убедитесь, что отображается область вывода. Если это не так, на **представление** последовательно выберите пункты **вывода**.  
  
**Для переноса данных**  
  
1.  Убедитесь, что вы загрузили объекты баз данных Access в [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] или SQL Azure.  
  
2.  Выберите объекты, которые содержат данные, которые требуется перенести в обозревателе метаданных доступа:  
  
    -   Чтобы выполнить миграцию данных для всей базы данных, установите флажок рядом с именем базы данных.  
  
    -   Для переноса данных из отдельных таблиц, разверните базу данных, затем **таблиц**, а затем установите флажок рядом с таблицей. Чтобы исключить данные из отдельных таблиц, снимите флажок.  
  
3.  Щелкните правой кнопкой мыши **баз данных** , а затем выберите **переноса данных**.  
  
Данные за пределами SSMA можно перенести с помощью [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **bcp** программы командной строки или [!INCLUDE[ssISnoversion](../../includes/ssisnoversion_md.md)]. Дополнительные сведения об этих средствах см. в разделе [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] электронной документации.  
  
## <a name="next-step"></a>Следующий шаг  
При наличии приложения баз данных Access, которые вы хотите продолжать использовать после миграции, связь между таблицами базы данных доступ к [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] или таблиц SQL Azure. Дополнительные сведения см. в разделе [связывания приложения Access в SQL Server](http://msdn.microsoft.com/en-us/82374ad2-7737-4164-a489-13261ba393d4).  
  
## <a name="see-also"></a>См. также:  
[Миграция баз данных Access в SQL Server](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
[Преобразование параметра и варианты миграции](http://msdn.microsoft.com/en-us/0a7304df-2f35-4453-96ef-7ac83dea1167)  
  
