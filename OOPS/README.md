# OOPS

- Object Oriented Programming System/Structure.
- OOPS is a Programming paradigm or methodology.
- Paradigm can also be termed as method to solve some problem or to do some tasks. Programming paradigm is an approach to solve problem using programming language or also we can say it is a method to solve a problem using tools and technique that are available to us following some approach.
- Programming paradigm are of different types.
  - Object Oriented paradigm.
  - Procedural paradigm.
  - Functional paradigm.
  - Logical paradigm.
  - Structred paradigm.
- 6 main pillars of OOPS are.
  - Class
  - Object and method
  - Inheritance
  - Polymorphism
  - Abstraction
  - Encapsulation

## Class

- Class is the collection of Object.
- Class is not a real world entity , it is just a template or blueprint or prototype.
- Class does not occupy memory.

**Syntax** - access-modifier class ClassName {

}

\*A class can have method, constructor, variable, blocks and nested class.

## Method

- A set of codes which perform a particular task

**Advantages of Method**

- Code reusability
- Code optimization

**Syntax**

access-modifier return-type methodName(list of parameters){

}

## Object

- Object is an instance of class.
- Object is a real world entity hence it occupies memory.
- Object consist of :-
  - Identity - name
  - State/Attribute - color, breed, age (represents variable)
  - Behaviour - eat, run, bark (represents method)

How to create an object?

- new keyword
- newInstance() method
- clone() method
- deserialization
- factory method

How to create object with the help of new keyword?

Declaration - Animal buzo;
![alt text](image-1.png)

Instantiation - buzo = new (new keyword is used to allocate memory)
![alt text](image-2.png)

Initialization - Animal buzo = new Animal(); (We initialize by creating constructor same as class name)
![alt text](image-3.png)

Animal buzo = new Animal();

To call the method or intialize the attribute of the object we use . operator

Example - buzo.run(); buzo.color = "black";

```java
public class Animal {
    public void eat(){
      System.out.println("I am eating");
    }
    public static void main(String[] args) { //there will be only one main method in the program
        System.out.println("1");
        Animal dog = new Animal();
        dog.eat();
        dog.run();
        Birds sparrow = new Birds();// to execute method of other class we have to make object of that class
        sparrow.fly();
    }
    public void run(){
      System.out.println("I am running");
    }
}
class Birds{
          void fly (){
            System.out.println("I am flying");
          }
}
```

Three ways by which we can initialize object -

1. Using reference variable

```java
class Animal{
     String color;
     int age;
     public static void main(String[] args){
      Animal dog = new Animal();
      dog.color = "white";
      dog.age = 5;
      System.out.println("Dog is " + dog.color + "and his age is " + dog.age);
     }
}
```

2. Using Method

```java
class Animal{
     String color;
     int age;
     void intObj(String c,  int a){
          color = c;
          age = a;
     }
     void display(){
        System.out.println("Dog is " + color + " and his age is " + age);
     }
     public static void main(String args[]){
      Animal dog = new Animal();
      dog.intObj("white", 5);
      dog.display();
     }
}
```

3. Using Constructor

## Constructor

- Constructor is block similar to method having same name as that of class name.
- Constructor does not have any return type not even void.
- The only modifier applicable for constructor are public, protected, default and private.
- It executes automatically when we create object.

```java
class Employee{
  String name;
  int emp_id;
  Employee(String name, int emp_id){//used constructor to initialize the instance variable of the object.
    this.name = name;
    this.emp_id = emp_id;
  }
  public static void main(String args[]){
    Employee e1 = new Employee("Ashish", 12);
    Employee e2 = new Employee("Rahul", 14);
    System.out.println(e1.name);
  }
}
```

### Types of Constructor

1. Default Constructor

- It is created by compiler.

```java
class Test{
  int a;
  Test(){
    super();
  }
  public static void main(String args[]){
    Test t = new Test();
    System.out.println(t.a);//a = 0 (default value)
  }
}
```

2. No-arg Constructor(User defined)

```java
class Test{
  Test(){//It is created by the user.
    System.out.println("No argument constructor");
  }
  public static void main(String args[]){
    Test t = new Test();
  }
}
```

3. Parametrized Constructor

```java
class Test{
  Test(String name){
    System.out.println("Parametrized Constructor");
  }
  public static void main(String args[]){
    Test t = new Test("Ashish");
  }
}
```

