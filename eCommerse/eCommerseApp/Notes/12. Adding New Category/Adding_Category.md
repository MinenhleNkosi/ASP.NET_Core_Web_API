# Adding a new category ➕
Now that we have the ui for Creating a new category:

<kbd>
  <img src="https://github.com/MinenhleNkosi/ASP.NET_Core_Web_API/blob/main/eCommerse/eCommerseApp/Notes/12.%20Adding%20New%20Category/Images/1.png?raw=true" height="auto" width="1000" />
</kbd>
<hr>

Our next step is to:
1. We take the user inputs
2. Pass them on to the controller.
3. Then store them on the database.

## Taking user inputs
For this part it's already accomplished using **tag helpers**, remember?
* For getting genre name we used `asp-for="Name"`
* For getting display order we used `asp-for="DisplayOrder"`

## Now let's pass our values to the Controller
Now when we examine the view page for adding new category, we can see that the form uses a **post** method:
```cshtml
<form method="post">
    //Some code here
</form>
```

So the **post** method means that when the **Create** button is triggered, it will hit the **post** method endpoint request.
Because of the **post** request, we now need to create an **action** method to handle the **post** request inside the *Category* controllerr.
```cs
[HttpPost]
public IActionResult CreateMethod(Category obj)
{
    _db.Categories.Add(obj);
    _db.SaveChanges();
    return RedirectToAction("Index");
}
```

From the above code:
* `obj` will hold the populated model of **Category**.
* Then we take `obj` and add it to the database using the database context instance `_db`
* After that we save the changes.
* Instead of just retunrning the view (which will return the create genre page), we have to make sure we return back to the page where we can view all added categories/genres. That page is the `Index.cshtml` page thus we have to redirect the view to that page by using the `redirectToAction();` method, and inside we have to pass in the page view name we want to go to thus we have `retrun RedirectToaction("Index");`

Now after clicking the "Create" button we should we able to store them on the database and the page will display the **Index** page.


## Store on the database
Right now our **Index** page has the below categories:

<kbd>
  <img src="https://github.com/MinenhleNkosi/ASP.NET_Core_Web_API/blob/main/eCommerse/eCommerseApp/Notes/12.%20Adding%20New%20Category/Images/2.png?raw=true" height="auto" width="1000" />
</kbd>

------------
Let's check the database for confirmation:

<kbd>
  <img src="https://github.com/MinenhleNkosi/ASP.NET_Core_Web_API/blob/main/eCommerse/eCommerseApp/Notes/12.%20Adding%20New%20Category/Images/3.png?raw=true" height="auto" width="600" />
</kbd>

------------
Let's make an example and add two categories:

<kbd>
  <img src="https://github.com/MinenhleNkosi/ASP.NET_Core_Web_API/blob/main/eCommerse/eCommerseApp/Notes/12.%20Adding%20New%20Category/Images/4.png?raw=true" height="auto" width="1000" />
</kbd>

------------
Now let's check our database to see if they were really added:

<kbd>
  <img src="https://github.com/MinenhleNkosi/ASP.NET_Core_Web_API/blob/main/eCommerse/eCommerseApp/Notes/12.%20Adding%20New%20Category/Images/5.png?raw=true" height="auto" width="600" />
</kbd>

