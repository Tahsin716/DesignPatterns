# State

### What is the State Design Pattern?

State Design Pattern is a behavioral design pattern that allows an object to alter its behavior when its internal state changes.

## What are the use cases of the State Design Pattern?

### 1. Object with Multiple States:

When an object exhibits different behaviors based on its internal state.

### 2. Stateful Components:

When you want to model the behavior of a component with a finite set of well-defined states.

### 3. Workflow Systems:

In systems where an object goes through different states as it progresses through a workflow.

### 4. Game Characters:

Representing the behavior of characters in a game that can be in various states (e.g., attacking, defending, idle).

## Implementations of the State Design Pattern:

#### Gumball Machine
Consider a gumball machine that can be in three states: **NoQuarterState**, **HasQuarterState**, and **SoldState**. The machine can perform different actions based on its current state, such as: 
- accepting a quarter
- dispensing a gumball
- or returning a quarter.

### 1. State Design Pattern:

`java`
```java
// State interface
public interface GumballMachineState {
    void insertQuarter();
    void ejectQuarter();
    void turnCrank();
    void dispense();
}

// Concrete state: NoQuarterState
public class NoQuarterState implements GumballMachineState {
    private final GumballMachine machine;

    public NoQuarterState(GumballMachine machine) {
        this.machine = machine;
    }

    @Override
    public void insertQuarter() {
        System.out.println("You inserted a quarter.");
        machine.setState(machine.getHasQuarterState());
    }

    @Override
    public void ejectQuarter() {
        System.out.println("You haven't inserted a quarter.");
    }

    @Override
    public void turnCrank() {
        System.out.println("You turned, but there's no quarter.");
    }

    @Override
    public void dispense() {
        System.out.println("You need to pay first.");
    }
}

// Concrete state: HasQuarterState
public class HasQuarterState implements GumballMachineState {
    private final GumballMachine machine;

    public HasQuarterState(GumballMachine machine) {
        this.machine = machine;
    }

    @Override
    public void insertQuarter() {
        System.out.println("You can't insert another quarter.");
    }

    @Override
    public void ejectQuarter() {
        System.out.println("Quarter returned.");
        machine.setState(machine.getNoQuarterState());
    }

    @Override
    public void turnCrank() {
        System.out.println("You turned the crank. Gumball coming!");
        machine.setState(machine.getSoldState());
    }

    @Override
    public void dispense() {
        System.out.println("No gumball dispensed.");
    }
}

// Concrete state: SoldState
public class SoldState implements GumballMachineState {
    private final GumballMachine machine;

    public SoldState(GumballMachine machine) {
        this.machine = machine;
    }

    @Override
    public void insertQuarter() {
        System.out.println("Please wait, we're already giving you a gumball.");
    }

    @Override
    public void ejectQuarter() {
        System.out.println("Sorry, you already turned the crank.");
    }

    @Override
    public void turnCrank() {
        System.out.println("Turning twice doesn't get you another gumball!");
    }

    @Override
    public void dispense() {
        machine.releaseGumball();
        if (machine.getCount() > 0) {
            machine.setState(machine.getNoQuarterState());
        } else {
            System.out.println("Oops, out of gumballs!");
            machine.setState(machine.getSoldOutState());
        }
    }
}

// Context class (Gumball machine)
public class GumballMachine {
    private GumballMachineState state;
    private int count = 0;

    private final GumballMachineState noQuarterState;
    private final GumballMachineState hasQuarterState;
    private final GumballMachineState soldState;
    private final GumballMachineState soldOutState;

    public GumballMachine(int initialCount) {
        count = initialCount;
        noQuarterState = new NoQuarterState(this);
        hasQuarterState = new HasQuarterState(this);
        soldState = new SoldState(this);
        soldOutState = new SoldOutState(this);

        if (initialCount > 0) {
            state = noQuarterState;
        } else {
            state = soldOutState;
        }
    }

    // Methods to perform actions based on the current state
    public void insertQuarter() {
        state.insertQuarter();
    }

    public void ejectQuarter() {
        state.ejectQuarter();
    }

    public void turnCrank() {
        state.turnCrank();
        state.dispense();
    }

    // Other methods...
    
    // State transition methods
    public void setState(GumballMachineState state) {
        this.state = state;
    }

    public GumballMachineState getNoQuarterState() {
        return noQuarterState;
    }

    public GumballMachineState getHasQuarterState() {
        return hasQuarterState;
    }

    public GumballMachineState getSoldState() {
        return soldState;
    }

    public GumballMachineState getSoldOutState() {
        return soldOutState;
    }

    // Other methods...
}

public class Client {
    public static void main(String[] args) {
        GumballMachine gumballMachine = new GumballMachine(5);

        gumballMachine.insertQuarter();
        gumballMachine.turnCrank();

        gumballMachine.insertQuarter();
        gumballMachine.ejectQuarter();
        gumballMachine.turnCrank();

        gumballMachine.insertQuarter();
        gumballMachine.turnCrank();
        gumballMachine.insertQuarter();
        gumballMachine.turnCrank();
        gumballMachine.insertQuarter();
        gumballMachine.turnCrank();
    }
}


```

