### Class Vs Object
---

| **Class**                            | **Object**                           |
|--------------------------------------|--------------------------------------|
| Blueprint or template for objects.  | Instance of a class.                 |
| Logical entity.                      | Physical entity.                     |
| Defines attributes and methods.      | Has specific values for attributes.  |
| Shared properties across objects.    | Unique representation of the class.  |
| Example: `Car` class defines structure.| Example: `myCar` is an object of `Car`. |

### Static Vs Non Static Method
---

| **Static Method**                                    | **Non-Static Method**                                |
|------------------------------------------------------|----------------------------------------------------|
| Belongs to the class, not an instance.               | Belongs to an instance of the class.               |
| Can be called without creating an object.            | Requires an object to be called.                  |
| Accesses only static data and methods.               | Accesses both static and non-static data/methods.  |
| Called using `ClassName::methodName`.                | Called using `objectName.methodName`.             |
| Example: `Math::sqrt(x)`.                            | Example: `car.startEngine()`.                     |

### Public Vs Private Constructor
---

| **Public Constructor**                                | **Private Constructor**                             |
|-------------------------------------------------------|-----------------------------------------------------|
| Can be accessed and instantiated from outside the class. | Cannot be accessed outside the class.               |
| Used to create objects freely in any part of the program. | Restricts object creation to within the class itself. |
| Example: Used when you want to allow external code to create objects. | Example: Used in Singleton design pattern to allow only one instance of a class. |
| Allows easy creation of multiple instances.           | Ensures only one or controlled instances are created. |

---

**Java Code Examples:**

### **Public Constructor Example**
```java
class Car {
    public Car() {  // Public Constructor
        System.out.println("Car created!");
    }
}

public class Main {
    public static void main(String[] args) {
        Car myCar = new Car();  // Can be instantiated from outside
    }
}
```
**Output:**  
Car created!

### **Private Constructor Example**
```java
class Singleton {
    private static Singleton instance;

    private Singleton() {  // Private Constructor
        System.out.println("Singleton instance created!");
    }

    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();  // Can only be instantiated inside the class
        }
        return instance;
    }
}

public class Main {
    public static void main(String[] args) {
        Singleton obj1 = Singleton.getInstance();  // Access via method
        Singleton obj2 = Singleton.getInstance();  // Always returns the same instance
    }
}
```
**Output:**  
Singleton instance created!


### **OOP Principles Notes with Java Code and Real-Life Examples**

---


#### **1. Abstraction**

- **Definition**: Hiding implementation details and showing only essential features.
- **Example**: _Using an ATM to withdraw cash without knowing its internal workings._

**Java Code Example:**

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

_Output:_  
Car moves on roads.  
Vehicle needs fuel.

---



#### **2. Encapsulation**

- **Definition**: Wrapping data (variables) and code (methods) together, restricting direct access to them using access modifiers.
- **Example**: _Capsule encloses medicine to protect its contents._

**Java Code Example:**

