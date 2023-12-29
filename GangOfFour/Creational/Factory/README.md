# Factory

### What is the Factory Design Pattern?

Factory Design Pattern is a creational pattern that creates objects without exposing their creation logic, letting clients specify and obtain desired products.

## What are the use cases of the Factory Design Pattern?

### 1. GUI Component Creation:

In a graphical user interface framework, a GUI component factory can be used to create various UI elements like buttons, text fields, and windows. Different platforms may have different implementations of these components, and a factory pattern helps create them based on the specific platform.

### 2. Document Creation in Word Processors:

In word processing applications, a document factory can be used to create different types of documents (e.g., text documents, spreadsheets, presentations). Each document type may require a different set of objects and behaviors, and a factory pattern helps create these documents.

### 3. Payment Gateway Integration:

In an e-commerce platform, a payment gateway integration can be abstracted using a factory pattern. Different payment gateways may have unique implementations, and a factory can create the appropriate payment gateway instance based on configuration or user preferences.

### 4. Database Connection Creation:

A database abstraction layer can use the Factory pattern to create specific database connections (e.g., MySQL, PostgreSQL, SQLite). This allows the application to switch between different database systems without changing the client code.


## Different implementations of Factory Pattern

### 1. **Simple Factory:**
In the Simple Factory pattern, a single factory class is responsible for creating objects based on input parameters.

`java`
```java
// Payment interface
interface Payment {
    void processPayment();
}

// Concrete payments
class CreditCardPayment implements Payment {
    public void processPayment() {
        System.out.println("Processing Credit Card Payment");
    }
}

class PayPalPayment implements Payment {
    public void processPayment() {
        System.out.println("Processing PayPal Payment");
    }
}

// Simple Factory
class PaymentFactory {
    public Payment createPayment(String type) {
        switch (type) {
            case "CreditCard":
                return new CreditCardPayment();
            case "PayPal":
                return new PayPalPayment();
            default:
                throw new IllegalArgumentException("Invalid payment type");
        }
    }
}

// Client code
public class Client {
    public static void main(String[] args) {
        PaymentFactory factory = new PaymentFactory();

        Payment creditCardPayment = factory.createPayment("CreditCard");
        creditCardPayment.processPayment();

        Payment payPalPayment = factory.createPayment("PayPal");
        payPalPayment.processPayment();
    }
}
```

`csharp`
```csharp
// Payment interface
interface IPayment
{
    void ProcessPayment();
}

// Concrete payments
class CreditCardPayment : IPayment
{
    public void ProcessPayment()
    {
        Console.WriteLine("Processing Credit Card Payment");
    }
}

class PayPalPayment : IPayment
{
    public void ProcessPayment()
    {
        Console.WriteLine("Processing PayPal Payment");
    }
}

// Simple Factory
class PaymentFactory
{
    public IPayment CreatePayment(string type)
    {
        switch (type)
        {
            case "CreditCard":
                return new CreditCardPayment();
            case "PayPal":
                return new PayPalPayment();
            default:
                throw new ArgumentException("Invalid payment type");
        }
    }
}

// Client code
class Client
{
    static void Main()
    {
        PaymentFactory factory = new PaymentFactory();

        IPayment creditCardPayment = factory.CreatePayment("CreditCard");
        creditCardPayment.ProcessPayment();

        IPayment payPalPayment = factory.CreatePayment("PayPal");
        payPalPayment.ProcessPayment();
    }
}

```

### 2. **Factory Method:**
In the Factory Method pattern, each subclass provides an interface for creating an object, but leaves the choice of its type to the subclasses, creating an instance of the appropriate subclass.

`java`
```java
// Payment interface
interface Payment {
    void processPayment();
}

// Concrete payments
class CreditCardPayment implements Payment {
    public void processPayment() {
        System.out.println("Processing Credit Card Payment");
    }
}

class PayPalPayment implements Payment {
    public void processPayment() {
        System.out.println("Processing PayPal Payment");
    }
}

// Payment creator interface
interface PaymentCreator {
    Payment createPayment();
}

// Concrete payment creators
class CreditCardPaymentCreator implements PaymentCreator {
    public Payment createPayment() {
        return new CreditCardPayment();
    }
}

class PayPalPaymentCreator implements PaymentCreator {
    public Payment createPayment() {
        return new PayPalPayment();
    }
}

// Client code
public class Client {
    public static void main(String[] args) {
        PaymentCreator creditCardPaymentCreator = new CreditCardPaymentCreator();
        Payment creditCardPayment = creditCardPaymentCreator.createPayment();
        creditCardPayment.processPayment();

        PaymentCreator payPalPaymentCreator = new PayPalPaymentCreator();
        Payment payPalPayment = payPalPaymentCreator.createPayment();
        payPalPayment.processPayment();
    }
}
```

`csharp`
```csharp
// Payment interface
interface IPayment
{
    void ProcessPayment();
}

// Concrete payments
class CreditCardPayment : IPayment
{
    public void ProcessPayment()
    {
        Console.WriteLine("Processing Credit Card Payment");
    }
}

class PayPalPayment : IPayment
{
    public void ProcessPayment()
    {
        Console.WriteLine("Processing PayPal Payment");
    }
}

// Payment creator interface
interface IPaymentCreator
{
    IPayment CreatePayment();
}

// Concrete payment creators
class CreditCardPaymentCreator : IPaymentCreator
{
    public IPayment CreatePayment()
    {
        return new CreditCardPayment();
    }
}

class PayPalPaymentCreator : IPaymentCreator
{
    public IPayment CreatePayment()
    {
        return new PayPalPayment();
    }
}

// Client code
class Client
{
    static void Main()
    {
        IPaymentCreator creditCardPaymentCreator = new CreditCardPaymentCreator();
        IPayment creditCardPayment = creditCardPaymentCreator.CreatePayment();
        creditCardPayment.ProcessPayment();

        IPaymentCreator payPalPaymentCreator = new PayPalPaymentCreator();
        IPayment payPalPayment = payPalPaymentCreator.CreatePayment();
        payPalPayment.ProcessPayment();
    }
}

```

