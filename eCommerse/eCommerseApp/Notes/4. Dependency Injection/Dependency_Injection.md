# Dependency Injection
Is a design pattern in which a class or an object has it's dependent classes injected rather than directly creating them.
It's effecient because we do not have to create, manage and dispose the object. It also improves the loose coupling between classes.

## Real World example
1. Bob wants to go Hiking
2. Since its a long hike, Bob will require many supplies like, map, flash light, food in order to hike safely.
3. He places everything he needs on his bag.
4. The next day when he goes Hiking, he takes the bag with him.
5. The bag acts as a container. During the Hike if he needs anything, he can takeit out of the bag.

So you put all the items you need in one container so that when you need them you can be able to use them anytime.

### How does the above mentioned relate to programming and dependency injection?
1. Let's in our web app we have 3 pages and two functionality (email and database).
2. We want to be able to send email and be able to access our database in all the 3 pages we have.
3. First we want to acces the database:
    * We will create an object of our class (in this case its `Db dbObj = new Db()`).
    * We then use `dbObj` to access the the database.
    * Then we will call some methods inside that object and retrieve data.
    * Once we are done, we will dispose that object we created which is `dbObj`.
    * This object create we will have to do for all the 3 pages.

      <kbd>
        <img src="https://github.com/MinenhleNkosi/ASP.NET_Core_Web_API/blob/main/eCommerse/eCommerseApp/Notes/2.%20MVC%20Architecture/Images/1.png?raw=true" height="auto" width="600" />
      </kbd>

    ![pic1](https://dev.azure.com/minenhlenkosi/a8e904a0-ca8c-4ee6-9bb8-acf45666f7c3/_apis/git/repositories/ea2d8e4f-4bb3-46c9-85b8-59c1cd082958/items?path=/eCommerse/eCommerseApp/Notes/4.%20Dependency%20Injection/Images/1.png&versionDescriptor%5BversionOptions%5D=0&versionDescriptor%5BversionType%5D=0&versionDescriptor%5Bversion%5D=master&resolveLfs=true&%24format=octetStream&api-version=5.0)



    * Same thing we will have to do for the email.
    
    ![pic2](https://dev.azure.com/minenhlenkosi/a8e904a0-ca8c-4ee6-9bb8-acf45666f7c3/_apis/git/repositories/ea2d8e4f-4bb3-46c9-85b8-59c1cd082958/items?path=/eCommerse/eCommerseApp/Notes/4.%20Dependency%20Injection/Images/2.png&versionDescriptor%5BversionOptions%5D=0&versionDescriptor%5BversionType%5D=0&versionDescriptor%5Bversion%5D=master&resolveLfs=true&%24format=octetStream&api-version=5.0)

    * This creates a lot of duplicate code.

4. The solution is to use dependency injection.
    * We will have a dependecy injection (DI) container and in that container we will register both email and database service.
    * So there we will have an interface of IEmail and IDb.
    * Then we will have the implementation inside Email and Db classes
    
    ![pic3](https://dev.azure.com/minenhlenkosi/a8e904a0-ca8c-4ee6-9bb8-acf45666f7c3/_apis/git/repositories/ea2d8e4f-4bb3-46c9-85b8-59c1cd082958/items?path=/eCommerse/eCommerseApp/Notes/4.%20Dependency%20Injection/Images/3.png&versionDescriptor%5BversionOptions%5D=0&versionDescriptor%5BversionType%5D=0&versionDescriptor%5Bversion%5D=master&resolveLfs=true&%24format=octetStream&api-version=5.0)



    * When any page access this functionalities, they would ask for the implementation of IDb or IEmail.
    * The pages do not know what implementations will be given to them and the DI container container is responsible for all of that.
    
    ![pic4](https://dev.azure.com/minenhlenkosi/a8e904a0-ca8c-4ee6-9bb8-acf45666f7c3/_apis/git/repositories/ea2d8e4f-4bb3-46c9-85b8-59c1cd082958/items?path=/eCommerse/eCommerseApp/Notes/4.%20Dependency%20Injection/Images/4.png&versionDescriptor%5BversionOptions%5D=0&versionDescriptor%5BversionType%5D=0&versionDescriptor%5Bversion%5D=master&resolveLfs=true&%24format=octetStream&api-version=5.0)



    * What the framework will do is when a page requests implementation for email interface (IEmail) it will look inside the container to find out that email interface is implemented inside the email class, thus it will create the object by default and pass it on to the page.
    * In that way we do not have to deal with creating the object, managing and disposing it after use in our page
    * The code will be clean as it will contain the interface and the implementation is provided by the DI container.
    * If we need to make any changes, then we will only change the implementation class in the DI container.
    * After that all the pages wil automatically get the new implementation.
    ![pic5](https://dev.azure.com/minenhlenkosi/a8e904a0-ca8c-4ee6-9bb8-acf45666f7c3/_apis/git/repositories/ea2d8e4f-4bb3-46c9-85b8-59c1cd082958/items?path=/eCommerse/eCommerseApp/Notes/4.%20Dependency%20Injection/Images/5.png&versionDescriptor%5BversionOptions%5D=0&versionDescriptor%5BversionType%5D=0&versionDescriptor%5Bversion%5D=master&resolveLfs=true&%24format=octetStream&api-version=5.0)

    

