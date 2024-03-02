## Connection String
It is what I will use in order to connect the database to the models

## Let's create a new database
1. Connect to your SSMS
2. Copy the name of your server, mine is "DESKTOP-CDTM6JF"
3. Go to `appsettings.json` file to initialize your connection string properties like I did below
    ```json
    "ConnectionStrings": {
        "LocalConection": "Server=DESKTOP-CDTM6JF; Database=CategoryDb; Trusted_Connection=True; TrustServerCertificate=True"
    }
    ```
4. Now that we have the connection string, now we need to install EF Core package by using the Nuget packages
    * Microsoft.EntityFrameworkCore
    * Microsoft.EntityFrameworkCore.SqlServer
    * Microsoft.EntityFrameworkCore.Tools

5. Install EF Core package by using the package manager console:
    * PM> install-package Microsoft.EntityFrameworkCore
    * PM> install-package Microsoft.EntityFrameworkCore.SqlServer
    * PM> install-package Microsoft.EntityFrameworkCore.Tools

6. Created a new Foldercalled "Data" in my project
    * Inside, create a class called "applicationDbContext.cs". Here I will perform basic configuration for EF Core.
    * Your class must implement the `DbContext` class (don't forget to add `using Microsoft.EntityFrameworkCore;` at the top).
    * `DbContext` is the root class of EF Core that we will be using to access EF Core features.
    * Inside the class, we must create a constructor that will implement from the base class (which is `DbContext` class):
        ```cs
        public ApplicationDbContext() : base()
        {

        }
        ```
    * We have to pass our connection string we have on our appsettings.json file to the base class `DbContext`.
    * We will do that when we inject the `AppicationDbContext` we will get the connection string as a parameter inside the constructor as `DbContextOptions`.
    * That parameter we will pass it on to the base class as we can see fron the above constructor. Let's complete our constructor code:
        ```cs
        public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options) : base(options)
        {

        }
        ```
    * Now what we need to do is inject the `DbContext` in order to link the connection string. That will be done in the `Program.cs` file:
        ```cs
        builder.Services.AddDbContext<ApplicationDbContext>();
        ```
    * Now that we have injected `DbContext` in our application, let us link the connection string. We do that by configuring some `options`:
        ```cs
        builder.Services.AddDbContext<ApplicationDbContext>(options => options.UseSqlServer(
            builder.Configuration.GetConnectionString("LocalConnection")));
        ```
    * Next we have to add the `DbSet<>` which will help create the table
        ```cs
        public DbSet<Category> Categories { get; set; }
        ```

    * The full complete code for the `ApplicationDbContext` class:
        ```cs
        using eCommerseApp.Models;
        using Microsoft.EntityFrameworkCore;

        namespace eCommerseApp.Data 
        {
            public class ApplicationDbContext : DbContext
            {
                public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options) : base (options)
                {

                }

                public DbSet<Category> Categories { get; set; }
            }
        }
        ```

7. Create the database
    * Open the Package Manager Console and type the commands:
    * add-migration "First Migrations"    (This is for keep track of migration history)
    * update-database  (this is for creating yor database using EF Core)
    * After the commands execute successfully, you should be able to see your database on Sql Server as below:
    
    ![pic](https://dev.azure.com/minenhlenkosi/a8e904a0-ca8c-4ee6-9bb8-acf45666f7c3/_apis/git/repositories/ea2d8e4f-4bb3-46c9-85b8-59c1cd082958/items?path=/eCommerse/eCommerseApp/Notes/6.%20Connection%20String/Images/2.png&versionDescriptor%5BversionOptions%5D=0&versionDescriptor%5BversionType%5D=0&versionDescriptor%5Bversion%5D=master&resolveLfs=true&%24format=octetStream&api-version=5.0)