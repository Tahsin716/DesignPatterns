# Strategy

### What is the Strategy Design Pattern?

Strategy Design Pattern is a behavioral design pattern that defines a family of algorithms, encapsulates each algorithm, and makes them interchangeable.

## What are the use cases of Strategy Design Pattern?

### 1. Sorting Algorithms:

Varying sorting algorithms (e.g., quicksort, bubblesort) based on different requirements.

### 2. File Compression:

Choosing different compression algorithms (e.g., ZIP, GZIP) based on file types or user preferences.

### 3. Payment Gateways:

Supporting different payment methods (credit card, PayPal, etc.) in an e-commerce application.

### 4. Graphics Rendering:

Rendering graphics using different rendering strategies based on the hardware capabilities.

## Implementations of Strategy Design Pattern:

### 1. Strategy Design Pattern:

`java`
```java
// Strategy interface
interface PaymentStrategy {
    void pay(int amount);
}

// Concrete Strategies
class CreditCardPayment implements PaymentStrategy {
    private String cardNumber;

    public CreditCardPayment(String cardNumber) {
        this.cardNumber = cardNumber;
    }

    @Override
    public void pay(int amount) {
        System.out.println("Paid " + amount + " using credit card: " + cardNumber);
    }
}

class PayPalPayment implements PaymentStrategy {
    private String email;

    public PayPalPayment(String email) {
        this.email = email;
    }

    @Override
    public void pay(int amount) {
        System.out.println("Paid " + amount + " using PayPal: " + email);
    }
}

// Context class
class ShoppingCart {
    private PaymentStrategy paymentStrategy;

    public void setPaymentStrategy(PaymentStrategy paymentStrategy) {
        this.paymentStrategy = paymentStrategy;
    }

    public void checkout(int amount) {
        paymentStrategy.pay(amount);
    }
}

// Client code
public class Client {
    public static void main(String[] args) {
        ShoppingCart cart = new ShoppingCart();

        // Using credit card payment strategy
        cart.setPaymentStrategy(new CreditCardPayment("1234-5678-9101-1121"));
        cart.checkout(100);

        // Using PayPal payment strategy
        cart.setPaymentStrategy(new PayPalPayment("john.doe@example.com"));
        cart.checkout(50);
    }
}

```

`csharp`
```csharp
using System;

// Strategy interface
public interface IPaymentStrategy
{
    void Pay(int amount);
}

// Concrete Strategies
public class CreditCardPayment : IPaymentStrategy
{
    private readonly string cardNumber;

    public CreditCardPayment(string cardNumber)
    {
        this.cardNumber = cardNumber;
    }

    public void Pay(int amount)
    {
        Console.WriteLine($"Paid {amount} using credit card: {cardNumber}");
    }
}

public class PayPalPayment : IPaymentStrategy
{
    private readonly string email;

    public PayPalPayment(string email)
    {
        this.email = email;
    }

    public void Pay(int amount)
    {
        Console.WriteLine($"Paid {amount} using PayPal: {email}");
    }
}

// Context class
public class ShoppingCart
{
    private IPaymentStrategy paymentStrategy;

    public void SetPaymentStrategy(IPaymentStrategy paymentStrategy)
    {
        this.paymentStrategy = paymentStrategy;
    }

    public void Checkout(int amount)
    {
        paymentStrategy.Pay(amount);
    }
}

// Client code
class Program
{
    static void Main()
    {
        ShoppingCart cart = new ShoppingCart();

        // Using credit card payment strategy
        cart.SetPaymentStrategy(new CreditCardPayment("1234-5678-9101-1121"));
        cart.Checkout(100);

        // Using PayPal payment strategy
        cart.SetPaymentStrategy(new PayPalPayment("john.doe@example.com"));
        cart.Checkout(50);
    }
}

```
