# Template

### What is a Template Design Pattern?

Template Design Pattern is a behavioral design pattern that defines the steps of an algorithm in the base class. Still, it lets the subclass override the implementation details of the algorithms, without changing the structure or the steps in which the methods are being called.

## Implementations of Template Design Pattern

### 1. Template Method Pattern

`java`
```java
// AbstractClass: JobScheduler
abstract class JobScheduler {
    // Template method
    public final void scheduleJob() {
        initializeJob();
        configureJobParameters();
        submitJob();
        notifyJobCompletion();
    }

    // Step: Initialize job (common to all jobs)
    protected void initializeJob() {
        System.out.println("Initializing job...");
    }

    // Step: Configure job parameters (specific to each job type)
    protected abstract void configureJobParameters();

    // Step: Submit job to the scheduler (common to all jobs)
    protected void submitJob() {
        System.out.println("Submitting job to the scheduler...");
    }

    // Step: Notify job completion (common to all jobs)
    protected void notifyJobCompletion() {
        System.out.println("Notifying job completion...");
    }
}

// ConcreteClassA: BatchJobScheduler
class BatchJobScheduler extends JobScheduler {
    @Override
    protected void configureJobParameters() {
        System.out.println("Configuring batch job parameters...");
    }
}

// ConcreteClassB: RealTimeJobScheduler
class RealTimeJobScheduler extends JobScheduler {
    @Override
    protected void configureJobParameters() {
        System.out.println("Configuring real-time job parameters...");
    }
}

// Client code
public class Client {
    public static void main(String[] args) {
        // Using BatchJobScheduler
        JobScheduler batchJobScheduler = new BatchJobScheduler();
        System.out.println("Scheduling Batch Job:");
        batchJobScheduler.scheduleJob();
        System.out.println();

        // Using RealTimeJobScheduler
        JobScheduler realTimeJobScheduler = new RealTimeJobScheduler();
        System.out.println("Scheduling Real-Time Job:");
        realTimeJobScheduler.scheduleJob();
    }
}

```

`csharp`
```csharp
// AbstractClass: JobScheduler
abstract class JobScheduler
{
    // Template method
    public void ScheduleJob()
    {
        InitializeJob();
        ConfigureJobParameters();
        SubmitJob();
        NotifyJobCompletion();
    }

    // Step: Initialize job (common to all jobs)
    protected void InitializeJob()
    {
        Console.WriteLine("Initializing job...");
    }

    // Step: Configure job parameters (specific to each job type)
    protected abstract void ConfigureJobParameters();

    // Step: Submit job to the scheduler (common to all jobs)
    protected void SubmitJob()
    {
        Console.WriteLine("Submitting job to the scheduler...");
    }

    // Step: Notify job completion (common to all jobs)
    protected void NotifyJobCompletion()
    {
        Console.WriteLine("Notifying job completion...");
    }
}

// ConcreteClassA: BatchJobScheduler
class BatchJobScheduler : JobScheduler
{
    protected override void ConfigureJobParameters()
    {
        Console.WriteLine("Configuring batch job parameters...");
    }
}

// ConcreteClassB: RealTimeJobScheduler
class RealTimeJobScheduler : JobScheduler
{
    protected override void ConfigureJobParameters()
    {
        Console.WriteLine("Configuring real-time job parameters...");
    }
}

// Client code
class Client
{
    static void Main()
    {
        // Using BatchJobScheduler
        JobScheduler batchJobScheduler = new BatchJobScheduler();
        Console.WriteLine("Scheduling Batch Job:");
        batchJobScheduler.ScheduleJob();
        Console.WriteLine();

        // Using RealTimeJobScheduler
        JobScheduler realTimeJobScheduler = new RealTimeJobScheduler();
        Console.WriteLine("Scheduling Real-Time Job:");
        realTimeJobScheduler.ScheduleJob();
    }
}

```
