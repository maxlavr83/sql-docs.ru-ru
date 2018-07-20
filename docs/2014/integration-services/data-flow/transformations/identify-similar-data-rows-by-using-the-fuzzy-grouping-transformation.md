---
title: Определение подобных строк данных с помощью преобразования "Нечеткое группирование" | Документы Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Fuzzy Grouping transformation
- match similar data [Integration Services]
- similar data rows [Integration Services]
- fuzzy matches
ms.assetid: ffcb41a6-e23d-49ea-8c32-ac980e3dc495
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 948a55588aa943ba05fc3ac536f6ca04213a2e99
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2018
ms.locfileid: "37233754"
---
# <a name="identify-similar-data-rows-by-using-the-fuzzy-grouping-transformation"></a>Определение подобных строк данных с помощью преобразования «Нечеткое группирование»
  Перед добавлением и настройкой преобразования «Нечеткое группирование» в пакете уже должен содержаться хотя бы один источник и задача потока данных.  
  
### <a name="to-implement-fuzzy-grouping-transformation-in-a-data-flow"></a>Включение преобразования «Нечеткое группирование» в поток данных  
  
1.  В среде [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]откройте проект служб [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] , содержащий необходимый пакет.  
  
2.  Чтобы открыть пакет, дважды щелкните его в обозревателе решений.  
  
3.  Перейдите на вкладку **Поток данных** , а затем из **области элементов**перетащите преобразование «Нечеткое группирование» в область конструктора.  
  
4.  Подключите преобразование «Нечеткое группирование» к потоку данных, перетащив соединитель из источника данных или предыдущего преобразования в преобразование «Нечеткое группирование».  
  
5.  Дважды щелкните преобразование «Нечеткое группирование».  
  
6.  В диалоговом окне **Редактор преобразования «Нечеткое группирование»** на вкладке **Диспетчер соединений** выберите диспетчер соединений OLE DB, подключающийся к базе данных [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
    > [!NOTE]  
    >  Соединение с базой данных [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] требуется преобразованию для создания временных таблиц и индексов.  
  
7.  Щелкните вкладку **Столбцы** и в списке **Доступные входные столбцы** установите флажок для входных столбцов, в которых будет производиться поиск похожих строк в наборе данных.  
  
8.  Установите флажок в столбце **Передать** для передачи входных столбцов на выход преобразования. Передаваемые столбцы не включаются в процесс выявления повторяющихся строк.  
  
    > [!NOTE]  
    >  Входные столбцы, используемые для группирования, автоматически помечаются как передаваемые, и эти флажки не могут быть сняты.  
  
9. Существует дополнительная возможность обновления имен выходных столбцов в столбце **Псевдоним выхода** .  
  
10. Можно также обновить имена очищенных столбцов в столбце **Псевдоним группы вывода** .  
  
    > [!NOTE]  
    >  По умолчанию столбцам присваиваются имена входных столбцов с суффиксом «_clean».  
  
11. Можно изменить используемый тип соответствия в столбце **Тип совпадения** .  
  
    > [!NOTE]  
    >  Хотя бы один из столбцов должен использовать нечеткое соответствие.  
  
12. Укажите в столбце **Минимальное подобие** уровень минимального подобия столбцов. Оно должно находиться в диапазоне от 0 до 1. Чем больше значение, тем более похожими должны быть значения входных столбцов для объединения в группы. Значение минимального подобия, равное 1, указывает на четкое соответствие.  
  
13. Можно также изменить имена столбцов подобия в столбце **Псевдоним выхода подобия** .  
  
14. Для указания обработки чисел в значениях данных измените значения в столбце **Числовые значения** .  
  
15. Чтобы указать, каким образом преобразование сравнивает символьные данные в столбце, измените установленные по умолчанию параметры сравнения в столбце **Флаги сравнения** .  
  
16. Щелкните вкладку **Дополнительно** , чтобы изменить имена столбцов, которые преобразование добавляет к выходу для уникального идентификатора строки (_key_in), идентификатора повторяющейся строки (_key_out) и значения подобия (_score).  
  
17. При желании можно отрегулировать порог подобия при помощи ползунка.  
  
18. Можно также сбросить флажки разделителей токенов, чтобы игнорировать разделители в данных.  
  
19. Нажмите кнопку **ОК**.  
  
20. Чтобы сохранить обновленный пакет, выберите пункт **Сохранить выбранные элементы** в меню **Файл** .  
  
## <a name="see-also"></a>См. также  
 [Преобразование «Нечеткое группирование»](fuzzy-grouping-transformation.md)   
 [Преобразования служб Integration Services](integration-services-transformations.md)   
 [Пути служб Integration Services](../integration-services-paths.md)   
 [Задача потока данных] ((.. /.. /Control-Flow/Data-Flow-Task.MD)  
  
  