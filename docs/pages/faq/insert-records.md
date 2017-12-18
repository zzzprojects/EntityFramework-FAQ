---
permalink: insert-records
---

## How to do a Bulk Insert?

Inserting thousand of entities for an initial load or a file importation is a typical scenario. 

**SaveChanges** method makes it quite impossible to handle this kind of situation directly from Entity Framework due to the number of database round-trips required.

SaveChanges requires one database round-trip for every entity to insert. So if you need to insert 10000 entities, then 10000 database round-trips will be performed which is **INSANELY** slow.

{% include template-example.html %} 
{% highlight csharp %}
using (var ctx = new CustomerContext())
{
    List<Customer> customers = new List<Customer>();
    
    foreach(var line in lines)
    {
        var customer = new Customer();
        // ...code...
        
        customers.Add(customer);
    }
    
    ctx.Customers.AddRange(customers);

    ctx.SaveChanges();
}

{% endhighlight %}

### StackOverflow Related Questions

 - [How to do a Bulk Insert - Linq to Entities](https://stackoverflow.com/questions/1609153/how-to-do-a-bulk-insert-linq-to-entities)
 - [How to do Bulk Insert using MySQL (like SqlBulkCopy) with Linq to Entities](https://stackoverflow.com/questions/10129001/how-to-do-bulk-insert-using-mysql-like-sqlbulkcopy-with-linq-to-entities?rq=1)

## Answer

[Entity Framework Extensions](http://entityframework-extensions.net/) library adds the BulkInsert extension method to the DbContext. **BulkInsert** requires the minimum database round-trips as compared to **SaveChanges**.

{% include template-example.html %} 
{% highlight csharp %}

using (var ctx = new CustomerContext())
{
    List<Customer> customers = new List<Customer>();
    
    foreach(var line in lines)
    {
        var customer = new Customer();
        // ...code...
        
        customers.Add(customer);
    }
    
    ctx.BulkInsert(customers);
}

{% endhighlight %}

[Learn more](http://entityframework-extensions.net/bulk-insert)

## What's the fastest way to insert?

When you want to insert hundreds, thousands, or millions entities, and your application suffers from performances issues.

### StackOverflow Related Questions

 - [Fastest Way of Inserting in Entity Framework](https://stackoverflow.com/questions/5940225/fastest-way-of-inserting-in-entity-framework)
 - [Writing to large number of records take too much time using Entity Framework](https://stackoverflow.com/questions/43981993/writing-to-large-number-of-records-take-too-much-time-using-entity-framework?noredirect=1&lq=1)
 
## Answer

### BulkInsert

There are many solutions to insert many records in the fastest way, but the most significant and recommended solution is BulkInsert provided by [Entity Framework Extensions](http://entityframework-extensions.net/) library. By default, identity value are populated to make it even easier to use.

#### Performance Comparisons

|Operations	|1,000 Entities	|2,000 Entities	|5,000 Entities|
|:--------- |:------------- |:------------- |:------------ |
|SaveChange |1,000 ms	    |2,000 ms	    |5,000 ms      |
|BulkInsert	|6 ms	        |10 ms	        |15 ms         |

#### Steps to use BulkInsert

 1. CREATE a list
 2. ADD entity to the list
 3. USE BulkInsert
 4. Done!

{% include template-example.html %} 
{% highlight csharp %}

using (var ctx = new CustomerContext())
{
    // 1. CREATE a list
    List<Customer> customers = new List<Customer>();
    
    foreach(var line in lines)
    {
        var customer = new Customer();
        // ...code...
        
        // 2. ADD entity to the list
        customers.Add(customer);
    }
    
    // 3. USE BulkInsert
    ctx.BulkInsert();
    
    // 4. Done!
}

{% endhighlight %}

### Alternative to BulkInsert

There are some free third party library alternative to Entity Framework Extensions, they are not hard to find but we don't recommand them since they work with simple scenario but fail at supporting complex type, inheritance and association.

### SqlBulkCopy

Using SqlBulkCopy (for SQL Server) is without a doubt the fastest solution (very slighty faster than Entity Framework Extensions) but also the longer to implement.

Be careful, this solution add some code complexity for the maintenance team.

#### Steps to use SqlBulkCopy

 1. CREATE a list
 2. ADD entity to the list
 3. CONVERT the list to a DataTable
 4. CREATE a SqlBulkCopy instance
 5. MAP the SqlBulkCopy to database
 6. Use WriteToServer
 7. Done!



