<properties
   pageTitle="Query Azure SQL Data Warehouse (sqlcmd)| Microsoft Azure"
   description="Querying Azure SQL Data Warehouse with the sqlcmd Command-line Utility."
   services="sql-data-warehouse"
   documentationCenter="NA"
   authors="sonyam"
   manager="barbkess"
   editor=""/>

<tags
   ms.service="sql-data-warehouse"
   ms.devlang="NA"
   ms.topic="get-started-article"
   ms.tgt_pltfrm="NA"
   ms.workload="data-services"
   ms.date="09/06/2016"
   ms.author="barbkess;sonyama"/>

# <a name="query-azure-sql-data-warehouse-sqlcmd"></a>Query Azure SQL Data Warehouse (sqlcmd)

> [AZURE.SELECTOR]
- [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
- [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
- [Visual Studio](sql-data-warehouse-query-visual-studio.md)
- [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 

This walkthrough uses the [sqlcmd][] command-line utility to query an Azure SQL Data Warehouse.  

## <a name="1-connect"></a>1. Connect

To get started with [sqlcmd][], open the command prompt and enter **sqlcmd** followed by the connection string for your SQL Data Warehouse database. The connection string requires the following parameters:

+ **Server (-S):** Server in the form `<`Server Name`>`.database.windows.net
+ **Database (-d):** Database name.
+ **Enable Quoted Identifiers (-I):** Quoted identifiers must be enabled to connect to a SQL Data Warehouse instance.

To use SQL Server Authentication, you need to add the username/password parameters:

+ **User (-U):** Server user in the form `<`User`>`
+ **Password (-P):** Password associated with the user.

For example, your connection string might look like the following:

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
```

To use Azure Active Directory Integrated authentication, you need to add the Azure Active Directory parameters:

+ **Azure Active Directory Authentication (-G):** use Azure Active Directory for authentication

For example, your connection string might look like the following:

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -G -I
```

> [AZURE.NOTE] You need to [enable Azure Active Directory Authentication](sql-data-warehouse-authentication.md) to authenticate using Active Directory.

## <a name="2-query"></a>2. Query

After connection, you can issue any supported Transact-SQL statements against the instance.  In this example, queries are submitted in interactive mode.

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
1> SELECT name FROM sys.tables;
2> GO
3> QUIT
```

These next examples show how you can run your queries in batch mode using the -Q option or piping your SQL to sqlcmd.

```sql
sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I -Q "SELECT name FROM sys.tables;"
```

```sql
"SELECT name FROM sys.tables;" | sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I > .\tables.out
```

## <a name="next-steps"></a>Next steps

See [sqlcmd documentation][sqlcmd] for more about details about the options available in sqlcmd.

<!--Image references-->

<!--Article references-->

<!--MSDN references--> 
[sqlcmd]: https://msdn.microsoft.com/library/ms162773.aspx
[Azure portal]: https://portal.azure.com

<!--Other Web references-->