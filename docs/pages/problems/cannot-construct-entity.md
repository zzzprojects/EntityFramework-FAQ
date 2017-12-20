---
permalink: cannot-construct-entity
---

## Exception: The entity cannot be constructed in a LINQ to Entities query

In Entity Framework, mapped entities represent database tables, and Entity Framework doesn't allow to project on a mapped entity in a LINQ to Entities query.  If you project on a mapped entity, then it will partially load an entity, which is not a valid state. EF won't have any clue how to handle when the entity is updated. 

{% include template-example.html %} 
{% highlight csharp %}
using (var context = new CustomerContext())
{
    var customer = context.Customers.Where(c => c.Id == 1)
        .Select(c => new Customer()
        {
            Name = c.Name
        })
        .FirstOrDefault();
}

{% endhighlight %}

### StackOverflow Related Questions

 - [The entity cannot be constructed in a LINQ to Entities query](https://stackoverflow.com/questions/5325797/the-entity-cannot-be-constructed-in-a-linq-to-entities-query)
 - ["The entity or complex type cannot be constructed in a LINQ to Entities query" in Controler](https://stackoverflow.com/questions/31920656/the-entity-or-complex-type-cannot-be-constructed-in-a-linq-to-entities-query-i)

## Answer

### Anonymous Type

The most straightforward solution to handle this exception is to project on anonymous type.

{% include template-example.html %} 
{% highlight csharp %}

using (var context = new CustomerContext())
{
    var customer = context.Customers.Where(c => c.Id == 1)
        .Select(c => new 
        {
            Name = c.Name
        })
        .FirstOrDefault();
}

{% endhighlight %}

### DTO
You can also project on Data Transfer Objects (DTO)

{% include template-example.html %} 
{% highlight csharp %}

using (var context = new CustomerContext())
{
    var customer = context.Customers.Where(c => c.Id == 1)
        .Select(c => new CustomerDTO()
        {
            Name = c.Name
        })
        .FirstOrDefault();
}

{% endhighlight %}

The DTO class will look like this.

{% include template-example.html %} 
{% highlight csharp %}

public class CustomerDTO
{
    public string Name { get; set; }
}

{% endhighlight %}

### Anonymous Type to Strongly Type

Another way of handling this problem is to project into anonymous type first and then map anonymous type to mapped entity or model entity.

{% include template-example.html %} 
{% highlight csharp %}

using (var context = new CustomerContext())
{
    var customers = context.Customers.Where(c => c.Name.StartsWith("J"))
        .Select(c => new
        {
            Name = c.Name
        })
        .ToList()
        .Select(x => new Customer { Name = x.Name })
        .ToList();
}

{% endhighlight %}
