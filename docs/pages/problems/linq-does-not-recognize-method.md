---
permalink: linq-does-not-recognize-method
---

## Exception: LINQ to Entities does not recognize the method 

It is the most common exception occurs when working with entity framework and converting data inside IQueryable result for filtering. 


{% include template-example.html %} 
{% highlight csharp %}
using (var context = new CustomerContext())
{
    var item = context.InvoiceItems
        .Where(i => i.Code == code.ToString())
        .FirstOrDefault();
}

{% endhighlight %}

### StackOverflow Related Questions


## Solution

There are different solutions for this specific problem.

### Move ToString() call to a separate line.

{% include template-example.html %} 
{% highlight csharp %}
using (var context = new CustomerContext())
{
    string codeStr = code.ToString();
    var item = context.InvoiceItems
        .Where(i => i.Code == codeStr)
        .FirstOrDefault();
}

{% endhighlight %}

### Use EF Extension Method,

{% include template-example.html %} 
{% highlight csharp %}
using (var context = new CustomerContext())
{
    var item = context.InvoiceItems
        .Where(i => i.Code == SqlFunctions.StringConvert(code))
        .FirstOrDefault();
}
{% endhighlight %}

### Convert IQueryable result to IEnumerable before Filtering

{% include template-example.html %} 
{% highlight csharp %}
using (var context = new CustomerContext())
{
    var item = context.InvoiceItems.AsEnumerable()
        .Where(i => i.Code == code.ToString())
        .FirstOrDefault();
}
{% endhighlight %}
