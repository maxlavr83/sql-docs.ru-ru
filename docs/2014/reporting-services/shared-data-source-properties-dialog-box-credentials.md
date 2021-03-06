---
title: Диалоговое окно свойств источника данных, учетные данные | Документация Майкрософт
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.shareddatasource.credentials.f1
ms.assetid: c08d1a5f-206b-4d53-ab1a-368b651ee5bb
author: maggiesmsft
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a6546a9b38c8f12e493ea9fa47741fa56c9fab79
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/02/2018
ms.locfileid: "48171084"
---
# <a name="shared-data-source-properties-dialog-box-credentials"></a>Диалоговое окно «Свойства общего источника данных» — «Учетные данные»
  Выберите вкладку **Учетные данные** в диалоговом окне **Свойства общего источника данных** для отображения и изменения учетных данных, используемых для подключения к общему источнику данных в отчете. Предоставленные учетные данные используются для доступа к источнику данных и кэширования копии данных для предварительного просмотра отчета. Дополнительные сведения о кэшировании данных для предварительного просмотра см. в разделе [Предварительный просмотр отчетов](reports/previewing-reports.md). Дополнительные сведения об учетных данных см. в разделе [Указание учетных данных и сведений о соединении для источников данных отчета](report-data/specify-credential-and-connection-information-for-report-data-sources.md).  
  
## <a name="options"></a>Параметры  
 **Использовать проверку подлинности Windows (встроенная безопасность)**  
 Выберите этот параметр, чтобы использовать проверку подлинности Windows.  
  
 **Использовать имя пользователя и пароль**  
 Выберите этот параметр, чтобы использовать определенное имя пользователя и пароль. Для общих источников данных при публикации проекта сервера отчетов на целевом сервере имя пользователя и пароль сохраняются как сохраненные учетные данные для базы данных. Если необходимо использовать имя пользователя и пароль как учетные данные Windows, можно изменить свойства опубликованного общего источника данных на целевом сервере. Дополнительные сведения см. в разделе [Создание, удаление или изменение общего источника данных (диспетчер отчетов)](../../2014/reporting-services/create-delete-or-modify-a-shared-data-source-report-manager.md).  
  
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
  
## <a name="see-also"></a>См. также  
 [Подключения к данным, источники данных и строки подключения в службах Reporting Services](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [Задание учетных данных и сведениях о соединении для источников данных отчета](report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [Диалоговое окно "Свойства общего источника данных" — "Общие"](../../2014/reporting-services/shared-data-source-properties-dialog-box-general.md)  
  
  
