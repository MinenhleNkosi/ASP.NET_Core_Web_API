# Category Model 🏗️
Here I will create a simple category model which we will use to categorise the products in my eCommerce Application.

The model is shown by the code below:
```cs
public class Category
{
    public int Id { get; set; }
    public string Name { get; set; }
    public int DisplayOrder { get; set; }
}
```

Next we need to use Data Annotation to explicitly specify some prperties conditions.

## Primary key
Is what sets the class/Table unique and it is required that every class must have one.
By default, EF Core looks for "Id" in your properties and takes it as a primary key.
So you can name your primary key as anything but you must include "Id" at the end so that EF Core will be able to pick it up.
If you have something like "MyKey___Id", EF Core won't be able to pick it up as a primary key thus there will be an error.

If you have primary key like "MyKey___Id", we use Data Annotation to make sure that EF Core knows that it's a primary key as shown below:
```cs
[Key]
public int MyKey___Id { get; set; }
```
In this way, EF Core will automatically think "MyKey___Id" is a primary keyword (sweet😎).


If you know that property "Name" is required, meaning it shouldn't be *null*. We use the Data Annotation shown below:
```cs
[Required]
public string Name { get; set; }
```

So my Model will look like below (note that the "Key" is not neccessary since "Id" will get picked up by EF Core):
```cs
public class Category
{
    [key]
    public int Id { get; set; }

    [Required]
    public string Name { get; set; }

    [DisplayName("Display Order")]
    public int DisplayOrder { get; set; }
}
```
