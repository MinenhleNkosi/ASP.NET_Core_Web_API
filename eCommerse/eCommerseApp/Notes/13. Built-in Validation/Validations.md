# Validation 🔐
Right when we are creating a new *category/genre*, we assume that it'll get created. Ask yourself how are we to know if:
1. The user does not input any details (leaving the Name and display order inpts empty)?
2. If the user tries to enter a negative number on the *display order* input?
3. If the user tries to enter special characters as *name* of the genre.
4. How many characters are allowed for the *name* of the genre.

The above tests mentioned are just a few of many ways to test if your application can pass all scenarios.
To solve the issue with user inputs, we have to make use of **validations**.

## Server Side validation
Are built-in methods used to check if input data passed in as parameters is of valid standards.
Let's check out some few server side validations we added
1. On the `Category.cs` model:
    ```cs
        public class Category
    {
        [Key]
        public int Id { get; set; }

        [Required]
        [DisplayName("Category Name")]
        [maxLength(30)]
        public string Name { get; set; }

        [DisplayName("Display Order")]
        [Range(1, 100)]
        public int DisplayOrder { get; set; }
    }
    ```

    From the above code:
    * `[Key]`: data annotation used to explicitly specify the `Id` for that model. Even if we written `Id` as anything like `sgdsgdhvs`, as long as we have `[Key]` then `sgdsgdhvs` will be taken as the `Id` of that model.
    * `[Required]`: It is there to make sure that the user doesn't leave this part empty.
    * `[DisplayName("Category Name")]`: data annotation used override the property variable (in this case it's Name) with the desired value as a placeholder (in this case which is Category Name).
    * `[maxLength(30)]`: represents the maximum number a **Name** can be, which is 30 characters.
    * `[Range(1, 100)]`: Used to select the required number of characters allowed for that value (in this case is the Display order), `1` represents the minimum number and 100 represents the maximum number allowed.

2. Validating on the controller:
    ```cs
    [HttpPost]
    public IActionResult CreateMethod(Category obj)
    {
        if (ModelState.IsValid)
        {
            _db.Categories.Add(obj);
            _db.SaveChanges();
        }
        return RedirectToAction("Index");
    }
    ```

    From the above code:
    * `ModelState.IsValid`: is used to check is our model (which is `Category.cs` and gets passed as `obj`) is valid or not. to check the validation, `obj` will be taken to the `Category.cs` model and check if each value from `obj` satisfies the data annotations for each property variables in `Category.cs` model. If the validation is *true* then the process continues but if the validation is *false* then an error will be thrown.

## Set-Back on server side validation (ModelState.IsValid)
1. If we intentionally leave the *category name* and click the **Create** button, we will get taken to the `Index.cshtml` page but the new category won't get created thus will not appear on the `Index.cshtml`. Likewise if we do it for the *display order* input.

2. What happens on the background (let's say we leave the *category name* input empty) is, when you click the **Create** button:
    * The UI will pass the user inputs to the controller using **Tag Helpers** (`asp-controller=""` & `asp-action=""` super useful neh 💪🏿🤣😂) and reach the action method (which in our case it'll be `CreateMethod()`).
    * User input will get passed to the action `CreateMethod()` and get passed as `obj` parameter object.
    * The `obj` will go through the `MoodelState.IsValid` built-in method, then the `MoodelState.IsValid` will take the `obj` parameter object and compare it with the `Category.cs` model.
    * The `obj` will fail (since there is `[Required]`) for the data annotations `Name` property since we left the *category name* blank (intentionally) in `obj` ❌.
    * If we place a break-point on the `if (ModelState.IsValid){}` statement (not forgetting that we left the *category name* empty), then click the **Create** button. We will be able to debug and see that there is an error captured on the server side that is causing the *category* to not get created.
        1. Hover over `ModelState`:

            <kbd>
              <img src="https://github.com/MinenhleNkosi/ASP.NET_Core_Web_API/blob/main/eCommerse/eCommerseApp/Notes/12.%20Adding%20New%20Category/Images/1.png?raw=true" height="auto" width="1000" />
            </kbd>
            <hr>
        
        2. Open **Result Review** at the bottom:

            <kbd>
              <img src="https://github.com/MinenhleNkosi/ASP.NET_Core_Web_API/blob/main/eCommerse/eCommerseApp/Notes/12.%20Adding%20New%20Category/Images/1.png?raw=true" height="auto" width="1000" />
            </kbd>
            <hr>

        3. Open **[1]** at the bottom:

            <kbd>
              <img src="https://github.com/MinenhleNkosi/ASP.NET_Core_Web_API/blob/main/eCommerse/eCommerseApp/Notes/12.%20Adding%20New%20Category/Images/1.png?raw=true" height="auto" width="1000" />
            </kbd>
            <hr>

        4. Open **Errors** then **[0]**:

            <kbd>
              <img src="https://github.com/MinenhleNkosi/ASP.NET_Core_Web_API/blob/main/eCommerse/eCommerseApp/Notes/12.%20Adding%20New%20Category/Images/1.png?raw=true" height="auto" width="1000" />
            </kbd>
            <hr>

        From here we can see that the error is **The field display order must be between 1 and 100**

    * If `obj` is valid for all data annotation then the category would get created and appear on the `Index.cshtml` page ✅.

3. As long as any of the user inputs violates the data annotations on the `Category.cs` model, that *category* will not get created. The user will not know why the *category* is not created.

Right now if we insert invalid inputs on the **client side**, we will get an error on the **server side**. Now we need to make sure that the user get's to see that error on the **server side**.

To achieve that we will make use of modifying the `CategoryController.cs` code on the `CreateMethod()` action method.
Current code:
```cs
[HttpPost]
public IActionResult CreateMethod(Category obj)
{
    if (ModelState.IsValid)
    {
        _db.Categories.Add(obj);
        _db.SaveChanges();
    }
    return RedirectToAction("Index");
}
```

Modified code:
```cs
[HttpPost]
public IActionResult CreateMethod(Category obj)
{
    if (ModelState.IsValid)
    {
        _db.Categories.Add(obj);
        _db.SaveChanges();
        return RedirectToAction("Index");
    }
    return View();
}
```

On the above code, the changes that were made are:
1. If validation is true, then save changes to the database and go to the *home* page.
    ```cs
    _db.Categories.Add(obj);
    _db.SaveChanges();
    return RedirectToAction("Index");
    ```

2. If the validation is false, then stay on that view:
    ```cs
    return View();
    ```
Now we are able to stay on the page that has an error 😁, now all we need to do is to display the error message on the **client side** that we get on the **server side**.
To achieve that we will use **Tag Helpers** 😎, by making use of `asp-validation-for`.
* `asp-validation-for`: will evaluate everything againsthe current model, just like how `ModelState.IsValid` does on the **server side**.

After adding the `asp-validation-for` for the *category name* and the *display order*, the code will be like below:
```cshtml
    <div class="mb-3 row">
        <div class="form-group">
            <label class="col-form-label p-0" for="inputDefault">Name</label>
            <input asp-for="Name" class="form-control" placeholder="Enter Category" id="inputDefault">
            <span asp-validation-for="Name" class="text-danger"></span>
        </div>
    </div>
    <div class="mb-3 row">
        <div class="form-group">
            <label class="col-form-label p-0" for="inputDefault">Display Order</label>
            <input asp-for="DisplayOrder" class="form-control" placeholder="Enter Display Order Number" id="inputDefault">
            <span asp-validation-for="DisplayOrder" class="text-danger"></span>
        </div>
    </div>
```

## Displaying server-side error messages to the clint-side
Now let's leave the *category name* then click the **Create** button and see if we do get to see **server side** error on the **client side**:

<kbd>
  <img src="https://github.com/MinenhleNkosi/ASP.NET_Core_Web_API/blob/main/eCommerse/eCommerseApp/Notes/12.%20Adding%20New%20Category/Images/1.png?raw=true" height="auto" width="1000" />
</kbd>
<hr>

Now let's leave the *display order* blank then click the **Create** button and see if we do get to see **server side** error on the **client side**:

<kbd>
  <img src="https://github.com/MinenhleNkosi/ASP.NET_Core_Web_API/blob/main/eCommerse/eCommerseApp/Notes/12.%20Adding%20New%20Category/Images/1.png?raw=true" height="auto" width="1000" />
</kbd>
<hr>

Now let's leave the *category name* and the *display order* blank then click the **Create** button and see if we do get to see **server side** errors on the **client side**:

<kbd>
  <img src="https://github.com/MinenhleNkosi/ASP.NET_Core_Web_API/blob/main/eCommerse/eCommerseApp/Notes/12.%20Adding%20New%20Category/Images/1.png?raw=true" height="auto" width="1000" />
</kbd>
<hr>


Yebo yesss we do get the error messages 🤯😊😉

## Overriding server-side error messages
When to take a closer look to the error message for the *display order* input:

<kbd>
  <img src="https://github.com/MinenhleNkosi/ASP.NET_Core_Web_API/blob/main/eCommerse/eCommerseApp/Notes/12.%20Adding%20New%20Category/Images/1.png?raw=true" height="auto" width="1000" />
</kbd>
<hr>

From the image we can see it says `Display Order must be between 1 and 100` while we want it to say `Display Order must be between 1-100`.
We can achieve this by overriding the error message by using **Data Annotation** on the controller at the `CreateMethod()` action for the `DisplayOrder` property:
```cs
[Range(1, 100, ErrorMessage = "Display Order must be between 1-100")]
```

Now after making the above changes to our code, let's run the application and leave the *display order* blank then click the **Create** button and see if we do get to see the overriden **server side** error on the **client side**:

<kbd>
  <img src="https://github.com/MinenhleNkosi/ASP.NET_Core_Web_API/blob/main/eCommerse/eCommerseApp/Notes/12.%20Adding%20New%20Category/Images/1.png?raw=true" height="auto" width="1000" />
</kbd>
<hr>

As we can see from the image above, we get the overriden error message. Iyahlangana mabitsooo 😂😁
