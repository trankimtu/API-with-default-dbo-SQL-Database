# API-with-default-dbo-SQL-Database

Back-End ASP.NET 6.0<br>
SQL Database


## appsettings.json
This file is used to store configuration settings for the application, such as the connection string for the SQL Server database. The ConnectionStrings section of the file contains the key-value pair for the "DefaultConnection" key, which specifies the connection string for the SQL Server database.

## Program.cs
This file is the entry point for the application. It sets up the web host using the ```CreateHostBuilder``` method and then starts the host. The ```CreateHostBuilder``` method sets up the host configuration by loading the configuration values from the ```appsettings.json``` file. The ```UseStartup``` method is called to configure the services and middleware for the application.

## Model.cs
This file defines the data model for the application. It contains classes that represent the entities in the database, such as ```User``` or ```Product```.

## DataContext.cs
This file is responsible for connecting to the database and providing a way to interact with the data. It inherits from the ```DbContext``` class, which is a part of the Entity Framework Core library. It contains a ```DbSet``` property for each entity in the data model, which allows the application to query and manipulate the data.

## Controller.cs
This file contains the controller logic for the application. It handles incoming HTTP requests, processes them, and returns an HTTP response to the client. It depends on the DataContext class to perform data access operations, such as retrieving data from the database or saving data to the database.

## How these files work together:

When the application starts up, ```Program.cs``` loads the configuration values from the ```appsettings.json``` file.

When a request is made to the application, the routing system routes the request to the appropriate controller action method in ```Controller.cs```.

```Controller.cs``` uses the ```DataContext``` class to interact with the data in the database. It queries the data by calling methods on the ```DbSet``` properties defined in ```DataContext.cs```. It saves data to the database by calling the ```SaveChanges``` method on the ```DataContext``` instance.

```DataContext.cs``` uses the connection string specified in ```appsettings.json``` to connect to the SQL Server database.

```Model.cs``` defines the data model for the application, which is used by ```DataContext.cs``` to map the entities to the database tables.

Overall, these files work together to provide a web application that can handle incoming requests, retrieve and manipulate data from a SQL Server database, and return HTTP responses to the client.







