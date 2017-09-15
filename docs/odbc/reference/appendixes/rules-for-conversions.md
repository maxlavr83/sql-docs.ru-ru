---
title: "Правила для преобразования | Документы Microsoft"
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
- numeric data type [ODBC], literals
- conversions with numeric literals [ODBC]
- numeric literals [ODBC]
- literals [ODBC], numeric
ms.assetid: 89f846a3-001d-496a-9843-ac9c38dc1762
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 06baaaff03f75cbf04da86527a25ea60755a473e
ms.contentlocale: ru-ru
ms.lasthandoff: 09/09/2017

---
# <a name="rules-for-conversions"></a>Правила для преобразования
Правила в этом разделе, применяются для преобразования, включающие числовые литералы. Для выполнения этих правил определяются следующие термины:  
  
-   *Сохранить назначение:* при отправке данных в столбец таблицы в базе данных. Это происходит во время вызовов **SQLExecute**, **SQLExecDirect**, и **SQLSetPos**. При назначении магазина «target» ссылается на столбец базы данных и «источник» ссылается на данные в буферах приложения.  
  
-   *Получение назначения:* при извлечении данных из базы данных в буферы приложения. Это происходит во время вызовов **SQLFetch**, **SQLGetData**, **SQLFetchScroll**, и **SQLSetPos**. При назначении извлечения «target» ссылается на буферы приложения и «источник» относится к столбцу базы данных.  
  
-   *CS:* значение источника символа.  
  
-   *NT:* значение в числовых целевой объект.  
  
-   *NS:* в источнике числовое значение.  
  
-   *CT:* значение в целевом символ.  
  
-   Точность точный числовой литерал: количество цифр, которые он содержит.  
  
-   Масштаб точный числовой литерал: количество цифр справа от явных или подразумеваемых периода.  
  
-   Точность приблизительных числовых литерала: точность его мантиссы.  
  
## <a name="character-source-to-numeric-target"></a>Исходный символ числовых целевой объект  
 Ниже приведены правила преобразования из источника символ (CS) к целевому объекту числовые (NT).  
  
1.  Замените значение, полученное путем удаления все начальные и конечные пробелы в CS CS. Если не является допустимым CS *числовой литерал*, возвращается SQLSTATE 22018 (Недопустимое символьное значение для спецификации приведения).  
  
2.  Замените значение, полученное путем удаления нулей в начале перед десятичной запятой, замыкающие нули после десятичной запятой, или оба CS.  
  
3.  Преобразуйте CS NT. Если преобразование приводит к потере значащих разрядов, возвращается SQLSTATE 22003 (численное значение вне допустимого диапазона). Если преобразование приводит к потере Незначимые цифры с кодом SQLSTATE 01S07 возвращается (частичное усечение).  
  
## <a name="numeric-source-to-character-target"></a>Числовые источника к целевому объекту символ  
 Ниже приведены правила преобразования из числовых источника (NS) к целевому объекту символ (CT).  
  
1.  Разрешить LT иметь длину в символах компьютерной телефонии Для назначения извлечения LT равна длине буфера в символах минус число байтов в кодировке конечное значение null для этого набора символов.  
  
2.  Случаи:  
  
    -   Если NS точный числовой тип, подождите, пока YP равно кратчайший символьная строка, соответствует определению *точного цифровой literal* таким образом, что масштаб YP совпадает со значением масштаба NS и интерпретируемые значение YP абсолютное значение NS.  
  
    -   Если NS приблизительный числовой тип, подождите, пока YP быть символьной строкой, как показано ниже:  
  
         Вариант.  
  
         Если NS равен 0, YP — 0.  
  
         Разрешить YSN быть кратчайший символьная строка, соответствует определению точное-*числовой литерал* и интерпретируемые, значение которого является абсолютное значение NS. Если длина YSN меньше, чем (*точности* + 1) типа данных NS позвольте YP равно YSN.  
  
         В противном случае YP является кратчайший символьная строка, соответствует определению *приблизительное цифровой literal* интерпретируемых, значение которого является абсолютное значение NS, для которых *мантиссы* состоит из один *цифра* то есть не "0", за которым следует *период* и *unsigned integer*.  
  
3.  Вариант.  
  
    -   Если NS меньше 0, подождите, пока Y быть результатом:  
  
         "-" &#124; &#124; YP  
  
         где "&#124; &#124;" является оператор объединения строк.  
  
         В противном случае позволяют равно YP Y.  
  
4.  Разрешить чтение иметь длину в символах Y.  
  
5.  Вариант.  
  
    -   Если Прошлых равно LT, CT равно Y.  
  
    -   Если Прошлых меньше LT, затем CT присвоено значение Y расширенных справа, соответствующее число пробелов.  
  
         В противном случае (Прошлых > LT), скопируйте первых символов LT Y в компьютерной телефонии  
  
         Вариант.  
  
         Если это назначение хранилища, возвращается ошибка SQLSTATE 22001 (строковые данные, усечение справа).  
  
         Если это назначение извлечения, возвращается предупреждение SQLSTATE 01004 (строковые данные, усечение справа). После копирования приводит к потере цифр дробной части (кроме нули в конце), это определяемые драйвером ли одно из следующих событий:  
  
         (1) драйвер производит усечение строки по оси Y для подходящего масштаба, (который также может быть равен нулю) и записывает результат в компьютерной телефонии  
  
         (2) драйвер округляет строка по оси Y для подходящего масштаба, (который также может быть равен нулю) и записывает результат в компьютерной телефонии  
  
         (3) драйвер ни усекает ни округляет, но только копирует первые символы LT Y в компьютерной телефонии