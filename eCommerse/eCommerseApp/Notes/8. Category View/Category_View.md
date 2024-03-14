# Category View ©
Right now on our View, which is on the **Views** => **Category** => *Index.cshtml* folder:

<kbd>
  <img src="https://github.com/MinenhleNkosi/ASP.NET_Core_Web_API/blob/main/eCommerse/eCommerseApp/Notes/8.%20Category%20View/Images/1.png?raw=true" height="auto" width="400" />
</kbd>


As of now our view only displays a message **Wola Boizin** since the view has the below code in it:
```html
<h1>Wola Boizin</h1>
```

Instead of showing **Wola Boizin** we should display data stored on the database.

## Displaying data stored on the database.
1. We want to display the data in a tabular format, thus let's create a table to handle the data:
```html
<table class="table table-bordered table-striped">
        <thead>
            <tr>
                <th>
                    Category Name
                </th>
                <th>
                    Display Order
                </th>
            </tr>
        </thead>
        <tbody></tbody>
</table>
```
`<thead></thead>` tag is for specifying the head part of your HTML section.
`<tr></tr>` tag is for specifying that any content inside it belongs in the same row (moving horizontally from left to right).
`<th></th>` tag is for specifying the table header(s) which is what we use to define the column attributes (moving vertically from top to bottom).
`<tbody></tbody>` tag is the middle section where mst of the data manipulation will take place in our view.

so the above code will yield the below table colmns created:

<kbd>
  <img src="https://github.com/MinenhleNkosi/ASP.NET_Core_Web_API/blob/main/eCommerse/eCommerseApp/Notes/8.%20Category%20View/Images/2.png?raw=true" height="auto" width="800" />
</kbd>

2. Now that we have the table headers, it's time to add the data into it's rightful columns
On our view we now have to specify the model which the data we want to display is based on, on our case it's the `Category.cs` model. We do that as below:
```cshtml
@model List<Category>

<table class="table table-bordered table-striped">
        <thead>
            <tr>
                <th>
                    Category Name
                </th>
                <th>
                    Display Order
                </th>
            </tr>
        </thead>
        <tbody></tbody>
</table>
```

By adding `@model List<Category>` we are letting the view to jexpect a list of category data.

3. Now that we defined the model, we can proceed to use it inside our table columns, as below:
Inside the body we want to display the category name and the display order:
```cshtml
<tbody>
    <tr>
        <td>
            Name
        </td>
        <td>
            DisplayOrder
        </td>
    </tr>
</tbody>
```

`<td></td>` tag specifies the table data that will be reflected on the view page.

4. So we know that `Name` and `Displayorder` will come from the list of category `List<Category>`, since it's a list we have to iterate through it in order to properly display the data.
We achieve that we use a `for-loop` to do the ieteration thus modifying the code as below:
```cshtml
<tbody>
    @foreach (var obj in Model)
    {
        <tr>
            <td>
                @obj.Name
            </td>
            <td>
                @obj.DisplayOrder
            </td>
        </tr>
    }

</tbody>
```

5. Now when we run the application, we can see our table displaying the data as expected

<kbd>
  <img src="https://github.com/MinenhleNkosi/ASP.NET_Core_Web_API/blob/main/eCommerse/eCommerseApp/Notes/8.%20Category%20View/Images/3.png?raw=true" height="auto" width="800" />
</kbd>

6. Now if we want to display the table in ascending order based on the display order, we can alter the code as below:
```cshtml
<tbody>
    @foreach (var obj in Model.OrderBy(s => s.DisplayOrder))
    {
        <tr>
            <td>
                @obj.Name
            </td>
            <td>
                @obj.DisplayOrder
            </td>
        </tr>
    }

</tbody>
```

7. Th final code for the category view:
```cshtml
@model List<Category>

<table class="table table-bordered table-striped">
    <thead>
        <tr>
            <th>
                Category Name
            </th>
            <th>
                Display Order
            </th>
        </tr>
    </thead>
    <tbody>
        @foreach (var obj in Model.OrderBy(s => s.DisplayOrder))
        {
            <tr>
                <td>
                    @obj.Name
                </td>
                <td>
                    @obj.DisplayOrder
                </td>
            </tr>
        }

    </tbody>
</table>
```
