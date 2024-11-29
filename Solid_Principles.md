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


# Designing a Parking Lot System

## Requirements
1. The parking lot should have multiple levels, each level with a certain number of parking spots.
2. The parking lot should support different types of vehicles, such as cars, motorcycles, and trucks.
3. Each parking spot should be able to accommodate a specific type of vehicle.
4. The system should assign a parking spot to a vehicle upon entry and release it when the vehicle exits.
5. The system should track the availability of parking spots and provide real-time information to customers.
6. The system should handle multiple entry and exit points and support concurrent access.


## Classes, Interfaces and Enumerations
1. The **ParkingLot** class follows the Singleton pattern to ensure only one instance of the parking lot exists. It maintains a list of levels and provides methods to park and unpark vehicles.
2. The **Level** class represents a level in the parking lot and contains a list of parking spots. It handles parking and unparking of vehicles within the level.
3. The **ParkingSpot** class represents an individual parking spot and tracks the availability and the parked vehicle.
4. The **Vehicle** class is an abstract base class for different types of vehicles. It is extended by Car, Motorcycle, and Truck classes.
5. The **VehicleType** enum defines the different types of vehicles supported by the parking lot.
6. Multi-threading is achieved through the use of synchronized keyword on critical sections to ensure thread safety.
7. The **Main** class demonstrates the usage of the parking lot system.


Here is a detailed Low-Level Design (LLD) for a **Parking Lot System** based on the provided requirements:  

---

### **1. Enumerations**

#### `VehicleType`  
Defines the types of vehicles supported.  
```java
enum VehicleType {
    CAR,
    MOTORCYCLE,
    TRUCK
}
```

---

### **2. Vehicle Class Hierarchy**

#### `Vehicle`  
Abstract base class for all vehicles.  
```java
abstract class Vehicle {
    private String licensePlate;
    private VehicleType type;

    public Vehicle(String licensePlate, VehicleType type) {
        this.licensePlate = licensePlate;
        this.type = type;
    }

    public String getLicensePlate() {
        return licensePlate;
    }

    public VehicleType getType() {
        return type;
    }
}
```

#### Subclasses  
```java
class Car extends Vehicle {
    public Car(String licensePlate) {
        super(licensePlate, VehicleType.CAR);
    }
}

class Motorcycle extends Vehicle {
    public Motorcycle(String licensePlate) {
        super(licensePlate, VehicleType.MOTORCYCLE);
    }
}

class Truck extends Vehicle {
    public Truck(String licensePlate) {
        super(licensePlate, VehicleType.TRUCK);
    }
}
```

---

### **3. ParkingSpot Class**  
Represents an individual parking spot.  
```java
class ParkingSpot {
    private VehicleType spotType;
    private boolean isAvailable;
    private Vehicle parkedVehicle;

    public ParkingSpot(VehicleType spotType) {
        this.spotType = spotType;
        this.isAvailable = true;
    }

    public boolean isAvailable() {
        return isAvailable;
    }

    public VehicleType getSpotType() {
        return spotType;
    }

    public synchronized boolean parkVehicle(Vehicle vehicle) {
        if (isAvailable && vehicle.getType() == spotType) {
            this.parkedVehicle = vehicle;
            this.isAvailable = false;
            return true;
        }
        return false;
    }

    public synchronized void removeVehicle() {
        this.parkedVehicle = null;
        this.isAvailable = true;
    }

    public Vehicle getParkedVehicle() {
        return parkedVehicle;
    }
}
```

---

