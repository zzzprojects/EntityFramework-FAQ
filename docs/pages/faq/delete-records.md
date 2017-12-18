---
permalink: delete-records
---

## How to Bulk Delete?

Deleting entities using a custom key from file importation is a typical scenario. Despite the ChangeTracker being outstanding to track what's modified, it lacks in term of scalability and flexibility.

SaveChanges requires one database round-trip for every entity to delete. So if you need to remove 10000 entities, then 10000 database round-trips will be performed which is **INSANELY** slow.

### StackOverflow Related Questions

 - [Batch update/delete EF5](https://stackoverflow.com/questions/12751258/batch-update-delete-ef5)

## Answer

[Entity Framework Extensions](http://entityframework-extensions.net/) library adds the BulkDelete extension method to the DbContext. **BulkDelete** offers great customization and requires the minimum database round-trips as compared to **SaveChanges**.

{% include template-example.html %} 
{% highlight csharp %}

// Easy to use
context.BulkDelete(list);

// Easy to customize
context.BulkDelete(customers, options => 
        options.ColumnPrimaryKeyExpression = customer => customer.Code);
{% endhighlight %}

All rows that match the entity key are considered as existing and are **DELETED** from the database.

#### Performance Comparisons

|Operations	|1,000 Entities	|2,000 Entities	|5,000 Entities|
|:--------- |:------------- |:------------- |:------------ |
|SaveChange |1,000 ms	    |2,000 ms	    |5,000 ms      |
|BulkDelete	|45 ms	        |50 ms	        |60 ms         |

[Learn more](http://entityframework-extensions.net/bulk-delete)

## Exception: 

### The object cannot be deleted because it was not found in the ObjectStateManager

When an entity is fetched and deleted using different DbContext object, then it throws an exception **The object cannot be deleted because it was not found in the ObjectStateManager.**

{% include template-example.html %} 
{% highlight csharp %}

Customer deletedCustomer = null;
using (var context = new CustomerContext())
{
    deletedCustomer = context.Customers.Where(d => d.CustomerId == 3).FirstOrDefault();
}

using (var context = new CustomerContext())
{
    context.Customers.Remove(deletedCustomer);
    context.SaveChanges();
}
{% endhighlight %}

In the above example, the customer entity is fetched in one DbContext instance, and then it is removed/deleted from the database in another DbContext instance.  
### StackOverflow Related Questions

 - [The object cannot be deleted because it was not found in the ObjectStateManager](https://stackoverflow.com/questions/7791149/the-object-cannot-be-deleted-because-it-was-not-found-in-the-objectstatemanager)

## Solution

To avoid the above exception, make sure that either entity is fetched and deleted in the same DbContext instance or an entity is attached to the context before removing it.
 
### Use Same DbContext Instance

{% include template-example.html %} 
{% highlight csharp %}

using (var context = new CustomerContext())
{
    var deletedCustomer = context.Customers.Where(d => d.CustomerId == 3).FirstOrDefault();
    context.Customers.Remove(deletedCustomer);
    context.SaveChanges();
}
{% endhighlight %}

### Attach Before Deleting

{% include template-example.html %} 
{% highlight csharp %}

Customer deletedCustomer = null;
using (var context = new CustomerContext())
{
    deletedCustomer = context.Customers.Where(d => d.CustomerId == 3).FirstOrDefault();
}

using (var context = new CustomerContext())
{
    context.Customers.Attach(deletedCustomer);
    context.Customers.Remove(deletedCustomer);
    context.SaveChanges();
}
{% endhighlight %}
