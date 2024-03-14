# The Design for Category List Page
Now we want to add all the appropriate functinalities within the Category page, like:
* A button for adding a new category
* A Title

Let's add those functionality in our `index.cshtml` file:
```cshtml
<div class="row pt-4 pb-1">
    <div class="col-6">
        <h1 class="text-primary">
            CATEGORY LIST
        </h1>
    </div>
    <div class="col-6 text-end">
        <a asp-controller="" asp-action="" class="btn btn-primary"><i class="bi bi-plus-circle"></i> Create Genre</a>
    </div>
</div>
```

Now let's examine the above code:
* `<div class="row pt-4 pb-1">` : We create a **div** which is of a row class
    * `pt-4` : stands for padding-top which is set to `4px`
    * `pb-1` : stands for padding-bottom which is set to `1px`
    * `col-6` : states that this div will have 6 columns under it, thus the word **Category List** will take a 6 column space and the other 6 column space will be taken by the button.
    * `text-end` : states that text will be placed on the far right end of the div.
    * `<i class="bi bi-plus-circle"></i>` : added a *plus-sign* icon for the create genre button.

    
The image below will showcase how the design for the category list page should look like in a grid layout.

<kbd>
  <img src="https://github.com/MinenhleNkosi/ASP.NET_Core_Web_API/blob/main/eCommerse/eCommerseApp/Notes/1.%20Project%20Structure/Images/1.png" height="auto" width="600" />
</kbd>
<hr>

The below image shows how the application looks like when we run it:

<kbd>
  <img src="https://github.com/MinenhleNkosi/ASP.NET_Core_Web_API/blob/main/eCommerse/eCommerseApp/Notes/1.%20Project%20Structure/Images/1.png" height="auto" width="600" />
</kbd>
<hr>


# Design for Create Genre Page
So now when we click the **Create Genre** button, there should be another page where we get to input details of the new genre we wish to add.
* There should be a title
* A container to hold the inputs from the user:
    * Where you enter the name
    * Where you enter the type of genre
* Buttons:
    * A button for creating the new genre.
    * a button for going back to the category page.


Below is the grid layout representation of the **Create Genre** page:

<kbd>
  <img src="https://github.com/MinenhleNkosi/ASP.NET_Core_Web_API/blob/main/eCommerse/eCommerseApp/Notes/1.%20Project%20Structure/Images/1.png" height="auto" width="600" />
</kbd>
<hr>

When we work with creating a new page, we don't directly create a new view page. 
Instead we first have to create an **action** method that will be invoked which in return will call the view.

1. We have to add that **action** method to the category controller:
    ```cshtml
    public IActionResult CreateMethod()
    {
        return View();
    }
    ```

2. Now that we have the **action** method on the controller, we have to now create the view for handling the UI part on the Category view folder.
Inside the `CreateMethod.cshtml` view file, we add just an h1 tag which displays a simple message:
    ```cshtml
    <h1>Wola Boizin!</h1>
    ```

3. Now that we have an action method and a view, it's time to make use of anchor tags in our **Create Genre** button so that when it's clicked it should take us to the create genre page.
Our button right now has the below code:
    ```cshtml
    <a asp-controller="" asp-action="" class="btn btn-primary"><i class="bi bi-plus-circle"></i> Create Genre</a>
    ```

Because of the above code, if we click on the *Create Genre** button, the application will be redirected to the **Home** Page, why?
The reason is we have not specified the `asp-controller=""` and the `asp-action=""`, so by default if no *controller* and *action* method are specified the page redirects to the **Home** page. Which is implemented in the below code at the `program.cs` file:
```cshtml
app.MapControllerRoute(
    name: "default",
    pattern: "{controller=Home}/{action=Index}/{id?}");
```

The code above clearly specifies that by default (if no controller name and action method name have been explicitly specified) the application will redirect to `"{controller=Home}/{action=Index}/{id?}"` when `{id?}` is optional.

4. So now we must add the **controller** name and the **action** method name so that when we click the **Create Genre** button it properly redirects to the create genre page and see the *Wola Boizin* message.
    ```cshtml
    <a asp-controller="Category" asp-action="CreateMethod" class="btn btn-primary"><i class="bi bi-plus-circle"></i> Create Genre</a>
    ```




