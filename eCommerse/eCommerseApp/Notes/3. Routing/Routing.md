# Routing ⬆️↗️➡️➡️↘️⬇️↙️↙️⬅️↖️
It what defines the `url` path as to where to send the request

## Default Routing
In the `Program.cs` file there is a default routing set:
```cs
app.MapControllerRoute(
    name: "default",
    pattern: "{controller=Home}/{action=Index}/{id?}");
```

## URL Pattern
The standard url pattern: 
`prtocol://domain-name:port-number/Controller/Action/Id`

e.g, `https://localhost:55555/Category/Index/5`

From the above example we see that:
1. `Category`: Controller
2. `Index`: Action
3. `5`: Id

For more illustartion refer to the image below:

<kbd>
  <img src="https://github.com/MinenhleNkosi/ASP.NET_Core_Web_API/blob/main/eCommerse/eCommerseApp/Notes/3.%20Routing/Images/1.png?raw=true" height="auto" width="800" />
</kbd>
<hr >
## Inside the Controllers folder
When creating a `Controller` file, you must name your file by putting file name first then foolowed by the word *Controller*.
If I want to name my file `Home.cs` then it should be `HomeController.cs`.
Your file should always be placed inside the **Controllers** folder or else it will not work.

<kbd>
  <img src="https://github.com/MinenhleNkosi/ASP.NET_Core_Web_API/blob/main/eCommerse/eCommerseApp/Notes/3.%20Routing/Images/2.png?raw=true" height="auto" width="800" />
</kbd>
<hr >
## Inside the Views folder
Since we named controller `HomeController.cs`, then here we must have a folder called **Home** and that is how the MVC architecture works.

<kbd>
  <img src="https://github.com/MinenhleNkosi/ASP.NET_Core_Web_API/blob/main/eCommerse/eCommerseApp/Notes/3.%20Routing/Images/3.png?raw=true" height="auto" width="800" />
</kbd>
<hr >
## Inside the Home folder we have two files:
    * `Index.cshtml`
    * `Privacy.cshtml`

These files (`index.cshtml` and `Privacy.cshtml`) are what we can see when we run the application.

<kbd>
  <img src="https://github.com/MinenhleNkosi/ASP.NET_Core_Web_API/blob/main/eCommerse/eCommerseApp/Notes/3.%20Routing/Images/4.png?raw=true" height="auto" width="800" />
</kbd>
<hr >
Pay close attention the the url from the image above. You can see that routing is not specified but yet our application works, how is that possible?
Well it is because of the default routing that takes over when no routing is specified:

```cs
app.MapControllerRoute(
    name: "default",
    pattern: "{controller=Home}/{action=Index}/{id?}");
```

When we do specify the routing where our controller name is **Home** and our action is **Index**, we still able to get the above results.

<kbd>
  <img src="https://github.com/MinenhleNkosi/ASP.NET_Core_Web_API/blob/main/eCommerse/eCommerseApp/Notes/3.%20Routing/Images/5.png?raw=true" height="auto" width="800" />
</kbd>
<hr >
Now we navigate to the **Privacy** page.

<kbd>
  <img src="https://github.com/MinenhleNkosi/ASP.NET_Core_Web_API/blob/main/eCommerse/eCommerseApp/Notes/3.%20Routing/Images/6.png?raw=true" height="auto" width="800" />
</kbd>
<hr >
## How does the Controller knows which View to open?
See image below for better illustration on rendering the **Index/Home** page.

<kbd>
  <img src="https://github.com/MinenhleNkosi/ASP.NET_Core_Web_API/blob/main/eCommerse/eCommerseApp/Notes/3.%20Routing/Images/7.png?raw=true" height="auto" width="1000" />
</kbd>
<hr >
See image below for better illustration on rendering the Privacy page.

<kbd>
  <img src="https://github.com/MinenhleNkosi/ASP.NET_Core_Web_API/blob/main/eCommerse/eCommerseApp/Notes/3.%20Routing/Images/8.png?raw=true" height="auto" width="1000" />
</kbd>
<hr >

`_Layout.cshtml`
* This file is the Master page, here is where everything is rendered.
* It consist of the vaigation bar, the footer we see on our application.
* The Index.cshtml and Privacy.cshtml files get rendered within the `_Layout.cshtml` file in the `RenderBody()` method.


## Inside the Shared folder

<kbd>
  <img src="https://github.com/MinenhleNkosi/ASP.NET_Core_Web_API/blob/main/eCommerse/eCommerseApp/Notes/3.%20Routing/Images/9.png?raw=true" height="auto" width="600" />
</kbd>
