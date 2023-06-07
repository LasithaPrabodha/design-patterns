## Command 🔥
The Command design pattern is a behavioral design pattern that provides a way to encapsulate a request as an object, thereby allowing clients to parameterize clients with different requests, queue or log requests, and support undoable operations.

The pattern consists of the following key components:

1. Command: This is an interface or abstract class that declares an execution method. It usually defines methods such as `execute()` and `undo()`, which encapsulate the specific actions to be taken.

2. ConcreteCommand: This is a class that implements the Command interface. It defines the binding between a receiver object and the actions that need to be performed. It maintains a reference to the receiver and invokes the corresponding operations on it when the `execute()` method is called.

3. Receiver: This is the object that performs the actual actions associated with a command. It has the necessary knowledge and methods to carry out the request.

4. Invoker: This is a class that sends a command to execute a request. It holds a reference to a Command object and can invoke the command's `execute()` method.

5. Client: This is the class or code that creates and configures the command objects, the receivers, and the invoker. It decides which commands to execute at what points.

By using the Command pattern, clients are decoupled from the receivers and can request different operations without knowing the specific details of how the commands are executed. This pattern also provides flexibility by allowing commands to be queued, logged, and undone, making it useful in scenarios like menu systems, multi-level undo/redo functionality, and remote control systems.

Here's a real-world example of the Command design pattern in C#. Let's consider a simple home automation system where we have a remote control that can control various electronic devices such as lights, fans, and speakers.

```csharp
using System;

// Receiver
class Light
{
    public void TurnOn()
    {
        Console.WriteLine("Light is on");
    }

    public void TurnOff()
    {
        Console.WriteLine("Light is off");
    }
}

// Command interface
interface ICommand
{
    void Execute();
}

// Concrete command classes
class LightOnCommand : ICommand
{
    private Light light;

    public LightOnCommand(Light light)
    {
        this.light = light;
    }

    public void Execute()
    {
        light.TurnOn();
    }
}

class LightOffCommand : ICommand
{
    private Light light;

    public LightOffCommand(Light light)
    {
        this.light = light;
    }

    public void Execute()
    {
        light.TurnOff();
    }
}

// Invoker
class RemoteControl
{
    private ICommand command;

    public void SetCommand(ICommand command)
    {
        this.command = command;
    }

    public void PressButton()
    {
        command.Execute();
    }
}

// Client
class Program
{
    static void Main(string[] args)
    {
        // Create the receiver (light)
        Light livingRoomLight = new Light();

        // Create the concrete command objects
        LightOnCommand lightOnCommand = new LightOnCommand(livingRoomLight);
        LightOffCommand lightOffCommand = new LightOffCommand(livingRoomLight);

        // Create the invoker (remote control)
        RemoteControl remoteControl = new RemoteControl();

        // Configure the invoker with the appropriate commands
        remoteControl.SetCommand(lightOnCommand);

        // Press the button on the remote control
        remoteControl.PressButton(); // Light is on

        // Configure the invoker with a different command
        remoteControl.SetCommand(lightOffCommand);

        // Press the button again
        remoteControl.PressButton(); // Light is off
    }
}
```

In this example, we have a `Light` class that represents a receiver object. We define `LightOnCommand` and `LightOffCommand` as concrete command classes that implement the `ICommand` interface. The `RemoteControl` class acts as the invoker and can be configured with different commands. The client code sets up the commands and invokes them by pressing a button on the remote control.

When the `PressButton` method is called on the remote control, it executes the corresponding command, which, in turn, calls the appropriate methods on the receiver object (`Light`). This allows us to control the light by turning it on and off using the remote control.

Please note that this is a simplified example to illustrate the Command pattern. In a real-world scenario, you would have more complex receivers and commands, and the invoker might have additional functionality like maintaining a history of commands for undo/redo operations.