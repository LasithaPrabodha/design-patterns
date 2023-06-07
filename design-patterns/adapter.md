## Adapter 🔥
The Adapter design pattern is a software design pattern that allows the interface of an existing class to be used by another class that expects a different interface. It is a structural pattern that helps two incompatible interfaces work together without changing their existing code.

The purpose of the Adapter pattern is to convert the interface of one class into another interface that clients expect. This allows classes with incompatible interfaces to work together by creating a middleman adapter class that handles the conversion.

Here's how the Adapter pattern works:

1. Target Interface: This is the interface that the client expects to work with. It defines the methods or functionality that the client will use.

2. Adaptee: This is the class or component that has the functionality that the client does not directly support. It has a different interface that is incompatible with the client.

3. Adapter: This is the class that adapts the interface of the Adaptee to the Target Interface. It implements the Target Interface and internally uses an instance of the Adaptee to handle the requested functionality.

The Adapter pattern allows the client to work with the Adapter, which in turn translates the requests into a format that the Adaptee can understand and execute. This way, the client can utilize the functionality of the Adaptee without needing to modify its code.

The Adapter pattern provides a way to achieve interoperability between classes or components with different interfaces, allowing them to collaborate and work together seamlessly. It is commonly used in situations where existing code needs to be integrated with new code or when working with third-party libraries or APIs that have incompatible interfaces.

Here's a real-world example of the Adapter design pattern in C#:

Let's say you have an existing application that logs messages to a file using a `FileLogger` class. However, you want to introduce a new logging library called `NewLogger` that has a different interface and functionality. You want to integrate this new logging library into your existing application without modifying the code that already uses the `FileLogger`.

Here's how you can use the Adapter pattern to accomplish this:

```csharp
// Target Interface
public interface ILogger
{
    void Log(string message);
}

// Adaptee - Existing FileLogger class
public class FileLogger
{
    public void LogToFile(string message)
    {
        Console.WriteLine("Logging message to file: " + message);
    }
}

// Adapter
public class NewLoggerAdapter : ILogger
{
    private readonly NewLogger _newLogger;

    public NewLoggerAdapter(NewLogger newLogger)
    {
        _newLogger = newLogger;
    }

    public void Log(string message)
    {
        _newLogger.LogMessage(message);
    }
}

// New Logger - Adaptee
public class NewLogger
{
    public void LogMessage(string message)
    {
        Console.WriteLine("Logging message using new logger: " + message);
    }
}

// Client
public class Client
{
    private readonly ILogger _logger;

    public Client(ILogger logger)
    {
        _logger = logger;
    }

    public void DoSomething()
    {
        _logger.Log("Doing something");
    }
}

// Usage
public class Program
{
    public static void Main(string[] args)
    {
        // Create an instance of the FileLogger (existing class)
        FileLogger fileLogger = new FileLogger();

        // Create an instance of the NewLogger (new class)
        NewLogger newLogger = new NewLogger();

        // Create an instance of the NewLoggerAdapter and pass the NewLogger to its constructor
        ILogger adapter = new NewLoggerAdapter(newLogger);

        // Create an instance of the Client and inject the adapter
        Client client = new Client(adapter);
        client.DoSomething();
    }
}
```

In this example, the existing `FileLogger` class represents the Adaptee, which logs messages to a file using the `LogToFile` method. The `NewLogger` class represents the new logging library, which has a different interface and uses the `LogMessage` method.

The `ILogger` interface represents the target interface that the client expects to work with. The `NewLoggerAdapter` class implements this interface and internally uses an instance of the `NewLogger` class to handle the logging functionality.

In the `Main` method, we create an instance of the `FileLogger` and an instance of the `NewLogger`. Then, we create an instance of the `NewLoggerAdapter`, passing the `NewLogger` instance to its constructor. Finally, we create an instance of the `Client` and inject the adapter into it.

When `client.DoSomething()` is called, it will use the adapter to log the message using the `NewLogger` class. The adapter translates the call to the appropriate method of the `NewLogger` class, allowing the new logging library to be integrated seamlessly into the existing application without modifying the code that already uses the `FileLogger`.

This example demonstrates how the Adapter pattern can be used to integrate new functionality into an existing system without requiring changes to the existing codebase.