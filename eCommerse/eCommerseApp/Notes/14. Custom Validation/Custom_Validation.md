# Custom Validation
Built-in validation use data annotation, but if you need custom validation which is not provided by data annotation like:
* Let's say you want to create a new category/genre and add a validation that "category name" and "display order" cannot be the same.
* To display all validation summary at the top part of your UI

## Match validation:
1. First we have to go to the **controller** used to create new category which is `CreateMethod.cs`.
2. From there we have to have an `if()` statement to check if the "category name" and "display order" are the same:
   ```cs
   if (obj.Name == obj.DisplayOrder.ToString())
   {
   
   }
   ```

3. If the above condition is true, then we will use the `ModelState.AddModelError()`:
    * The `ModelState.AddModelError()` takes in two argument/parameters, the `key` and the `errorMessage`.
    * The `key` will be the `asp-for="Name"` variable `Name` found inside the input tag in the `CreateMethod.cshtml` 
      
         <kbd>
           <img src="https://github.com/MinenhleNkosi/ASP.NET_Core_Web_API/blob/main/eCommerse/eCommerseApp/Notes/14.%20Custom%20Validation/Images/1.png?raw=true" height="auto" width="1000" />
         </kbd>
         <hr>

    * Now we add the `ModelState.AddModelError()`:
       ```cs
       if (obj.Name == obj.DisplayOrder.ToString())
       {
           ModelState.AddModelError("name", "The Name cannot exactly match the Display Order");
       }
       ```


## Validation Summary
For this part we work with the *view* rather than the *controller*
Validation summary groups all the errors that appear on the client-side.
The summary can be added using a `div` tag on the view which is `CreateMethod.cshtml` in our case.
The validation summary will include all error messages because we there is the `All` keyword from the `asp-validation-summary="All"` code.
```html
<div asp-validation-summary="All"></div>
```


The image below shows how the validation summarry appears on the client-side:

<kbd>
  <img src="https://github.com/MinenhleNkosi/ASP.NET_Core_Web_API/blob/main/eCommerse/eCommerseApp/Notes/14.%20Custom%20Validation/Images/2.png?raw=true" height="auto" width="1000" />
</kbd>
<hr>

Now let's recall that the error message `The Name cannot exactly match the Display Order` appears only when there is an error on the *category name* input field. 
This is because we specified the `key` *name* in the `AddModelError()` method as seen below:
```cs
if (obj.Name == obj.DisplayOrder.ToString())
{
    ModelState.AddModelError("name", "The Name cannot exactly match the Display Order");
}
```

    Note
    The key name from the controller corresponds with the `asp-for="Name"` on the client-side in `CreateMethod.cshtml` view.

Now let's add another validation on the category controller at action `CreateMethod()`:
```cs
if (obj.Name != null && obj.Name.ToLower() == "test")
{
    ModelState.AddModelError("", "Test is an invalid value");
}
```

The reasons for the above validation:
* We want to see what will happen if we don't specify the `Key` (which was *name*)
* To see if `obj.Name.ToLower() == "test"` will work as expected


Let's run the application and see what we get

<kbd>
  <img src="https://github.com/MinenhleNkosi/ASP.NET_Core_Web_API/blob/main/eCommerse/eCommerseApp/Notes/14.%20Custom%20Validation/Images/3.png?raw=true" height="auto" width="1000" />
</kbd>
<hr>

Both the validation were displayed regardless of whether we specified the `key` or not.
The error message `Test is an invalid value` only appeared on the validation summary and not on the *category name* even though the word *test* was an input on the *category name*
By now we know that the reason the error message `Test is an invalid value` appears on the validation summary it's because *All* was specfied on the view `asp-validation-summary="All"`.


## asp-validation-summary=""
What are options we have for the validation summary? We have:
1. `All`: Displays every error message on the client-side.
    `<div asp-validation-summary="All" style="-webkit-text-fill-color: red"></div>`
   
      <kbd>
        <img src="https://github.com/MinenhleNkosi/ASP.NET_Core_Web_API/blob/main/eCommerse/eCommerseApp/Notes/14.%20Custom%20Validation/Images/2.png?raw=true" height="auto" width="1000" />
      </kbd>
      <hr>

3. `ModelOnly`: Disables property related validations from the model.
    `<div asp-validation-summary="ModelOnly" style="-webkit-text-fill-color: red"></div>`

      <kbd>
        <img src="https://github.com/MinenhleNkosi/ASP.NET_Core_Web_API/blob/main/eCommerse/eCommerseApp/Notes/13.%20Built-in%20Validation/Images/9.png?raw=true" height="auto" width="1000" />
      </kbd>
      <hr>
      (image5)

--------------------
3. `None`: Disables validation summary.
    `<div asp-validation-summary="None" style="-webkit-text-fill-color: red"></div>` 
   
      <kbd>
        <img src="https://github.com/MinenhleNkosi/ASP.NET_Core_Web_API/blob/main/eCommerse/eCommerseApp/Notes/13.%20Built-in%20Validation/Images/9.png?raw=true" height="auto" width="1000" />
      </kbd>
      <hr>
      (image4)






