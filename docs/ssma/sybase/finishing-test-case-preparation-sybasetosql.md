---
title: "Завершение подготовки тестового случая (SybaseToSQL) | Документы Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
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
- Tester Component,Test Case Settings
ms.assetid: 8b2a49b0-4296-4f3f-9e56-323aa6a6fa8e
caps.latest.revision: 6
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 7568e7a78e0129204a23797cbc589139816ac13e
ms.contentlocale: ru-ru
ms.lasthandoff: 08/02/2017

---
# <a name="finishing-test-case-preparation-sybasetosql"></a>Завершение подготовки тестового случая (SybaseToSQL)
Последней странице мастера отображается описание тестового случая и сведения об объектах, задействованных в тесте. Кроме того на этой странице можно задать теста параметры выполнения.  
  
**Сведения тестового случая** разделе показаны имя тестового случая и описание.  
  
**Тестовые объекты** раздел содержит список именованных протестированных объекты, сгруппированные по типу объекта.  
  
**Затронутые объекты анализируемых** раздел список именованных объектов, какие изменения данных должны сравниваться после выполнения протестированных объектов.  
  
## <a name="test-case-settings"></a>Параметры тестовых случаев  
В **параметры тестового случая** раздела, можно задать выполнение следующих параметров теста:  
  
### <a name="stop-test-execution-after-first-failure"></a>Остановить выполнение теста после первой ошибки  
Указывает на прерывание выполнения теста при возникновении ошибки во время выполнения теста.  
  
-   При выборе **Да**, тестирование прерывания выполнения, если происходит ошибка.  
  
-   При выборе **нет**, выполнение теста продолжает работу после возникновения ошибки.  
  
### <a name="perform-data-rollback"></a>Выполнить откат данных  
Включите автоматические данные откат после выполнения теста.  
  
-   При выборе **Да**, данные изменения будут утеряны после выполнения теста.  
  
-   При выборе **нет**, все тестовые выполнения изменения данных будут сохранены.  
  
### <a name="auxiliary-tables-saving-mode"></a>Дополнительные таблицы, в режиме энергосбережения  
Определяет режим сохранения для вспомогательных таблиц, создаваемых во время выполнения теста. См. в описании вспомогательных таблицах в [выполнение тестовых случаев &#40; SybaseToSQL &#41; ](../../ssma/sybase/running-test-cases-sybasetosql.md) раздела.  
  
-   При выборе **всегда сохранять**, для использования в дальнейшем всегда будут храниться данные вспомогательных таблиц.  
  
-   При выборе **сохранить, если не удалось выполнить сравнение таблиц**, вспомогательных таблиц данных будут храниться только в том случае, если происходит ошибка.  
  
-   При выборе **всегда удалять**, вспомогательных таблицах всегда удаляются после выполнения теста.  
  
-   При выборе **попросите пользователя, если не удалось выполнить сравнение таблиц**, пользователь может выбрать необходимое действие, если происходит ошибка.  
  
Нажмите кнопку **Готово** кнопку, чтобы сохранить тестовый случай, подготовленного в [репозиториев теста с помощью &#40; SybaseToSQL &#41; ](../../ssma/sybase/using-test-repositories-sybasetosql.md).  
  
## <a name="see-also"></a>См. также:  
[С помощью репозиториев теста &#40; SybaseToSQL &#41;](../../ssma/sybase/using-test-repositories-sybasetosql.md)  
[Выполнение тестовых случаев &#40; SybaseToSQL &#41;](../../ssma/sybase/running-test-cases-sybasetosql.md)  
[Тестирование миграции объектов базы данных &#40; SybaseToSQL &#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
