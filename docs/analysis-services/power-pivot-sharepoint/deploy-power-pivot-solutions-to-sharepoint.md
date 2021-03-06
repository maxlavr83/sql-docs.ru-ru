---
title: Развертывание решений PowerPivot для SharePoint | Документация Майкрософт
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: cc0286a3799aa56090fc6861b0a79b302b47aa26
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2018
ms.locfileid: "52544268"
---
# <a name="deploy-power-pivot-solutions-to-sharepoint"></a>Развертывание решений PowerPivot в SharePoint
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Используйте следующие инструкции, чтобы вручную развернуть два пакета решений, которые добавляют компоненты [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] в среду SharePoint Server 2010. Развертывание решений — это обязательный шаг по настройке [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] для SharePoint на сервере SharePoint 2010. Сведения о просмотре полного списка необходимых действий см. в разделе [Настройка и администрирование сервера Power Pivot в центре администрирования](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md).  
  
 Кроме того, для развертывания решений можно использовать средство настройки [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . При установке одиночного сервера проще и удобнее использовать средство настройки, однако если вы предпочитаете знакомое средство или если требуется настроить несколько компонентов одновременно, то лучше пользоваться центром администрирования и PowerShell. Дополнительные сведения об использовании средства настройки см. в разделе [Средства настройки PowerPivot](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md).  
  
 Перед развертыванием решения необходимо установить [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] для SharePoint с установочного носителя SQL Server 2012. Программа установки SQL Server устанавливает пакеты решения, которое вы собираетесь развертывать.  
  
 Этот раздел состоит из следующих подразделов.  
  
 [Предварительные требования. Убедитесь, что веб-приложения используется классический режим проверки подлинности](#bkmk_classic)  
  
 [Шаг 1. Развертывание решения фермы](#bkmk_farm)  
  
 [Шаг 2. Развертывание решения Power Pivot веб-приложения в центре администрирования](#deployCA)  
  
 [Шаг 3. Развертывание решения Power Pivot веб-приложения в других веб-приложений](#deployUI)  
  
 [Повторное развертывание или отзыв решения](#retract)  
  
 [О решениях PowerPivot](#intro)  
  
##  <a name="bkmk_classic"></a> Предварительные требования. Проверка использования классического режима проверки подлинности в веб-приложении  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] для SharePoint поддерживается только в тех веб-приложениях, которые используют классическую проверку подлинности Windows. Чтобы проверить, использует ли приложение классический режим, выполните следующий командлет PowerShell из **консоль управления SharePoint 2010**, заменив **http://\<имя сайта верхнего уровня >** с Имя сайта SharePoint:  
  
```  
Get-spwebapplication http://<top-level site name> | format-list UseClaimsAuthentication  
```  
  
 Должно быть возвращено значение **false**. Если значение равно **true**, доступ к данным [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] с помощью этого веб-приложения невозможен.  
  
##  <a name="bkmk_farm"></a> Шаг 1. Разверните решение фермы  
 В этом разделе показано, как развертывать решения с помощью PowerShell, но для этой задачи можно использовать и средство настройки [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Дополнительные сведения см. в разделе [Настройка или восстановление Power Pivot для SharePoint 2010 (средство настройки Power Pivot)](http://msdn.microsoft.com/d61f49c5-efaa-4455-98f2-8c293fa50046).  
  
 Это действие выполняется один раз после установки [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] для SharePoint.  
  
1.  На сервере, где установлен компонент [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] для SharePoint, откройте консоль управления SharePoint 2010 с параметром **Запуск от имени администратора** .  
  
2.  Для добавления решения фермы выполните следующий командлет.  
  
    ```  
    Add-SPSolution -LiteralPath "C:\Program Files\Microsoft SQL Server\110\Tools\PowerPivotTools\ConfigurationTool\Resources\PowerPivotFarm.wsp"  
    ```  
  
     Командлет возвратит имя решения, его идентификатор, а также атрибут Deployed=False. На следующем шаге будет выполнено развертывание решения.  
  
3.  Выполните следующий командлет, чтобы развернуть решение фермы.  
  
    ```  
    Install-SPSolution -Identity PowerPivotFarm.wsp -GACDeployment -Force  
    ```  
  
##  <a name="deployCA"></a> Шаг 2. Развертывание решения Power Pivot веб-приложения в центре администрирования  
 После развертывания решения фермы следует развернуть решение веб-приложения для центра администрирования. Это действие добавляет в центр администрирования панель мониторинга [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
1.  Откройте консоль управления SharePoint 2010, выбрав команду **Запуск от имени администратора** .  
  
2.  Выполните следующий командлет, чтобы создать ссылку на центр администрирования.  
  
    ```  
    $centralAdmin = $(Get-SPWebApplication -IncludeCentralAdministration | Where { $_.IsAdministrationWebApplication -eq $TRUE})  
    ```  
  
3.  Для добавления решения фермы выполните следующий командлет.  
  
    ```  
    Add-SPSolution -LiteralPath "C:\Program Files\Microsoft SQL Server\110\Tools\PowerPivotTools\ConfigurationTool\Resources\PowerPivotWebApp.wsp"  
    ```  
  
     Командлет возвратит имя решения, его идентификатор, а также атрибут Deployed=False. На следующем шаге будет выполнено развертывание решения.  
  
4.  Выполните следующий командлет для установки решения веб-приложения в центре администрирования.  
  
    ```  
    Install-SPSolution -Identity PowerPivotWebApp.wsp -GACDeployment -Force -WebApplication $centralAdmin  
    ```  
  
 Теперь, когда решение веб-приложения развернуто в центре администрирования, оставшиеся шаги конфигурации можно выполнить с помощью центра администрирования.  
  
##  <a name="deployUI"></a> Шаг 3. Развертывание решения Power Pivot веб-приложения в других веб-приложений  
 В предыдущей задаче решение powerpivotwebapp.wsp было развернуто в центре администрирования. В этом разделе описано развертывание решения powerpivotwebapp.wsp для каждого веб-приложения, поддерживающего доступ к данным [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . При добавлении других веб-приложений в дальнейшем необходимо будет повторить для них этот шаг.  
  
1.  В разделе «Системные параметры» центра администрирования выберите **Управление решениями фермы**.  
  
2.  Щелкните **powerpivotwebapp.wsp**.  
  
3.  Нажмите **Развернуть решение**.  
  
4.  В разделе **Развертывание в**выберите веб-приложение SharePoint, для которого необходимо добавить поддержку компонента [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
5.  Нажмите кнопку **ОК**.  
  
6.  Повторите процедуру для других веб-приложений SharePoint, которые тоже будут поддерживать доступ к данным [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
##  <a name="retract"></a> Повторное развертывание или отзыв решения  
 Хотя центр администрирования SharePoint позволяет отзывать решения, для файла powerpivotwebapp.wsp это следует делать только тогда, когда систематически проводится диагностика проблем установки или развертывания обновлений.  
  
1.  В разделе «Системные параметры» центра администрирования SharePoint 2010 выберите **Управление решениями фермы**.  
  
2.  Щелкните **Powerpivotwebapp.wsp**.  
  
3.  Нажмите **Отозвать решение**.  
  
 Если при развертывании сервера возникли проблемы, связанные с решением фермы, повторите развертывание, выбрав в средстве настройки **вариант** Восстановить [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Предпочтительнее выполнять операции восстановления с помощью PowerPivot Configuration Tool, так как они включают меньше шагов. Дополнительные сведения см. в разделе [Настройка или восстановление Power Pivot для SharePoint 2010 (средство настройки Power Pivot)](http://msdn.microsoft.com/d61f49c5-efaa-4455-98f2-8c293fa50046).  
  
 Если же необходимо повторное развертывание всех решений, обязательно выполните его в следующем порядке:  
  
1.  Отзыв решения для веб-приложений [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] из всех веб-приложений SharePoint, которые его используют.  
  
2.  Отзыв решения фермы [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
3.  Повторное развертывание решения фермы [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
4.  Повторное развертывание решения [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] для веб-приложений PowerPivot для всех веб-приложений SharePoint.  
  
##  <a name="intro"></a> О решениях PowerPivot  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] для SharePoint использует два пакета решений для развертывания страниц своего приложения и программных файлов в ферме и отдельных веб-приложениях.  
  
-   Решение фермы является глобальным. Оно развертывается один раз и автоматически становится доступным для любого нового сервера [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] для SharePoint, который будет добавлен в ферму в будущем.  
  
-   Решение веб-приложения для каждого приложения свое и должно развертываться для каждого приложения на ферме, включая веб-приложение центра администрирования (Central Administration).  
  
 Каждое решение развертывается индивидуально.  Решение фермы развертывается один раз после установки первого экземпляра [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] для SharePoint. Для развертывания решения фермы используется средство настройки [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] или командлеты PowerShell.  
  
 Решение веб-приложения сначала развертывается в центре администрирования, а затем — в любых дополнительных веб-приложениях с поддержкой запросов к данным [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Развернуть решение веб-приложения в центре администрирования можно с помощью средства настройки [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] или командлета PowerShell. Решение веб-приложения для других веб-приложений можно развернуть вручную с помощью центра администрирования или PowerShell.  
  
|Решение|Описание|  
|--------------|-----------------|  
|Powerpivotfarm.wsp|Добавляет файл Microsoft.AnalysisServices.SharePoint.Integration.dll к глобальной сборке.<br /><br /> Добавляет файл Microsoft.AnalysisServices.ChannelTransport.dll к глобальной сборке.<br /><br /> Устанавливает функции и файлы ресурсов, а также регистрирует типы содержимого.<br /><br /> Добавляет шаблоны библиотек для библиотек веб-канала данных и коллекции [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .<br /><br /> Добавляет страницы приложений для настройки приложений службы, панели мониторинга [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , обновления данных и коллекции [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .|  
|powerpivotwebapp.wsp|Добавляет файлы ресурсов Microsoft.AnalysisServices.SharePoint.Integration.dll в папку расширений веб-сервера на сервере клиентского веб-интерфейса.<br /><br /> Добавляет веб-службу [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] к серверу клиентского веб-интерфейса.<br /><br /> Добавляет возможность формирования эскизов для коллекции [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .|  
  
## <a name="see-also"></a>См. также  
 [Обновление Power Pivot для SharePoint](../../database-engine/install-windows/upgrade-power-pivot-for-sharepoint.md)   
 [Настройка и администрирование сервера Power Pivot в центре администрирования](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)   
 [Настройка PowerPivot с помощью Windows PowerShell](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell.md)  
  
  
