---
permalink: use-linq-dynamically
---

## How to use LINQ dynamically? 

LINQ enables you to write type-safe queries, and you will get compile-time checking of your LINQ queries. The type-safe queries are excellent for most scenarios, but there are some cases where you will need the flexibility to construct queries on the fly dynamically. 

For example, we have a very simple case where we want to sort customers, but we don't know how we want to order it until we actually get to runtime. So it's something the user clicks on or types in of how they want to order something. There's no way a compile time can formulate that.

### StackOverflow Related Questions

- [Dynamically generate LINQ queries](https://stackoverflow.com/questions/9505189/dynamically-generate-linq-queries)
- [Dynamic WHERE clause in LINQ]()

## Answer

One way to sort the customers is that you could write big switch statements that are depending on the user input and wrote a different lambda expression for each case of the switch statement that would set the ORDER BY and that's difficult and becomes difficult to maintain in the long run too.

### Dynamic Query Library

Traditionally these types of dynamic query scenarios are often handled by concatenating strings together to construct dynamic SQL queries. Dynamic Query Library provided by the LINQ team constructs LINQ queries dynamically.

It allows you to express LINQ queries using extension methods that take string arguments instead of type-safe language operators.  

{% include template-example.html %} 
{% highlight csharp %}
using (var context = new CustomerContext())
{
    var customersList1 = context.Customers
        .OrderBy("Name")
        .ToList();
    
    var customersList2 = context.Customers
        .Include(x => x.Invoices)
        .OrderBy("Invoices.Count descending")
        .ToList();    
}

{% endhighlight %}

### Eval-Expression.NET

[Eval-Expression.NET](https://github.com/zzzprojects/Eval-Expression.NET) library allows you to evaluate, compile, and execute C# code and as well as an expression at runtime. The library also contains extension method for dynamic LINQ.

{% include template-example.html %} 
{% highlight csharp %}
using (var context = new CustomerContext())
{
    var invoices = context.Invoices
        .Where(i => "i.Items.Count > 0")
        .ToList();    
}

{% endhighlight %}

#### OrderByDynamic and OrderByDescendingDynamic

{% include template-example.html %} 
{% highlight csharp %}
using (var context = new CustomerContext())
{
    var customersList1 = context.Customers
        .OrderByDynamic(c => "c.Name")
        .ToList();
    
    var customersList2 = context.Customers
        .Include(x => x.Invoices)
        .Where(c => "c.Invoices.Count > 0")
        .OrderByDescendingDynamic(c => "c.Invoices.Count")
        .ToList();    
}

{% endhighlight %}

[Learn more](https://github.com/zzzprojects/Eval-Expression.NET/wiki/LINQ-Dynamic)