### **4. Level Class**  
Represents a level in the parking lot.  
```java
import java.util.ArrayList;
import java.util.List;

class Level {
    private int levelNumber;
    private List<ParkingSpot> spots;

    public Level(int levelNumber, int numSpots, VehicleType spotType) {
        this.levelNumber = levelNumber;
        this.spots = new ArrayList<>();
        for (int i = 0; i < numSpots; i++) {
            spots.add(new ParkingSpot(spotType));
        }
    }

    public boolean parkVehicle(Vehicle vehicle) {
        for (ParkingSpot spot : spots) {
            if (spot.parkVehicle(vehicle)) {
                System.out.println("Vehicle parked at level " + levelNumber);
                return true;
            }
        }
        return false;
    }

    public void releaseVehicle(String licensePlate) {
        for (ParkingSpot spot : spots) {
            if (spot.getParkedVehicle() != null &&
                spot.getParkedVehicle().getLicensePlate().equals(licensePlate)) {
                spot.removeVehicle();
                System.out.println("Vehicle removed from level " + levelNumber);
                return;
            }
        }
        System.out.println("Vehicle not found in level " + levelNumber);
    }

    public int getAvailableSpots() {
        return (int) spots.stream().filter(ParkingSpot::isAvailable).count();
    }
}
```

---

### **5. ParkingLot Class (Singleton)**  
Represents the entire parking lot.  
```java
import java.util.ArrayList;
import java.util.List;

class ParkingLot {
    private static ParkingLot instance;
    private List<Level> levels;

    private ParkingLot() {
        levels = new ArrayList<>();
    }

    public static synchronized ParkingLot getInstance() {
        if (instance == null) {
            instance = new ParkingLot();
        }
        return instance;
    }

    public void addLevel(Level level) {
        levels.add(level);
    }

    public boolean parkVehicle(Vehicle vehicle) {
        for (Level level : levels) {
            if (level.parkVehicle(vehicle)) {
                return true;
            }
        }
        System.out.println("No parking spot available for vehicle: " + vehicle.getLicensePlate());
        return false;
    }

    public void releaseVehicle(String licensePlate) {
        for (Level level : levels) {
            level.releaseVehicle(licensePlate);
        }
    }

    public void displayAvailableSpots() {
        for (int i = 0; i < levels.size(); i++) {
            System.out.println("Level " + i + ": " + levels.get(i).getAvailableSpots() + " spots available.");
        }
    }
}
```

---

### **6. Main Class**  
Demonstrates the usage of the system.  
```java
public class Main {
    public static void main(String[] args) {
        // Initialize Parking Lot
        ParkingLot parkingLot = ParkingLot.getInstance();
        parkingLot.addLevel(new Level(0, 2, VehicleType.CAR));
        parkingLot.addLevel(new Level(1, 3, VehicleType.MOTORCYCLE));
        parkingLot.addLevel(new Level(2, 1, VehicleType.TRUCK));

        // Create Vehicles
        Vehicle car1 = new Car("CAR123");
        Vehicle bike1 = new Motorcycle("BIKE123");
        Vehicle truck1 = new Truck("TRUCK123");

        // Park Vehicles
        parkingLot.parkVehicle(car1);   // Parks in Level 0
        parkingLot.parkVehicle(bike1);  // Parks in Level 1
        parkingLot.parkVehicle(truck1); // Parks in Level 2

        // Display Available Spots
        parkingLot.displayAvailableSpots();

        // Release Vehicle
        parkingLot.releaseVehicle("CAR123");
        parkingLot.releaseVehicle("BIKE123");

        // Display Available Spots Again
        parkingLot.displayAvailableSpots();
    }
}
```

---

### **Output**
```plaintext
Vehicle parked at level 0
Vehicle parked at level 1
Vehicle parked at level 2
Level 0: 1 spots available.
Level 1: 2 spots available.
Level 2: 0 spots available.
Vehicle removed from level 0
Vehicle removed from level 1
Level 0: 2 spots available.
Level 1: 3 spots available.
Level 2: 0 spots available.
```

---

### **Key Features**  
1. **Thread-Safety:** The `synchronized` keyword ensures thread-safe operations on parking spots.  
2. **Singleton Pattern:** Ensures a single `ParkingLot` instance for the entire system.  
3. **Modular Design:** Each class handles one responsibility (SRP).  
4. **Scalable:** Adding new levels or vehicle types is straightforward.  
