---
title: 表值参数
ms.date: 10/12/2018
dev_langs:
- csharp
- vb
ms.assetid: 370c16d5-db7b-43e3-945b-ccaab35b739b
ms.openlocfilehash: 59c6732dacf225097e22957ebe6536308a2798d4
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69938446"
---
# <a name="table-valued-parameters"></a>表值参数
表值参数提供一种将客户端应用程序中的多行数据封送到 SQL Server 的简单方式，不需要多次往返或特殊服务器端逻辑来处理数据。 您可以使用表值参数来包装客户端应用程序中的数据行，并使用单个参数化命令将数据发送到服务器。 传入的数据行存储在一个表变量中，然后您可以通过使用 Transact-SQL 对该表变量进行操作。  
  
 可以使用标准的 Transact-SQL SELECT 语句来访问表值参数中的列值。 表值参数为强类型，其结构会自动进行验证。 表值参数的大小仅受服务器内存的限制。  
  
> [!NOTE]
> 无法在表值参数中返回数据。 表值参数是只可输入的参数；不支持 OUTPUT 关键字。  
  
 有关表值参数的更多信息，请参见下列资源。  
  
|资源|描述|  
|--------------|-----------------|  
|SQL Server 联机丛书中的[表值参数 (数据库引擎)](https://go.microsoft.com/fwlink/?LinkId=98363)|说明如何创建和使用表值参数。|  
|SQL Server 联机丛书中的[用户定义表类型](https://go.microsoft.com/fwlink/?LinkId=98364)|说明用于声明表值参数的用户定义的表类型。|  
  
## <a name="passing-multiple-rows-in-previous-versions-of-sql-server"></a>在 SQL Server 的早期版本中传递多行  
 在将表值参数引入 SQL Server 2008 之前, 将多行数据传递到存储过程或参数化 SQL 命令的选项受到限制。 开发人员可以选择使用以下选项，将多个行传递给服务器：  
  
- 使用一系列单个参数表示多个数据列和行中的值。 使用此方法传递的数据量受所允许的参数数量的限制。 SQL Server 过程最多可以有 2100 个参数。 必须使用服务器端逻辑才能将这些单个值组合到表变量或临时表中以进行处理。  
  
- 将多个数据值捆绑到分隔字符串或 XML 文档中，然后将这些文本值传递给过程或语句。 此过程要求相应的过程或语句包括验证数据结构和取消捆绑值所需的逻辑。  
  
- 针对影响多个行的数据修改创建一系列的单个 SQL 语句，例如通过调用 `Update` 的 <xref:System.Data.SqlClient.SqlDataAdapter> 方法创建的内容。 可将更改单独提交给服务器，也可以将其作为组进行批处理。 不过，即使是以包含多个语句的批处理形式提交的，每个语句在服务器上还是会单独执行。  
  
- 使用 `bcp` 实用工具程序或 <xref:System.Data.SqlClient.SqlBulkCopy> 对象将很多行数据加载到表中。 尽管这项技术非常有效，但不支持服务器端处理，除非将数据加载到临时表或表变量中。  
  
## <a name="creating-table-valued-parameter-types"></a>创建表值参数类型  
 表值参数以通过使用 Transact-SQL CREATE TYPE 语句定义的强类型表结构为基础。 您必须先在 SQL Server 中创建一个表类型并定义结构，才能在客户端应用程序中使用表值参数。 有关创建表类型的详细信息, 请参阅 SQL Server 联机丛书中的[用户定义表类型](https://go.microsoft.com/fwlink/?LinkID=98364)。  
  
 下面的语句可创建一个名为 CategoryTableType 的表类型，其中包括 CategoryID 和 CategoryName 列：  
  
```  
CREATE TYPE dbo.CategoryTableType AS TABLE  
    ( CategoryID int, CategoryName nvarchar(50) )  
```  
  
 创建一个表类型后，您可以基于该类型声明表值参数。 下面的 Transact-SQL 片段演示如何在存储过程定义中声明表值参数。 请注意，声明表值参数时需要使用 READONLY 关键字。  
  
```  
CREATE PROCEDURE usp_UpdateCategories   
    (@tvpNewCategories dbo.CategoryTableType READONLY)  
```  
  
## <a name="modifying-data-with-table-valued-parameters-transact-sql"></a>通过表值参数修改数据 (Transact-SQL)  
 表值参数可在基于集的数据修改中使用，这些数据修改可通过执行单个语句影响多个行。 例如，您可以选择表值参数中的所有行，然后将它们插入到数据库表中；您也可以通过将表值参数联接到要更新的表中来创建更新语句。  
  
 下面的 Transact-SQL UPDATE 语句演示如何通过将表值参数联接到 Categories 表来使用它。 在 FROM 子句中将表值参数与 JOIN 一起使用时，您还必须为其提供一个别名，如此处所示，表值参数的别名为“ec”：  
  
```  
UPDATE dbo.Categories  
    SET Categories.CategoryName = ec.CategoryName  
    FROM dbo.Categories INNER JOIN @tvpEditedCategories AS ec  
    ON dbo.Categories.CategoryID = ec.CategoryID;  
```  
  
 此 Transact-SQL 示例演示如何从表值参数中选择行以在单个基于集的操作中执行 INSERT。  
  
```  
INSERT INTO dbo.Categories (CategoryID, CategoryName)  
    SELECT nc.CategoryID, nc.CategoryName FROM @tvpNewCategories AS nc;  
```  
  
## <a name="limitations-of-table-valued-parameters"></a>表值参数的限制  
 以下是表值参数的几个限制：  
  
- 不能将表值参数传递给[CLR 用户定义函数](/sql/relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions)。  
  
- 只有对表值参数进行索引才能支持 UNIQUE 或 PRIMARY KEY 约束。 SQL Server 不维护有关表值参数的统计信息。  
  
- 在 Transact-SQL 代码中表值参数是只读的。 无法更新表值参数的行中的列值且无法插入或删除行。 若要修改传递给表值参数中的存储过程或参数化语句的数据，则必须将数据插入到临时表或表变量中。  
  
- 无法使用 ALTER TABLE 语句来修改表值参数的设计。  
  
## <a name="configuring-a-sqlparameter-example"></a>配置 SqlParameter 示例  
 <xref:System.Data.SqlClient><xref:System.Data.DataTable>支持从<xref:System.Data.Common.DbDataReader>或对象填充<xref:System.Collections.Generic.IEnumerable%601>表值参数。  \  <xref:Microsoft.SqlServer.Server.SqlDataRecord> 必须通过使用 <xref:System.Data.SqlClient.SqlParameter.TypeName%2A> 的 <xref:System.Data.SqlClient.SqlParameter> 属性指定表值参数的类型名称。 `TypeName` 必须与以前在服务器上创建的兼容类型的名称相匹配。 下面的代码段演示如何配置 <xref:System.Data.SqlClient.SqlParameter> 以插入数据。  
 
在下面的示例中, `addedCategories`变量包含一个<xref:System.Data.DataTable>。 若要查看如何填充变量, 请参阅下一节中的示例, 将[表值参数传递给存储过程](#passing)。

```csharp  
// Configure the command and parameter.  
SqlCommand insertCommand = new SqlCommand(sqlInsert, connection);  
SqlParameter tvpParam = insertCommand.Parameters.AddWithValue("@tvpNewCategories", addedCategories);  
tvpParam.SqlDbType = SqlDbType.Structured;  
tvpParam.TypeName = "dbo.CategoryTableType";  
```  
  
```vb  
' Configure the command and parameter.  
Dim insertCommand As New SqlCommand(sqlInsert, connection)  
Dim tvpParam As SqlParameter = _  
   insertCommand.Parameters.AddWithValue( _  
  "@tvpNewCategories", addedCategories)  
tvpParam.SqlDbType = SqlDbType.Structured  
tvpParam.TypeName = "dbo.CategoryTableType"  
```  
  
 您也可以使用从 <xref:System.Data.Common.DbDataReader> 中派生的任何对象，将数据行流处理到表值参数，如本代码段所示：  
  
```csharp  
// Configure the SqlCommand and table-valued parameter.  
SqlCommand insertCommand = new SqlCommand("usp_InsertCategories", connection);  
insertCommand.CommandType = CommandType.StoredProcedure;  
SqlParameter tvpParam = insertCommand.Parameters.AddWithValue("@tvpNewCategories", dataReader);  
tvpParam.SqlDbType = SqlDbType.Structured;  
```  
  
```vb  
' Configure the SqlCommand and table-valued parameter.  
Dim insertCommand As New SqlCommand("usp_InsertCategories", connection)  
insertCommand.CommandType = CommandType.StoredProcedure  
Dim tvpParam As SqlParameter = _  
  insertCommand.Parameters.AddWithValue("@tvpNewCategories", _  
  dataReader)  
tvpParam.SqlDbType = SqlDbType.Structured  
```  
  
## <a name="passing"></a>将表值参数传递给存储过程  
 此示例演示如何将表值参数数据传递给存储过程。 示例代码通过使用 <xref:System.Data.DataTable> 方法，将已添加的行提取到新的 <xref:System.Data.DataTable.GetChanges%2A> 中。 然后，示例代码定义一个 <xref:System.Data.SqlClient.SqlCommand>，并将 <xref:System.Data.SqlClient.SqlCommand.CommandType%2A> 属性设置为 <xref:System.Data.CommandType.StoredProcedure>。 示例代码通过使用 <xref:System.Data.SqlClient.SqlParameter> 方法对 <xref:System.Data.SqlClient.SqlParameterCollection.AddWithValue%2A> 进行填充，并将 <xref:System.Data.SqlClient.SqlParameter.SqlDbType%2A> 设置为 `Structured`。 然后，通过使用 <xref:System.Data.SqlClient.SqlCommand> 方法执行 <xref:System.Data.SqlClient.SqlCommand.ExecuteNonQuery%2A>。  
  
```csharp  
// Assumes connection is an open SqlConnection object.  
using (connection)  
{  
  // Create a DataTable with the modified rows.  
  DataTable addedCategories = CategoriesDataTable.GetChanges(DataRowState.Added);  

  // Configure the SqlCommand and SqlParameter.  
  SqlCommand insertCommand = new SqlCommand("usp_InsertCategories", connection);  
  insertCommand.CommandType = CommandType.StoredProcedure;  
  SqlParameter tvpParam = insertCommand.Parameters.AddWithValue("@tvpNewCategories", addedCategories);  
  tvpParam.SqlDbType = SqlDbType.Structured;  

  // Execute the command.  
  insertCommand.ExecuteNonQuery();  
}  
```  
  
```vb  
' Assumes connection is an open SqlConnection object.  
Using connection  
   '  Create a DataTable with the modified rows.  
   Dim addedCategories As DataTable = _  
     CategoriesDataTable.GetChanges(DataRowState.Added)  
  
  ' Configure the SqlCommand and SqlParameter.  
   Dim insertCommand As New SqlCommand( _  
     "usp_InsertCategories", connection)  
   insertCommand.CommandType = CommandType.StoredProcedure  
   Dim tvpParam As SqlParameter = _  
     insertCommand.Parameters.AddWithValue( _  
     "@tvpNewCategories", addedCategories)  
   tvpParam.SqlDbType = SqlDbType.Structured  
  
   '  Execute the command.  
   insertCommand.ExecuteNonQuery()  
End Using  
```  
  
### <a name="passing-a-table-valued-parameter-to-a-parameterized-sql-statement"></a>将表值参数传递给参数化 SQL 语句  
 下面的示例演示如何通过使用带有 SELECT 子查询（具有作为数据源的表值参数）的 INSERT 语句将数据插入 dbo.Categories 表中。 将表值参数传递给参数化 SQL 语句时，必须通过使用 <xref:System.Data.SqlClient.SqlParameter.TypeName%2A> 的新 <xref:System.Data.SqlClient.SqlParameter> 属性指定表值参数的类型名称。 此 `TypeName` 必须与以前在服务器上创建的兼容类型的名称相匹配。 此示例中的代码使用 `TypeName` 属性来引用 dbo.CategoryTableType 中定义的类型结构。  
  
> [!NOTE]
> 如果为表值参数中的标识列提供值，则必须为该会话发出 SET IDENTITY_INSERT 语句。  
  
```csharp  
// Assumes connection is an open SqlConnection.  
using (connection)  
{  
  // Create a DataTable with the modified rows.  
  DataTable addedCategories = CategoriesDataTable.GetChanges(DataRowState.Added);  

  // Define the INSERT-SELECT statement.  
  string sqlInsert =   
      "INSERT INTO dbo.Categories (CategoryID, CategoryName)"  
      + " SELECT nc.CategoryID, nc.CategoryName"  
      + " FROM @tvpNewCategories AS nc;"  

  // Configure the command and parameter.  
  SqlCommand insertCommand = new SqlCommand(sqlInsert, connection);  
  SqlParameter tvpParam = insertCommand.Parameters.AddWithValue("@tvpNewCategories", addedCategories);  
  tvpParam.SqlDbType = SqlDbType.Structured;  
  tvpParam.TypeName = "dbo.CategoryTableType";  

  // Execute the command.  
  insertCommand.ExecuteNonQuery();  
}  
```  
  
```vb  
' Assumes connection is an open SqlConnection.  
Using connection  
  ' Create a DataTable with the modified rows.  
  Dim addedCategories As DataTable = _  
    CategoriesDataTable.GetChanges(DataRowState.Added)  
  
  ' Define the INSERT-SELECT statement.  
  Dim sqlInsert As String = _  
  "INSERT INTO dbo.Categories (CategoryID, CategoryName)" _  
  & " SELECT nc.CategoryID, nc.CategoryName" _  
  & " FROM @tvpNewCategories AS nc;"  
  
  ' Configure the command and parameter.  
  Dim insertCommand As New SqlCommand(sqlInsert, connection)  
  Dim tvpParam As SqlParameter = _  
     insertCommand.Parameters.AddWithValue( _  
    "@tvpNewCategories", addedCategories)  
  tvpParam.SqlDbType = SqlDbType.Structured  
  tvpParam.TypeName = "dbo.CategoryTableType"  
  
  ' Execute the query  
  insertCommand.ExecuteNonQuery()  
End Using  
```  
  
## <a name="streaming-rows-with-a-datareader"></a>使用 DataReader 对行进行流处理  
 您也可以使用从 <xref:System.Data.Common.DbDataReader> 中派生的任何对象，将数据行流处理到表值参数。 下面的代码段演示如何使用 <xref:System.Data.OracleClient.OracleCommand> 和 <xref:System.Data.OracleClient.OracleDataReader> 来检索 Oracle 数据库中的数据。 然后，示例代码配置 <xref:System.Data.SqlClient.SqlCommand> 以使用单个输入参数调用存储过程。 <xref:System.Data.SqlClient.SqlParameter.SqlDbType%2A> 的 <xref:System.Data.SqlClient.SqlParameter> 属性设置为 `Structured`。 <xref:System.Data.SqlClient.SqlParameterCollection.AddWithValue%2A> 将 `OracleDataReader` 结果集作为表值参数传递给存储过程。  
  
```csharp  
// Assumes connection is an open SqlConnection.  
// Retrieve data from Oracle.  
OracleCommand selectCommand = new OracleCommand(  
   "Select CategoryID, CategoryName FROM Categories;",  
   oracleConnection);  
OracleDataReader oracleReader = selectCommand.ExecuteReader(  
   CommandBehavior.CloseConnection);  
  
 // Configure the SqlCommand and table-valued parameter.  
 SqlCommand insertCommand = new SqlCommand(  
   "usp_InsertCategories", connection);  
 insertCommand.CommandType = CommandType.StoredProcedure;  
 SqlParameter tvpParam =  
    insertCommand.Parameters.AddWithValue(  
    "@tvpNewCategories", oracleReader);  
 tvpParam.SqlDbType = SqlDbType.Structured;  
  
 // Execute the command.  
 insertCommand.ExecuteNonQuery();  
```  
  
```vb  
' Assumes connection is an open SqlConnection.  
' Retrieve data from Oracle.  
Dim selectCommand As New OracleCommand( _  
  "Select CategoryID, CategoryName FROM Categories;", _  
  oracleConnection)  
Dim oracleReader As OracleDataReader = _  
  selectCommand.ExecuteReader(CommandBehavior.CloseConnection)  
  
' Configure SqlCommand and table-valued parameter.  
Dim insertCommand As New SqlCommand("usp_InsertCategories", connection)  
insertCommand.CommandType = CommandType.StoredProcedure  
Dim tvpParam As SqlParameter = _  
  insertCommand.Parameters.AddWithValue("@tvpNewCategories", _  
  oracleReader)  
tvpParam.SqlDbType = SqlDbType.Structured  
  
' Execute the command.  
insertCommand.ExecuteNonQuery()  
```  
  
## <a name="see-also"></a>请参阅

- [配置参数和参数数据类型](../../../../../docs/framework/data/adonet/configuring-parameters-and-parameter-data-types.md)
- [命令和参数](../../../../../docs/framework/data/adonet/commands-and-parameters.md)
- [DataAdapter 参数](../../../../../docs/framework/data/adonet/dataadapter-parameters.md)
- [ADO.NET 中的 SQL Server 数据操作](../../../../../docs/framework/data/adonet/sql/sql-server-data-operations.md)
- [ADO.NET 托管提供程序和数据集开发人员中心](https://go.microsoft.com/fwlink/?LinkId=217917)
