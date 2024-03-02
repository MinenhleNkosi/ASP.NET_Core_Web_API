# Routing
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
  <img src="https://github.com/MinenhleNkosi/ASP.NET_Core_Web_API/blob/main/eCommerse/eCommerseApp/Notes/2.%20MVC%20Architecture/Images/1.png?raw=true" height="auto" width="600" />
</kbd>
![pic1](https://dev.azure.com/minenhlenkosi/a8e904a0-ca8c-4ee6-9bb8-acf45666f7c3/_apis/git/repositories/ea2d8e4f-4bb3-46c9-85b8-59c1cd082958/items?path=/eCommerse/eCommerseApp/Notes/3.%20Routing/Images/1.png&versionDescriptor%5BversionOptions%5D=0&versionDescriptor%5BversionType%5D=0&versionDescriptor%5Bversion%5D=master&resolveLfs=true&%24format=octetStream&api-version=5.0)

## Inside the Controllers folder
When creating a `Controller` file, you must name your file by putting file name first then foolowed by the word *Controller*.
If I want to name my file `Home.cs` then it should be `HomeController.cs`.
Your file should always be placed inside the **Controllers** folder or else it will not work.

![pic2](https://dev.azure.com/minenhlenkosi/a8e904a0-ca8c-4ee6-9bb8-acf45666f7c3/_apis/git/repositories/ea2d8e4f-4bb3-46c9-85b8-59c1cd082958/items?path=/eCommerse/eCommerseApp/Notes/3.%20Routing/Images/2.png&versionDescriptor%5BversionOptions%5D=0&versionDescriptor%5BversionType%5D=0&versionDescriptor%5Bversion%5D=master&resolveLfs=true&%24format=octetStream&api-version=5.0)

## Inside the Views folder
Since we named controller `HomeController.cs`, then here we must have a folder called **Home** and that is how the MVC architecture works.

![pic3](https://dev.azure.com/minenhlenkosi/a8e904a0-ca8c-4ee6-9bb8-acf45666f7c3/_apis/git/repositories/ea2d8e4f-4bb3-46c9-85b8-59c1cd082958/items?path=/eCommerse/eCommerseApp/Notes/3.%20Routing/Images/3.png&versionDescriptor%5BversionOptions%5D=0&versionDescriptor%5BversionType%5D=0&versionDescriptor%5Bversion%5D=master&resolveLfs=true&%24format=octetStream&api-version=5.0)

## Inside the Home folder we have two files:
    * Index.cshtml
    * Privacy.cshtml

These files (index.cshtml and Privacy.cshtml) are what we can see when we run the application.

![pic4](https://dev.azure.com/minenhlenkosi/a8e904a0-ca8c-4ee6-9bb8-acf45666f7c3/_apis/git/repositories/ea2d8e4f-4bb3-46c9-85b8-59c1cd082958/items?path=/eCommerse/eCommerseApp/Notes/3.%20Routing/Images/4.png&versionDescriptor%5BversionOptions%5D=0&versionDescriptor%5BversionType%5D=0&versionDescriptor%5Bversion%5D=master&resolveLfs=true&%24format=octetStream&api-version=5.0)


Pay close attention the the url from the image above. You can see that routing is not specified but yet our application works, how is that possible?
Well it is because of the default routing that takes over when no routing is specified:
```cs
app.MapControllerRoute(
    name: "default",
    pattern: "{controller=Home}/{action=Index}/{id?}");
```

When we do specify the routing where our controller name is **Home** and our action is **Index**, we still able to get the above results.

![pic5](https://dev.azure.com/minenhlenkosi/a8e904a0-ca8c-4ee6-9bb8-acf45666f7c3/_apis/git/repositories/ea2d8e4f-4bb3-46c9-85b8-59c1cd082958/items?path=/eCommerse/eCommerseApp/Notes/3.%20Routing/Images/5.png&versionDescriptor%5BversionOptions%5D=0&versionDescriptor%5BversionType%5D=0&versionDescriptor%5Bversion%5D=master&resolveLfs=true&%24format=octetStream&api-version=5.0)


Now we navigate to the **Privacy** page.

![pic6](https://dev.azure.com/minenhlenkosi/a8e904a0-ca8c-4ee6-9bb8-acf45666f7c3/_apis/git/repositories/ea2d8e4f-4bb3-46c9-85b8-59c1cd082958/items?path=/eCommerse/eCommerseApp/Notes/3.%20Routing/Images/6.png&versionDescriptor%5BversionOptions%5D=0&versionDescriptor%5BversionType%5D=0&versionDescriptor%5Bversion%5D=master&resolveLfs=true&%24format=octetStream&api-version=5.0)



## How does the Controller knows which View to open?
See image below for better illustration on rendering the Index/Home page.

![pic7](https://dev.azure.com/minenhlenkosi/a8e904a0-ca8c-4ee6-9bb8-acf45666f7c3/_apis/git/repositories/ea2d8e4f-4bb3-46c9-85b8-59c1cd082958/items?path=/eCommerse/eCommerseApp/Notes/3.%20Routing/Images/7.png&versionDescriptor%5BversionOptions%5D=0&versionDescriptor%5BversionType%5D=0&versionDescriptor%5Bversion%5D=master&resolveLfs=true&%24format=octetStream&api-version=5.0)



See image below for better illustration on rendering the Privacy page.

![pic8](https://dev.azure.com/minenhlenkosi/a8e904a0-ca8c-4ee6-9bb8-acf45666f7c3/_apis/git/repositories/ea2d8e4f-4bb3-46c9-85b8-59c1cd082958/items?path=/eCommerse/eCommerseApp/Notes/3.%20Routing/Images/8.png&versionDescriptor%5BversionOptions%5D=0&versionDescriptor%5BversionType%5D=0&versionDescriptor%5Bversion%5D=master&resolveLfs=true&%24format=octetStream&api-version=5.0)

```
    _Layout.cshtml
    This file is the Master page, here is where everything is rendered.
    It consist of the vaigation bar, the footer we see on our application.
    The Index.cshtml and Privacy.cshtml files get rendered within the _Layout.cshtml file in the RenderBody() method.
```


## Inside the Shared folder

![pic9](https://dev.azure.com/minenhlenkosi/a8e904a0-ca8c-4ee6-9bb8-acf45666f7c3/_apis/git/repositories/ea2d8e4f-4bb3-46c9-85b8-59c1cd082958/items?path=/eCommerse/eCommerseApp/Notes/3.%20Routing/Images/9.png&versionDescriptor%5BversionOptions%5D=0&versionDescriptor%5BversionType%5D=0&versionDescriptor%5Bversion%5D=master&resolveLfs=true&%24format=octetStream&api-version=5.0)
