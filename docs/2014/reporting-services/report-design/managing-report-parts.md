---
title: Управление элементами отчета | Документы Майкрософт
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 41947b4c-8ecf-4e4f-b30e-66e1d6692b74
caps.latest.revision: 6
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: b8b08d19493528f1c93cea4752f548040fb47322
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2018
ms.locfileid: "37286700"
---
# <a name="managing-report-parts"></a>Управление элементами отчета
  Начиная с версии [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], элементы отчета могут быть публиковаться на серверах отчетов и повторно использоваться в других отчетах и другими пользователями, если они имеют соответствующие разрешения.  
  
 Элементы отчета могут повторно использоваться несколькими пользователями и в нескольких отчетах. Пользователи могут искать элементы отчета на сервере и добавлять их в отчет.  Пользователи могут также получать уведомления об обновлениях для элемента отчета на сервере и заново публиковать новые версии элемента отчета. Права доступа служб отчетов могут влиять на действия по созданию отчетов, а также позволяют управлять ими.  В этом разделе рассматриваются свойства и режимы работы для элементов отчетов после их появления на сервере.  
  
## <a name="managing-report-parts"></a>Управление элементами отчета  
 Чтобы управлять элементами отчета, можно использовать диспетчер отчетов для сервера отчетов, работающего в собственном режиме, или страницы приложения для сервера отчетов, работающего в режиме интеграции с SharePoint.  
  
### <a name="server-side-interaction-and-search"></a>Взаимодействие с серверными компонентами и поиск  
 Элементы отчета могут публиковаться на сервере отчетов, работающем как в собственном режиме, так и в режиме интеграции с SharePoint. Для поиска элементов отчетов и их включения в свои отчеты можно использовать галерею элементов отчетов в таком приложении разработки отчетов, как построитель отчетов [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Когда пользователь ищет элемент отчета, процедура поиска просматривает каталог сервера отчетов независимо от того, для какого режима был установлен сервер.  
  
 Если элементы отчетов публикуются из такого приложения для создания отчетов, как построитель отчетов, на сервере отчетов, работающем в режиме интеграции с SharePoint, также происходит обновление каталога сервера отчетов, а результаты поиска в галерее точно отражают новый или обновленный элемент отчета.  
  
#### <a name="directly-uploading-report-parts-to-a-sharepoint-folder"></a>Непосредственная передача элементов отчетов в папку SharePoint  
 Если элемент отчета загружается напрямую в папку документов SharePoint (а не публикуется из приложения создания отчета), каталог сервера отчетов не обновляется. Поиск в галерее элементов отчетов не позволяет найти такой переданный элемент отчета. Чтобы обеспечить постоянную синхронизацию папок SharePoint и каталога сервера отчетов, можно активировать функцию синхронизации файлов служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] на сервере SharePoint. Дополнительные сведения см. в статье [активировать функции синхронизации файлов сервера отчетов в центре администрирования SharePoint](../activate-report-server-file-sync-feature-sharepoint-central-administration.md).  
  
 Файлы также можно синхронизировать, вызвав некоторые API-интерфейсы управления службами отчетов (например, GetProperties и SetProperties).  
  
### <a name="organizing-and-moving-report-parts"></a>Организация и перемещение элементов отчетов  
 Рекомендуется заранее продумать и запланировать, как рабочая группа будет использовать и организовывать элементы отчетов, общие наборы данных и общие источники данных. Хотя перенести их можно и позже, могут возникнуть проблемы.  
  
#### <a name="native-mode-report-server"></a>Сервер отчетов в собственном режиме  
 Если внутри сервера отчетов, работающего в собственном режиме, элемент отчета перемещается из одной папки в другую, это не мешает приложениям создания отчетов искать или загружать обновления для элементов отчетов. Это объясняется тем, что сервер использует уникальный идентификатор компонента ComponentID. Но если элемент отчета перемещается в папку, на которую у пользователя нет разрешений, этот элемент отчета не будет найден и для этого пользователя уведомления об обновлении элементов отчетов не будут поступать.  
  
#### <a name="report-server-in-sharepoint-integrated-mode"></a>Сервер отчетов в режиме интеграции с SharePoint  
 Перемещение элементов отчета в другую библиотеку документов или папку имеет тот же эффект, что и передача их непосредственно на сервер SharePoint: каталог сервера отчетов синхронизироваться не будет. Чтобы избежать этого, активируйте функцию синхронизации файлов сервера отчетов на сервере SharePoint.  
  
 Исключением являются подпапки. Поиск во вложенных папках выполняется всегда, поэтому, если вручную переместить элемент отчета во вложенную папку, поиск этого элемента отчета из галереи элементов отчетов будет успешным. В ходе поиска из галереи отчетов отчет будет по-прежнему найден.  
  
### <a name="report-server-catalog-properties"></a>Свойства каталога сервера отчетов  
 В следующей таблице показано, как существующие поля каталога сервера отчетов связаны с элементами отчета и с новыми полями, которые добавляются в каталог для элементов отчета. Доступ к ним предоставляется в диспетчере отчетов и библиотеках SharePoint, а также в таких приложениях создания отчетов, как построитель отчетов.  
  
 Звездочка (*) указывает, что свойство является новым для этого выпуска.  
  
