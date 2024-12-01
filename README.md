# 📝 **OOP Concepts Notes**  

---

## 🎯 **Class vs. Object**

| **Class**                             | **Object**                             |
|---------------------------------------|----------------------------------------|
| Blueprint or template for objects.    | Instance of a class.                   |
| Logical entity.                      | Physical entity.                       |
| Defines attributes and methods.      | Has specific values for attributes.    |
| Shared across objects.               | Unique representation of the class.    |
| `Car` class defines structure.       | `myCar` is an object of `Car`.         |

---

## 🛠️ **Static vs Non-Static Method**  

| **Static Method**                          | **Non-Static Method**                  |
|--------------------------------------------|----------------------------------------|
| Belongs to the class, not an instance.     | Belongs to an instance of the class.   |
| Can be called without creating an object.  | Requires an object to be called.       |
| Only static data and methods.              | Both static and non-static data/methods.|
| Called using `ClassName::methodName`.      | Called using `objectName.methodName`.  |
| `Math::sqrt(x)`.                          | `car.startEngine()`.                   |

---

## 🔒 **Public vs Private Constructor**  

| **Public Constructor**                          | **Private Constructor**                         |
|------------------------------------------------|------------------------------------------------|
| Accessible from outside the class.              | Restricted to within the class.                |
| Freely creates objects in any program part.     | Limits object creation (e.g., Singleton).      |
| Used for general object creation.               | Used in Singleton design patterns.             |
| Multiple instances easily created.             | Controlled/Single instance ensured.            |

### **Java Examples**  

#### **Public Constructor**  
```java
class Car {
    public Car() {  // Public Constructor
        System.out.println("Car created!");
    }
}

public class Main {
    public static void main(String[] args) {
        Car myCar = new Car();  // Instantiating from outside
    }
}
```
**Output**:  
```
Car created!
```

#### **Private Constructor**  
```java
class Singleton {
    private static Singleton instance;

    private Singleton() {  // Private Constructor
        System.out.println("Singleton instance created!");
    }

    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();  // Only created inside the class
        }
        return instance;
    }
}

public class Main {
    public static void main(String[] args) {
        Singleton obj1 = Singleton.getInstance();  // Access via method
        Singleton obj2 = Singleton.getInstance();  // Returns same instance
    }
}
```
**Output**:  
```
Singleton instance created!
```

---

## 🔑 **OOP Principles with Examples**  

| **Principle**     | **Definition**                                | **Real-Life Example**                  |
|--------------------|-----------------------------------------------|----------------------------------------|
| **Abstraction**    | Hides internal details; shows relevant parts.| Using an ATM.                          |
| **Encapsulation**  | Restricts access, exposes via methods.       | Medicine in a capsule.                 |
| **Inheritance**    | Reuses properties of a parent class.         | Child inherits parent's traits.        |
| **Polymorphism**   | Same method behaves differently in contexts. | Person acts as Student, Friend, Employee.|

---

### 1️⃣ **Abstraction**  
- **Definition**: Hiding implementation details, exposing only essential features.  
- **Example**: Using an ATM without knowing its internal workings.  

**Java Example**:  
```java
abstract class Vehicle {
    abstract void move();  // Abstract method

    void fuel() {  // Concrete method
        System.out.println("Vehicle needs fuel.");
    }
}

class Car extends Vehicle {
    @Override
    void move() {
        System.out.println("Car moves on roads.");
    }
}

public class Main {
    public static void main(String[] args) {
        Vehicle vehicle = new Car();
        vehicle.move();
        vehicle.fuel();
    }
}
```
**Output**:  
```
Car moves on roads.  
Vehicle needs fuel.
```

---

### 2️⃣ **Encapsulation**  
- **Definition**: Wrapping data (variables) and code (methods) together while restricting access.  
- **Example**: Capsule encloses medicine to protect contents.  

**Java Example**:  
```java
class BankAccount {
    private double balance;  // Private variable

    public double getBalance() {  // Getter
        return balance;
    }

    public void setBalance(double balance) {  // Setter
        if (balance > 0) {
            this.balance = balance;
        } else {
            System.out.println("Invalid balance amount.");
        }
    }
}

public class Main {
    public static void main(String[] args) {
        BankAccount account = new BankAccount();
        account.setBalance(1000);
        System.out.println("Balance: " + account.getBalance());
    }
}
```
**Output**:  
```
Balance: 1000
```

---

### 3️⃣ **Inheritance**  
- **Definition**: Acquiring properties and methods from a parent class.  
- **Example**: Child inherits traits from parents.  

**Java Example**:  
```java
class Animal {
    void eat() {
        System.out.println("This animal eats food.");
    }
}

class Dog extends Animal {
    void bark() {
        System.out.println("Dog barks.");
    }
}

public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog();
        dog.eat();  // Inherited method
        dog.bark();
    }
}
```
**Output**:  
```
This animal eats food.  
Dog barks.
```

---

### 4️⃣ **Polymorphism**  
- **Definition**: Ability of a method to behave differently based on context.  
- **Types**:  
  - Compile-time (method overloading).  
  - Run-time (method overriding).  
