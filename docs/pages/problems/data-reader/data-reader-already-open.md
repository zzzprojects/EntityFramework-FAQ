---
permalink: data-reader-already-open
---

## Exception: There is already an open DataReader associated with this Command which must be closed first

When executing the following code.

{% include template-example.html %} 
{% highlight csharp %}

foreach (var blog in blogs)
{
    blog.Name += " updated";
    blog.Url += " updated";
    context.SaveChanges();
}

{% endhighlight %}

It gives the following exception.

`InvalidOperationException: There is already an open DataReader associated with this Command which must be closed first.`

### StackOverflow Related Questions

 - [There is already an open DataReader associated with this Command which must be closed first](https://stackoverflow.com/questions/6062192/there-is-already-an-open-datareader-associated-with-this-command-which-must-be-c)

## Solution
This can happen if you execute a query while iterating over the results from another query.

### Solution 1

 - This can be easily solved by allowing MARS in your connection string. 
 - Add `MultipleActiveResultSets=true` to the provider part of your connection string.

<connectionStrings>
    <add name="BloggingContextDb" connectionString="Data Source=(localdb)\ProjectsV13;Initial Catalog=BloggingContextDb;
            Integrated Security=True;Connect Timeout=30;Encrypt=False;TrustServerCertificate=True;ApplicationIntent=ReadWrite;
            MultiSubnetFailover=False;MultipleActiveResultSets=true;" providerName="System.Data.SqlClient" />
</connectionStrings>

 - Enabling MARS should only be done for a very small subset of problems/use-cases. 
 - In most cases, the error is caused by BAD CODE within the calling application. 

### Solution 2

Adding .ToList() to the collection using in foreach loop will likely solve the problem.

{% include template-example.html %} 
{% highlight csharp %}

var blogList = blogs.ToList();
foreach (var blog in blogList)
{
    blog.Name += " updated";
    blog.Url += " updated";
    context.SaveChanges();
}

{% endhighlight %}

### Solution 3

Call SaveChanges() outside foreach loop

{% include template-example.html %} 
{% highlight csharp %}

foreach (var blog in blogs)
{
    blog.Name += " updated";
    blog.Url += " updated";
}
context.SaveChanges();

{% endhighlight %}

