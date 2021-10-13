# Create C# apps using SQL Server

## Summary

## Estimate Time

## Resources
Microsoft - [Create C# apps using SQL Server on Windows](https://www.microsoft.com/en-us/sql-server/developer-get-started/csharp/win)

## Directions
The directions say:
>In this section, you will get SQL Server 2017 on Windows. After that you will install the necessary dependencies to create .NET Framework apps with SQL Server.

However, these directions will work for a .NET Core Application and using SQL Server 2019.

### Skip instructions for
- Step 1.1 Install SQL Server
  - Read these steps, but you have already installed SQL server on you computer.  Do not reinstall SQL server.
- Step 1.2 Install Visual Studio Community Edition and .NET Framework
 - You already have Visual Studio installed on your machine.  You may skip these steps and move *go to step 2.*

### Step 2.1 Create a C# app that connects to SQL Server and executes queries
The lesson will tell you to copy and paste the code.  Do not copy and paste the code.  Instead learn through rewriting the code into Visual Studio. *It may make sesnse to copy a line or two, but overall writing the code will give you a deeper understanding.*

This lesson relies on the [System.Data.SqlClient.dll](https://docs.microsoft.com/en-us/dotnet/api/system.data.sqlclient.sqldatareader?view=dotnet-plat-ext-5.0) assembly, but does not explain many of the types used.  You may learn more about these classes on MS Docs:
- [SqlConnection](https://docs.microsoft.com/en-us/dotnet/api/system.data.sqlclient.sqlconnection?view=dotnet-plat-ext-5.0)
- [SqlCommand](https://docs.microsoft.com/en-us/dotnet/api/system.data.sqlclient.sqlcommand?view=dotnet-plat-ext-5.0)
- [SqlDataReader](https://docs.microsoft.com/en-us/dotnet/api/system.data.sqlclient.sqldatareader?view=dotnet-plat-ext-5.0)
- [SqlException](https://docs.microsoft.com/en-us/dotnet/api/system.data.sqlclient.sqlexception?view=dotnet-plat-ext-5.0)

As you write the code, note new information including:
- Opening a sql connection with `connection.Open();`
- Managing the release of the resources through the [using](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/using-statement) keyword. `SqlCommand` is an example of a managed type that accesses unmanaged resources.  The using statement guarantees correct releaseing of the resources once no longer needed.
- Selecting the database to add a table too before creating a new table `sb.Append("USE SampleDB; ");`
  - It is a common mistake to accidently add tables to the master database.
- Passing arguments using the sql statement using @"  `"@name"`
- Catching Sql expections and writing them to the console: `catch (SqlException e) { Console.WriteLine(e.ToString()); }`
  - *Expect applicatin to not work initially.  Use the exceptions to help debug.*
- Reading rows returned from the database through `SqlDataReader`:
```csharp
using (SqlDataReader reader = command.ExecuteReader())
{
    while (reader.Read())
    {
        Console.WriteLine("{0} {1} {2}", reader.GetInt32(0), reader.GetString(1), reader.GetString(2));
    }
}
```

Notes:
- You may add new account with a new UserID and password to your sql server through following Adams Wilberts instructions at [Microsoft SQL Server 2019 Essential Training: Create a new user account](https://www.linkedin.com/learning/microsoft-sql-server-2019-essential-training/create-a-new-user-account)
- You likely need to download the packages for `System.Data.SqlClient` to acces the classes `SqlConnectionStringBuilder()` and `SqlConnection`.
- There are several intersting choices made in this example:
  - All the code lives in the Main method
  - The author does not include `connection.Close()`
  - The author enjoys using string builder to create the query strings.  String builder is not required. 
  - The apporaches in this lesson do not represent industry best practices.  

### STOP Do not continue and do not complete the sections: 
- Step 2.2 Create a C# app that connects to SQL Server using the Entity Framework ORM in .NET Framework
- Step 3.1
- Try the mssql extension for Visual Studio Code!