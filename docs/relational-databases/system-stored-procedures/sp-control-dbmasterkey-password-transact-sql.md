---
title: sp_control_dbmasterkey_password (Transact-SQL) | Документация Майкрософт
ms.custom: ''
ms.date: 02/25/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_control_dbmasterkey_password
- sp_control_dbmasterkey_password_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_control_dbmasterkey_password
ms.assetid: 63979a87-42a2-446e-8e43-30481faaf3ca
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: af6e23ba3cce2ef4dfaa6901f51a9d6c0b034e60
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/01/2018
ms.locfileid: "47659912"
---
# <a name="spcontroldbmasterkeypassword-transact-sql"></a>sp_control_dbmasterkey_password (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Добавляет или удаляет учетные данные, содержащие пароль, необходимый для открытия главного ключа базы данных.  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
sp_control_dbmasterkey_password @db_name = 'database_name,  
     @password = 'master_key_password' , @action = { 'add' | 'drop' }  
```  
  
## <a name="arguments"></a>Аргументы  
 @db_name= N'*имя_базы_данных*"  
 Указывает имя базы данных, ассоциированной с этими учетными данными. База данных не может быть системной. *database_name* — **nvarchar**.  
  
 @password= N'*пароль*"  
 Указывает пароль для главного ключа. *пароль* — **nvarchar**.  
  
 @action= N'add "  
 Указывает на то, что учетные данные для указанной базы данных будет добавлены в хранилище учетных данных. Учетные данные будут содержать пароль главного ключа базы данных. Значение, передаваемое @action — **nvarchar**.  
  
 @action= N'drop "  
 Указывает на то, что учетные данные для указанной базы данных будет удалены из хранилища учетных данных. Значение, передаваемое @action — **nvarchar**.  
  
## <a name="remarks"></a>Примечания  
 Если [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] нужен главный ключ базы данных для расшифровки или шифрования ключа, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] пытается расшифровать главный ключ базы данных с помощью главного ключа службы экземпляра. Если расшифровка заканчивается неудачей, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] выполняет в хранилище учетных данных поиск учетных данных главного ключа, имеющих идентификатор GUID того же семейства, что и у базы данных, для которой нужен главный ключ. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] пытается расшифровать главный ключ базы данных с помощью всех подходящих учетных данных, пока не удастся расшифровать ключ или пока не кончатся учетные данные.  
  
> [!CAUTION]  
>  Не создавайте учетные данные главного ключа для базы данных, которая должна быть недоступна sa и другим привилегированным участникам [системы безопасности] на уровне сервера. База данных может быть настроена таким образом, чтобы иерархия ее ключей не могла быть расшифрована главным ключом службы. Этот параметр поддерживается для максимальной защиты баз данных, содержащих зашифрованные сведения, которые не должны быть доступны sa или другим привилегированным участникам [системы безопасности] на уровне сервера. Создание учетных данных главного ключа для такой базы данных сводит на нет эту защиту, позволяя sa и другим привилегированным участникам [системы безопасности] на уровне сервера расшифровывать базу данных.  
  
 Учетные данные, созданные с помощью процедуры sp_control_dbmasterkey_password, отображаются в [sys.master_key_passwords](../../relational-databases/system-catalog-views/sys-master-key-passwords-transact-sql.md) представления каталога. Имена учетных данных, созданные для главных ключей базы данных имеют следующий формат: `##DBMKEY_<database_family_guid>_<random_password_guid>##`. Пароль хранится как секретные учетные данные. Для каждого пароля, добавленного в хранилище учетных данных, существует строка в представлении sys.credentials.  
  
 Процедуру sp_control_dbmasterkey_password нельзя использовать для создания учетных данных для следующих системных баз данных: master, model, msdb или tempdb.  
  
 Процедура sp_control_dbmasterkey_password не проверяет возможность пароля открывать главный ключ указанной базы данных.  
  
 Если задан пароль, который уже хранится в учетных данных для указанной базы данных, выполнение процедуры sp_control_dbmasterkey_password будет завершено неудачно.  
  
> [!NOTE]  
>  Две базы данных из различных экземпляров сервера могут иметь один и тот же идентификатор GUID семейства. Если такое происходит, базы данных будут иметь одну и ту же запись главного ключа в хранилище учетных данных.  
  
 Параметры, переданные в процедуру sp_control_dbmasterkey_password, не появляются в трассировках.  
  
> [!NOTE]  
>  Если учетные данные, добавленные с помощью процедуры sp_control_dbmasterkey_password, используются для открытия главного ключа базы данных, то главный ключ базы данных повторно шифруется главным ключом службы. Если база данных находится в режиме только для чтения, то операция повторного шифрования оканчивается неудачей и главный ключ базы данных останется незашифрованным. Для последующего доступа к главному ключу базы данных необходимо использовать инструкцию OPEN MASTER KEY и пароль. Чтобы избежать необходимости использовать пароль, создавайте учетные данные до того, как база данных будет переведена в режим только для чтения.  
  
 **Потенциальная проблема обратной совместимости:** в настоящее время хранимая процедура не проверяет наличие главного ключа. Это разрешено для обратной совместимости, но при этом отображается предупреждение. Такое поведение является устаревшим. В следующем выпуске главный ключ должен существовать и пароль, используемый в хранимой процедуре **sp_control_dbmasterkey_password** должен быть тот же пароль, что один из паролей, которые используются для шифрования главного ключа базы данных.  
  
## <a name="permissions"></a>Разрешения  
 Требует разрешения CONTROL для базы данных.  
  
## <a name="examples"></a>Примеры  
  
### <a name="a-creating-a-credential-for-the-adventureworks2012-master-key"></a>A. Создание учетных данных для главного ключа AdventureWorks2012  
 В следующем примере создаются учетные данные для главного ключа базы данных `AdventureWorks2012`, пароль главного ключа сохраняется в виде секретного кода в учетных данных. Так как все параметры, передаваемые `sp_control_dbmasterkey_password` должен иметь тип данных **nvarchar**, текстовые строки преобразуются оператором приведения `N`.  
  
```  
EXEC sp_control_dbmasterkey_password @db_name = N'AdventureWorks2012',   
    @password = N'sdfjlkj#mM00sdfdsf98093258jJlfdk4', @action = N'add';  
GO  
```  
  
### <a name="b-dropping-a-credential-for-a-database-master-key"></a>Б. Удаление учетных данных для главного ключа базы данных  
 В следующем примере удаляются учетные данные, созданные в примере A. Обратите внимание, что все параметры являются обязательными, включая пароль.  
  
```  
EXEC sp_control_dbmasterkey_password @db_name = N'AdventureWorks2012',   
    @password = N'sdfjlkj#mM00sdfdsf98093258jJlfdk4', @action = N'drop';  
GO  
```  
  
## <a name="see-also"></a>См. также  
 [Настройка зашифрованной зеркальной базы данных](../../database-engine/database-mirroring/set-up-an-encrypted-mirror-database.md)   
 [Хранимые процедуры безопасности (Transact-SQL)](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [Системные хранимые процедуры (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.credentials (Transact-SQL)](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)   
 [Учетные данные (компонент Database Engine)](../../relational-databases/security/authentication-access/credentials-database-engine.md)  
  
  
