## Composite 🔥
The Composite design pattern is a structural design pattern that allows you to treat individual objects and groups of objects uniformly, by creating a hierarchical structure. It composes objects into tree-like structures to represent part-whole hierarchies.

The main idea behind the Composite pattern is that a single object (leaf) or a group of objects (composite) can be treated in the same way. This pattern enables clients to perform operations on individual objects as well as on collections of objects.

Here are the key components of the Composite pattern:

1. Component: This is the base interface or abstract class that defines the common operations for both the leaf objects and composite objects. It declares methods for accessing and manipulating the objects.

2. Leaf: It represents the individual objects that do not have any children. They implement the operations defined by the Component interface.

3. Composite: It represents the container or composite objects that can hold a collection of child objects. It implements the operations defined by the Component interface. It also provides methods to add, remove, and access child components.

The Composite pattern allows you to create complex structures by combining objects in a tree-like hierarchy. This pattern is useful when you need to represent part-whole hierarchies and want to treat individual objects and groups of objects uniformly. It provides a flexible way to work with objects and simplifies the client code by abstracting the complexity of the underlying structure.

Let's consider a real-world example of a file system in C# to demonstrate the Composite pattern.

```csharp
using System;
using System.Collections.Generic;

// Component
interface IFileSystemComponent
{
    void PrintName();
}

// Leaf
class File : IFileSystemComponent
{
    private string name;

    public File(string name)
    {
        this.name = name;
    }

    public void PrintName()
    {
        Console.WriteLine(name);
    }
}

// Composite
class Directory : IFileSystemComponent
{
    private string name;
    private List<IFileSystemComponent> components;

    public Directory(string name)
    {
        this.name = name;
        components = new List<IFileSystemComponent>();
    }

    public void AddComponent(IFileSystemComponent component)
    {
        components.Add(component);
    }

    public void RemoveComponent(IFileSystemComponent component)
    {
        components.Remove(component);
    }

    public void PrintName()
    {
        Console.WriteLine("Directory: " + name);

        foreach (var component in components)
        {
            component.PrintName();
        }
    }
}

class Program
{
    static void Main(string[] args)
    {
        // Create files
        var file1 = new File("file1.txt");
        var file2 = new File("file2.txt");
        var file3 = new File("file3.txt");

        // Create directories
        var dir1 = new Directory("Directory 1");
        var dir2 = new Directory("Directory 2");
        var dir3 = new Directory("Directory 3");

        // Add files to directories
        dir1.AddComponent(file1);
        dir2.AddComponent(file2);
        dir3.AddComponent(file3);

        // Create a composite directory
        var compositeDir = new Directory("Composite Directory");
        compositeDir.AddComponent(dir1);
        compositeDir.AddComponent(dir2);
        compositeDir.AddComponent(dir3);

        // Print the names of all files and directories
        compositeDir.PrintName();
    }
}
```

In this example, we have three types of objects: `File`, `Directory`, and `Composite Directory`. The `File` class represents a leaf object, which is a file in the file system. The `Directory` class represents a composite object, which can contain other files or directories. The `Composite Directory` class is also a composite object that holds multiple directories.

We create files and directories and add them to the composite directory. Finally, we call the `PrintName` method on the composite directory, which recursively prints the names of all files and directories within the composite structure.

This example demonstrates how the Composite pattern allows us to treat individual files and directories uniformly, simplifying the client code and providing a flexible way to work with the file system components.