---
title: Изменения в поведении полнотекстового поиска | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server], breaking changes
- behavior changes [full-text search]
- full-text indexes [SQL Server], breaking changes
ms.assetid: 573444e8-51bc-4f3d-9813-0037d2e13b8f
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 0d3bf42ec031415d16ea45bc8241c85c6d937c35
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2018
ms.locfileid: "52508869"
---
# <a name="behavior-changes-to-full-text-search"></a>Изменения в функциях полнотекстового поиска
  В этом разделе описаны изменения поведения полнотекстового поиска. Изменения в работе оказывают влияние на способ выполнения функций или взаимодействие между ними в [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] по сравнению с предыдущими версиями [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
## <a name="behavior-changes-in-full-text-search-in-includesssql14includessssql14-mdmd"></a>Изменения в работе полнотекстового поиска в [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 Сведения будут доступны позже.  
  
## <a name="behavior-changes-in-full-text-search-in-includesssql11includessssql11-mdmd"></a>Изменения в работе полнотекстового поиска в [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
 В [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] устанавливается новая версия средств разбиения по словам и парадигматических модулей для языков «Английский (США)» (код 1033) и «Английский (Соединённое Королевство)» (код 2057). Однако можно переключиться на предыдущую версию этих компонентов, если требуется сохранить предыдущий режим работы. Дополнительные сведения см. в статье [Изменение средства разбиения по словам, используемого для английского (США) и английского (Британского)](../relational-databases/search/change-the-word-breaker-used-for-us-english-and-uk-english.md).  
  
### <a name="new-word-breakers-and-stemmers-installed"></a>Установлены новые средства разбиения по словам и парадигматические модули  
 В выпуске [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] обновлены все средства разбиения по словам и парадигматические модули, используемые при полнотекстовом и семантическом поиске. Для обеспечения согласованности между содержимым индексов и результатами запросов рекомендуется выполнить повторное заполнение существующих полнотекстовых индексов.  
  
1.  Для английского языка добавлены новые средства разбиения по словам. Если необходимо сохранить поведение, существовавшее в предыдущем выпуске, см. раздел [Изменение средства разбиения текста на слова, используемого для английского языка (США и Великобритания)](../relational-databases/search/change-the-word-breaker-used-for-us-english-and-uk-english.md)  
  
2.  Средства разбиения по словам сторонних поставщиков для датского, польского и турецкого языков, входившие в предыдущие выпуски [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], заменены компонентами [!INCLUDE[msCoName](../includes/msconame-md.md)]. Эти новые компоненты включены по умолчанию.  
  
3.  Добавлены средства разбиения по словам для чешского и греческого языков. В предыдущих выпусках [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] компонент полнотекстового поиска (Full-Text Search) не поддерживал эти два языка.  
  
### <a name="behavior-changes-of-new-word-breakers-and-stemmers"></a>Изменения в поведении новых средств разбиения по словам и парадигматических модулей  
 Новые компоненты могут возвращать при заполнении полнотекстовых индексов и запросах к ним результаты, отличные от результатов, возвращаемых старыми компонентами. В следующих таблицах показаны некоторые различия, которые могут возникнуть в результатах на английском языке.  
  
 Сведения о сохранении прежнего поведения средства разбиения по словам и парадигматических модулей см. в следующих разделах:  
  
-   [Изменение средства разбиения текста на слова, используемого для английского языка (США и Соединенное Королевство)](../relational-databases/search/change-the-word-breaker-used-for-us-english-and-uk-english.md)  
  
-   [Восстановление предыдущих версий средств разбиения текста на слова, используемых поиском](../relational-databases/search/revert-the-word-breakers-used-by-search-to-the-previous-version.md)  
  
 В некоторых случаях новые компоненты возвращают *больше* результатов.  
  
|**Термин**|**Результаты с предыдущего разбиения по словам и парадигматического модуля**|**Результаты с помощью нового разбиения по словам и парадигматического модуля**|  
|--------------|--------------------------------------------------------|---------------------------------------------------|  
|cat-dog|cat<br /><br /> dog|cat<br /><br /> cat-dog<br /><br /> dog|  
|cat@dog.com|cat<br /><br /> com<br /><br /> dog|cat<br /><br /> cat@dog.com<br /><br /> com<br /><br /> dog|  
|12/11/2011<br /><br /> *(где терм — дата)*|12/11/2011<br /><br /> dd20111211|11<br /><br /> 12<br /><br /> 12/11/2011<br /><br /> 2011<br /><br /> dd20111211|  
  
 В некоторых случаях новые компоненты возвращают *подобные* результаты:  
  
|**Термин**|**Результаты с предыдущего разбиения по словам и парадигматического модуля**|**Результаты с помощью нового разбиения по словам и парадигматического модуля**|  
|--------------|--------------------------------------------------------|---------------------------------------------------|  
|100$|100$<br /><br /> nn100$|100$<br /><br /> nn100usd|  
|022|022<br /><br /> nn022|022<br /><br /> nn22|  
|10:49AM<br /><br /> *(где терм — время)*|10:49AM<br /><br /> tt1049|10:49AM<br /><br /> tt24104900|  
  
 В некоторых случаях новые компоненты возвращают *меньше* результатов, что может быть непредвиденным для приложений:  
  
|**Термин**|**Результаты с предыдущего разбиения по словам и парадигматического модуля**|**Результаты с помощью нового разбиения по словам и парадигматического модуля**|  
|--------------|--------------------------------------------------------|---------------------------------------------------|  
|jěˊÿqℭžl<br /><br /> *(где термы не являются допустимыми символами английского языка)*|«jěˊÿqℭžl»|je yq zl|  
|table's|table's<br /><br /> table|table's|  
|cat-|cat<br /><br /> cat-|cat|  
|v-z *(где v и z являются пропускаемыми словами)*|*(нет результатов)*|v-z|  
|$100 000 USD|$100<br /><br /> 000<br /><br /> nn000<br /><br /> nn100$<br /><br /> usd|$100 000 USD<br /><br /> nn100000usd|  
|beautiful U.S land|beautiful<br /><br /> land<br /><br /> u.s<br /><br /> us|beautiful<br /><br /> land|  
|Mt. Kent and Mt Challenger|challenger<br /><br /> kent<br /><br /> mt<br /><br /> Mt.|mt<br /><br /> kent<br /><br /> challenger|  
  
## <a name="behavior-changes-in-full-text-search-in-sql-server-2008"></a>Изменения в поведении полнотекстового поиска в SQL Server 2008  
 В [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] и более поздних версий, механизм полнотекстового поиска интегрировано как служба базы данных в реляционную базу данных как часть инфраструктуры подсистемы запросов и хранилища сервера. Новая архитектура полнотекстового поиска обеспечила достижение следующих целей.  
  
-   Интегрированного хранилища и управления полнотекстового поиска интегрировано непосредственно с присущие хранения и управления функциями [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], и служба MSFTESQL больше не существует.  
  
    -   Полнотекстовые индексы хранятся в файловых группах баз данных, а не в файловой системе. Административные операции с базой данных, например создание резервной копии, автоматически влияют на ее полнотекстовые индексы.  
  
    -   Полнотекстовый каталог теперь является виртуальным объектом, не принадлежащим ни одной файловой группе; он является логическим понятием, ссылающимся на группу полнотекстовых индексов. В связи с этим многие из функций управления каталогами устарели. Данное устаревание вызвало наличие критических изменений в некоторых функциях. Дополнительные сведения см. в разделе [нерекомендуемые функции ядра СУБД в SQL Server 2014](deprecated-database-engine-features-in-sql-server-2016.md) и [критические изменения полнотекстового поиска](breaking-changes-to-full-text-search.md).  
  
        > [!NOTE]  
        >  Инструкции DDL языка [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)][!INCLUDE[tsql](../includes/tsql-md.md)], указывающие полнотекстовые каталоги, работают правильно.  
  
