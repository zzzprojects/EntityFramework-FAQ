---
permalink: batch-delete
---

## Introduction

Batch Delete allows you to improve EF performance by deleting multiple records in a database from a LINQ Query without loading entities.

## Why Batch Delete?

For **HUGE** performance gains, everything is executed on the database side.

## Google Related Searches

 - [Entity Framework Delete Without Loading](https://www.google.com/search?q=entity+framework+delete+without+loading)
 - [Entity Framework Delete Without Retrieving](https://www.google.com/search?q=entity+framework+delete+without+retrieving)

## StackOverflow Related Questions

 - [How do I delete multiple rows in Entity Framework (without foreach)](https://stackoverflow.com/questions/2519866/how-do-i-delete-multiple-rows-in-entity-framework-without-foreach)
 - [How to Delete multiple records in Linq to Entity?](https://stackoverflow.com/questions/20452652/how-to-delete-multiple-records-in-linq-to-entity?noredirect=1&lq=1)
 - [Bulk-deleting in LINQ to Entities](https://stackoverflow.com/questions/869209/bulk-deleting-in-linq-to-entities?noredirect=1&lq=1)

{% include template-example.html %} 
{% highlight csharp %}
// using Z.EntityFramework.Plus; // Don't forget to include this.

// DELETE all users inactive for 2 years
ctx.Users.Where(x => x.LastLoginDate < DateTime.Now.AddYears(-2))
         .Delete();

// DELETE using a BatchSize
ctx.Users.Where(x => x.LastLoginDate < DateTime.Now.AddYears(-2))
         .Delete(x => x.BatchSize = 1000);
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
|[EntityFramework.Extended](https://github.com/zzzprojects/EntityFramework.Extended)	|FREE	|EF5<br>EF6	|No	    |Yes    |Audit<br>Batch Delete<br>Batch Update<br>Cache<br>Future|