- **Example**: Person acts as a student, friend, or employee in different situations.  

**Java Example (Overriding)**:  
```java
class Shape {
    void draw() {
        System.out.println("Drawing a shape.");
    }
}

class Circle extends Shape {
    @Override
    void draw() {
        System.out.println("Drawing a circle.");
    }
}

public class Main {
    public static void main(String[] args) {
        Shape shape = new Circle();  // Runtime polymorphism
        shape.draw();
    }
}
```
**Output**:  
```
Drawing a circle.
``` 

---

## 🔀 **Polymorphism Types**  

### 1️⃣ **Compile-Time Polymorphism (Method Overloading)**  

| **Aspect**          | **Details**                                         |
|----------------------|-----------------------------------------------------|
| **Definition**       | Same method name with different parameter lists.    |
| **Achieved Through** | Method Overloading.                                 |
| **Resolved At**      | Compile-time.                                       |
| **Key Points**       | - Changes in method signature (parameters).         |
|                      | - Improves readability and reusability.             |
| **Real-Life Example**| A calculator adds integers, floats, or doubles.     |

**Java Example**:  
```java
class Calculator {  
    int add(int a, int b) {  
        return a + b;  
    }  

    double add(double a, double b) {  
        return a + b;  
    }  

    int add(int a, int b, int c) {  
        return a + b + c;  
    }  
}  

public class Main {  
    public static void main(String[] args) {  
        Calculator calc = new Calculator();  
        System.out.println(calc.add(5, 3));         // Calls add(int, int)  
        System.out.println(calc.add(5.5, 3.5));     // Calls add(double, double)  
        System.out.println(calc.add(1, 2, 3));      // Calls add(int, int, int)  
    }  
}
```
**Output**:  
```
8  
9.0  
6  
```

---

### 2️⃣ **Run-Time Polymorphism (Method Overriding)**  

| **Aspect**          | **Details**                                         |
|----------------------|-----------------------------------------------------|
| **Definition**       | Subclass provides specific implementation for a parent class method. |
| **Achieved Through** | Method Overriding.                                  |
| **Resolved At**      | Run-time.                                           |
| **Key Points**       | - Requires inheritance and `@Override`.             |
|                      | - Enables dynamic behavior based on object type.    |
| **Real-Life Example**| Vehicles move differently: car on roads, boat on water.|

**Java Example**:  
```java
class Vehicle {  
    void move() {  
        System.out.println("Vehicle is moving.");  
    }  
}  

class Car extends Vehicle {  
    @Override  
    void move() {  
        System.out.println("Car moves on roads.");  
    }  
}  

class Boat extends Vehicle {  
    @Override  
    void move() {  
        System.out.println("Boat sails on water.");  
    }  
}  

public class Main {  
    public static void main(String[] args) {  
        Vehicle vehicle;  

        vehicle = new Car();  
        vehicle.move();  // Calls Car's move()  

        vehicle = new Boat();  
        vehicle.move();  // Calls Boat's move()  
    }  
}
```
**Output**:  
```
Car moves on roads.  
Boat sails on water.  
```

---

## ⚔️ **Comparison: Method Overloading vs Method Overriding**  

| **Feature**         | **Method Overloading**            | **Method Overriding**               |
|----------------------|------------------------------------|--------------------------------------|
| **Binding**          | Compile-time                     | Run-time                             |
| **Inheritance**      | Not required                     | Requires inheritance                 |
| **Method Signature** | Same name, different parameters  | Same name and parameters             |
| **Usage**            | Improves readability             | Provides specific subclass behavior  |
| **Example**          | `add(int, int)` vs `add(double, double)` | `move()` in `Vehicle` vs `Car`       |

---

## 🛠️ **Abstract Class vs Interface**  

### 1️⃣ **Abstract Class**  

| **Aspect**          | **Details**                                         |
|----------------------|-----------------------------------------------------|
| **Definition**       | Can have abstract (no body) and concrete (implemented) methods. |
| **Purpose**          | Provides shared functionality and enforces method implementation. |
| **Key Features**     | - Supports single inheritance.                     |
|                      | - Can have fields, constructors, and static methods.|
| **Real-Life Example**| A `Vehicle` concept shared by cars, bikes, etc.     |

**Java Example**:  
```java
abstract class Vehicle {  
    abstract void move();  // Abstract method (no body)  

    void fuel() {  // Concrete method  
        System.out.println("Vehicle needs fuel.");
    }  
}  

class Car extends Vehicle {  
    @Override  
    void move() {  
        System.out.println("Car moves on roads.");  
    }  
}  

public class Main {  
    public static void main(String[] args) {  
        Vehicle myCar = new Car();  
        myCar.move();  // Calls Car's move()  
        myCar.fuel();  // Calls Vehicle's fuel()  
    }  
}
```
**Output**:  
```
Car moves on roads.  
Vehicle needs fuel.  
```

---

### 2️⃣ **Interface**  

