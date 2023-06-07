## Decorator 
The Decorator design pattern is a structural design pattern that allows you to add behavior or functionalities to an object dynamically at runtime without affecting the behavior of other objects of the same class. It is used to enhance the functionality of individual objects by wrapping them with one or more decorator classes.

In the Decorator pattern, there is an abstract base class (often called the "Component") that defines the common interface for both the core object and its decorators. The core object represents the original object to which additional functionalities can be added, while the decorators provide the additional functionalities.

Here's how the Decorator pattern works:

1. Define an abstract base class (Component) that declares the common interface for both the core object and its decorators.
2. Create a concrete implementation of the Component class, representing the core object that you want to enhance with additional functionalities.
3. Create one or more decorator classes that inherit from the Component class. These decorators have a similar interface to the Component but also contain a reference to an instance of the Component.
4. The decorators add their own behavior by delegating some or all of the work to the wrapped Component instance and then performing additional actions before or after the delegated work.
5. You can stack multiple decorators on top of each other, adding multiple layers of functionality to the core object.

The key benefits of using the Decorator pattern include:

1. It provides a flexible alternative to subclassing for extending the functionality of objects at runtime.
2. It allows you to add and remove responsibilities dynamically, as decorators can be easily added or removed.
3. It follows the Open-Closed Principle, as it allows classes to be easily extended with new decorators without modifying existing code.

Overall, the Decorator pattern enables you to add new behaviors to objects without modifying their original implementation, promoting code reuse and flexibility in object composition.

Let's consider a real-world example of a beverage ordering system using the Decorator pattern in C#.

Suppose you have a base interface called `IBeverage` that represents a beverage and defines the `GetCost()` and `GetDescription()` methods:

```csharp
public interface IBeverage
{
    decimal GetCost();
    string GetDescription();
}
```

Now, let's create a concrete implementation of the `IBeverage` interface called `Coffee`, which represents a basic coffee:

```csharp
public class Coffee : IBeverage
{
    public decimal GetCost()
    {
        return 2.0m; // Base cost of coffee
    }

    public string GetDescription()
    {
        return "Coffee";
    }
}
```

Now, let's create some decorator classes that will add additional functionalities to the core `Coffee` object. For example, let's create a `Milk` decorator that adds milk to the coffee:

```csharp
public class Milk : IBeverage
{
    private readonly IBeverage _beverage;

    public Milk(IBeverage beverage)
    {
        _beverage = beverage;
    }

    public decimal GetCost()
    {
        return _beverage.GetCost() + 0.5m; // Additional cost for milk
    }

    public string GetDescription()
    {
        return _beverage.GetDescription() + ", Milk";
    }
}
```

Similarly, let's create another decorator called `Sugar` that adds sugar to the coffee:

```csharp
public class Sugar : IBeverage
{
    private readonly IBeverage _beverage;

    public Sugar(IBeverage beverage)
    {
        _beverage = beverage;
    }

    public decimal GetCost()
    {
        return _beverage.GetCost() + 0.25m; // Additional cost for sugar
    }

    public string GetDescription()
    {
        return _beverage.GetDescription() + ", Sugar";
    }
}
```

Now, you can create a coffee object and wrap it with various decorators to customize the beverage according to the customer's preferences:

```csharp
// Create a basic coffee
IBeverage coffee = new Coffee();

// Add milk to the coffee
coffee = new Milk(coffee);

// Add sugar to the coffee
coffee = new Sugar(coffee);

Console.WriteLine(coffee.GetDescription()); // Output: Coffee, Milk, Sugar
Console.WriteLine(coffee.GetCost()); // Output: 2.75
```

In this example, the `Coffee` object is decorated with `Milk` and `Sugar` decorators, which dynamically add the functionalities of adding milk and sugar to the coffee. The `GetDescription()` method returns the description of the coffee with the added decorators, and the `GetCost()` method returns the total cost of the beverage.

By using the Decorator pattern, you can easily add or remove functionalities at runtime and create customized beverages with different combinations of decorators.