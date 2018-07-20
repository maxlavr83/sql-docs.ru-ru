---
title: Источник данных свойства учетных данных (построитель отчетов) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- "10017"
ms.assetid: 4531f09f-d653-4c05-a120-d7788838bc99
caps.latest.revision: 11
author: maggiesmsft
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c0b6689c1a75cfc9354f8c47532d0ed773f3c6e5
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2018
ms.locfileid: "37238594"
---
# <a name="data-source-properties-dialog-box-credentials-report-builder"></a>Диалоговое окно «Свойства источника данных» — «Учетные данные» (построитель отчетов)
  Вкладка **Учетные данные** в диалоговом окне **Свойства источника данных** позволяет просмотреть и изменить учетные данные, используемые для подключения к источнику данных, внедренному в отчет. Указанные учетные данные используются для доступа к источнику данных во время просмотра отчетов. Дополнительные сведения об учетных данных см. в разделе [Указание учетных данных в построителе отчетов](../../2014/reporting-services/specify-credentials-in-report-builder.md).  
  
## <a name="options"></a>Параметры  
 **Использовать проверку подлинности Windows (встроенная безопасность)**  
 Выберите этот параметр, чтобы использовать проверку подлинности Windows.  
  
 **Использовать имя пользователя и пароль**  
 Выберите этот параметр, чтобы использовать определенное имя пользователя и пароль. Для встроенных источников данных: при публикации проекта сервера отчетов на целевом сервере имя пользователя и пароль сохраняются как хранимые учетные данные для базы данных. Если необходимо использовать имя пользователя и пароль как учетные данные Windows, можно изменить свойства опубликованного общего источника данных на целевом сервере. Дополнительные сведения см. в разделе [Создание, удаление или изменение общего источника данных (диспетчер отчетов)](../../2014/reporting-services/create-delete-or-modify-a-shared-data-source-report-manager.md) документации к [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] в [электронной документации](http://go.microsoft.com/fwlink/?linkid=121312) по [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 **Имя пользователя**  
 Введите имя пользователя для получения доступа к источнику данных.  
  
 **Пароль**  
 Введите пароль для получения доступа к источнику данных.  
  
 **Запрос учетных данных**  
 Выберите этот параметр, чтобы учетные данные запрашивались при запуске отчета.  
  
 **Введите строку приглашения**  
 Введите предложение пользователю ввести учетные данные входа для источника данных.  
  
 **Без учетных данных**  
 Выберите этот параметр, чтобы учетные данные не запрашивались при доступе к источнику данных. Этот параметр работает, только если источник данных не принимает учетные данные или если учетные данные передаются каким-то другим способом.  
  
 Для некоторых модулей обработки данных необходимо настроить на сервере отчетов учетную запись автоматического выполнения.  
  
 Дополнительные сведения см. в разделе по соответствующему типу источника данных: [Добавление данных из внешних источников данных (службы SSRS)](report-data/add-data-from-external-data-sources-ssrs.md) и [Настройка учетной записи автоматического выполнения (диспетчер конфигурации служб SSRS)](install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md) в документации к [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] в [электронной документации](http://go.microsoft.com/fwlink/?linkid=121312) по [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>См. также  
 [Справка построителя отчетов для диалоговых окон, панелей и мастеров](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [Диалоговое окно "Свойства источника данных" — "Общие" (построитель отчетов)](../../2014/reporting-services/data-source-properties-dialog-box-general-report-builder.md)   
 [Добавление и проверка подключения к данным или источнику данных &#40;построитель отчетов и службы SSRS&#41;](report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)   
 [Добавление данных в отчет &#40;построитель отчетов и службы SSRS&#41;](report-data/report-datasets-ssrs.md)  
  
  