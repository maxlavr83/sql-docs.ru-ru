---
title: Шаг 1. Копирование пакета, созданного на занятии 5 | Документы Майкрософт
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: a25fcc13-987e-4f3d-8f0c-76f7e6e59920
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b7d58507dac1d1071f0b546e0610f39381b648de
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2018
ms.locfileid: "52501809"
---
# <a name="lesson-6-1---copying-the-lesson-5-package"></a>Занятие 6–1. Копирование пакета, созданного на занятии 5
В этой задаче будет создана копия пакета Lesson 5.dtsx, созданного на занятии 5. Либо можно добавить пакет для занятия 5, прилагаемый к учебнику по проекту, и скопировать его. Полученная копия впоследствии будет использоваться на протяжении всего занятия 6.  
  
### <a name="to-copy-the-lesson-5-package"></a>Копирование пакета занятия 5  
  
1.  Если SQL Server Data Tools еще не открыты, нажмите кнопку «Пуск», укажите пункт «Все программы», пункт «Microsoft SQL Server 2012», а затем выберите пункт «SQL Server Data Tools».  
  
2.  В меню Файл последовательно выберите команды Открыть, Проект или решение, Учебник по службам SSIS и нажмите кнопку Открыть, а затем дважды щелкните значок SSIS Tutorial.sln.  
  
3.  В обозревателе решений правой кнопкой мыши щелкните Lesson 5.dtsx и выберите команду «Копировать».  
  
4.  В обозревателе решений правой кнопкой мыши щелкните значок Пакеты служб SSIS и выберите команду Вставить.  
  
    По умолчанию копируемому пакету присваивается имя Lesson 6.dtsx.  
  
5.  Чтобы открыть пакет, в обозревателе решений дважды щелкните Lesson 6.dtsx.  
  
6.  Щелкните правой кнопкой мыши фон вкладки Поток управления и выберите Свойства.  
  
7.  В окне «Свойства» измените свойство Name на «Занятие 6».  
  
8.  Установите флажок для свойства ID, щелкните стрелку раскрывающегося списка, а затем в списке выберите <Generate New ID>.  
  
### <a name="to-add-the-completed-lesson-5-package"></a>Добавление готового пакета занятия 5  
  
1.  Откройте SQL Server Data Tools, затем откройте проект «Учебник по службам SSIS».  
  
2.  В обозревателе решений правой кнопкой мыши щелкните значок Пакеты служб SSIS и выберите команду Добавить существующий пакет.  
  
3.  В диалоговом окне «Добавление копии существующего пакета» в разделе «Размещение пакета» выберите пункт «Файловая система».  
  
4.  Нажмите кнопку обзора (…), перейдите в папку пакета Lesson 5.dtsx и нажмите кнопку **Открыть**.  
  
    Чтобы загрузить все пакеты занятий этого учебника, выполните следующие действия.  
  
    1.  Перейдите к [образцам продуктов служб Integration Services](https://go.microsoft.com/fwlink/?LinkId=275027).  
  
    2.  Перейдите на вкладку **DOWNLOADS** .  
  
    3.  Щелкните файл SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip.  
  
5.  Выполните копирование и вставку пакета занятия 5, как описано в шагах 3–8 предыдущей процедуры.  
  
    После копирования пакета занятия 5, если в настоящее время в решении используются пакеты из предыдущих занятий, щелкните правой кнопкой мыши каждый пакет из занятий 1–5, а затем выберите «Исключить из проекта». По завершении в решении должен остаться только файл Lesson 6.dtsx.  
  
## <a name="next-task-in-lesson"></a>Следующая задача занятия  
[Шаг 2. Преобразование проекта в модель развертывания проекта](../integration-services/lesson-6-2-converting-the-project-to-the-project-deployment-model.md)  
  
