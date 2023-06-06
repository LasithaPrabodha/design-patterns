## Proxy 🔥
The Proxy design pattern is a structural design pattern that provides a surrogate or placeholder for another object to control its access. It allows you to create a substitute or representative object that can perform additional actions before or after accessing the original object. The proxy object acts as an intermediary between the client and the real object, allowing the client to interact with the object indirectly.

The Proxy pattern is useful in scenarios where you want to add an extra layer of control or functionality to the original object without modifying its code. It can be applied in various situations, such as remote communication, access control, caching, lazy loading, logging, and more.

The Proxy pattern typically consists of three main components:

1. Proxy: This is the object that acts as a substitute for the real object. It implements the same interface as the real object and maintains a reference to it. The proxy controls the access to the real object, performing additional tasks if necessary.

2. Real Subject: This is the actual object with the business logic or functionality that the client wants to access. The proxy holds a reference to the real subject and delegates the requested operations to it.

3. Client: The client is the code that interacts with the proxy object, assuming it is working directly with the real subject. The client remains unaware of the proxy's existence and interacts with it through the same interface as the real object.

Here's an example of the Proxy design pattern in C#:

```csharp
using System;

// Interface implemented by both RealSubject and Proxy
interface IImage
{
    void Display();
}

// RealSubject - The actual object representing an image
class RealImage : IImage
{
    private string filename;

    public RealImage(string filename)
    {
        this.filename = filename;
        LoadFromDisk();
    }

    private void LoadFromDisk()
    {
        Console.WriteLine("Loading image: " + filename);
    }

    public void Display()
    {
        Console.WriteLine("Displaying image: " + filename);
    }
}

// Proxy - The surrogate object that controls access to RealImage
class ImageProxy : IImage
{
    private string filename;
    private RealImage realImage;

    public ImageProxy(string filename)
    {
        this.filename = filename;
    }

    public void Display()
    {
        if (realImage == null)
        {
            realImage = new RealImage(filename);
        }
        realImage.Display();
    }
}

// Client code
class Program
{
    static void Main(string[] args)
    {
        IImage image = new ImageProxy("example.jpg");
        // The client interacts with the proxy, not the real object
        image.Display();
    }
}
```

In this example, the `RealImage` class represents the actual image object, and the `ImageProxy` acts as a proxy controlling access to it. The `IImage` interface is implemented by both the `RealImage` and `ImageProxy` classes, ensuring they have a common set of methods.

When the client calls the `Display()` method on the proxy, it checks if the real image has been loaded. If not, it creates an instance of `RealImage` and then delegates the display operation to it.

You can run this code in a C# environment to see the output:

```
Loading image: example.jpg
Displaying image: example.jpg
```

The Proxy pattern provides a way to add an additional layer of control or functionality to an object, without modifying its core implementation.