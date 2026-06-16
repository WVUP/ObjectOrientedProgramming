# Module 5: Inheritance

# Introduction

> "Methods that use references to base classes must be able to use objects of derived
classes without knowing it."
>
> **Liskov Substitution Principle**

## Learning Objectives
- [Abstraction](#abstraction)
- [Encapsulation](#encapsulation)
- [Object Inheritance](#object-inheritance)
- [Polymorphism](#polymorphism)
- [Inheritance and the DRY Principle](#inheritance-and-the-dry-principle)
- [Casting](#casting)
- [Overrides](#overrides)
- [Comparing Objects](#comparing-objects)
- [Advanced Topics](#advanced-topics)

There are four aspects of Object-Oriented Programming that make it such a powerful paradigm for writing software. They are ***abstraction***, ***encapsulation***, ***inheritance***, and ***polymorphism***. These features allow an application to represent real-world things in software effectively and enable the creation of modular, reusable, and extensible code.

# Abstraction

***Abstraction*** is the process of hiding complex implementation details and exposing only the essential features or behaviors of the software that are relevant to solving the business problem to the user. It allows developers to focus on the relevant aspects of an object while ignoring the unnecessary details. Abstraction is achieved using classes, which provide a blueprint for creating objects with specific attributes and methods.

One example of abstraction might be representing a person in an application. A person will have a first name, last name, date of birth, address, race, gender, height, weight, hair color, eye color, etc. If they are in college, they’ll have a major, a list of classes they have completed (transcript), an advisor, and several other pieces of information about being in college.

A college student probably also has a driver’s license, and the DMV needs to keep track of several things that are important in an application for managing driver’s licenses. While there is some overlap, there are aspects of being a college student that the DMV doesn’t care about, and there are aspects of a state issued driver’s license that a college or university wouldn’t care about. Ignoring the things that are not relevant to the business problem that do exist in the real world and only managing what is relevant in an application is an example of abstraction.

Another example of abstraction would be calculating a GPA for a college student. There is a
weighted average formula for calculating a GPA that is a bit involved. It requires the final letter grade in a class and the number of credit hours for the class and uses this for all classes that have been completed to derive the GPA. Having all the data needed for this calculation as private fields in an object instance and just calling a public method on the student object, getGPA(), would be an example of abstraction. The actual calculation is hidden inside the method, but the result is available to other parts of the application with a simple method call. Hiding the complexity and implementation of the calculation behind this method call is also an example of abstraction.

# Encapsulation

***Encapsulation*** is the bundling of information (attributes) and behavior (methods) together within a single object. It enforces data hiding, where the internal implementation details are hidden from the outside world, and only a public interface is exposed for interacting with the object. Encapsulation promotes code modularity, data integrity, and code reusability. 

As a basic example, consider this code representing a bank account

<caption><strong>Code Example: Bank Account class</strong></caption>

```java
/**
 * A class representing a bank account that holds a customer's money.
 * @author Jane Q. Public
 * @version 2026.06.11.01
 */
public class BankAccount
{
  private double balance; 

  /**
   * Constructor that initializes the account with the provided balance.
   */
  public BankAccount(double initialBalance)
  {
    this.balance = initialBalance;
  }

  /**
   * @return double The current balance of the account.
   */
  public double getBalance()
  {
    // Rounds the balance to 2 digits of significance (dollars and cents)
    return Math.round(balance * 100.0) / 100.0;
  }

  /**
   * Add money to the account.
   *   The amount must be a positive value.
   * @throws Exception - Thrown if the amount is not a postivie value
   */
  public void deposit(double amount)
  {
    if (amount > 0.0)
    {
      balance += amount;
    }
    else
    {
      throw new Exception("Invalid value, amount must be positive");
    }
  }

  /**
   * Take money out of the account.
   *   The amount must not be more than has been deposited.
   * @throws Exception - Thrown if the amount requested is more than has been deposited
   */
  public void withdraw(double amount)
  {
    if (balance >= amount)
    {
      balance -= amount;
    }
    else
    {
      throw new Exception("Insufficient funds");
    }
  }
}
```

In this example, the *BankAccount* class encapsulates the balance field by making it private. The class provides public methods (*getBalance()*, *deposit()*, *withdraw()*) to access and modify the balance in a controlled manner.

This encapsulation protects the internal state (*balance*) from being directly accessed or
modified from outside the class. When getting the balance the underlying value is rounded into a two digit decimal number to better represent dollars and cents (later it will be explained why using a double data type for money is a bad idea). Also, two different instances of the BankAccount class would have the same fields and methods, but they would each have their own copy of them. This means updating the balance in one instance of a *BankAccount* would not impact the balance in the other instance.

In contrast, if a field or a method is marked ***static*** then the field or method is considered a ***class-level*** field or method instead of ***instance-level***. In that case, the ***static*** class component is not encapsulated in the instance but rather a single copy is shared among all instances.

Notice the validation logic in the class, where deposit ensures a positive amount is being added to the balance and withdrawal makes sure the balance has enough to cover the amount being withdrawn. If the balance was directly accessible outside of this class by being public, this validation could not be enforced outside of the class. This field being private and only read or changed with public methods ensures data integrity and allows additional logic or validation to be applied when reading or modifying the balance. This is the reason that Java classes make fields private and have public accessor and mutator methods.

# Object Inheritance

One of the key features of ***Object-Oriented Programming*** is inheritance. ***Inheritance*** is a mechanism that allows a new class to be based on an existing class, inheriting its attributes and behaviors. The ***derived class*** can add new functionality or ***override*** (replace) the inherited members functionality.  In doing so, the derived class becomes a more specific version of the class it inherits from. Inheritance supports ***code reuse***, facilitates ***polymorphism***, and models ***hierarchical relationships*** between classes, enabling the creation of more specialized or generalized classes from existing ones.

A simple example can be seen with what was described earlier about ***abstraction*** with a student and a driver. Recall we said a real person has a first name, last name, date of birth, address, race, gender, height, weight, hair color, eye color, etc. and if they are in college, they’ll have a major, a list of classes they have completed (transcript), an advisor, and several other pieces of information about being in college. If they are a driver, they may have restrictions on their license or endorsements.

<caption><strong>Without Inheritance</strong></caption>
<br />
<caption><strong>Figure 1: Student Class Diagram</strong></caption>

<pre class="mermaid">
classDiagram
    class Student
    Student: -String firstName
    Student: -String lastName
    Student: -Date birthDay
    Student: -Address address
    Student: -char race
    Student: -char gender
    Student: -ArrayList&lt;Course&gt; transcript
    Student: -String degree
    Student: -Professor advisor
    Student: +Student(firstName, lastName, birthDay, address, race, transcript, advisor)
    Student: +getFirstName()
    Student: +setFirstName(firstName)
    Student: +getLastName()
    Student: +setLastName(lastName)
    Student: +getBirthDay()
    Student: +getAddress()
    Student: +setAddress(address)
    Student: +getRace()
    Student: +getGender()
    Student: +setGender(gender)
    Student: +getTranscript()
    Student: +addCourseToTranscript(course)
    Student: +getDegree()
    Student: +setDegree(degree)
    Student: +getAdvisor()
    Student: +setAdvisor(advisor)
    Student: +getGPA()
</pre>

<br />
<caption><strong>Figure 2: Driver Class Diagram</strong></caption>

<pre class="mermaid">
classDiagram
    class Driver
    Driver: -String firstName
    Driver: -String lastName
    Driver: -Date birthDay
    Driver: -Address address
    Driver: -char race
    Driver: -char gender
    Driver: -int height
	Driver: -int weight
	Driver: -ArrayList&lt;Endorsement&gt; endorsements
	Driver: -ArrayList&lt;Restriction&gt; restrictions
	Driver: +Driver(firstName, lastName, birthDay, address, race, gender, height, weight)
    Driver: +getFirstName()
    Driver: +setFirstName(firstName)
    Driver: +getLastName()
    Driver: +setLastName(lastName)
    Driver: +getBirthDay()
    Driver: +getAddress()
    Driver: +setAddress(address)
    Driver: +getRace()
    Driver: +getGender()
    Driver: +setGender(gender)
	Driver: +getHeight()
	Driver: +setHeight(inches)
	Driver: +getWeight()
	Driver: +setWeight(pounds)
	Driver: +addEndorsement(endorsement)
	Driver: +removeEndorsement(endorsement)
	Driver: +getEndorsements()
	Driver: +addRestriction(restriction)
	Driver: +removeRestriction(restriction)
	Driver: +getRestrictions()
</pre>

While there are a few differences, it's obvious that there is a lot of duplication between these two classes. While it is unlikely to have an application that would need these exact objects, it shows how much duplication can sometimes exist. Creating these would require declaring several identical fields, and with each field the corresponding accessor and mutator methods, along with all validation logic for each. This works, but it is clearly inefficient.

Inheritance can solve this problem by putting all common fields into a single class and then
letting the two classes only add or change what's unique to them.

<caption><strong>With Inheritance</strong></caption>
<br />
<caption><strong>Figure 3: Person Superclass Diagram</strong></caption>

<pre class="mermaid">
classDiagram
    class Person
    Person<|-- Student
    Person<|-- Driver
    Person: -String firstName
    Person: -String lastName
    Person: -Date birthDay
    Person: -Address address
    Person: -char race
    Person: -char gender
    Person: +Person(firstName, lastName, birthDay, address, race, gender)
    Person: +getFirstName()
    Person: +setFirstName(firstName)
    Person: +getLastName()
    Person: +setLastName(lastName)
    Person: +getBirthDay()
    Person: +getAddress()
    Person: +setAddress(address)
    Person: +getRace()
    Person: +getGender()
    Person: +setGender(gender)
    class Student{
	    -ArrayList&lt;Course&gt; transcript
	    -String degree
	    -Professor advisor
	    +Student(firstName, lastName, birthDay, address, race, transcript, advisor)
	    +getTranscript()
	    +addCourseToTranscript(course)
	    +getDegree()
	    +setDegree(degree)
	    +getAdvisor()
	    +setAdvisor(advisor)
	    +getGPA()
	}
	class Driver{
		-int height
		-int weight
		-ArrayList&lt;Endorsement&gt; endorsements
		-ArrayList&lt;Restriction&gt; restrictions
		+Driver(firstName, lastName, birthDay, address, race, gender, height, weight)
		+getHeight()
		+setHeight(inches)
		+getWeight()
		+setWeight(pounds)
		+addEndorsement(endorsement)
		+removeEndorsement(endorsement)
		+getEndorsements()
		+addRestriction(restriction)
		+removeRestriction(restriction)
		+getRestrictions()		
	}
</pre>

Doing this provides a simple way to write this common code once and re-use it. These classes
are now "related" to each other through inheritance, in what is known as an "is-a" relationship. In this example, a *Student* ***is-a*** *Person*, with student specific things added, and a *Driver* ***is-a*** *Person*, with driver specific things added. The things that are shared between them were moved to a new class and that class is re-used through inheritance instead of being rewritten.

<section class="callout info">
In addition to the <i><b>is-a</b></i> relationship, there is also the <i><b>has-a</b></i> relationship, describing the components of the class. For instance, the <i>Student</i> <i><b>has-a</b></i> <i>Professor</i> who is the advisor.
</section>

The *Person* class as depicted is just like any other class, there is nothing special about it. This means under normal circumstances any class can be inherited from. The two other classes, *Student* and *Driver*, are declared with the keyword ***extends*** to create the inherited relationship, like this:

<caption><strong>Code Example: Inheriting from another class</strong></caption>

```java
public class Person
{
  ...
}
  ```

```java
public class Student extends Person
{
  ...
}
  ```

```java
public class Driver extends Person
{
  ...
}
```

With the *extends Person* on each of these class declarations, both *Student* and *Driver* get everything that was created in the *Person* class for free. Both have a *firstName* and *lastName* field, and the corresponding get/set methods, along with all the other fields and their corresponding get/set methods, along with any other methods, including the *Person* constructor.

## Initializing The Superclass
Since a subclass gets everything in the superclass for free, it is important that they initialize the state of the superclass in their own constructors. To do this, whenever a class inherits from another class the first call in any constructor of the subclass needs to be to the superclass constructor. This is done with the keyword super, like this:

<caption><strong>Code Example: Initializing the superclass</strong></caption>

```java
/**
 * A Student at the school.
 *   This inherits from Person to re-use its fields, methods, and logic.
 * @author: John Doe
 * @version: 2026.06.11.01
 */
public class Student extends Person
{
  private ArrayList&lt;Course&gt; transcript;
  private Professor advisor;

  /**
   * Student class constructor initializing with no data.
   */
  public Student()
  {
    // Calling the parent class's default constructor
    super();
    ...
  }

  /**
   * Student class constructor setting all fields using parameters.
   */
  public Student(String firstName, 
				   String lastName, 
				   Date birthDay, 
				   Address address, 
				   char race, 
				   char gender, 
				   ArrayList&lt;Course&gt; courses, 
				   Professor advisor)
	{
		// First, initialize the *Person* parts of the class
		super(firstName, lastName, birthDay, address, race, gender);
		// Then initialize the *Student* part of the class
		transcript = courses;
		this.advisor = advisor;
	}

  // Other methods
  ...
}
```

If a class inherits from another and does not call super as the first call of its own constructor, Java will implicitly call the parent class’s default constructor by adding a *super()* call as the first line when it builds the project.

## Types of Relationships

The classes that *extend* another class (known as ***subclasses*** or ***child classes***) know about the relationship, but the class being extended (known as ***superclass*** or ***parent class***) has no code to indicate the inheritance relationship and therefore no way to know about it. UML class diagrams have an arrow pointing to the parent class from the child class, which reinforces this. In Java, the class being extended (*Person* in this example) is known as the ***superclass***, and the classes inheriting from *Person* (*Student* and *Driver*) are known as ***subclasses*** of the ***superclass*** or ***child classes*** of the ***parent class***. These two terms mean the same thing.

Another example of this would be an application for playing card games. In almost all card games one of the players is also the dealer. The dealer has a deck of cards and is responsible for shuffling the deck of cards and handing out cards to all the other players. All players will receive cards from the dealer, and based on the cards they receive they'll have a score which determines the winner. The dealer also plays the game though, so the dealer is really just a regular player that also has a deck of cards and deals the cards out to other players. Inheritance is a great solution for this problem.

<caption><strong>Figure 4: A Card UML Class diagram</strong></caption>

<pre class="mermaid">
	classDiagram
		class Card
			Card: -Suit suit
			Card: -String name
			Card: -int value
			Card: -boolean visible
			Card: +Card(suit, name, value, visible)
			Card: +getSuit()
			Card: +getName()
			Card: +getValue()
			Card: +isVisible()
			Card: +show()
            Card: +hide()
</pre>

<caption><strong>Figure 5: A Player superclass and a Dealer subclass UML Class diagram</strong></caption>

<pre class="mermaid">
classDiagram
	class Player
		Player<|--Dealer
		Player: -ArrayList&lt;Card&gt; hand
		Player: -String name
		Player: -int chips
		Player: +receiveCard(card)
		Player: +setChips(value)
		Player: +getChips()
		Player: +clearHand()
		Player: +scoreHand()
		Player: +showAllCards()
		class Dealer{
				-ArrayList&lt;Card&gt; deck
				+shuffle()
				+deal()
			}	
</pre>

<section class="callout info">
Here, <i>Dealer</i> <i><b>is-a</b></i> <i>Player</i>, and <i><b>has-a</b></i> <i>Deck</i>, which itself <i><b>has-a</b></i> collection of <i>Card</i> objects.
</section>

This basic approach is used in almost all card game applications.

## Levels of Inheritance

A class can only have one direct class that it inherits from in Java. It is not possible to extend more than one class directly. This is a safety mechanism in the language. Imagine what would happen if two classes were declared as direct parent classes, and they each declared the same field but as different data types, or each declared the same method with the same signature. Which one would the subclass use in that case? Java avoids this problem altogether by only allowing one direct superclass.

Classes can have as many layers as needed in the inheritance hierarchy. This means a class can be a subclass of one, and a superclass to one or more other classes.

Consider this example:
<caption><strong>Figure 6: A UML Class diagram representing part of the hierarchy of the Animal Kingdom</strong></caption>

<pre class="mermaid">
classDiagram
    class Animal
    Animal<|-- Mammal
    Mammal<|-- Dog
    Mammal<|-- Cat
    Dog<|-- Labrador
    Dog<|-- Terrier
    Cat<|-- Tabby
    Cat<|-- Tiger
    Animal<|-- Bird
    Bird<|-- Duck
    Bird<|-- Songbird
    Duck<|-- Mallard
    Duck<|-- Canvasback
    Songbird<|-- Cardinal
    Songbird<|-- Robin
    Songbird<|-- Thrush
    Thrush<|-- Wood Thrush
    Thrush<|-- Hermit Thrush
</pre>

<section class="callout info">
While Java doesn't have a limit to the depth of a class hierarchy, the developer still needs to keep track of everything mentally. Use the level of depth that makes sense for the application, and don't go so far that you cannot keep track of what is where.
</section>

Here the animal kingdom is partially represented, and several classes are both a superclass and a subclass.

## The Object Class

Java is considered a purely ***Object-Oriented programming language***. What that means is everything in Java is an object. But what does that mean, and how is that possible?

Every class in Java, whether it comes from the SDK or is created as part of the current project, inherits directly or indirectly from the *Object* class. If a class does not use the *extends* keyword to inherit from another specific class, then Java automatically has that class extend the Object class. So, in the previous examples, the *Person*, *Player*, *Card* and *Animal* classes all implicitly inherit from *Object*.

<section class="callout info">
The <i>Object</i> class is in the <i>java.lang</i> package, which is automatically imported into every class
</section>

<caption><strong>Code Example: A class definition without the <i>extends</i> keyword</strong></caption>

```java
public class Card
{
  ...
}
```

Since this card class doesn't explicitly *extend* another class, Java treats it as though it were written like this:

<caption><strong>Code Example: A class definition with the <i>extends</i> keyword implicitly added</strong></caption>

```java
public class Card extends Object
{
  ...
}
```

What this ultimately means is every class in Java ultimately inherits from the *Object* class. Consider each of the previous examples. This means they are all in this object hierarchy:

<caption><strong>Figure 7: A UML Class diagram representing how all classes in Java ultimately inherit from the <i>Object</i> class</strong></caption>

<pre class="mermaid">
classDiagram
	class Object
		Object<|--Animal
		Object<|--Person
		Object<|--Player
		Object<|--Card
</pre>

This being the case, every object in Java inherits the *Object* class’s public methods, known as the object's ***API (Application Programming Interface)***. Many of these are useful in providing common capabilities of all objects in Java. One of the most used and most useful is the *Object* *toString()* method. Every object in Java has this (and a few others) because they are inherited from the *Object* class.

<section class="callout info">
This is why the <i>System.out.print()</i> and <i>System.out.println()</i> methods can just have an object instance passed into them as a parameter. These methods just call the <i>toString()</i> method that every object is guaranteed to have because they all ultimately inherit from the <i>Object</i> object.
</section>

# Polymorphism

The word "polymorphism" originates from the Greek roots "poly" meaning "many" and "morph" meaning "form" or "shape." When combined, "polymorphism" literally translates to "many forms." 

***Polymorphism*** in object-oriented programming (OOP) is a concept that allows objects of
subclasses to be treated as objects of their superclass. This is a direct application of the ***is-a*** relationship. With inheritance, a subclass is a more specific version of the superclass. This is because the subclass has everything in the superclass, and then adds or replaces certain things to better represent the specific subclass and its functionality.

This is also known as the ***Liskov Substitution Principle***, named after Barbara Liskov. This principle states that objects of a superclass should be replaceable with objects of a subclass without affecting the correctness of the program. In other words, if class *B* is a subclass of class *A* (*B **is-a** A*), then objects of type *A* should be substitutable with objects of type *B* without altering the correctness of the program.

Any subclass should only enhance the functionality of the superclass to be more specific. It **can not** radically change what the superclass is intending to do. Subclasses should adhere to the same public API, which means they should implement the same public methods in a way that maintains the same behavior. 

An example would be a card player object which could score the cards in the hand according to the rules of the card game. This player class could be extended to create a dealer as seen earlier, which would make the dealer a player that could also deal cards. The dealer's score hand method and other functionality would be identical.

For this to work, subclasses can not require more preconditions (requirements before a method is executed) or weaken postconditions (guarantees after a method is executed). This ensures that the subclass does not impose additional constraints or fail to meet the expectations set by the superclass. This is important for allowing subclasses to be substituted where superclass instances are required or declared.

### Invariant Preservation

The invariants (conditions that should hold true for an object during its lifetime) established by the superclass should be preserved by the subclass. This means that the subclass should not violate any rules or constraints that are true for the superclass.

One example would be the card player described earlier and its *scoreHand()* method.  According to the ***Liskov Substitution Principle***, the *Dealer* class should not change the behavior of the *scoreHand()* method because anywhere a *Player* instance is used, the behavior of that method should remain the same.

### Static and Dynamic Types

Consider this basic example using a class hierarchy of birds:

<caption><strong>Code Example: A *Bird* parent class and two subclasses, *Sparrow* and *Penguin*</strong></caption>

```java
class Bird 
{
	public String fly() 
	{
        return "flies in the sky";
    }
}
```

```java
class Sparrow extends Bird 
{
  // This override of the fly method adds to the parent class's implementation
  @Override
  public String fly() 
  {
      return "Sparrow " + super.fly();
  }
}
```

```java
class Penguin extends Bird 
{
  // This override of the fly method replaces the parent class's implementation
  @Override
  public String fly() 
  {
      return "Penguins can't fly";
  }
}
```

Consider the following declarations:

<caption><strong>Code Example: Declaring several objects and initializing them with the same class's constructor or the subclass constructor.</strong></caption>

```java
Bird bird = new Bird();

Sparrow sparrow = new Sparrow();

Penguin penguin = new Penguin();

Bird bird1 = new Sparrow();

Bird bird2 = new Penguin();
```

The *bird* object is declared as the type *Bird*, and the *Bird* constructor is used to build the instance of the *Bird*. Everything matches, and there's no question it's an instance of a *Bird*. The same is true for the *sparrow* and *penguin* objects.

The *bird1* and *bird2* declarations don't look like they match though. The instance type is *Bird* but the constructor being called is *Sparrow()* and *Penguin()*. Will this work?

This will work because both *Sparrow* and *Penguin* inherit from *Bird*, so they are just more specific Bird classes. 

What will happen here though:

<caption><strong>Code Example: Assigning one subclass object instance to an instance variable of a different subclass type.</strong></caption>

```java
sparrow = penguin;
```

This will not work, because while both the sparrow and penguin object are birds, a sparrow is not a penguin. A sparrow doesn't know how to be a penguin and vice versa.

Take a look at what would happen if the Sparrow and Penguin are assigned to instances of Bird:

<caption><strong>Code Example: Substituting subclass instances for their parent class</strong></caption>

```java
public class Main 
{
  // Thanks to polymorphism and the Liskov Substitution Principle, this method can
  // take an instance of Bird as a parameter, or an instance of any Bird subclass
    public static void makeBirdFly(Bird bird) 
    {
        System.out.println(bird.fly());
    }

    public static void main(String[] args) 
    {
        Bird sparrow = new Sparrow();
        Bird penguin = new Penguin();

        makeBirdFly(sparrow);  // Output: Sparrow flies in the sky
        makeBirdFly(penguin);  // Output: Penguins can't fly
    }
}
```

This code would compile and run without any errors.
<caption><strong>Console Output:</strong></caption>

```console
Sparrow flies in the sky
Penguins can't fly
```

Another example of polymorphism at work would be the card game's *Player* and *Dealer*.  Since the *Dealer* ***is-a*** *Player*, an instance of the *Dealer* can be assigned to any *Player* variable.

<caption><strong>Code Example: A <i>Dealer</i> subclass meets all the requirements to be a <i>Player</i></strong></caption>

```java
public class Player
{
	...
}
```

```java
public class Dealer extends Player
{
	...
}
```

```java
public class Main 
{
  public static void main(String[] args) 
  {
    // Any object that "is-a" Player can be added to the players list
    ArrayList&lt;Player&gt; players = new ArrayList&lt;&gt;();
    
    Player player = new Player();
    Dealer dealer = new Dealer();

    // This works because the dealer "is-a" Player thanks to polymorphism
    players.add(player);
    players.add(dealer);
  }
}
```

# Inheritance and the DRY Principle

One of the biggest “evils” in software development in any language is writing the same code more than once. Avoiding this is known as ***the DRY principle***, which stands for Don’t Repeat Yourself. This is closely related to the concept of ***normalization*** in database design, which seeks to eliminate data redundancy.

The DRY principle in practice aims to reduce redundancy and duplication of code by promoting the reuse of existing code and logic. One simple example of this can be seen with this *BankAccount* class. The constructor takes a parameter of an initial balance and uses the *deposit()* method, which includes business rule validation logic, to set the initial state of the object.

<caption><strong>Code Example: A <i>BankAccount</i> class that passes the <i>initialAmount</i> to the deposit method in the constructor thereby re-using the validation code in <i>deposit()</i></strong></caption>

```java
/**
 * A class representing a bank account that holds a customer's money.
 * @author Jane Q. Public
 * @version 2026.06.11.01
 */
public class BankAccount
{
  private double balance; 

  /**
   * Constructor that initializes the account with the provided balance.
   */
  public BankAccount(double initialBalance)
  {
    deposit(initialBalance);
  }

  /**
   * @return double The current balance of the account.
   */
  public double getBalance()
  {
    // Rounds the balance to 2 digits of significance (dollars and cents)
    return Math.round(balance * 100.0) / 100.0;
  }

  /**
   * Add money to the account.
   *   The amount must be a positive value.
   * @throws Exception - Thrown if the amount is not a postivie value
   */
  public void deposit(double amount)
  {
    if (amount > 0.0)
    {
      balance += amount;
    }
    else
    {
      throw new Exception("Invalid value, amount must be positive");
    }
  }

  /**
   * Take money out of the account.
   *   The amount must not be more than has been deposited.
   * @throws Exception - Thrown if the amount requested is more than has been deposited
   */
  public void withdraw(double amount)
  {
    if (balance >= amount)
    {
      balance -= amount;
    }
    else
    {
      throw new Exception("Insufficient funds");
    }
  }
}
```

The key aspects of the DRY principle are:
- Avoid code duplication: Instead of repeating the same code in multiple places, extract it into a reusable function, module, or component.
- Single source of truth: Each piece of knowledge or logic should have a single, authoritative representation in the codebase. This is where the parallel to database normalization comes from.
- Modular and reusable code: By following DRY, code becomes more modular, reusable, and
easier to maintain.

Following the DRY principle has several advantages:
- Maintainability: If a change is required, it only needs to be made in one place, reducing the risk of introducing intermitent bugs.
- Readability: DRY code is often more readable because it avoids redundancy and promotes
abstraction.
- Reusability: By extracting common logic into reusable components, code can be shared
across multiple parts of the application.
- Consistency: With a single source of truth, the behavior and output of a particular logic
remain consistent throughout the codebase.

The DRY principle promotes code reuse, maintainability, and consistency by eliminating redundancy, while the WET principle represents the opposite approach of duplicating code. DRY is generally considered a best practice.

## Inheritance and Avoiding Duplication

Inheritance can be another great way to apply the DRY principle.  If this *BankAccount* class was then used as the parent class of a new *CheckingAccount* and *SavingsAccount* class, they both could "reuse" this validation logic as well by using the *deposit()* method they inherited from the *BankAccount* class.

# Casting

Earlier the ***is-a*** relationship was described. This is a way of describing that a class inherits from a superclass. Essentially, any subclass is a version of the superclass. This is true because any subclass has everything needed to be an instance of the superclass type, it just has something extra that makes it more specific.

<caption><strong>Code Example: A Vehicle object v is assigned a new Car instance</strong></caption>

```java
  Vehicle v = new Car();
```

This assumes *Car* inherits from *Vehicle*, so it *is-a* vehicle, with extra car specific things added. Where are those car specific things though? The car constructor would set up the state of the object to initialize those extra things, but since vehicle doesn't know about the car specific things, they are hidden in the object instance v.

<section class="callout info">
	
***Casting*** in Java is a way to convert or treat an object of one type as another related type as long as they are in the same object hierarchy. It is closely tied to the concept of polymorphism.
</section>

## Upcasting

Upcasting is implicitly done by the compiler when you assign a subclass object to a superclass reference variable, such as ```Vehicle v = new Car();``` Whenever the parent class is used as the ***static data type*** (the type the variable is declared as, such as *Vehicle*) and a child class is used as the ***dynamic data type*** (the type the object *actually* is, such as *Car*), it is an example of upcasting. This is a perfect example of The Liskov Substitution Principle at work.

<section class="callout info">
  
- The term ***static*** in this context refers to object type checking done by the java compiler when it builds the application, converting the *.java* files into the *.class* files that the **Java Runtime Environment (JRE)** can execute. This is known as static because the compiler will read the source code every time in the same exact way. Thus, static data types are what the compiler is validating are compatible.
  - To work, static data types must be at the same level or higher in the same object hierarchy.
- The term ***dynamic*** in this context refers to the actual object type when the application is executing, which is called the runtime.  It is known as dynamic because the application can change what it is doing based on its inputs or environment while it is executing.
  - To work, dynamic data types must be at the same level or lower in the same object hierarchy.
</section>

Upcasting is always safe because the subclass object has all the methods and fields of the superclass. If the parts that make a Car object are there but hidden, then they cannot be used. To use the Car specific functionality of the object v, these hidden things need to be unhidden. It is possible to do this with a process known as Downcasting, or more often just called Casting.

## Downcasting

When you have a reference variable of a superclass type pointing to an object of a subclass, you can use casting to treat that object as an instance of the subclass. This allows you to access the subclass-specific methods and fields. This is also known as Downcasting and is most often what is meant by the term Casting.

- Downcasting is the opposite of upcasting, where you treat a superclass object as an instance of a subclass.
- Downcasting requires an explicit cast because the compiler cannot guarantee that the
object being cast is indeed an instance of the subclass.
  - Example of downcasting with an explicit cast: ```Car c = (Car) v;```
  - This unhides the *Car* specific things that the *Car()* constructor built when the variable *v* was initialized, and returns this.  It doesn't actually change the variable *v*, so what the casting operation returns is assigned to a new variable, *c*.
- Downcasting is only safe if the object being cast is actually an instance of the target subclass.
  - Remember, super classes know nothing about their potential subclasses.
- Downcasting is unsafe if the object is not actually the target subclass type.  If this is attempted, the JRE will throw a *ClassCastException* at runtime.

### Checking before downcasting

To avoid getting a *ClassCastException* thrown, first check if the object being cast is an instance of the target subclass using the instanceof operator.

<caption><strong>Code Example: Validating the dynamic type before downcasting</strong></caption>

```java
if (v instanceof Car) 
{
    Car c = (Car) v; // Safe downcast
    
    // Access Child-specific methods and fields using the c variable
}
```

Putting the actual dynamic class type in parentheses in front of the instance variable will unhide the subclass specific elements and return an object reference. By assigning that to a new instance variable of the specific type, all of the subclass public API is now exposed and available.

Without this instanceof check, it would be possible for the application to try converting an object into another type that was incompatible. Imagine this situation:

<caption><strong>Code Example: An invalid downcasting operation</strong></caption>

```java
Animal a = new Dog();
Car c = (Car) a;
```

Clearly, a dog is not a car in the real world, and an object hierarchy would not exist between a Dog or Animal and a Car class. Because a Car is not a Dog or Animal, this code would fail by throwing an exception if it was tried. Checking before trying to do the cast can prevent this error and is a best practice.

Casting is an essential part of polymorphism in Java. It allows you to write more generic code that works with superclass references while still being able to access subclass-specific behavior when needed. Downcasting should always be used with caution and always preceded by an instanceof check to ensure type safety.

# Object Reference

In Java, an ***object reference*** is a variable that stores the *memory address* of an object instance. It acts as a ***reference*** or ***pointer*** to the actual object stored in memory. When you create an object using the *new* keyword, the JRE asks the operating system for a chunk of memory big enough to hold an instance of the class.  The operating system searches through its memory, known as the ***heap***, and when it finds a chunk big enough, it reserves that chunk of memory and returns its starting address to the JRE.  The JRE then puts that starting memory address in as the object variable's actual under the hood value.  Thanks to the class definition the JRE knows how to find everything inside the object instance by calculating its memory address offset (how far away it is) from the starting memory address.

<section class="callout info">

  Inside any class, Java also provides the keyword ***this*** as an object to access the instance of a class in the code. The *this* variable is a reference inside the class to the instance itself.
</section>
<br />
<caption><strong>Code Example: Using the <i>this</i> object reference</strong></caption>

```java
/**
 * A very simple Car object.
 * @author Jane Q. Public
 * @version 2026.06.11
 */
public class Car
{
  private String make;
  private String model;
  private int year;

  /**
   * Constructor initializing the car make, model, and year it was manufactured.
   */
  public Car(String make, String model, int year)
  {
    // Here, the make, model, and year variables are parameters.
    // To set the object instance's fields, the names 
    //     have to be differentiated using the this object reference.
    this.make = make;
    this.model = model;
    this.year = year;
  }
}
```

Because the constructor parameters have a smaller scope (method-level) than the class fields (class-level), the variables passed in as parameters take precedence.  In order to tell Java to use the class fields inside this method that have the same name, they need to be accessed from the *this* object reference.

<caption><strong>Code Example: Creating an instance variable, then initializing it</strong></caption>

```java
// There is no object reference yet, so myCar has the value null
Car myCar; 

// Now myCar actually references an object instance
myCar = new Car("Toyota", "Camry", 2022); 
```

On the first line, where *myCar* is declared, its initial default value is null. ***Null*** means the absence of a value. On the second line, the *myCar* variable is assigned to what is returned by the *Car* constructor, thanks to the *new* keyword. The *new* keyword tells the Java runtime to go to the operating system and ask for a block of memory big enough to hold a *Car* object. The operating system returns the starting address of a block of memory that size from its available, unused memory (known as the ***heap***), and Java builds an instance of a *Car* object in that block of memory by declaring all the variables and setting up the initial object state by running one of the object’s constructor methods. The *myCar* instance variable then gets the address of that memory assigned to it as its "under the hood" value. So the value *null* is actually the absence of a memory address in this situation.

<section class="callout info">

The ***heap*** is a region of memory used for dynamic (as needed) memory allocation. It is a shared memory area where objects are allocated at runtime. There is no way to predict where in the heap an object may be created, and it will almost certainly not be at the same memory address when the program is ran at a different time.  
</section>

The memory address stored in a variable's underlying value can be changed, either by reassigning the value to null or by assigning the same variable to a different object.

<caption><strong>Code Example: Creating and assigning an instance variable with the new keyword</strong></caption>

```java
// myCar references the memory address where Java created the 2024 Toyota Camry instance
Car myCar = new Car("Toyota", "Camry", 2024)
```

Object instance variables just hold this memory address as their "under the hood" value. This is why they are called references, they reference the location in memory where the object instance is stored. The same object instance in memory can have more than one instance variable pointed at it.

<caption><strong>Code Example: Showing that two object variables can "reference" the same actual object in memory.</strong></caption>

```java
// Here, otherCar references the same memory address as myCar.  
Car otherCar = myCar;
// The two variable names, myCar and otherCar, actually point to the same object instance in memory. This is not a copy, it is the same actual object.

// Changing one will be reflected in the other.
myCar.openHood(); // hood is now open in the one object in memory
otherCar.isHoodOpen(); // Returns true, because it was opened using the myCar reference
```

# Overrides

Sometimes the methods inherited from a parent class are inadequate for the child class' needs.  When this happens, a subclass can replace the parent class' implementation of a method by overriding it.

<section class="callout info">
Overrides vs. Overloads

- Overriding a method involves writing a method with the exact same signature of a method from
the superclass in a subclass.
  - This replaces the superclass' method implementation with the subclass' implementation and is what will run when any other class calls that method on the instance variable.
- Overloading a method involves writing a method with the same visibility, return type, and name, but with different parameters.
</section>

Creating an ***override*** on a method is simple. If the subclass has a method with the same signature as the parent class, the subclass' method overrides, or replaces the parent class implementation. This should also have the annotation ***@Override*** directly above the method signature, like this:

<caption><strong>Code Example: The @Override annotation on a toString() method</strong></caption>

```java
public class Car
{
  ...
  @Override
  public String toString()
  {
    return year + " " + make + " " + model;
  }
}
```

In this example the *toString()* method that was inherited from *Object* is replaced with this specific implementation that can now generate a string representing the state of this Car object instance.

***Overloading*** on the other hand involves creating a method with the same return type and name, but with a different parameter list. This is often done with class constructors, although it can be done with any method. Due to the different parameters, these have a different signature and are considered separate methods. It does not matter if the methods are in the same class or a subclass.  Overloaded methods do not have an annotation.

This is an important distinction because overloaded methods can all be accessed and executed from anywhere by simply providing the correct set of parameters for the version needed. In contrast, an overridden method is hidden from any other class except the superclass and subclass. The subclass can still access the superclass' method by using the ***super*** reference to the parent and calling the method from it (```super.methodName()```), but only the subclass can do this.

When overriding methods, the access modifier in the subclass cannot be more restrictive than in the superclass. It can be made less restrictive. For example, a *protected* method in the superclass can be overridden as *public* in the subclass, but it could not be overridden as private.

## Visibility

A key part of Java's encapsulation involves the access modifiers used when declaring classes, fields, and methods. These define what the scope, or "visibility" of the class, field, or method is. Java supports four levels of visibility: *public*, *protected*, *default*, and *private*.

***Public*** members are accessible from anywhere in the program and can be accessed by any other class, regardless of package. Public members of a superclass are fully inherited by subclasses and remain public in the subclass. Public access is used for API methods and classes that need to be widely available to other classes. It is also used for fields which are constant and utility methods meant for general use, such as the Collections.shuffle or Collections.sort methods. Public is also the visibility of classes that define core functionality, such as ArrayList, HashSet, or HashMap.

***Protected*** members are accessible within the same package and by subclasses, even if those subclasses are in different packages. Protected members of a superclass are inherited by subclasses and remain protected in the subclass. Protected is used for methods or variables that should be available to child classes, especially if there are implementation details that may need to be overridden or accessed by subclasses. This level allows controlled access to superclass members in inheritance hierarchies.

A ***package*** is a logical organization of related classes into a ***namespace***. Think of a package like a neighborhood of related objects.  Objects in the same package do not need an import statement to see each other, but that also means class names within a package must be unique.  Part of the advantage of packages is so different teams and companies do not need to worry about having completely unique names across the entire Java ecosystem.  In this way, packages help organize code, grouping related components and preventing naming conflicts. Packages use folders to organize the code, along with the declaration at the top of the class file of the package name.  The subfolders are indicated with a period, as seen in the following code example, which means the class is in a folder named *util*, under the folder named *java*: 

<caption><strong>Code Example: A package declaration at the top of a class file</strong></caption>

```java 
package java.util;

public class ArrayList&lt;T&gt;
{
  ...
}
```

<section class="callout info">

It has become standard practice for an organization to use their internet domain name in reverse order as their organization's package prefix.  For instance, Java packages from Google would be named like this: ```com.google.gson``` for the *gson* package namespace, and it would be in a folder structure if they used IntelliJ that would look like this:

- src/
  - com/
    - google/
      - gson/
        - *gson.java* and other related java files
</section>

Packages also help control access to classes and their members. This is achieved by putting related classes into their own folders. To use classes in a different package, an import statement is required.  

***Default*** visibility, also known as ***package-private***, allows access only within the same package. Default members of a superclass are inherited by subclasses in the same package, but are ***not*** accessible to subclasses in different packages. 

This is the default when no access modifier is specified. It's used for classes that should only be used within a package, or helper methods/variables shared between related classes in a package. This is useful for limiting access to package-specific functionality.

***Private*** members are only accessible within the declaring class itself. Private members of a superclass are not directly accessible in the subclass. While they are technically inherited, they cannot be directly accessed or used in the subclass. Private is the most restrictive visibility and is used for internal implementation details that should be hidden from other classes. Private visibility is the main mechanism for enforcing encapsulation by hiding implementation details. Methods that are marked private can only be used internally by the class itself.

Subclasses can expand the visibility of inherited members but cannot reduce it. For example, if a subclass inherits a protected method, it could override that method and declare it as public. It could not however override that method and declare it as private. This ensures that the subclass maintains the "contract" established by the superclass API.

These visibility modifiers help enforce encapsulation and information hiding. They allow control over which parts of the code are exposed to other parts of the program. This can improve maintainability and reduce coupling between components, but also must be carefully considered when using inheritance. Access modifiers allow you to control which parts of a superclass are exposed to subclasses, other packages, and other classes in general. Controlling this visibility helps maintain encapsulation while still allowing for inheritance. By carefully choosing access modifiers, it is possible to control the level of encapsulation and the inheritance behavior of classes, ensuring that subclasses have
appropriate access to superclass members while maintaining the integrity of the superclass design.

## Dynamic Method Lookup

When a method of a superclass is overridden in a subclass, there are now two methods with the same signature in the class hierarchy.

<caption><strong>Figure: UML Inheritance Class diagram showing a method override</strong></caption>

<pre class="mermaid">
classDiagram
	class Object
		Object<|--Car
		Object: +toString()
		class Car{
				+toString()
			}
</pre>

Take the aforementioned *toString()* method as an example. If an object instance were declared like this:

```java
Object car = new Car();
System.out.println(car.toString());
```

Which version of the toString() method would run, the one in Car or the one in Object? Basically, the method lookup process is a bottom-up approach in terms of the inheritance hierarchy. 

First, the variable is accessed (car in the above example). The object instance stored in the variable is found in memory. Once the instance is found, then the class used to create that instance is found (Car in this example). The class is then searched for a method matching the signature. If found, that method is executed. If no match is found, the superclass (Object in this example) is searched.

This process is repeated until a match is found, or the class hierarchy is exhausted. This is why overriding methods take precedence – they override, or replace, inherited copies by being accessed earlier in the lookup process.

This lookup process has a lot to do with why Java does not allow multiple inheritance of superclasses. If two direct parents defined the same method and the subclass did not override it, Java would have no way of knowing which one to run.

## Overriding Object Methods

Several methods are present in all Java objects because they are defined in the Object object. This allows Java and java developers to have a common API for certain object functionality, which can be very powerful.

### Class Information

The Object object has two methods that are used to provide information about an instance of an object. One is the toString method, which simply returns a string that can represent the object instance. This is the most commonly overridden method from Object. Developers typically create a string in this method reporting on the state of the object and return it.
Consider the previously discussed Car object, which had a make, model, and year field:

<caption><strong>Code Example: A package declaration at the top of a class file</strong></caption>

```java 
public class Car
{
  ...

  @Override
  public String toString()
  {
    return "A " + year + " " + make + " " + model;
  }
}

```

Consider a new instance that is declared like this:

<caption><strong>Code Example: The toString() method is used any time a String representation of the object is needed</strong></caption>

```java 
Car c = new Car("Toyota", "Camry", 2022);
System.out.println(c.toString()); // Would print A 2022 Toyota Camry
```

Since litteraly every single class in Java ultimately inherits from *Object*, and *Object* is where the *toString()* method is first declared, the above code can be simplified to this:

<caption><strong>Code Example: The toString() method is implicitly used by the System.out.println() method</strong></caption>

```java 
Car c = new Car("Toyota", "Camry", 2022);
System.out.println(c); // Also prints A 2022 Toyota Camry
```

The *toString()* method is implicitly called wherever Java needs a string representation of the object instance. Thanks to inheritance, this and a few other methods are guaranteed to be present in every object.

Everything in the Java ecosystem can get the string representation of any object instance by using the *toString()* method. Since the *Object* class could never know what fields this specific class would have or what a string representing this object's state should be, replacing the *toString()* method with an override version unique to this class makes sense. Using a known method name that every object shares gives the best of both worlds.

#### More efficient Strings 

In the above example, the string representing the state of the Car class was built using concatenation by doing this: ``` "A " + year + " " + make + " " + model ```

This approach is very common in a lot of code, but it isn't exactly doing what it looks like. It looks like the letter *A* followed by a space is then getting the variable make's value, then is getting a space added to it, then the value of the model variable is getting added, then a space, then the year. What is actually happening with each ***+*** operator is a new string object instance is being built under the hood

*String* objects are stored as a private array of char primitives. Since arrays are a fixed size, it is not possible to resize a string. This is a lot of why *String* objects are immutable (read-only). The above code is easy and intuitive to write, but it is somewhat expensive to execute. 

A better approach is to use the *StringBuilder* object. The *StringBuilder* object has an *append()* method, with several overloads allowing different types of data to be added. *StringBuilder* uses a list that can dynamically grow to store and add to what's previously been appended, so instead of creating a new *String* object each time it actually does append each piece of new data. Once all the data is added to the *StringBuilder* instance, the *String* object is available through its overridden *toString()* method.

<caption><strong>Code Example: Using StringBuilder to append values,then get a String result.</strong></caption>

```java 
public class Car
{
  ...
  @Override
  public String toString()
  {
    StringBuilder sb = new StringBuilder();
    sb.append("A ");
    sb.append(make);
    sb.append(" ");
    sb.append(model);
    sb.append(" ");
    sb.append(year);
    return sb.toString();
  }
}
```

# Comparing Objects

One very common task in developing applications is to compare two different object instances. This can be more challenging than it might first appear. Java does provide a couple of standard methods to help do this between objects, in the *equals()* and *hashCode()* methods inherited from *Object*.

## The *equals()* method

Object equality refers to the concept of comparing two objects to determine if they are the same object. This can mean different things though, because there are two ways to think of "the same object."

### Reference Equality

In the example code of the previous section where object references were introduced, the references for *myCar* and *otherCar* both referenced the same memory address. There was only one object instance. Any change to the state of *myCar* also showed up in *otherCar* because they are the same instance and are therefore considered ***equal***. This is an example of ***reference equality***, meaning the two object variables point to the same address in memory under the hood.  Reference equality is tested using the ***==*** operator.

<caption><strong>Code Example: Reference equality</strong></caption>

```java
Car c1 = new Car("Toyota", "Camry", 2024);
Car c2 = c1; // Now both c1 and c2 point to, or reference, the same object in memory

c1 == c2; // True, these two object variables point to the same object instance in memory
c2 = new Car("Toyota", "Camry", 2024);

// The new operator creates a different instance at a different location in memory
c1 == c2; // Returns false, otherCar now points to a different memory address
```

### State Equality

The other way two objects can be considered equal involves the *state* of the two objects.  Recall that the ***state of an object*** is the current value of all of the fields.  Assuming two objects are the same type (instances of the same class), if the two different objects have the same state, then they may also be considered *equal*. 

In the example above using the *Car* object, the constructor initializes three fields, the *make*, the *model*, and the *year* of the car. Assuming those are the only three fields of this object, comparing those three values in two different instances would be used to see if the state of two instances was the same. If all three values were the same, then the two different instances would be considered equal.

Another basic example of this can be seen in playing cards. Assuming there are two decks of cards, each deck will hold 52 individual cards with different combinations of suit and rank. Is the *Ace of Spades* from one deck the same as the *Ace of Spades* from the second deck? Both are the *Ace of Spades*, so while they are two different physical cards, they would likely also be considered equal because they are both an *Ace of Spades*.

The *Object* object includes several methods related to this functionality that through inheritance are available on all Java objects. One of which is the *.equals(Object object)* method. It is common to override this method when creating any new class. This method follows the same basic ***algorithm*** no matter what the class is:

- Check for reference equality.
  - If they point to the same memory address, they are the same instance, so they are equal, return *true*
- Check if the parameter object is the same class type as the current class.
  - If not, they cannot be equal because they are not the same type, return *false*
- If they are the same type, cast the object as the actual class type, and then compare each field one by one
  - If each of the fields have the same value, return *true* because they have the same state
  - If not, return *false*

<section class="callout info">
Primitive fields are compared with the ***==*** to test the value stored in the field, while fields that are other objects are compared using that object's *equals()* method
</section>

<caption><strong>Code Example: The *equals()* method</strong></caption>

```java
public class Car
{
	...
	@Override
	public boolean equals(Object object)
	{
		// Testing reference equality
		if (this == object)
		{
			return true;
		}
		// Testing type equality
		else if (!(object instanceof Car))
		{
			return false;
		}
		// The parameter is a Car, testing state equality
		Car c = (Car) object;
		
		// model and make are String objects, so here the String .equals() method is used
		return this.model.equals(c.getModel()) &&
				this.make.equals(c.getMake()) &&
				 this.year == c.getYear(); // Year is an integer, so == is used
	}
}
``` 

<section class="callout info">
Notice the <i>make</i> and <i>model</i> fields are compared using the <i>String</i> object's <i>equals()</i> method.
</section>

New developers will often make the parameter type for the *equals()* method the same as the class it is being written in. On an intuitive level, this makes sense: if this is a *Car* class, we want to compare it to other cars. The original *equals()* method is in the *Object* class though, and the method signature has an *Object* parameter, not a more specific class like *Car*.  

If the parameter was defined as a *Car* object, what would happen if someone tried to pass an instance of a *Dog* class?  The method signature would not match because *Car* and *Dog* wouldn't be in the same object inheritance hierarchy, and the *equals()* call would fall back to what is defined in the *Object* class due to the method lookup process discussed earlier.  Needless to say, the *Object* class knows nothing about our *Car* or *Dog*, so the comparison would not be reliable.

Through the ***is-a*** relationship, this will still technically work, but it also limits the code in another way. Why on earth would anyone try to compare a Dog class to a Car? While this does not make sense on the surface, things like this can happen, especially when different teams are using classes to develop an application without good documentation or collaboration. Using *Object* as the parameter and doing the *instanceof* check ensures the code will continue to function even if something like this happens. Overall, using Object is more robust and therefore considered a higher quality approach.

#### Comparing primitive fields

Comparing primitives is done by using the **==** comparison operator, because primitives will simply compare the value stored in each field. There *is* one exception to this though, which is comparing non-integer numbers stored as floats and doubles. Both floats and doubles have precision issues in most programming languages due to how floating-point numbers are stored in memory. In other words, ***these numbers aren't guaranteed to be exact***. The way these numbers are stored is described in the ***IEEE 754*** standard.

It may seem odd that a computer cannot store a number precisely, but there are a few reasons why. Floating-point numbers are stored in binary, which can't exactly represent many decimal fractions. For instance, 0.1 in binary is an infinitely repeating fraction, and there are an infinite number of digits to the right of the decimal place in π. Floats use 32 bits and doubles use 64 bits to represent numbers. This finite storage means they can't represent all real numbers exactly. Different operations on floating-point numbers often introduce ***small rounding errors*** due to the limitations of storage size and binary binary representation.

<caption><strong>Code Example: Comparing real numbers</strong></caption>

```java
private static void doubleComparison() 
{
	double d1 = 0.0;
	double d2 = 0.0;
	
	// Adding .1 11 times
	for (int i = 1; i <= 11; i++) 
	{
		d1 += .1;
	}

	// Multiplying .1 by 11
	double d2 = .1 * 11;

	System.out.println("d1 = " + d1);
	System.out.println("d2 = " + d2);

	if (d1 == d2)
		System.out.println("d1 and d2 are equal\n");
	else
		System.out.println("d1 and d2 are not equal\n");
}
```

This program will generate the following output, even though they should be the same:

<caption><strong>Console Output:</strong></caption>

```console
d1 = 1.0999999999999999
d2 = 1.1
d1 and d2 are not equal
```

<section class="callout info">
This is why it is a very bad idea to use a double or a float to represent money in an application.
</section>

There are a few ways this can be handled. The easiest and most common way is to choose a ***threshold of precision***. If the difference between the two numbers is less than this threshold, that difference is ignored as a rounding error and the numbers are considered equal.

<caption><strong>Code Example: Threshold of precision</strong></caption>

```java
double a = 0.1 + 0.2;
double b = 0.3;
boolean equal = (Math.abs(a - b) < 0.0001);
```

In this example, if the difference is less than 0.0001, they will be considered equal.

Another approach to this problem is to leverage the wrapper class’s *compare()* method. Both the *Float* and *Double* wrapper classes implement this method, and handle special cases like NaN (***Not a Number***) error and positive/negative zero correctly. The *compare()* method is a static method used to compare two values, and returns an int value of the result. The *compare()* method will return 0 if both the parameter values are numerically equal to each other. It will return a positive value if the first parameter is numerically greater than the second parameter. In contrast, the method will return a negative value if the first parameter is numerically less than the second parameter.

<caption><strong>Code Example: Using a wrapper class for comparison</strong></caption>

```java
double a = 0.1 + 0.2;
double b = 0.3;

int result = Double.compare(a, b);

if (result == 0) 
{
    System.out.println("a and b are equal");
} 
else if (result < 0) 
{
    System.out.println("a is less than b");
} 
else 
{
    System.out.println("a is greater than b");
}
``` 

<section class="callout info">
This can be useful when you need to determine the ordering of values for sorting, not just equality.  Using it this way will be covered in the chapter introducing <b>interfaces</b>.
</section>

A third approach is to use the built in Java object *BigDecimal*. Using this object type is recommended for precise decimal calculations.

<caption><strong>Code Example: Using BigDecimal for comparison</strong></caption>

```java
BigDecimal a = new BigDecimal("0.1");
BigDecimal b = new BigDecimal("0.2");
BigDecimal c = a.add(b);
BigDecimal d = new BigDecimal("0.3");

if (c.compareTo(d) == 0) {
    System.out.println("c and d are equal");
}
``` 

*BigDecimal* allows you to specify rounding modes and precision, making it suitable for financial calculations or other scenarios requiring exact decimal representation.

Money should not be stored as a float or double field due to this imprecision. For precise values, money is often stored as an int representing cents and dollars are derived from that by dividing by 100. Alternatively, money can be stored as a BigDecimal instance.

<section class="callout info">
Always avoid direct equality comparisons with the == operator for floats and doubles to ensure reliable results in your applications.
</section>

## The *hashCode()* method

Another method that is inherited from *Object* is *hashCode()*. The *hashCode()* method calculates an integer value that provides a quick representation of the state of an object's instance. All fields used in an *equals()* method should be used when calculating a hashCode result, and vice versa. 

Any object instance with the same state will always return the same integer value for a *hashCode()* method call. Two objects with a different state however are ***not guaranteed*** to calculate a different value (called a ***collision***). This provides a shortcut for comparing and retrieving objects in hash-based collections like *HashMap*, *HashSet*, or *HashTable*.

### The hashCode-equals Contract

If two objects are equal according to the equals() method, they must have the same hash code.  Two unequal objects ***may have the same hash code*** (collision), but this should be minimized for performance reasons. If you override *equals()*, you ***must*** also override *hashCode()* to maintain this contract.

#### Implementing *hashCode()*

In the book *Effective Java*, author Joshua Bloch provided a good general algorithm for calculating a hashcode. Consider the *Car* class used earlier, which has a make, model, and year field:

<caption><strong>Code Example: Implementing *hashCode()*</strong></caption>

```java
public class Car
{
	...
	@Override
	public boolean equals(Object object)
	{
		...
	}
	
	@Override
	public int hashCode()
	{
		int result = 17;
		result = 37 * result + make.hashCode();
		result = 37 * result + model.hashCode();
		result = 37 * result + year;
		return result;
	}
}
``` 

The basic * ***hashCode()*** **algorithm** is this:
- A *result* variable is seeded with the value *17* (a prime number)
- For each field, the result is multiplied by 37 (also a prime number) and
  - For primitive field types, the value is added to the primitive variable's integer equivalent value
  - For objects, the return of that object's *hashCode()* method

Alternatively, if the class was a subclass, the superclass hashCode could be incorporated like this:

<caption><strong>Code Example: Using <i>super.hashCode()</i></strong></caption>

```java
public class Car
{
	...
	@Override
	public boolean equals(Object object)
	{
		...
	}
	
	@Override
	public int hashCode()
	{
		int result = 17;
        result = 37 * result + super.hashCode();
        // Now the new subclass fields get the regular hashCode calculation
	}
}
```

# Advanced Topics

## The *Class* class

The *Class* class in Java is a built-in object type that represents the runtime representation of a class or interface in Java. This is what is checked by the *instanceof* operator. It provides information about the class or interface, such as its name, fields, methods, constructors, and modifiers. It is used most often for reflection in Java. ***Reflection*** is a feature that allows a program to inspect and manipulate the class without explicitly knowing its type when the application is running.

Here are some key points about the Class class:
- Obtaining a *Class* Object by:
  - Using the *.class* syntax:
    - Example: *String.class* returns the *Class* object instance for the String class.
      - This is declared in the Object class, so all Java classes have this.
  - Using the *Class.forName()* method:
    - Example: *Class.forName("java.lang.String")* returns the *Class* object for the *String* class.
  - Using the *getClass()* method on an object instance:
    - *"Hello".getClass()* returns the *Class* object for the *String* class because "Hello" is a String literal.
- Checking Class Relationships: The Class class provides methods to check the relationships
between classes, such as:
  - *isInstance(Object obj)*: Returns true if the specified object is an instance of the class or interface represented by the *Class* object.
  - *isAssignableFrom(Class<?> cls)*: Returns true if instances of the specified class can
be assigned to instances of the class represented by the Class object.
  - *isInterface()*: Returns true if the *Class* object represents an interface.
  - *isArray()*: Returns true if the *Class* object represents an array class.
- The *Class* class is an essential part of the Java language and is used extensively in various frameworks, libraries, and applications that rely on reflection, dynamic class loading, and runtime class discovery or manipulation.

## Sealed classes

A sealed class in Java is a class that explicitly specifies which other classes are allowed to extend it. This feature was introduced in Java 17 to provide better control and predictability over class hierarchies.

A sealed class is declared using the sealed keyword, followed by the permits clause that lists the classes allowed to extend it.

<caption><strong>Code Example: Sealed class declaration</strong></caption>

```java
public sealed class Animal permits Dog, Cat, Bird
{  
	// class implementation  
}
```

Sealed classes offer several benefits:
1. Controlled Extensibility: By explicitly specifying permitted subclasses, it is possible to have fine-grained control over the class hierarchy, reducing the risk of unintended extensions and preserving code integrity.
2. Improved Readability: Sealed classes enhance code readability by clearly indicating which
subclasses are allowed, making the intended structure of the hierarchy more apparent.
3. Early Error Detection: Attempts to create unauthorized subclasses are caught at build time, preventing runtime errors.
4. Refactoring Safety: Modifying class hierarchies is safer and less error-prone with sealed
classes, as the permits list can be updated to reflect the new allowed subclasses.
5. API Stability: For library developers, sealed classes provide a means to maintain API stability by controlling which parts of the API can be extended by client code, preventing breaking changes in future releases.

Permitted subclasses of a sealed class must follow these constraints:
- They must be accessible by the sealed class at compile time.
- They must directly extend the sealed class.
- They must have one of the following modifiers: final (cannot be extended further), sealed (can only be extended by its permitted subclasses), or non-sealed (can be extended by unknown
subclasses).
- They must be in the same module as the sealed class (if the sealed class is in a named module) or in the same package (if the sealed class is in the unnamed module).

## Final classes

A final class in Java is a class that cannot be extended or inherited from.
- They cannot be extended by other classes.
- This prevents any modification or overriding of the class's behavior by inheriting classes.
- Final classes are often used for creating immutable classes like the *String* class, where the state cannot be changed after creation.
- Wrapper classes like *Integer*, *Double*, etc. are also declared as final classes to prevent extension.

The main purposes of using final classes are:
1. Security: final classes cannot be overridden, ensuring their behavior remains consistent and secure from external modifications.
2. Efficiency: The compiler can apply certain optimizations for final classes since their behavior is fixed.
3. Providing Constants: final classes can be used to group constants and utility methods
together, acting as a namespace.
