# OOPS in CPP

## What is Class ?
A class is a blueprint or template that defines the properties (attributes) and behavior (functions) of objects. It acts like a cookie cutter that you can use to create multiple objects of the same kind.

## What is Object ?
An object is an instance of a class.  Imagine a class as a blueprint or template that defines the characteristics and functionalities of a particular kind of thing. An object is like a specific example created from that blueprint.

## What is Contructor ?
Constructors are special member functions of a class that are automatically invoked whenever you create an object of that class. They are essential for initializing the object's data members (member variables) with appropriate values right at the time of creation.

### Properties of Contructor:
1. Name same as Class Name
2. No Return Type
3. Automatic Invocation

### Types of Contructor:
1. Default Constructor
    - A class can have a default constructor that takes no arguments. If you don't define a constructor explicitly, the compiler provides a default one that typically performs minimal initialization

    ```cpp

    class Car {
        public:
        std::string model;
        int year;

        // Default constructor (no arguments)
        Car() {
            model = "Unknown";
            year = 0;
            std::cout << "Car object created using default constructor." << std::endl;
        }
    };

    ```

2. Parameterized Constructor
    - You can define constructors that take arguments. These arguments allow you to specify initial values for the object's data members during creation. This is useful when you want to create objects with customized states.

    ```cpp

    class Car {
        public:
        std::string model;
        int year;

        // Parameterized constructor (takes model and year as arguments)
        Car(const std::string& carModel, int carYear) {
            model = carModel;
            year = carYear;
            std::cout << "Car object created using parameterized constructor." << std::endl;
        }
    };

    ```

3. Copy Constructor
    - A copy constructor is used to create a new object as a copy of an existing object of the same class. It takes an existing object as an argument and initializes the new object with the values from the existing one.


    ```cpp

    class Car {
    public:
        std::string model;
        int year;

        Car() : model("Unknown"), year(0) {}
        Car(const std::string& carModel, int carYear) : model(carModel), year(carYear) {}

        // Copy Contructor
        Car(const Car& other) : model(other.model), year(other.year) {}
    };


    ```



## What is OOP ?
OOP is a programming paradigm that organizes code around objects.  These objects are like blueprints for real-world things or concepts.

## Pillars of OOPS
1. Encapsulation
2. Inheritance
3. Polymorphism
4. Abstraction

### Encapsulation
- Encapsulation is the bundling of data (attributes) and methods (functions) that operate on that data together within a single unit called an object.
- This protects the data from unauthorized access and promotes modularity by keeping the internal workings of an object hidden.
- In C++, access specifiers (public, private, protected) are used to control how data and methods can be accessed from outside the class.


```cpp
#include <iostream>
#include <string>

class BankAccount {
private:

  std::string name;
  int accountNumber;
  double balance;

public:

  BankAccount(const std::string& accountName, int acctNum) : name(accountName), accountNumber(acctNum), balance(0.0) {}

  void deposit(double amount) {
    if (amount > 0) {
      balance += amount;
      std::cout << "Deposit successful. New balance: $" << balance << std::endl;
    } else {
      std::cout << "Invalid deposit amount." << std::endl;
    }
  }

  void withdraw(double amount) {
    if (amount > 0 && amount <= balance) {
      balance -= amount;
      std::cout << "Withdrawal successful. New balance: $" << balance << std::endl;
    } else {
      std::cout << "Invalid withdrawal amount." << std::endl;
    }
  }

  double getBalance() const {
    return balance;
  }
};
```

#### Acces Modifirs
1. Private:
 - Members declared as private are only accessible within the class itself. They cannot be accessed directly from outside the class. This is the most restrictive access modifier and promotes strong encapsulation.

2. Public:
 - Members declared as public are accessible from anywhere in the program, including outside the class. This allows other parts of your code to interact with the class and its members directly. Use public members with caution, as unrestricted access can weaken encapsulation.

3. Protected:
 - Members declared as protected are accessible from within the class itself and from derived classes (classes that inherit from the current class). This provides a middle ground between private and public access. Protected members are often used to define an interface that derived classes can inherit and use to implement specific functionality.


```sh
Private     -- 	    Class itself only
Public	    --      Anywhere in the program
Protected   -- 	    Class itself and derived classes

```

### Inheritance
Inheritance in C++ is a powerful mechanism that allows you to create new classes (derived classes) that inherit properties and behaviors from existing classes (base classes). It promotes code reusability and creates hierarchical relationships between classes.

#### Types of Inheritance:
1. Single Inheritance
```cpp
class Animal {
public:
  void eat() {
    std::cout << "Eating..." << std::endl;
  }
};

class Dog : public Animal {
public:
  void bark() {
    std::cout << "Barking..." << std::endl;
  }
};

```

