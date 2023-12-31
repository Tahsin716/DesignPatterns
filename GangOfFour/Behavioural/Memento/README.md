# Memento

### What is the Memento Design Pattern?

Memento Design Pattern is a behavioral design pattern to store/restore the state of the object.

### What are the components in the Memento Design Pattern?

#### `Originator:`

The object whose state needs to be saved. It creates a Memento containing a snapshot of its internal state.

#### `Memento:`

Represents the state of the Originator at a specific point in time. It has methods to retrieve and set the state.

#### `Caretaker:`

Responsible for keeping track of multiple versions (Mementos) of the Originator's state. It doesn't have direct access to the Memento's state.

## What are the use cases of Memento Design Pattern?

### 1. Text Editors with Undo Feature:

Storing and restoring the state of a document or text editor to support undo/redo operations.

### 2. Transactional Systems:

Capturing and restoring the state of a transactional system to ensure data consistency in case of failures.

### 3. Game State Management:

Saving and loading the state of a game to allow players to resume their progress.

## Different implementations of Memento Design Pattern

### 1. Memento Design Pattern using Class:

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

### 2. Memento Design Pattern using Records:

`java`
```java
// Memento record
public record Memento(String state) {}

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
### 3. Memento Design Pattern with History and Undo:

`java`
```java
import java.util.Stack;

// Memento class
class Memento {
    private final String state;

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
    private Stack<Memento> mementos = new Stack<>();

    public void setState(String state) {
        this.state = state;
        saveMemento();
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

    private void saveMemento() {
        mementos.push(createMemento());
    }

    public Memento undo() {
        if (!mementos.isEmpty()) {
            mementos.pop(); // Discard the current state
            return mementos.peek(); // Return the previous state
        } else {
            System.out.println("No more undo steps available.");
            return mementos.peek();
        }
    }
}

// Caretaker class
public class Caretaker
{
    // In this example, Caretaker is not used directly, as the history is managed within the Originator.
}

// Client code
public class MementoExample {
    public static void main(String[] args) {
        Originator originator = new Originator();

        // Save the initial state
        originator.setState("State 1");

        // Change the state and save
        originator.setState("State 2");

        // Change the state and save
        originator.setState("State 3");

        // Undo to the previous state
        originator.undo();

        // Display the current state
        System.out.println("Current State: " + originator.getState());
    }
}

```

`csharp`
```csharp
using System;
using System.Collections.Generic;

// Memento class
public record Memento(string State);

// Originator class
public class Originator
{
    private string state;
    private Stack<Memento> mementos = new Stack<Memento>();

    public void SetState(string state)
    {
        this.state = state;
        SaveMemento();
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

    private void SaveMemento()
    {
        mementos.Push(CreateMemento());
    }

    public Memento Undo()
    {
        if (mementos.Count > 1)
        {
            mementos.Pop(); // Discard the current state
            return mementos.Peek(); // Return the previous state
        }
        else
        {
            Console.WriteLine("No more undo steps available.");
            return mementos.Peek();
        }
    }
}

// Caretaker class
public class Caretaker
{
    // In this example, Caretaker is not used directly, as the history is managed within the Originator.
}

// Client code
class Program
{
    static void Main()
    {
        Originator originator = new Originator();

        // Save the initial state
        originator.SetState("State 1");

        // Change the state and save
        originator.SetState("State 2");

        // Change the state and save
        originator.SetState("State 3");

        // Undo to the previous state
        originator.Undo();

        // Display the current state
        Console.WriteLine("Current State: " + originator.GetState());
    }
}

```
