## Strategy 🔥
The Strategy design pattern is a behavioral design pattern that allows you to define a family of interchangeable algorithms, encapsulate each one as a separate class, and make them interchangeable at runtime. This pattern enables you to select and use a specific algorithm from a set of available algorithms dynamically, depending on the context or specific requirements.

Here's how the Strategy design pattern typically works:

1. Define the Strategy interface: This interface declares a method or a set of methods that represent the algorithms. It defines a common interface that all the concrete strategy classes must implement.

2. Implement concrete strategies: Each concrete strategy class provides a specific implementation of the algorithm defined in the Strategy interface. These classes encapsulate the algorithm and can vary independently from each other.

3. Use a context or client class: The context or client class holds a reference to the strategy object and delegates the algorithm's execution to the strategy. It can interact with the strategy object through the common interface provided by the Strategy interface.

4. Set the strategy at runtime: The context or client class can set or change the strategy object at runtime. This flexibility allows the application to switch between different strategies dynamically, without modifying the client code.

The Strategy pattern promotes loose coupling between the client and the concrete strategies, as well as separates the algorithm implementation from the client code. This pattern is useful when you have a set of similar algorithms that need to be interchangeable or when you want to provide different behavior variations for a specific task.

By utilizing the Strategy pattern, you can achieve more flexible and maintainable code that can adapt to changing requirements or preferences without introducing significant modifications or complexities.

Let's consider a real-world example of a payment processing system implemented in C# that utilizes the Strategy design pattern.

```csharp
// Step 1: Define the Strategy interface
public interface IPaymentStrategy
{
    void ProcessPayment(double amount);
}

// Step 2: Implement concrete strategies
public class CreditCardPaymentStrategy : IPaymentStrategy
{
    public void ProcessPayment(double amount)
    {
        // Logic to process payment using a credit card
        Console.WriteLine($"Processing credit card payment of {amount}$");
    }
}

public class PayPalPaymentStrategy : IPaymentStrategy
{
    public void ProcessPayment(double amount)
    {
        // Logic to process payment using PayPal
        Console.WriteLine($"Processing PayPal payment of {amount}$");
    }
}

// Step 3: Use a context or client class
public class PaymentProcessor
{
    private IPaymentStrategy paymentStrategy;

    public PaymentProcessor(IPaymentStrategy paymentStrategy)
    {
        this.paymentStrategy = paymentStrategy;
    }

    public void ProcessPayment(double amount)
    {
        paymentStrategy.ProcessPayment(amount);
    }
}

// Step 4: Set the strategy at runtime
public class Program
{
    public static void Main()
    {
        // Client code
        double amount = 100.00;

        PaymentProcessor processor;

        // Select a payment strategy dynamically based on user's choice
        Console.WriteLine("Please select a payment method: 1 - Credit Card, 2 - PayPal");
        int choice = int.Parse(Console.ReadLine());

        if (choice == 1)
        {
            processor = new PaymentProcessor(new CreditCardPaymentStrategy());
        }
        else if (choice == 2)
        {
            processor = new PaymentProcessor(new PayPalPaymentStrategy());
        }
        else
        {
            Console.WriteLine("Invalid choice.");
            return;
        }

        // Process the payment using the selected strategy
        processor.ProcessPayment(amount);
    }
}
```

In this example, we have a payment processing system that supports different payment methods, such as credit card and PayPal. The `IPaymentStrategy` interface defines the common `ProcessPayment` method that all concrete strategies must implement. The `CreditCardPaymentStrategy` and `PayPalPaymentStrategy` classes provide specific implementations for processing payments using credit cards and PayPal, respectively.

The `PaymentProcessor` class serves as the context or client class, which accepts a payment strategy during its construction. It delegates the payment processing to the strategy object. The client code can create an instance of the `PaymentProcessor` class and provide a specific payment strategy dynamically based on user input or other conditions.

At runtime, the user is prompted to select a payment method, and based on the choice, the appropriate concrete strategy is instantiated and passed to the `PaymentProcessor`. The `ProcessPayment` method is then called, which executes the payment processing logic specific to the selected strategy.

This way, the payment processing system can easily switch between different payment strategies without modifying the core logic. New payment strategies can also be added without impacting the existing code, promoting extensibility and maintainability.