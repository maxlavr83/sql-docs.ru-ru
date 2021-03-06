---
title: Управление сервером служб аналитики SQL Server | Документация Майкрософт
ms.date: 11/15/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 41c689b2dfb122b94204cfbb8d52f9f8e9a1a8fb
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2018
ms.locfileid: "51700442"
---
# <a name="sql-server-analysis-services-server-management"></a>Управление сервером SQL Server Analysis Services
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]

Службы Azure Analysis Services, см. в разделе [управление Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-manage).

  Экземпляр сервера служб Analysis Services — это копия **msmdsrv.exe** исполняемый файл, который запускается как служба операционной системы. Каждый экземпляр полностью независим от других экземпляров на том же сервере и обладает собственной конфигурацией, разрешениями, портами, стартовыми учетными записями, областью хранения файлов и свойствами режима сервера.  
  
 Каждый экземпляр выполняется как служба Windows, Msmdsrv.exe, в контексте безопасности определенной учетной записи входа.  
  
-   Имя службы экземпляра по умолчанию является MSSQLServerOLAPService.  
  
-   Имя службы каждого именованного экземпляра — MSOLAP$ InstanceName.  
  
> [!NOTE]  
>  Если установлено несколько экземпляров, программа установки также устанавливает службу перенаправления, встроенную в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] службы браузера. Служба перенаправления отвечает за направление клиентов на соответствующий именованный экземпляр служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Служба браузера [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] всегда запускается в контексте безопасности учетной записи локальной службы — учетной записи пользователя с ограниченными правами, которая используется Windows для системных служб, не получающих доступ к ресурсам за пределами локального компьютера.  
  
 Можно создать конфигурацию с масштабным развертыванием из нескольких экземпляров сервера отчетов, установленных на одном компьютере. В частности, для служб Analysis Services это означает, что можно организовать поддержку различных режимов сервера за счет запуска нескольких экземпляров на одном и том же сервере, каждый из которых может быть настроен на работу в определенном режиме.  
  
 Режим сервера — это свойство, которое определяет архитектуру организации хранилища и использования памяти для конкретного экземпляра. Сервер, работающий в многомерном режиме, использует слой управления ресурсами, созданный для баз данных многомерных кубов и моделей интеллектуального анализа данных. В отличие от этого, в табличном режиме сервера используется подсистема аналитики в памяти VertiPaq и сжатие данных для статистической обработки данных при выполнении запросов.  
  
 Различия в архитектуре хранения и использования памяти означают, что на одном экземпляре служб Analysis Services будут запускаться либо табличные базы данных, либо многомерные базы данных, но не оба типа одновременно. Свойство «Режим сервера» определяет тип базы данных, запущенной в этом экземпляре.  
  
 Режим сервера включается во время установки, если указать тип базы данных, которая будет выполняться на сервере. Чтобы обеспечить поддержку всех доступных режимов, можно установить несколько экземпляров служб Analysis Services на одном и том же сервере, каждый из которых будет настроен на работу в режиме, соответствующем строящимся проектам.  
  
 Как правило, большинство необходимых административных задач можно выполнить в одном режиме. Системный администратор служб Analysis Services может с помощью одних тех же процедур и скриптов управлять любым экземпляром Analysis Services в сети, вне зависимости от типа установки.  
  
> [!NOTE]  
>  Единственным исключением является [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] для SharePoint. Администрирование развернутой на сервере системы [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] всегда осуществляется в контексте фермы SharePoint. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] отличается от других режимов сервера тем, что всегда существует лишь один экземпляр, который управляется либо из центра администрирования SharePoint, либо с помощью средства настройки [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Подключение [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] для SharePoint к среде SQL Server Management Studio или к среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]возможно, но нежелательно. Ферма SharePoint включает инфраструктуру, выполняющую синхронизацию состояния сервера и отслеживающую доступность сервера. Использование других средств может повлиять на эти операции. Дополнительные сведения о [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] администрирования сервера, см. в разделе [Power Pivot для SharePoint ](../../analysis-services/power-pivot-sharepoint/power-pivot-for-sharepoint-ssas.md).  
  
## <a name="common-server-management-topics"></a>Основные темы вопросов управления сервера  
  
|Ссылка|Описание задачи|  
|----------|----------------------|  
|[Настройка после установки](../../analysis-services/instances/post-install-configuration-analysis-services.md)|Описываются обязательные и необязательные задачи, которые завершают или изменяют установку служб Analysis.|  
|[Подключение к службам Analysis Services](../../analysis-services/instances/connect-to-analysis-services.md)|Описывает свойства строки подключения, клиентские библиотеки, методики проверки подлинности и действия по установке или завершению соединений.|  
|[Наблюдение за экземпляром служб Analysis Services](../../analysis-services/instances/monitor-an-analysis-services-instance.md)|Описываются средства и способы наблюдения за экземпляром сервера, в том числе сведения об использовании средства отслеживания производительности и приложения SQL Server Profiler.|  
|[Высокий уровень доступности и масштабируемость](../../analysis-services/instances/high-availability-and-scalability-in-analysis-services.md)|В этой статье описаны наиболее часто используемые методы для создания высокодоступных масштабируемых баз данных для служб Analysis Services. |  
|[Сценарии глобализации для служб Analysis Services](../../analysis-services/globalization-scenarios-for-analysis-services.md)|Описывает поддерживаемые языки и параметры сортировки, действия по изменению обоих свойств и рекомендации по настройке и тестированию поведений языка и параметров сортировки.|  
|[Журнал операций в службах Analysis Services](../../analysis-services/instances/log-operations-in-analysis-services.md)|Описывает журналы и способы их настройки.|  
  
  
## <a name="see-also"></a>См. также  
 [Сравнение табличных и многомерных решений ](../../analysis-services/comparing-tabular-and-multidimensional-solutions-ssas.md)   
 [Определение режима работы сервера экземпляра служб Analysis Services](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