|Свойство|Описание|Элемент отчета<br /><br /> Критерии поиска в галерее|  
|--------------|-----------------|---------------------------------------------|  
|Имя|Это один из критериев поиска в галерее элементов отчетов.|Да|  
|Описание|Возможно, придется упорядочить имена элементов отчетов так, чтобы пользователям было легче искать их в галерее. Например, чтобы найти все элементы отчета с данными о продажах и презентациях, можно искать описание, начинающееся со строки «Продажи>>».|Да|  
|CreatedBy|Идентификатор пользователя, который добавил элемент отчета в базу данных сервера отчетов. Точный формат зависит от метода проверки подлинности. Например, если используются некоторые методы проверки подлинности, в полях CreatedBy и ModifiedBy отображаются полные доменные имена или имена пользователей.|Да|  
|CreationDate|Дата первоначального создания элемента отчета.<br /><br /> Это один из критериев поиска в галерее элементов отчетов.|Да|  
|ModifiedBy|Поле ModifiedBy — это идентификатор последнего пользователя, который внес изменения в элемент отчета.|Да|  
|ModifiedDate|Дата последнего изменения элемента отчета на сервере.<br /><br /> Это поле используется в алгоритме для определения того, есть ли обновления на сервере для этого элемента отчета. Дополнительные сведения см. в описании параметра ComponentID далее в этой таблице.|Да|  
|SubType (*)|SubType — это строка, указывающая, какой элемент отчета искать, например «табликс» или «диаграмму».|Да|  
|ComponentID (*)|ComponentID — это уникальный идентификатор элемента отчета. Это новое поле в каталоге видимо как в серверных приложениях, так и в приложениях создания отчетов, например, в построителе отчетов.<br /><br /> Это поле используется клиентскими приложениями для проверки наличия на сервере обновлений к элементу отчета. Клиентское приложение ищет на сервере идентификаторы ComponentID, содержащиеся в текущем клиентском отчете. Если идентификатор ComponentID найден, поле ModifiedDate сравнивается с SyncDate для элемента отчета на клиентской стороне.|Нет|  
  
## <a name="controlling-access-to-report-parts"></a>Управление доступом к элементам отчетов  
 В следующих таблицах указано, какие роли назначаются по умолчанию и как это позволяет выполнять различные операции. Имена назначений ролей зависят от того, какой сервер отчетов используется.  
  
### <a name="server-in-native-mode"></a>Сервер в собственном режиме работы  
  
|Действия|Роли|  
|-------------|-----------|  
|Добавление, удаление, изменение свойств элементов, управление безопасностью и загрузка элементов отчетов|Диспетчер содержимого<br /><br /> Мои отчеты|  
|Добавление, удаление и загрузка элементов отчетов|Издатель|  
|Поиск и повторное использование|Браузер<br /><br /> построитель отчетов|  
  
### <a name="server-in-sharepoint-integrated-mode"></a>Сервер в режиме интеграции с SharePoint  
  
|Действия|Роль|  
|-------------|----------|  
|Добавление, удаление, изменение свойств элементов, управление безопасностью и загрузка элементов отчетов|Полный доступ|  
|Добавление, удаление, изменение свойств элементов и загрузка элементов отчетов|Конструирование<br /><br /> Участие|  
|Поиск и повторное использование|Чтение<br /><br /> Только просмотр|  
  
### <a name="security-considerations"></a>Вопросы безопасности  
  
-   Если определения элементов отчета повторно используются в отчете, они полностью копируются в определение отчета вместе с идентификатором ComponentID. Если элемент отчета обновляется на сервере, пользователи могут пожелать загрузить обновленные элементы отчетов в свои отчеты. Загруженные обновления также представляют собой полные копии элементов отчетов и заменяют версии элементов отчетов, которые находились в отчете раньше.  
  
    > [!IMPORTANT]  
    >  В каждом из этих шагов важно убедиться, что элементы отчетов, повторно используемые в отчетах, поступили из мест и от пользователей, заслуживающих доверия.  
  
-   Для элементов отчетов используются те же политики разрешений, что и для существующего типа элемента «Resource». Если посмотреть на это с точки зрения наследования параметров безопасности, в пределах одной папки нет никакой разницы между традиционными элементами ресурсов и элементами отчетов. Внутри папки элемент отчета наследует ту же политику разрешений, что и изображения. Если требуется их различать, для соответствующих элементов отчетов можно задать параметры безопасности на уровне элементов. Или можно поместить элементы отчетов в разные папки и задать необходимые разрешения.  
  
## <a name="see-also"></a>См. также  
 [Элементы отчета и наборы данных в построителе отчетов](../report-data/report-parts-and-datasets-in-report-builder.md)   
 [Элементы отчета «общие свойства», &#40;диспетчера отчетов&#41;](../general-properties-page-report-parts-report-manager.md)   
 [Перемещение элементов страницы &#40;диспетчера отчетов&#41;](../move-items-page-report-manager.md)   
 [Управление содержимым сервера отчетов &#40;собственный режим служб SSRS&#41;](../report-server/report-server-content-management-ssrs-native-mode.md)   
 [Устранение неполадок в элементах отчета &#40;построитель отчетов и службы SSRS&#41;](../report-parts-report-builder-and-ssrs.md)   
 [Элементы отчетов в конструкторе отчетов (SSRS)](report-parts-in-report-designer-ssrs.md)  
  
  