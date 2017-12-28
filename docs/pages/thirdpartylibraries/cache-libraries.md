---
permalink: cache-libraries
---

## Introduction

Cache library allow you to cache the result of a LINQ query, usually in the memory, and re-use the cached result for subsequent calls.

## Why Cache?

### Common Scenarios:

 - Cache read-only table like countries and states
 - Cache rarely modified table (most libraries allow cache expiration)
 - Cache information related to the user logged

## Google Related Searches

 - [Entity Framework Caching Data](https://www.google.com/search?q=entity+framework+caching+data)
 - [Entity Framework First Level Cache](https://www.google.com/search?q=entity+framework+first+level+cache)
 - [Entity Framework Second Level Cache](https://www.google.com/search?q=entity+framework+second+level+cache)

## StackOverflow Related Questions

 - [Entity Framework flexible cache](https://stackoverflow.com/questions/38527253/entity-framework-flexible-cache)
 - [Entity Framework second level cache](https://stackoverflow.com/questions/35549009/entity-framework-second-level-cache)


{% include template-example.html %} 
{% highlight csharp %}
// using Z.EntityFramework.Plus; // Don't forget to include this.
var ctx = new EntitiesContext();

// The first call perform a database round trip
var countries1 = ctx.Countries.FromCache().ToList();

// Subsequent calls will take the value from the memory instead
var countries2 = ctx.Countries.FromCache().ToList();

{% endhighlight %}

## Supported Libraries

|Library	|Type	|EF Version	|Support	|Doc	|Features|
|:----------|:----------|:----------|:----------|:----------|:----------|
|[Z.EntityFramework.Plus](http://entityframework-plus.net/)	|FREE	|EF5<br>EF6<br>EF Core|	< 1 Day	|Yes    |Audit<br>Batch Delete<br>Batch Update<br>Cache<br>Deferred Query<br>Filter<br>Future<br>Include Filter<br>Include Optimized|
|[EntityFramework.Cache](https://github.com/moozzyk/EFCache)	|FREE	|EF6	|< 2 Days	|No	    | Cache |

## Unsuported Library

Use these libraries at your risk!

|Library	|Type	|EF Version	|Support	|Doc	|Features |
|:--------- |:--------- |:--------- |:--------- |:--------- |:--------- |
|[EntityFramework.Extended](https://github.com/zzzprojects/EntityFramework.Extended)	|FREE	|EF5<br>EF6	|No	    |Yes    |Audit<br>Batch Delete<br>Batch Update<br>Cache<br>Future|