### 3. **Abstract Factory:**
The Abstract Factory pattern provides an interface for creating families of related or dependent objects without specifying their concrete classes.

`java`
```java
// Abstract payment interfaces
interface CreditCardPayment {
    void processCreditCardPayment();
}

interface PayPalPayment {
    void processPayPalPayment();
}

// Concrete credit card payments
class VisaCreditCardPayment implements CreditCardPayment {
    public void processCreditCardPayment() {
        System.out.println("Processing Visa Credit Card Payment");
    }
}

class MasterCardCreditCardPayment implements CreditCardPayment {
    public void processCreditCardPayment() {
        System.out.println("Processing MasterCard Credit Card Payment");
    }
}

// Concrete PayPal payments
class StandardPayPalPayment implements PayPalPayment {
    public void processPayPalPayment() {
        System.out.println("Processing Standard PayPal Payment");
    }
}

class ExpressPayPalPayment implements PayPalPayment {
    public void processPayPalPayment() {
        System.out.println("Processing Express PayPal Payment");
    }
}

// Abstract Factory interface
interface PaymentFactory {
    CreditCardPayment createCreditCardPayment();
    PayPalPayment createPayPalPayment();
}

// Concrete factories
class StandardPaymentFactory implements PaymentFactory {
    public CreditCardPayment createCreditCardPayment() {
        return new VisaCreditCardPayment();
    }

    public PayPalPayment createPayPalPayment() {
        return new StandardPayPalPayment();
    }
}

class ExpressPaymentFactory implements PaymentFactory {
    public CreditCardPayment createCreditCardPayment() {
        return new MasterCardCreditCardPayment();
    }

    public PayPalPayment createPayPalPayment() {
        return new ExpressPayPalPayment();
    }
}

// Client code
public class Client {
    public static void main(String[] args) {
        PaymentFactory standardPaymentFactory = new StandardPaymentFactory();
        CreditCardPayment standardCreditCardPayment = standardPaymentFactory.createCreditCardPayment();
        PayPalPayment standardPayPalPayment = standardPaymentFactory.createPayPalPayment();
        standardCreditCardPayment.processCreditCardPayment();
        standardPayPalPayment.processPayPalPayment();

        PaymentFactory expressPaymentFactory = new ExpressPaymentFactory();
        CreditCardPayment expressCreditCardPayment = expressPaymentFactory.createCreditCardPayment();
        PayPalPayment expressPayPalPayment = expressPaymentFactory.createPayPalPayment();
        expressCreditCardPayment.processCreditCardPayment();
        expressPayPalPayment.processPayPalPayment();
    }
}
```

`csharp`
```csharp
// Abstract payment interfaces
interface ICreditCardPayment
{
    void ProcessCreditCardPayment();
}

interface IPayPalPayment
{
    void ProcessPayPalPayment();
}

// Concrete credit card payments
class VisaCreditCardPayment : ICreditCardPayment
{
    public void ProcessCreditCardPayment()
    {
        Console.WriteLine("Processing Visa Credit Card Payment");
    }
}

class MasterCardCreditCardPayment : ICreditCardPayment
{
    public void ProcessCreditCardPayment()
    {
        Console.WriteLine("Processing MasterCard Credit Card Payment");
    }
}

// Concrete PayPal payments
class StandardPayPalPayment : IPayPalPayment
{
    public void ProcessPayPalPayment()
    {
        Console.WriteLine("Processing Standard PayPal Payment");
    }
}

class ExpressPayPalPayment : IPayPalPayment
{
    public void ProcessPayPalPayment()
    {
        Console.WriteLine("Processing Express PayPal Payment");
    }
}

// Abstract Factory interface
interface IPaymentFactory
{
    ICreditCardPayment CreateCreditCardPayment();
    IPayPalPayment CreatePayPalPayment();
}

// Concrete factories
class StandardPaymentFactory : IPaymentFactory
{
    public ICreditCardPayment CreateCreditCardPayment()
    {
        return new VisaCreditCardPayment();
    }

    public IPayPalPayment CreatePayPalPayment()
    {
        return new StandardPayPalPayment();
    }
}

class ExpressPaymentFactory : IPaymentFactory
{
    public ICreditCardPayment CreateCreditCardPayment()
    {
        return new MasterCardCreditCardPayment();
    }

    public IPayPalPayment CreatePayPalPayment()
    {
        return new ExpressPayPalPayment();
    }
}

// Client code
class Client
{
    static void Main()
    {
        IPaymentFactory standardPaymentFactory = new StandardPaymentFactory();
        ICreditCardPayment standardCreditCardPayment = standardPaymentFactory.CreateCreditCardPayment();
        IPayPalPayment standardPayPalPayment = standardPaymentFactory.CreatePayPalPayment();
        standardCreditCardPayment.ProcessCreditCardPayment();
        standardPayPalPayment.ProcessPayPalPayment();

        IPaymentFactory expressPaymentFactory = new ExpressPaymentFactory();
        ICreditCardPayment expressCreditCardPayment = expressPaymentFactory.CreateCreditCardPayment();
        IPayPalPayment expressPayPalPayment = expressPaymentFactory.CreatePayPalPayment();
        expressCreditCardPayment.ProcessCreditCardPayment();
        expressPayPalPayment.ProcessPayPalPayment();
    }
}

```