```java
class BankAccount {
    private double balance;  // Private variable

    // Getter method
    public double getBalance() {
        return balance;
    }

    // Setter method
    public void setBalance(double balance) {
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

_Output:_  
Balance: 1000

---

#### **3. Inheritance**

- **Definition**: Mechanism to acquire properties and methods from a parent class.
- **Example**: _Child inherits traits from parents in real life._

**Java Code Example:**

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

_Output:_  
This animal eats food.  
Dog barks.

---

#### **4. Polymorphism**

- **Definition**: Ability to take many forms, allowing methods to behave differently based on objects.
- **Types**: Compile-time (method overloading) & Run-time (method overriding).
- **Example**: _A person acts as a student, friend, or employee in different situations._

**Java Code Example (Overriding):**

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

_Output:_  
Drawing a circle.

---


### **Summary Table**

| **Principle** | **Definition**                               | **Real-Life Example**              |
| ------------- | -------------------------------------------- | ---------------------------------- |
| Inheritance   | Reuse properties of a parent class.          | Child inherits parent's traits.    |
| Polymorphism  | Same method behaves differently in contexts. | Person: Student, Friend, Employee. |
| Encapsulation | Restrict access, exposing through methods.   | Medicine in a capsule.             |
| Abstraction   | Show relevant features, hide internal logic. | Using an ATM.                      |


---

### **Polymorphism Types**

---

#### **1. Compile-Time Polymorphism (Method Overloading)**

- **Definition**: Same method name with different parameter lists in the same class.  
- **Achieved Through**: Method Overloading.  
- **Resolved At**: Compile-time.

**Key Points:**
- Method signature changes (number or type of parameters).
- Enhances readability and reusability.

**Real-Life Example**:  
A calculator can add integers, floats, or doubles based on inputs.

**Java Code Example:**
```java
class Calculator {  
    // Overloaded methods  
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
**Output:**  
8  
9.0  
6  

---

#### **2. Run-Time Polymorphism (Method Overriding)**

- **Definition**: Subclass provides a specific implementation of a method already defined in the parent class.  
- **Achieved Through**: Method Overriding.  
- **Resolved At**: Run-time.

**Key Points:**
- Uses inheritance and the `@Override` annotation.
- Enables dynamic method invocation based on the object type.

**Real-Life Example**:  
A vehicle can move differently based on its type (e.g., car, bike, or train).

**Java Code Example:**
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
**Output:**  
Car moves on roads.  
Boat sails on water.  

---

### **Comparison: Method Overloading vs. Method Overriding**

| **Feature**              | **Method Overloading**                     | **Method Overriding**                   |
|---------------------------|--------------------------------------------|-----------------------------------------|
| **Binding**               | Compile-time                              | Run-time                                |
| **Inheritance**           | Not required                              | Requires inheritance                    |
| **Method Signature**      | Same name, different parameters            | Same name and parameters                |
| **Usage**                 | Improves readability                      | Provides specific subclass behavior     |
| **Example**               | `add(int, int)` vs. `add(double, double)` | `move()` in `Vehicle` vs. `Car`         |  


### **Abstract Class vs Interface in Java**

---

#### **1. Abstract Class**
- **Definition**: A class that can have both abstract (no implementation) and concrete (with implementation) methods.  
- **Purpose**: To provide a base class with shared functionality while enforcing some method implementation in child classes.  
- **Key Features**:  
  - Can have abstract and non-abstract methods.  
  - Can have constructors, fields, and static methods.  
  - Supports single inheritance.

**Real-Life Example**:  
A *Vehicle* is an abstract concept; cars and bikes inherit common behavior but implement specific functionality.

**Java Code Example:**
```java
abstract class Vehicle {  
    abstract void move();  // Abstract method (no body)  

    void fuel() {  // Concrete method (implemented)  
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
**Output:**  
Car moves on roads.  
Vehicle needs fuel.  

---

#### **2. Interface**
- **Definition**: A blueprint for a class that contains only abstract methods (prior to Java 8). From Java 8, interfaces can have default methods (with implementation) and static methods.  
- **Purpose**: To achieve full abstraction and support multiple inheritance.  
- **Key Features**:  
  - All methods are implicitly public and abstract (unless specified otherwise).  
  - Cannot have constructors or instance variables (only constants).  
  - A class can implement multiple interfaces.  

**Real-Life Example**:  
A *RemoteControl* interface defines standard methods (e.g., turnOn/turnOff) for any device, such as TVs or ACs.

**Java Code Example:**
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
**Output:**  
TV is now ON.  
Resetting to factory settings.  
TV is now OFF.  

---

### **Comparison: Abstract Class vs Interface**

| **Feature**                  | **Abstract Class**                                   | **Interface**                                 |
|-------------------------------|----------------------------------------------------|----------------------------------------------|
| **Methods**                  | Abstract and concrete methods.                     | Abstract methods (default methods since Java 8). |
| **Fields**                   | Can have instance variables.                       | Only constants (public, static, final).      |
| **Inheritance**              | Single inheritance.                                | Multiple inheritance supported.             |
| **Access Modifiers**         | Can have private, protected, and public methods.   | All methods are `public` by default.        |
| **Constructors**             | Allowed.                                           | Not allowed.                                |
| **Usage**                    | Use when classes share common functionality.       | Use to define a contract for implementation. |

---

**Key Takeaway**:  
- Use an **abstract class** when you want to share code among related classes.  
- Use an **interface** to define a contract that unrelated classes can implement.  

### Types of Constructors

| **Type of Constructor**                               | **Description**                                        | **Example**                                      |
|-------------------------------------------------------|--------------------------------------------------------|--------------------------------------------------|
| **Default Constructor**                               | A constructor with no parameters. Automatically provided by Java if no other constructors are defined. | Used when no specific initialization is required. |
| **Parameterized Constructor**                         | A constructor that accepts parameters to initialize object attributes at the time of object creation. | Used when you need to initialize object with specific values. |
| **Copy Constructor**                                  | A constructor that creates a new object by copying values from another object of the same class. | Used to create a copy of an existing object. |
| **Private Constructor**                               | A constructor with a private access modifier, preventing object creation outside the class. | Used in Singleton design pattern. |

---

### **Default Constructor Example:**
```java
class Car {
    String model;
    int year;

