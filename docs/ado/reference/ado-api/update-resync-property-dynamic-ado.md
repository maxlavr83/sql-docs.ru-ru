---
title: Обновить повторная синхронизация свойство (динамическое) (ADO) | Документация Майкрософт
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Update Resync property [ADO]
ms.assetid: 8a3bb608-66d7-4128-a3ef-84cb0556de0d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 43b8864d03e3ec2e563984e203779e5905a15813
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/01/2018
ms.locfileid: "47762764"
---
# <a name="update-resync-property-dynamic-ado"></a>Свойство Update Resync (динамическое) (ADO)
Указывает ли [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) метод сопровождается неявным [Resync](../../../ado/reference/ado-api/resync-method.md) работы метода и если да, область этой операции.  
  
## <a name="settings-and-return-values"></a>Параметры и возвращаемые значения  
 Задает или возвращает один или несколько [ADCPROP_UPDATERESYNC_ENUM](../../../ado/reference/ado-api/adcprop-updateresync-enum.md) значения.  
  
## <a name="remarks"></a>Примечания  
 Значения ADCPROP_UPDATERESYNC_ENUM могут быть объединены, за исключением adResyncAll, который уже представляет сочетание остальная часть значения.  
  
 Константа **adResyncConflicts** сохраняет значения повторной синхронизации в качестве базового значения, но не переопределяет ожидающие изменения.  
  
 **Обновить повторная синхронизация** динамическое свойство добавляется к [записей](../../../ado/reference/ado-api/recordset-object-ado.md) объект [свойства](../../../ado/reference/ado-api/properties-collection-ado.md) коллекции при [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) свойству **adUseClient**.  
  
## <a name="applies-to"></a>Объект применения  
 [Объект Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
