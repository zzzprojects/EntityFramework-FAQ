# ComplexType

The Complex types are non-scalar properties of entity types that enable scalar properties to be organized within entities. 

 - `ComplexType` doesn't have keys and therefore cannot exist independently. 
 - It can only exist as properties of entity types or other complex types.
 - It cannot participate in associations and cannot contain navigation properties.
 - Complex type properties cannot be null. 
 - Scalar properties of complex objects can be null.


The following example maps the `BookTitle` property in the Book entity to a database column named `Title`.

```csharp
public class Book
{
    public int BookId { get; set; }
    [Column("Title")]
    public string BookTitle { get; set; }
}
```

[Try it](https://dotnetfiddle.net/Rh3pAR)
