## Template Method 
The Template Method design pattern is a behavioral design pattern that allows you to define the skeleton of an algorithm in a base class while allowing subclasses to provide specific implementations of certain steps of the algorithm. It promotes code reuse and provides a way to define a common structure for a group of related algorithms.

Here's how the Template Method pattern works:

1. The pattern starts with the creation of an abstract base class (also known as the template class) that defines the overall structure of the algorithm. This class contains one or more abstract methods or hooks that subclasses must implement.

2. The base class also includes a template method, which is a method that defines the algorithm's skeleton. It consists of a series of method calls, including the abstract methods or hooks that subclasses will provide implementations for.

3. Subclasses inherit from the base class and override the abstract methods or hooks to provide their specific implementations. These subclasses can also choose to override or extend other methods from the base class, but they cannot change the overall structure defined by the template method.

4. Clients interact with the subclasses through the base class interface. They can create instances of specific subclasses and invoke the template method, which will execute the algorithm's steps in the predefined order, including the overridden or extended methods in the subclasses.

The Template Method pattern allows you to define a common structure for a group of related algorithms while providing flexibility for customizing specific steps of the algorithm in subclasses. It promotes code reuse and encapsulates the algorithm's details in the base class, allowing subclasses to focus on their specific implementations.

This pattern is particularly useful when you have a set of algorithms that share common steps but have variations in certain parts. By using the Template Method pattern, you can avoid code duplication and provide a consistent interface for clients to interact with different algorithm implementations.

Let's consider a real-world example of using the Template Method pattern in C# for building a web page template.

Suppose you are developing a web application that needs to generate different types of web pages, such as a home page, about page, and contact page. Each page may have a different layout and content, but they share some common elements, such as header, footer, and navigation menu.

Here's how you can apply the Template Method pattern to create a web page template:

```csharp
// Abstract class representing the web page template
abstract class WebPageTemplate
{
    public void GeneratePage()
    {
        GenerateHeader();
        GenerateContent();
        GenerateFooter();
    }

    protected abstract void GenerateContent();

    protected void GenerateHeader()
    {
        Console.WriteLine("Generating header...");
        // Common code for generating header
    }

    protected void GenerateFooter()
    {
        Console.WriteLine("Generating footer...");
        // Common code for generating footer
    }
}

// Concrete subclass representing the home page
class HomePage : WebPageTemplate
{
    protected override void GenerateContent()
    {
        Console.WriteLine("Generating home page content...");
        // Specific code for generating home page content
    }
}

// Concrete subclass representing the about page
class AboutPage : WebPageTemplate
{
    protected override void GenerateContent()
    {
        Console.WriteLine("Generating about page content...");
        // Specific code for generating about page content
    }
}

// Concrete subclass representing the contact page
class ContactPage : WebPageTemplate
{
    protected override void GenerateContent()
    {
        Console.WriteLine("Generating contact page content...");
        // Specific code for generating contact page content
    }
}

// Usage example
class Program
{
    static void Main(string[] args)
    {
        WebPageTemplate homePage = new HomePage();
        homePage.GeneratePage();

        Console.WriteLine();

        WebPageTemplate aboutPage = new AboutPage();
        aboutPage.GeneratePage();

        Console.WriteLine();

        WebPageTemplate contactPage = new ContactPage();
        contactPage.GeneratePage();

        Console.ReadLine();
    }
}
```

In this example, the `WebPageTemplate` class serves as the abstract base class defining the skeleton of the web page generation algorithm. The `GeneratePage()` method represents the template method, which calls the common methods like `GenerateHeader()` and `GenerateFooter()`, as well as the abstract method `GenerateContent()`, which must be implemented by the concrete subclasses.

The `HomePage`, `AboutPage`, and `ContactPage` classes are concrete subclasses that inherit from `WebPageTemplate`. They provide their specific implementations of the `GenerateContent()` method to generate the content specific to each page type.

When the `GeneratePage()` method is called on an instance of a concrete subclass, it executes the algorithm defined in the template method. The common elements like header and footer are generated by the base class, and the specific content is generated by the overridden method in the subclass.

By using the Template Method pattern, you can reuse the common code for generating the header and footer across different web page types, while allowing flexibility for customizing the content generation in each page type.