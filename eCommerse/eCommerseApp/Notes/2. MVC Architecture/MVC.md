# MVC Architecture 💪
It stands for Models View and Controllers will is a design pattern widely used in .NET.

## Model
Represents the shape of the data which in the database side it represents the tables and in the programming side it represents the classes

## View
It represents the user interface (frontend), this is what you see on the screen.

## Controller
It handles the user request and acts as a middleman between the Model and the View

## MVC in action
1. The user will send a request using the `View` (frontend).
2. That **request** will first reach the `Controller`.
3. Then the `Controller` will determines which `Model` to use based on the request parameters.
4. When the `Model` is selected, that `Model` will be used to fecth the requested data (backend).
5. The requested data will be passed to the `Controler` then to the `View`.
6. The `View` will then populate the `HTMl` will the data and send it back to the `Controller`.
7. Then lastly the `Controller` will send that data back to the client as a **response** which you get to view on your screen. 

![pic](https://dev.azure.com/minenhlenkosi/a8e904a0-ca8c-4ee6-9bb8-acf45666f7c3/_apis/git/repositories/ea2d8e4f-4bb3-46c9-85b8-59c1cd082958/items?path=/eCommerse/eCommerseApp/Notes/2.%20MVC%20Architecture/Images/1.png&versionDescriptor%5BversionOptions%5D=0&versionDescriptor%5BversionType%5D=0&versionDescriptor%5Bversion%5D=master&resolveLfs=true&%24format=octetStream&api-version=5.0)