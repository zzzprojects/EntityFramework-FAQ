---
permalink: why-first-query-slow
---

## Why Entity Framework First Load is Slow?

Entity framework is very slow to load for the first time after every compilation especially when you have a large model.

## Answer

Entity Framework loads very slow for the first time because on the first query EF compiles the model. To speed up your application startup time here are three suggestions mentioned in this [post](https://www.fusonic.net/en/blog/3-steps-for-fast-entityframework-6.1-code-first-startup-performance/).

 - Using a Cached DbModelStore
 - Generate pre-compiled Views
 - Generate pre-compiled version of entity framework using NGen to avoid jitting

### Using a Cached DbModelStore

It will cache the code-first pipeline mapping and store it in a XML file. The next time your application starts, EF will deserialize this cached mapping file which significantly reduces startup time. The cached DbModelStore can be enabled with the following lines of code.

{% include template-example.html %} 
{% highlight csharp %}
public class MyContextConfiguration : DbConfiguration
{
    public MyContextConfiguration()
    {
        MyDbModelStore cachedDbModelStore = new MyDbModelStore(MyContext.EfCacheDirPath);
        IDbDependencyResolver dependencyResolver = new SingletonDependencyResolver<DbModelStore>(cachedDbModelStore);
        AddDependencyResolver(dependencyResolver);
    }

    private class MyDbModelStore : DefaultDbModelStore
    {
        public MyDbModelStore(string location)
            : base(location)
        {}

        public override DbCompiledModel TryLoad(Type contextType)
        {
            string path = GetFilePath(contextType);
            if(File.Exists(path))
            {
                DateTime lastWriteTime = File.GetLastWriteTimeUtc(path);
                DateTime lastWriteTimeDomainAssembly = File.GetLastWriteTimeUtc(typeof(MyDomain.SomeTypeInOurDomain).Assembly.Location);
                if (lastWriteTimeDomainAssembly > lastWriteTime)
                {
                    File.Delete(path);
                    Tracers.EntityFramework.TraceInformation("Cached db model obsolete. Re-creating cached db model edmx.");
                }
            }
            else
            {
                Tracers.EntityFramework.TraceInformation("No cached db model found. Creating cached db model edmx.");
            }

            return base.TryLoad(contextType);
        }
    }
}
{% endhighlight %}

[Learn more about Cached DbModelStore](https://gist.github.com/davidroth/9886349)

### Generate Pre-compiled Views

View generation can have a significant enhancement on startup performance, so caching this step is a must to achieve good EF startup performance. There are different ways to generate and store pre-compiled views such as;

 - [Entity Framework Pre-Generated Mapping Views](https://msdn.microsoft.com/en-us/library/dn469601%28v=vs.113%29.aspx?f=255&MSPPError=-2147217396)
 - [EFInteractiveViews](https://github.com/moozzyk/EFInteractiveViews)

### Generate Pre-compiled Version of EF Using NGen

Entity Framework does not come in the default installation of the .net Framework. Therefore, the EF assembly is not NGEN'd by default which means that EF code needs to be JITTED each time the application starts.

[Learn more about Entity Framework 6 and NGEN](https://msdn.microsoft.com/tr-tr/data/dn582034?f=255&MSPPError=-2147217396)
