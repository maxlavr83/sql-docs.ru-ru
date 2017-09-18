---
title: "Свойство обработчика (RDS) | Документы Microsoft"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- Handler property [ADO]
ms.assetid: fdc34362-6d47-4727-b171-8d033159408e
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 25ac7c676fbab1e8b5899a3502fab2199b0afd22
ms.contentlocale: ru-ru
ms.lasthandoff: 09/09/2017

---
# <a name="handler-property-rds"></a>Свойство обработчика (RDS)
Указывает имя программы настройки на стороне сервера (обработчик), которая расширяет функциональность [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)и любые параметры, используемые *обработчик*.  
  
 **Область применения:** [DataControl объекта (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
> [!IMPORTANT]
>  Начиная с Windows 8 и Windows Server 2012, серверные компоненты служб удаленных рабочих СТОЛОВ больше не включаются в операционной системе Windows (в разделе Windows 8 и [руководство по Windows Server 2012 совместимости](https://www.microsoft.com/en-us/download/details.aspx?id=27416) для получения дополнительных сведений). Клиентские компоненты служб удаленных рабочих СТОЛОВ будут удалены в будущих версиях Windows. Избегайте использования этого компонента в новых разработках и запланируйте изменение существующих приложений, в которых он применяется. Приложения, использующие служб удаленных рабочих СТОЛОВ необходимо перенести в [службы данных WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
DataControl.Handler = String  
```  
  
#### <a name="parameters"></a>Параметры  
 *DataControl*  
 Объектную переменную, которая представляет [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) объекта.  
  
 *Строковые значения*  
 Объект **строка** значение, содержащее имя обработчика и все параметры всех разделяемых точкой с запятой (например, `"handlerName,parm1,parm2,...,parm` *N*`"`).  
  
## <a name="remarks"></a>Замечания  
 Это свойство поддерживает [настройки](../../../ado/guide/remote-data-service/datafactory-customization.md), функциональные возможности этого требует параметр [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) свойства **adUseClient**.  
  
 Имя обработчика и его параметрах, если таковые имеются, разделяются запятыми («,»). Приведет к непредсказуемому поведению, если точка с запятой («;») отображается в любом месте в пределах *строка*. Можно написать собственный обработчик, предоставляемых он поддерживает **IDataFactoryHandler** интерфейса.  
  
 Обработчик по умолчанию называется **MSDFMAP. Обработчик**, и его параметр по умолчанию с именем файла настроек **MSDFMAP. INI**. Это свойство можно используйте для вызова альтернативные настройки файлы, созданные администратором сервера.  
  
 Вместо него следует использовать параметр **обработчик** будет указать обработчик и параметры в свойство [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) свойства; т. е»**обработчик =** * handlerName параметр1, параметр2...; *".  
  
## <a name="applies-to"></a>Объект применения  
 [Объект DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>См. также:  
 [Пример свойства обработчика (Visual Basic)](../../../ado/reference/rds-api/handler-property-example-vb.md)   
 [Настройка DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Объект DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)