2. Multilevel Inheritance:
```cpp
class Vehicle {
public:
  void move() {
    std::cout << "Moving..." << std::endl;
  }
};

class Car : public Vehicle {
public:
  void accelerate() {
    std::cout << "Car accelerating..." << std::endl;
  }
};

class ElectricCar : public Car {
public:
  void charge() {
    std::cout << "Electric car charging..." << std::endl;
  }
};

```

3. Hierarchical Inheritance:
```cpp
class Animal {
public:
  void eat() {
    std::cout << "Eating..." << std::endl;
  }
};

class Dog : public Animal {
public:
  void bark() {
    std::cout << "Barking..." << std::endl;
  }
};

class Cat : public Animal {
public:
  void meow() {
    std::cout << "Meowing..." << std::endl;
  }
};

```

4. Multiple Inheritance:
    - A derived class inherits from multiple base classes. This can become complex to manage and can lead to ambiguity (the diamond problem). It's generally advised to avoid multiple inheritance unless absolutely necessary due to potential complexities.

```cpp
class Shape {
public:
  virtual void draw() {
    std::cout << "Drawing a shape..." << std::endl;
  }
};

class Colored {
public:
  std::string color;

  Colored(const std::string& col) : color(col) {}
};

class Rectangle : public Shape, public Colored {
public:
  int width, height;

  Rectangle(int w, int h, const std::string& col) : Shape(), Colored(col), width(w), height(h) {}

  void draw() override {
    std::cout << "Drawing a " << color << " rectangle with width: " << width << " and height: " << height << std::endl;
  }
};

int main() {
  Rectangle rect(5, 3, "red");
  rect.draw();
  return 0;
}

```

#### Diamond Problem: 
```cpp
#include <iostream>

class Animal {
public:
  void speak() {
    std::cout << "Animal sound..." << std::endl;
  }
};

class Mammal : public Animal {
public:
  void speak() {
    std::cout << "Mammal speak..." << std::endl;
  }
};

class Bird : public Animal {
public:
  void speak() {
    std::cout << "Bird Speak..." << std::endl;
  }
};

class Bat : public Mammal, public Bird { 

};

int main() {
  Bat bat;
  bat.speak(); // bat.Bird::speak();
  return 0;
}
```

#### Access Modifiers in Inheritance: 
- Public Inheritance:
    - Members that are public in the base class remain public in the derived class.
    - Members that are protected in the base class remain protected in the derived class.
    - Members that are private in the base class are not accessible in the derived class.
- Protected Inheritance:
    - Members that are public in the base class become protected in the derived class.
    - Members that are protected in the base class remain protected in the derived class.
    - Members that are private in the base class are not accessible in the derived class.
- Private Inheritance:
    - Members that are public in the base class become private in the derived class.
    - Members that are protected in the base class become private in the derived class.
    - Members that are private in the base class are not accessible in the derived class.

#### Virtual Inheritance:

Virtual inheritance is a technique in C++ used to solve the "diamond problem" of multiple inheritance, where an ambiguity arises due to a class being derived from two classes that share a common base class.

**How It Works**

With virtual inheritance, the C++ compiler ensures that there is only one instance of the virtual base class (A), regardless of how many times it is inherited. This is achieved by the compiler keeping a single shared instance of A for all the derived classes that use virtual inheritance.

```cpp
class A {
public:
    void show() {
        cout << "Class A" << endl;
    }
};

class B :  public A { // make it virtual to solve error
};

class C : public A { // make it virtual to solve error
};

class D : public B, public C {
};

int main() {
    D obj;
    obj.show(); // This line will cause ambiguity
    return 0;
}
```


### Polymorphism
Polymorphism in C++ is a fundamental concept in object-oriented programming that allows objects of different classes to respond differently to the same message (function call or operator). It promotes flexibility and code reusability.

**There are two main types of polymorphism in C++:**

1. Compile-time Polymorphism (Static Binding):

This type of polymorphism is resolved by the compiler at compile time. It involves two key mechanisms:

- **Methold Overloading:** This allows you to define multiple functions with the same name but different parameter lists. The compiler determines which function to call based on the number, types, and order of the arguments provided during the call.

```cpp
class Calculator {
public:
  int add(int a, int b) {
    return a + b;
  }

  double add(double a, double b) {
    return a + b;
  }
};

int main() {
  Calculator calc;
  int result1 = calc.add(3, 4);  
  double result2 = calc.add(2.5, 1.7); 
  std::cout << result1 << ", " << result2 << std::endl;
  return 0;
}

```

- **Operator Overloading:** You can redefine the behavior of operators (like +, -, *, etc.) for custom classes. The compiler selects the appropriate overloaded operator based on the operand types involved in the operation.

```cpp
#include <iostream>

class Complex {
private:
  double real, imag;

public:
  Complex(double r = 0, double i = 0) : real(r), imag(i) {}

  Complex operator+(const Complex& other) {
    return Complex(real + other.real, imag + other.imag);
  }
};

int main() {
  Complex c1(2, 3);
  Complex c2(4, 1);
  Complex c3 = c1 + c2;
  std::cout << "c1 = " << c1 << std::endl;
  std::cout << "c2 = " << c2 << std::endl;
  std::cout << "c3 = c1 + c2 = " << c3 << std::endl;

  return 0;
}

```

