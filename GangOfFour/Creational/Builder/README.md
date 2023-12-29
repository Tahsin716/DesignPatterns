# Builder

### What is a Builder Design Pattern?

Builder Design Pattern is a creational pattern to create complex objects piecewise and succinctly.

### What problem does the Builder Pattern aim to solve?

The Builder Pattern aims to solve the problem of an anti-pattern known as the telescoping constructor. Telescoping constructors occur when a class has multiple constructors with an increasing number of parameters, which can lead to confusion and error-prone code.


## Different implementations of Builder Pattern

### 1. Regular Builder Pattern

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