## Inheritance

- Inheritance is a mechanism that allows a new class to inherits all the properties and behaviors of the existing class, and can also add its own properties and behaviors.
- We achive inheritance by using **extends** keyword.

```java
class Animal{// parent class or super class
  void eat(){
    System.out.println("I am eating");
  }
}
class Dog extends Animaml{// child class or sub class
  public static void main(String args[]){
    Dog d = new Dog();
    d.eat();
  }
}
```

Dog **Is A** Animal (**is a** relationship)

**Advantages of Inheritance**

- Code reusability.
- It promotes runtime polymorphism by allowing method overriding.

**Disadvantages of Inheritance**

- Tight Coupling -: Inheritance can lead to tight coupling between classes, where changes in one class (especially in the superclass) can have unforeseen consequences on subclasses.

### Types of Inheritance

1. Single Inheritance - A class inherit from only one super class.

```java
class Animal {
    void eat() {
        System.out.println("Animal is eating");
    }
}

class Dog extends Animal {
    void bark() {
        System.out.println("Dog is barking");
    }
}

public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog();
        dog.eat(); // Inherits from Animal class
        dog.bark(); // Method defined in Dog class
    }
}
```

2. Multilevel Inheritance - In multilevel inheritance, a class inherits from another class, and that class, in turn, can act as a superclass for another class.

```java
// Example of Multilevel Inheritance
class Animal {
    void eat() {
        System.out.println("Animal is eating");
    }
}

class Dog extends Animal {
    void bark() {
        System.out.println("Dog is barking");
    }
}

class Puppy extends Dog {
    void wagTail() {
        System.out.println("Puppy is wagging its tail");
    }
}

public class Main {
    public static void main(String[] args) {
        Puppy puppy = new Puppy();
        puppy.eat(); // Inherits from Animal class
        puppy.bark(); // Inherits from Dog class
        puppy.wagTail(); // Method defined in Puppy class
    }
}
```

3. Hierarchical Inheritance: In hierarchical inheritance, multiple classes inherit from a single superclass.

```java
class Animal {
    void eat() {
        System.out.println("Animal is eating");
    }
}

class Dog extends Animal {
    void bark() {
        System.out.println("Dog is barking");
    }
}

class Cat extends Animal {
    void meow() {
        System.out.println("Cat is meowing");
    }
}

public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog();
        dog.eat(); // Inherits from Animal class
        dog.bark(); // Method defined in Dog class

        Cat cat = new Cat();
        cat.eat(); // Inherits from Animal class
        cat.meow(); // Method defined in Cat class
    }
}

```

**Important points of Inheritance**

- There is no multiple inheritance and hybrid inheritance in java.
- If any class doest not inherit any other class it will indirectly inherit Object class.
- Object class is the parent class of all the class.
- Below does not take part in inheritance.
  - Constructors - A subclass inherit all the members(fields, method and nested class) from its super class. Constructors are not members so they are not inherited by subclasses, but the constructor of the super class can be invoked from the subclass.
  - Private member - A sublcass does not inherit private member of its parent class.

### Relationship between classess.

There are two types of relation

![alt text](test.drawio.png)

**Advantages**

1. Code reusability
2. Cost cutting
3. Reduce redundancy

### Inheritance

```java
class Vehicle{

}
class Car extends Vehicle{

}
```

Car Is A Vehicle (Is A relationship)

- In this realtion both classes are tightly coupled that means if we make changes in the first class second class also get affected.

### Association

```java
class Student{
  String name;
  int roll_no;
}
```

Student **Has A** name(Has a relation)\
Student **Has A** roll_no(Has a relation)

```java
class Engine{

}
class Car{
  Engine e = new Engine();
}

```

Car **Has a** Engine

- Classes are not tightly coupled that means we can use required properties of engine class with the help of reference object.

**Aggregation:**

Aggregation is a "has-a" relationship where one class, often called the container or parent class, contains references to another class, often called the contained or child class. The contained class is not dependent on the container class, meaning it can exist independently. Aggregation is a weaker form of association compared to composition.

**Composition**

Composition is a stronger form of association where one class, the composite, contains an instance of another class, the component, and the component cannot exist without the composite. In other words, the lifetime of the component is managed by the composite.

