---
permalink: ef-dynamic-filters 
---

## Definition

**Entity Framework Dynamic Filters** is a library that Creates global and scoped filters for Entity Framework queries.

The filters are automatically applied to every query and can be used to support use cases such as Multi-Tenancy, Soft Deletes, Active/Inactive, etc.

## How It Works?

The library will add extensions methods automatically to DbContext and DbModelBuilder classes to access **Dynamic Filters**.

- Filters are defined in DbContext.OnModelCreating().
- Filters can be created using boolean LINQ expressions.
- It also supports the Contains() operator to define filters.

Filters can be defined on a specific entity class or an interface by providing a specific value.

{% include template-example.html%} 
{% highlight csharp %}

modelBuilder.Filter("IsDeleted", (ISoftDelete d) => d.IsDeleted, false);

{% endhighlight %}

This filter will apply to all classes that implements ISoftDelete.

## Enabling and Disabling Filters

Filter can be easily disabled by using the DbContext.DisableFilter extension method. To disable a filter globally, use DbModelBuilder.DisableFilterGlobally method after it is created in OnModelCreating

{% include template-example.html%} 
{% highlight csharp %}

context.DisableFilter("IsDeleted");

//Disable a filter globally
modelBuilder.DisableFilterGlobally("IsDeleted");

{% endhighlight %}

You can also enable/disable all filters at once within a context. 

{% include template-example.html%} 
{% highlight csharp %}

context.DisableAllFilters();
context.EnableAllFilters();

{% endhighlight %}

## Conditionally Enabling Filters

Filters can also be enabled conditionally and you will even need to define those conditions along with your filter definition.

{% include template-example.html%} 
{% highlight csharp %}

modelBuilder.Filter("BlogEntryFilter", (BlogEntry b, Guid accountID) => (b.AccountID == accountID), 
                    () => GetPersonIDFromPrincipal(Thread.CurrentPrincipal));
modelBuilder.EnableFilter("BlogEntryFilter", () => !UserIsAdmin(Thread.CurrentPrincipal));

{% endhighlight %}

In this example, a filter is defined on BlogEntry records to restrict to only the current AccountID. But the filter will only be enabled if the user is not an Admin user.

## Requirements

### Entity Framework Version

 - Entity Framework Core 2.x
 - Entity Framework 6.x

[Learn more](http://entityframework-dynamicfilters.net/overview)
