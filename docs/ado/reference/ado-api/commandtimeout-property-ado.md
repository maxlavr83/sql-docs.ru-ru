---
title: Свойство CommandTimeout (ADO) | Документация Майкрософт
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::CommandTimeout
helpviewer_keywords:
- CommandTimeout property [ADO]
ms.assetid: c611f857-d6b0-4dca-8925-f4a02e769eb0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c5bb74384e043130ccfe4c3399b363b25d40737c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/01/2018
ms.locfileid: "47632162"
---
# <a name="commandtimeout-property-ado"></a>Свойство CommandTimeout (ADO)
Указывает время ожидания при выполнении команды перед завершается и генерируется ошибка.  
  
## <a name="settings-and-return-values"></a>Параметры и возвращаемые значения  
 Возвращает или задает **Long** значение, которое указывает, в секундах время ожидания выполнения команды. По умолчанию — 30.  
  
## <a name="remarks"></a>Примечания  
 Используйте **CommandTimeout** свойство [подключения](../../../ado/reference/ado-api/connection-object-ado.md) объекта или [команда](../../../ado/reference/ado-api/command-object-ado.md) разрешает отмену [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) метод вызов, из-за задержки от использования сетевой трафик или большим числом операций сервера. Если значение интервала **CommandTimeout** свойство истекает до завершения команды выполнения, возникает ошибка и ADO отменяет команду. Если свойство задано равным нулю, ADO будет ждать неограниченное время выполнения. Убедитесь, что поставщик и источник данных к которой вы пишете код поддержки **CommandTimeout** функциональные возможности.  
  
 **CommandTimeout** на **подключения** объекта не оказывает влияния на **CommandTimeout** на **команда** объект же **подключения**, то есть **команда** объекта **CommandTimeout** свойства не наследует значение **подключения** объекта **CommandTimeout** значение.  
  
 На **подключения** объекта, **CommandTimeout** остается свойство чтения/записи после **подключения** открыт.  
  
## <a name="applies-to"></a>Объект применения  
  
|||  
|-|-|  
|[Объект Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[Объект Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|  
  
## <a name="see-also"></a>См. также  
 [ActiveConnection, CommandText, CommandTimeout, CommandType, размер и направление свойства пример (Visual Basic)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, размер и направление пример свойства (Visual C++)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, размер и направление примеры свойств (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)   
 [Свойство ConnectionTimeout (ADO)](../../../ado/reference/ado-api/connectiontimeout-property-ado.md)
