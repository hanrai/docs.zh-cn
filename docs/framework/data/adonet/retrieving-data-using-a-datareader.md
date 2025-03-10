---
title: 使用 DataReader 检索 ADO 数据
ms.date: 10/29/2018
dev_langs:
- csharp
- vb
ms.assetid: 97afc121-fb8b-465b-bab3-6d844420badb
ms.openlocfilehash: 561ebd7ac6948fa42f73ebb4f1eb97c574e6d7e7
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69963168"
---
# <a name="retrieve-data-using-a-datareader"></a>使用 DataReader 检索数据
若要使用**DataReader**检索数据, 请创建**命令**对象的实例, 然后通过调用**ExecuteReader**来创建**DataReader** , 以从数据源中检索行。 **DataReader**提供了一个未缓冲的数据流, 该数据流允许过程逻辑有效地按顺序处理数据源中的结果。 当检索大量数据时, **DataReader**是一个不错的选择, 因为数据不会缓存在内存中。

下面的示例阐释了如何使用**DataReader**, `reader`其中表示有效的 datareader `command`并表示有效的命令对象。  

```csharp
reader = command.ExecuteReader();  
```

```vb
reader = command.ExecuteReader()
```  

使用**DataReader**方法可从查询结果中获取行。 通过向**DataReader**传递列的名称或序号, 可以访问返回行的每一列。 但是, 为获得最佳性能, **DataReader**提供一系列方法, 使你可以访问其本机数据类型 (**GetDateTime**、 **GetDouble**、 **GetGuid**、 **GetInt32**等) 中的列值。 有关特定于数据访问接口的**datareader**的类型化访问器方法的<xref:System.Data.OleDb.OleDbDataReader>列表<xref:System.Data.SqlClient.SqlDataReader>, 请参阅和。 当您知道基础数据类型时, 使用类型化访问器方法可减少检索列值时所需的类型转换量。  
  
 下面的示例循环访问**DataReader**对象并返回每行中的两列。  
  
 [!code-csharp[DataWorks SqlClient.HasRows#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlClient.HasRows/CS/source.cs#1)]
 [!code-vb[DataWorks SqlClient.HasRows#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlClient.HasRows/VB/source.vb#1)]  
  
## <a name="closing-the-datareader"></a>关闭 DataReader  
 当完成使用**DataReader**对象时, 请始终调用**Close**方法。  
  
 如果你的**命令**包含输出参数或返回值, 则在**DataReader**关闭之前, 这些值将不可用。  
  
 当**datareader**打开时, 该**datareader**以独占方式使用**连接**。 不能对**连接**执行任何命令, 包括创建另一个**datareader**, 直到原始**DataReader**关闭为止。  
  
> [!NOTE]
> 不要对类的**Finalize**方法中的**连接**、 **DataReader**或任何其他托管对象调用**Close**或**Dispose**操作。 在终结器中，仅释放类直接拥有的非托管资源。 如果类不拥有任何非托管资源, 则不要在类定义中包括**Finalize**方法。 有关详细信息, 请参阅[垃圾回收](../../../standard/garbage-collection/index.md)。  
  
## <a name="retrieving-multiple-result-sets-using-nextresult"></a>使用 NextResult 检索多个结果集  
 如果**DataReader**返回多个结果集, 请调用**NextResult**方法以按顺序循环访问结果集。 以下示例显示 <xref:System.Data.SqlClient.SqlDataReader> 如何使用 <xref:System.Data.SqlClient.SqlCommand.ExecuteReader%2A> 方法处理两个 SELECT 语句的结果。  
  
 [!code-csharp[DataWorks SqlClient.NextResult#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlClient.NextResult/CS/source.cs#1)]
 [!code-vb[DataWorks SqlClient.NextResult#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlClient.NextResult/VB/source.vb#1)]  
  
## <a name="getting-schema-information-from-the-datareader"></a>从 DataReader 获取架构信息  
 当**DataReader**打开时, 可以使用**GetSchemaTable**方法检索有关当前结果集的架构信息。 **GetSchemaTable**返回一个<xref:System.Data.DataTable>用行和列填充的对象, 其中包含当前结果集的架构信息。 对于结果集的每一列, **DataTable**都包含一行。 架构表中的每一列都映射到在结果集的行中返回的列的属性, 其中**ColumnName**是属性的名称, 列的值是属性的值。 下面的示例写出**DataReader**的架构信息。  
  
 [!code-csharp[DataWorks SqlClient.GetSchemaTable#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlClient.GetSchemaTable/CS/source.cs#1)]
 [!code-vb[DataWorks SqlClient.GetSchemaTable#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlClient.GetSchemaTable/VB/source.vb#1)]  
  
## <a name="working-with-ole-db-chapters"></a>使用 OLE DB 章节  
 可以使用<xref:System.Data.OleDb.OleDbDataReader>检索分层行集或章节 (OLE DB 类型**DBTYPE_HCHAPTER**、ADO 类型 adChapter)。 当包含某一章节的查询作为**datareader**返回时, 该章节将作为该**datareader**中的列返回, 并作为**datareader**对象公开。  
  
 ADO.NET**数据集**还可用于通过使用表之间的父子关系来表示分层行集。 有关详细信息, 请参阅[数据集、数据表和 dataview](../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)。  
  
 以下代码示例使用 MSDataShape 提供程序来为客户列表中的每个客户生成订单的章节列。  
  
```vb  
Using connection As OleDbConnection = New OleDbConnection(
    "Provider=MSDataShape;Data Provider=SQLOLEDB;" &
    "Data Source=localhost;Integrated Security=SSPI;Initial Catalog=northwind")

    Using custCMD As OleDbCommand = New OleDbCommand(
        "SHAPE {SELECT CustomerID, CompanyName FROM Customers} " &
        "APPEND ({SELECT CustomerID, OrderID FROM Orders} AS CustomerOrders " &
        "RELATE CustomerID TO CustomerID)", connection)

        connection.Open()

        Using custReader As OleDbDataReader = custCMD.ExecuteReader()

            Do While custReader.Read()
                Console.WriteLine("Orders for " & custReader.GetString(1))
                ' custReader.GetString(1) = CompanyName  

                Using orderReader As OleDbDataReader = custReader.GetValue(2)
                    ' custReader.GetValue(2) = Orders chapter as DataReader  

                    Do While orderReader.Read()
                        Console.WriteLine(vbTab & orderReader.GetInt32(1))
                        ' orderReader.GetInt32(1) = OrderID  
                    Loop
                    orderReader.Close()
                End Using
            Loop
            ' Make sure to always close readers and connections.  
            custReader.Close()
        End Using
    End Using
End Using
```  
  
```csharp  
using (OleDbConnection connection = new OleDbConnection(
    "Provider=MSDataShape;Data Provider=SQLOLEDB;" +
    "Data Source=localhost;Integrated Security=SSPI;Initial Catalog=northwind"))
{
    using (OleDbCommand custCMD = new OleDbCommand(
        "SHAPE {SELECT CustomerID, CompanyName FROM Customers} " +
        "APPEND ({SELECT CustomerID, OrderID FROM Orders} AS CustomerOrders " +
        "RELATE CustomerID TO CustomerID)", connection))
    {
        connection.Open();

        using (OleDbDataReader custReader = custCMD.ExecuteReader())
        {

            while (custReader.Read())
            {
                Console.WriteLine("Orders for " + custReader.GetString(1));
                // custReader.GetString(1) = CompanyName  

                using (OleDbDataReader orderReader = (OleDbDataReader)custReader.GetValue(2))
                {
                    // custReader.GetValue(2) = Orders chapter as DataReader  

                    while (orderReader.Read())
                        Console.WriteLine("\t" + orderReader.GetInt32(1));
                    // orderReader.GetInt32(1) = OrderID  
                    orderReader.Close();
                }
            }
            // Make sure to always close readers and connections.  
            custReader.Close();
        }
    }
}
```  
  
## <a name="returning-results-with-oracle-ref-cursors"></a>用 Oracle REF cursor 返回结果  
 Oracle .NET Framework 数据提供程序支持使用 Oracle REF CURSOR 返回查询结果。 Oracle REF CURSOR 以 <xref:System.Data.OracleClient.OracleDataReader> 的形式返回。  
  
 您可以<xref:System.Data.OracleClient.OracleDataReader> <xref:System.Data.OracleClient.OracleCommand.ExecuteReader%2A>使用方法检索表示 Oracle REF CURSOR 的对象。 还可以指定<xref:System.Data.OracleClient.OracleCommand>返回一个或多个 Oracle REF cursor 的, <xref:System.Data.OracleClient.OracleDataAdapter>作为用于填充<xref:System.Data.DataSet>的的**SelectCommand** 。  
  
 若要访问从 Oracle 数据源返回的 REF CURSOR, 请<xref:System.Data.OracleClient.OracleCommand>为查询创建, 并将引用该引用光标的 output 参数添加<xref:System.Data.OracleClient.OracleCommand.Parameters>到的集合<xref:System.Data.OracleClient.OracleCommand>中。 该参数的名称必须与查询中的 REF CURSOR 参数名称相匹配。 将参数的类型设置为<xref:System.Data.OracleClient.OracleType.Cursor?displayProperty=nameWithType>。 的方法为 REF CURSOR <xref:System.Data.OracleClient.OracleDataReader>返回一个。 <xref:System.Data.OracleClient.OracleCommand> <xref:System.Data.OracleClient.OracleCommand.ExecuteReader?displayProperty=nameWithType>  
  
 <xref:System.Data.OracleClient.OracleCommand>如果返回多个 REF 游标, 请添加多个输出参数。 可以通过调用<xref:System.Data.OracleClient.OracleCommand.ExecuteReader?displayProperty=nameWithType>方法来访问不同的 REF cursor。 对<xref:System.Data.OracleClient.OracleCommand.ExecuteReader>的调用将<xref:System.Data.OracleClient.OracleDataReader>返回引用第一个引用游标的。 然后, 可以调用<xref:System.Data.OracleClient.OracleDataReader.NextResult?displayProperty=nameWithType>方法来访问后续的 REF cursor。 尽管<xref:System.Data.OracleClient.OracleCommand.Parameters?displayProperty=nameWithType>集合中的参数与 REF CURSOR 输出参数按名称匹配<xref:System.Data.OracleClient.OracleDataReader> , 但<xref:System.Data.OracleClient.OracleCommand.Parameters>会按照它们添加到集合中的顺序来访问这些参数。  
  
 例如，请看下面这个 Oracle 包和包正文。  
  
```sql
CREATE OR REPLACE PACKAGE CURSPKG AS   
  TYPE T_CURSOR IS REF CURSOR;   
  PROCEDURE OPEN_TWO_CURSORS (EMPCURSOR OUT T_CURSOR,   
    DEPTCURSOR OUT T_CURSOR);   
END CURSPKG;  
  
CREATE OR REPLACE PACKAGE BODY CURSPKG AS   
  PROCEDURE OPEN_TWO_CURSORS (EMPCURSOR OUT T_CURSOR,   
    DEPTCURSOR OUT T_CURSOR)   
  IS   
  BEGIN   
    OPEN EMPCURSOR FOR SELECT * FROM DEMO.EMPLOYEE;   
    OPEN DEPTCURSOR FOR SELECT * FROM DEMO.DEPARTMENT;   
  END OPEN_TWO_CURSORS;   
END CURSPKG;   
```  
  
 下面的代码创建一个<xref:System.Data.OracleClient.OracleCommand> , 它通过将类型<xref:System.Data.OracleClient.OracleType.Cursor?displayProperty=nameWithType>的两个参数添加到<xref:System.Data.OracleClient.OracleCommand.Parameters?displayProperty=nameWithType>集合中, 从以前的 Oracle 包返回 REF cursor。  
  
```vb  
Dim cursCmd As OracleCommand = New OracleCommand("CURSPKG.OPEN_TWO_CURSORS", oraConn)  
cursCmd.Parameters.Add("EMPCURSOR", OracleType.Cursor).Direction = ParameterDirection.Output  
cursCmd.Parameters.Add("DEPTCURSOR", OracleType.Cursor).Direction = ParameterDirection.Output  
```  
  
```csharp  
OracleCommand cursCmd = new OracleCommand("CURSPKG.OPEN_TWO_CURSORS", oraConn);  
cursCmd.Parameters.Add("EMPCURSOR", OracleType.Cursor).Direction = ParameterDirection.Output;  
cursCmd.Parameters.Add("DEPTCURSOR", OracleType.Cursor).Direction = ParameterDirection.Output;  
```  
  
 下面的代码使用<xref:System.Data.OracleClient.OracleDataReader.Read>的和<xref:System.Data.OracleClient.OracleDataReader.NextResult>方法<xref:System.Data.OracleClient.OracleDataReader>返回前一个命令的结果。 REF CURSOR 参数按顺序返回。  
  
```vb  
oraConn.Open()  
  
Dim cursCmd As OracleCommand = New OracleCommand("CURSPKG.OPEN_TWO_CURSORS", oraConn)  
cursCmd.CommandType = CommandType.StoredProcedure  
cursCmd.Parameters.Add("EMPCURSOR", OracleType.Cursor).Direction = ParameterDirection.Output  
cursCmd.Parameters.Add("DEPTCURSOR", OracleType.Cursor).Direction = ParameterDirection.Output  
  
Dim reader As OracleDataReader = cursCmd.ExecuteReader()  
  
Console.WriteLine(vbCrLf & "Emp ID" & vbTab & "Name")  
  
Do While reader.Read()  
  Console.WriteLine("{0}" & vbTab & "{1}, {2}", reader.GetOracleNumber(0), reader.GetString(1), reader.GetString(2))  
Loop  
  
reader.NextResult()  
  
Console.WriteLine(vbCrLf & "Dept ID" & vbTab & "Name")  
  
Do While reader.Read()  
  Console.WriteLine("{0}" & vbTab & "{1}", reader.GetOracleNumber(0), reader.GetString(1))  
Loop  
' Make sure to always close readers and connections.  
reader.Close()  
oraConn.Close()  
```  
  
```csharp  
oraConn.Open();  
  
OracleCommand cursCmd = new OracleCommand("CURSPKG.OPEN_TWO_CURSORS", oraConn);  
cursCmd.CommandType = CommandType.StoredProcedure;  
cursCmd.Parameters.Add("EMPCURSOR", OracleType.Cursor).Direction = ParameterDirection.Output;  
cursCmd.Parameters.Add("DEPTCURSOR", OracleType.Cursor).Direction = ParameterDirection.Output;  
  
OracleDataReader reader = cursCmd.ExecuteReader();  
  
Console.WriteLine("\nEmp ID\tName");  
  
while (reader.Read())  
  Console.WriteLine("{0}\t{1}, {2}", reader.GetOracleNumber(0), reader.GetString(1), reader.GetString(2));  
  
reader.NextResult();  
  
Console.WriteLine("\nDept ID\tName");  
  
while (reader.Read())  
  Console.WriteLine("{0}\t{1}", reader.GetOracleNumber(0), reader.GetString(1));  
// Make sure to always close readers and connections.  
reader.Close();  
oraConn.Close();  
```  
  
 下面的示例使用上一个命令, <xref:System.Data.DataSet>用 Oracle 包的结果填充。  
  
```vb  
Dim ds As DataSet = New DataSet()  
  
Dim adapter As OracleDataAdapter = New OracleDataAdapter(cursCmd)  
adapter.TableMappings.Add("Table", "Employees")  
adapter.TableMappings.Add("Table1", "Departments")  
  
adapter.Fill(ds)  
```  
  
```csharp  
DataSet ds = new DataSet();  
  
OracleDataAdapter adapter = new OracleDataAdapter(cursCmd);  
adapter.TableMappings.Add("Table", "Employees");  
adapter.TableMappings.Add("Table1", "Departments");  
  
adapter.Fill(ds);  
```

> [!NOTE]
> 为了避免**OverflowException**, 我们建议你还在将<xref:System.Data.DataRow>值存储在中之前, 先处理从 Oracle NUMBER 类型到有效 .NET Framework 类型的任何转换。 您可以使用<xref:System.Data.Common.DataAdapter.FillError>事件来确定是否发生了**OverflowException** 。 有关<xref:System.Data.Common.DataAdapter.FillError>事件的详细信息, 请参阅[处理 DataAdapter 事件](../../../../docs/framework/data/adonet/handling-dataadapter-events.md)。  
  
## <a name="see-also"></a>请参阅

- [DataAdapters 和 DataReaders](../../../../docs/framework/data/adonet/dataadapters-and-datareaders.md)
- [命令和参数](../../../../docs/framework/data/adonet/commands-and-parameters.md)
- [检索数据库架构信息](../../../../docs/framework/data/adonet/retrieving-database-schema-information.md)
- [ADO.NET 托管提供程序和数据集开发人员中心](https://go.microsoft.com/fwlink/?LinkId=217917)
