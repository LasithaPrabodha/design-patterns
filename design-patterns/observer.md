## Observer 🔥
The Observer design pattern is a behavioral design pattern that defines a one-to-many dependency between objects, so that when one object changes its state, all its dependents are notified and updated automatically. It is also known as the Publish-Subscribe pattern.

The Observer pattern consists of two main components:

1. Subject: The subject is the object that maintains a list of its dependents, known as observers. It provides an interface to attach and detach observers, as well as a mechanism to notify them of any state changes.

2. Observer: The observer is the object that is interested in receiving updates from the subject. It defines an interface that the subject uses to notify the observer of any changes.

Here's how the Observer pattern typically works:

1. The subject maintains a list of observers and provides methods to attach, detach, and notify observers.

2. Observers register themselves with the subject by attaching to it. This is usually done by implementing the observer interface and providing the necessary callback methods.

3. When the state of the subject changes, it notifies all its observers by calling a predefined method or methods on each observer. This allows the observers to update themselves with the new state or perform any other necessary actions.

4. Observers can also detach from the subject if they are no longer interested in receiving updates.

The Observer pattern promotes loose coupling between the subject and the observers. The subject doesn't need to know the concrete classes of its observers, and the observers can be added or removed dynamically without affecting the subject or other observers. This flexibility makes the Observer pattern useful in scenarios where multiple objects need to react to changes in another object's state.

Overall, the Observer pattern provides a way to establish relationships between objects where changes in one object can automatically trigger updates in other dependent objects, promoting maintainability and extensibility in software systems.

Let's consider a real-world example of the Observer pattern in C# within the context of a weather monitoring system.

```csharp
using System;
using System.Collections.Generic;

// Subject (Observable)
class WeatherStation
{
    private double temperature;
    private List<IObserver> observers = new List<IObserver>();

    public void Attach(IObserver observer)
    {
        observers.Add(observer);
    }

    public void Detach(IObserver observer)
    {
        observers.Remove(observer);
    }

    public void SetTemperature(double temperature)
    {
        this.temperature = temperature;
        Notify();
    }

    private void Notify()
    {
        foreach (IObserver observer in observers)
        {
            observer.Update(temperature);
        }
    }
}

// Observer
interface IObserver
{
    void Update(double temperature);
}

// Concrete Observer
class TemperatureDisplay : IObserver
{
    public void Update(double temperature)
    {
        Console.WriteLine("Temperature Display: " + temperature + " °C");
    }
}

class HumidityDisplay : IObserver
{
    public void Update(double temperature)
    {
        Console.WriteLine("Humidity Display: " + GetHumidity(temperature) + " %");
    }

    private double GetHumidity(double temperature)
    {
        // Just a placeholder logic for demonstration
        return temperature * 0.6;
    }
}

class Program
{
    static void Main(string[] args)
    {
        WeatherStation weatherStation = new WeatherStation();

        TemperatureDisplay tempDisplay = new TemperatureDisplay();
        HumidityDisplay humDisplay = new HumidityDisplay();

        weatherStation.Attach(tempDisplay);
        weatherStation.Attach(humDisplay);

        weatherStation.SetTemperature(25.5);

        weatherStation.Detach(humDisplay);

        weatherStation.SetTemperature(30.0);

        Console.ReadLine();
    }
}
```

In the example above, we have a `WeatherStation` class that acts as the subject (observable). It maintains a list of observers (`IObserver`), which in this case are the `TemperatureDisplay` and `HumidityDisplay` classes. 

The `WeatherStation` class provides methods to attach and detach observers, as well as a `SetTemperature` method to update the temperature. Whenever the temperature changes, the `WeatherStation` notifies all its observers by calling the `Update` method on each observer.

The `TemperatureDisplay` and `HumidityDisplay` classes implement the `IObserver` interface, which requires them to have an `Update` method. Each observer defines its own behavior in response to the temperature update.

In the `Main` method, we create instances of the `WeatherStation`, `TemperatureDisplay`, and `HumidityDisplay` classes. We attach both displays to the weather station and then set the temperature to 25.5°C. Both displays receive the update and print the temperature and humidity accordingly. Later, we detach the `HumidityDisplay` and set the temperature to 30.0°C, which results in only the `TemperatureDisplay` being updated.

This example demonstrates how the Observer pattern allows multiple objects (`TemperatureDisplay` and `HumidityDisplay`) to observe and react to changes in the state of another object (`WeatherStation`) without being tightly coupled.