-   Встроенной обработки новый компонент full-text search запроса обработчик запросов является частью компонента Database Engine и полностью интегрирован с обработчиком запросов SQL Server. Это означает, что оптимизатор запросов распознает полнотекстовые предикаты запросов и автоматически выполняет их наиболее эффективным способом.  
  
-   Улучшенные средства администрирования и устранения неполадок интегрированной full-text search предоставляет средства для анализа структур поиска, такие как полнотекстовый индекс, выходные данные заданного разбиения по словам, конфигурации стоп-слов и т. д.  
  
-   Пропускаемые слова и файлы пропускаемых слов были заменены стоп-словами и списками стоп-слов. Список стоп-слов представляет собой объект базы данных, обеспечивающий выполнение задач управления для стоп-слов и улучшающий целостность между различными экземплярами серверов и средами. Дополнительные сведения см. в разделе [Настройка стоп-слов и списков стоп-слов для полнотекстового поиска и управление ими](../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md).  
  
-   В [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] и более поздние версии включены новые средства разбиения по словам для многих языков, присутствующих в [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]. Остались без изменения только средства разбиения по словам для английского, корейского, тайского и китайского языков (всех форм). Для других языков, если полнотекстовый каталог был импортирован при [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] база данных была обновлена до [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] или более поздней версии, один или несколько языков, используемых полнотекстовыми индексами в полнотекстового каталога, могут быть связаны с новыми средствами, может отличаться от словам. Дополнительные сведения о том, как обеспечить соответствие между запросами и содержимым полнотекстового индекса см. в разделе [обновление полнотекстового поиска](../relational-databases/search/upgrade-full-text-search.md).  
  
-   Была добавлена служба FDHOST Launcher (MSSQLFDLauncher). Дополнительные сведения см. в разделе [приступить к работе с Full-Text Search](../relational-databases/search/get-started-with-full-text-search.md).  
  
-   Полнотекстовое индексирование работает с [FILESTREAM](../relational-databases/blob/filestream-sql-server.md) столбца таким же образом, как `varbinary(max)` столбца. В таблице FILESTREAM должен присутствовать столбец, в котором содержится расширение имени файла для каждого блока больших двоичных объектов (BLOB) FILESTREAM. Дополнительные сведения см. в разделе [запрос с Full-Text Search](../relational-databases/search/query-with-full-text-search.md),[Настройка и управление фильтрами для поиска](../relational-databases/search/configure-and-manage-filters-for-search.md), и [sys.fulltext_document_types &#40;Transact-SQL&#41; ](/sql/relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql).  
  
     Полнотекстовый поиск индексирует содержимое блоков больших двоичных объектов (BLOB) FILESTREAM. Индексирование таких файлов, как изображения, может оказаться нецелесообразным. При обновлении блоков больших двоичных объектов (BLOB) FILESTREAM выполняется их повторное индексирование.  
  
## <a name="see-also"></a>См. также  
 [Компонент Full-text Search](../relational-databases/search/full-text-search.md)   
 [Обратная совместимость Full-Text Search](../../2014/database-engine/full-text-search-backward-compatibility.md)   
 [Обновление полнотекстового поиска](../relational-databases/search/upgrade-full-text-search.md)   
 [Начало работы с компонентом Full-Text Search](../relational-databases/search/get-started-with-full-text-search.md)  
  
  
