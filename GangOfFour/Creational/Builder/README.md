# Builder

### What is a Builder Design Pattern?

Builder Design Pattern is a creational pattern to create complex objects piecewise and succinctly.

### What problem does the Builder Pattern aim to solve?

The Builder Pattern aims to solve the problem of an anti-pattern known as the telescoping constructor. Telescoping constructors occur when a class has multiple constructors with an increasing number of parameters, which can lead to confusion and error-prone code.

## What are the use cases of the Builder Design Pattern?

### 1. Building Documents in Word Processors:

Word processors often need to create complex documents with various formatting options, styles, and elements. A builder pattern can be used to construct documents step by step, setting attributes like fonts, paragraphs, tables, and images.

### 2. Creating SQL Queries:

When constructing SQL queries dynamically, especially when dealing with complex queries involving multiple conditions, joins, and sorting options, a builder pattern can help create a query object step by step, allowing for flexibility and readability.

### 3. Configuring Network Requests:

When making HTTP requests, constructing a request with headers, parameters, authentication details, and other configurations can be intricate. A builder pattern can simplify this process, allowing developers to set specific options as needed.

### 4. Building User Interface Components:

In graphical user interface frameworks, constructing complex UI components involves setting various properties such as size, color, layout, and event handlers. A builder pattern can be employed to create these components with a fluent API, making the code more expressive.

## Different implementations of Builder Pattern

### 1. Regular Builder Pattern:

`java`
```java
// Product
//
// Represents the complex object being constructed. It's the final object that the client code wants to obtain.
public class Computer {
    private String CPU;
    private String RAM;
    private String storage;

    // Constructor and getters...
}

// Builder interface
//
// An interface or abstract class that defines the steps to construct the product.
//Each step corresponds to setting a specific attribute or part of the product.
public interface ComputerBuilder {
    void buildCPU(String cpu);
    void buildRAM(String ram);
    void buildStorage(String storage);
    Computer getResult();
}

// ConcreteBuilder
//
// Implements the Builder interface and provides concrete implementations for constructing the product.
// It keeps track of the constructed product and provides methods for setting its attributes.
public class DesktopComputerBuilder implements ComputerBuilder {
    private Computer computer = new Computer();

    public void buildCPU(String cpu) {
        computer.setCPU(cpu);
    }

    public void buildRAM(String ram) {
        computer.setRAM(ram);
    }

    public void buildStorage(String storage) {
        computer.setStorage(storage);
    }

    public Computer getResult() {
        return computer;
    }
}

// Director
//
// Orchestrates the construction of the product using a builder.
// It knows the order in which to call the builder's methods to construct the final product.
public class ComputerDirector {
    public Computer construct(ComputerBuilder builder) {
        builder.buildCPU("Intel i7");
        builder.buildRAM("16GB");
        builder.buildStorage("512GB SSD");
        return builder.getResult();
    }
}

// Client code
public class Client {
    public static void main(String[] args) {
        ComputerBuilder builder = new DesktopComputerBuilder();
        ComputerDirector director = new ComputerDirector();

        Computer desktop = director.construct(builder);
        System.out.println(desktop);
    }
}
```

`csharp`
```csharp
// Product
//
// Represents the complex object being constructed. It's the final object that the client code wants to obtain.
public class Computer
{
    public string CPU { get; set; }
    public string RAM { get; set; }
    public string Storage { get; set; }

    // Constructors and methods...
}

// Builder interface
//
// An interface or abstract class that defines the steps to construct the product.
//Each step corresponds to setting a specific attribute or part of the product.
public interface IComputerBuilder
{
    void BuildCPU(string cpu);
    void BuildRAM(string ram);
    void BuildStorage(string storage);
    Computer GetResult();
}

// ConcreteBuilder
//
// Implements the Builder interface and provides concrete implementations for constructing the product.
// It keeps track of the constructed product and provides methods for setting its attributes.
public class DesktopComputerBuilder : IComputerBuilder
{
    private Computer computer = new Computer();

    public void BuildCPU(string cpu)
    {
        computer.CPU = cpu;
    }

    public void BuildRAM(string ram)
    {
        computer.RAM = ram;
    }

    public void BuildStorage(string storage)
    {
        computer.Storage = storage;
    }

    public Computer GetResult()
    {
        return computer;
    }
}

// Director
//
// Orchestrates the construction of the product using a builder.
// It knows the order in which to call the builder's methods to construct the final product.
public class ComputerDirector
{
    public Computer Construct(IComputerBuilder builder)
    {
        builder.BuildCPU("Intel i7");
        builder.BuildRAM("16GB");
        builder.BuildStorage("512GB SSD");
        return builder.GetResult();
    }
}

// Client code
class Client
{
    static void Main()
    {
        IComputerBuilder builder = new DesktopComputerBuilder();
        ComputerDirector director = new ComputerDirector();

        Computer desktop = director.Construct(builder);
        Console.WriteLine(desktop);
    }
}

```

