## Design Patterns
Design patterns in software engineering are reusable solutions to commonly occurring problems in software design. They provide proven approaches and best practices for structuring, organizing, and solving specific design problems. Design patterns help improve the quality, flexibility, and maintainability of software systems.

The 23 Gang of Four (GoF) patterns are generally considered the foundation for all other patterns. They are categorized in three groups: Creational, Structural, and Behavioral (for a complete list see below). This reference provides source code for each of the 23 GoF patterns.

1. Creational Patterns:
    - [Singleton](singleton.md): Ensures that a class has only one instance and provides a global point of access to it.
    - [Factory Method](factory-method.md): Defines an interface for creating objects, but lets subclasses decide which class to instantiate.
    - [Abstract Factory](abstract-factory.md): Provides an interface for creating families of related or dependent objects.
    - [Builder](builder.md): Separates the construction of complex objects from their representation, allowing the same construction process to create various representations.
    - [Prototype](prototype.md): Creates new objects by cloning existing ones, avoiding the need for explicit instantiation.


2. Structural Patterns:
    - [Adapter](adapter.md): Converts the interface of a class into another interface that clients expect.
    - [Decorator](decorator.md): Dynamically adds responsibilities to an object without modifying its structure.
    - [Proxy](proxy.md): Provides a surrogate or placeholder for another object to control access to it.
    - [Composite](composite.md): Composes objects into a tree structure to represent part-whole hierarchies.
    - [Bridge](bridge.md): Separates an abstraction from its implementation, allowing them to vary independently.
    - [Facade](fascade.md): Provides a simplified interface to a complex subsystem, making it easier to use.
    - [Flyweight](flyweight.md): Aims to minimize the memory usage and improve performance by sharing objects with similar or identical state across multiple contexts.

3. Behavioral Patterns:
    - [Observer](observer.md): Defines a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically.
    - [Strategy](strategy.md): Encapsulates interchangeable algorithms within a family and makes them interchangeable.
    - [Command](command.md): Encapsulates a request as an object, thereby letting you parameterize clients with queues, requests, and operations.
    - [Iterator](iterator.md): Provides a way to access the elements of an aggregate object sequentially without exposing its underlying representation.
    - [Template Method](template-method.md): Defines the skeleton of an algorithm in a base class, allowing subclasses to override specific steps of the algorithm.
    - [State](state.md): Allows an object to alter its behavior when its internal state changes.
    - Chain of Responsibility: Enables an object to pass a request along a chain of potential handlers until one handles it.
    - [Mediator](mediator.md): Defines an object that encapsulates how a set of objects interact, promoting loose coupling between them.
    - [Visitor](visitor.md): Separates an algorithm from the objects it operates on by placing the algorithm in a separate visitor object.
    - [Chain of Resp.](chain-of-responsibility.md): Allows an object to pass a request along a chain of potential handlers until one of them handles it.
    - [Interpreter](interpreter.md): Defines a representation of a grammar and provides a way to evaluate and interpret sentences in that grammar
    - [Memento](memento.md): Allows capturing and restoring the internal state of an object without violating encapsulation

Other design patterns we might need to consider checking out,

1. Architectural Patterns:
   - Model-View-Controller (MVC): Separates the application into three interconnected components (Model, View, Controller) to achieve separation of concerns.
   - Model-View-ViewModel (MVVM): Similar to MVC, but introduces a ViewModel that exposes data and actions to the View.
   - Layered Architecture: Separates the application into multiple layers (e.g., presentation, business logic, data access) to enforce modularity and maintainability.

2. Concurrency Patterns:
   - Producer-Consumer: Provides a way to decouple the production and consumption of data, allowing multiple threads to work together efficiently.
   - Mutex: Provides exclusive access to a shared resource by allowing only one thread to acquire a lock at a time.
   - Read-Write Lock: Allows concurrent read access to a resource but exclusive write access.

Each pattern has a specific intent and addresses different aspects of software design. It's important to choose and apply patterns appropriately based on the problem at hand and the specific requirements of the software system.