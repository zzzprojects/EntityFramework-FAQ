---
permalink: check-object-existence
---

## How to check if an object exists in the database?

What is the best way performance wise to check if object exists in the database. 

### StackOverflow Related Questions

 - [Best way to check if object exists in Entity Framework?](https://stackoverflow.com/questions/1802286/best-way-to-check-if-object-exists-in-entity-framework)


## Answer

For IEnumerable<T>, using **Any()** method is generally the fastest way to check if object exists in the database. It only has to look at one iteration and will return as soon as it finds a match.

{% include template-example.html %} 
{% highlight csharp %}
using (var context = new CustomerContext())
{
    if(context.Customers.Any(c => c.Id == 1))
    {
        //match
    }  
}
{% endhighlight %}