`csharp`
```csharp
using System;

// State interface
public interface IGumballMachineState
{
    void InsertQuarter();
    void EjectQuarter();
    void TurnCrank();
    void Dispense();
}

// Concrete States
public class NoQuarterState : IGumballMachineState
{
    private readonly GumballMachine machine;

    public NoQuarterState(GumballMachine machine)
    {
        this.machine = machine;
    }

    public void InsertQuarter()
    {
        Console.WriteLine("You inserted a quarter.");
        machine.SetState(machine.HasQuarterState);
    }

    public void EjectQuarter()
    {
        Console.WriteLine("You haven't inserted a quarter.");
    }

    public void TurnCrank()
    {
        Console.WriteLine("You turned, but there's no quarter.");
    }

    public void Dispense()
    {
        Console.WriteLine("You need to pay first.");
    }
}

public class HasQuarterState : IGumballMachineState
{
    private readonly GumballMachine machine;

    public HasQuarterState(GumballMachine machine)
    {
        this.machine = machine;
    }

    public void InsertQuarter()
    {
        Console.WriteLine("You can't insert another quarter.");
    }

    public void EjectQuarter()
    {
        Console.WriteLine("Quarter returned.");
        machine.SetState(machine.NoQuarterState);
    }

    public void TurnCrank()
    {
        Console.WriteLine("You turned the crank. Gumball coming!");
        machine.SetState(machine.SoldState);
    }

    public void Dispense()
    {
        Console.WriteLine("No gumball dispensed.");
    }
}

public class SoldState : IGumballMachineState
{
    private readonly GumballMachine machine;

    public SoldState(GumballMachine machine)
    {
        this.machine = machine;
    }

    public void InsertQuarter()
    {
        Console.WriteLine("Please wait, we're already giving you a gumball.");
    }

    public void EjectQuarter()
    {
        Console.WriteLine("Sorry, you already turned the crank.");
    }

    public void TurnCrank()
    {
        Console.WriteLine("Turning twice doesn't get you another gumball!");
    }

    public void Dispense()
    {
        machine.ReleaseGumball();
        if (machine.Count > 0)
        {
            machine.SetState(machine.NoQuarterState);
        }
        else
        {
            Console.WriteLine("Oops, out of gumballs!");
            machine.SetState(machine.SoldOutState);
        }
    }
}

public class SoldOutState : IGumballMachineState
{
    private readonly GumballMachine machine;

    public SoldOutState(GumballMachine machine)
    {
        this.machine = machine;
    }

    public void InsertQuarter()
    {
        Console.WriteLine("Sorry, the machine is sold out.");
    }

    public void EjectQuarter()
    {
        Console.WriteLine("No quarter to eject.");
    }

    public void TurnCrank()
    {
        Console.WriteLine("You turned, but there are no gumballs.");
    }

    public void Dispense()
    {
        Console.WriteLine("No gumball dispensed.");
    }
}

// Context class (Gumball machine)
public class GumballMachine
{
    private IGumballMachineState state;
    private int count;

    public GumballMachine(int initialCount)
    {
        count = initialCount;
        NoQuarterState = new NoQuarterState(this);
        HasQuarterState = new HasQuarterState(this);
        SoldState = new SoldState(this);
        SoldOutState = new SoldOutState(this);

        if (initialCount > 0)
        {
            state = NoQuarterState;
        }
        else
        {
            state = SoldOutState;
        }
    }

    // Methods to perform actions based on the current state
    public void InsertQuarter() => state.InsertQuarter();

    public void EjectQuarter() => state.EjectQuarter();

    public void TurnCrank()
    {
        state.TurnCrank();
        state.Dispense();
    }

    // Other methods...

    // State transition methods
    public void SetState(IGumballMachineState newState) => state = newState;

    public IGumballMachineState NoQuarterState { get; }
    public IGumballMachineState HasQuarterState { get; }
    public IGumballMachineState SoldState { get; }
    public IGumballMachineState SoldOutState { get; }

    // Other methods...
}

// Client code
class Program
{
    static void Main()
    {
        GumballMachine gumballMachine = new GumballMachine(5);

        gumballMachine.InsertQuarter();
        gumballMachine.TurnCrank();

        gumballMachine.InsertQuarter();
        gumballMachine.EjectQuarter();
        gumballMachine.TurnCrank();

        gumballMachine.InsertQuarter();
        gumballMachine.TurnCrank();
        gumballMachine.InsertQuarter();
        gumballMachine.TurnCrank();
        gumballMachine.InsertQuarter();
        gumballMachine.TurnCrank();
    }
}

```
