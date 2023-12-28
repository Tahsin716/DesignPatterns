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

Note the use of the `volatile` keyword to ensure that changes to the instance variable are visible to all threads.

### 3. **Eager Initialization:**
In this approach, the instance is created at the time of class loading, even before it is being used.

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

This implementation is thread-safe by default but may not be efficient if the instance is not always needed.

### 4. **Bill Pugh Singleton (Initialization-on-demand holder idiom):**

This approach uses a static inner helper class to achieve lazy loading and thread safety.

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
