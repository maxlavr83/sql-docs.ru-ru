---
title: Образец входного XML-файла со встроенной рабочей нагрузкой (DTA) | Документы Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- sample applications [DTA]
ms.assetid: 7c04fe1d-6669-44a1-8b73-36d469e9b002
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b1b53076a7528d0e9eaff1244c206dee4127150e
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/03/2018
ms.locfileid: "52769536"
---
# <a name="xml-input-file-sample-with-inline-workload-dta"></a>Образец входного XML-файла с описанием встроенной рабочей нагрузки (DTA)
  Скопируйте и вставьте этот входной XML-файл, задающий рабочую нагрузку элементом **EventString** , в свой привычный редактор XML или текстовый редактор. Элемент **EventString** можно использовать для указания во входном файле XML рабочей нагрузки из скрипта [!INCLUDE[tsql](../../includes/tsql-md.md)] вместо использования отдельного файла рабочей нагрузки. Скопировав данный образец, замените значения, указанные для элементов **Server**, **Database**, **Schema**, **Table**, **Workload**, **EventString**и **TuningOptions** , значениями, характерными для вашего сеанса настройки. Дополнительные сведения обо всех атрибутах и дочерних элементов, которые можно использовать с этими элементами, см. в разделе [Справочник по входным файлам XML &#40;помощник по настройке ядра СУБД&#41;](xml-input-file-reference-database-engine-tuning-advisor.md). В следующем образце используется только подмножество доступных атрибутов и параметров дочерних элементов.  
  
## <a name="code"></a>Код  
 [!code-xml[InputFileSamples#InlineWorkloadInputFile](../../snippets/xml/SQL14/dta_xml/inputfilesamples/xml/dta_xml_input_file_samples.xml#inlineworkloadinputfile)]  
  
## <a name="comments"></a>Комментарии  
 `USE database_name` EventString **EventString** .  
  
## <a name="see-also"></a>См. также  
 [Запуск и использование помощника по настройке ядра СУБД](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)   
 [Просмотр и работа с выходными данными помощника по настройке ядра СУБД](../../relational-databases/performance/view-and-work-with-the-output-from-the-database-engine-tuning-advisor.md)   
 [Справочник по входным XML-файлам (помощник по настройке ядра СУБД)](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
