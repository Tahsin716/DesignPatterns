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

public class Client {
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