---
title: Экспорт отчетов (построитель отчетов и службы SSRS) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- "10437"
ms.assetid: a2bab8c1-505d-4da3-b1db-ea0ae13b2336
caps.latest.revision: 18
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: f4760d57cec11c6955e1ad87d4278d6c22a55ee7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2018
ms.locfileid: "37255806"
---
# <a name="exporting-reports-report-builder-and-ssrs"></a>Экспорт отчетов (построитель отчетов и службы SSRS)
  После запуска отчета его можно экспортировать в другой формат, например Excel или PDF, либо экспортировать отчет путем создания сервисного документа Atom, в котором перечислены совместимые с Atom веб-каналы данных, доступные в отчете.  
  
 Экспортируйте отчет, чтобы можно было делать следующее.  
  
-   Работать с данными отчета в другом приложении. Например, можно экспортировать отчет в Excel и продолжить работу с данными в Excel.  
  
-   Печатать отчет в другом формате. Например, можно экспортировать отчет в формат PDF-файла, а затем вывести его на печать.  
  
-   Сохранять копии отчета в файле другого формата. Например, можно экспортировать отчет в Word, а затем сохранить документ, создав копию отчета.  
  
-   Использовать данные отчета в качестве веб-канала данных в приложениях. Например, можно создать Atom-совместимые веб-каналы данных, которые может обрабатывать клиент [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , а затем работать с этими данными в [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)].  
  
 Выполнить экспорт можно с помощью панели инструментов в средстве просмотра отчетов диспетчера отчетов, которая отображается в верхней части каждого отчета во время просмотра отчета на сервере отчетов, и с помощью ленты построителя отчетов при предварительном просмотре отчета. Параметр веб-канала данных доступен только в диспетчере отчетов.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] предоставляют несколько модулей подготовки отчетов, поддерживающих экспорт в общеупотребимые форматы. Модули подготовки отчетов поддерживают форматы с мягкими разрывами страниц (например, Word или Excel), жесткими разрывами страниц (например, PDF или TIFF) либо только с данными (например, CSV или Atom-совместимый XML).  
  
 Чтобы быстро начать работу с экспорту отчетов и формированию Atom совместимые потоки данных из отчетов, см. в разделе [Экспорт отчета в файл другого типа &#40;построитель отчетов и службы SSRS&#41; ](../export-a-report-as-another-file-type-report-builder-and-ssrs.md) и [создания веб-каналов данных из Отчет &#40;построитель отчетов и службы SSRS&#41;](generate-data-feeds-from-a-report-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="RendererTypes"></a> Типы модулей подготовки отчетов  
 Службы [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] предоставляют три типа модулей подготовки отчетов.  
  
-   **Модули подготовки данных.** Модули подготовки данных исключают из отчета всю информацию о форматировании и макете и отображают только данные. Результирующий файл может использоваться для импорта бесформатных данных отчета в файл другого типа, такой как Excel, в другую базу данных, в сообщение XML-данных или в пользовательское приложение. Модули подготовки данных не поддерживают разрывы страниц.  
  
     Поддерживаются следующие типы модулей подготовки данных: CSV, XML и Atom.  
  
-   **Модули подготовки отчетов с мягкими разрывами страниц.** Модули подготовки отчетов с мягкими разрывами страниц сохраняют макет и форматирование отчета. Результирующий файл оптимизирован для просмотра на экране и доставки, например в виде веб-страниц или в виде элементов управления **ReportViewer** .  
  
     Поддерживаются следующие модули подготовки отчетов к просмотру: [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel, [!INCLUDE[msCoName](../../includes/msconame-md.md)] Word и веб-архив (MHTML).  
  
-   **Модули подготовки отчетов с жесткими разрывами страниц.** Модули подготовки отчетов с жесткими разрывами страниц сохраняют макет и форматирование отчета. Результирующий файл оптимизирован для согласованного представления при печати или для просмотра отчета в режиме в сети в виде книги.  
  
     Поддерживаются следующие модули подготовки отчетов к печати: TIFF и PDF.  
  
##  <a name="ExportFormats"></a> Форматы экспорта  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] предоставляют модули подготовки отчетов, которые подготавливают отчеты в различных форматах. Если планируется использовать эту функцию, следует оптимизировать структуру отчета в соответствии с выбранным форматом файла. Раздел по каждому модулю подготовки отчетов содержит подробные сведения о подготовке отчета в соответствующем формате.  
  
 В следующей таблице приводятся доступные форматы.  
  
|Формат|Тип модуля подготовки отчетов|Описание|  
|------------|------------------------------|-----------------|  
|CSV|Данные |Модуль подготовки отчетов в формате с разделителями-запятыми (CSV) готовит отчеты для просмотра в виде плоских представлений данных стандартизованного текстового вида. Этот формат легко читается и может использоваться для обмена со многими приложениями.<br /><br /> Дополнительные сведения см. в разделе [Exporting to a CSV File &#40;Report Builder and SSRS&#41;](exporting-to-a-csv-file-report-builder-and-ssrs.md).|  
|Excel|Мягкие разрывы страниц|Модуль подготовки отчетов Excel подготавливает отчет как документ Excel, которая совместима с [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 2007 – 2010, а также [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 2003 с пакетом совместимости Microsoft Office для Word, Excel и PowerPoint установлен. При экспорте отчетов на лист Excel некоторые исходные элементы макета теряются. Свойства отчета и групп внутри отчета можно задать таким образом, чтобы имена листам присваивались при экспорте в Excel. Файлы, созданные этим модулем подготовки отчетов, имеют расширение xlsx.<br /><br /> Дополнительные сведения см. в разделе [Exporting to Microsoft Excel &#40;Report Builder and SSRS&#41;](exporting-to-microsoft-excel-report-builder-and-ssrs.md).<br /><br /> Примечание: Excel 2003 модулю подготовки отчетов обрабатывает собственный формат [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 2003, доступен в некоторых сценариях отчетов.|  
|Word|Мягкие разрывы страниц|Модуль подготовки отчетов Word подготавливает отчет как документ Word, совместимый с [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 2007 – 2010, а также [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 2003 с [!INCLUDE[msCoName](../../includes/msconame-md.md)] пакет обеспечения совместимости Microsoft Office для Word, Excel и PowerPoint установлен. После экспорта отчета в документ Word можно изменить содержимое отчета и спроектировать отчеты в стиле документа, такие как наклейки для почтовой рассылки, заказы на покупку или стандартные письма. Файлы, созданные этим модулем подготовки отчетов, имеют расширение docx.<br /><br /> Дополнительные сведения см. в разделе [Экспорт в Microsoft Word (построитель отчетов и службы SSRS)](exporting-to-microsoft-word-report-builder-and-ssrs.md).<br /><br /> Примечание: Word 2003 модулю подготовки отчетов обрабатывает собственный формат [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 2003, доступен в некоторых сценариях отчетов.|  
|Веб-архив|Мягкие разрывы страниц|Модуль подготовки отчетов в формате HTML подготавливает отчет к просмотру в HTML-формате. Модуль подготовки отчетов также позволяет создавать полностью сформированные HTML-страницы или фрагменты HTML для внедрения в другие HTML-страницы. Все документы HTML создаются в кодировке UTF-8.<br /><br /> Модуль подготовки отчетов в формате HTML используется по умолчанию для отчетов, просматриваемых предварительно в построителе отчетов, затем в браузере, в том числе при запуске в диспетчере отчетов.<br /><br /> Дополнительные сведения см. в разделе [Rendering to HTML &#40;Report Builder and SSRS&#41;](rendering-to-html-report-builder-and-ssrs.md).|  
|Файл Acrobat (PDF)|Жесткие разрывы страниц|Модуль подготовки отчетов в формате PDF создает отчет в файлах, которые можно открыть в Adobe Acrobat и других средствах просмотра PDF сторонних разработчиков, поддерживающих формат PDF 1.3. Хотя формат PDF версии 1.3 совместим с Adobe Acrobat 4.0 и более поздними версиями, службы [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] поддерживают Adobe Acrobat 6 или более поздние версии. Модуль подготовки отчетов не требует программного обеспечения Adobe для создания отчета. Однако средства просмотра PDF, например Adobe Acrobat, необходимы для просмотра или печати отчетов в формате PDF.<br /><br /> Дополнительные сведения см. в разделе [Экспорт в PDF-файл (построитель отчетов и службы SSRS)](exporting-to-a-pdf-file-report-builder-and-ssrs.md).|  
|TIFF-файл|Жесткие разрывы страниц|Модуль подготовки отчетов изображений преобразует отчет в битовую карту или метафайл. По умолчанию модуль подготовки изображения создает отчет в файле TIFF, который можно просматривать на нескольких страницах. Полученное изображение клиент может просмотреть в программе просмотра изображений и распечатать.<br /><br /> Модуль подготовки изображений способен создавать файлы в любых форматах, поддерживаемых [!INCLUDE[ndptecgdiplus](../../includes/ndptecgdiplus-md.md)]: BMP, EMF, EMFPlus, GIF, JPEG, PNG и TIFF.<br /><br /> Дополнительные сведения см. в разделе [Exporting to an Image File &#40;Report Builder and SSRS&#41;](exporting-to-an-image-file-report-builder-and-ssrs.md).|  
|XML|Данные|Модуль подготовки XML-отчета возвращает отчет в XML-формате. Схема для XML-документа, используемого в отчете, создается специально для этого отчета и содержит только данные. Данные макета не обрабатываются модулем подготовки XML-отчета, и разбивка на страницы не сохраняется. XML-документ, сформированный данным модулем, можно импортировать в базу данных, использовать как сообщение XML-данных или отправить пользовательскому приложению.<br /><br /> Дополнительные сведения см. в разделе [Exporting to XML &#40;Report Builder and SSRS&#41;](exporting-to-xml-report-builder-and-ssrs.md).|  
|Atom|Данные |Модуль подготовки отчетов Atom создает на основе отчетов веб-канал данных, совместимый с Atom. Веб-каналы данных доступны для чтения и обмена данными с такими приложениями, как клиент [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , работающими с Atom-совместимыми веб-каналами данных.<br /><br /> Выводом является сервисный документ Atom, в котором перечислены веб-каналы данных, доступные из отчета. Для каждой области данных отчета создается по крайней мере один веб-канал данных. В зависимости от типа области данных и самих данных, которые отображает эта область, может быть создано несколько веб-каналов данных.<br /><br /> Дополнительные сведения см. в разделе [Generating Data Feeds from Reports &#40;Report Builder and SSRS&#41;](generating-data-feeds-from-reports-report-builder-and-ssrs.md).|  
  
##  <a name="ExportingReport"></a> Экспорт отчета  
 Чтобы экспортировать отчет, запустите его в диспетчере или построителе отчетов, а затем выберите формат в раскрывающемся списке «Экспорт». Появится приглашение о сохранении или открытии файла. При выборе **Открыть**отчет откроется в приложении, которое связано с выбранным форматом подготовки отчета. (Например, если выбран формат **Excel** , отчет открывается в Excel.) При выборе **Сохранить**отчет сохраняется. Например, при экспорте в Excel отчет сохраняется с расширением XLS. Приложение, в котором будут открываться отчеты в каждом формате, зависит от сопоставления файлов на данном локальном компьютере. Дополнительные сведения см. в разделе [Экспорт отчета в файл другого типа &#40;построитель отчетов и службы SSRS&#41;](../export-a-report-as-another-file-type-report-builder-and-ssrs.md).  
  
 Сервер отчетов экспортирует отчет в том виде, в каком он представлен во время текущего пользовательского сеанса. Если какой-либо пользователь отчета опубликует обновленную версию отчета, открытого в данный момент другим пользователем, либо данные, отображаемые в отчете, изменятся, экспортируемый отчет не обновится.  
  
 При экспорте отчета в другой формат может измениться разбиение отчета на страницы. Во время предварительного просмотра отчет отображается после обработки модулем подготовки отчетов в формате HTML, который следует правилам мягкого разрыва страниц. Если отчет экспортируется в другой формат файлов, например в Adobe Acrobat (PDF), разбиение на страницы выполняется на основе физического размера страницы (применяются правила жесткого разрыва страниц). Страницы также могут разделяться логическими разрывами страниц, добавленными в отчет, но фактическая длина страницы изменяется в зависимости от типа используемого модуля подготовки отчетов. Чтобы изменить разбиение на страницы для отчета, необходимо ознакомиться с правилами разбиения на страницы выбранного модуля подготовки отчетов. Может понадобиться изменить макет отчета в соответствии с этим модулем подготовки отчетов. Дополнительные сведения см. в разделе [Макет страницы и подготовка к просмотру (построитель отчетов и службы SSRS)](../report-design/page-layout-and-rendering-report-builder-and-ssrs.md).  
  
##  <a name="GeneratingDataFeedsFromReport"></a> Формирование веб-каналов данных из отчета  
 Чтобы создать веб-каналы данных на основе отчета, запустите диспетчер отчетов, затем щелкните значок **Создать канал данных** на панели инструментов диспетчера отчетов. Появится приглашение о сохранении или открытии файла. При выборе команды **Открыть**сервисный документ Atom откроется в приложении, связанном с расширением файла ATOMSVC. При выборе команды **Сохранить**документ сохраняется в файле с расширением ATOMSVC. По умолчанию имя файла совпадает с именем отчета. Это имя можно заменить на более осмысленное.  
  
 Сервисный документ Atom будет сохранен на компьютере. Позднее можно передать его на сервер отчетов или другой сервер, чтобы он был доступен другим пользователям. Дополнительные сведения см. в разделах [Формирование веб-каналов данных из отчетов (построитель отчетов и службы SSRS)](generating-data-feeds-from-reports-report-builder-and-ssrs.md) и [Формирование веб-каналов данных из отчета (построитель отчетов и службы SSRS)](generate-data-feeds-from-a-report-report-builder-and-ssrs.md).  
  
##  <a name="Troubleshooting"></a> Устранение неполадок, связанных с экспортированными отчетами  
 Иногда отчеты после экспорта в другой формат могут выглядеть по-другому или не работать должным образом. Это связано с тем, что к модулю подготовки отчетов могут применяться определенные правила или ограничения. Многие ограничения можно преодолеть, учитывая их во время создания отчета. Возможно, потребуется несколько изменить макет отчета, тщательно выровнять элементы в отчете, ограничить колонтитулы отчета одной строкой текста и так далее.  
  
 Если в отчете содержится текст в формате Юникод с арабскими цифрами или даты на арабском, при экспорте отчета в любом из следующих форматов или его печати даты и цифры отображаются некорректно.  
  
-   PDF  
  
-   Word  
  
-   Excel  
  
-   Изображение/TIFF  
  
 При экспорте отчета в формате HTML даты и цифры отображаются правильно.  
  
 В разделах, относящихся к конкретным модулям подготовки, описывается механизм подготовки элементов отчетов и областей данных к просмотру, а также ограничения и способы их обхода для каждого из модулей подготовки отчетов.  
  
-   [Экспорт в CSV-файл &#40;построитель отчетов и службы SSRS&#41;](exporting-to-a-csv-file-report-builder-and-ssrs.md)  
  
-   [Экспорт в Microsoft Excel &#40;построитель отчетов и службы SSRS&#41;](exporting-to-microsoft-excel-report-builder-and-ssrs.md)  
  
-   [Экспорт в Microsoft Word &#40;построитель отчетов и службы SSRS&#41;](exporting-to-microsoft-word-report-builder-and-ssrs.md)  
  
-   [Подготовка к просмотру в HTML &#40;построитель отчетов и службы SSRS&#41;](rendering-to-html-report-builder-and-ssrs.md)  
  
-   [Экспорт в PDF-файл &#40;построитель отчетов и службы SSRS&#41;](exporting-to-a-pdf-file-report-builder-and-ssrs.md)  
  
-   [Экспорт в файл изображения &#40;построитель отчетов и службы SSRS&#41;](exporting-to-an-image-file-report-builder-and-ssrs.md)  
  
-   [Экспорт в XML &#40;построитель отчетов и службы SSRS&#41;](exporting-to-xml-report-builder-and-ssrs.md)  
  
-   [Формирование потоков данных из отчетов &#40;построитель отчетов и службы SSRS&#41;](generating-data-feeds-from-reports-report-builder-and-ssrs.md)  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] предоставляют дополнительные функции для создания отчетов, корректно отображаемых в других форматах. Разрывы страниц в областях данных табликса (таблицы, матрицы и списка), группах и прямоугольниках дают возможность лучшего управления разбиением отчета на страницы. Страницы отчета, разграниченные разрывами страницы, могут иметь разные имена страниц и позволяют сбрасывать нумерацию страниц. С использованием выражений можно динамически обновлять имена страниц и номера страниц при выполнении отчета. Дополнительные сведения см. в разделе [Разбиение на страницы в службах Reporting Services (построитель отчетов и службы SSRS)](../report-design/pagination-in-reporting-services-report-builder-and-ssrs.md).  
  
 Кроме того, можно воспользоваться встроенным глобальным выражением RenderFormat для условного применения различных макетов отчета для различных модулей подготовки отчетов. Дополнительные сведения см. в разделе [Встроенные глобальные значения и ссылки на пользовательские поля (построитель отчетов и службы SSRS)](../report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md).  
  
##  <a name="OtherWaysExportingReports"></a> Другие методы экспорта отчетов  
 Экспорт отчета является задачей, выполняемой по требованию при открытии отчета в диспетчере или построителе отчетов. Если нужно автоматизировать экспорт отчетов (например, для экспорта отчетов в общую папку в виде файлов определенного типа согласно повторяющемуся расписанию), создайте подписку, доставляющую отчеты в общую папку. Дополнительные сведения см. в разделе [File Share Delivery in Reporting Services](../subscriptions/file-share-delivery-in-reporting-services.md).  
  
 Отчеты, просматриваемые в средствах формирования отчетов или в приложении-браузере, например в диспетчере отчетов, вначале всегда выводятся в формате HTML. Нельзя указать другой модуль подготовки отчетов по умолчанию для просмотра. Однако можно создать подписку, создающую отчет в том формате, в котором он будет впоследствии доставлен в почтовый ящик или общую папку. Дополнительные сведения см. в разделе [создание, изменение и удаление стандартных подписок &#40;служб Reporting Services в собственном режиме&#41; ](../subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md) и [создание, изменение и удаление управляемой данными подписки](../subscriptions/data-driven-subscriptions.md).  
  
 Кроме того, можно открыть отчет по URL-адресу с указанным модулем подготовки отчетов (в качестве параметра URL) и подготовить отчет к просмотру непосредственно в нужном формате, минуя HTML. Следующий пример демонстрирует подготовку отчета к просмотру в формате Excel:  
  
```  
http://<Server Name>/reportserver?/Sales/YearlySalesSummary&rs:Format=Excel&rs:Command=Render  
```  
  
 Дополнительные сведения см. в разделе [Export a Report Using URL Access](../export-a-report-using-url-access.md).  
  
## <a name="see-also"></a>См. также  
 [Управление разрывами страниц, заголовками, столбцами и строками &#40;построитель отчетов и службы SSRS&#41;](../report-design/controlling-page-breaks-headings-columns-and-rows-report-builder-and-ssrs.md)   
 [Поиск, просмотр отчетов и управление ими (построитель отчетов и службы SSRS)](finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [Печать отчетов (построитель отчетов и службы SSRS)](print-reports-report-builder-and-ssrs.md)   
 [Сохранение отчетов &#40;построитель отчетов&#41;](saving-reports-report-builder.md)  
  
  