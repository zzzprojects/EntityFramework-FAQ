---
permalink: bulk-insert-libraries
---

## Introduction

BulkInsert allows you to improve EF performance by inserting multiples entities with bulk operations.

## Why BulkInsert?

For **HUGE** performance gains, Entity Framework makes one database round-trip for each entity to insert/update/delete. 

So if you want to add 10,000 entities, 10,000 database round trip will be required which is **INSANELY** slow. To use BulkInsert, you will need to use a third-party library.

|Operations	|1,000 Entities	|2,000 Entities	|5,000 Entities|
|:----------|:----------|:----------|:----------|
|BulkInsert	|6 ms	|10 ms	|15 ms|
|SaveChanges	|1,000 ms	|2,000 ms	|5,000 ms|

## Google Related Searches

 - [Entity Framework Insert Multiple Records](https://www.google.com/search?q=entity+framework+insert+multiple+records)
 - [Entity Framework Insert Multiple Rows](https://www.google.com/search?q=entity+framework+insert+multiple+rows)
 - [Entity Framework Add Range](https://www.google.com/search?q=entity+framework+add+range)

## StackOverflow Related Questions

 - [Fastest way of inserting many parent and child records](https://stackoverflow.com/questions/36606000/fastest-way-of-inserting-many-parent-and-child-records)
 - [Bulk Insert in Entity Framework v6.1](https://stackoverflow.com/questions/39745043/bulk-insert-in-entity-framework-v6-1)
 - [C# & EF: bulkinsert related objects](https://stackoverflow.com/questions/39320956/c-sharp-ef-bulkinsert-related-objects)
 - [Entity framework 6 code first Many to many insert slow](https://stackoverflow.com/questions/36939520/entity-framework-6-code-first-many-to-many-insert-slow)
 - [Insert thousands of many to many links to the DB quickly](https://stackoverflow.com/questions/35415557/insert-thousands-of-many-to-many-links-to-the-db-quickly)
 - [Entity Framework Bulk Insert Throws KeyNotFoundException error](https://stackoverflow.com/questions/32225183/entity-framework-bulk-insert-throws-keynotfoundexception-error/37969443#37969443)
 - [Bulk insert from a csv file using Entity Framework](https://stackoverflow.com/questions/36725006/bulk-insert-from-a-csv-file-using-entity-framework)


{% include template-example.html %} 
{% highlight csharp %}
// using Z.EntityFramework.Extensions; // Don't forget to include this.

// Easy to use
context.BulkInsert(list);

// Easy to customize
context.BulkInsert(list, bulk => bulk.BatchSize = 100);
{% endhighlight %}

## Supported Libraries

|Library	|Type	|EF Version	|Support	|Doc	|Features|
|:----------|:----------|:----------|:----------|:----------|:----------|
|[Z.EntityFramework.Plus](http://entityframework-plus.net/)	|FREE	|EF5<br>EF6<br>EF Core|	< 1 Day	|Yes    |Audit<br>Batch Delete<br>Batch Update<br>Cache<br>Deferred Query<br>Filter<br>Future<br>Include Filter<br>Include Optimized|

## Unsuported Library

Use these libraries at your risk!

|Library	|Type	|EF Version	|Support	|Doc	|Features |
|:--------- |:--------- |:--------- |:--------- |:--------- |:--------- |
|[EFUtilities](https://github.com/MikaelEliasson/EntityFramework.Utilities)	|FREE	|EF5<br>EF6	|No	    |No |Bulk Insert<br>Batch Delete<br>Batch Update<br>Include Optimized<br>
|[EntityFramework.BulkInsert](https://efbulkinsert.codeplex.com/)	|FREE	|EF5<br>EF6    |No	    |Yes    |Bulk Insert |

