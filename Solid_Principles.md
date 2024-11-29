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
