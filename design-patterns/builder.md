## Builder 
The Builder design pattern is a creational design pattern that is used to construct complex objects step by step. It separates the construction of an object from its representation, allowing the same construction process to create different representations.

The main idea behind the Builder pattern is to encapsulate the construction logic within a separate class (the builder) that knows how to create the object. The builder exposes methods to set the individual attributes or properties of the object, and then a separate method to retrieve the constructed object.

Here's an example of how the Builder pattern can be implemented in C#:

```csharp
// The product being built
class Pizza
{
    public string Dough { get; set; }
    public string Sauce { get; set; }
    public string Topping { get; set; }
}

// Abstract builder class
abstract class PizzaBuilder
{
    protected Pizza pizza;

    public void CreateNewPizza()
    {
        pizza = new Pizza();
    }

    public Pizza GetPizza()
    {
        return pizza;
    }

    public abstract void SetDough();
    public abstract void SetSauce();
    public abstract void SetTopping();
}

// Concrete builder classes
class HawaiianPizzaBuilder : PizzaBuilder
{
    public override void SetDough()
    {
        pizza.Dough = "cross";
    }

    public override void SetSauce()
    {
        pizza.Sauce = "mild";
    }

    public override void SetTopping()
    {
        pizza.Topping = "ham+pineapple";
    }
}

class SpicyPizzaBuilder : PizzaBuilder
{
    public override void SetDough()
    {
        pizza.Dough = "pan baked";
    }

    public override void SetSauce()
    {
        pizza.Sauce = "hot";
    }

    public override void SetTopping()
    {
        pizza.Topping = "pepperoni+salami";
    }
}

// Director class
class Cook
{
    private PizzaBuilder pizzaBuilder;

    public void SetPizzaBuilder(PizzaBuilder builder)
    {
        pizzaBuilder = builder;
    }

    public Pizza GetPizza()
    {
        return pizzaBuilder.GetPizza();
    }

    public void ConstructPizza()
    {
        pizzaBuilder.CreateNewPizza();
        pizzaBuilder.SetDough();
        pizzaBuilder.SetSauce();
        pizzaBuilder.SetTopping();
    }
}

// Client code
class Program
{
    static void Main(string[] args)
    {
        var cook = new Cook();

        var hawaiianPizzaBuilder = new HawaiianPizzaBuilder();
        cook.SetPizzaBuilder(hawaiianPizzaBuilder);
        cook.ConstructPizza();
        var hawaiianPizza = cook.GetPizza();

        var spicyPizzaBuilder = new SpicyPizzaBuilder();
        cook.SetPizzaBuilder(spicyPizzaBuilder);
        cook.ConstructPizza();
        var spicyPizza = cook.GetPizza();

        Console.WriteLine("Hawaiian pizza: " + hawaiianPizza.Dough + ", " + hawaiianPizza.Sauce + ", " + hawaiianPizza.Topping);
        Console.WriteLine("Spicy pizza: " + spicyPizza.Dough + ", " + spicyPizza.Sauce + ", " + spicyPizza.Topping);
    }
}
```

In this example, we have a `Pizza` class representing the product being built. We define an abstract `PizzaBuilder` class with methods to set the dough, sauce, and topping. We also have concrete builder classes, `HawaiianPizzaBuilder` and `SpicyPizzaBuilder`, that implement the abstract builder and provide their own implementation of the methods.

The `Cook` class acts as the director and orchestrates the construction process. It has a `SetPizzaBuilder` method to set the specific builder and a `ConstructPizza` method