## Iterator 🔥
The Iterator design pattern is a behavioral design pattern that provides a way to access the elements of a collection sequentially without exposing its underlying structure. It decouples the client code from the implementation details of traversing a collection, making the code more flexible and reusable.

The Iterator pattern consists of two main components:

1. Iterator: This is an interface or an abstract class that defines the methods for traversing the collection. It typically includes methods like `next()`, `hasNext()`, `remove()`, etc., which allow the client to iterate over the elements of the collection.

2. Collection: This represents the collection of objects that the iterator will traverse. The collection may be implemented as an array, a list, a tree, or any other data structure. The collection provides a method to create an iterator object that can be used to traverse its elements.

The iterator object keeps track of the current position within the collection and provides methods to retrieve the next element and check if there are more elements available. The client can use these methods to iterate over the collection without worrying about its internal structure or implementation details.

By using the Iterator pattern, you can achieve several benefits, including:

- Separation of concerns: The client code is decoupled from the collection's implementation details, allowing them to vary independently.
- Single Responsibility Principle: The iterator is responsible for traversing the collection, separating the traversal logic from the collection itself.
- Flexibility: Different types of collections can have their own iterator implementations, providing specific traversal behaviors without affecting the client code.

Overall, the Iterator design pattern provides a standardized way to iterate over the elements of a collection, making the code more modular, maintainable, and reusable.

Let's consider a real-world example of using the Iterator design pattern in C# for a bookstore application. Assume we have a `Book` class representing a book with properties like `Title`, `Author`, and `Price`.

Here's an implementation of the Iterator pattern:

```csharp
// Book class representing a book
public class Book
{
    public string Title { get; set; }
    public string Author { get; set; }
    public decimal Price { get; set; }
}

// Iterator interface
public interface IIterator<T>
{
    T Next();
    bool HasNext();
}

// Concrete Iterator implementation for Book collection
public class BookIterator : IIterator<Book>
{
    private Book[] books;
    private int position;

    public BookIterator(Book[] books)
    {
        this.books = books;
        position = 0;
    }

    public Book Next()
    {
        Book book = books[position];
        position++;
        return book;
    }

    public bool HasNext()
    {
        return position < books.Length;
    }
}

// Collection class
public class BookCollection
{
    private Book[] books;

    public BookCollection()
    {
        books = new Book[0];
    }

    public void AddBook(Book book)
    {
        Array.Resize(ref books, books.Length + 1);
        books[books.Length - 1] = book;
    }

    public IIterator<Book> CreateIterator()
    {
        return new BookIterator(books);
    }
}

// Client code
public class Program
{
    static void Main()
    {
        BookCollection collection = new BookCollection();
        collection.AddBook(new Book { Title = "Book 1", Author = "Author 1", Price = 10.99m });
        collection.AddBook(new Book { Title = "Book 2", Author = "Author 2", Price = 19.99m });
        collection.AddBook(new Book { Title = "Book 3", Author = "Author 3", Price = 14.99m });

        IIterator<Book> iterator = collection.CreateIterator();

        while (iterator.HasNext())
        {
            Book book = iterator.Next();
            Console.WriteLine($"Title: {book.Title}, Author: {book.Author}, Price: {book.Price}");
        }
    }
}
```

In this example, we have a `BookCollection` class that represents a collection of books. It has a method `CreateIterator()` that creates and returns an iterator object (`BookIterator`).

The `BookIterator` class implements the `IIterator<Book>` interface. It maintains a reference to the book collection and keeps track of the current position. The `Next()` method returns the next book in the collection, and the `HasNext()` method checks if there are more books available.

The client code creates a `BookCollection` object, adds some books to it, and then creates an iterator using the `CreateIterator()` method. It uses the iterator to iterate over the books in the collection and displays their details.

By using the Iterator pattern, the client code can iterate over the book collection without having to know its internal structure. The traversal logic is encapsulated within the iterator object, providing a standardized way to access the books.