# Module 7: Abstract Classes and Interfaces

# Introduction

> "Abstraction is the elimination of the irrelevant and the amplification of the essential." 
> 
> **Robert C. Martin**


One of the biggest advantages of object-oriented programming (OOP) is the ability to leverage inheritance and polymorphism. Inheritance allows more specific types of objects with each new subclass. Conversely, going back up the class hierarchy then each class becomes more generalized. 

## Learning Objectives
- [Abstract Classes](#abstract-classes) 
- [Interfaces](#interfaces) 
- [Multiple Inheritance](#multiple-inheritance) 
- [Interface Testing](#interface-testing) 
- [Plugins](#plugins)
- [Advanced Topics](#advanced-topics)

# Abstract Classes

There are cases where there will be a common, shared behavior but there is no way to have a common, shared implementation. Some examples include a Shape class calculating the area of the shape or the perimeter of the shape. Both a Circle and a Square class would need to have methods to do this, but the actual calculation of the area or perimeter would be different between a Circle and a Square. Another example would be a card game application. All card games need to score the player's hand, but the scoring is done differently in each game. 

In these cases, when a common behavior is needed but there is no common implementation possible, the method in question and the class must be declared as abstract. The abstract class and method are represented in UML Class Diagrams either with the class name and abstract method in *italics*, or like this:

<figure>
    <pre class="mermaid">
    classDiagram
        Shape <|-- Circle
        Shape <|-- Square
    
        class Shape {
            &lt;&lt;abstract&gt;&gt;
            +area() double
            +perimeter() double
        }
    
        class Circle {
            -radius : double
            +area() double
            +perimeter() double
        }
    
        class Square {
            -sideLength : double
            +area() double
            +perimeter() double
        }
    </pre>
  <figcaption class="align-center">Figure 7.1: UML of abstract and concrete classes</figcaption>
</figure>

This diagram represents an abstract class, Shape, with two abstract methods. Through inheritance the *Circle* and *Square* class extend *Shape* and implement their own *area()* and *perimeter()* methods.

An ***abstract method*** declares a method signature but with no method body. If a class has even one abstract method, the entire class must also be abstract. If a method is abstract and therefore missing an implementation, it's not possible to create an instance of that class. If that method was called, Java wouldn't know what to do! This is why any class with an abstract method makes the entire class an abstract class. A subclass that is not also abstract must override this method and provide an implementation before an object instance can be created. This means that abstract methods cannot be private.

<caption><strong>Code Example: Abstract methods</strong></caption>

```java
/**
 * Represent a geometric shape
 * @version 20240730.01
 */
public abstract class Shape
{
  ...
  
  public Shape()
  {
  
  }
  
  ...
  
  /**
  * Calculate the area of the shape
  * @return the area of the shape
  */
  public abstract double area();
  
  /**
  * Calculate the perimeter of the shape
  * @return the area of the shape
  */
  public abstract double perimeter();
} 
```

## Abstract Class Usage
Since there are parts of the class implementation declared but missing, abstract classes can only be used as a superclass, no instances of an abstract class can be created. Abstract classes can have everything a regular class would have, including instance variables, constructors, and methods that are implemented. Since an abstract class can have some implementation, abstract classes are still limited to single class inheritance. 

Abstract classes are used when you want to provide a common base implementation for related classes but don’t know enough to create a common shared implementation. They are only used in an inheritance hierarchy as the superclass of more specific classes that can provide the implementation. The subclasses do this by overriding the abstract method to provide the implementation.

<caption><strong>Code Example: Circle class</strong></caption>

```java
public class Circle extends Shape
{
  private double radius;
  private double area;
  
  public Circle(double radius)
  {
    super();
  }
  ...
  @Override
  public double area()
  {
    // PI r^2
    return Math.PI * radius * radius;
  }
  
  @Override
  public double perimeter()
  {
    // 2PIr
    return 2 * Math.PI * radius;
  }
  ...
} 
```

These abstract classes can still be used as a ***static data type***, so all the benefits of ***polymorphism*** are still possible. In this example, even though Shape is an abstract class it can still be used as the instance’s data type.

<caption><strong>Code Example: Polymorphism</strong></caption>

```java
Shape shape = new Circle(16.0);
```

The abstract method in *Shape* is essentially a contract with the Java compiler. It says *Shape* doesn’t know what the abstract method’s implementation will be, but it guarantees to the compiler that they will be implemented in the subclass. 

This gives the best of all worlds! The DRY principle is leveraged with the ability to write commonly implemented code once, while guaranteeing a common functionality (calculating the area of a shape in the example) and still using polymorphism. Abstract classes can do all of this by simply allowing unknown details to be implemented in a common way later in a specific subclass.

# Interfaces

Imagine taking the concept of an abstract class to the extreme, where every single method was abstract. Is this possible? Yes! It is a concept called an ***interface*** and is a surprisingly powerful tool in object-oriented programming.

## Abstract Method Redux
An abstract method in Java is a method that is declared without an implementation. This means that the method does not have a body and is meant to be overridden in subclasses. This is used to define a shared behavior among the subclasses even when there is no way to know how that might be implemented. Abstract methods enable a clear and enforceable contract for subclasses that the Java compiler recognizes.

## Interfaces
An interface is treated like a special type of class in Java. In a lot of ways an interface is like an abstract class, because it defines behavior for common classes, but doesn't provide any implementation. Interfaces provide a powerful way to achieve abstraction in Java. They allow developers to define a contract that classes can implement, specifying what methods a class must have without dictating how these methods should be implemented. There are many examples of this from comparing two objects for sorting to doing database operations.

<section class="callout info">
A class that implements an interface can and often does implement other methods beyond what are required by the interface.
</section>

Variables can be declared in an interface, but they must be public, static, and constant. Since every method in an interface is abstract, the abstract keyword is omitted. Likewise, every method in an interface must be public, so the public keyword is also omitted.

<caption><strong>Code Example: Interface format</strong></caption>

```java
public interface InterfaceName
{
  ReturnType methodName(parameters);
  ...
} 
```

An interface can be used in Java much like an abstract class. The interface essentially provides a contract to the Java compiler guaranteeing that at least these methods will be there when the application runs. An interface can be used as a static data type for a variable. Like abstract classes, an instance of an interface cannot be created with the new keyword.

<section class="callout info">
When using an interface or abstract class as an object type, any methods outside of those defined in the abstract class or interface are hidden until the object is cast to the actual type.
</section>

A very good example of the power of interfaces can be seen in the Java *Comparable* interface. The [Comparable interface in Java](https://docs.oracle.com/javase/8/docs/api/java/lang/Comparable.html) is built into the SDK and is used to define a natural ordering for objects of a class. This allows objects of a class to be compared and sorted in a collection. It defines a single method, *compareTo()*, that determines the order of objects. 

Think about comparing String objects to each other versus comparing Integer objects to each other. The String would probably be compared alphabetically, but the Integer class would use the actual numeric value for comparison. There is no common implementation for these, but the behavior of comparing them for sorting is quite easy to understand. This is a great use of an interface!

Because an interface does not dictate any shared implementation, they promote loose coupling and design flexibility. They allow developers to change the implementation (the dynamic type of an object) without affecting the code that depends on the interface. This makes the code more modular, which is easier to maintain and extend. This is known as the ***Dependency Inversion Principle***. 

The *Comparable* interface shown earlier is a great example of this, with the static *Collections.sort()* method using the *Comparable* interface to sort any collection of objects, whether they are part of the Java SDK or custom objects created as part of a single project. In short, because the *Comparable.sort()* method can guarantee the objects have a *compareTo()* method, it will work for absolutely anything that has this implemented without needing to be rewritten.

## Using Interfaces
An interface is very similar to an abstract class, but the way it is declared in a class is slightly different. Since there are normally no concrete methods available, an interface uses the keyword ***implements*** instead of extends. Here's an example of a class implementing the *Comparable* interface:

<caption><strong>Code Example: Using the Comparable interface</strong></caption>

```java
public class Shape implements Comparable<Shape>
{
  ...
  public abstract area();
  ...
  
  @Override
  public int compareTo(Shape o)
  {
    // Comparing the area of the two shapes
    return this.area() - o.area();
  }
} 
```

<section class="callout info">
Comparable is using a ***Generic***, which says this must use a class of the type defined inside the &gt; &lt; brackets. In this case, *Comparable* is being implemented only with *Shape* objects.
</section>

Another good example from the Java SDK of an interface with similar functionality is the ***Comparator*** interface. The *Comparator* interface allows custom sorting of objects that don’t have a natural ordering, or when you want to sort objects in an order different from their natural ordering. Consider a playing card for a card game. It will have a rank, points, and a suit. It can be useful to sort on any one of these fields. The *Comparator* interface makes this possible. 

Implementing the *Comparator* interface is done in a different class than the one being compared. That class must override the *compare(T o1, T o2)* method for comparing two objects of the same type. The *compare()* method returns an integer just like the *Comparable* interface’s *compareTo()* method.

<caption><strong>Code Example: Using the Comparator interface</strong></caption>

```java
public SuitComparator implements Comparator<Card>
{
  public Suitcomparator()
  {
  
  }
  
  @Override
  public int compare(Card o1, Card o2)
  {
    // Assuming Suit is an enum, use the Comparable is using a Generic, which says this must use a class of the type defined inside the <> brackets.
    // In this case, Comparable is being implemented only with Shape objects.
    
    // ordinal integer value for comparison
    return o1.getSuit().ordinal() - o2.getSuit().ordinal();
  }
} 
```

Other implementations can be created for rank and points in this case, and these can all be passed to *Collections.sort()* or *Arrays.sort()* for sorting. It would be used like this, assuming there was a collection of *Card* objects called cards:

<caption><strong>Code Example: Calling the Collections.sort() method</strong></caption>

```java
Collections.sort(cards, new SuitComparator());
```

While *Comparator* uses another helper class to do its work, it makes sense to implement it in the class itself. This can be done using a static method that will return a *Comparator* object.

<caption><strong>Code Example: Implementing Comparable and Comparator interfaces</strong></caption>

```java
public Card implements Comparable<Card>, Comparator<Card>
{
  ...
  @Override
  public int compareTo(Card o)
  {
    return this.getPoints() - o.getPoints();
  }
  
  public static Comparator<Card> suitComparator = new Comparator<Card>
  {
    @Override
    public int compare(Card o1, Card o2)
    {
      // Assuming Suit is an enum, use the ordinal integer value for comparison
      return o1.getSuit().ordinal() - o2.getSuit().ordinal();
    }
  }
}
```

Here the static method *suitComparator()* returns an anonymous implementation of the *Comparator* interface. Other implementations can be created for rank and points in this case, and these can all be passed to *Collections.sort()* or *Arrays.sort()* for sorting. This keeps all these utility classes directly associated with the class they work on. It would be used like this, assuming there was a collection of *Card* objects called cards:

<caption><strong>Code Example: Calling the Collections.sort() method with Card class' suitComparator</strong></caption>

```java
Collections.sort(cards, Card.suitComparator);
```

<section class="callout info">
Anonymous classes are created and instantiated in a single expression. They are anonymous because they don’t have a class name associated with them.
</section>

### Sorting with a Secondary Key
It is also possible to do a sort on a secondary key if the primary sort field is equal. People’s names are often sorted this way, where if two different people have the same last name, they will then be sorted on Anonymous classes are created and instantiated in a single expression. They are anonymous because they don’t have a class name associated with them. their first name. The person’s first name is the secondary sort key. The *Card* object could also do the same thing, where if the main field was equal a secondary field could help refine the comparison.

<caption><strong>Code Example: Secondary key sort</strong></caption>

```java
import java.util.Comparator;

public Card implements Comparable<Card>
{
  ...
  @Override
  public int compareTo(Card o)
  {
    int result = this.getPoints() - o.getPoints();
    
    // If points are equal, compare the suit
    if (result == 0)
    {
      // Assuming suit is an enum
      result = this.getSuit().ordinal() - o.getSuit().ordinal();
    }
    return result;
  }
  
  public static Comparator<Card> suitComparator = new Comparator<Card>
  {
    @Override
    public int compare(Card o1, Card o2)
    {
      // Assuming Suit is an enum, use the ordinal integer value for comparison
      int result = o1.getSuit().ordinal() - o2.getSuit().ordinal();
      
      if (result == 0)
      {
        result = o1.getPoints - o2.getPoints();
      }
      return result;
    }
  }
} 
```

Now, if two cards have the same points, the two will be sorted against each other using the suit when using *Comparable*. Similarly, if two cards have the same suit, they will be sorted against each other using the points when using the *Comparator*. 

**Comparable vs Comparator** 
- The *Comparable* interface can be used to provide a single (natural) way of sorting, whereas the *Comparator* interface is used to provide different ways of sorting collections of the same object 
- For using *Comparable*, classes need to implement it in the class, but when using *Comparator* a separate class needs to be created 
    - The *Comparable* interface is in *java.lang* package and doesn’t require an import
    - The *Comparator* interface is in *java.util* package and does require an import 
- *Arrays.sort()* and *Collection.sort()* methods automatically uses the *Comparable* interface’s *compareTo()* method of the class

### Interface Documentation
Classes that implement an interface and have Javadoc can often skip writing the Javadoc for the methods the class overrides. Any class that implements this interface doesn't have to write this documentation again, the documentation on the interface applies everywhere it is implemented. However, the documentation may be written to elaborate on specific implementation details.

# Multiple Inheritance

Class inheritance is tightly controlled in Java, with each class only being allowed to directly inherit from one other class. This is done to prevent any contradiction between two parent classes. Imagine if two different classes implemented the exact same method and a subclass inherited from each directly. When that superclass method was called, which one would Java use? There would be no way to know which should have priority.

<figure>
    <pre class="mermaid">
    classDiagram
        class SubClass
        SuperClass1 <|-- SubClass
        SuperClass2 <|-- SubClass
        class SuperClass1 {
            +method1()
        }
        class SuperClass2 {
            +method1()
        }
    </pre>
  <figcaption class="align-center">Figure 7.2: Problems with multi-class inheritance</figcaption>
</figure>

Here, if such a class hierarchy were possible and an instance of *SubClass* tried to call *method1()* there are two possible choices. Would Java run the implementation in *SuperClass1* or *SuperClass2*? There would be no way to prioritize one over the other. To avoid this, Java eliminates the problem completely by preventing multiple inheritance from classes. This is done with Java syntax by only allowing a class to directly extend one other class. 

Is this a problem with interfaces though? Since interfaces have no implementation, the implementing class must provide its own override implementation.
<figure>
    <pre class="mermaid">
    classDiagram
    
    class Interface1 {
        &lt;&lt;interface&gt;&gt;
        +method1() void
    }
    
    class Interface2 {
        &lt;&lt;interface&gt;&gt;
        +method1() void
    }
    
    class MyClass {
        +method1() void
    }
    
    Interface1 <|.. MyClass
    Interface2 <|.. MyClass
    </pre>
  <figcaption class="align-center">Figure 7.3: Multiple inheritance using interfaces</figcaption>
</figure><p>

This means if two different interfaces happened to declare the same method interface, the subclass override would still provide a clear implementation for Java to call. This means there would be no confusion about which implementation to use. Because of this, it is possible to implement multiple interfaces in Java, giving a form of multiple inheritance.

<caption><strong>Code Example: Multiple interfaces format</strong></caption>

```java
public class MyClass implements Comparable, Cloneable 
{ 
  ... 
}
```

The comma separated list of interfaces tells the Java Compiler that all methods defined in both interfaces will be implemented. If two different interfaces declared the same method, the implementing class would satisfy both interfaces when that method was implemented.

# Interface Testing

Since interfaces define a shared set of behavior, it is possible to write one set of unit tests that will work for any implementation. This makes testing significantly easier and more scalable. 

Since any class that implements an interface must implement the same methods as declared in the interface, it makes sense that the same tests should work for all implementations of the interface. Instead of re-writing the same tests, with a little bit of thought it is possible to design one set of tests that can be reused. Using ***reflection***, it is possible to create an instance of a class using the *Class* object. The *Object* class includes an instance of the *Class* class as a field, accessible with *ClassType.class* or the method *instance.getClass()*.

<section class="callout info">
The Class object in Java is a special type of object that represents the runtime metadata of a class. It serves as a blueprint or template for creating instances of that class and provides information about the class itself.
</section>

<section class="callout info">
Reflection is the ability to inspect and modify a class when an application is running. This includes obtaining information about the fields, methods, and constructors of loaded classes and invoking them, even if they are private or protected.
</section>

Here is a very basic example testing the *size()* method of the *List* interface, using the *ArrayList* and *LinkedList* implementations. Reflection is used to create instances of each in a JUnit 5 parameterized test:

<caption><strong>Code Example: Parameterized test for the List interface</strong></caption>

```java
@ParameterizedTest
@ValueSource(classes = { ArrayList.class, LinkedList.class })
void parameterizedInterfaceTest(Class<?> c)
{
  // Arrange - Declaring the fixture using the Interface type
  List<Integer> l = null;
  
  try
  {
    // Act - this may throw an exception
    // Reflection is used to get an instance of the class from a constructor
    // This instance is then cast as a List<Integer>
    l = (List<Integer>) c.getDeclaredConstructor().newInstance();
    
    // Assert
    Assertions.assertEquals(0, l.size());
  }
  catch (Exception e)
  {
    // If getDeclaredConstructor threw an exception, the test failed
    Assertions.fail();
  }
} 
```

If there were a third implementation of the interface, the same test could be used by simply adding it to the *ValueSource* collection. Classes that extend an abstract class may be able to use this approach to test the abstract methods.

# Plugins

A software ***plugin*** is a component loaded from outside the application. Plugins add specific enhancements or functionality to an existing computer program or application without modifying its core code. Plugins enable 3rd party users to add new features, improve performance, or integrate third-party services without altering the main program.

<section class="callout info">
3rd party is a term that refers to an independent person or organization not affiliated with the main application or software product.
</section>

When a user interacts with the plugin's elements, the plugin code is executed by the main application, performing its intended function. This could involve adding new tools, processing data, or calling external services. IntelliJ is one example of a software package that supports using plugins to add, improve, or change its functionality. On the welcome page of IntelliJ, where a project can be opened or created, there is also an option to manage Plugins.

<figure>
  <img class="align-center" src="images/7/intellij_plugin_marketplace.png" alt="The IntelliJ plugin browser showing plugins from the online IntelliJ Plugin Browser">
  <figcaption class="align-center">Figure 7.4: IntelliJ Plugin Browser</figcaption>
</figure><p>

<section class="callout info">
Marketplace allows searching for any available plugin. 

Installed shows plugins currently installed in IntelliJ, and the ability to uninstall, or if updates are available, update installed plugins
</section>

Search for the following three plugins and read about what each one of them does: 
- Indent Rainbow by Dmitry Murzin 
- Rainbow Brackets by Zhihao Zhang 
- SonarLint by SonarSource

<section class="callout success">
If these three plugins are not installed, it is highly recommended to add them.
</section>

None of these three plugins were written by JetBrains or a member of the IntelliJ team. Each adds a nice enhancement to IntelliJ that isn't natively available. How is it possible for a person or company to write code that will directly integrate with IntelliJ if they aren't on the IntelliJ development team? The answer is simple, Interfaces! 

Any application that supports plugins provides an interface to 3rd party developers outside of the organization. The method or methods in that interface provide the hook that allows the main application to understand how to interact with the plugin code. 

The main application (IntelliJ in this case) loads each plugin from a ***JAR file*** in a particular folder on the computer's hard drive. It then declares an instance of the class(es) inside the JAR file using the interface as the static object type. The program then calls the method(s) on that interface and the plugin then executes, adding the new functionality.

<section class="callout info">
JAR stands for Java ARchive, and is a way of building and packaging Java components so they can be distributed and shared with others.
</section>

Writing an application that supports plugins is beyond the scope of this book. For a basic working code example and accompanying article, look at the following [GitHub repository on Java plugin quickstart](https://github.com/suvodeep-pyne/java-plugin-quickstart){:target="_blank"}

# Advanced Topics

## Marker Interfaces
A Java interface that does not define any methods or fields is commonly referred to as a ***marker interface***. Marker interfaces provide the ability to do type tagging and provide metadata about classes. Marker interfaces are used to tag or mark a class as having a particular property or capability. This tagging can then be used by other parts of the code, such as frameworks or libraries, to apply specific behavior to marked classes. [Cloneable](https://docs.oracle.com/javase/8/docs/api/java/lang/Cloneable.html) is a good example of a marker interface used for tagging.

The other common use of a marker interface is to provide metadata about a class. This metadata can then be checked at runtime using reflection to determine if a class should be treated differently based on the presence of the marker interface.

<section class="callout info">
Annotations are often used as an alternative to marker interfaces for providing metadata. Annotations can provide more flexibility and additional information compared to marker interfaces.
</section>

## Interface Methods
***Default methods*** are a feature added in Java version 8 for Java interfaces and provide a way to add method implementations to interfaces. The main purpose of default methods is to enable adding new methods to existing interfaces without forcing all implementing classes to provide an implementation. This allowed adding new methods to existing interfaces in the JDK without breaking backwards compatibility. They are declared using the ***default*** keyword. This blurs the line significantly between abstract classes and interfaces.

<caption><strong>Code Example: Description</strong></caption>

```java
interface InterfaceWithDefaultMethod
{
  void abstractMethod();
  
  default void defaultMethod()
  {
    System.out.println("This is a default method.");
  }
}
```

Default methods also introduce potential problems with the ability of interfaces to provide multiple inheritance. The workaround is if two different interfaces provide a default method implementation for the same method signature, the implementing class **MUST** override that and provide its own implementation. If a class wants to use one of the interface's methods, it needs to override the method and then call the specific interface implementation.

<caption><strong>Code Example: Interface1 implementation</strong></caption>

```java
interface Interface1
{
  default void show()
  {
    System.out.println("Default show method in Interface1");
  }
} 
```

<caption><strong>Code Example: Interface2 implementation</strong></caption>

```java
interface Interface2
{
  default void show()
  {
    System.out.println("Default show method in Interface2");
  }
}
```

<caption><strong>Code Example: Explicit reference to show() method</strong></caption>

```java
class MyClass implements Interface1, Interface2
{
  // Providing an implementation of the show method from both interfaces
  public void show()
  {
    // Provide our own implementation
    System.out.println("Method in MyClass");
    
    // Or, use super keyword to call the show method of one of the Interfaces
    Interface1.super.show();
  }
} 
```

Since abstract classes already provided a way to implement some but not all methods, why was this introduced? As mentioned earlier, this enabled adding new methods to existing interfaces without breaking backwards compatibility, since the default method provides an implementation for older code written before the interface had new methods added. Default methods also helped facilitate the introduction of lambda expressions and functional interfaces in Java 8. If a project doesn’t fit into one of these two situations, it is recommended to stick with abstract classes. 

In addition to default methods, interfaces can also have static methods, just like a class. These methods are called the same way as well.

## Interface Fields
While an interface can have a field, such a field is implicitly public, static, and final, meaning it is effectively constant. As such, naming conventions for any constant apply (ALL_CAPS using snake case). Since they are public, they can be accessed directly without the need of an accessor method. Interface fields are of limited usefulness but is a feature to be aware of.

## Composition
Inheritance is a key feature of object-oriented programming, but it is not the only way to achieve clean code reuse. An alternative approach is called ***Composition***. 

Composition is a design technique where a class contains instances of other classes as instance variables. The containing class is said to be composed of the contained classes, and it uses their behavior through their exposed public API (public methods). In Java, composition is achieved by creating an instance of one class within another class. 

In this example, the Car class is composed partially of the Engine class:

<caption><strong>Code Example: Engine class definition</strong></caption>

```java
class Engine
{
  ...
  void start()
  {
    System.out.println("Engine started.");
  }
} 
```

<caption><strong>Code Example: Car partial composition</strong></caption>

```java
class Car
{
  private Engine engine;
  
  Car()
  {
    engine = new Engine();
  }
  
  void startCar()
  {
    engine.start();
  }
} 
```

With this structure, the Engine class can easily be re-used in any other class, such as a Motorcycle, Boat, Airplane, Bandsaw, Drill Press, etc. without being forced into a class hierarchy. 

While both composition and inheritance promote code reuse, they have different implications and tradeoffs: 
- **Flexibility**: Composition provides more flexibility than inheritance o With composition, you can change the behavior of a class by replacing the composed objects at runtime. With inheritance, the behavior is fixed at compile-time
- **Code Reuse**: Inheritance promotes code reuse through the inheritance hierarchy, while composition allows code reuse by creating instances of existing classes 
- **Coupling**: Inheritance creates a tight coupling between the subclass and superclass, as changes in the superclass can affect the subclass. Composition promotes loose coupling, as the containing class and contained classes are independent of each other 
- **Extensibility**: Composition is generally preferred for extensibility, as it allows you to create new classes by combining existing ones, without modifying the existing code 
- **Polymorphism**: Inheritance has better direct support for polymorphism

# Summary

## Abstract Class Summary
- An abstract method can only be declared in an abstract class. If a subclass of an abstract class doesn’t override and implement all abstract methods from the superclass, then it also must be abstract 
- Abstract classes and methods are non-static, although an abstract class can implement a static method 
- An abstract class cannot be instantiated using the new operator, but constructors can still be defined. They are used in subclasses with a call to super 
- A class with an abstract method must be an abstract class. It is possible though for a class to be abstract with no abstract methods. In this case, the abstract class still cannot have instances created due to being abstract 
- A subclass can be abstract even if the superclass is not. For instance, the Object class is not abstract, but other Java classes can be 
- A subclass can override a method from the superclass and define it as abstract. This is extremely rare but might be useful if the implementation in the superclass is invalid for some reason in the subclass 
- An instance of an abstract class cannot be created with the new operator, but an abstract class can be used as a data type. This means all the capability of Polymorphism applies to abstract classes

## Interfaces Summary
- Cannot be instantiated 
- Can only contain abstract methods (prior to Java 8) 
- Can have default and static methods (Java 8+) 
- Cannot have instance variables (only static final constants) 
- Support multiple inheritance (a class can implement multiple interfaces) 
- All members are implicitly public 
- Used to define a contract that classes must adhere to

## Comparing Interfaces and Abstract Classes
- Abstract classes can have state (instance variables), while interfaces cannot 
- A class can extend only one abstract class but implement multiple interfaces 
- Abstract classes can have constructors, interfaces cannot 
- Abstract classes can have any access modifier for members, interfaces are implicitly public 
- Both abstract classes and interfaces are used for abstraction, but abstract classes are typically used when you want to provide a common base implementation, while interfaces are used to define a contract for unrelated classes with a common behavior 
- A class name is a noun, whereas interface names may be adjectives or nouns
