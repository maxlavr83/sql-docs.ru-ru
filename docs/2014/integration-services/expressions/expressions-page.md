---
title: Страница "Выражения" | Документы Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.expressionspage.f1
helpviewer_keywords:
- Expressions Page dialog box
ms.assetid: c9016ec6-11c1-4ebd-b2a7-0fa6631fd9e4
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 01cabd46c51ed09af8d5de3a173e218dedbd5ac1
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/03/2018
ms.locfileid: "52773246"
---
# <a name="expressions-page"></a>Страница «Выражения»
  На странице **Выражения** можно изменить выражения свойств и открыть диалоговые окна **Редактор выражений свойств** и **Построитель выражений для свойств** .  
  
 Выражения свойств обновляют значения свойств при выполнении пакета. Выражения свойств можно использовать вместе со свойствами пакетов, задач, контейнеров, диспетчеров соединений, а также с некоторыми компонентами потока данных. Выражения оцениваются, и их результаты используются вместо значений свойств, которые устанавливаются при конфигурации пакета и объектов пакета. Выражения могут включать переменные, а также функции и операторы, предоставляемые языком выражений. К примеру, можно создать строку темы сообщения для задачи «Отправка почты» путем объединения значения переменной, в которой содержится строка «Прогноз погоды на », и возвращаемых результатов функции GETDATE(), чтобы получить строку вида «Прогноз погоды на 4/5/2006».  
  
 Дополнительные сведения о написании выражений и использовании выражений свойств см. в разделах [Выражения служб Integration Services (SSIS)](integration-services-ssis-expressions.md) и [Использование выражений свойств в пакетах](use-property-expressions-in-packages.md).  
  
## <a name="options"></a>Параметры  
 **Выражения (...)**  
 Нажмите кнопку с многоточием, чтобы открыть диалоговое окно **Редактор выражений свойств** . Дополнительные сведения см. в статье [Property Expressions Editor](property-expressions-editor.md).  
  
 **\<имя_свойства>**  
 Нажмите кнопку с многоточием, чтобы открыть диалоговое окно **Построитель выражений** . Дополнительные сведения см. в статье [Expression Builder](expression-builder.md).  
  
## <a name="see-also"></a>См. также:  
 [Переменные в службах Integration Services (SSIS)](../integration-services-ssis-variables.md)   
 [Системные переменные](../system-variables.md)   
 [Выражения служб Integration Services (SSIS)](integration-services-ssis-expressions.md)  
  
  