2. Runtime Polymorphism (Dynamic Binding):

This type of polymorphism is resolved at runtime. It relies on virtual functions and Methold Overiding:

 - **Virtual Functions:** A function declared as virtual in a base class allows derived classes to override its behavior. When a virtual function is called through a base class pointer or reference, the actual object's type (derived class) determines which function implementation is executed at runtime.

 ```cpp
class Animal {
    public:
        virtual void makeSound() {
            std::cout << "Generic animal sound..." << std::endl;
        }
    };

    class Dog : public Animal {
    public:
        void makeSound() override { 
            std::cout << "Woof!" << std::endl;
        }
};

    int main() {
    Animal* animal = new Dog; 
    animal->makeSound();
    delete animal;
    return 0;
}

 ```

 #### **Properties of virtual functions**
```sh
- Overridden in derived classes

- Virtual Destructors: When a base class has virtual functions, it's recommended to declare a virtual destructor in the base class as well. This ensures proper object destruction when dealing with base class pointers or references to derived class objects.
```

 - **Methold Overiding:** Derived classes inherit virtual functions from their base class. When you call a virtual function through a base class pointer or reference that points to a derived class object, the overridden version in the derived class is invoked at runtime.

 ```cpp
class Animal {
public:
  void eat() {
    std::cout << "Generic animal eating..." << std::endl;
  }
};

class Dog : public Animal {
public:
  void eat() override {
    std::cout << "Dog chomping on food!" << std::endl;
  }
};

int main() {
  Animal* animal = new Dog; 
  animal->eat();
  delete animal;
  return 0;
}

 ```

### Abstraction:
It focuses on hiding the internal details (implementation) of an object and providing a simplified interface for users to interact with. It's like creating a mental model or a high-level view of something, focusing on the essential features

```cpp
#include <iostream>

class Shape {
public:
  // Pure virtual function with no implementation (abstract method)
  virtual double area() const = 0;

  virtual ~Shape() = default; // Virtual destructor (recommended for proper cleanup)
};

// Destructor definition outside the class (not mandatory, but recommended practice)
Shape::~Shape() {}

class Square : public Shape {
public:
  double side;

  Square(double sideLength) : side(sideLength) {}

  double area() const override {
    return side * side;
  }
};

class Circle : public Shape {
public:
  double radius;

  Circle(double circleRadius) : radius(circleRadius) {}

  double area() const override {
    return 3.14159 * radius * radius;
  }
};

int main() {
  // You cannot create objects of an abstract class (Shape)
  // Shape shape;  // This would cause an error

  Square sq(5);
  Circle cir(3);

  std::cout << "Area of square: " << sq.area() << std::endl;
  std::cout << "Area of circle: " << cir.area() << std::endl;

  return 0;
}
```

## Friend Function
```cpp

#include <iostream>

class Box {
private:
  int length;
  int width;
  int height;

public:
  Box(int l = 0, int w = 0, int h = 0) : length(l), width(w), height(h) {}

  // Regular member function to get volume
  int getVolume() const {
    return length * width * height;
  }

  // Friend function to print volume with a different format
  friend void printBoxVolume(const Box& box);
};

// Friend function definition outside the class
void printBoxVolume(const Box& box) {
  std::cout << "Volume of the box: " << box.length * box.width * box.height << std::endl;
}

int main() {
  Box box(5, 3, 2);

  // Call regular member function
  std::cout << "Volume using member function: " << box.getVolume() << std::endl;

  // Call friend function
  printBoxVolume(box);

  return 0;
}

```

# EXTRA

### Association
In object-oriented programming (OOP), association refers to a relationship between two or more classes that describes a "has-a" or "uses-a" connection. It represents how objects of different classes are linked together and potentially collaborate. Associations are a fundamental concept for modeling real-world relationships between entities.

1. Simple Association:
The most basic type. Two classes have a connection, but neither class has ownership or control over the other. They simply "know about" each other.

```cpp
class Student {
public:
  std::string name;
  Course* enrolledCourse; // Pointer to a Course object
};

class Course {
public:
  std::string title;
  // No reference to Student
};
```

2. Aggregation:
A stronger form of association where one class (the whole) "has-a" part of another class. The whole class has a lifetime responsibility for the part class. If the whole class is destroyed, the part class might also be destroyed.

```cpp
class Library {
public:
  std::vector<Book> books; // Has-a collection of Book objects
};

class Book {
public:
  std::string title;
};
```

3. Composition
The strongest type of association. The whole class "has-a" part and is responsible for the part's entire lifecycle. If the whole class is destroyed, the part class is also destroyed.

```cpp
class Car {
public:
  Engine engine; // Has-a required Engine object
};

class Engine {
public:
  void start() { ... }
};
```

