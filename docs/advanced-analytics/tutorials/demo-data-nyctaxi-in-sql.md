---
title: Загрузите демонстрационные данные о такси Нью-ЙОРКА и сценарии для внедренных R и Python (машинного обучения SQL Server) | Документация Майкрософт
description: Инструкции по скачиванию демонстрационные данные о такси Нью-Йорке и создании базы данных. Данные используются в SQL Server Python и R языка учебников, показывающих, как внедрить скрипт в хранимых процедурах SQL Server и функций T-SQL.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/19/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: f9482a43a37f3c4feee497ae2fd93029143c84f9
ms.sourcegitcommit: 70e47a008b713ea30182aa22b575b5484375b041
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/23/2018
ms.locfileid: "49806714"
---
# <a name="nyc-taxi-demo-data-for-sql-server-python-and-r-tutorials"></a>Демонстрационные данные такси Нью-ЙОРКА для учебники по SQL Server Python и R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

В этой статье объясняется, как установить образец базы данных, состоящий из общедоступных данных из [такси Нью-Йорке и Лимузинов комиссии](http://www.nyc.gov/html/tlc/html/about/trip_record_data.shtml). Эти данные используются в учебниках несколько R и Python для анализа в базе данных в SQL Server. Образец данных — один процент общедоступного набора данных. В системе файл резервной копии базы данных является немного более чем 90 МБ, предоставляя 1,7 млн. строк в первичной таблице данных.

Для этого упражнения вам понадобится [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017) или другое средство, которое можно восстановить файл резервной копии базы данных и выполнять запросы T-SQL.

Учебники и примеры использования, с помощью этого набора данных включают следующее:

+  [Использовать модели Python в SQL Server для обучения и оценки](train-score-using-python-in-tsql.md)

## <a name="download-files"></a>Скачивание файлов

Образец базы данных находится файл резервной копии на серверах корпорации Майкрософт. Загрузка файла начинается немедленно при щелчке ссылки. 

Размер файла составляет около 90 МБ.

1. Нажмите кнопку [NYCTaxi_Sample.bak](https://sqlmldoccontent.blob.core.windows.net/sqlml/NYCTaxi_Sample.bak) для загрузки файла резервной копии базы данных.

2. Скопируйте файл C:\Program files\Microsoft SQL Server\MSSQL экземпляр name\MSSQL\Backup папку.

3. В среде Management Studio щелкните правой кнопкой мыши **баз данных** и выберите **восстановление файлов и файловых групп**.

4. Введите *NYCTaxi_Sample* имя базы данных.

5. Нажмите кнопку **с устройства** и перейдите на страницу выбора файлов выберите файл резервной копии. Нажмите кнопку **добавить** для выбора NYCTaxi_Sample.bak.

6. Выберите **восстановить** флажок и нажмите кнопку **ОК** восстановление базы данных.

## <a name="review-database-objects"></a>Ознакомьтесь с объектами базы данных
   
Подтвердите объекты базы данных существуют в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] экземпляра с помощью [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Вы увидите базы данных, таблиц, функций и хранимых процедур.
  
   ![rsql_devtut_BrowseTables](media/rsql-devtut-browsetables.png "rsql_devtut_BrowseTables")

### <a name="objects-in-nyctaxisample-database"></a>Объекты в базе данных NYCTaxi_Sample

В следующей таблице перечислены объекты, созданные в демонстрационной базы данных о такси Нью-ЙОРКА.

|**Имя объекта**|**Тип объекта**|**Описание**|
|----------|------------------------|---------------|
|**NYCTaxi_Sample** | База данных |Созданный скрипт create-db ТБ Отправка data.sql. Создает базу данных и две таблицы:<br /><br />таблицу dbo.nyctaxi_sample: содержит основной набор данных о такси Нью-ЙОРКА. К таблице добавляется кластеризованный индекс columnstore для оптимизации хранения данных и производительности запросов. В примере 1% набора данных такси Нью-ЙОРКА вставляется в эту таблицу.<br /><br />таблица dbo.nyc_taxi_models: используется для сохранения обученной модели расширенной аналитики.|
|**fnCalculateDistance** |скалярная функция | Создаваемые сценарием fnCalculateDistance.sql. Вычисляет прямое расстояние между местами посадки и высадки. Эта функция используется в [Создание функций данных](sqldev-create-data-features-using-t-sql.md), [обучение и сохранение модели](sqldev-train-and-save-a-model-using-t-sql.md) и [ввод в эксплуатацию моделей R](sqldev-operationalize-the-model.md).|
|**fnEngineerFeatures** |функция с табличным значением | Создаваемые сценарием fnEngineerFeatures.sql. Формирует новые характеристики данных для обучения модели. Эта функция используется в [Создание функций данных](sqldev-create-data-features-using-t-sql.md) и [ввод в эксплуатацию моделей R](sqldev-operationalize-the-model.md).|
|**PlotHistogram** |хранимая процедура | Создаваемые сценарием PlotHistogram.sql. Вызывает функцию R для построения гистограммы на переменную, а затем возвращает диаграмму в виде двоичного объекта. Эта хранимая процедура используется в [анализ и визуализация данных](sqldev-explore-and-visualize-the-data.md).|
|**PlotInOutputFiles** |хранимая процедура| Создаваемые сценарием PlotInOutputFiles.sql. Создает график с помощью функции R и затем сохраняет результат в виде локального файла PDF. Эта хранимая процедура используется в [анализ и визуализация данных](sqldev-explore-and-visualize-the-data.md).|
|**PersistModel** |хранимая процедура | Создаваемые сценарием PersistModel.sql. Принимает модель, сериализованную как тип данных varbinary и записывает ее в указанную таблицу. |
|**PredictTip**  |хранимая процедура |Создаваемые сценарием PredictTip.sql. Вызывает обученную модель для создания прогнозов с помощью модели. Хранимая процедура принимает запрос в качестве входного параметра и возвращает столбец числовых значений, представляющих оценки для входных строк. Эта хранимая процедура используется в [ввод в эксплуатацию моделей R](sqldev-operationalize-the-model.md).|
|**PredictTipSingleMode**  |хранимая процедура| Создаваемые сценарием PredictTipSingleMode.sql. Вызывает обученную модель для создания прогнозов с помощью модели. Эта хранимая процедура принимает новое наблюдение в качестве входных данных, причем отдельные значения характеристик передаются как встроенные параметры, и возвращает значение, представляющее прогнозируемый результат для нового наблюдения. Эта хранимая процедура используется в [ввод в эксплуатацию моделей R](sqldev-operationalize-the-model.md).|
|**TrainTipPredictionModel**  |хранимая процедура|Создаваемые сценарием TrainTipPredictionModel.sql. Обучает модель логистической регрессии, вызывая пакет r. Модель прогнозирует значение для столбца tipped и обучается на основе случайной выборки, содержащей 70 % данных. Выходными данными хранимой процедуры является обученная модель, которая сохраняется в таблице nyc_taxi_models. Эта хранимая процедура используется в [обучение и сохранение модели](sqldev-train-and-save-a-model-using-t-sql.md).|

## <a name="query-the-data"></a>Запрос данных

В качестве шага проверки выполните запрос, чтобы убедиться, что данные были отправлены.

1. В обозревателе объектов в базах данных, щелкните правой кнопкой мыши **NYCTaxi_Sample** базы данных, а затем запустите новый запрос.

2. Выполните некоторые простые запросы:

    ```sql
    SELECT TOP(10) * FROM dbo.nyctaxi_sample;
    SELECT COUNT(*) FROM dbo.nyctaxi_sample;
    ```
База данных содержит 1,7 млн. строк.

## <a name="next-steps"></a>Следующие шаги

Образец данных о такси Нью-ЙОРКА теперь доступна пройти Практическое обучение.

+ [Дополнительные аналитические функции в базе данных с помощью языка R в SQL Server](sqldev-in-database-r-for-sql-developers.md)