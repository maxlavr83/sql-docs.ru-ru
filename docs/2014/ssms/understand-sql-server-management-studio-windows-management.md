---
title: Общие сведения об управлении окнами среды SQL Server Management Studio | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- autohide [SQL Server Management Studio]
- SQL Server Management Studio [SQL Server], tool windows
- push pin [SQL Server Management Studio]
- tool windows [SQL Server Management Studio]
ms.assetid: bebf8383-dcaf-466e-84f5-63b81c9cfe52
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 076db2370f027b0d7dffeccb294899b48a065c40
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/03/2018
ms.locfileid: "52817126"
---
# <a name="understand-sql-server-management-studio-windows-management"></a>Общие сведения об управлении окнами среды SQL Server Management Studio
  Окна инструментов в [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] — это высокофункциональная, гибкая и эффективная система, позволяющая:  
  
-   увеличивать рабочее пространство пользователя для задач разработки и управления;  
  
-   уменьшать количество одновременно отображаемых неиспользуемых окон;  
  
-   свободно настраивать пользовательскую среду.  
  
 Управление окнами является важной частью функционирования среды [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] . Пользователи получают быстрый доступ к часто используемым окнам и средствам. Они могут контролировать объем предоставляемого для различных данных пространства, а среда должна соответственно увеличить пространство для редактирования запросов. Окна можно перемещать в различные места экрана. Многие окна можно открепить и вытащить из рабочей области среды [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] . Это особенно удобно при использовании более одного монитора.  
  
 Для увеличения пространства редактирования с сохранением функциональности все окна снабжены функцией автоматического скрытия, которая позволяет свернуть окно в виде вкладки на панели, находящейся на границе основной среды [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] . При наведении указателя на одну из вкладок на экране появится соответствующее окно. Функцию автоматического скрытия можно включить или выключить, нажав кнопку **Автоматически скрывать** в форме канцелярской кнопки в правом верхнем углу окна. Также имеется пункт **Автоматически скрывать все** в меню **Окна** .  
  
 Некоторые компоненты можно настраивать как в режиме вкладок, в котором компоненты представлены в виде вкладок в одном фиксированном месте, так и в режиме многодокументного интерфейса (MDI), когда для каждого документа открывается отдельное окно. Чтобы настроить эту функцию, в меню **Сервис** выберите **Параметры**, **Среда**, а затем **Общие**.  
  
> [!IMPORTANT]  
>  Если имя входа (или пользователь автономной базы данных) используется для подключения и выполняется проверка подлинности, при подключении данные идентификаторов имени входа сохраняются. Для имени входа, использующегося при проверке подлинности Windows, сюда относятся данные о членстве в группах Windows. Идентификатор имени входа остается зарегистрированным на протяжении периода, в который поддерживается соединение. Для принудительного изменения идентификатора, например сброса пароля или изменения членства в группе Windows, имя входа необходимо использовать для выхода из центра проверки подлинности (Windows или [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]), а затем повторно выполнить вход. Член предопределенной роли сервера **sysadmin** или любого имени входа с разрешением **ALTER ANY CONNECTION** может использовать команду **KILL** и принудительно разорвать подключение для выполнения повторного подключения с использованием имени входа. [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] может повторно использовать сведения о соединении при открытии нескольких соединений в окнах обозревателя объектов и редактора запросов. Закройте все соединения для принудительного повторного подключения.  
  
> [!IMPORTANT]  
>  Если имя входа (или пользователь автономной базы данных) используется для подключения и выполняется проверка подлинности, данные идентификаторов имени входа при подключении помещаются в кэш. Для имени входа, использующегося при проверке подлинности Windows, сюда относятся данные о членстве в группах Windows. Идентификатор имени входа остается зарегистрированным на протяжении периода, в который поддерживается соединение. Для принудительного изменения идентификатора, например сброса пароля или изменения членства в группе Windows, имя входа необходимо использовать для выхода из центра проверки подлинности (Windows или [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]), а затем повторно выполнить вход. Член предопределенной роли сервера **sysadmin** или любого имени входа с разрешением **ALTER ANY CONNECTION** может использовать команду **KILL** и принудительно разорвать подключение для выполнения повторного подключения с использованием имени входа. [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] может повторно использовать сведения о соединении при открытии нескольких соединений в окнах обозревателя объектов и редактора запросов. Закройте все соединения для принудительного повторного подключения.  
  
## <a name="see-also"></a>См. также  
 [Использование среды SQL Server Management Studio](../database-engine/use-sql-server-management-studio.md)   
 [Среда SQL Server Management Studio](the-sql-server-management-studio-environment.md)  
  
  
