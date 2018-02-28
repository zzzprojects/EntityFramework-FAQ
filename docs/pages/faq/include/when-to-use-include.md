---
permalink: when-to-use-include
---

## When to use Include() with Entity Framework? 

When to use Include with Entity Framework and is it related to lazy loading?

## Answer

Before jumping into the answer of when to use Include, let's have a look at the following simple example which contains three entities.

{% include template-example.html %} 
{% highlight csharp %}

public class Customer
{
    [Key]
    public int Id { get; set; }
    public string Name { get; set; }
    public virtual ICollection<Invoice> Invoices { get; set; }
}

public class Invoice
{
    public int Id { get; set; }
    public DateTime Date { get; set; }
    public virtual ICollection<Item> Items { get; set; }
    public int CustomerId { get; set; }
    public virtual Customer Customer { get; set; }
}

public class Item
{
    public int Id { get; set; }
    public string ItemName { get; set; }
    public int InvoiceId { get; set; }
    public virtual Invoice Invoice { get; set; }
}

{% endhighlight %}

 - Lazy loading is the process whereby an entity or collection of entities is automatically loaded from the database. 
 - Lazy loading is enabled by default in Entity Framework, and we can mark specific navigation properties or even whole entities as lazy by making them virtual.

Now let's retrieve all the customers from a database and also iterate over their invoices as well and then print the invoice date.

{% include template-example.html %} 
{% highlight csharp %}

using (var context = new MyContext())
{
    var list = context.Customers.ToList();
    foreach (var customer in list)
    {
        Console.WriteLine("Customer Name: {0}", customer.Name);
        foreach (var customerInvoice in customer.Invoices)
        {
            Console.WriteLine("\tInvoice Date: {0}", customerInvoice.Date);
        }
    }
}

{% endhighlight %}

If you look at the generated SQL, then you will see that one SQL query is executed for retrieving customers and then for each customer, another query is executed for retrieving the Invoices related to that customer. So, it means, if you have 1000 customers in your database then EF will execute 1000 queries for retrieving invoices for that 1000 customers.

EF generates the following query for retrieving customers.

{% include template-example.html %} 
{% highlight csharp %}

SELECT
    [Extent1].[Id] AS [Id],
    [Extent1].[Name] AS [Name]
    FROM [dbo].[Customers] AS [Extent1]

{% endhighlight %}

And the following query is generated for retrieving invoices of a specific customer.

{% include template-example.html %} 
{% highlight csharp %}
SELECT
    [Extent1].[Id] AS [Id],
    [Extent1].[Date] AS [Date],
    [Extent1].[CustomerId] AS [CustomerId]
    FROM [dbo].[Invoices] AS [Extent1]
    WHERE [Extent1].[CustomerId] = @EntityKeyValue1

{% endhighlight %}

 - Lazy loading is a great mechanism but only if you know when and how to use it. 
 - But look at our example again. Now if you look at this example, then you will see the **select N+1 problem.** 
 - The problem is happening because the Lazy loading is enabled by default and when we are executing a single query and then N following queries (N is the number of parent entities) to query for something. 

The best way to avoid the select N+1 problem in Entity Framework is to use the Include method. It will create one query with needed data using SQL JOIN clause which is more efficient as compared to the previous one.

Let's update our query by using the Include method.

{% include template-example.html %} 
{% highlight csharp %}

using (var context = new MyContext())
{
    var list = context.Customers
        .Include(c => c.Invoices)    
        .ToList();    
    
    foreach (var customer in list)
    {
        Console.WriteLine("Customer Name: {0}", customer.Name);
        foreach (var customerInvoice in customer.Invoices)
        {
            Console.WriteLine("\tInvoice Date: {0}", customerInvoice.Date);
        }
    }
}

{% endhighlight %}

In the above example, we are telling EF explicitly that besides Customers we also need their Invoices. The following is the SQL generated query:

{% include template-example.html %} 
{% highlight csharp %}

SELECT
    [Project1].[Id] AS [Id],
    [Project1].[Name] AS [Name],
    [Project1].[C1] AS [C1],
    [Project1].[Id1] AS [Id1],
    [Project1].[Date] AS [Date],
    [Project1].[CustomerId] AS [CustomerId]
    FROM ( SELECT
        [Extent1].[Id] AS [Id],
        [Extent1].[Name] AS [Name],
        [Extent2].[Id] AS [Id1],
        [Extent2].[Date] AS [Date],
        [Extent2].[CustomerId] AS [CustomerId],
        CASE WHEN ([Extent2].[Id] IS NULL) THEN CAST(NULL AS int) ELSE 1 END AS [C1]
        FROM  [dbo].[Customers] AS [Extent1]
        LEFT OUTER JOIN [dbo].[Invoices] AS [Extent2] ON [Extent1].[Id] = [Extent2].[CustomerId]
    )  AS [Project1]
    ORDER BY [Project1].[Id] ASC, [Project1].[C1] ASC

{% endhighlight %}

As you can see that Entity Framework has used `LEFT OUTER JOIN` clause to get all needed data. Another important point is that using Include method in the context which supports lazy loading can prevent the n+1 problem.