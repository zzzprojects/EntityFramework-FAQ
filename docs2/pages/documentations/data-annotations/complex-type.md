# ComplexType

The Complex types are non-scalar properties of entity types that enable scalar properties to be organized within entities. 

 - `ComplexType` doesn't have keys and therefore cannot exist independently. 
 - It can only exist as properties of entity types or other complex types.
 - It cannot participate in associations and cannot contain navigation properties.
 - Complex type properties cannot be null. 
 - Scalar properties of complex objects can be null.


The following example maps the `BookTitle` property in the Book entity to a database column named `Title`.

```csharp
public class Author
{
    public int AuthorId { get; set; }
    public string Name { get; set; }
    public Address Address { get; set; }
}

[ComplexType]
public class Address
{
    public string City { get; set; }
    public string Street { get; set; }
    public string StateOrProvince { get; set; }
    public string Country { get; set; }
}
```

[Try it](https://dotnetfiddle.net/Rh3pAR)
