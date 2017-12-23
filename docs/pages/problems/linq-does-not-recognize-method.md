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

 - [Why LINQ to Entities does not recognize the method 'System.String ToString()?](https://stackoverflow.com/questions/10110266/why-linq-to-entities-does-not-recognize-the-method-system-string-tostring)
 - [LINQ to Entities does not recognize the method 'System.String Format(System.String, System.Object, System.Object)'](https://stackoverflow.com/questions/10079990/linq-to-entities-does-not-recognize-the-method-system-string-formatsystem-stri)
 - [LINQ to Entities does not recognize the method 'System.String ToString()' method, and this method cannot be translated into a store expression](https://stackoverflow.com/questions/5899683/linq-to-entities-does-not-recognize-the-method-system-string-tostring-method)

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
