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
   * [Adapter](#adapter)
   * [Bridge](#bridge)
   * [Composite](#composite)
   * [Decorator](#decorator)
   * [Facade](#facade)
   * [Flyweight](#flyweight)
* **Behavioral patterns**
  * [Chain Of Responsability](#cor)
  * [Command](#command)
  * [Iterator](#iterator)
  * [Mediator](#mediator)
  * [Memento](#memento)
  * [Observer](#observer)
  * [State](#state)
  * [Strategy](#strategy)
  * [Template Method](#tm)
  * [Visitor](#visitor)
  
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

## Structural Patterns
### <a name="adapter"></a> Adapter

The Adapter pattern is a structural design pattern that allows two classes with incompatible interfaces to work together. It converts the interface of one class into another interface that the client expects. This allows objects with different interfaces to work together, without the client needing to modify the code of the original class.

In Java, the Adapter pattern is implemented through an adapter class that implements the desired interface and contains an instance of the original class. The adapter class implements the methods of the desired interface and calls the corresponding methods in the original class.

Here is a real-world example of the Adapter pattern in Java:

Suppose we have a class that provides weather information, but its interface is not compatible with the interface that the client wants to use. Instead of modifying the original class, we can create an adapter class that implements the desired interface and calls the corresponding methods in the original class.

```java
// Client interface
public interface WeatherInfo {
    public double getTemperature();
    public double getHumidity();
}

// Original class with incompatible interface
public class Weather {
    public float getTemp() {
        // code to get the temperature
    }

    public float getHumi() {
        // code to get the humidity
    }
}

// Adapter class
public class WeatherAdapter implements WeatherInfo {
    private Weather weather;

    public WeatherAdapter(Weather weather) {
        this.weather = weather;
    }

    public double getTemperature() {
        return weather.getTemp();
    }

    public double getHumidity() {
        return weather.getHumi();
    }
}
```

In this example, the `Weather` class provides weather information, but its interface is not compatible with the client's interface. The `WeatherAdapter` class implements the `WeatherInfo` interface and contains an instance of the `Weather` class. The `WeatherAdapter` class implements the methods of the `WeatherInfo` interface and calls the corresponding methods in the `Weather` class.

With the Adapter pattern, the client can use the `WeatherAdapter` class to get weather information, without needing to modify the original `Weather` class. This allows objects with different interfaces to work together, without the client needing to modify the code of the original class.

##

### <a name="bridge">Bridge</a>

The Bridge pattern is a structural design pattern that separates an abstraction from its implementation, allowing both to vary independently. This is useful when we have multiple variations of abstractions and implementations, and we want to avoid an explosion of subclasses.

In Java, the Bridge pattern can be implemented using an abstract class that represents the abstraction and an interface that represents the implementation. The abstract class has a reference to the interface and delegates the method calls to the implementation.

Here is a real example of the Bridge pattern in Java:

Suppose we have a drawing application that allows the user to draw different shapes, such as rectangles, circles, and triangles. For each shape, we have different variations of colors and drawing styles. To avoid an explosion of subclasses for each combination of shape and style, we can use the Bridge pattern.

```java
// Implementation interface
public interface DrawingAPI {
    public void drawShape(int x, int y, int width, int height);
}

// Implementation A
public class DrawingAPIA implements DrawingAPI {
    public void drawShape(int x, int y, int width, int height) {
        // draw the shape using implementation A
    }
}

// Implementation B
public class DrawingAPIB implements DrawingAPI {
    public void drawShape(int x, int y, int width, int height) {
        // draw the shape using implementation B
    }
}

// Abstraction
public abstract class Shape {
    protected DrawingAPI drawingAPI;

    public Shape(DrawingAPI drawingAPI) {
        this.drawingAPI = drawingAPI;
    }

    public abstract void draw();
}

// Refined Abstraction
public class Rectangle extends Shape {
    private int x, y, width, height;

    public Rectangle(int x, int y, int width, int height, DrawingAPI drawingAPI) {
        super(drawingAPI);
        this.x = x;
        this.y = y;
        this.width = width;
        this.height = height;
    }

    public void draw() {
        drawingAPI.drawShape(x, y, width, height);
    }
}

// Refined Abstraction
public class Circle extends Shape {
    private int x, y, radius;

    public Circle(int x, int y, int radius, DrawingAPI drawingAPI) {
        super(drawingAPI);
        this.x = x;
        this.y = y;
        this.radius = radius;
    }

    public void draw() {
        drawingAPI.drawShape(x, y, radius, radius);
    }
}
```

In this example, the `DrawingAPI` interface represents the implementation of how to draw the shapes. The `DrawingAPIA` and `DrawingAPIB` classes are different implementations of the `DrawingAPI` interface.

The abstract class `Shape` represents the abstraction of a generic shape. It has a reference to the `DrawingAPI` interface and delegates the `draw()` method call to the implementation. The `Rectangle` and `Circle` classes are refined variations of the `Shape` abstraction, each with their own specific parameters and behaviors.

With the Bridge pattern, we can add new shapes or implementations without needing to create a new class for each combination of shape and style. This simplifies the code and makes maintenance easier.

##

### <a name="composite">Composite</a>

The Composite pattern is a structural design pattern that allows composing objects into tree structures to represent object hierarchies. It enables clients to treat individual objects and collections of objects uniformly.

In Java, the Composite pattern can be implemented using an interface or abstract class that represents the base component and a class that represents the composite component. The base component can have methods that are implemented by both simple components and composite components. The composite component maintains a list of its child components and implements methods that work with the child list.

Here is a real-world example of the Composite pattern in Java:

Suppose we have a hierarchy of components to build a menu for an application. The menu can be composed of several menu items, including drop-down menus and regular menu items. Each menu item can have a label, an icon, and an action associated with it. We can use the Composite pattern to create a tree structure to represent the menu.

```java
// Base component
public interface MenuComponent {
    public void add(MenuComponent menuComponent);
    public void remove(MenuComponent menuComponent);
    public MenuComponent getChild(int i);
    public String getName();
    public String getDescription();
    public void print();
}

// Leaf component
public class MenuItem implements MenuComponent {
    private String name;
    private String description;
    private boolean vegetarian;
    private double price;

    public MenuItem(String name, String description, boolean vegetarian, double price) {
        this.name = name;
        this.description = description;
        this.vegetarian = vegetarian;
        this.price = price;
    }

    public String getName() {
        return name;
    }

    public String getDescription() {
        return description;
    }

    public boolean isVegetarian() {
        return vegetarian;
    }

    public double getPrice() {
        return price;
    }

    public void print() {
        System.out.print("  " + getName());
        if (isVegetarian()) {
            System.out.print("(v)");
        }
        System.out.println(", " + getPrice());
        System.out.println("     -- " + getDescription());
    }

    public void add(MenuComponent menuComponent) {
        throw new UnsupportedOperationException();
    }

    public void remove(MenuComponent menuComponent) {
        throw new UnsupportedOperationException();
    }

    public MenuComponent getChild(int i) {
        throw new UnsupportedOperationException();
    }
}

// Composite component
public class Menu implements MenuComponent {
    private List<MenuComponent> menuComponents = new ArrayList<>();
    private String name;
    private String description;

    public Menu(String name, String description) {
        this.name = name;
        this.description = description;
    }

    public void add(MenuComponent menuComponent) {
        menuComponents.add(menuComponent);
    }

    public void remove(MenuComponent menuComponent) {
        menuComponents.remove(menuComponent);
    }

    public MenuComponent getChild(int i) {
        return menuComponents.get(i);
    }
    
    public String getName() {
        return name;
    }

    public String getDescription() {
        return description;
    }

    public void print() {
        System.out.println("\n" + getName());
        System.out.println(", " + getDescription());
        System.out.println("---------------------");

        for (MenuComponent menuComponent : menuComponents) {
           menuComponent.print();
     }
}
```


In this example, the `MenuComponent` interface is the base component, and the `MenuItem` and `Menu` classes are the leaf and composite components, respectively. The `MenuItem` class represents a regular menu item, while the `Menu` class represents a drop-down menu. The `Menu` class maintains a list of its child components and implements the `add`, `remove`, and `getChild` methods to manage them.

When we want to print the menu, we can call the `print` method of the root component of the hierarchy, which in our case is the `Menu` class. The `print` method traverses the child component list and calls the `print` method on each of them, printing the name, description, and price of the menu items, as well as the names of the drop-down menus.

##

### <a name="decorator">Decorator</a>
The Decorator design pattern is a structural pattern that allows adding additional behaviors to objects dynamically, without modifying their original structure. It is very useful in situations where we need to add functionalities to an object in a flexible and modular way, without the need to create subclasses for each combination of functionalities.

The Decorator pattern is implemented by creating an abstract Decorator class that implements the same interface as the original object and contains a reference to the original object. Then, the concrete classes that implement the additional behavior extend the Decorator class and add their functionalities to the original object.

To illustrate the Decorator pattern, let's consider an example of a coffee shop that sells different types of coffee. Each coffee can be decorated with different ingredients, such as milk, whipped cream, caramel, etc. Instead of creating a separate class for each possible combination of coffee with additional ingredients, we can use the Decorator pattern to dynamically add the desired ingredients.

```java
// Component interface
public interface Beverage {
    String getDescription();
    double getCost();
}

// Concrete component
public class Espresso implements Beverage {
    public String getDescription() {
        return "Espresso";
    }

    public double getCost() {
        return 1.99;
    }
}

// Decorator abstract class
public abstract class CondimentDecorator implements Beverage {
    protected Beverage beverage;

    public CondimentDecorator(Beverage beverage) {
        this.beverage = beverage;
    }

    public abstract String getDescription();
}

// Concrete decorator classes
public class Milk extends CondimentDecorator {
    public Milk(Beverage beverage) {
        super(beverage);
    }

    public String getDescription() {
        return beverage.getDescription() + ", Milk";
    }

    public double getCost() {
        return beverage.getCost() + 0.10;
    }
}

public class Caramel extends CondimentDecorator {
    public Caramel(Beverage beverage) {
        super(beverage);
    }

    public String getDescription() {
        return beverage.getDescription() + ", Caramel";
    }

    public double getCost() {
        return beverage.getCost() + 0.20;
    }
}

// Client code
public class Cafe {
    public static void main(String[] args) {
        Beverage espresso = new Espresso();
        System.out.println(espresso.getDescription() + " $" + espresso.getCost());

        Beverage espressoWithMilk = new Milk(espresso);
        System.out.println(espressoWithMilk.getDescription() + " $" + espressoWithMilk.getCost());

        Beverage espressoWithCaramel = new Caramel(espresso);
        System.out.println(espressoWithCaramel.getDescription() + " $" + espressoWithCaramel.getCost());

        Beverage espressoWithMilkAndCaramel = new Caramel(new Milk(espresso));
        System.out.println(espressoWithMilkAndCaramel.getDescription() + " $" + espressoWithMilkAndCaramel.getCost());
    }
}
```
In this example, the `Beverage` interface is the base component, and the `Espresso` class is the concrete implementation of this component. The `CondimentDecorator`, `Milk`, and `Caramel` classes are the abstract and concrete decorators, respectively. The `CondimentDecorator` class is an abstract class that extends the `Beverage` interface and contains a reference to another Beverage instance. The `Milk` and `Caramel` classes are concrete decorators that extend the `CondimentDecorator` class and add functionalities to the original object. The client code creates different combinations of coffee with ingredients by instantiating different decorators and chaining them together with the original `Beverage` object.

##

### <a name="facade">Facade</a>
The Facade pattern is a structural design pattern that provides a simplified interface to a set of more complex and hard-to-use classes. The goal of the Facade pattern is to provide an abstraction layer that hides the underlying complexity of the system and provides a simple and easy-to-use interface for clients.

The Facade pattern is useful when there is a complex system with many classes and interfaces, and the client needs to interact with several parts of it. Instead of the client having to know all the implementation details of the system, they can simply use the interface provided by the facade.

The Facade pattern is implemented by creating a class that provides a simplified interface to the client, hiding all the complexity of the underlying system. The facade delegates method calls to the system classes and returns results in a simple and easy-to-use way for the client.

To illustrate the Facade pattern, let's consider an example of a banking system. The banking system may have many different classes and interfaces, such as bank accounts, credit cards, loans, etc. Instead of the client having to interact directly with all these classes and interfaces, we can provide a facade that simplifies the client's interaction with the banking system.

```java
// Facade class
public class BankSystem {
    private AccountService accountService;
    private CreditCardService creditCardService;
    private LoanService loanService;

    public BankSystem() {
        accountService = new AccountService();
        creditCardService = new CreditCardService();
        loanService = new LoanService();
    }

    public void createAccount(String customerName, String accountType) {
        accountService.createAccount(customerName, accountType);
    }

    public void applyForCreditCard(String customerName) {
        creditCardService.applyForCreditCard(customerName);
    }

    public void applyForLoan(String customerName, double amount) {
        loanService.applyForLoan(customerName, amount);
    }
}

// Account service class
public class AccountService {
    public void createAccount(String customerName, String accountType) {
        // Implementation details
    }
}

// Credit card service class
public class CreditCardService {
    public void applyForCreditCard(String customerName) {
        // Implementation details
    }
}

// Loan service class
public class LoanService {
    public void applyForLoan(String customerName, double amount) {
        // Implementation details
    }
}

// Client code
public class BankClient {
    public static void main(String[] args) {
        BankSystem bankSystem = new BankSystem();
        bankSystem.createAccount("John Doe", "Checking");
        bankSystem.applyForCreditCard("John Doe");
        bankSystem.applyForLoan("John Doe", 10000);
    }
}
```
In this example, the `BankSystem` class is the facade that provides a simplified interface for the client to interact with the banking system. The facade delegates method calls to the `AccountService`, `CreditCardService`, and `LoanService` classes, which are the complex classes of the banking system. The client interacts only with the facade, which hides all the complexity of the underlying system.

The Facade pattern is very useful when dealing with complex and hard-to-use systems. It provides an abstraction layer that makes it easier for clients to use the system, and it also makes it easier to change the system without affecting the clients.

##

### <a name="flyweight">Flyweight</a>
The Flyweight pattern is used to minimize memory usage when dealing with large numbers of similar objects. The idea behind this pattern is to share as much data as possible between similar objects, rather than creating new objects every time.

In Java, the Flyweight pattern can be implemented using a combination of a factory class and a flyweight class. The factory class is responsible for managing the flyweights and maintaining a cache of existing flyweights. The flyweight class contains the shared state between the objects and the context-specific state is passed in as arguments when the flyweight method is called.

Here's an example implementation of the Flyweight pattern in Java:

```java
import java.awt.Color;
import java.awt.Graphics;
import java.util.HashMap;
import java.util.Map;

// Flyweight interface
interface Shape {
    void draw(Graphics g, int x, int y, int width, int height, Color color);
}

// Concrete flyweight
class Circle implements Shape {
    private Color color;

    public void draw(Graphics g, int x, int y, int width, int height, Color color) {
        this.color = color;
        g.setColor(color);
        g.drawOval(x, y, width, height);
    }
}

// Flyweight factory
class ShapeFactory {
    private static final Map<Color, Shape> circleMap = new HashMap<>();

    public static Shape getCircle(Color color) {
        Circle circle = (Circle) circleMap.get(color);

        if (circle == null) {
            circle = new Circle();
            circleMap.put(color, circle);
        }

        return circle;
    }
}

// Client code
public class Client {
    private static final Color[] colors = { Color.RED, Color.GREEN, Color.BLUE };

    public static void main(String[] args) {
        for (int i = 0; i < 20; ++i) {
            Circle circle = (Circle) ShapeFactory.getCircle(getRandomColor());
            circle.draw(getRandomX(), getRandomY(), getRandomWidth(), getRandomHeight(), circle.color);
        }
    }

    private static Color getRandomColor() {
        return colors[(int) (Math.random() * colors.length)];
    }

    private static int getRandomX() {
        return (int) (Math.random() * 100);
    }

    private static int getRandomY() {
        return (int) (Math.random() * 100);
    }

    private static int getRandomWidth() {
        return (int) (Math.random() * 100);
    }

    private static int getRandomHeight() {
        return (int) (Math.random() * 100);
    }
}
```

In this example, the `Shape` interface represents the flyweight and the `Circle` class represents a concrete flyweight. The `ShapeFactor`y class is responsible for managing the flyweights and maintaining a cache of existing flyweights. The `Client` class uses the `ShapeFactory` to obtain flyweights and calls their `draw()` method with context-specific state.

The `ShapeFactory` maintains a `Map` of existing `Circle` objects keyed by their color. When a new `Circle` object is requested, the `ShapeFactory` checks if an object with the requested color already exists. If it does, the existing object is returned. If not, a new `Circle` object is created, added to the cache, and returned.

In this example, 20 `Circle` objects are created with random colors and positions. Note that the colors are shared among multiple Circle objects, thanks to the use of the Flyweight pattern. By using this pattern, we can significantly reduce the amount of memory required to store similar objects. Instead of creating 20 `Circle` objects with different colors, only 3 `Circle` objects are created,

##

### <a name="cor"></a> Chain of Responsability

The Chain of Responsibility pattern is a behavioral pattern that **allows a series of objects (or handlers) to handle a request, where each object decides whether to handle the request** or pass it on to the next object in the chain. It is like an assembly line, where each step adds some value and then passes the product to the next step.

The pattern is composed of three main elements:

* Handler: Defines a common interface for all objects in the chain. This object is responsible for handling the request and deciding whether to pass it on to the next object in the chain or not.

* ConcreteHandler: Implements the handler interface and handles the request. If the object cannot handle the request, it will pass the request to the next object in the chain.

* Client: Initiates the request for the chain of objects.

Let's say we are building a login validation system for a Java web application. In this system, we want to ensure that the user's password has at least 8 characters, contains uppercase and lowercase letters, and has at least one special character.

We can use the Chain of Responsibility pattern to implement password validation, where each validation will be handled by a different handler, and if a validation fails, the responsibility will be passed to the next handler in the chain.

Here is an example implementation:

```java
public abstract class PasswordValidator {
    private PasswordValidator nextValidator;

    public PasswordValidator(PasswordValidator nextValidator) {
        this.nextValidator = nextValidator;
    }

    public boolean validate(String password) {
        if (this.performValidation(password)) {
            if (this.nextValidator != null) {
                return this.nextValidator.validate(password);
            } else {
                return true;
            }
        } else {
            return false;
        }
    }

    protected abstract boolean performValidation(String password);
}

public class LengthValidator extends PasswordValidator {
    public LengthValidator(PasswordValidator nextValidator) {
        super(nextValidator);
    }

    protected boolean performValidation(String password) {
        return password.length() >= 8;
    }
}

public class UppercaseValidator extends PasswordValidator {
    public UppercaseValidator(PasswordValidator nextValidator) {
        super(nextValidator);
    }

    protected boolean performValidation(String password) {
        return password.matches(".*[A-Z].*");
    }
}

public class LowercaseValidator extends PasswordValidator {
    public LowercaseValidator(PasswordValidator nextValidator) {
        super(nextValidator);
    }

    protected boolean performValidation(String password) {
        return password.matches(".*[a-z].*");
    }
}

public class SpecialCharValidator extends PasswordValidator {
    public SpecialCharValidator(PasswordValidator nextValidator) {
        super(nextValidator);
    }

    protected boolean performValidation(String password) {
        return password.matches(".*[!@#$%^&*()_+\\-=\\[\\]{};':\"\\\\|,.<>\\/?].*");
    }
}
```

In this example, we have the abstract class `PasswordValidator`, which defines the structure of the password validation chain. Each validation handler is implemented by a concrete class that inherits from `PasswordValidator`. Each handler performs a specific validation on the password and calls the next handler in the chain if the validation is successful.

The `Client` class can then create an instance of each handler and configure the responsibility chain by setting the next handler for each one. Then, the client calls the `validate` method of the instance of the first handler in the chain, passing in the password to be validated.

```java
public class Client {
    public static void main(String[] args) {
        PasswordValidator lengthValidator = new LengthValidator(null);
        PasswordValidator uppercaseValidator = new UppercaseValidator(lengthValidator);
        PasswordValidator lowercaseValidator = new LowercaseValidator(uppercaseValidator);
        PasswordValidator specialCharValidator = new SpecialCharValidator(lowercaseValidator);
        
        String password = "MyPassword123!";

        if (specialCharValidator.performValidation(senha)) {
            System.out.println("Valid password!");
        } else {
            System.out.println("Invalid password!");
        }
    }
 }
```

Overall, the Chain of Responsibility pattern provides a flexible and scalable way to handle requests in a system by allowing a chain of objects to handle the request. This can be useful in a variety of scenarios, such as validation, logging, error handling, and more. By breaking down the handling of requests into smaller, more manageable parts, the Chain of Responsibility pattern can help to simplify complex systems and make them easier to maintain and extend.

##

### <a name="command"></a> Command

The Command pattern is a behavioral design pattern that is used to **encapsulate a request as an object**, allowing you to parameterize clients with different requests, queue or log requests, and support undoable operations. In other words, the Command pattern **helps to separate the object that issues a request from the object that actually executes the request.**

Let's say we have an application that can perform various tasks, such as saving a file, printing a document, closing a program, etc. With the Command pattern, we can encapsulate each task as a command object, which can be executed later. Here is a simple example of how the Command pattern can be implemented in Java:

```java
public interface Command {
    void execute();
}

public class SaveCommand implements Command {
    private Document document;

    public SaveCommand(Document document) {
        this.document = document;
    }

    @Override
    public void execute() {
        document.save();
    }
}

public class PrintCommand implements Command {
    private Document document;

    public PrintCommand(Document document) {
        this.document = document;
    }

    @Override
    public void execute() {
        document.print();
    }
}

public class Document {
    public void save() {
        // code to save the document
    }

    public void print() {
        // code to print the document
    }
}

public class Application {
    private Command saveCommand;
    private Command printCommand;

    public Application(Command saveCommand, Command printCommand) {
        this.saveCommand = saveCommand;
        this.printCommand = printCommand;
    }

    public void saveDocument() {
        saveCommand.execute();
    }

    public void printDocument() {
        printCommand.execute();
    }
}
```

In this example, we have a `Command` interface that defines the `execute()` method that must be implemented by each specific command. Next, we have two concrete command classes, `SaveCommand` and `PrintCommand`, each with a reference to the `Document` object that will be manipulated. The `Document` class contains the actual operations to save and print a document.

Finally, we have the `Application` class, which has references to the command objects and provides methods to execute them. Note that the `Application` class does not need to know how each command is implemented, it just needs to know that each command implements the `Command` interface and can be executed.

Thus, we can create an instance of `Application` by passing the `SaveCommand` and `PrintCommand` objects as arguments, and then call the `saveDocument()` and `printDocument()` methods when necessary.

```java
Document document = new Document();
Command saveCommand = new SaveCommand(document);
Command printCommand = new PrintCommand(document);
Application app = new Application(saveCommand, printCommand);

// save the document
app.saveDocument();

// print the document
app.printDocument();
```

Note that if we needed to add a new operation, such as closing the document, for example, we could create a new command class that implements the `Command` interface and add it to the `Application` class without affecting existing code. This is possible thanks to the encapsulation provided by the Command pattern.

##

### <a name="iterator"></a> Iterator

The Iterator pattern is a behavioral design pattern that **allows iterating over elements of a collection sequentially without exposing its internal structure**. It enables accessing the elements of a collection without concerning how the collection is implemented or stored. In Java, the Iterator pattern is extensively used in the collections of the Java Collections Framework API, such as ArrayList, LinkedList, and HashSet.

The Iterator pattern defines two main interfaces: the Iterator interface and the Iterable interface. The Iterator interface is used for iterating over the elements of a collection, while the Iterable interface is used for obtaining an Iterator object for a collection. The class that implements the Iterable interface should provide an implementation of the iterator() method that returns an Iterator object for the collection.

Here's an example of how to use the Iterator pattern in Java:

```java
import java.util.ArrayList;
import java.util.Iterator;

public class IteratorExample {

    public static void main(String[] args) {
        ArrayList<String> names = new ArrayList<>();
        names.add("Alice");
        names.add("Bob");
        names.add("Charlie");

        // Get an Iterator object for the names collection
        Iterator<String> iterator = names.iterator();

        // Traverse the collection using the Iterator
        while (iterator.hasNext()) {
            String name = iterator.next();
            System.out.println(name);
        }
    }

}
```

In this example, we create a collection of names using the `ArrayList` class. Next, we obtain an Iterator object for the collection using the `iterator()` method of the `ArrayList` class. Then, we use a `while` loop to traverse the collection using the `Iterator`. Inside the while loop, we use the `hasNext()` method to check if there are still elements in the collection and the `next()` method to get the next element.

Another example is the following:

```java
import java.util.HashSet;
import java.util.Iterator;

public class IteratorExample {

    public static void main(String[] args) {
        HashSet<Integer> numbers = new HashSet<>();
        numbers.add(1);
        numbers.add(2);
        numbers.add(3);

        // Get an Iterator object for the numbers collection
        Iterator<Integer> iterator = numbers.iterator();

        // Traverse the collection using the Iterator
        while (iterator.hasNext()) {
            Integer number = iterator.next();
            System.out.println(number);
        }
    }

}
```

In this example, we create a collection of numbers using the `HashSet` class. Next, we obtain an `Iterator` object for the collection using the `iterator()` method of the `HashSet` class. Then, we use a `while` loop to traverse the collection using the `Iterator`. Inside the `while` loop, we use the `hasNext()` method to check if there are still elements in the collection and the `next()` method to get the next element.

The Iterator pattern is an efficient and flexible way to iterate over elements of a collection in Java. It provides a high-level abstraction that allows traversing the collection independently of the underlying implementation. It also provides a safe mechanism for accessing the elements of the collection and protects the collection against accidental modifications during iteration.

##

### <a name="mediator"></a> Mediator

The Mediator pattern is a behavioral design pattern that **allows communication between different objects without them directly knowing each other**. Instead, a mediator object is responsible for managing the communication and interactions between the objects. This helps decouple the involved objects and simplify their interaction, making code maintenance and evolution easier.

In Java, the Mediator pattern can be used in various situations, such as messaging systems, chat systems, multiplayer games, home automation systems, among others. Let's analyze an example of a chat system to better understand how the pattern works.

Suppose we are developing a chat system where several people can chat in the same room. Each person can send and receive messages from the other users in the room. To implement this using the Mediator pattern, we can create a ChatRoom class that acts as the mediator between the different users in the room.

Here's an example of how to use the Mediator pattern in Java:

```java
import java.util.ArrayList;
import java.util.List;

public class ChatRoom {
    private List<User> users = new ArrayList<>();

    public void sendMessage(String message, User sender) {
        for (User user : users) {
            if (user != sender) {
                user.receiveMessage(message);
            }
        }
    }

    public void addUser(User user) {
        users.add(user);
    }
}

public class User {
    private String name;
    private ChatRoom chatRoom;

    public User(String name, ChatRoom chatRoom) {
        this.name = name;
        this.chatRoom = chatRoom;
    }

    public void sendMessage(String message) {
        chatRoom.sendMessage(message, this);
    }

    public void receiveMessage(String message) {
        System.out.println(name + " received message: " + message);
    }
}

public class ChatRoomExample {
    public static void main(String[] args) {
        ChatRoom chatRoom = new ChatRoom();

        User alice = new User("Alice", chatRoom);
        User bob = new User("Bob", chatRoom);
        User charlie = new User("Charlie", chatRoom);

        chatRoom.addUser(alice);
        chatRoom.addUser(bob);
        chatRoom.addUser(charlie);

        alice.sendMessage("Hello, everyone!");
        bob.sendMessage("Hi, Alice!");
        charlie.sendMessage("Hey, guys!");
    }
}
```

In this example, the `ChatRoom` class acts as the mediator between the different users in the room. It has a list of users who have been added to the room and a `sendMessage` method that sends a message to all users except the sender.

The `User` class represents a user in the chat room. Each user has a name and a reference to the chat room they are participating in. Each user also has a `sendMessage` method that sends a message to the chat room using the `sendMessage` method of the `ChatRoom` class. When a user receives a message, the `receiveMessage` method is called to print the message on the screen.

Finally, in the `ChatRoomExample` class, we create a chat room and add three users to the room. Then, each user sends a message to the chat room using the `sendMessage` method.

The Mediator pattern is an efficient way to manage communication between different objects in Java, helping to decouple the objects involved in the communication. It is particularly useful in scenarios where multiple objects need to communicate with each other in a complex way and can be used in various types of applications, from chat applications to complex enterprise applications.

##

### <a name="memento"></a> Memento

The Memento pattern is a behavioral design pattern that **allows you to save and restore the state of an object without violating encapsulation**. This is especially useful in situations where you want to allow an object to return to a previous state without exposing its internal structure.

In Java, the Memento pattern **is commonly used in applications where an object's state history is important**, such as text editors, games, and drawing applications. Let's take a look at an example of a text editor to better understand how the pattern works.

Suppose we're developing a text editor that allows the user to type and edit the contents of the document. Additionally, the editor should be able to undo the changes made by the user, returning the contents of the document to a previous state. To implement this using the Memento pattern, we can create a Memento class that acts as a capsule that stores the object's previous state.

Here's an example of using the Memento pattern in Java:

```java
public class TextEditor {
    private StringBuilder content = new StringBuilder();
    private Stack<TextEditorMemento> mementos = new Stack<>();

    public void append(String text) {
        mementos.push(saveMemento());
        content.append(text);
    }

    public void undo() {
        if (!mementos.isEmpty()) {
            restoreMemento(mementos.pop());
        }
    }

    private TextEditorMemento saveMemento() {
        return new TextEditorMemento(content.toString());
    }

    private void restoreMemento(TextEditorMemento memento) {
        content = new StringBuilder(memento.getState());
    }

    public String getContent() {
        return content.toString();
    }

    private class TextEditorMemento {
        private String state;

        public TextEditorMemento(String state) {
            this.state = state;
        }

        public String getState() {
            return state;
        }
    }
}

public class TextEditorExample {
    public static void main(String[] args) {
        TextEditor editor = new TextEditor();

        editor.append("Hello");
        editor.append(", World!");

        System.out.println(editor.getContent()); // Output: "Hello, World!"

        editor.undo();

        System.out.println(editor.getContent()); // Output: "Hello"
    }
}
```

In this example, the `TextEditor` class represents the text editor itself. It has a `StringBuilder` that stores the current contents of the document and a `Stack` that stores the previous states of the document. The `append` and `undo` methods are used to add text to the document and undo the last change, respectively.

The `TextEditorMemento` class acts as the capsule that stores the previous state of the document. It has a single attribute that represents the previous state of the document and a `getState` method to return the stored state.

When the `append` method is called, the text editor pushes a new `TextEditorMemento` to the mementos stack and adds the text to the `StringBuilder`. When the undo method is called, the text editor restores the previous state of the document using the most recent `TextEditorMemento` in the mementos stack.

Finally, in the `TextEditorExample` class, we create a text editor, add two lines of text to the document, and then undo the last action using the undo method. Then we add one more line of text and undo again. At the end, we print the updated document to verify that only the first and third lines remain.

The Memento pattern is useful in situations where you need to save an object's state at a certain point in time so that it can be restored later, such as in text editors, graphics editors, games, and financial applications. It allows the object to maintain

##

### <a name="observer"></a> Observer

The Observer pattern is a behavioral design pattern that defines a **one-to-many relationship between objects, so that when one object changes its state, all of its dependents are notified and updated automatically**.

The Observer pattern is composed of two main entities: the subject (or observable) and the observer. The subject is the object that contains the state that can change, while the observer is the object that depends on the subject's state and needs to be notified when a change occurs.

In Java, the `Observer` pattern is often implemented using the `Observer` interface and the `Observable` class. The `Observable` class represents the subject and the Observer interface represents the observer.

Here's a simple example of how to use the Observer pattern in Java:

```java
import java.util.Observable;
import java.util.Observer;

public class WeatherStation extends Observable {
    private int temperature;
    private int humidity;

    public void setWeather(int temperature, int humidity) {
        this.temperature = temperature;
        this.humidity = humidity;

        setChanged();
        notifyObservers();
    }

    public int getTemperature() {
        return temperature;
    }

    public int getHumidity() {
        return humidity;
    }
}

public class PhoneDisplay implements Observer {
    private WeatherStation weatherStation;

    public PhoneDisplay(WeatherStation weatherStation) {
        this.weatherStation = weatherStation;
        weatherStation.addObserver(this);
    }

    public void update(Observable obs, Object arg) {
        if (obs instanceof WeatherStation) {
            WeatherStation weatherStation = (WeatherStation) obs;
            System.out.println("Temperature: " + weatherStation.getTemperature() + "°C, Humidity: " + weatherStation.getHumidity() + "%");
        }
    }
}

public class WeatherStationExample {
    public static void main(String[] args) {
        WeatherStation weatherStation = new WeatherStation();
        PhoneDisplay phoneDisplay = new PhoneDisplay(weatherStation);

        weatherStation.setWeather(25, 60); // Output: "Temperature: 25°C, Humidity: 60%"
    }
}
```

In this example, the `WeatherStation` class represents the subject and contains the state that can change, represented by the temperature and humidity. When the `setWeather` method is called, the state is updated and the `setChanged` and `notifyObservers` methods are called. The `setChanged` method informs that the object's state has changed and the `notifyObservers` method notifies all registered observers about the change.

The `PhoneDisplay` class represents the observer and is notified about the state change using the `update` method. The `update` method is automatically called by the subject whenever a change occurs. In this example, the observer prints the current temperature and humidity.

Finally, in the `WeatherStationExample` class, we create an instance of the `WeatherStation` class and an instance of the `PhoneDisplay` class. The `PhoneDisplay` instance registers as an observer of the `WeatherStation` instance using the `addObserver` method. Then, we `update` the temperature and humidity using the `setWeather` method and observe that the `PhoneDisplay` instance is automatically notified and prints the current temperature and humidity.

In summary, the Observer pattern is useful for implementing communication between objects in a decoupled way, allowing an object to be automatically notified when a change occurs in another object, without there being coupling between them. This allows an object to be changed without affecting other objects that depend on it, making the code more modular and flexible.

##

### <a name="state"></a> State

The State pattern is a behavioral design pattern that allows an object to change its behavior when its internal state changes. This is achieved by separating the behavior into separate classes that represent each possible state of the object.

The State pattern is composed of two main entities: the context and the state. The context is the object that contains the internal state that can change, while the state is the class that represents each possible state of the object.

In Java, the State pattern is often implemented using interfaces and concrete classes. The `State` interface represents the state, and the concrete classes implement the specific logic of the state. The `Context` class represents the object that contains the internal state.

Here's a simple example of how to use the State pattern in Java:

```java
public interface State {
    void pressPlay();
}

public class ReadyState implements State {
    private AudioPlayer audioPlayer;

    public ReadyState(AudioPlayer audioPlayer) {
        this.audioPlayer = audioPlayer;
    }

    public void pressPlay() {
        audioPlayer.changeState(new PlayingState(audioPlayer));
    }
}

public class PlayingState implements State {
    private AudioPlayer audioPlayer;

    public PlayingState(AudioPlayer audioPlayer) {
        this.audioPlayer = audioPlayer;
    }

    public void pressPlay() {
        audioPlayer.changeState(new ReadyState(audioPlayer));
    }
}

public class AudioPlayer {
    private State state;

    public AudioPlayer() {
        state = new ReadyState(this);
    }

    public void changeState(State newState) {
        state = newState;
    }

    public void pressPlay() {
        state.pressPlay();
    }
}

public class AudioPlayerExample {
    public static void main(String[] args) {
        AudioPlayer audioPlayer = new AudioPlayer();

        audioPlayer.pressPlay(); // Output: "Playing"
        audioPlayer.pressPlay(); // Output: "Ready"
    }
}
```

In this example, the `State `class represents the state and defines the `pressPlay` method. The `ReadyState` and `PlayingState` classes implement the specific logic of each state and implement the `pressPlay` method according to the necessary behavior.

The `AudioPlayer` class represents the context and contains the internal state of the object. The `changeState` method changes the internal state of the object to the new state. The `pressPlay` method delegates the `pressPlay` call to the current state.

Finally, in the `AudioPlayerExample` class, we create an instance of the `AudioPlayer` class and call the `pressPlay` method twice. In the first call, the object's state is changed to `PlayingState`, and the message "Playing" is printed. In the second call, the object's state is changed back to ReadyState, and the message "Ready" is printed.

In summary, the State pattern is useful for implementing objects that change behavior according to their internal state. This allows the code to be more modular and flexible, as the logic of each state is encapsulated in its own class. Additionally, the State pattern allows the object to change its behavior without the need to change its public interface.

##

### <a name="strategy"></a> Strategy

The Strategy pattern is a behavioral design pattern that allows an object to have variable behavior, enabling the class to select an algorithm from several different ones, depending on the needs of the context in which the object is being used. This can be useful in situations where a class needs to dynamically change its behavior at runtime.

In Java, the Strategy pattern is often implemented using interfaces and concrete classes. The Strategy interface defines the common behavior of all strategies, while the concrete classes implement specific algorithms.

Here is a simple example of using the Strategy pattern in Java:

```java
public interface PaymentStrategy {
    void pay(double amount);
}

public class CreditCardStrategy implements PaymentStrategy {
    private String name;
    private String cardNumber;
    private String cvv;
    private String dateOfExpiry;

    public CreditCardStrategy(String name, String cardNumber, String cvv, String dateOfExpiry) {
        this.name = name;
        this.cardNumber = cardNumber;
        this.cvv = cvv;
        this.dateOfExpiry = dateOfExpiry;
    }

    public void pay(double amount) {
        System.out.println("Paid " + amount + " using credit card");
    }
}

public class PayPalStrategy implements PaymentStrategy {
    private String email;
    private String password;

    public PayPalStrategy(String email, String password) {
        this.email = email;
        this.password = password;
    }

    public void pay(double amount) {
        System.out.println("Paid " + amount + " using PayPal");
    }
}

public class ShoppingCart {
    private List<Item> items;

    public ShoppingCart() {
        this.items = new ArrayList<>();
    }

    public void addItem(Item item) {
        this.items.add(item);
    }

    public void removeItem(Item item) {
        this.items.remove(item);
    }

    public double calculateTotal() {
        double sum = 0;
        for (Item item : items) {
            sum += item.getPrice();
        }
        return sum;
    }

    public void pay(PaymentStrategy paymentStrategy) {
        double amount = calculateTotal();
        paymentStrategy.pay(amount);
    }
}

public class StrategyExample {
    public static void main(String[] args) {
        ShoppingCart cart = new ShoppingCart();

        Item item1 = new Item("Shirt", 100);
        Item item2 = new Item("Pants", 200);

        cart.addItem(item1);
        cart.addItem(item2);

        cart.pay(new CreditCardStrategy("John Doe", "123456789", "123", "12/24"));
        cart.pay(new PayPalStrategy("johndoe@example.com", "password"));
    }
}
```

In this example, the `PaymentStrategy` interface defines the common behavior of all strategies. The `CreditCardStrategy` and `PayPalStrategy` classes implement specific payment algorithms using credit card and PayPal, respectively.

The `ShoppingCart` class represents the context in which the strategy is used. The `pay` method delegates the call to the `pay` method to the selected strategy. This allows the `ShoppingCart` object to have different payment behaviors, depending on the selected strategy.

In the `StrategyExample` class, we create an instance of the `ShoppingCart` class and add two items. Then, we select different payment strategies, passing each one as a parameter to the `pay` method.

In summary, the Strategy pattern is a behavioral design pattern that allows different algorithms to be dynamically selected at runtime, depending on the context in which they are used. It separates the algorithm from its implementation, allowing each to be changed independently without affecting the client code.

##

### <a name="tm"></a> Template Method

The Template Method pattern is a behavioral design pattern that defines the basic structure of an algorithm, allowing subclasses to provide specific implementations for certain steps of the algorithm. This allows the overall structure of the algorithm to be defined in a base class, while specific details are left to the subclasses.

The Template Method pattern **is useful in situations where multiple algorithms have similar structures, but differ in some details**. Instead of repeating the same basic structure in multiple classes, the Template Method pattern **allows the overall structure to be defined in a single class and specific details to be implemented in subclasses**.

In Java, the Template Method pattern is often implemented using an abstract class that defines the template method, which defines the overall structure of the algorithm, and abstract methods, which subclasses must implement to provide specific details.

Here is a simple example of how to use the Template Method pattern in Java:

```java
public abstract class Game {
    protected abstract void initialize();
    protected abstract void startPlay();
    protected abstract void endPlay();

    public final void play() {
        initialize();
        startPlay();
        endPlay();
    }
}

public class Chess extends Game {
    @Override
    protected void initialize() {
        System.out.println("Initializing Chess Game...");
    }

    @Override
    protected void startPlay() {
        System.out.println("Starting Chess Game...");
    }

    @Override
    protected void endPlay() {
        System.out.println("Ending Chess Game...");
    }
}

public class TicTacToe extends Game {
    @Override
    protected void initialize() {
        System.out.println("Initializing Tic-Tac-Toe Game...");
    }

    @Override
    protected void startPlay() {
        System.out.println("Starting Tic-Tac-Toe Game...");
    }

    @Override
    protected void endPlay() {
        System.out.println("Ending Tic-Tac-Toe Game...");
    }
}

public class TemplateMethodExample {
    public static void main(String[] args) {
        Game chess = new Chess();
        chess.play();

        Game tictactoe = new TicTacToe();
        tictactoe.play();
    }
}
```

In this example, the abstract class `Game` defines the template method `play`, which defines the overall structure of the game. The `Chess` and `TicTacToe` subclasses implement the abstract methods `initialize`, `startPlay`, and `endPlay`, which provide specific details for each game.

The `TemplateMethodExample` class creates instances of the `Chess` and `TicTacToe` subclasses and calls the `play` method on each of them. The `play` method executes the overall structure of the game, calling the `initialize`, `startPlay`, and `endPlay` methods in the subclasses.

In summary, the Template Method pattern is a behavioral design pattern that defines the basic structure of an algorithm in a base class and allows subclasses to provide specific details. In Java, the Template Method pattern is often implemented using an abstract class that defines the template method and abstract methods that subclasses must implement. The example above shows how to use the Template Method pattern to create different games with similar structures but different specific details.

##

### <a name="visitor"></a> Visitor

The Visitor pattern is a behavioral design pattern that allows adding new operations to an existing object structure without modifying the structure itself. It separates the object operations into separate classes called visitors, allowing new operations to be added to the system without modifying existing classes.

The Visitor pattern is **useful when there is a complex object structure that contains many different types of objects and many operations that can be performed on those objects**. Instead of adding these operations directly to the objects, the Visitor pattern adds them as visitors, which visit the objects and perform the operations.

In Java, the Visitor pattern is often implemented using interfaces for visitors and the classes that will be visited. The visited classes implement an accept method that takes a visitor as an argument and calls the appropriate method of the visitor. Each visitor implements methods to perform the operations on the objects it visits.

Here is a simple example of how to use the Visitor pattern in Java:
```java
interface Visitor {
    void visit(Circle circle);
    void visit(Square square);
}

interface Shape {
    void accept(Visitor visitor);
}

class Circle implements Shape {
    public void accept(Visitor visitor) {
        visitor.visit(this);
    }
}

class Square implements Shape {
    public void accept(Visitor visitor) {
        visitor.visit(this);
    }
}

class AreaVisitor implements Visitor {
    public void visit(Circle circle) {
        System.out.println("Calculating area of circle");
    }
    public void visit(Square square) {
        System.out.println("Calculating area of square");
    }
}

class PerimeterVisitor implements Visitor {
    public void visit(Circle circle) {
        System.out.println("Calculating perimeter of circle");
    }
    public void visit(Square square) {
        System.out.println("Calculating perimeter of square");
    }
}

public class VisitorExample {
    public static void main(String[] args) {
        Shape[] shapes = {new Circle(), new Square()};
        Visitor areaVisitor = new AreaVisitor();
        Visitor perimeterVisitor = new PerimeterVisitor();

        for (Shape shape : shapes) {
            shape.accept(areaVisitor);
            shape.accept(perimeterVisitor);
        }
    }
}
```

In this example, the `Shape` interface defines the `accept` method, which takes a visitor as an argument. The `Circle` and `Square` classes implement the accept method, calling the appropriate visitor method.

The `Visitor`, `AreaVisitor`, and `PerimeterVisitor` interfaces define the operations that can be performed on the visited objects. Each of the visitor classes implements the methods defined in the `Visitor` interface, performing the operations on the visited objects.

The `VisitorExample` class creates an array of `Shape` objects and two visitors, `AreaVisitor` and `PerimeterVisitor`. It iterates through the array of `Shape` objects, calling the `accept` method on each one, passing the visitors as arguments. The `accept` method calls the appropriate visitor method, which performs the appropriate operation on the visited object.

In summary, the Visitor pattern is a behavioral design pattern that allows adding new operations to an existing object structure without modifying the structure itself. In Java, the Visitor pattern is often implemented using interfaces for visitors and the classes that will be visited. The example shown defines how the Visitor pattern can be implemented in Java to add a new operation to an existing object structure.

#

## Congratulation!! You finished all topics of Guide GoF

Congratulations on completing this comprehensive guide to the 23 design patterns defined by the Gang of Four! We hope you have found it informative and useful in your development work.

By understanding and implementing these patterns, you will be able to write more flexible, reusable, and maintainable code. These patterns are tried and true solutions to common problems in software design, and their use can greatly enhance the quality of your applications.

We would like to thank you for taking the time to read this guide and hope that it has helped you become a better developer. If you found it useful, we would appreciate it if you could give the repository a star and share it with your friends and colleagues.

For more information on software design patterns and related topics, please follow us on social media:

* Instagram: [@ivii.ns](https://www.instagram.com/ivii.ns/)
* Linkedin: [Dev-Ivi](https://www.linkedin.com/in/ivisson-pereira-b301aa250/)
> Thank you again for reading, and happy coding!
