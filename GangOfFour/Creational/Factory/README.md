# Factory

### What is the Factory Design Pattern?

Factory Design Pattern is a creational pattern that creates objects without exposing their creation logic, letting clients specify and obtain desired products.


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