    // Default constructor
    public Car() {
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
        car.display();         // Output: Model: Unknown, Year: 0
    }
}
```

---

### **Parameterized Constructor Example:**
```java
class Car {
    String model;
    int year;

    // Parameterized constructor
    public Car(String model, int year) {
        this.model = model;
        this.year = year;
    }

    void display() {
        System.out.println("Model: " + model + ", Year: " + year);
    }
}

public class Main {
    public static void main(String[] args) {
        Car car = new Car("Tesla", 2023);  // Parameterized constructor called
        car.display();                     // Output: Model: Tesla, Year: 2023
    }
}
```

---

### **Copy Constructor Example:**
```java
class Car {
    String model;
    int year;

    // Parameterized constructor
    public Car(String model, int year) {
        this.model = model;
        this.year = year;
    }

    // Copy constructor
    public Car(Car car) {
        this.model = car.model;
        this.year = car.year;
    }

    void display() {
        System.out.println("Model: " + model + ", Year: " + year);
    }
}

public class Main {
    public static void main(String[] args) {
        Car originalCar = new Car("Tesla", 2023);  // Original object
        Car copiedCar = new Car(originalCar);      // Copy constructor called
        copiedCar.display();                       // Output: Model: Tesla, Year: 2023
    }
}
```

---

### **Private Constructor Example:**
```java
class Singleton {
    private static Singleton instance;

    // Private constructor
    private Singleton() {}

    // Static method to get the single instance
    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}

public class Main {
    public static void main(String[] args) {
        Singleton obj1 = Singleton.getInstance();  // Accessing Singleton via getInstance method
        Singleton obj2 = Singleton.getInstance();
        System.out.println(obj1 == obj2);  // Output: true (same instance)
    }
}


```
### Shallow Vs Deep Copy
---
| **Shallow Copy**                                       | **Deep Copy**                                      |
|--------------------------------------------------------|----------------------------------------------------|
| Creates a new object, but elements within the object are still references to the original objects. | Creates a new object and recursively copies all objects, ensuring the original object and the copy do not share any references. |
| Changes in the nested objects of the copied object reflect in the original object. | Changes in nested objects do not affect the original object. |
| Faster because it only copies references to the objects. | Slower because it copies all elements recursively. |
| Example: Used when only the outer structure needs to be copied. | Example: Used when both the outer and inner structures need to be independent. |

---
