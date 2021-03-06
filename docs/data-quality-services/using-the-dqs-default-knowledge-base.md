---
title: Использование базы знаний DQS по умолчанию | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2012
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: b36af13b-9fcc-4168-bb92-214d600b1c93
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: bd057885bbaa3aa6439079a744ac0b2d341dd638
ms.sourcegitcommit: c19696d3d67161ce78aaa5340964da3256bf602d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/29/2018
ms.locfileid: "52616734"
---
# <a name="using-the-dqs-default-knowledge-base"></a>Использование базы знаний DQS по умолчанию

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  В этом разделе описывается база знаний **DQS Data**, которая используется по умолчанию и устанавливается со службами [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Эта готовая база данных содержит следующие домены.  
  
-   **Страна/регион**. Содержит длинное (официальное) название страны или региона, общепринятое короткое название (используемое в списках, на картах и т. п.), двухбуквенное или трехбуквенное обозначение, а также трехзначный цифровой код каждого расположения.  В качестве первого значения указывается длинное название страны.  
  
-   **Страна/регион (трехбуквенное первое значение)**. Содержит длинное (официальное) название страны или региона, общепринятое короткое название (используемое в списках, на картах и т. п.), двухбуквенное или трехбуквенное обозначение, а также трехзначный цифровой код каждого расположения.  В качестве первого значения указывается трехбуквенное обозначение округа.  
  
-   **Страна/регион (двухбуквенное первое значение)**. Содержит длинное (официальное) название страны или региона, общепринятое короткое название (используемое в списках, на картах и т. п.), двухбуквенное или трехбуквенное обозначение, а также трехзначный цифровой код каждого расположения.  В качестве первого значения указывается двухбуквенное обозначение страны.  
  
-   **США — округа**. Содержит список округов США.  
  
-   **США — фамилии**. Содержит список фамилий, встречающихся 100 или более раз в отчете о переписи населения Census 2000.  
  
-   **США — географические пункты**. Содержит список географических пунктов для 50 штатов, округа Колумбия и Пуэрто-Рико из переписи Census 2010.  
  
-   **США — штаты**. Содержит условное длинное (официальное) название и двухбуквенное обозначение каждого штата США. В качестве первого значения указывается длинное (официальное) название штата.  
  
-   **США — штат (двухбуквенный заголовок)**. Содержит условное длинное (официальное) название и двухбуквенное обозначение каждого штата США. В качестве первого значения указывается двухбуквенное обозначение штата.  
  
## <a name="using-the-default-knowledge-base"></a>Использование базы знаний по умолчанию  
 База знаний по умолчанию DQS Data служб DQS позволяет сделать следующее.  
  
-   Быстро запустить и внедрить проект по качеству данных с помощью базы знаний по умолчанию, не создавая новую базу знаний служб DQS.  
  
-   Выполнять действия по управлению доменами и обнаружению знаний, а также действия, связанные с политикой сопоставления, в базе данных по умолчанию. Для этого нажмите кнопку **Открыть базу знаний** на экране [Data Quality Client Home Screen](../data-quality-services/data-quality-client-home-screen.md), выберите базу знаний **DQS Data** на экране **Открыть базу знаний** и выберите нужное действие в области **Выбрать действие** . Чтобы продолжить, нажмите кнопку **Далее** .  
  
-   Создать новую базу знаний с помощью базы знаний по умолчанию. Сведения о создании базы знаний на основе существующей базы знаний см. в разделе [Create a Knowledge Base](../data-quality-services/create-a-knowledge-base.md).  
  
-   Использовать базу знаний по умолчанию можно в [компоненте DQS Cleansing  в службах Integration Services](https://go.microsoft.com/fwlink/?LinkId=238830) , а также в [надстройке Master Data Services для Excel](../master-data-services/microsoft-excel-add-in/data-quality-matching-in-the-mds-add-in-for-excel.md).  
  
## <a name="see-also"></a>См. также:  
 [Базы знаний и домены DQS](../data-quality-services/dqs-knowledge-bases-and-domains.md)  
  
  
