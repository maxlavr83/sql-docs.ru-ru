---
title: Метод ListReportServersInDatabase (WMI MSReportServer_ConfigurationSetting) | Документы Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
api_name:
- ListReportServersInDatabase (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- ListReportServersInDatabase method
ms.assetid: a4bf5968-c46f-484f-a510-65e2dde65a0d
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: e66a3277554c349b18499b4a1b4546ed504a043c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/02/2018
ms.locfileid: "48165374"
---
# <a name="listreportserversindatabase-method-wmi-msreportserverconfigurationsetting"></a>Метод ListReportServersInDatabase (WMI MSReportServer_ConfigurationSetting)
  Возвращает список установок сервера отчетов, которые находятся в базе данных сервера отчетов независимо от наличия доступа к защищенным сведениям.  
  
## <a name="syntax"></a>Синтаксис  
  
```vb  
Public Sub ListReportServersInDatabase(ByRef MachineNames() As String, _  
    ByRef InstanceNames() As String, ByRef InstallationIDs() As String, _  
    ByRef IsInitialized() As Boolean, ByRef Length As Int32, _  
    ByRef HRESULT As Int32, ByRef ExtendedErrors() As String)  
```  
  
```csharp  
public void ListReportServersInDatabase (out string[] MachineNames,   
    out string[] InstanceNames, out string[] InstallationIDs,   
    out Boolean[] IsInitialized,out Int32 Length, out Int32 HRESULT,    
    out string[] ExtendedErrors);  
```  
  
## <a name="parameters"></a>Параметры  
 *MachineNames[]*  
 [out] Массив, который содержит имена компьютеров, где установлен сервер отчетов в базе данных.  
  
 *InstanceNames[]*  
 [out] Массив, который содержит имена экземпляров каждого установленного сервера отчетов в базе данных.  
  
 *InstallationIDs[]*  
 [out] Массив, который содержит коды установки каждого установленного сервера отчетов в базе данных.  
  
 *IsInitialized[]*  
 [out] Массив, который содержит состояние инициализации каждого установленного сервера отчетов в базе данных.  
  
 *Длина*  
 [out] Длина массивов, возвращаемых методом. Все возвращенные массивы имеют одинаковую длину.  
  
 *HRESULT*  
 [out] Значение, которое указывает, окончился ли вызов успехом или сбоем.  
  
 *ExtendedErrors[]*  
 [out] Массив строк, содержащий дополнительные ошибки, возвращенные в результате вызова.  
  
## <a name="return-value"></a>Возвращаемое значение  
 Возвращает значение *HRESULT* , являющееся признаком успешного или неуспешного завершение вызова метода. Значение 0 указывает, что вызов метода завершился успешно. Ненулевое значение указывает, что произошла ошибка.  
  
## <a name="remarks"></a>Примечания  
 Метод ListReportServersInDatabase выводит список установленных серверов отчетов, которые имеются в базе данных сервера отчетов, независимо от наличия у них доступа к защищенным сведениям, и возвращает сопоставленный набор массивов с данными о каждом установленном сервере отчетов.  
  
## <a name="requirements"></a>Требования  
 **Пространство имен:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>См. также  
 [Элементы MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
