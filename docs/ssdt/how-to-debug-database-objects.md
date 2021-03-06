---
title: "How to: Debug Database Objects | Microsoft Docs"
ms.custom: 
  - "SSDT"
ms.date: "02/09/2017"
ms.prod: "sql"
ms.technology: ssdt
ms.reviewer: ""
ms.topic: conceptual
ms.assetid: f5d4584f-e85f-4558-b056-83681c365978
author: "stevestein"
ms.author: "sstein"
manager: "craigg"
---
# How to: Debug Database Objects
A SQL Server unit test consists of the following:  
  
-   Unit test code written in in Visual C\# or Visual Basic. This code, which is generated by the SQL Server Unit Test Designer, is responsible for submitting the Transact\-SQL script that forms the body of the test.  
  
-   One or more test conditions, which are written in Visual C\# or Visual Basic. To debug test conditions, follow the procedure for debugging a unit test as described in [How to: Debug while a Test Is Running (Visual Studio 2010)](http://msdn.microsoft.com/library/ms182484(VS.100).aspx) or [How to: Debug while a Test Is Running (Visual Studio 2012)](http://msdn.microsoft.com/library/ms182484.aspx).  
  
-   One or more Transact\-SQL scripts that run on objects in the database that you are testing. You cannot debug these Transact\-SQL scripts.  
  
The procedures in this topic describe how to debug particular database objects, such as stored procedures, functions, and triggers in the database you are testing. To debug a database object, follow these procedures in this order:  
  
1.  Enable SQL Server debugging on your test project.  
  
2.  Enable application debugging on the SQL Server instance that hosts the database you are testing.  
  
3.  Set breakpoints in the Transact\-SQL script of the database object(s) you are debugging.  
  
4.  Debug your unit test. In this procedure, you run the test in debug mode.  
  
### To enable SQL Debugging on your test project  
  
1.  Open **Solution Explorer**.  
  
2.  In **Solution Explorer**, right-click the test project, and click **Properties**.  
  
    A properties page that has the same name as the test project opens.  
  
3.  On the properties page, click **Debug**.  
  
4.  Under **Enable Debuggers**, click **Enable SQL Server debugging**.  
  
5.  Save your changes.  
  
### To set an increased execution context timeout to enable debugging for your test project  
  
1.  On the **File** menu, point to **Open**, and click **File**.  
  
2.  Browse to the folder that contains your test project, and double-click the app.config file.  
  
    The app.config file opens in the editor.  
  
3.  Modify the ExecutionContext node to add a command timeout, as in the following example:  
  
    ```  
    <ExecutionContext CommandTimeout ="300" Provider="System.Data.SqlClient" ConnectionString="Data Source=TargetServerName\TargetInstanceName;Initial Catalog=TargetDatabaseName;Integrated Security=True;Pooling=False" />  
    ```  
  
4.  Save your changes.  
  
5.  Rebuild your unit test project.  
  
> [!IMPORTANT]  
> If you do not rebuild your project, the changes that you made to app.config will not be applied when you run your unit tests, and debugging will fail.  
  
### To add breakpoints to your Transact\-SQL script  
  
1.  On the **View** menu, open **SQL Server Object Explorer**.  
  
2.  Under **Data Connections**, expand the node of the database that you want to test.  
  
3.  If a small red 'x' appears next to the icon of the database, the connection to the database is closed. In this case, right-click the database, and click **Refresh**. You might have to supply credentials to open the connection to the database.  
  
4.  Expand the **Views**, **Stored Procedures**, or **Functions** node to find the object that you want to debug.  
  
5.  Double-click the object that you want to debug.  
  
6.  Click the gray sidebar to set a breakpoint.  
  
### To debug your SQL Server unit test  
  
1.  Visual Studio 2010, open the (Test -> Windows) **Test View** window. In Visual Studio 2012, open the **Test Explorer** window.  
  
2.  Right click the test whose Transact\-SQL script exercises the database object in which you set breakpoints and select **Debug Selection**.  
  
    The test runs in debug mode until a breakpoint in the database object is encountered.  
  
3.  (Optional) To open another debug window, open the **Debug** menu, point to **Windows**, and click **Breakpoints**, **Output**, or **Immediate**.  
  
## See Also  
[Running SQL Server Unit Tests](../ssdt/running-sql-server-unit-tests.md)  
[Debugging Transact-SQL (Visual Studio 2010)](http://go.microsoft.com/fwlink/?LinkId=163975)  
  
