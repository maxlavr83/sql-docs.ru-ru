---
title: Реализация класса DataReader для модуля обработки данных | Документы Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- data processing extensions [Reporting Services], data readers
- data readers [Reporting Services]
- DataReader class
- read-only data
ms.assetid: 23e286e7-6074-4fbe-be29-203420d6c3d0
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 8815a136a80ad6ba3ae838d54e50e7932435b3ac
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/13/2018
ms.locfileid: "53363296"
---
# <a name="implementing-a-datareader-class-for-a-data-processing-extension"></a>Реализация класса DataReader для модуля обработки данных
  Объект **DataReader** позволяет клиенту принимать доступный только для чтения однопроходный поток данных из источника данных. Результаты возвращаются после выполнения запроса и хранятся в сетевом буфере на клиенте до тех пор, пока не будут запрошены с помощью метода **Read** класса **DataReader**. Чтобы создать класс **DataReader**, следует реализовать <xref:Microsoft.ReportingServices.DataProcessing.IDataReader> и, возможно, реализовать <xref:Microsoft.ReportingServices.DataProcessing.IDataReaderExtension>. Объект **DataReader** позволяет увеличить производительность приложения двумя способами: путем получения данных, как только они становятся доступны, вместо ожидания возвращения всех результатов запроса, а также (по умолчанию) путем сохранения в памяти только одной строки за один раз, что снижает нагрузку на системные ресурсы.  
  
 После создания экземпляра класса **Command** создайте объект **DataReader**, вызвав **Command.ExecuteReader** для получения строк из источника данных. Реализация **DataReader** должна предоставлять две основные возможности: однопроходный доступ к результирующим наборам, полученным при выполнении команды, и доступ к типам столбцов, именам и значениям в каждой строке. Клиенты используют метод **Read** объекта **DataReader** для получения строки из результатов запроса.  
  
 В конструкторе отчетов объект **DataReader** используется для получения списка полей, а также сведений о схеме для результирующего набора. Это достигается путем реализации методов **GetName**, **GetValue**, **GetFieldType** и **GetOrdinal** экземпляра <xref:Microsoft.ReportingServices.DataProcessing.IDataReader>.  
  
 Экземпляр <xref:Microsoft.ReportingServices.DataProcessing.IDataReaderExtension> позволяет предоставлять конкретные сведения статистической обработки результирующего набора. Пример реализации класса **DataReader** см. в разделе [Образцы продуктов служб SQL Server Reporting Services](https://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="see-also"></a>См. также  
 [Модули служб Reporting Services](../reporting-services-extensions.md)   
 [Реализация модуля обработки данных](implementing-a-data-processing-extension.md)   
 [Библиотека модулей Reporting Services](../reporting-services-extension-library.md)  
  
  
