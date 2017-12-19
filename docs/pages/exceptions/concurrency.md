---
permalink: concurrency
---

## Store update, insert, or delete statement affected an unexpected number of rows (0)

A concurrency conflict occurs when one user displays an entity's data in order to edit it, and then another user updates or deletes the same entity's data before the first user's change is written to the database. 

Another for this exception is when a new object is created and and it's state is set to modified the EntityState.Modified.

{% include template-example.html %} 
{% highlight csharp %}

using (var context = new CustomerContext())
{
    var customer = new Customer();
    // ...code...

    context.Entry(customer).State = EntityState.Modified;
    context.SaveChanges();
}

{% endhighlight %}

### StackOverflow Related Questions

 - [Entity Framework: Store update, insert, or delete statement affected an unexpected number of rows (0).](https://stackoverflow.com/questions/1836173/entity-framework-store-update-insert-or-delete-statement-affected-an-unexpec)

## Solution

The easiest solution to handle this exception is to set the state of the entity to **Added** instead of **Modified**.

{% include template-example.html %} 
{% highlight csharp %}

using (var context = new CustomerContext())
{
    var customer = new Customer();
    // ...code...

    context.Entry(customer).State = EntityState.Added;
    context.SaveChanges();
}

{% endhighlight %}

The entity can be added directly to the database by using the DbSet.Add method.

{% include template-example.html %} 
{% highlight csharp %}

using (var context = new CustomerContext())
{
    var customer = new Customer();
    // ...code...

    ctx.Customers.Add(customer);
    context.SaveChanges();
}

{% endhighlight %}
