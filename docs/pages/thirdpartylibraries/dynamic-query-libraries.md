---
permalink: dynamic-query-libraries
---

## Introduction

Dynamic Query allows you to perform dynamic where clause, select, order by, with string expression at runtime.

## Why Dynamic Query?

### Common Scenarios:

 - Use dynamic select clause with string expression
 - Use dynamic order by with string expression
 - Use dynamic where clause with string expression

## Google Related Searches

 - [Entity Framework Dynamic LINQ](https://www.google.com/search?q=entity+framework+dynamic+linq)
 - [Entity Framework Dynamic Where Clause](https://www.google.com/search?q=entity+framework+dynamic+where+clause)
 - [Entity Framework OrderBy String](https://www.google.com/search?q=entity+framework+orderby+string)

## StackOverflow Related Questions

 - [Building dynamic where clauses in LINQ to EF queries](https://stackoverflow.com/questions/14901430/building-dynamic-where-clauses-in-linq-to-ef-queries)
 - [Dynamic LINQ OrderBy on IEnumerable< T >](https://stackoverflow.com/questions/41244/dynamic-linq-orderby-on-ienumerablet?rq=1)
 - [How to Dynamically build Select as relates to Linq & Entity Framework](https://stackoverflow.com/questions/44441338/how-to-dynamically-build-select-as-relates-to-linq-entity-framework)
 - [Using dynamic linq in EF Linq to Entities](https://stackoverflow.com/questions/28721888/using-dynamic-linq-in-ef-linq-to-entities)

{% include template-example.html %} 
{% highlight csharp %}
var customersList1 = context.Customers
    .OrderByDynamic(c => "c.Name")
    .ToList();

var customersList2 = context.Customers
    .Include(x => x.Invoices)
    .Where(c => "c.Invoices.Count > 0")
    .OrderByDescendingDynamic(c => "c.Invoices.Count")
    .ToList();

{% endhighlight %}

## Supported Libraries

|Library	|Type	|EF Version	|Support	|Doc	|Features|
|:----------|:----------|:----------|:----------|:----------|:----------|
|[Eval Expression.NET](https://github.com/zzzprojects/Eval-Expression.NET/wiki/LINQ-Dynamic)	|FREE/PRO	|All	|< 1 Day	|Yes	|Dynamic Query|
|[System.Linq.Dynamic](https://github.com/kahanu/System.Linq.Dynamic)	|FREE	|All	|< 1 Day	|Yes    |Dynamic Query  |
