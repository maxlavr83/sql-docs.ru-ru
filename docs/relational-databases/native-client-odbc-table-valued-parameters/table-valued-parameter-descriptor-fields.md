---
title: "Поля дескрипторов возвращающего табличное значение параметра | Документы Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-table-valued-parameters
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: table-valued parameters (ODBC), descriptor fields
ms.assetid: 4e009eff-c156-4d63-abcf-082ddd304de2
caps.latest.revision: "31"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 60db5e1eed36ab731c982d7171ca186b3012aacc
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/08/2018
---
# <a name="table-valued-parameter-descriptor-fields"></a>Поля дескрипторов возвращающего табличное значение параметра
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Поддержка возвращающих табличное значение параметров включает новые поля в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-дескрипторах параметра ODBC-приложения и дескрипторах параметра реализации.  
  
## <a name="remarks"></a>Remarks  
  
|Имя|Местоположение|Тип|Description|  
|----------|--------------|----------|-----------------|  
|SQL_CA_SS_TYPE_NAME|IPD|SQLTCHAR*|Имя серверного типа возвращающего табличное значение параметра.<br /><br /> Если указано имя типа возвращающего табличное значение параметра во время вызова SQLBindParameter, его необходимо всегда указывается как значение Юникода, даже в тех приложениях, построенных с кодировкой ANSI. Значение, используемое для параметра *StrLen_or_IndPtr* должен быть SQL_NTS или длина строки имени, умноженную на sizeof(WCHAR).<br /><br /> Если имя типа возвращающего табличное значение параметра указываются с помощью SQLSetDescField, он может быть указан с помощью литерал, который соответствует способу приложения встроен. Диспетчер драйвера ODBC выполнит все необходимые преобразования данных в Юникод.|  
|SQL_CA_SS_TYPE_CATALOG_NAME (только для чтения)|IPD|SQLTCHAR*|Каталог, в котором определен тип.|  
|SQL_CA_SS_TYPE_SCHEMA_NAME|IPD|SQLTCHAR*|Схема, в которой определен тип.|  
  
 Приложения не должны устанавливать SQL_CA_SS_TYPE_CATALOG_NAME для возвращающих табличное значение параметров. Иначе будет возвращена ошибка SQL_ERROR и зарегистрирована диагностическая запись с SQLSTATE = HY091 и сообщением «Недопустимый идентификатор поля дескриптора».  
  
 Если фокус параметра установлен на возвращающий табличное значение параметр, то к возвращающим табличное значение параметрам применяются следующие атрибуты инструкций и поля заголовка дескриптора:  
  
|Имя|Местоположение|Тип|Description|  
|----------|--------------|----------|-----------------|  
|SQL_ATTR_PARAMSET_SIZE<br /><br /> (эквивалентен SQL_DESC_ARRAY_SIZE в дескрипторе параметра приложения)|APD|SQLUINTEGER|Размер массива для массивов буфера для возвращающего табличное значение параметра. Это максимальное количество строк, которое может быть размещено в буферах, или размер буферов в строках. Возвращающий табличное значение параметр может иметь больше или меньше строк, чем помещается в буфер. По умолчанию — 1.<br /><br /> Примечание: Если SQL_SOPT_SS_PARAM_FOCUS установлено в значение по умолчанию 0, SQL_ATTR_PARAMSET_SIZE ссылается на инструкцию и указывает число наборов параметров. Если для SQL_SOPT_SS_PARAM_FOCUS задан порядковый номер возвращающего табличное значение параметра, то он ссылается на возвращающий табличное значение параметр и указывает число строк для набора параметров для возвращающего табличное значение параметра.|  
|SQL_ATTR_PARAM _BIND_TYPE|APD|SQLINTEGER|По умолчанию имеет значение SQL_PARAM_BIND_BY_COLUMN.<br /><br /> Чтобы выбрать привязку на уровне строки, это поле имеет значение длины структуры или экземпляра буфера, который будет привязан к набору строк возвращающего табличное значение параметра. Эта длина должна включать пробел для всех связанных столбцов и все заполнения структуры или буфера. Это гарантирует, что если адрес связанного столбца увеличивается на указанную длину, результат будет указывать на начало того же столбца в следующей строке. При использовании **sizeof** оператор в ANSI C, такое поведение гарантируется.|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR|APD|SQLINTEGER*|Значение по умолчанию — указатель NULL.<br /><br /> Если это поле имеет значение, отличное от NULL, драйвер разыменовывает указатель, добавляет разыменованное значение к каждому из отложенных полей в записи дескриптора (SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR и SQL_DESC_OCTET_LENGTH_PTR), и использует новые значения указателя, чтобы получить значения данных.|  
  
 Эти поля допустимы только для возвращающих табличное значение параметров и не учитываются для всех остальных типов данных.  
  
 Поле SQL_CA_SS_TYPE_NAME не является обязательным для вызовов хранимых процедур. Оно должно быть указано для инструкций SQL, не являющихся вызовами процедур, чтобы разрешить серверу определять тип возвращающего табличное значение параметра.  
  
 Если необходимо имя типа и тип таблицы для возвращающего табличное значение параметра определяется в схеме, отличной от этой хранимой процедуры, то значение SQL_CA_SS_TYPE_SCHEMA_NAME должно быть задано в дескрипторе параметра реализации. Иначе сервер не сможет определить тип возвращающего табличное значение параметра. Это приведет к ошибке при вызове SQLExecute или SQLExecDirect. Ошибка будет иметь статус SQLSTATE= 07006 и сообщение «Нарушение атрибута ограниченного типа данных».  
  
 Столбцы возвращающего табличное значение параметра могут использовать привязки на уровне столбца или строки. По умолчанию используется привязка на уровне столбца. Установив параметр SQL_ATTR_PARAM_BIND_TYPE и SQL_ATTR_ PARAM_BIND_OFFSET_PTR, можно указать привязку на уровне строки. Это аналогично привязке на уровне строки столбцов и параметров.  
  
 Атрибуты SQL_CA_SS_TYPE_CATALOG_NAME и SQL_CA_SS_TYPE_SCHEMA_NAME могут также использоваться для получения каталога и схемы, связанных с параметрами определяемых пользователем типов данных CLR. Это альтернатива для существующих атрибутов схемы каталога, зависящих от типа, для этих типов.  
  
## <a name="see-also"></a>См. также:  
 [Возвращающие табличные значения параметры &#40; ODBC &#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  