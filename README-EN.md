**Language: [PT-BR](https://github.com/Ivi-SCD/GoF-DesignPatterns) | > EN**

## :bamboo: Complete Guide To GoF Design Patterns :bamboo:
In this repository I will treat all design patterns defined in the book **[GoF - Gang of Four](https://www.amazon.in/Design-Patterns-Object-Oriented-Addison-Wesley-Professional-ebook/dp/B000SEIBB8)**, also known as "Design Patterns: Elements of Reusable Object-Oriented Software". This programming-oriented book is essential for all programmers, especially those working with the object-oriented paradigm. It was written by Erich Gamma, Richard Helm, Ralph Johnson and John Vlissides. The book was published in 1994 and since then has been one of the main resources for understanding object-oriented design patterns. The GoF authors present a set of **23 design patterns** that are divided into three categories: **Creational Patterns, Structural Patterns and Behavioral Patterns.**

Design patterns are solutions to common problems that arise during software development. They are proven techniques that can be used to solve these problems efficiently and effectively. Each design pattern is a complete description of a specific problem and a general solution that can be adapted to meet different design requirements, in any language.

Summary of all types of design patterns:
* **Creational Patterns**
   * [Singleton](#singleton)
   * [Factory Method](#factory)
   * [Abstract Factory](#afactory)
   * [Builder](#builder)
   * [Prototype](#prototype)
* **Structural Patterns**
   * adapter
   * Bridge
   * Composite
   * decorator
   * facade
   * Flyweight
* **Behavioral patterns**
   * Chain Of Responsibility
   *Command
   * Iterator
   * mediator
   * memento
   * Observer
   * State
   * Strategy
   * Template Method
   * Visitor
  
Each of these patterns is explained in detail in the GoF book, along with code examples and guidelines for its implementation, this repository will cover all the main points of the book, but to understand and be able to enjoy 100% of what is offered, I strongly recommend reading the book. As you study and understand these patterns, you can create software solutions that are more flexible, reusable, and easier to maintain. So let's start! Hands-On! Don't forget to mark this repository with a :star: so that you can always review and study the design patterns whenever you need to.

## Creational Patterns
### <a name="singleton"></a>Singleton

Singleton is a creational pattern, it guarantees that a class has **only one instance** and provides a global point of access to it. This is useful when we need, for example, an object that coordinates actions throughout the system, such as a configuration manager or a cache. The Singleton pattern ensures that there is only one instance of these objects, avoiding the need for multiple instances and therefore reducing system resource consumption.

The basic implementation of the Singleton pattern consists of **a class that has a private constructor and a static method that returns the single instance of the class**. The static method **checks to see if an instance has already been created and, if not, creates a new instance.** The created instance is then returned to any caller requesting the instance.

I know that with words it is a little difficult to understand and assimilate the subject so here is an example of implementing the Singleton pattern in Java:

```java
public class Singleton {
     private static Singleton instance;

     private Singleton() {
         // Private constructor to avoid external instantiation
     }

     public static Singleton getInstance() {
         if (instance == null) {
             instance = new Singleton();
         }
         return instance;
     }

     // Other methods of the Singleton class
}

```

In the example above, the `Singleton` class has a private constructor and a static `getInstance()` method that returns the single instance of the class. The instance is only created when the `getInstance()` method is called for the first time, and thereafter the same instance is returned in all subsequent calls.

Here's a code example that uses the `Singleton` class:

```java
public class MyApp {
     public static void main(String[] args) {
         Singleton s1 = Singleton.getInstance();
         Singleton s2 = Singleton.getInstance();
         System.out.println(s1 == s2); // true, both variables refer to the same instance
     }
}

```

In the example above, two variables are created from the `Singleton` class using the `getInstance()` method. Since the `Singleton` class guarantees that **only one instance exists**, both variables refer to the same instance. The code output will be `true`, confirming that both variables refer to the same instance.
 
In summary, the Singleton pattern is useful when we need to ensure that **only one instance of a class exists in the system and when we need to provide a global point of access to that instance**. This can be used in many cases like cache or configuration managers. The implementation of the Singleton pattern consists of a class with a private constructor and a static method that returns the single instance of the class, creating it only when needed.

##

### <a name="factory"></a>Factory Method

The Factory Method is a creational design pattern that **provides an interface for creating objects in a class**, but lets subclasses decide which class to instantiate. The problem this pattern solves is allowing a class to delegate the creation of objects to its subclasses, avoiding the need for the main class to know in advance which concrete classes will be created.

An example of a Factory Method application can be found in a sales order processing application in a virtual store. Suppose the store has multiple order types, such as Domestic Order, International Order, Express Order, and so on. Each type of order requires specific treatment and may have different attributes and behaviors.

To solve this problem, we can use the Factory Method so that the Order class can be created by its subclasses according to the specific needs of each type of order. In this way, the main class does not need to know in advance which concrete classes will be created, but delegates this responsibility to the subclasses.

```java
public abstract class Order {
     protected double value;
     protected String address;

     public Order(double value, String address) {
         this.value = value;
         this.endereco = address;
     }

     public abstract double calculateShipping();

     // Other methods of the Order class
}

public class NationalOrder extends Order{
     public NationalOrder(double value, String address) {
         super(value, address);
     }

     public double calculateShipping() {
         return value * 0.1;
     }

     // Other methods of the National Order class
}

public class InternationalOrder extends Order{
     public InternationalOrder(double value, String address) {
         super(value, address);
     }

     public double calculateShipping() {
         return value * 0.2;
     }

     // Other methods of the International Order class
}

public interface FactoryOrders {
     public Order createOrder(double value, String address);
}

public class FabricOrderNational implements FactoryOrders {
     public Order createOrder(double value, String address) {
         return new NationalOrder(value, address);
     }
}

public class FabricOrderInternational implements FactoryOrders {
     public Order createOrder(double value, String address) {
         return new InternationalOrder(value, address);
     }
}

public class VirtualStore {
     private FactoryOrders manufactures;

     public VirtualStore(FabricaOrders factory) {
         this.fabrica = manufactures;
     }

     public Order createOrder(double value, String address) {
         return factory.createOrder(value, address);
     }
}

```

The above example may have scared you a bit but it is relatively simple to understand, basically the Order class is an abstract class that defines the interface for creating orders and it also has an abstract method `calculateShipping()`. The `NationalOrder` and `InternationalOrder` subclasses implement this interface and implement their own freight calculation behavior.

The `FactoryOrders`, `FabricOrderNational` and `FabricOrderInternational` classes implement the `Factory Method`, providing an interface for creating Order objects. The `VirtualStore` class is responsible for creating an Order object according to the specific type of order.

The following is a code example that uses the `Factory Method`:

```java
public class Main {
     public static void main(String[] args) {
         // Implementing the factories
         FactoryOrders fabricNational = new FabricOrderNational();
         FactoryOrders fabricInternational = new FabricaOrderInternational();
        
         // Creating a VirtualStore object and assigning it to fabricaNacional in its constructor
         VirtualStore store = new VirtualStore(fabricNational);
        
         //Making the national order
         Order orderNational = store.createOrder(1000, "123 A Street");
        
        
         //Following the same logic, now with the factoryInternational and the orderInternational
         store = new VirtualStore(fabricInternational);
         Order orderInternational = store.createOrder(2000, "Av. B, 456");

         System.out.println("National order shipping value: " + orderNational.calculateShipping());
         System.out.println("Freight value of the international order: " + orderInternational.calculateShipping());

     }
}
```

In the example above, the `Main` class creates two factories, one for `NationalOrder` and another for `InternatioalOrder`. Next, `VirtualStore` is instantiated with the national order factory and a national order is created.

The `calculateShipping()` method of each Order object is called, showing the calculated freight value according to the implementation of each concrete class.

##

### <a name="afactory"></a> Abstract Factory
Abstract Factory is a design pattern very similar to Factory Method. It **provides an interface for creating families of related or dependent objects**, without specifying their concrete classes. In other words, it allows you to **create objects that share the same theme**, like objects of different types, but that have some relationship with each other. Complicated to understand but you will understand better with the examples.

A good example of an Abstract Factory application is a vehicle management system, in which there are two types of vehicles: cars and motorcycles. Each type of vehicle has its own characteristics such as engine, wheels, model, etc. And for each type of vehicle, there can be different makes and models. Abstract Factory can be used to create objects that are related to each other, such as a car of a certain make and model, or a motorcycle of a certain make and model.

The following is a code example that uses Abstract Factory:

```java
public interface VehicleFactory {
    Car createCar();
    Moto createMoto();
}

public class FiatFactory implements VehicleFactory {
    public Car createCar() {
       return new Palio();
    }
    public Moto createMoto() {
       return new Ducati();
    }
}

public class ChevroletFactory implements VehicleFactory {
    public Car createCar() {
       return new Onix();
    }
    public Moto createMoto() {
       return new HarleyDavidson();
    }
}

public class VehicleStore {
    private VehicleFactory manufacturesVehicle;
   
    public VehicleStore(VehicleFactory manufacturesVehicle) {
       this.manufacturesVehicle = manufactureVehicle;
    }
   
    public Car createCar() {
       return manufacturesVehicle.createCar();
    }
   
    public Moto createMoto() {
       return manufacturesVehicle.createMoto();
    }
}

public class Main {
    public static void main(String[] args) {
       VehicleFactory fiatFactory = new FiatFactory();
       VehicleFactory chevroletFactory = new ChevroletFactory();
      
       VehicleStore fiatStore = new VehicleStore(fiatFactory);
       VehicleStore chevroletStore = new VehicleStore(chevroletFactory);
      
       Car palio = fiatStore.criarCarro();
       Moto ducati = fiatStore.createMoto();
      
       Car onix = chevroletStore.createCar();
       Moto harleyDavidson = chevroletStrore.createMoto();
    }
}

```

In this example, there is a `VehicleFactory` interface that defines the methods for creating cars and motorcycles. The `FiatFactory` and `ChevroletFactory` classes implement this interface and provide concrete implementations to create Fiat and Chevrolet cars and motorcycles, respectively. The `VehicleStore` class uses the vehicle factory to create cars and motorcycles of different makes and models. Finally, the `Main` class shows how to create Car and Motorbike objects using different vehicle factories.

This pattern solves the problem of creating objects related to each other without specifying their concrete classes, allowing objects of different types to be created, but which have some relationship to each other.

Ok, understood, but what is the difference between Abstract Factory and Factory?
Basically, the fundamental difference between the Abstract Factory pattern and the Factory Method pattern is that the Abstract Factory is used to create **families of related or dependent objects**, while the Factory Method is used to create **individual objects**.

In short, while the Factory Method creates a single object, the Abstract Factory creates an entire family of related objects.

##

### <a name="builder"></a> Builder

The Builder pattern is another one of the creational patterns. It **separates the construction of a complex object from its representation**, allowing the same construction process to create different representations.

In other words, the Builder **allows the step-by-step construction of a complex object**, without exposing the complexity of the construction process to the end customer.

Suppose we want to create a `Car` class with the following attributes: `tag`, `model`, `yearFabrication`, `numPorts`, `color` and `motorization`. In addition, we want the creation of the car to be done step by step, that is, first we define the make and model, then the year, then the number of doors, and so on.

Using the Builder pattern, we can simplify the creation of objects of this class by allowing attributes to be defined in separate steps, on a per-client basis.

Here's the example:

```java
public class Car {
     private String tag;
     private String model;
     private int yearFabrication;
     private int numPorts;
     private String color;
     private String motorization;

     public Car() {}

     public Car(String tag, String model, int yearFabrication, int numPorts, String color, String motorization) {
         this.tag = tag;
         this.model = model;
         this.yearFabrication = yearFabrication;
         this.numPorts = numPorts;
         this.color = color;
         this.motorization = motorization;
     }

     // getters and setters
}
```

Now, we create a Builder class that will allow us to build the car step by step:
```java
public class CarBuilder {
     private String tag;
     private String model;
     private int yearFabrication;
     private int numPorts;
     private String color;
     private String motorization;

     public CarBuilder() {}

     public CarBuilder withTag(String tag) {
         this.tag = tag;
         return this;
     }

     public CarBuilder withModel(String model) {
         this.model = model;
         return this;
     }

     public CarBuilder withYearFabrication(int yearFabrication) {
         this.yearFabrication = yearFabrication;
         return this;
     }

     public CarBuilder withNumPorts(int numPorts) {
         this.numPorts = numPorts;
         return this;
     }

     public CarBuilder withColor(String color) {
         this.color = color;
         return this;
     }

     public CarBuilder withMotorization(String motorization) {
         this.motorization = motorization;
         return this;
     }

     public Car build() {
         return new Carro(tag, model, yearFabrication, numPorts, color, motorization);
     }
}
```
Note that the `Builder` has the same attributes as the `Car` class, but also has methods to define each of these attributes step by step. Each of these methods returns its own Builder (this), allowing us to chain the method calls into a single line.

Finally, we can use Builder to create a car step by step:

```java
Car car = new CarBuilder()
         .withTag("Ford")
         .withModel("Mustang")
         .withYearFabrication(2022)
         .withNumPorts(2)
         .withColor("red")
         .withMotorization("V8")
         .build();
```

Notice how each Builder method call sets an attribute of the car. When we call the `build()` method at the end, the Builder creates and returns a Car object complete with all the attributes and characteristics we passed, making object instantiation a simple and flexible process.

##
### Prototype

The Prototype design pattern aims to allow the creation of new objects from **cloning existing objects**, without requiring detailed knowledge of its implementation. In other words, **it allows the creation of new objects from an existing model**.

The Prototype pattern is useful in situations where creating an object is very expensive or complex, or when creating an object requires setting many parameters. Instead of creating a new object every time it is needed, the Prototype pattern **allows the cloning of the existing object, making the creation process much more efficient**.

In terms of implementation, the Prototype pattern defines a `Cloneable` interface, which allows an object to be cloned. This object must implement the `clone()` method, which makes a copy of the object and returns a reference to the new cloned object.

A real example of using the Prototype pattern in Java is when creating documents. Suppose an application needs to create documents with different layouts and styles. Instead of creating a new object for each document, we can create an initial template and clone it to create new documents with the same characteristics.

Here is an example implementation in Java:

```java
public abstract class Document implements Cloneable {
 
     private String content;
 
     public Document(String content) {
         this.content = content;
     }
 
     public abstract Document clone();
 
     public String getContent() {
         return content;
     }
 
     public void setContent(String content) {
         this.content = content;
     }
 
}
```

In this example, the abstract class `Document` defines the initial model for all documents. It implements the `Cloneable` interface and defines an abstract `clone` method, which will be implemented by concrete subclasses.

Here is an example of a concrete class that implements object cloning:

```java
public class DefaultDocument extends Document {
 
     public StandardDocument(String content) {
         super(content);
     }
 
     public Document clone() {
         return new StandardDocument(getContent());
     }
 
}
```

In this example, the `DocumentoPadrao` class extends the Document class and implements the `clone` method. This method creates a new instance of `StandardDocument` and returns a reference to it.

With the implementation of the `Prototype` pattern, we can create different types of documents with different layouts and styles from an initial template, making the process of creating new documents much more efficient and simplified.

##

## Structural Patterns [Building... 👷]
