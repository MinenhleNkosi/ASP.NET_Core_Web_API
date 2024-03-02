# Project Structre 
It is how a project gets structured and every IDE consist of slightly different ways of structuring a project.

<kbd>
  <img src="https://github.com/MinenhleNkosi/ASP.NET_Core_Web_API/blob/main/eCommerse/eCommerseApp/Notes/1.%20Project%20Structure/Images/1.png" height="auto" width="800" />
</kbd>

## Visual Studio 2022
* The project files are found on the **Solution Explorer** on the right hand side.

## Solution and Project
* It is found within the solution explorer which in this case it is called `eCommerse`.
* There can only be one solution per application.
* A project exist within the solution and I named it `eCommerseApp`.
* A solution can have multiple projects within it.

![pic2](https://dev.azure.com/minenhlenkosi/a8e904a0-ca8c-4ee6-9bb8-acf45666f7c3/_apis/git/repositories/ea2d8e4f-4bb3-46c9-85b8-59c1cd082958/items?path=/eCommerse/eCommerseApp/Notes/1.%20Project%20Structure/Images/2.png&versionDescriptor%5BversionOptions%5D=0&versionDescriptor%5BversionType%5D=0&versionDescriptor%5Bversion%5D=master&resolveLfs=true&%24format=octetStream&api-version=5.0)

## Project file
To find information about your project:
1. Right click on your project.
2. Select *Edit Project File*.

![pic3](https://dev.azure.com/minenhlenkosi/a8e904a0-ca8c-4ee6-9bb8-acf45666f7c3/_apis/git/repositories/ea2d8e4f-4bb3-46c9-85b8-59c1cd082958/items?path=/eCommerse/eCommerseApp/Notes/1.%20Project%20Structure/Images/3.png&versionDescriptor%5BversionOptions%5D=0&versionDescriptor%5BversionType%5D=0&versionDescriptor%5Bversion%5D=master&resolveLfs=true&%24format=octetStream&api-version=5.0)


3. Project information appears.
4. Inside the `PropertyGroup` it is where you find all your project properties like: 
    * `TargeFramework`: It is the .NET version your application runs on.
    * `Nullable`: Checks for nullability of variable when dealing with data.
    * `ImplicitUsing`: Instead of explicitly importing external libraries for use, the `using` is used in C# (which is awesome 😜)

![pic4](https://dev.azure.com/minenhlenkosi/a8e904a0-ca8c-4ee6-9bb8-acf45666f7c3/_apis/git/repositories/ea2d8e4f-4bb3-46c9-85b8-59c1cd082958/items?path=/eCommerse/eCommerseApp/Notes/1.%20Project%20Structure/Images/4.png&versionDescriptor%5BversionOptions%5D=0&versionDescriptor%5BversionType%5D=0&versionDescriptor%5Bversion%5D=master&resolveLfs=true&%24format=octetStream&api-version=5.0)

## Inside the Project
1. **Connected Services**:
    * We will ignore this one since it mostly remains empty.
2. **Dependencies**:
    * It is a way to note that this project is dependent on some packages or other project(s).
    * When we add more packages for more functionality this is where we see them.
3. **Properties**:
    * Here we have a file called `launchSettings.json`.
    * This file defines what or how to host our application when it's running.
    * When the application is ran it can be hosted on different profiles like HTTP, HTTPS, IIS Express.
    * Define `environmentVariables` for development or production.
4. **wwwroot**:
    * This folder holds all the static content (by static content we mean any css, javascript, nuget packages or third party library, images or files)
5. **Controllers**:
    * This folder is for handling the user request.
6. **Models**:
    * Represents the shape of the data.
7. **Views**:
    * It represents the user interface (frontend) files, this is what you see on the screen.
8. **appsettings.json**:
    * This is where I will host all of my connection strings or any secret keys that require protection.
9. **Program.cs**:
    * There are two things to recall about this file, first we add the service to the container and then we configure the request pipeline.
    * The service that is added/injected by default is the `AddControllersWithViews()` which enables us to make use of controller without explicit injection.
    * Then when it comes to configuring the pipeline, first on our pipeline we check the environment:
        * IsDevelopment
        * IsProduction
        * IsStaging
    * The order of addidng any service matters, e.g, you can't add `app.UseAuthorization();` without adding `app.UseAuthentication();` first when dealing with **Identity**.

![pic5](https://dev.azure.com/minenhlenkosi/a8e904a0-ca8c-4ee6-9bb8-acf45666f7c3/_apis/git/repositories/ea2d8e4f-4bb3-46c9-85b8-59c1cd082958/items?path=/eCommerse/eCommerseApp/Notes/1.%20Project%20Structure/Images/5.png&versionDescriptor%5BversionOptions%5D=0&versionDescriptor%5BversionType%5D=0&versionDescriptor%5Bversion%5D=master&resolveLfs=true&%24format=octetStream&api-version=5.0)


