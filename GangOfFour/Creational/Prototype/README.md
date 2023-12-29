# Prototype

### What is the Prototype Design Pattern?

Prototype Design Pattern is a creational pattern used to create new objects by copying an existing object, known as a prototype.

### What problem does Prototype Design Pattern aim to solve?

The pattern is particularly useful when the cost of creating an object is more expensive than copying an existing one, or when the initial state of an object needs to be preserved.

## Different implementations of Prototype Design Pattern

### 1. Shallow Copy

Copies the object and its primitive member variables. If the object contains references to other objects, the references are shared between the original and the clone.

`java`
```java
// Prototype interface
interface Prototype {
    Prototype clone();
}

// Address class
class Address {
    private String city;
    private String zipCode;

    public Address(String city, String zipCode) {
        this.city = city;
        this.zipCode = zipCode;
    }

    @Override
    public String toString() {
        return "Address{city='" + city + "', zipCode='" + zipCode + "'}";
    }
}

// Person class with a reference to Address
class Person implements Prototype {
    private String name;
    private int age;
    private Address address;

    public Person(String name, int age, Address address) {
        this.name = name;
        this.age = age;
        this.address = address;
    }

    // Shallow copy constructor
    private Person(Person source) {
        this.name = source.name;
        this.age = source.age;
        this.address = source.address; // Shallow copy of Address reference
    }

    @Override
    public Prototype clone() {
        return new Person(this);
    }

    @Override
    public String toString() {
        return "Person{name='" + name + "', age=" + age + ", address=" + address + "}";
    }
}

class Client {
    public static void main(String[] args) {
        // Original person
        Address originalAddress = new Address("City1", "12345");
        Person originalPerson = new Person("John", 25, originalAddress);

        System.out.println("Original Person: " + originalPerson);

        // Shallow copy
        Person clonedPerson = (Person) originalPerson.clone();
        System.out.println("Cloned Person: " + clonedPerson);

        // Modify the address in the cloned person
        clonedPerson.address = new Address("City2", "67890");

        // Print the original person to show that the address is shared
        System.out.println("Original Person after modifying clone: " + originalPerson);
    }
}

```

`csharp`
```csharp
// Prototype interface
public interface IPrototype
{
    IPrototype Clone();
}

// Address class
public class Address
{
    public string City { get; set; }
    public string ZipCode { get; set; }

    public Address(string city, string zipCode)
    {
        City = city;
        ZipCode = zipCode;
    }

   
    public override string ToString()
    {
        return $"Address{{City='{City}', ZipCode='{ZipCode}'}}";
    }
}

// Person class with a reference to Address
public class Person : IPrototype
{
    public string Name { get; set; }
    public int Age { get; set; }
    public Address Address { get; set; }

    public Person(string name, int age, Address address)
    {
        Name = name;
        Age = age;
        Address = address;
    }

    private Person(Person source)
    {
        Name = source.Name;
        Age = source.Age;
        Address = source.Address // Shallow copy of Address
    }

    // Shallow copy method
    public IPrototype Clone()
    {
        return new Person(this);
    }

    public override string ToString()
    {
        return $"Person{{Name='{Name}', Age={Age}, Address={Address}}}";
    }
}

class Client
{
    static void Main()
    {
        // Original person
        Address originalAddress = new Address("City1", "12345");
        Person originalPerson = new Person("John", 25, originalAddress);

        Console.WriteLine("Original Person: " + originalPerson);

        // Shallow copy
        Person clonedPerson = (Person)originalPerson.Clone();
        Console.WriteLine("Cloned Person: " + clonedPerson);

        // Modify the address in the cloned person
        clonedPerson.Address = new Address("City2", "67890");

        // Print the original person to show that the address is shared
        Console.WriteLine("Original Person after modifying clone: " + originalPerson);
    }
}

```

### 2. Deep Copy

Creates a new object and recursively copies all referenced objects. The clone and the original have no shared references to objects.

`java`
```java
// Prototype interface
interface Prototype {
    Prototype clone();
}

// Address class
class Address implements Prototype {
    private String city;
    private String zipCode;

    public Address(String city, String zipCode) {
        this.city = city;
        this.zipCode = zipCode;
    }

    // Deep copy constructor
    private Address(Address source) {
        this.city = source.city;
        this.zipCode = source.zipCode;
    }

    @Override
    public Prototype clone() {
        return new Address(this);
    }

    @Override
    public String toString() {
        return "Address{city='" + city + "', zipCode='" + zipCode + "'}";
    }
}

// Person class with a reference to Address
class Person implements Prototype {
    private String name;
    private int age;
    private Address address;

    public Person(String name, int age, Address address) {
        this.name = name;
        this.age = age;
        this.address = address;
    }

    // Deep copy constructor
    private Person(Person source) {
        this.name = source.name;
        this.age = source.age;
        this.address = (Address) source.address.clone(); // Deep copy of Address
    }

    @Override
    public Prototype clone() {
        return new Person(this);
    }

    @Override
    public String toString() {
        return "Person{name='" + name + "', age=" + age + ", address=" + address + "}";
    }
}

class Client {
    public static void main(String[] args) {
        // Original person
        Address originalAddress = new Address("City1", "12345");
        Person originalPerson = new Person("John", 25, originalAddress);

        System.out.println("Original Person: " + originalPerson);

        // Deep copy
        Person clonedPerson = (Person) originalPerson.clone();
        System.out.println("Cloned Person: " + clonedPerson);

        // Modify the address in the cloned person
        clonedPerson.address = new Address("City2", "67890");

        // Print the original person to show that the address is not shared
        System.out.println("Original Person after modifying clone: " + originalPerson);
    }
}
```

`csharp`
```csharp
// Prototype interface
public interface IPrototype
{
    IPrototype Clone();
}

// Address class
public class Address : IPrototype
{
    public string City { get; set; }
    public string ZipCode { get; set; }

    public Address(string city, string zipCode)
    {
        City = city;
        ZipCode = zipCode;
    }

    // Deep copy constructor
    private Address(Address source)
    {
        City = source.City;
        ZipCode = source.ZipCode;
    }

    // Deep copy method
    public IPrototype Clone()
    {
        return new Address(this);
    }

    public override string ToString()
    {
        return $"Address{{City='{City}', ZipCode='{ZipCode}'}}";
    }
}

// Person class with a reference to Address
public class Person : IPrototype
{
    public string Name { get; set; }
    public int Age { get; set; }
    public Address Address { get; set; }

    public Person(string name, int age, Address address)
    {
        Name = name;
        Age = age;
        Address = address;
    }

    // Deep copy constructor
    private Person(Person source)
    {
        Name = source.Name;
        Age = source.Age;
        Address = (Address) source.Address.Clone(); // Deep copy of address
    }

    // Deep copy method
    public IPrototype Clone()
    {
        return new Person(this);
    }

    public override string ToString()
    {
        return $"Person{{Name='{Name}', Age={Age}, Address={Address}}}";
    }
}

class Client
{
    static void Main()
    {
        // Original person
        Address originalAddress = new Address("City1", "12345");
        Person originalPerson = new Person("John", 25, originalAddress);

        Console.WriteLine("Original Person: " + originalPerson);

        // Deep copy
        Person clonedPerson = (Person)originalPerson.Clone();
        Console.WriteLine("Cloned Person: " + clonedPerson);

        // Modify the address in the cloned person
        clonedPerson.Address = new Address("City2", "67890");

        // Print the original person to show that the address is not shared
        Console.WriteLine("Original Person after modifying clone: " + originalPerson);
    }
}

```
