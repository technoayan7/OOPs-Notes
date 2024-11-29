Solid Principles in Java help you write clean, organized, and maintainable code. Think of them as "rules" to avoid confusion and bugs. Here's a simple explanation with examples:  

---

### 1. **Single Responsibility Principle (SRP)**  
**Rule:** A class should do only one thing.  

**Example:**  
A class `Student` should only manage student details, not save data to a file.  
```java
// BAD
class Student {
    void getDetails() { /* Fetch student details */ }
    void saveToFile() { /* Save to file */ } // Unrelated work
}

// GOOD
class Student {
    void getDetails() { /* Fetch student details */ }
}
class FileManager {
    void saveToFile() { /* Save to file */ }
}
```

---

### 2. **Open/Closed Principle (OCP)**  
**Rule:** A class should be open for extension but closed for modification.  

**Example:**  
Adding new shapes without changing existing code.  
```java
// BAD
class AreaCalculator {
    double calculate(String shape, double radius, double length) {
        if (shape.equals("Circle")) return Math.PI * radius * radius;
        else if (shape.equals("Square")) return length * length; 
        // Keep adding conditions for new shapes
    }
}

// GOOD
abstract class Shape {
    abstract double calculateArea();
}

class Circle extends Shape {
    double radius;
    Circle(double radius) { this.radius = radius; }
    double calculateArea() { return Math.PI * radius * radius; }
}

class Square extends Shape {
    double length;
    Square(double length) { this.length = length; }
    double calculateArea() { return length * length; }
}
```

---

### 3. **Liskov Substitution Principle (LSP)**  
**Rule:** Subclasses should work as a substitute for their parent class without breaking anything.  

**Example:**  
If `Bird` is a parent class, subclasses like `Sparrow` should behave like a bird.  

```java
// BAD
class Bird {
    void fly() { System.out.println("Flying"); }
}

class Penguin extends Bird {
    // Penguins don't fly! Violates LSP
}

// GOOD
abstract class Bird {
    abstract void move();
}

class Sparrow extends Bird {
    void move() { System.out.println("Flying"); }
}

class Penguin extends Bird {
    void move() { System.out.println("Swimming"); }
}
```

---

### 4. **Interface Segregation Principle (ISP)**  
**Rule:** Don’t force a class to implement methods it doesn’t need.  

**Example:**  
```java
// BAD
interface Animal {
    void fly();
    void swim();
}

class Dog implements Animal {
    public void fly() { /* Empty or throws error */ } // Dogs don't fly
    public void swim() { System.out.println("Dog swimming"); }
}

// GOOD
interface Flyable {
    void fly();
}

interface Swimmable {
    void swim();
}

class Dog implements Swimmable {
    public void swim() { System.out.println("Dog swimming"); }
}
```

---

### 5. **Dependency Inversion Principle (DIP)**  
**Rule:** High-level modules (main code) should not depend on low-level modules (details). Both should depend on abstractions (interfaces).  

**Example:**  
```java
// BAD
class Keyboard { /* Low-level module */ }
class Computer {
    Keyboard keyboard = new Keyboard(); // Hardcoded dependency
}

// GOOD
interface InputDevice { /* Abstract */ }
class Keyboard implements InputDevice { /* Low-level */ }
class Computer {
    InputDevice device; // Uses abstraction
    Computer(InputDevice device) { this.device = device; }
}
```

---

### Why Use These?  
- Makes your code easier to understand.  
- Reduces bugs and errors.  
- Easier to add new features without breaking old code.  


Here’s a complete **Low-Level Design (LLD)** example of a **Library Management System** in Java, following SOLID principles:  

---

### **Scenario**  
The system allows users to:  
1. Search for books by title or author.  
2. Borrow and return books.  
3. Maintain user and book data.

---

### **Code**  

#### **1. Book Class**
Represents a book in the library.  
```java
class Book {
    private String id;
    private String title;
    private String author;
    private boolean isAvailable;

    public Book(String id, String title, String author) {
        this.id = id;
        this.title = title;
        this.author = author;
        this.isAvailable = true;
    }

    public String getId() { return id; }
    public String getTitle() { return title; }
    public String getAuthor() { return author; }
    public boolean isAvailable() { return isAvailable; }

    public void borrowBook() { this.isAvailable = false; }
    public void returnBook() { this.isAvailable = true; }
}
```

---

#### **2. User Class**
Represents a library user.  
```java
class User {
    private String userId;
    private String name;

    public User(String userId, String name) {
        this.userId = userId;
        this.name = name;
    }

    public String getUserId() { return userId; }
    public String getName() { return name; }
}
```

---

#### **3. Library Class**
Manages the collection of books and user interactions.  
```java
import java.util.ArrayList;
import java.util.List;
import java.util.stream.Collectors;

class Library {
    private List<Book> books;

    public Library() {
        books = new ArrayList<>();
    }

    public void addBook(Book book) {
        books.add(book);
    }

    public List<Book> searchByTitle(String title) {
        return books.stream()
                .filter(book -> book.getTitle().equalsIgnoreCase(title))
                .collect(Collectors.toList());
    }

    public List<Book> searchByAuthor(String author) {
        return books.stream()
                .filter(book -> book.getAuthor().equalsIgnoreCase(author))
                .collect(Collectors.toList());
    }

    public boolean borrowBook(String bookId, User user) {
        for (Book book : books) {
            if (book.getId().equals(bookId) && book.isAvailable()) {
                book.borrowBook();
                System.out.println(user.getName() + " borrowed " + book.getTitle());
                return true;
            }
        }
        System.out.println("Book not available for borrowing.");
        return false;
    }

    public void returnBook(String bookId, User user) {
        for (Book book : books) {
            if (book.getId().equals(bookId) && !book.isAvailable()) {
                book.returnBook();
                System.out.println(user.getName() + " returned " + book.getTitle());
                return;
            }
        }
        System.out.println("Invalid return attempt.");
    }
}
```

---

#### **4. Main Class**
Tests the Library Management System.  
```java
public class LibraryManagementSystem {
    public static void main(String[] args) {
        // Create Library
        Library library = new Library();

        // Add Books
        library.addBook(new Book("1", "Java Basics", "John Doe"));
        library.addBook(new Book("2", "Python Guide", "Jane Smith"));
        library.addBook(new Book("3", "Data Structures", "John Doe"));

        // Create User
        User user = new User("101", "Alice");

        // Search by Title
        System.out.println("Search Results for 'Java Basics':");
        for (Book book : library.searchByTitle("Java Basics")) {
            System.out.println(book.getTitle() + " by " + book.getAuthor());
        }

        // Borrow Book
        library.borrowBook("1", user);

        // Try to Borrow the Same Book Again
        library.borrowBook("1", user);

        // Return Book
        library.returnBook("1", user);

        // Try to Return the Same Book Again
        library.returnBook("1", user);
    }
}
```

---

### **Output**
```plaintext
Search Results for 'Java Basics':
Java Basics by John Doe
Alice borrowed Java Basics
Book not available for borrowing.
Alice returned Java Basics
Invalid return attempt.
```

---

### **Explanation**  
1. **SOLID Applied:**
   - **SRP:** Each class has a single responsibility (e.g., `Book` for book data, `Library` for management).  
   - **OCP:** Easily extend the system (e.g., add new features like user membership).  
   - **LSP:** Subclasses (if created) can replace parent classes without issues.  
   - **ISP:** Interfaces could be introduced if required (e.g., for different types of books).  
   - **DIP:** `Library` interacts with `Book` and `User` through methods, no hard coupling.  

2. The design is modular and flexible for future extensions, like adding genres or late fees.
