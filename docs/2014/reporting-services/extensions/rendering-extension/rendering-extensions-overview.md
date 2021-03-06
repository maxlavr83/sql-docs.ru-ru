---
title: Общие сведения о модулях подготовки отчетов | Документы Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- formats [Reporting Services], rendering extensions
- rendering extensions [Reporting Services], about extensions
ms.assetid: 909356a0-4709-43e5-b597-33bd9bb22882
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 2272cffe68db5c4ad417bfdbf81ed45a8d309a17
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/13/2018
ms.locfileid: "53376916"
---
# <a name="rendering-extensions-overview"></a>Общие сведения о модулях подготовки отчетов
  Модуль подготовки отчетов – это компонент или модуль сервера отчетов, преобразующий данные отчета и сведения о макете в формат, определяемый устройством отображения. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] включает в себя семь модулей подготовки отчетов: HTML, Excel, Word, CSV или текст, XML, изображения и PDF. Можно создать дополнительные модули подготовки для создания отчетов в других форматах.  
  
> [!NOTE]  
>  Чтобы определить доступные модули подготовки отчетов, можно просмотреть список установленных модулей подготовки отчетов в файле RSReportServer.config.  
  
 В следующей таблице описаны модули подготовки отчетов, присутствующие в службах [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
|Extension Name|Описание|  
|--------------------|-----------------|  
|`XML`|Отчет подготавливается в формате XML. Отчет будет открываться в веб-браузере. Применение дополнительных преобразований к данному выходному формату XML может быть эффективнее разработки собственного модуля подготовки отчетов.|  
|`CSV`|Отчет подготавливается в формате с разделителями-запятыми. Отчет открывается в средстве просмотра, связанном с файлами CSV.|  
|`IMAGE`|Отчет подготавливается в формате для печати. В раскрывающемся списке "Экспорт" панели инструментов отчета формат представлен как **TIFF**.|  
|`PDF`|Отчет подготавливается в формате Adobe Acrobat Reader. В раскрывающемся списке "Экспорт" панели инструментов отчета формат представлен как **Файл Acrobat (PDF)**.|  
|`EXCEL`|Отчет подготавливается в формате [!INCLUDE[ofprexcel](../../../includes/ofprexcel-md.md)].|  
|`WORD`|Отчет подготавливается в формате [!INCLUDE[ofprword](../../../includes/ofprword-md.md)].|  
|`HTML 4.0` (часть модуля подготовки отчетов в формате HTML)|Формат HTML применяется для первоначальной подготовки отчета. Если браузер поддерживает стандарт HTML 4.0, то используется этот формат. В противном случае используется стандарт HTML 3.2.|  
|`MHTML` (часть модуля подготовки отчетов в формате HTML)|Отчет подготавливается в формате MHTML. Отчет, сохраненный в этом формате, открывается в Internet Explorer. В раскрывающемся списке "Экспорт" панели инструментов отчета формат представлен как **Веб-архив**.|  
|`NULL`|Отчет не подготавливается в каком-либо формате. Данный модуль подготовки отчетов удобен для помещения отчетов в кэш. Подготовку Null следует использовать совместно с запланированным выполнением или доставкой.|  
  
 Дополнительные сведения о рекомендованных форматах и методах их использования см. в статье [Экспорт отчетов (построитель отчетов и службы SSRS)](../../report-builder/export-reports-report-builder-and-ssrs.md).  
  
 Во всех модулях подготовки отчетов, внедренных [!INCLUDE[msCoName](../../../includes/msconame-md.md)] и поставляемых со службами [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], используется общий набор интерфейсов. Это обеспечивает сравнимые функциональные возможности во всех модулях и снижает сложность кода отображения в ядре сервера отчетов.  
  
## <a name="rendering-object-model"></a>Модель объектов для подготовки отчетов  
 Результатом обработки отчет является находящаяся в открытом доступе модель объектов, называемая «модель объектов для подготовки отчетов» (ROM). Модель объектов для подготовки отчетов — это коллекция классов, определяющих содержимое, макет и данные обработанного отчета. Данная модель доступна разработчикам, которые хотят проектировать, разрабатывать и разворачивать пользовательские модули подготовки отчетов для служб [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. Модель объектов для подготовки отчетов создается, когда сервер отчетов обрабатывает определение XML отчета вместе с определенными пользователем данными отчета. После окончания обработки отчета открытая модель объектов используется модулем подготовки отчетов для определения вывода отчета. Доступные открытые классы данной модели определены в пространстве имен `Microsoft.ReportingServices.OnDemandReportRendering`.  
  
## <a name="writing-custom-rendering-extensions"></a>Создание пользовательского модуля подготовки отчетов  
 Перед созданием пользовательского модуля подготовки отчетов следует оценить более простые альтернативы. Можно выполнить следующие действия:   
  
-   Настроить выводимые данные, указав настройки сведений об устройствах для существующих модулей.  
  
-   Добавить пользовательские функции форматирования и представления, совместно используя преобразования XSL (XSLT) и выходные данные в формате XML.  
  
 Создание пользовательского модуля подготовки отчетов — это сложный процесс. Обычно модуль подготовки отчетов должен поддерживать все возможные сочетания элементов отчета; кроме того, для него необходимо внедрить сотни классов, интерфейсов, методов и свойств. Если пользователю необходимо подготовить отчет в формате, не присутствующем в службах [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], и он решил написать собственную реализацию с использованием управляемого кода, то в коде модуля подготовки отчетов должен быть реализован интерфейс `Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension`, необходимый серверу отчетов.  
  
 Дополнительную документацию и технические документы по службам [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] см. в новейших технических ресурсах на [веб-сайте служб Reporting Services](https://go.microsoft.com/fwlink/?LinkId=19951).  
  
## <a name="see-also"></a>См. также  
 [Реализация модуля подготовки отчетов](implementing-a-rendering-extension.md)   
 [Библиотека модулей Reporting Services](../reporting-services-extension-library.md)  
  
  
