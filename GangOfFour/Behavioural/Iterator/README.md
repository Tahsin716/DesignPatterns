# Iterator

### What is the Iterator Design Pattern?

Iterator Design Pattern is a behavioral design pattern that provides a way to access the elements of a collection sequentially without exposing the underlying representation of the collection.

### What are the components of the Iterator Design Pattern?

#### `Iterator:`

Defines an interface for accessing and traversing elements of a collection.

#### `ConcreteIterator:`

Implements the Iterator interface and keeps track of the current position in the traversal.

 #### `Aggregate:`

Defines an interface for creating an Iterator object.

#### `ConcreteAggregate:`

Implements the Aggregate interface to create an Iterator object.

## Implementations of Iterator Design Pattern

### 1. Iterator Design Pattern:

`java`
```java
import java.util.ArrayList;
import java.util.List;
import java.util.NoSuchElementException;

// Iterator interface
interface Iterator<T> {
    T next();
    boolean hasNext();
}

// ConcreteIterator
class ConcreteIterator<T> implements Iterator<T> {
    private int currentPosition = 0;
    private final List<T> elements;

    public ConcreteIterator(List<T> elements) {
        this.elements = elements;
    }

    @Override
    public T next() {
        if (hasNext()) {
            return elements.get(currentPosition++);
        }
        throw new NoSuchElementException("No more elements");
    }

    @Override
    public boolean hasNext() {
        return currentPosition < elements.size();
    }
}

// Aggregate interface
interface Aggregate<T> {
    Iterator<T> createIterator();
}

// ConcreteAggregate
class ConcreteAggregate<T> implements Aggregate<T> {
    private final List<T> elements = new ArrayList<>();

    public void addElement(T element) {
        elements.add(element);
    }

    @Override
    public Iterator<T> createIterator() {
        return new ConcreteIterator<>(elements);
    }
}

// Client code
public class Client {
    public static void main(String[] args) {
        ConcreteAggregate<String> aggregate = new ConcreteAggregate<>();
        aggregate.addElement("Item 1");
        aggregate.addElement("Item 2");
        aggregate.addElement("Item 3");

        Iterator<String> iterator = aggregate.createIterator();

        while (iterator.hasNext()) {
            System.out.println(iterator.next());
        }
    }
}

```

`csharp`
```csharp
using System;
using System.Collections.Generic;
using System.Linq;

// Iterator interface
interface Iterator<T>
{
    T Next();
    bool HasNext();
}

// ConcreteIterator
class ConcreteIterator<T> : Iterator<T>
{
    private int currentPosition = 0;
    private readonly List<T> elements;

    public ConcreteIterator(List<T> elements)
    {
        this.elements = elements;
    }

    public T Next()
    {
        if (HasNext())
        {
            return elements[currentPosition++];
        }
        throw new InvalidOperationException("No more elements");
    }

    public bool HasNext()
    {
        return currentPosition < elements.Count;
    }
}

// Aggregate interface
interface Aggregate<T>
{
    Iterator<T> CreateIterator();
}

// ConcreteAggregate
class ConcreteAggregate<T> : Aggregate<T>
{
    private readonly List<T> elements = new List<T>();

    public void AddElement(T element)
    {
        elements.Add(element);
    }

    public Iterator<T> CreateIterator()
    {
        return new ConcreteIterator<T>(elements);
    }
}

// Client code
class Program
{
    static void Main()
    {
        ConcreteAggregate<string> aggregate = new ConcreteAggregate<string>();
        aggregate.AddElement("Item 1");
        aggregate.AddElement("Item 2");
        aggregate.AddElement("Item 3");

        Iterator<string> iterator = aggregate.CreateIterator();

        while (iterator.HasNext())
        {
            Console.WriteLine(iterator.Next());
        }
    }
}

```
