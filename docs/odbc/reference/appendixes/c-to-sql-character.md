---
title: "C в SQL: символ | Документы Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- character data type [ODBC]
- data conversions from C to SQL types [ODBC], character
- converting data from c to SQL types [ODBC], character
ms.assetid: be66188a-ebdb-4c9e-af72-c379886766fa
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e8d6ab676fc351afd7819c1fe60d59a58bfe7207
ms.contentlocale: ru-ru
ms.lasthandoff: 09/09/2017

---
# <a name="c-to-sql-character"></a>C в SQL: символ
Идентификаторы типа данных ODBC C символ следующие:  
  
 SQL_C_CHAR  
  
 SQL_C_WCHAR  
  
 Следующая таблица показывает ODBC SQL типы данных, к которым может быть преобразован C символьных данных. Объяснение столбцы и условия в таблице см. в разделе [преобразование данных из C в типы данных SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
> [!NOTE]  
>  При преобразовании данных Юникода SQL C символьных данных, длина данных в Юникоде должно быть четным числом.  
  
|Идентификатор типа SQL|Тест|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|Байтовая длина данных < = длина столбца.<br /><br /> Байтовая длина данных > длина столбца.|н/д<br /><br /> 22001|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|Длина данных символьной < = длина столбца.<br /><br /> Длина данных символьной > длина столбца.|н/д<br /><br /> 22001|  
|SQL_DECIMAL<br /><br /> SQL_NUMERIC<br /><br /> SQL_TINYINT<br /><br /> SQL_SMALLINT<br /><br /> SQL_INTEGER SQL_BIGINT|Преобразовать без усечения данных<br /><br /> Преобразование данных с усечение цифр дробной части [e]<br /><br /> Преобразование данных приведет к потере разрядов (в отличие от доли) [e]<br /><br /> Значение данных не *числовой литерал*|н/д<br /><br /> 22001<br /><br /> 22001<br /><br /> 22018|  
|SQL_REAL<br /><br /> SQL_FLOAT<br /><br /> SQL_DOUBLE|Данных входит в диапазон типа данных, в который преобразуется значение<br /><br /> Данных находится вне диапазона типа данных, в который преобразуется значение<br /><br /> Значение данных не *числовой литерал*|н/д<br /><br /> 22003<br /><br /> 22018|  
|SQL_BIT|Данные являются 0 или 1<br /><br /> Данные больше 0, меньше 2 и не равно 1<br /><br /> Данных меньше 0 или больше или равно 2<br /><br /> Данные не *числовой литерал*|н/д<br /><br /> 22001<br /><br /> 22003<br /><br /> 22018|  
|SQL_BINARY<br /><br /> SQL_VARBINARY<br /><br /> SQL_LONGVARBINARY|(Числа байт данных) / 2 < = длина столбца в байтах<br /><br /> (Числа байт данных) / 2 > длина столбца в байтах<br /><br /> Значение данных не шестнадцатеричное значение|н/д<br /><br /> 22001<br /><br /> 22018|  
|SQL_TYPE_DATE|Значение данных допустимо *ODBC-литерал даты*<br /><br /> Значение данных допустимо *ODBC-timestamp-literal*; промежуток времени равен нулю<br /><br /> Значение данных допустимо *ODBC-timestamp-literal*; — времени ненулевое значение, [a]<br /><br /> Значение данных не является допустимым *ODBC-литерал даты* или *ODBC-timestamp-literal*|н/д<br /><br /> н/д<br /><br /> 22008<br /><br /> 22018|  
|SQL_TYPE_TIME|Значение данных допустимо *ODBC-литерал времени*<br /><br /> Значение данных допустимо *ODBC-timestamp-literal*; дробная часть секунд — ноль [b]<br /><br /> Значение данных допустимо *ODBC-timestamp-literal*; дробная часть секунд — ненулевое значение [b]<br /><br /> Значение данных не является допустимым *ODBC-литерал времени* или *ODBC-timestamp-literal*|н/д<br /><br /> н/д<br /><br /> 22008<br /><br /> 22018|  
|SQL_TYPE_TIMESTAMP|Значение данных допустимо *ODBC-timestamp-literal*; дробная часть секунд не усекаются<br /><br /> Значение данных является допустимым *ODBC-timestamp-literal*; дробная часть секунд усечено<br /><br /> Значение данных допустимо *ODBC-литерал даты*[c]<br /><br /> Значение данных допустимо *ODBC-литерал времени*[d]<br /><br /> Значение данных не является допустимым *ODBC-литерал даты*, *ODBC-литерал времени*, или *ODBC-timestamp-literal*|н/д<br /><br /> 22008<br /><br /> н/д<br /><br /> н/д<br /><br /> 22018|  
|Все типы SQL интервал|Значение данных допустимо *значение интервала*; усечение не происходит<br /><br /> Значение данных допустимо *значение интервала*; усечено значение в одном из полей<br /><br /> Значение не является допустимый интервал литерала|н/д<br /><br /> 22015<br /><br /> 22018|  
  
 [] усечен промежуток времени отметка времени.  
  
 [b] часть даты отметка времени учитывается.  
  
 [c часть времени временная метка присваивается нулевое значение.  
  
 [d] часть даты отметка времени задается текущая дата.  
  
 [e] источника драйвера или данных фактически ожидает, пока не получил всю строку (даже если символьные данные отправляются по частям вызовы **SQLPutData**) перед попыткой выполнить преобразование.  
  
 Когда символ C данные преобразуются в числовые, даты, времени или данных timestamp SQL, начальные и завершающие пробелы игнорируются.  
  
 При C символьные данные преобразуются в двоичные данные SQL, каждый два байта символьные данные преобразуются в один байт (8 бит) двоичные данные. Каждый двух байт символьных данных представляет число в шестнадцатеричной форме. Например «01» преобразуется в двоичное 00000001 и «FF» преобразуется в двоичное 11111111.  
  
 Драйвер всегда преобразует пары шестнадцатеричных цифр в отдельных байтов и игнорирует байтов конечное значение null. Из-за этого Если длина символьной строки является нечетным, последний байт строки (за исключением байт конечное значение null, если таковые имеются) не преобразуется.  
  
> [!NOTE]  
>  Разработчики приложений, не рекомендуется из привязки C символьных данных в двоичный тип данных SQL. Обычно это преобразование является неэффективной и медленной.