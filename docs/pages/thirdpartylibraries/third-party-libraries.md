---
permalink: third-party-libraries
---

## Introduction

Entity Framework **Third Party Libraries** allow you to extend EF functionality which is not available in the official Entity Framework library, for example, auditing, caching, and filtering etc. 

## Why we need Third Party Libraries?

Entity Framework is great, but a lot of essential features is missing for some application scenarios.

The only way to achieve is either create code for this kind of scenario or use a library which fully or partially cover them.

## Supported Libraries


|Library	|Type	|EF Version	|Support	|Doc	|Features|
|:----------|:----------|:----------|:----------|:----------|:----------|
|[Z.EntityFramework.Extensions](/ef-extesnsions)	|PRO	|EF6	|< 1 Day	|Yes	| Bulk SaveChanges<br>Bulk Insert<br>Bulk Update<br>Bulk Delete<br>Bulk Merge|
|[Z.EntityFramework.Plus](/ef-plus)	|FREE	|EF5<br>EF6<br>EF Core|	< 1 Day	|Yes    |Audit<br>Batch Delete<br>Batch Update<br>Cache<br>Deferred Query<br>Filter<br>Future<br>Include Filter<br>Include Optimized|
|[Eval Expression.NET](https://github.com/zzzprojects/Eval-Expression.NET/wiki/LINQ-Dynamic)	|FREE/PRO	|All	|< 1 Day	|Yes	|Dynamic Query|
|[Audit.NET](https://github.com/thepirat000/Audit.NET)	|FREE	|EF6<br>EF Core	|< 1 Day	|Yes    |Audit  |
|[System.Linq.Dynamic](https://github.com/kahanu/System.Linq.Dynamic)	|FREE	|All	|< 1 Day	|Yes    |Dynamic Query  |
|[EntityFramework.Cache](https://github.com/moozzyk/EFCache)	|FREE	|EF6	|< 2 Days	|No	    | Cache |
|[EntityFramework.DynamicFilters](https://github.com/zzzprojects/EntityFramework.DynamicFilters)	|FREE	|EF6	|< 2 Days	|Yes    |Filter |
|[Microsoft.EntityFrameworkCore.AutoHistory](https://github.com/Arch/AutoHistory)	|FREE	|EF Core	|< 1 Day	|No	    | Audit |

## Unsuported Library

Use these libraries at your risk!

|Library	|Type	|EF Version	|Support	|Doc	|Features |
|:--------- |:--------- |:--------- |:--------- |:--------- |:--------- |
|[AuditDbContext](https://auditdbcontext.codeplex.com/)	|FREE	|EF6	|No |Yes    |Audit  |
|[EFAuditing](https://github.com/johannbrink/EFAuditing)	|FREE	|EF Core	|No	    |No |Audit  |
|[EFUtilities](https://github.com/MikaelEliasson/EntityFramework.Utilities)	|FREE	|EF5<br>EF6	|No	    |No |Bulk Insert<br>Batch Delete<br>Batch Update<br>Include Optimized<br>
|[EntityFramework.Extended](https://github.com/zzzprojects/EntityFramework.Extended)	|FREE	|EF5<br>EF6	|No	    |Yes    |Audit<br>Batch Delete<br>Batch Update<br>Cache<br>Future|
|[EntityFramework.Filters](https://github.com/jbogard/EntityFramework.Filters)	|FREE	|EF6	|No	    |Yes    |Filter |
|[EntityFramework.MappingAPI](https://efmappingapi.codeplex.com/)	|FREE	|EF6	|No	    |No     |Model API  |
|[TrackerEnabledDbContext](https://github.com/bilal-fazlani/tracker-enabled-dbcontext)	|FREE	|EF6	|No	    |Yes	|Audit  |
|[EntityFramework.BulkInsert](https://efbulkinsert.codeplex.com/)	|FREE	|EF5<br>EF6    |No	    |Yes    |Bulk Insert |