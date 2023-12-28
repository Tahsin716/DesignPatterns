# Singleton

### What is the Singleton Design Pattern?

The Singleton Design Pattern is a creational pattern that ensures a class has only **one instance** and provides a global access point to that instance. 


### What are the use cases of the Singleton Design Pattern?

It's useful for managing shared resources, configurations, or objects that should exist only once in an application.

For Example

- Managing configuration settings
- Handling database connections
- Logging systems
- Thread pools
- Resource access controllers

## Different implementations of the Singleton Pattern


### 1. **Classic Singleton (Lazy Initialization):**
This is a basic implementation of the Singleton pattern where the instance is created when it is first requested.

`java`
``` java
public class ClassicSingleton {
    private static ClassicSingleton instance;

    private ClassicSingleton() {
        // Private constructor to prevent instantiation
    }

    // Public static method to get the instance
    public static ClassicSingleton getInstance() {
        // Lazy initialization - create the instance if it doesn't exist
        if (instance == null) {
            instance = new ClassicSingleton();
        }
        return instance;
    }
}
```

`csharp`
``` csharp
public class ClassicSingleton
{
    private static ClassicSingleton instance;

    private ClassicSingleton()
    {
        // Private constructor to prevent instantiation
    }

    public static ClassicSingleton Instance
    {
        get
        {
            if (instance == null)
            {
                instance = new ClassicSingleton();
            }
            return instance;
        }
    }
}

```

### 2. **Thread-Safe Singleton (Double-Checked Locking):**
To ensure thread safety, you can use double-checked locking. This implementation ensures that the instance is only created once and is thread-safe.

`java`
```java
public class ThreadSafeSingleton {
    private static volatile ThreadSafeSingleton instance;

    private ThreadSafeSingleton() {
        // Private constructor to prevent instantiation
    }

    public static ThreadSafeSingleton getInstance() {
        if (instance == null) {
            synchronized (ThreadSafeSingleton.class) {
                if (instance == null) {
                    instance = new ThreadSafeSingleton();
                }
            }
        }
        return instance;
    }
}
```

`csharp`
```csharp
public class ThreadSafeSingleton
{
    private static volatile ThreadSafeSingleton instance;
    private static object lockObject = new object();

    private ThreadSafeSingleton()
    {
        // Private constructor to prevent instantiation
    }

    public static ThreadSafeSingleton Instance
    {
        get
        {
            if (instance == null)
            {
                lock (lockObject)
                {
                    if (instance == null)
                    {
                        instance = new ThreadSafeSingleton();
                    }
                }
            }
            return instance;
        }
    }
}

```

Note the use of the `volatile` keyword to ensure that changes to the instance variable are visible to all threads.

### 3. **Eager Initialization:**
In this approach, the instance is created at the time of class loading, even before it is being used.

`java`
```java
public class EagerSingleton {
    private static final EagerSingleton instance = new EagerSingleton();

    private EagerSingleton() {
        // Private constructor to prevent instantiation
    }

    public static EagerSingleton getInstance() {
        return instance;
    }
}
```

`csharp`
```csharp
public class EagerSingleton
{
    private static readonly EagerSingleton instance = new EagerSingleton();

    private EagerSingleton()
    {
        // Private constructor to prevent instantiation
    }

    public static EagerSingleton Instance
    {
        get { return instance; }
    }
}

```

This implementation is thread-safe by default but may not be efficient if the instance is not always needed.

### 4. a) **Bill Pugh Singleton (Initialization-on-demand holder idiom):**

This approach uses a static inner helper class to achieve lazy loading and thread safety.

`java`
```java
public class BillPughSingleton {
    private BillPughSingleton() {
        // Private constructor to prevent instantiation
    }

    private static class SingletonHelper {
        private static final BillPughSingleton instance = new BillPughSingleton();
    }

    public static BillPughSingleton getInstance() {
        return SingletonHelper.instance;
    }
}
```

This method is thread-safe, efficient, and provides lazy initialization.

### 4. b) Lazy Initialization with `Lazy<T>`

C# provides a `Lazy<T>` class to simplify lazy initialization.

`csharp`
```csharp
public class LazySingleton
{
    private static readonly Lazy<LazySingleton> lazyInstance =
        new Lazy<LazySingleton>(() => new LazySingleton());

    private LazySingleton()
    {
        // Private constructor to prevent instantiation
    }

    public static LazySingleton Instance
    {
        get { return lazyInstance.Value; }
    }
}
```

This implementation is thread-safe and uses the Lazy<T> class for efficient lazy initialization.

## Drawbacks of the Singleton Design Pattern

### 1. **Global State:** 

Singletons introduce a global state to your application, and this global state can be modified from anywhere in the code. This can lead to unexpected side effects and make it challenging to understand and reason about the behavior of the system.

   ```java
   // Example of modifying global state using a Singleton
   Singleton.getInstance().setSomeValue(42);
   ```

### 2. **Testability Issues:** 

Due to the global state, it can be difficult to isolate and test components that depend on a Singleton. Mocking or substituting the Singleton instance for testing purposes might be necessary, which can be cumbersome.

   ```java
   // Example of a class tightly coupled to a Singleton
   public class MyClass {
       private Singleton singleton = Singleton.getInstance();

       // ...
   }
   ```

### 3. **Violates Single Responsibility Principle:** 

The Singleton pattern can lead to a violation of the Single Responsibility Principle (SRP) because a Singleton is responsible for both 

1. managing its instance
2. performing its primary functionality

This can make the code less modular and harder to maintain.

   ```java
   // Example of a Singleton violating SRP
   public class DatabaseSingleton {
       private static DatabaseSingleton instance;

       private DatabaseSingleton() {
           // ...
       }

       public static DatabaseSingleton getInstance() {
           if (instance == null) {
               instance = new DatabaseSingleton();
           }
           return instance;
       }

       public void performDatabaseOperation() {
           // Database operation logic here
       }
   }
   ```

### 4. **Difficulties in Subclassing:** 

Extending a class that follows the Singleton pattern can be challenging, especially when dealing with inheritance. Subclassing a Singleton might lead to unexpected behavior, and modifying the Singleton to allow subclassing could break its intended design.

   ```java
   // Example of subclassing a Singleton
   public class SubclassSingleton extends Singleton {
       // ...
   }
   ```

### 5. **Concurrency Issues (in some implementations):** 

In scenarios where lazy initialization is used and multiple threads are involved, there can be race conditions. If not properly handled, this can lead to the creation of multiple instances of the Singleton, defeating the purpose of the pattern.

   ```java
   // Example of a lazy Singleton with a potential concurrency issue
   public class LazySingleton {
       private static LazySingleton instance;

       private LazySingleton() {
           // ...
       }

       public static LazySingleton getInstance() {
           if (instance == null) {
               // Potential race condition here
               instance = new LazySingleton();
           }
           return instance;
       }
   }
   ```