### 2. Using Lombok library:

`java`
```java
import lombok.Builder;
import lombok.ToString;

// Product class
@Builder
@ToString
public class Computer {
    private String CPU;
    private String RAM;
    private String storage;
}

// Client code
public class Client {
    public static void main(String[] args) {
        // Use the generated builder to construct the object
        Computer desktop = Computer.builder()
                .CPU("Intel i7")
                .RAM("16GB")
                .storage("512GB SSD")
                .build();

        // Print the result
        System.out.println(desktop);
    }
}

```

### 3. Using Fluent Interface:

Builder Design Patterns using a fluent interface involve chaining method calls in a way that makes the code more readable and expressive.

`java`
```java
public class Computer {
    private String CPU;
    private String RAM;
    private String storage;

    // Constructor of the Product class is private
    // It is called from within the inner builder class
    private Computer(Builder builder) {
        this.CPU = builder.CPU;
        this.RAM = builder.RAM;
        this.storage = builder.storage;
    }

    public String getCPU() {
        return CPU;
    }

    public String getRAM() {
        return RAM;
    }

    public String getStorage() {
        return storage;
    }

    @Override
    public String toString() {
        return "Computer{" +
                "CPU='" + CPU + '\'' +
                ", RAM='" + RAM + '\'' +
                ", storage='" + storage + '\'' +
                '}';
    }

    // Builder class
    //
    // The builder class is inside of the product class
    // this inner builder class calls the private product class
    public static class Builder {
        private String CPU;
        private String RAM;
        private String storage;

        public Builder setCPU(String CPU) {
            this.CPU = CPU;
            return this;
        }

        public Builder setRAM(String RAM) {
            this.RAM = RAM;
            return this;
        }

        public Builder setStorage(String storage) {
            this.storage = storage;
            return this;
        }

        public Computer build() {
            return new Computer(this);
        }
    }
}

// Example of fluent interface usage
public static void main(String[] args) {
    Computer computer = new Computer.Builder()
            .setCPU("Intel i7")
            .setRAM("16GB")
            .setStorage("512GB SSD")
            .build();

    System.out.println(computer);
}

```

`csharp`
```csharp
using System;

public class Computer
{
    private string CPU;
    private string RAM;
    private string storage;

    // Constructor of the Product class is private
    // It is called from within the inner builder class
    private Computer(Builder builder)
    {
        this.CPU = builder.CPU;
        this.RAM = builder.RAM;
        this.storage = builder.Storage;
    }

    public string GetCPU()
    {
        return CPU;
    }

    public string GetRAM()
    {
        return RAM;
    }

    public string GetStorage()
    {
        return storage;
    }

    public override string ToString()
    {
        return $"Computer{{CPU='{CPU}', RAM='{RAM}', Storage='{storage}'}}";
    }

    // Builder class
    //
    // The builder class is inside of the product class
    // this inner builder class calls the private product class
    public class Builder
    {
        public string CPU { get; private set; }
        public string RAM { get; private set; }
        public string Storage { get; private set; }

        public Builder SetCPU(string cpu)
        {
            this.CPU = cpu;
            return this;
        }

        public Builder SetRAM(string ram)
        {
            this.RAM = ram;
            return this;
        }

        public Builder SetStorage(string storage)
        {
            this.Storage = storage;
            return this;
        }

        public Computer Build()
        {
            return new Computer(this);
        }
    }
}

// Example of fluent interface usage
public static void Main()
{
    Computer computer = new Computer.Builder()
        .SetCPU("Intel i7")
        .SetRAM("16GB")
        .SetStorage("512GB SSD")
        .Build();

    Console.WriteLine(computer);
}

```
