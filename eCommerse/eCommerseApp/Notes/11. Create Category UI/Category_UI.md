# Create Category UI
When we create a new page (the one that will appear when we click "create genre"), we don't directly create a new **view** for it. But instead, we first have to create an **action** method from our *controller* that will be invoked and that **action** method invokation will call the **view**.

So, on the Category controller we add the below action method:
```cs
public IActionResult CreateMethod()
{
    return View();
}
```

## Creating the view page
Navigate to the *views folder* and go to the **Category** folder, from there we will create our *view* and call it `CreateMethod.cshtml`.
Now let's just put in some text to visualize on our *create method page*:
```html
<h1>Wola Bolova!!</h1>
```

Now we can assume that when we click the button "Create Genre" we should get taken to the page and see the **Wola Bolova!!** text right?
But unfortunately there is one piece missing, thus when we click the button "Create Genre" we get taken back to the **Home** page.
1. What we need to do is to go back to the `index.html` file, and go to where we created the button "Create Genre":
    ```cshtml
    <div class="col-6 text-end">
        <a asp-controller="" asp-action="" class="btn btn-primary"><i class="bi bi-plus-circle"></i> Create Genre</a>
    </div>
    ```

2. From the code above we can see that we haven't specified the **controller** name `asp-controller=""` and the **action** name `asp-action=""` thus that's why when we press the "Create Genre" button it displays the **Home** page.
3. Let's fix the code: 
    ```cshtml
        <div class="col-6 text-end">
            <a asp-controller="Category" asp-action="CreateMethod" class="btn btn-primary"><i class="bi bi-plus-circle"></i> Create Genre</a>
        </div>
    ```

    NOTE
    Always write the controller name before the action name so that whenever you face an issue and you will know that actionmethods are always inside the controller which makes it easy to debug

4. Now when we click the "Create Genre" button we do see the text "Wola Boizin!!" which means we can now access the "Create Genre" page.
5. Now let's remove the "Wola boizin!!"text since we wanted to use it for testing:
6. Inside the page we will have:
    * A **form** where the user can input the name of the category and display order.
    * A **button** to submit user inputs.


## Things to focus on when creating a view page
1. First we think of what **model** will handle the user inputs which are the *category name* and the *display order*
2. Looking at the **models** we have, we can easily see that the `Category.cs` model will handle the user inputs since it has **Name** and **DisplayOrder** properties.
3. Now that we know which model we will be using in the "Create Genre" page, let's define it on our page:
    ```cshtml
    @model category
    ```

4. Next we create our form for the user inputs:
    ```cshtml
    <form method="post">
        <div class="border p-3 mt-4">
            <div class="row pb-2">
                <h2 class="text-primary"><i class="bi bi-bag-plus"></i> Create Category </h2>
                <hr />
            </div>
            <div class="mb-3 row">
                <div class="form-group">
                    <label class="col-form-label p-0" for="inputDefault">Name</label>
                    <input class="form-control" placeholder="Enter Category" id="inputDefault">
                </div>
            </div>
            <div class="mb-3 row">
                <div class="form-group">
                    <label class="col-form-label p-0" for="inputDefault">Display Order</label>
                    <input class="form-control" placeholder="Enter Display Order Number" id="inputDefault">
                </div>
            </div>
        </div>
    </form>
    ```

5. Now we add the button:
    ```cshtml
    <form method="post">
        <div class="border p-3 mt-4">
            <div class="row pb-2">
                <h2 class="text-primary"><i class="bi bi-bag-plus"></i> Create Category </h2>
                <hr />
            </div>
            <div class="mb-3 row">
                <div class="form-group">
                    <label class="col-form-label p-0" for="inputDefault">Name</label>
                    <input class="form-control" placeholder="Enter Category" id="inputDefault">
                </div>
            </div>
            <div class="mb-3 row">
                <div class="form-group">
                    <label class="col-form-label p-0" for="inputDefault">Display Order</label>
                    <input class="form-control" placeholder="Enter Display Order Number" id="inputDefault">
                </div>
            </div>
            <div class="row">
                <div class="col-6">
                    <button type="submit" class="btn btn-primary form-control"> Create </button>
                </div>
                <div class="col-6">
                    <a asp-controller="Category" asp-action="Index" class="btn btn-outline-secondary form-control"> Back to Category </a>
                </div>
            </div>
        </div>
    </form>
    ```

## Input TAG Helpers
We will use tag helper to specify which *input value* belongs to which *model property*.
To specify any property inside the view page, we use `asp-for=""`:
```cshtml
<form method="post">
    <div class="border p-3 mt-4">
        <div class="row pb-2">
            <h2 class="text-primary"><i class="bi bi-bag-plus"></i> Create Category </h2>
            <hr />
        </div>
        <div class="mb-3 row">
            <div class="form-group">
                <label class="col-form-label p-0" for="inputDefault">Name</label>
                <input asp-for="Name" class="form-control" placeholder="Enter Category" id="inputDefault">
            </div>
        </div>
        <div class="mb-3 row">
            <div class="form-group">
                <label class="col-form-label p-0" for="inputDefault">Display Order</label>
                <input asp-for="DisplayOrder" class="form-control" placeholder="Enter Display Order Number" id="inputDefault">
            </div>
        </div>
        <div class="row">
            <div class="col-6">
                <button type="submit" asp-controller="Category" asp-action="CreateMethod" class="btn btn-primary form-control"> Create </button>
            </div>
            <div class="col-6">
                <a asp-controller="Category" asp-action="Index" class="btn btn-outline-secondary form-control"> Back to Category </a>
            </div>
        </div>
    </div>
</form>
```

This is the final look for Adding a new category:

<kbd>
  <img src="https://github.com/MinenhleNkosi/ASP.NET_Core_Web_API/blob/main/eCommerse/eCommerseApp/Notes/10.%20Category%20list%20Page%20Design/Images/2.png?raw=true" height="auto" width="1050" />
</kbd>
<hr>

