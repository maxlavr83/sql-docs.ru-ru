---
title: 'Задача 8: Создание составного правила домена | Документация Майкрософт'
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.topic: conceptual
ms.assetid: cff3b662-7876-4445-9bdd-96be35b3ca0c
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 19b4922446f564435970fbb7f0422a3c98de48df
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/02/2018
ms.locfileid: "48151964"
---
# <a name="task-8-creating-a-composite-domain-rule"></a>Задача 8. Создание составного правила домена
  В этой задаче вы создаете правило для **проверка адреса** составной домен. Определить междоменное правило: Если **Город** — **Лос-Анджелес**, **состояние** должно быть **ЦС** где **Город** и **состояние** — это два домена.  
  
1.  В области справа перейдите **правила CD** вкладки.  
  
2.  Нажмите кнопку **добавить новое правило домена** на панели инструментов.  
  
3.  Тип **City-State Rule** для **имя** и нажмите клавишу **ввод**.  
  
4.  В **построить правило** области выберите **Город** в списке доменов и выберите условие **значение равно** и тип **Лос-Анджелес** для значение.  
  
5.  В **затем** области выберите **состояние** в списке доменов и выберите **значение равно**, тип **ЦС** значение, и нажмите клавишу **ВКЛАДКЕ**.  
  
     ![Правило составного домена](../../2014/tutorials/media/et-creatingacompositedomainrule.jpg "правило составного домена")  
  
6.  Нажмите кнопку **закрыть** кнопки в нижней части страницы, чтобы переключиться на главную страницу клиента DQS. На следующем занятии вы опубликуете базу знаний. Обратите внимание, что база знаний находится в заблокированном состоянии (значок блокировки).  
  
## <a name="next-step"></a>Следующий шаг  
 [Задача 9. Настройка службы ссылочных данных](../../2014/tutorials/task-9-configuring-a-reference-data-service.md)  
  
  
