# Entity Framework - Retrieve Id of Inserted Entity

## How can I get Id of inserted entity? 

I have a problem with Entity Framework in Asp.net. I want to get the Id value whenever I add an object to database. How can I do this?

### StackOverflow Related Questions

 - [How can I get Id of inserted entity in Entity framework?](https://stackoverflow.com/questions/5212751/how-can-i-get-id-of-inserted-entity-in-entity-framework)
 - [Get Record ID in Entity Framework after insert](https://stackoverflow.com/questions/16954767/get-record-id-in-entity-framework-after-insert)

## Answer

It is pretty easy. If you are using DB generated Ids (like `IDENTITY` in MS SQL) you just need to add entity to the contexct and call SaveChanges on that context. Id will be automatically filled for you.


```csharp
using (var context = new MyContext())
{
    Student student = new Student()
    {
        Name = "Mark";
    };  
    context.Students.Add(student);
    context.SaveChanges();

  int id = student.Id;
}
```

Entity framework by default follows each `INSERT` with SELECT `SCOPE_IDENTITY()` when auto-generated Ids are used.