![alt text](relationex.drawio.png)

## Polymorphism

- Polymorphism in Java is a concept by which we can perform a single action in different ways.
- The word "poly" means many and "morphs" means forms.

### Types of polymorphism

**1. Compile Time Polymorphism**

- It is also known as static polymorphism.
- We can achive compile time polymorphism by method overloading.
- It is handle by compiler.

**2. Run Time Polymorphism**

- It is also known as dynamic polymorphism.
- We can achive run time polymorphism by method overriding.
- It is handle by JVM.

### Method Overloading

- Method name should be same.
- Method should belong to same class.
- Argument should be different.
  - Number of argument should be different.
  - Sequence of argument should be different.
  - Type of argument should be different.

```java
public class Calculator {

    public int add(int a, int b) {
        return a + b;
    }

    // Number of argument is different
    public int add(int a, int b, int c) {
        return a + b + c;
    }

    // Type of argument is different
    public String add(String a, String b) {
        return a + b;
    }



    public static void main(String[] args) {
        Calculator calculator = new Calculator();

        // Adding two integers
        int sum1 = calculator.add(10, 20);
        System.out.println("Sum of two integers: " + sum1);

        // Adding three integers
        int sum2 = calculator.add(10, 20, 30);
        System.out.println("Sum of three integers: " + sum2);

        // Concatenating two strings
        String result = calculator.add("Hello", " World!");
        System.out.println("Concatenated string: " + result);
    }

}
```

Special cases of method overloading

**1. Can we achive Method overloading by changing the return type of method only?**

Ans.

```java
class Test{
  void show(int a){
    System.out.println("1");
  }
  String show(int a){
    System.out.println("2");
  }
  public static void main(String args[]){
    Test t = new Test();
    t.show(10);
  }
}

```

In java Method overloading is not possible by changing the return type of the method only because of ambiguity.

**2. Can we overload java main() method**

Ans.

```java

class Test{
  public static void main(String args[]){
    System.out.println("1");
    Test t = new Test();
    t.main(10);
  }
  public static void main(int a){
    System.out.println("2");
  }
}

//Output- 1 2
```

Yes we can have any number of main method in a class by method overloading. This is because JVM always calls main() method which recieves string array as argument only.

#### Method Overloading - Case 1

```java
class Test{
  void show(int a){
    System.out.println("int method");
  }
  void show(String a){
    System.out.println("string method");
  }
  public static void main(String args[]){
    Test t = new Test();
    t.show('a');
  }
}

//Output - int method
```

**Automatic promotion**

One type is promoted to other implicitly if no matching data type is found.

![alt text](image-4.png)

#### Method Overloading - Case 2

```java
class Test{
  void show(Object a){
    System.out.println("Object method");
  }
  void show(String a){
    System.out.println("String method");
  }
  public static void main(String args[]){
    Test t = new Test();
    t.show("abc");
  }
}

//Output - String method
```

While resolving Overloaded Methods, Compiler will always give precedent for the child type argument than compared with parent type argument.

#### Method Overloading - Case 3

```java
class Test{
  void show(StringBuffer a){
    System.out.println("String Buffer method");
  }
  void show(String a){
    System.out.println("String method");
  }
  public static void main(String args[]){
    Test t = new Test();
    t.show("abc");//String method
    t.show(new StringBuffer("xyz"));//String Buffer method
    t.show(null);//reference to show is ambiguos
  }
}
```

#### Method Overloading - Case 4

```java
class Test{
  void show(int a, float b){
    System.out.println("int float method");
  }
  void show(float a, int b){
    System.out.println("float int method");
  }
  public static void main(String args[]){
    Test t = new Test();
    t.show(10,20.5f);//int float
    t.show(10.5f,20);//float int
    t.show(10,20)//reference to show is ambiguos - No automatic promotion
  }
}
```

#### Method Overloading - Case 4

```java
class Test{
  void show(int a){
    System.out.println("int method");
  }
  void show(int... a){//varargs allow the method to accept zero or multliple argument
    System.out.println("varargs method");
  }
  public static void main(String args[]){
    Test t = new Test();
    t.show(10);// int method
    t.show(10,20,30);// varargs method
    t.show();// varargs method

  }
}
```

Varargs get less priority i.e if no other method matched, then only vararg method will get the chance.
