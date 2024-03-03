# Category Controller
This controller we want to use for performing CRUD operations, which is to say we want to be able to **create** a category, **update** a category, **read** a category, **delete** a category.

## Create Category Controller
1. On the Controller folder, right click on it and select *add*

    <kbd>
      <img src="https://github.com/MinenhleNkosi/ASP.NET_Core_Web_API/blob/main/eCommerse/eCommerseApp/Notes/7.%20Category%20Controller/Images/11.png?raw=true" height="auto" width="600" />
    </kbd>

2. The select *controller*, select *MVC Controller - Empty*

    <kbd>
      <img src="https://github.com/MinenhleNkosi/ASP.NET_Core_Web_API/blob/main/eCommerse/eCommerseApp/Notes/7.%20Category%20Controller/Images/2.png?raw=true" height="auto" width="600" />
    </kbd>

3. Name the controller as `CategoryController.cs`and then press *Add* (when you create a controller the *controller* keyword must be included at the end).

    <kbd>
      <img src="https://github.com/MinenhleNkosi/ASP.NET_Core_Web_API/blob/main/eCommerse/eCommerseApp/Notes/7.%20Category%20Controller/Images/33.png?raw=true" height="auto" width="600" />
    </kbd>

4. When the controller has been created, it will have the below code:
    ```cs
    using Microsoft.AspNetCore.Mvc;

    namespace eCommerseApp.Controllers
    {
        public class CategoryController : Controller
        {
            public IActionResult Index()
            {
                return View();
            }
        }
    }
    ```
5. Now that we have the controller, we need to create a **View**
6. Inside the **Views** folder we will create a new folder called **Category**.
7. Inside that folder we will add a file called `Index.cshtml`

    <kbd>
      <img src="https://github.com/MinenhleNkosi/ASP.NET_Core_Web_API/blob/main/eCommerse/eCommerseApp/Notes/7.%20Category%20Controller/Images/44.png?raw=true" height="auto" width="600" />
    </kbd>
    
    -----------------
    <kbd>
      <img src="https://github.com/MinenhleNkosi/ASP.NET_Core_Web_API/blob/main/eCommerse/eCommerseApp/Notes/7.%20Category%20Controller/Images/55.png?raw=true" height="auto" width="600" />
    </kbd>

    <kbd>
      <img src="https://github.com/MinenhleNkosi/ASP.NET_Core_Web_API/blob/main/eCommerse/eCommerseApp/Notes/2.%20MVC%20Architecture/Images/1.png?raw=true" height="auto" width="600" />
    </kbd>
    (image66)

## Add Category Link in Header
To be able to add category link in header we will have to make use of the `_Layout.cshtml` file.
Add the below code to the *header* tag:
```html
<li class="nav-item">
    <a class="nav-link text-dark" asp-area="" asp-controller="Category" asp-action="Index">Category </a>
</li>
```
Then the Category link on the nav bar will appear as shown below:

<kbd>
  <img src="https://github.com/MinenhleNkosi/ASP.NET_Core_Web_API/blob/main/eCommerse/eCommerseApp/Notes/2.%20MVC%20Architecture/Images/1.png?raw=true" height="auto" width="600" />
</kbd>
(image7)

<br />

# CRUD Operations
<h2>Seed Data to the Database (Create)</h2>

Seeding data to our database is basically explicitly adding data to the database using the `OnModelCreating()` method.
1. Open the `ApplicationDbContext` class and add the below code:
    ```cs
    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        modelBuilder.Entity<Category>().HasData(
            new Category { Id = 1, Name = "Action", DisplayOrder = 1},
            new Category { Id = 2, Name = "SciFi", DisplayOrder = 2 },
            new Category { Id = 3, Name = "History", DisplayOrder = 3 }
            );
    }
    ```
2. Next, we add migration by using the below command:
add-migration "Give it a unique phrase or name"
3. After that we update the databse using the below command:
update-database
4. Your database will have new data in the database table:

    <kbd>
      <img src="https://github.com/MinenhleNkosi/ASP.NET_Core_Web_API/blob/main/eCommerse/eCommerseApp/Notes/2.%20MVC%20Architecture/Images/1.png?raw=true" height="auto" width="600" />
    </kbd>
    (image8)


## Get all Categories (Read)
Now what we want to do is to retrieve the category data from the database and display them in the category view (UI).

1. First we have to retrieve the data from our controller.
    * In **.NET Core** what happens is that, when you add something to the services container in the `Program.cs` file. That service is added to **dependency injection**:
        ```cs
        builder.Services.AddDbContext<ApplicationDbContext>(options => options.UseSqlServer(
            builder.Configuration.GetConnectionString("LocalConnection")));
        ```
    * On the above code, I have told the **.NET Core** application that whenever someone needs an implementation of `ApplicationDbContext` this is the configuration to use. So the **Dependency Injection** container will create an object and provide it to use for accessing the database.
    * So on our controller we will directly tell the application that we want an implementation of `ApplicationDbContext` since it is already registered as a service in the DI container. The code below demonstrates how to achieve that:
        ```cs
        public class CategoryController : Controller
        {
            private readonly ApplicationDbContext _db;
            public CategoryController(ApplicatinDbContext db)
            {
                _db = db;
            }
        }
        ```

2. Then pass it over the view to dispaly all the categories.
    * First we will have to use object `_db` to access the database and get all the `Categories` and store them in a list:
        ```cs
        var objCategory = _db.Category.ToList();
        ``` 

3. The code base to get all the categories using the controller is found below:
    ```cs
    public class CategoryController : Controller
        {
            private readonly ApplicationDbContext _db;
            public CategoryController(ApplicatinDbContext db)
            {
                _db = db;
            }

            public IActionResult Index()
            {
                List<Category> objCategory = _db.Categories.ToList();
                return View(objCategory);
            }
        }
    ```