| **Aspect**          | **Details**                                         |
|----------------------|-----------------------------------------------------|
| **Definition**       | A blueprint with only abstract methods (prior to Java 8). From Java 8, supports default/static methods. |
| **Purpose**          | Achieves full abstraction and supports multiple inheritance. |
| **Key Features**     | - All methods are `public` and `abstract` by default. |
|                      | - Only constants allowed, no constructors.          |
|                      | - A class can implement multiple interfaces.        |
| **Real-Life Example**| A `RemoteControl` interface for devices like TVs or ACs.|

**Java Example**:  
```java
interface RemoteControl {  
    void turnOn();  // Abstract method  

    void turnOff();  

    default void reset() {  // Default method (Java 8+)  
        System.out.println("Resetting to factory settings.");
    }  
}  

class TV implements RemoteControl {  
    @Override  
    public void turnOn() {  
        System.out.println("TV is now ON.");
    }  

    @Override  
    public void turnOff() {  
        System.out.println("TV is now OFF.");
    }  
}  

public class Main {  
    public static void main(String[] args) {  
        RemoteControl tv = new TV();  
        tv.turnOn();  
        tv.reset();  
        tv.turnOff();  
    }  
}
```
**Output**:  
```
TV is now ON.  
Resetting to factory settings.  
TV is now OFF.  
```

---

## 🆚 **Abstract Class vs Interface**  

| **Feature**          | **Abstract Class**                                  | **Interface**                              |
|-----------------------|----------------------------------------------------|-------------------------------------------|
| **Methods**           | Abstract and concrete methods.                     | Abstract methods; default methods since Java 8. |
| **Fields**            | Can have instance variables.                       | Only constants (`public static final`).    |
| **Inheritance**       | Single inheritance.                                | Supports multiple inheritance.             |
| **Access Modifiers**  | Can have private, protected, and public methods.   | All methods are `public` by default.       |
| **Constructors**      | Allowed.                                           | Not allowed.                               |
| **Usage**             | Use for shared functionality among related classes.| Use to define a contract for implementation. |

**Key Takeaways**:  
- Use **Abstract Class** to share common functionality among related classes.  
- Use **Interface** to define a contract that unrelated classes can implement.  

---

## 🛠️ **Types of Constructors**  

| **Type**              | **Description**                                                    | **Example Use**                           |
|-----------------------|--------------------------------------------------------------------|-------------------------------------------|
| **Default Constructor** | No parameters; auto-generated if no other constructors exist.    | When no specific initialization is needed.|
| **Parameterized Constructor** | Accepts parameters to initialize attributes.              | To set specific values during object creation. |
| **Copy Constructor**   | Copies values from another object of the same class.             | To create a copy of an existing object.   |
| **Private Constructor** | Restricts instantiation outside the class.                      | Used in Singleton Design Pattern.         |

### **Examples**  

1️⃣ **Default Constructor**:  
```java
class Car {
    String model;
    int year;

    public Car() {  // Default constructor
        model = "Unknown";
        year = 0;
    }

    void display() {
        System.out.println("Model: " + model + ", Year: " + year);
    }
}

public class Main {
    public static void main(String[] args) {
        Car car = new Car();  // Default constructor called
        car.display();        // Output: Model: Unknown, Year: 0
    }
}
```

2️⃣ **Parameterized Constructor**:  
```java
class Car {
    String model;
    int year;

    public Car(String model, int year) {  // Parameterized constructor
        this.model = model;
        this.year = year;
    }

    void display() {
        System.out.println("Model: " + model + ", Year: " + year);
    }
}

public class Main {
    public static void main(String[] args) {
        Car car = new Car("Tesla", 2023);  // Initialize with values
        car.display();                     // Output: Model: Tesla, Year: 2023
    }
}
```

3️⃣ **Copy Constructor**:  
```java
class Car {
    String model;
    int year;

    public Car(String model, int year) {  // Parameterized constructor
        this.model = model;
        this.year = year;
    }

    public Car(Car car) {  // Copy constructor
        this.model = car.model;
        this.year = car.year;
    }

    void display() {
        System.out.println("Model: " + model + ", Year: " + year);
    }
}

public class Main {
    public static void main(String[] args) {
        Car original = new Car("Tesla", 2023);  // Original object
        Car copy = new Car(original);          // Copy constructor
        copy.display();                        // Output: Model: Tesla, Year: 2023
    }
}
```

4️⃣ **Private Constructor (Singleton)**:  
```java
class Singleton {
    private static Singleton instance;

    private Singleton() {}  // Private constructor

    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}

public class Main {
    public static void main(String[] args) {
        Singleton obj1 = Singleton.getInstance();
        Singleton obj2 = Singleton.getInstance();
        System.out.println(obj1 == obj2);  // Output: true (same instance)
    }
}
```

---

## 🆚 **Shallow Copy vs Deep Copy**  

| **Shallow Copy**                                  | **Deep Copy**                              |
|--------------------------------------------------|-------------------------------------------|
| Copies object references; changes in nested objects reflect in both copies. | Copies objects recursively, creating independent copies. |
| Faster (only references are copied).             | Slower (requires recursive copying).      |
| When only the outer structure needs duplication. | When full independence between objects is required. |

### **Examples**  

- **Shallow Copy**: Default object copying in Java (`clone()` method without deep logic).  
- **Deep Copy**: Custom implementation to duplicate nested objects.  


