# Memento

### What is the Memento Design Pattern?

Memento Design Pattern is a behavioral design pattern to store/restore the state of the object.

## What are the use cases of Memento Design Pattern?

### 1. Text Editors with Undo Feature:

Storing and restoring the state of a document or text editor to support undo/redo operations.

### 2. Transactional Systems:

Capturing and restoring the state of a transactional system to ensure data consistency in case of failures.

### 3. Game State Management:

Saving and loading the state of a game to allow players to resume their progress.

## Implementations of Memento Design Pattern

### 1. Memento Design Pattern using class

`java`
```java
// Memento class
class Memento {
    private String state;

    public Memento(String state) {
        this.state = state;
    }

    public String getState() {
        return state;
    }
}

// Originator class
class Originator {
    private String state;

    public void setState(String state) {
        this.state = state;
    }

    public Memento createMemento() {
        return new Memento(state);
    }

    public void restoreFromMemento(Memento memento) {
        state = memento.getState();
    }

    public String getState() {
        return state;
    }
}

// Caretaker class
class Caretaker {
    private Memento memento;

    public void setMemento(Memento memento) {
        this.memento = memento;
    }

    public Memento getMemento() {
        return memento;
    }
}

// Client code
public class Client {
    public static void main(String[] args) {
        Originator originator = new Originator();
        Caretaker caretaker = new Caretaker();

        // Save the initial state
        originator.setState("State 1");
        caretaker.setMemento(originator.createMemento());

        // Change the state
        originator.setState("State 2");

        // Save the new state
        caretaker.setMemento(originator.createMemento());

        // Restore to the first state
        originator.restoreFromMemento(caretaker.getMemento());
        System.out.println("Current State: " + originator.getState());
    }
}

```

`csharp`
```csharp
using System;

// Memento class
public class Memento
{
    public string State { get; }

    public Memento(string state)
    {
        State = state;
    }
}

// Originator class
public class Originator
{
    private string state;

    public void SetState(string state)
    {
        this.state = state;
    }

    public Memento CreateMemento()
    {
        return new Memento(state);
    }

    public void RestoreFromMemento(Memento memento)
    {
        state = memento.State;
    }

    public string GetState()
    {
        return state;
    }
}

// Caretaker class
public class Caretaker
{
    private Memento memento;

    public void SetMemento(Memento memento)
    {
        this.memento = memento;
    }

    public Memento GetMemento()
    {
        return memento;
    }
}

// Client code
class Program
{
    static void Main()
    {
        Originator originator = new Originator();
        Caretaker caretaker = new Caretaker();

        // Save the initial state
        originator.SetState("State 1");
        caretaker.SetMemento(originator.CreateMemento());

        // Change the state
        originator.SetState("State 2");

        // Save the new state
        caretaker.SetMemento(originator.CreateMemento());

        // Restore to the first state
        originator.RestoreFromMemento(caretaker.GetMemento());
        Console.WriteLine("Current State: " + originator.GetState());
    }
}

```

### 2. Memento Design Pattern using records

`java`
```java
// Memento record
record Memento(String state) {}

// Originator class
class Originator {
    private String state;

    public void setState(String state) {
        this.state = state;
    }

    public Memento createMemento() {
        return new Memento(state);
    }

    public void restoreFromMemento(Memento memento) {
        state = memento.state();
    }

    public String getState() {
        return state;
    }
}

// Caretaker class
class Caretaker {
    private Memento memento;

    public void setMemento(Memento memento) {
        this.memento = memento;
    }

    public Memento getMemento() {
        return memento;
    }
}

// Client code
public class Client {
    public static void main(String[] args) {
        Originator originator = new Originator();
        Caretaker caretaker = new Caretaker();

        // Save the initial state
        originator.setState("State 1");
        caretaker.setMemento(originator.createMemento());

        // Change the state
        originator.setState("State 2");

        // Save the new state
        caretaker.setMemento(originator.createMemento());

        // Restore to the first state
        originator.restoreFromMemento(caretaker.getMemento());
        System.out.println("Current State: " + originator.getState());
    }
}

```

`csharp`
```csharp
using System;

// Memento record
public record Memento(string State);

// Originator class
public class Originator
{
    private string state;

    public void SetState(string state)
    {
        this.state = state;
    }

    public Memento CreateMemento()
    {
        return new Memento(state);
    }

    public void RestoreFromMemento(Memento memento)
    {
        state = memento.State;
    }

    public string GetState()
    {
        return state;
    }
}

// Caretaker class
public class Caretaker
{
    private Memento memento;

    public void SetMemento(Memento memento)
    {
        this.memento = memento;
    }

    public Memento GetMemento()
    {
        return memento;
    }
}

// Client code
class Program
{
    static void Main()
    {
        Originator originator = new Originator();
        Caretaker caretaker = new Caretaker();

        // Save the initial state
        originator.SetState("State 1");
        caretaker.SetMemento(originator.CreateMemento());

        // Change the state
        originator.SetState("State 2");

        // Save the new state
        caretaker.SetMemento(originator.CreateMemento());

        // Restore to the first state
        originator.RestoreFromMemento(caretaker.GetMemento());
        Console.WriteLine("Current State: " + originator.GetState());
    }
}

```
