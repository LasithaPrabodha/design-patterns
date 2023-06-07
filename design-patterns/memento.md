## Memento 
The Memento design pattern is a behavioral design pattern that provides a way to capture and restore an object's internal state without violating encapsulation. It allows you to save the state of an object at a particular point in time and restore it later, effectively providing undo and redo mechanisms or checkpoints for an object.

The pattern consists of three main components:

1. Originator: This is the object whose state needs to be saved and restored. It creates a memento object that represents its internal state and can also restore its state from a memento.

2. Memento: This is an immutable object that stores the state of the originator. It provides a way to retrieve the saved state but does not expose any methods that would allow modification of the state.

3. Caretaker: This object is responsible for keeping track of the mementos. It requests a memento from the originator and stores it. It can also provide mementos back to the originator for restoring its state.

The typical flow of the Memento pattern involves the following steps:

1. The client creates an originator object and performs some operations on it.

2. When the client wants to save the state, it requests a memento from the originator, which creates a memento object containing its current state and returns it to the client.

3. The client stores the memento in a caretaker object.

4. If the client wants to restore the state, it retrieves the desired memento from the caretaker and provides it back to the originator. The originator then restores its state based on the memento.

By using the Memento pattern, you can separate the responsibility of state management from the originator, providing a clean and flexible way to save and restore object states. It helps in maintaining encapsulation and can be particularly useful in scenarios where you need to implement undo/redo functionality or implement checkpoints in an application.

Let's consider a real-world example of a text editor application in C#. The Memento pattern can be used to implement an undo/redo functionality.

```csharp
// Originator
public class TextEditor
{
    private string text;

    public string Text
    {
        get { return text; }
        set { text = value; }
    }

    public TextEditorMemento Save()
    {
        return new TextEditorMemento(text);
    }

    public void Restore(TextEditorMemento memento)
    {
        text = memento.Text;
    }
}

// Memento
public class TextEditorMemento
{
    private string text;

    public TextEditorMemento(string text)
    {
        this.text = text;
    }

    public string Text
    {
        get { return text; }
    }
}

// Caretaker
public class UndoManager
{
    private Stack<TextEditorMemento> mementos = new Stack<TextEditorMemento>();

    public void SaveState(TextEditorMemento memento)
    {
        mementos.Push(memento);
    }

    public TextEditorMemento Undo()
    {
        if (mementos.Count > 1)
        {
            mementos.Pop(); // Discard the current state
            return mementos.Peek(); // Return the previous state
        }

        return null; // No previous state available
    }
}

// Client
public class Program
{
    public static void Main(string[] args)
    {
        TextEditor textEditor = new TextEditor();
        UndoManager undoManager = new UndoManager();

        textEditor.Text = "Hello";

        undoManager.SaveState(textEditor.Save());

        textEditor.Text = "Hello World";

        undoManager.SaveState(textEditor.Save());

        Console.WriteLine("Current Text: " + textEditor.Text);

        textEditor.Restore(undoManager.Undo());

        Console.WriteLine("Undo Text: " + textEditor.Text);
    }
}
```

In this example, the `TextEditor` class represents the originator that has a `Text` property representing the text being edited. It provides methods to save the current state as a memento (`Save()`) and restore the state from a given memento (`Restore()`).

The `TextEditorMemento` class represents the memento object that stores the state of the `TextEditor`. It has a `Text` property to retrieve the saved text.

The `UndoManager` class acts as a caretaker and maintains a stack of mementos. It has methods to save the state (`SaveState()`) and retrieve the previous state (`Undo()`).

In the `Main` method, we create a `TextEditor`, an `UndoManager`, and perform some text editing operations. We save the states of the `TextEditor` using `SaveState()` and restore the previous state using `Undo()`.

When executed, the program will output:

```
Current Text: Hello World
Undo Text: Hello
```

This example demonstrates how the Memento pattern allows us to save and restore the state of a `TextEditor` object, providing undo functionality by maintaining a history of previous states.