---
permalink: update-records
---

## How to Bulk Update?

Updating entities using a custom key from file importation is a typical scenario. Despite the ChangeTracker being outstanding to track what's modified, it lacks in term of scalability and flexibility.

SaveChanges requires one database round-trip for every entity to update. So if you need to update 10000 entities, then 10000 database round-trips will be performed which is **INSANELY** slow.

### StackOverflow Related Questions

 - [Batch update/delete EF5](https://stackoverflow.com/questions/12751258/batch-update-delete-ef5)
 - [EntityFrameWork Update Multiple Rows](https://stackoverflow.com/questions/19035312/entityframework-update-multiple-rows?noredirect=1&lq=1)

## Answer

[Entity Framework Extensions](http://entityframework-extensions.net/) library adds the BulkUpdate extension method to the DbContext. **BulkUpdate** offers great customization and requires the minimum database round-trips as compared to **SaveChanges**.

{% include template-example.html %} 
{% highlight csharp %}
// Easy to use
context.BulkUpdate(list);

// Easy to customize
context.BulkUpdate(customers, options => 
        options.ColumnPrimaryKeyExpression = customer => customer.Code);

{% endhighlight %}

All rows that match the entity key are considered as existing and are UPDATED in the database.

#### Performance Comparisons

|Operations	|1,000 Entities	|2,000 Entities	|5,000 Entities|
|:--------- |:------------- |:------------- |:------------ |
|SaveChange |1,000 ms	    |2,000 ms	    |5,000 ms      |
|BulkUpdate	|50 ms	        |55 ms	        |65 ms         |

[Learn more](http://entityframework-extensions.net/bulk-update)

## How to update without loading entities in the context?

Updating entities using SaveChanges requires typically to load them first in the ChangeTracker. These additional round-trips are often not necessary.

### StackOverflow Related Questions

 - [Update a record without first querying?](https://stackoverflow.com/questions/4218566/update-a-record-without-first-querying)
 - [Update record without fetching first Entity Framework](https://stackoverflow.com/questions/45938864/update-record-without-fetching-first-entity-framework?noredirect=1&lq=1)

## Answer

### BulkUpdate

[Entity Framework Extensions](http://entityframework-extensions.net/) library adds the UpdateFromQuery extension method. **UpdateFromQuery** gives you access to directly execute an `UPDATE` statement in the database and provide a **HUGE** performance improvement.

UPDATE all rows from the database using a LINQ Query without loading entities in the context.

An UPDATE statement is built using the LINQ expression and directly executed in the database.

{% include template-example.html %} 
{% highlight csharp %}

// UPDATE all customers that are inactive for more than two years
context.Customers
    .Where(x => x.Actif && x.LastLogin < DateTime.Now.AddYears(-2))
    .UpdateFromQuery(x => new Customer {Actif = false});
	
// UPDATE customers by id
context.Customers.Where(x => x.ID == userId).UpdateFromQuery(x => new Customer {Actif = false});

{% endhighlight %}

#### Performance Comparisons

|Operations	     |1,000 Entitie  |2,000 Entities |5,000 Entities|
|:-------------- |:------------- |:------------- |:------------ |
|SaveChange      |1,000 ms	     |2,000 ms	     |5,000 ms      |
|UpdateFromQuery |1 ms	         |1 ms	         |1 ms          |

[Learn more](http://entityframework-extensions.net/update-from-query)
