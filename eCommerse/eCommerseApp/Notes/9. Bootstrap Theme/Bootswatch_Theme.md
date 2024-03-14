# Everyone loves a pretty application 🫧
To make our application more appealing to the eye we will make use of **Bootstrap** and **Bootswatch Theme**

## Bootswatch Theme
1. Go to the below link:
	`https://bootswatch.com/`
2. Download your favourite theme (for this application we are using the Cerulea theme) as shown below:

	<kbd>
	  <img src="https://github.com/MinenhleNkosi/ASP.NET_Core_Web_API/blob/main/eCommerse/eCommerseApp/Notes/9.%20Bootstrap%20Theme/Images/2.png?raw=true" height="auto" width="400" />
	</kbd>

3. Open the `bootstrap.css` file after downloading it. Copy everything and paste it on the `bootstrap.css` file inside your css folder in your applicaton:

	<kbd>
	  <img src="https://github.com/MinenhleNkosi/ASP.NET_Core_Web_API/blob/main/eCommerse/eCommerseApp/Notes/8.%20Category%20View/Images/1.png?raw=true" height="auto" width="400" />
	</kbd>

4. In the `_Layout.cshtml` file, instead of using the `bootstrap.min.css` file link we will use the `bootstrap.css` file link. On the `<head></head>` tag section:
Replace : `<link rel="stylesheet" href="~/lib/bootstrap/dist/css/bootstrap.min.css" />`
With : `<link rel="stylesheet" href="~/lib/bootstrap/dist/css/bootstrap.css" />`

5. Now let's pimp up our Nav-bar:
Replace : `<nav class="navbar navbar-expand-sm navbar-toggleable-sm navbar-light bg-white border-bottom box-shadow mb-3">`
With : `<nav class="navbar navbar-expand-sm navbar-toggleable-sm navbar-dark bg-primary border-bottom box-shadow mb-3">`

6. Let's pimp up the footer:
    Replace:
    ```html
    <footer class="border-top footer text-muted">
        <div class="container text-white" style="text-align: center;">
            &copy; 2024 - eCommerseApp ></i>
        </div>
    </footer>
    ```

    With:
    ```html
    <footer class="border-top bg-primary footer text-muted">
        <div class="container text-white" style="text-align: center;">
            &copy; 2024 - eCommerseApp
        </div>
    </footer>
    ```

7. Let's add icons on our footer:
* Go to the link:
    `https://icons.getbootstrap.com/`

* Go to the **Install** section and copy the first link on the **CDN** section:

    <kbd>
	  <img src="https://github.com/MinenhleNkosi/ASP.NET_Core_Web_API/blob/main/eCommerse/eCommerseApp/Notes/8.%20Category%20View/Images/1.png?raw=true" height="auto" width="400" />
	</kbd>

* Paste it on the `_Layout.cshtml` head tag section:
    ```html
    <head>
        <meta charset="utf-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>@ViewData["Title"] - eCommerseApp</title>
        <link rel="stylesheet" href="~/lib/bootstrap/dist/css/bootstrap.css" />
        <link rel="stylesheet" href="~/css/site.css" asp-append-version="true" />
        <link rel="stylesheet" href="~/eCommerseApp.styles.css" asp-append-version="true" />
        <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.3/font/bootstrap-icons.min.css">
    </head>
    ```

* Now let's search fr an icon by using the search bar then after copy the icon link and add it on your footer section:
    ```html
    <footer class="border-top bg-primary footer text-muted">
        <div class="container text-white" style="text-align: center;">
            &copy; 2024 - eCommerseApp - For the <i class="bi bi-balloon-heart"></i> of  <i class="bi bi-code-slash"></i>
        </div>
    </footer>
    ```
 
