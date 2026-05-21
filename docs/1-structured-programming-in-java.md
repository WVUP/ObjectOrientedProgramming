# Module 1: Structured Programming in Java

# Introduction

> “Programs must be written for people to read, and only incidentally for machines to execute.”
> 
> **Harold Abelson**

The concept of Structured Programming started in the late 1950’s with the goal of improving clarity, quality, and development time of computer programs. Edsger Dijkstra, a leading computer scientist in the mid to late 20th century, argued that any computer program can be created using just three things: A sequence of steps, selection (making decisions), and iteration (looping). Writing software using these three things is known as structured programming.

All modern programming languages use a structured programming approach. Java makes extensive use of structured programming mechanisms, and a quick refresher before introducing new object-oriented concepts will be valuable.

## Learning Objectives
- [Variables and Data](#variables-and-data)
- [Classes](#classes)
- [Control Structures](#control-structures)
- [Collections](#collections)
- [Loops](#loops)
- [Methods](#methods)
- [Style and Comments](#style-and-comments)
- [Advanced Topics](#advanced-topics)

# Variable and Data

In Java, variables and data types are fundamental concepts that enable storing and manipulating data. Without data and the ability to change it in code, computers would be almost useless. Java supports this with variables, data types, and objects. 

A variable in Java is a human friendly name that under the hood points to a place in memory where a value is stored. For primitive data types, the value is a single piece of information compatible with the primitive data type, such as 5 for an int or true for a boolean. For an object, this value is the ***memory address*** where the actual object instance was created, which is called an ***object reference***. 

Variable names must start with a letter, underscore ( _ ), or dollar sign ( $ ), and can have letters, \_, $, and numbers in the name after the first character. Variable names are case sensitive, cannot have spaces or other whitespace characters, and cannot use reserved Java words like ***int*** or ***boolean***. 

Variables have three components to them: a data type, a variable name, and a value. Variables must be declared and initialized before they can be used. 

<caption><strong>Code Example: Variable declaration format</strong></caption>

```java
type variableName = value; 
```

In this example, the variable *variableName* is being assigned a value and that value must be compatible with the type. A real-world example might be where the variable *gallonsOfGas* gets the value 5. Since 5 is a valid integer, this will succeed. 

<caption><strong>Code Example: Variable declaration</strong></caption>

```java
int gallonsOfGas = 5; 
```

## Visibility
Class components such as fields, methods, and constructors have visibility associated with them. For most methods, the visibility is ***public***, meaning any class in any Java package can see and run this method. The other visibility that is often used is ***private***, which means only the code in this class can see whatever is marked this way. Typically, fields are private, and methods are public. This is a way of hiding implementation details and is a way of implementing ***encapsulation*** and ***abstraction***.

## Primitive Data Types
Data types can be either ***primitive*** or ***object types***. A primitive data type holds a single value such as a number, a single character, or a boolean value of true or false. Java supports eight primitive data types for single values, and arrays for a group or collection of values.

<caption><strong>Table 2.1: Primitive Data Types</strong></caption>

| Type    | Description                                                              |
| ------- | ------------------------------------------------------------------------ |
| byte    | 8 bit integer (-128 to 127)                                              |
| short   | 16 bit integer (-32,768 to 32,767)                                       |
| int     | 32 bit integer (-2,147,483,648 to 2,147,483,647)                         |
| long    | 64 bit integer (-9,223,372,036,854,775,808 to 9,223,372,036,854,775,807) |
| float   | Single-precision floating point (6 to 7 decimal digits)                  |
| double  | Double-precision floating point (15 to 16 decimal digits)                |
| char    | A single 16 bit Unicode character                                        |
| boolean | A boolean value of true or false                                         |



## Type Names
Primitive data types all begin with a lower-case letter. This is an important convention because object classes by convention all begin with an upper-case letter. This convention is known as Pascal case (***PascalCase***) because it was popularized in the Pascal programming language. Object instance variables are named using the ***camelCase*** convention. This helps distinguish primitives from classes and classes from object instances when reading source code.

## Variable Names
Since whitespace characters are not allowed in variable names, the convention is to use a workaround for a second or third word. Each language tends to have an approach that is used throughout the language. In Java, the convention is to have the first character of each word after the first one capitalized. Variable names following this convention are known as camel case (camelCase). The first character is the only difference between this and pascal case.

If a variable is a constant or final, meaning the value cannot change, then the convention is to declare that variable in all capital letters and use the underscore ( _ ) to separate words. Using the underscore to separate words is known as ***snake case*** and is a common convention in other languages. Using all capital letters this way is known as ***screaming snake case***: 

<caption><strong>Code Example: Constant variable declaration</strong></caption>

```java
static final double TAX_RATE = 0.15;
```

## Default Values and Arithmetic
In all cases of the primitive data types, when a variable is declared but not assigned a value a default value equating to 0 is automatically assigned. For any number this means 0 or 0.0, for a char variable this equates to \u0000, which is the *null* character. For boolean variables this is *false*. 

Any number without a decimal point is generally understood to be an int. If it is assigned to a byte, short, or long variable it will be automatically converted to that type - provided the actual value will fit in the memory space. A literal number can be declared as a long by adding the letter L after the number. A lower-case l also works but should be avoided because it looks like the number 1. Similarly, any number with a decimal point will default to a double unless there is an F or f after the number, forcing it to be a float. 

The numeric primitives all support basic arithmetic operations such as adding, subtracting, multiplying, and dividing. They can also be used in comparison operations. One interesting note though is when doing arithmetic operations of two primitives of the same type, the result will be of the same type even if the actual answer is not. What that means in practice is if you divide any of the whole-number types (byte, short, int, or long) the result is quotient division where any remainder is thrown away. As an example, dividing 1 / 2 does not give you 0.5, it gives you 0, and the .5 remainder is thrown away. 

<caption><strong>Table 2.2: Arithmetic Operators</strong></caption>

| Arithmetic Operator | Action                              |
| ------------------- | ----------------------------------- |
| +                   | Addition                            |
| -                   | Subtraction                         |
| *                   | Multiplication                      |
| /                   | Division                            |
| %                   | Modulus or remainder after division |
| =                   | Assignment                          |



To overcome this one of the numbers is typically converted or cast to a float or double, as shown below. Notice that only one operand must be a float or double to make the result a float or a double. Interestingly, char variables can be used as numeric values also. Java uses the number of the character in the ASCII or Unicode table that corresponds to the character.

<caption><strong>Code Example: Three different ways to cast an integer to a float for arithmetic</strong></caption>

```java
1 / 2.0; 
1F / 2; 
1 / (float)2;
```



## Shorthand Operators
In Java, the ++, --, +=, -=, and related operators are shorthand for performing common operations. They include increment (add), decrement (subtract), and compound assignment operators. 

The ++ operator increases a variable's value by 1. It can be used in two forms: 
- Prefix (++variable): Increments the variable before its value is used. 
- Postfix (variable++): Increments the variable after its value is used. 

<caption><strong>Code Example: Increment</strong></caption>

```java
int x = 5; 

// Prefix 
System.out.println(++x); // Output: 6 (x is incremented first) 

// Postfix 
System.out.println(x++); // Output: 6 (x is used, then incremented) 
System.out.println(x); // Output: 7 
```

Similarly, the -- operator decreases a variable’s value by 1. It also has the same two forms. 

<caption><strong>Code Example: Decrement</strong></caption>

```java
int y = 5; 
// Prefix 
System.out.println(--y); // Output: 4 (y is decremented first) 

// Postfix 
System.out.println(y--); // Output: 4 (y is used, then decremented) 
System.out.println(y); // Output: 3
```

The compound assignment operators combine an arithmetic operation with assignment, allowing you to update a variable's value in place. 

<caption><strong>Code Example: Compound assignment operator format</strong></caption>

```java
// Without compound assignment 
variable = variable operator value; 

// With compound assignment 
variable operator= value; 
```

There are several compound assignment operators described below. 

<caption><strong>Code Example: Addition with +=</strong></caption>

```java
int a = 10; 
a += 5; // Equivalent to a = a + 5 
System.out.println(a); // Output: 15 
```

<caption><strong>Code Example: Subtraction with -=</strong></caption>

```java
int b = 10; 
b -= 3; // Equivalent to b = b - 3 
System.out.println(b); // Output: 7 
```

<caption><strong>Code Example: Multiplication with \*=</strong></caption>
 
```java
int c = 4; 
c *= 3; // Equivalent to c = c * 3 
System.out.println(c); // Output: 12 
```

<caption><strong>Code Example: Division with /=</strong></caption>

```java
int d = 10; 
d /= 2; // Equivalent to d = d / 2 
System.out.println(d); // Output: 5 
```

<caption><strong>Code Example: Modulus with %=</strong></caption>

```java
int e = 10; 
e %= 3; // Equivalent to e = e % 3 
System.out.println(e); // Output: 1 
```

In addition to the compound assignment operators Java supports bitwise assignment operators: 

<caption><strong>Code Example: Bitwise AND with &=</strong></caption>

```java
int x = 5; // Binary: 0101 
x &= 3; // Binary: 0011 (Result: 0001) 
System.out.println(x); // Output: 1 
```

<caption><strong>Code Example: Bitwise OR with |=</strong></caption>

```java
int x = 5; // Binary: 0101 
x |= 3; // Binary: 0011 (Result: 0111) 
System.out.println(x); // Output: 7 
```

<caption><strong>Code Example: Bitwise XOR with ^=</strong></caption>

```java
int x = 5; // Binary: 0101 
x ^= 3; // Binary: 0011 (Result: 0110) 
System.out.println(x); // Output: 6 
```

<caption><strong>Code Example: Left Shift with <<=</strong></caption>

```java
int x = 2; // Binary: 0010 
x <<= 1; // Binary: 0100 (Shift left by 1 bit) 
System.out.println(x); // Output: 4 
```

<caption><strong>Code Example: Right Shift with >>=</strong></caption>

```java
int x = 4; // Binary: 0100 
x >>= 1; // Binary: 0010 (Shift right by 1 bit) 
System.out.println(x); // Output: 2 
```

## Objects
All other variable types are objects. These include class and interface types from the Java SDK, such as String or List, and user-defined types. User defined types are classes that a developer creates. Objects are sometimes called ***complex data types***. 

An object variable does not hold a value the way a primitive variable type does. Instead, object types hold a reference to a memory address, where that object exists in the computer’s memory. In other languages this is sometimes called a pointer. Unlike primitives, if an object variable is declared but not initialized by using the keyword ***new***, the variable has a default value of ***null***. 

## Wrapper Classes 
Primitive data types are not objects, so they have no methods associated with them. There are several situations though where an object is required, and for that each of the primitive data types has a corresponding object type, called a ***wrapper class***. Wrapper classes are unique in that they can be used directly in place of a primitive thanks to a feature known as *autoboxing* and *unboxing*, which simplifies the conversion between primitive types and their corresponding wrapper classes. Basically, Java allows these objects to be assigned a primitive value directly or allows the object instance to be used in place of a primitive value directly so that a wrapper class and its primitive are completely interchangeable. 

<caption><strong>Table 2.3: Wrapper Classes</strong></caption>

| Primitive Type | Wrapper Type |
| -------------- | ------------ |
| byte           | Byte         |
| short          | Short        |
| int            | Integer      |
| long           | Long         |
| float          | Float        |
| double         | Double       |
| char           | Character    |
| boolean        | Boolean      |

# Classes

Classes, objects, and instances are fundamental concepts in ***object-oriented programming***. Objects represent real-world or abstract people, places, things, or ideas. In other words, an object is a software representation of a noun. A ***class*** is a blueprint or template for creating objects. It defines the structure and behavior that objects of that class type will have. It ***encapsulates*** data for the object in the form of ***fields*** or ***attributes***, it defines ***methods*** that represent the object's behavior, and it serves as a user-defined data type. For example, a *Student* class might define attributes like *name* and *age*, and methods like *study()* or *takeExam()*.

An ***object*** is a runtime ***instance*** of a class created by the program when it is running. Objects are pieces of software that represent real-world entities, with both state (data) and behavior (methods). They are created based on the blueprint provided by the class. For example, *student1* could be an object of the *Student* class, with specific values for name and age and the ability to study or take an exam.

An ***instance*** of a class is essentially an object. It's a specific realization of a class. When ***instantiating*** a class, the developer is creating an instance of the object from that class. This is done with the ***new*** keyword. Each instance has its own unique memory address and its own copy of the class fields and methods. This means each object of a particular class will have the same attributes defined in the class but can have its own values for those attributes. This is known as the ***object state***.

For example, if *student1* and *student2* are two different instances of the *Student* class, each will have their own unique data, but both could call *study()* or *takeExam()*. This is done using the dot ( . ) notation, by referencing the object instance, a dot, then the method name.

For *student1* to study, the code would call:


```java
student1.study();

```

For *student2* to take an exam, the code would call:

```java
student2.takeExam(); 

```

This ensures the actions the method takes impact only that instance, which is a key part of object ***encapsulation***.

In summary, a class is the blueprint, while objects and instances are the concrete entities created from that blueprint. Each instance of an object exists in its own space inside the computer's memory once instantiated. Objects are instantiated, or “created”, with the new keyword when the program runs.

## Creating Classes

To create a class, it needs to be declared with the ***class*** keyword, followed by opening and closing curly braces. All the code defining the class fields and functionality are inside the classes’ curly braces. See the *BaseballPlayer* class below for an example. There is a general structure to a class that should always be followed:

- All classes should have class-level Javadoc comments
- All public methods should have method-level Javadoc comments
- All import statements should be at the top of the class, below the Javadoc
- Classes should be in their own file, and follow ***PascalCase*** naming conventions
- The classes should use the same convention for aligning curly braces throughout the code 
    - This text uses the convention of each opening curly brace being on its own line by itself, lined up vertically with the starting character directly above it
    - Closing curly braces are also on their own line, and in the same column as the corresponding opening curly brace
    - There should not be a blank line between multiple closing curly braces
- Code should be nested, with code inside a curly brace indented one level 
    - Indentation can be a tab or a set number of spaces, typically 4 in Java. Either one is fine, but use the same thing throughout the class and program, do not mix and match
- Each “section” of the code should be separated by a blank line
- All fields should be private and declared at the top of the class
- All fields should be declared on their own line and be private
- Constant fields can be public since their values cannot change
- Right after the fields, class constructors should be declared
- If there are any static methods, they would be declared before the instance methods 
    - Developers reading the code can see the class-level behavior (static methods) before diving into instance-specific details.
- Right after class constructors and any static methods, accessor and mutator methods should be declared 
    - The accessor and mutator method for each field should be declared together, not all accessors then all mutators
    - On very large classes it is a good idea to declare fields, accessors, and mutators in alphabetical order. Finding them is faster and easier this way
- After the accessor and mutator methods, business logic methods should be declared
- After the business logic methods, standard class methods such as *toString()* should be declared
- After those, any private methods used only in this class should be declared 
    - Private methods do not get Javadoc comments. You can and should use regular multi-line comments if needed to add clarity

<section class="callout info">
Some of this can be done in IntelliJ by going to the top menu bar, selecting Code => Reformat Code.

  Alternatively, with the class open in the editor, click CTRL+ALT+L on Windows or Linux, and Command + Option + L on a Mac to do the same thing. If you want to format an entire directory or project, right-click on the folder in the Project Explorer and select Reformat Code.

To customize the code formatter, go to File => Settings on Windows or Linux (Preferences on a Mac). Navigate to Editor => Code Style. Select Java, then customize the specific formatting rules such as indentation, spaces, braces, etc.
</section>


### The DRY Principle

When writing methods, a very important best practice is to not write the same application logic out twice. This is known as the ***DRY Principle***, which stands for *Don’t Repeat Yourself*. This is very important in terms of writing clear, concise, and easily maintainable code. If the same logic is in more than one place, it is more difficult to document and troubleshoot. Imagine if there was a bug and the same code was in four places, but the developer only updated the code in two of them. These inconsistencies greatly reduce the quality of the source code and the ease with which a new developer can understand a program.

### Naming Conventions

There are a few rules and guidelines about classes that any developer should follow. First, each class should be in its own file, and the class name and file name need to be the same. This makes importing just the classes needed possible and facilitates reusing code. Class names should always be ***PascalCase***, and instance names should always be ***camelCase*** in Java. This makes it clear what a developer is looking at when they are reading code and facilitates understanding.

### Fields, Accessors, and Mutators

Fields should always be declared as private and use public ***accessor*** and ***mutator*** methods as needed for access. As a standard convention in Java, these should be named with the word get and set in front of the field name. For a field firstName, the methods would be *getFirstName()* and *setFirstName(String newName)* respectively. This allows the developer to impose their own validation logic in the setter method and control the view of the data through the getter method as well. If a field is directly public a client class could assign an invalid value to the field and put the instance in an invalid state.

Consider a real-world example. In baseball, each player has a batting average which is a percentage of the times they step up to the plate to try to hit the ball versus the number of times they hit the ball and get on base. It’s a ratio of the player’s hits to the number of attempts, so clearly the number of hits cannot be greater than the number of attempts. This number is always represented with 3 digits of significance in baseball, even though the number may not actually divide out evenly to 3 digits. This is an example of what are known as business rules.

<caption><strong>Code Example: BaseballPlayer class</strong></caption>

```java
public class BaseballPlayer
{
	private int hits;
	private int atBats;
	
	// Constructor
	public BaseballPlayer(int hits, int atBats)
	{
		// Using the validation logic in the setter methods to keep it DRY
		setHits(hits);
		setAtBats(atBats);
	}
	
	public int getHits()
	{
		return hits;
	}
	
	public void setHits(int hits)
	{
		if (hits < 0)
		{
			System.err.println("Hits cannot be negative.");
		}
		else if (hits > this.atBats)
		{
			System.err.println("Hits cannot be greater than at-bats.");
		}
		else
		{
			this.hits = hits;
		}
	}
	
	public int getAtBats()
	{
		return atBats;
	}
	
	public void setAtBats(int atBats)
	{
		if (atBats < 0)
		{
			System.err.println("At-bats cannot be negative.");
		}
		else if (atBats < this.hits)
		{
			System.err.println("At-bats cannot be less than hits.");
		}
		else
		{
			this.atBats = atBats;
		}
	}
	
	// Getter for batting average
	public double getBattingAverage()
	{
		if (atBats == 0)
		{
			return 0.0; // Avoid division by zero
		}
		
		// Avoid quotient division where the remainder is thrown away
		double average = (double) hits / atBats;
		
		return Math.round(average * 1000) / 1000.0; // Round to 3 decimal places
	}
} 

```

***Business rules*** refer to the logical constraints and conditions that govern the behavior of the application and ensuring data integrity and correct functionality by enforcing real-world or domain-specific requirements in the software. Think about it in this context, if the fields were public in a *BaseballPlayer* class, it would be possible in another class to assign things like -3 hits or 10 hits and 7 at-bats to a player instance. Both are valid values in Java, but not in baseball. Having the fields be private and using public methods with validation and formatting for assigning and displaying the data enforces these business rules. This is why fields are private and accessor and mutator methods are public.

## Static Fields

***Static fields*** are also known as ***class variables***. Static fields are shared across all instances of a class, meaning there is one copy that all instances share. If one instance changes a static field, the new value is changed for all other instances as well.

Static fields are declared using the ***static*** keyword and are initialized only once. They need to be public, unlike instance fields. They are ideal for storing data that should be common to all instances, such as configuration settings, counters, or known constants. Static fields can be accessed using the class name, without the need for an object instance. One good example that already exists in Java is the value of π, which is in the *Math* class.

<caption><strong>Code Example: Java's Math.PI declaration</strong></caption>

```java
/** 
 * The most accurate approximation to the mathematical constant _pi_: 
 * `3.141592653589793`. This is the ratio of a circle's diameter 
 * to its circumference. 
*/ 
public static final double PI = 3.141592653589793; 

```

In this case the value is also declared as a constant because it never changes. Since the value of π is a known value that never changes it makes sense to have one copy of the value that all math equations can share. Static fields are a great solution to this situation.

Accessing a static field is done using the class itself, instead of an instance variable.

<caption><strong>Code Example: Static variable usage in a print statement</strong></caption>

```java
System.out.print(Math.PI); 

```

Initializing a static field is typically done when the field is declared, as shown above with Math.PI. This is the simplest and most straightforward approach and works almost all the time. Remember, static fields exist at the class level so they cannot work with instance fields or instance methods.

Another approach for more complex initialization is to use a static initialization block. Think of this like a constructor but only for static fields in a class. Complex logic using if/else, calculations, or calling other static methods can be used in this block.

<caption><strong>Code Example: Static initialization block</strong></caption>

```java
static 
{ 
	// initialize static fields here 
} 

```

## Static Methods

***Static methods***, like static fields, are methods that belong to the class rather than any instance. They are also declared using the static keyword, should be public, and are also called using the class name. Static methods can access static fields but cannot access instance variables directly, and they do not operate on an instance of the class.

Static methods can be called without creating an instance of the class. For example, *Math.sqrt(4)* is a call to a static method of the *Math* class with a parameter of 4 in this case. Static methods can only access static fields or method parameters directly and cannot use instance variables or methods unless they are passed as parameters.

Declaring a static method is like an instance method, but with the word *static* added.

<caption><strong>Code Example: Java's Math.sqrt() declaration</strong></caption>

```java
/**
 * Take a square root. If the argument is NaN or negative, the result is
 * NaN; if the argument is positive infinity, the result is positive
 * infinity; and if the result is either zero, the result is the same.
 * This is accurate within the limits of doubles.i
 *
 * <p>For a cube root, use cbrt. For other roots, use
 * pow(a, 1 / rootNumber).</p>
 *
 * @param a the numeric argument
 * @return the square root of the argument
 * @see #cbrt(double)
 * @see #pow(double, double)
*/
public static double sqrt(double a)
{
	return VMMath.sqrt(a);
} 

```

Static methods like sqrt are often used for utility or helper functions that do not require any object state. Probably the most important static method though is the ***main method*** in Java. The main method is static because it serves as the starting point of the application and needs to be callable without creating an instance of a class. It’s the classic Chicken or the Egg problem, how would you create an instance of a class to call main without already being in an instance of another class! Declaring the main method as static is a neat workaround to this conundrum.

### Static Method Restrictions

Because static methods exist at the class level and not the instance level, they cannot use this keyword since they are not associated with any instance. They also cannot directly access non-static fields or methods, although these may be passed as parameters when they are called.

## Enumerations

The ***Enum*** in Java is a special type of class that represents a group of constants. They provide a type-safe way of defining a fixed set of values. They are created using the *enum* keyword instead of the class keyword. As a convention, the values of an enum are typically written in uppercase and separated by commas. In Java, enums can have fields, constructors, and methods, making them very powerful.

There are several benefits to using an enum. They provide compile-time type safety, which guarantees that only predefined values can be used in the application code. Because of this, enums are ideal for representing fixed sets of constants, such as days of the week, months of the year, card suits, or directions of the compass. They also work well with switch statements, making decisions easy based on enum values. The enum type also supports iteration using the built-in values() method. Enums in Java offer a clean and type-safe way to represent fixed sets of constants, providing more functionality and safety compared to using plain constants or integers.

<caption><strong>Table 2.4: Enum methods</strong></caption>

| Method               | Description                                                                                                              |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| Values()             | Returns an array containing all the enum constants in the order they are declared                                        |
| ValueOf(String name) | Returns the enum constant with the specified name                                                                        |
| Ordinal()            | Returns the integer position (zero-based index) of the enum constant in its declaration                                  |
| Name()               | Returns the name of the enum constant as a String. The returned value is final                                           |
| ToString()           | Returns the string representation of the enum constant. By default, it returns the same as name(), but can be overridden |
| CompareTo()          | Compares the enum constants based on their ordinal value                                                                 |




Here's a simple enum definition and its use:

<caption><strong>Code Example: Enum definiiton</strong></caption>

```java
public enum DayOfWeek 
{
	MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY 
}
```


<caption><strong>Code Example: Enum usage in another class</strong></caption>

```java
DayOfWeek today = DayOfWeek.MONDAY; 
System.out.println(today);
```

# Control Structures

***Control structures*** in a programming language make decisions and therefore change the order that statements are executed in. They are divided into two main categories: selection statements and loops. 

***Selection statements*** give the developer a way to make a choice in the code based on a ***condition***. If a condition is true one path through the code will execute, and if the condition is false a different path through the code will execute. There are two code structures that can do this in Java, the if/else statement, and the switch statement. 

***Loops*** let a developer write a block of code and execute that same block of code multiple times. There are four different types of loops, and they either execute a set number of times (count-controlled loops) or they execute an indefinite number of times, so long as the test condition evaluates to true. Count controlled loops include the for loop and the for-each loop, while condition-controlled loops include the while and the do/while loop. 

## Logical Expressions
All statements rely on the concept of a logical expression. ***Logical expressions*** are anything that evaluates to true or false. This is typically done using comparison operators. ***Comparison operators*** compare the value of a variable to another variable’s value, or to a literal value. Alternatively, a boolean value can be used directly. 

<caption><strong>Table 2.5: Comparison Operators </strong></caption>

| Comparison Operator | Meaning                                        |
| ------------------- | ---------------------------------------------- |
| ==                  | Equal                                          |
| !=                  | Not equal                                      |
| >                   | Greater than                                   |
| <                   | Less than                                      |
| >=                  | Greater than or equal                          |
| <=                  | Less than or equal                             |
| !                   | Logical not operator (Inverts a boolean value) |



It is also possible to combine two or more logical expressions together into one compound logical expression. This can be done by evaluating if both simple statements are true, called a logical AND operation, or if one or the other simple statements are true, called a logical OR operation. Logical AND operations are done with the && operator, while logical OR operations are done with the || operator. Assuming there are two int type variables, a and b, a compound logical expression might look like one of these two examples: 

<caption><strong>Code Example: Compound logical expression</strong></caption>

```java
if (a == b && a > 0) 
if (a == b || a > 0) 
```

A compound and condition of (a == b && a > 0) would evaluate to true if the value in variable a is the same as the value in variable b and the value in variable a is greater than zero. The compound statement will only evaluate to true if both simple statements are true. Conversely a compound condition of (a == b || a > 0) would evaluate to true if the value of variable a is the same as the value in variable b, or even if they aren’t equal, it would still evaluate to true if the value in variable a is greater than zero. Only one of the two simple statements needs to be true for the compound OR statement to be true. 

Both compound operators, && and ||, are applied in a somewhat unusual way. If the first operand of a && is false, the second one is not evaluated because the compound statement cannot possibly be true. Likewise, if the first operand of a || is true, the second one is not evaluated because the compound statement cannot possibly be false. This is called a ***short-circuit***. The alternative to this is to nest a statement inside of another one, typically using an if statement inside of another if statement. 

## If/Else Statements
The most common selection statement is the ***if/else statement***. There are three main forms of this statement:

<caption><strong>Code Example: If/else statement format 1</strong></caption>

```java
if (expression) 
{ 
	// Statements that run if the expression evaluates to true 
} 
```

The statements inside the if block will only run if the expression evaluates to true. Everything before and after the if statement will run regardless. 

<caption><strong>Code Example: If/else statement format 2</strong></caption>

```java
if (expression) 
{ 
	// Statements that run if the expression evaluates to true 
} 
else 
{ 
	// Statements that run if the expression evaluates to false 
} 
```

In this form the statements inside the if block will only run if the expression evaluates to true; the statements in the else block will be skipped. If the expression evaluates to false, then the if block will be skipped and the else block will run. 


<caption><strong>Code Example: If/else statement format 3</strong></caption>

```java
if (expression) 
{ 
	// Statements that run if the expression evaluates to true 
} 
else if (different expression) 
{ 
	// Statements that run if the first expression evaluates to false 
	// and this expression evaluates to true 
} 
else 
{ 
	// Statements that run if the first two expressions evaluates to false 
} 
```

This is the most common decision structure used in code. It can be used in any of these forms and with compound statements for anything that can evaluate to a logical expression value of true or false. 

## Switch Statements
The second approach to making decisions in code is the ***switch statement***. The switch statement is a multi-way branch statement like the if/else-if/else statement that allows you to execute a specific block of code based on the value of an expression. 


<caption><strong>Code Example: Switch statement format</strong></caption>

```java
switch (expression)
{
	case value1:
		// code to be executed
		break;
	case value2:
		// code to be executed
		break;
	...
	default:
		// code to be executed if no case matches
		break; // break is optional for default
} 
```

The switch statement is more compact when there are several alternatives to evaluate so it can be easier to read. There are some key differences with the if/else if/else statement though. The switch statement can only work with the following data types:
- Primitive data types: byte, short, char, int, and long. 
- Enumerated types (Enums). 
- String class (supported since Java 7). 
- Wrapper classes: Byte, Short, Integer, Long, etc. 

Also, the *break* keyword is used to exit the switch block after the matching case's code is executed. Here is an example of using the ***switch*** statement to determine the day of the week based on a number: 

<caption><strong>Code Example: Switch statement</strong></caption>

```java
int day = 4;
switch (day) 
{
	case 1:
		System.out.println("Monday");
		break;
	case 2:
		System.out.println("Tuesday");
		break;
	case 3:
		System.out.println("Wednesday");
		break;
	case 4:
		System.out.println("Thursday");
		break;
	case 5:
		System.out.println("Friday");
		break; 
	case 6:
		System.out.println("Saturday");
		break;
	case 7:
		System.out.println("Sunday");
		break;
	default:
		System.out.println("Invalid day");
}
// Outputs "Thursday"
```

The break statement is easy to forget, and if break is not used the execution will continue to the next case until it finds a break or reaches the end of the switch block. This is known as "fall-through." 

<caption><strong>Code Example: Switch statement fall-through</strong></caption>

```java
int expression = 2;
switch (expression) 
{
	case 1:
		System.out.println("Case 1");
	case 2:
		System.out.println("Case 2");
	case 3:
		System.out.println("Case 3");
	default:
		System.out.println("Default case");
}
// Outputs "Case 2", "Case 3", and "Default case"
```

Using an enum in a switch statement is straightforward as well:

<caption><strong>Code Example: Switch statement using enum</strong></caption>

```java
switch (today)
{
	case MONDAY:
		System.out.println("Start of the work week");
		break;
	case WEDNESDAY:
		System.out.println("Midweek");
		break;
	case FRIDAY:
		System.out.println("TGIF!");
		break;
	default:
		System.out.println("Other day");
} 
```

Switch statements are not as powerful or as versatile as if/else-if/else statements and generally should be avoided. Switch statements only work with integral types (primitives) and strings, and only test for equality. They can also only compare against constant values, so there is no way to use a switch for range checks or if one variable is equal to another variable. 

Each case in a switch statement requires a break statement to prevent fall through behavior, which is easy to forget. The last case should be a default case, equivalent to an else block in an if/else to handle any cases not explicitly matched. In addition, it is not possible to nest a switch statement inside of another switch statement, so complex decision making is difficult or impossible. 

## Ternary Statements
Another control structure that is available is a ***ternary statement***. Think of this as a one line if/else statement. 

<caption><strong>Code Example: Ternary statement format</strong></caption>

```java
logical-expression ? valueIfTrue : valueIfFalse; 
```


<caption><strong>Code Example: Ternary statement determining even or odd values</strong></caption>

```java
String result = (number % 2 == 0) ? "Even" : "Odd"; 
```

If the number variable is divisible by zero with no remainder, the result variable will be assigned the value “Even”, otherwise it will be assigned the value “Odd”. 


<caption><strong>Code Example: If/else statement equivalent to determine even or odd values</strong></caption>

```java
String result; 
if (number % 2 == 0) 
{ 
	result = "Even"; 
} 
else 
{ 
	result = "Odd"; 
} 
```

The ternary operator provides a much shorter and cleaner syntax for simple conditions. Best Practices with ternary statements are to use them only for simple conditions that are small and straightforward. Use parentheses to ensure clarity when using ternaries in expressions. Avoid nested ternaries because they make code hard to read and debug. For complex conditions use if-else statements.

# Collections

***Collections*** provide a way to manage and access multiple items, known as elements, as a single entity. This eliminates the need for individual variables for each piece of data. Think of a collection as a group of objects. Collections allow developers to store multiple items of the same data types together and reference this grouping as one instance variable. Having several of the same kind of data is very useful in solving a lot of problems in computer science. 

There are many different types of collections, each with their own strengths and weaknesses. They include arrays, lists, queues, stacks, sets, and maps. All but one of these (arrays) are actually implemented as their own object type in the java.util package and require an import statement. These are declared as ***generics***, meaning the object type of the elements the collection will hold must be provided when the collection is declared. As a consequence, these collections cannot directly hold primitive values, although they can hold the wrapper classes that correspond to the primitive values. These classes provide methods for common operations like adding, removing, and retrieving elements from the group. The various collections that are available in the Java SDK also provide efficient methods for searching, sorting, and filtering data in the collection. 

## Arrays
***Arrays*** are the only type that are native to Java without needing an import statement. The array is considered a primitive data type in Java, since the JVM directly supports arrays. Arrays are also the only collection that can directly hold other primitive values such as char, int, or boolean. When an array is declared it must have the size provided, which means the number of elements in the array must be known up front. Because of this, arrays are a fixed size. The array instance has a property, *length*, which provides the size of the array. 

Arrays are declared by specifying the data type followed by square brackets and the array name. 

<caption><strong>Code Example: Array declaration</strong></caption>

```java
int[] myArray; 
String[] names; 
```

There is more than one way to initialize an array also. If a value is not specified, then each element will get the default value of that type. For primitives this is an actual value but for objects this is *null*. 

Providing the values when the array is declared:

<caption><strong>Code Example: Array declaration and initialization with a data set</strong></caption>

```java
int[] numbers = {1, 2, 3, 4, 5}; 
String[] fruits = {"apple", "banana", "orange"}; 
```

<caption><strong>Code Example: Initializing the size of the array</strong></caption> 

```java
int[] scores = new int[5]; 
```

<caption><strong>Code Example: Separating the declaration and initialization with a data set</strong></caption>

```java
int[] ages; 
ages = new int[]{25, 30, 35, 40}; 
```


## Lists
A ***List*** provides an ordered sequence of elements. Unlike arrays, a list can grow and shrink as needed. The two most common lists are the ArrayList and LinkedList types. They differ in the underlying mechanism they use to store and manage elements which can have performance trade-offs in different use cases. Both collections allow elements to be accessed, added, and removed at any location in the group. 

Here are examples of declaring different types of lists for *Student* and *Teacher* objects: 

<caption><strong>Code Example: Class import, declaration, and initialization of ArrayList and LinkedList variables</strong></caption>

```java
import java.util.ArrayList; 
import java.util.LinkedList; 
...
private ArrayList<Student> students = new ArrayList(); 
private LinkedList<Teacher> teachers = new LinkedList(); 
```

## Stacks and Queues
Another type of collection that is useful in certain circumstances is the ***Stack*** and ***Queue***. A stack is a Last-In-First-Out (LIFO) collection, where the order elements are added determines the order they are retrieved. The last element added to a stack is the first one retrieved back, and this cannot be changed. A queue operates in much the same way, except it is a First-In-First-Out (FIFO) collection. In both cases, the order that elements were added determines the order they can be removed. There is also a hybrid collection of these two, the dequeue (double ended queue, pronounced deck). It is a collection that can act as both a stack and a queue, allowing retrieval of elements from either the front or the back of the collection but not from the middle of the collection. 

Here are examples of declaring a stack of integer and a queue of string objects:

<caption><strong>Code Example: Class import, declaration, and initialization of Stack and Queue variables</strong></caption>

```java
import java.util.Stack; 
import java.util.Queue; 
...
private Stack<Integer> stack = new Stack(); 
private Queue<String> queue = new Queue(); 
```

## Sets
The ***Set*** collection type is a collection that holds unique elements. Put another way, a set cannot hold duplicate objects. The set is also an unordered collection, meaning there is no guarantee when an element is added about where it is in relation to other objects under the hood. There are several implementations of the Set collection in Java, but the most used one is ***HashSet***. HashSet uses a hash table to store and retrieve elements which gives it great performance. 

<section class="callout info">
A <strong>hash</strong> function on an object calculates a hash code for each field of the object, then uses those to compute a hash code for the entire object. Essentially it is an integer that tries to uniquely represent the state of an object. Two object instances with the same state must calculate the same hash code, but there isn’t necessarily a guarantee that different states won’t calculate the same hash value. When that happens, it is known as a collision.
</section> 

Here is an example of declaring a set of Employee objects: 

<caption><strong>Code Example: Class import, declaration, and initialization of a HashSet variable</strong></caption>

```java
import java.util.HashSet; 
...
private HashSet<Employee> employees = new HashSet(); 
```

## Methods for Collections
Each of these collections share the same basic methods. This is done through something known as an Interface, which defines several core methods that must be implemented. These all implement the Collections interface. How this works will be covered in detail later in the book. 

<caption><strong>Table 2.6: Common methods of collections and lists</strong></caption>

| Method                                | Description                                                                                                                                          |
| ------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Adding Elements**                   |                                                                                                                                                      |
| add(Object instance)                  | Add the object parameter to the collection and return a boolean indicating success or failure                                                        |
| addAll(Collection instance)           | Add the elements in the collection parameter to this collection and return a boolean indicating success or failure                                   |
| **Retrieving Elements - Lists only**  |                                                                                                                                                      |
| get(index number)                     | Return the element at the given index number, but also leaving it in the list                                                                        |
| remove(index number)                  | Remove the parameter object from the collection and returns it                                                                                       |
| **Removing Elements**                 |                                                                                                                                                      |
| remove(Object object)                 | Remove the parameter object from the collection and returns a boolean indicating success or failure                                                  |
| removeAll(Collection instance)        | Remove the elements in the collection parameter from this collection and return a boolean indicating success or failure                              |
| clear()                               | Remove all elements in the collection and return a boolean indicating success or failure                                                             |
| **Searching**                         |                                                                                                                                                      |
| contains(Object instance)             | Searches the collection for the object instance passed as a parameter. Returns true if the parameter is in the collection or false if it is not      |
| containsAll(Collection instance)      | Searches this collection for the collection instance passed as a parameter. Returns true if the parameter is in the collection or false if it is not |
| isEmpty()                             | Returns true if the size of the collection is zero or false if it is not                                                                             |
| size()                                | Returns the number of elements in the collection                                                                                                     |
| **Iterating and Converting**          |                                                                                                                                                      |
| iterator()                            | Returns an iterator for the collection                                                                                                               |
| toArray()                             | Converts this collection into an array holding the same object elements or primitive values                                                          |
| **Stream operations (Java 8 and up)** |                                                                                                                                                      |
| stream()                              | Returns a sequential stream with this collection as its source of elements                                                                           |


## Maps
The ***Map*** collection is somewhat unique compared to the others. Maps are a versatile type of collection that stores ***key-value pairs***. Whereas an array uses an index number to uniquely identify each element, a map can use any object type to uniquely identify each element. Keys in a map must be unique, but values can be duplicated. This gives very quick access to values based on their keys, just like an array gives easy access to any element based on its index number. The data type of the key does not have to be the same as the data type of the value in a map, although all keys have to be the same type and all values have to be the same type. The most common map used is the HashMap, which uses a hash function for keys, like a HashSet. 

Here is an example of declaring a map of ISBN objects mapped to Book objects as the key-value pair: 

<caption><strong>Code Example: Class import, declaration, and initialization of a HashMap variable</strong></caption>

```java
import java.util.HashMap; 
...
private HashMap<ISBN, Book> books = new HashMap(); 
```

## Methods for Maps
Just like collections, each implementation of a map will share the same basic methods. This is also done through an Interface, but now it is the Map interface instead of the Collections interface.

<caption><strong>Table 2.7: Common methods of maps</strong></caption>

| Method                                        | Description                                                                                                                           |
| --------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| **Adding and Updating Elements**              |                                                                                                                                       |
| put(Object key, Object value)                 | Inserts a key-value pair into the map, or updates the existing key-value pair if the key is already in the map                        |
| putAll(Map m)                                 | Add the key-value elements in the map parameter to this map and return a boolean indicating success or failure                        |
| putIfAbsent(Object key, Object value)         | Inserts the key-value pair if the key doesn't exist                                                                                   |
| replace(Object key, Object value)             | Replaces the value for the specified key only if it's currently in the map                                                            |
| **Retrieving Elements**                       |                                                                                                                                       |
| get(Object key)                               | Returns the value associated with the specified key                                                                                   |
| getOrDefault(Object key, Object defaultValue) | Returns the value for the key, or a default value if the key is not found                                                             |
| **Removing Elements**                         |                                                                                                                                       |
| remove(Object key)                            | Removes the mapping for the specified key                                                                                             |
| clear()                                       | Removes all mappings from the map                                                                                                     |
| **Searching**                                 |                                                                                                                                       |
| containsKey(Object key)                       | Searches the map’s keys for the key instance passed as a parameter. Returns true if the key is in the map or false if it is not       |
| containsValue(Object value)                   | Searches the map’s values for the value instance passed as a parameter. Returns true if the value is in the map or false if it is not |
| isEmpty()                                     | Returns true if the size of the map is zero or false if it is not                                                                     |
| size()                                        | Returns the number of key-value pairs in the collection                                                                               |
| **Iterating and Converting**                  |                                                                                                                                       |
| forEach()                                     | Performs the given action for each entry in the map                                                                                   |
| keySet()                                      | Returns a Set view of the keys in the map                                                                                             |
| values()                                      | Returns a Collection view of the values in the map                                                                                    |

# Loops

Loops are a type of control structure common to all programming languages. Loops provide a way to easily re-run a block of code. They are essential for automating repetitive tasks and processing collections of data efficiently, although if not careful they can introduce a couple of different bugs into a program. 

There are two categories of loops: ***count-controlled loops*** and ***condition-controlled loops***. Count-controlled loops run a set number of times and are the most common way of processing every element in a collection. Condition-controlled loops run as many times as needed until the condition being evaluated changes. Java provides two count-controlled loops and two condition-controlled loops. Regardless of the type of loop, each pass through the loop’s block of code is known as one ***iteration***. 

## Count-Controlled Loops
The primary count-controlled loop in Java is the ***for loop***. For loops are ideal for iterating over arrays or when you need to repeat an action a specific number of times. The for loop is used when the number of iterations is known in advance. It consists of three parts:
- Initialization: Setting up the loop variable
- Condition: The test of the loop variable to decide if the loop will go again or exit 
- Post-loop action: The change made to the loop variable on each iteration 


<caption><strong>Code Example: For loop statement format</strong></caption>

```java
for (initialization; condition; post-loop action)
{
	// code to be executed 
} 
```

The initialization portion references declaring a variable and initializing its value. This is almost always an integer and most often used to access an array or ArrayList index when processing a collection. The loop variable can be named anything that is a valid Java variable name that is not already declared, but it is most often simply named *i*, which is short for *index*. This variable only exists inside the loop’s { } brackets. 

The condition portion is a logical expression. This condition is checked at the beginning of the loop, and the loop will continue to iterate if this logical expression evaluates to true. 

The third portion tells the for loop how to change the loop variable after each iteration is completed. This ensures the variable updates, and since the variable is almost always used to access an element of a collection this ensures the block of code will access a different element. It also ensures the loop will eventually exit. 


<caption><strong>Code Example: For loop statement counting from 0 to 4</strong></caption>

```java
for (int i = 0; i < 5; i++) 
{ 
	System.out.println("The i variable is set to: " + i); 
} 
```

When this runs, it will produce this output.

<caption><strong>Console Output:</strong></caption>

```
The i variable is set to: 0 
The i variable is set to: 1 
The i variable is set to: 2 
The i variable is set to: 3 
The i variable is set to: 4 
```

Accessing elements of the collection inside the loop is done by using the index variable with the collection. 

<caption><strong>Code Example: Accessing data from an array and ArrayList, respectively</strong></caption>

```java
// Will print the value of the myArray element at the index of the i variable 
System.out.println(myArray[i]); 
// Will print the value of the myList element at the index of the i variable 
System.out.println(myList.get(i)); 
```

Java’s second count-controlled loop is often combined with the classic for-loop and simply called an ***enhanced for-loop***. This is often called a ***for-each loop*** and is designed specifically for looping over collections. This is very useful for working with collections that do not have an index number such as sets and maps, although it also works well with arrays and lists. 

<caption><strong>Code Example: Enhanced for loop statement format</strong></caption>

```java
for (Student s : students) 
{ 
	// Each student instance will be assigned to the variable s 
	// for one iteration 
} 
```

## Condition-Controlled Loops
The other category of loops are known as condition-controlled loops. These don’t run a set number of times but rather run as long as the condition is true. There are two types of count-controlled loops in Java, the ***while loop*** and the ***do-while loop***. The syntax is slightly different, but fundamentally the only difference is a while loop checks the condition at the beginning of the loop and the do-while checks the condition at the end of the loop. The consequence of this is a while loop will run zero or more times, whereas a do-while loop will always run one or more times. With both, the loop needs to manipulate the variable being checked in the condition to prevent an infinite loop. 


<caption><strong>Code Example: While loop statement format</strong></caption>

```java
while(condition) 
{ 
	// Loop code 
} 
```

The condition is any logical expression that evaluates to true or false. This condition is checked before entering the loop, so if the condition is false, the loop is never executed. If the loop is true, it will execute the code inside the curly braces, then re-evaluate the condition. 

The only real difference between a while loop and a do-while loop is when the condition is tested. In a do-while loop the condition is tested at the end of the loop, guaranteeing that the loop will run at least once. The syntax of a do-while loop is very similar. 


<caption><strong>Code Example: Do-while loop statement format</strong></caption>

```java
do 
{ 
	// Loop code 
} while(condition); 
```

The do-while loop is particularly helpful for things like validating user input, where the user will be asked for input and then the input is checked. If it is valid the first time the loop is exited, but if the user’s input is invalid the loop will continue until the user provides valid input. 


<caption><strong>Code Example: User input validation</strong></caption>

```java
int input = 0; 
boolean validInput = false; 

do 
{ 
	System.out.print("Select a number between 1 and 4: "); 
	input = scan.nextInt(); 
	
	if (input >= 1 && input <= 4) 
	{ 
		validInput = true; 
	} 
	else 
	{ 
		System.err.println("Invalid selection, please try again"); 
	} 
} while (validInput == true); 
```

## Nested Loops 
Sometimes it is necessary to run a loop inside of another loop. This is called a ***nested loop*** and is important for solving many different problems. It can be done with any kind of loop but is most often done with a for-loop structure. This is useful for visiting every element of a grid such as a 2-dimensional array, and for sorting a collection using one of several different algorithms. 

<caption><strong>Code Example: Nested for loops</strong></caption>

```java
for (int i = 0; i < 10; i++) 
{ 
	for (int j = 0; j < 10; j++;) 
	{ 
		// Do something with i and j. 
		// For each value of i, j will loop through all its values 0 - 9 
	}
}
```

This works well for solving several different problems but be aware that as the size of the loops grows the number of iterations grows exponentially. For example, in the above code there are two loops that iterate 10 times, but because one loop is inside the other, the inner loop executes 100 times. This is because the inner loop runs ten times when the outer loop is on its first iteration, then ten times when the outer loop is on its second iteration, and so on. 

## Iteration Manipulation
There are certain situations where a developer might want to skip an iteration of a loop or get out of the loop altogether before it would normally finish. There are two tools to do exactly these things. The first one is the ***continue*** statement, which skips the rest of the current iteration and moves straight to the next iteration. The second one is the ***break*** statement, which stops the current iteration and exits the loop altogether. 

In this example of a for loop, the modulus (%) operator is used to test if the i variable is evenly divisible by two or not. This is a quick way to test if a number is even or odd. In this case, if the number is even, the loop will skip the remainder of the code block and run the next iteration. If the number is odd, the loop will continue to execute and run the print statement. 

<caption><strong>Code Example: Continue keyword usage</strong></caption>

```java
for (int i = 0; i < 10; i++) 
{ 
	// skip every other iteration 
	if(i % 2 == 0) 
	{ 
		continue; 
	} 
	System.out.println("i is " + i); 
} 
```

When this runs, it will produce this output.

<caption><strong>Console Output:</strong></caption>

```
i is 1
i is 3
i is 5
i is 7
i is 9
```

In this next example, a loop has been created to play a game until the user chooses to exit. This is technically an infinite loop, but the break statement makes it possible to exit when the player chooses to quit.

<caption><strong>Code Example: Break keyword usage</strong></caption>

```java
while(playGame)
{ 
	// User plays a game until they choose to exit 
	...
	if (playGame == false) 
	{ 
		break; 
	} 
} 
```

## Troubleshooting Loops 
Loops are incredibly useful and necessary, but they introduce several potential pitfalls. Being aware of them can help recognize and avoid or fix them when they do crop up. 

One mistake often made by new programmers is to put a ; after the for loop itself, and before the opening curly brace.

<caption><strong>Code Example: For loop header typo - semicolon at the end</strong></caption>

```java
for(int i = 0; i < 10; i++); 
```

This will cause the block of code below the for loop to be treated as a separate entity independent of the for loop. 

One potential bug that can occur with this portion of a for loop is known as an ***infinite loop***. An infinite loop will prevent a program from ever getting out of the loop because the condition portion of the loop will always evaluate to true if the increment/decrement portion doesn’t eventually cause the condition portion to evaluate to false. 

<caption><strong>Code Example: For loop - infinite loop</strong></caption>

```java
for (int i = 0; i < 5; i—) 
{ 
	System.out.println("The i variable is set to: " + i); 
}
```

In this example, the i variable starts with a value of 0, and goes down by one on each iteration. The condition being checked for is as long as *i* is less than five. Since *i* is going down in value instead of up in value this condition will always be true. The system will run this code until the *i* variable exceeds the maximum size of an integer on the system, then the application will crash. 

Another potential bug that can occur with the condition portion of a for loop is known as an off-by-one error. An off-by-one error happens when a loop runs one too many or one to few times. Most often it happens when developers do not account for a collection’s index starting at 0 instead of 1. If an array’s length or a collection’s size() is 10 for instance, it is easy to accidentally count from 1 - 10, instead of from 0 - 9. When the code in the loop tries to access index 10 of the collection it won’t exist, and the application will likely crash. 

Since for loops are most often used to process every element in a collection, it is typical to declare them using the collection’s length or size.

<caption><strong>Code Example: Array length in condition statement</strong></caption>

```java
for (int i = 0; i < myArray.length; i++) 
```


<caption><strong>Code Example: ArrayList size() in condition statement</strong></caption>

```java
for (int i = 0; i < myArrayList.size(); i++) 
```

The key here is to use < and not <=, because both will return the total number of elements, not the number of elements from a 0-based index. This means if there are 10 elements, indexed 0 - 9, the array’s *length* property or the list’s size() method will return 10.

# Methods

Objects represent real-world or abstract people, places, things, or ideas. In other words, an object is a software representation of a noun. Objects have two major aspects to them: ***fields*** and ***methods***. An object’s fields are the variables and their values that make up an instance’s state. All objects of the same class will have the same fields, but likely at least some different values. 

In addition to the fields, objects have methods. Methods define what actions an object can take. In this sense, a method is a software representation of a verb. There are several parts of a method that are important to understand, but at the most basic level a method has a signature and a body. The signature includes the method’s visibility, its return type, the method name, and the list of parameters a method takes. The body of a method is the code that will execute when that method is called and involves all of the code inside the curly braces attached to the method signature. 

<caption><strong>Code Example: Method declaration format</strong></caption>

```java
visibility return methodName(parameters) 
{ 
	// Body of the method inside the curly braces 
}
```

One special kind of method should always exist in every class. This is called a ***constructor method***. A constructor method is what gets executed when an object is created using the new keyword. A constructor always has the same name as the class and does not have a return type. This is because a constructor always returns a new instance of the object. A constructor sets the initial state of the new object by setting the values of the fields in the object. 

<caption><strong>Code Example: Constructor method format</strong></caption>

```java
public className(parameters)
{
	// Body of the constructor inside the curly braces 
}
```

For most methods, the visibility is ***public***, meaning any class in any Java package can see and run this method. The return is what the method is sending back to wherever the method was called from. Return types can be ***void*** for just returning control, any primitive type’s value, any object instance, or ***null***. 

The parameter list can be empty if the method doesn’t take any parameters, but the ( and ) still need to be there. Also, the parameter values do not need to be declared inside the body of the method again, they are already declared in the parameter list. Another thing that often confuses new developers is that the names of the parameters do not matter when calling the method from another block of code. For instance, calling the *add()* method might look like either of these examples: 

<caption><strong>Code Example: Method declaration - add()</strong></caption>

```java
public class MethodDemo 
{
	// fields, constructors, etc. 
	... 
	public int add(int a, int b) 
	{ 
		int sum = a + b;
		return sum; // This is the int that is returned 
	} 
}
```

In the same class, this method can be called just by the method name.

<caption><strong>Code Example: Internal method call</strong></caption>

```java
int answer = add(10, 5); // Answer will get the value 15 
```

In another class, this method would be used like this: 

<caption><strong>Code Example: External method call</strong></caption>

```java
MethodDemo methodDemo = new MethodDemo();

// Passing literal values to the method. 
// The value returned is assigned to the result variable 
int result = methodDemo.add(5, 4); 

// Passing a literal and the value of a variable 
int secondResult = methodDemo.add(99, result);
```

If a method has the same return type and the same name, but a different list of parameters, it is called an ***overloaded method***. This is especially common with constructors. 

A method with a return can be used anywhere that type of data is needed. This can lead to some interesting looking code but works just like having a variable of the same type. 

<caption><strong>Code Example: Nested method call</strong></caption>

```java
int calculation = methodDemo.add(3, methodDemo.add(5, 15)); 
```

The *calculation* variable will get the value returned by the first, or outer-most, call to the *add()* method. This method takes two parameters though. The second parameter is the returned value of the second, inner call to the add method where the parameters are 5 and 15.

# Styles and Comments

As described in the earlier Classes section, it is very important for a developer to stick with a consistent style when writing source code. The quote at the beginning of the chapter alludes to why: 

> “Programs must be written for people to read, and only incidentally for machines to execute.”
> 
> **Harold Abelson**

Code for an application is not written once and never looked at again. In fact, the biggest part of any ***software development life cycle (SDLC)*** is the ***maintenance phase***, where the application is deployed for people to use. In this phase, developers fix bugs and add features as needed. Most of the time the developers doing maintenance are not the developers who wrote the original code, or even if it is the same developer, it has been so long since the code was written the developer may not remember it. In either case, it is important that the source code be as clear and well documented as possible to convey clearly and easily what the code is supposed to do and why. 

Most business applications and open-source software is created by a team of developers. If all developers follow the same general style and structure, it improves the code quality and maintainability. This makes the application more stable over the long term. Having consistent formatting and style make the code easier to read and understand for all team members, regardless of who wrote it. A uniform code structure reduces the likelihood of misunderstanding and errors during updates or bug fixes because the structure of the code is consistent and predictable. Debugging and troubleshooting become easier when team members understand the flow of the code without needing clarification. 

Having a uniform code style and structure also makes it easier for new developers to quickly understand and contribute to the code base if it follows a standard structure. Developers spend less time debating style choices or reformatting inconsistent code and more time working on real solutions. As a student it is important because it makes the code you write easier for the person grading it to understand! 

Some guidelines that are helpful in any situation with any language would be to use descriptive variable names that explain what they do or what they hold. This is known as ***self-documenting code*** and is not a replacement for code comments but enhances readability. An example would be naming a variable for a person *firstName* instead of *var1*. The name *firstName* is much clearer about the intent of that variable. Methods should be named similarly. Collection variables should generally be named plural, and individual variables should be named singularly. Methods should also generally be no more than one screen’s worth of code. If a method is hundreds of lines long, break the steps up into smaller methods that solve each step individually. Another useful guideline for readability is to not let one line of code be so long it goes off the screen. Lastly, add code comments to improve understanding and clarify intent, don’t add comments stating the obvious.

<caption><strong>Code Example: "Useless" comment</strong></caption>

```java
// Declare a variable to hold the first name 
private String firstName; 
```

# Advanced Topics

## Recursion
***Recursion*** is a technique in programming where a method calls itself to solve a problem. It can be considered a form of looping because it repeatedly performs operations until a specified condition (the base case) is met. However, recursion achieves repetition differently compared to traditional iterative loops like for or while. 

For recursion to work, there are two conditions that the method needs to evaluate. Any recursive method needs a condition where the recursion stops, known as the base case. Without a base case, recursion would continue indefinitely, leading to a stack overflow error and the application would crash. The second condition is the recursive case, which is the part of the method where the method calls itself with modified arguments, moving closer to the base case. 

Recursion can make some solutions more elegant and easier to understand, especially for problems with nested or branching structures. However, recursive calls use stack memory. Without a proper base case, the stack may overflow. Loops are more efficient for simple iterations since recursion involves the added overhead of the method call for each iteration. While recursion provides a cleaner solution for certain problems, loops are generally preferred for straightforward, performance-sensitive tasks.

# Summary

Programming follows a structured approach to solve problems in code. To function correctly, a program needs a way to store, retrieve, and manipulate data. This is typically done using variables which provide a human friendly name in the code to do this for each piece of data. Variables can hold either primitive or object data. The type of data associated with a variable is set when the variable is declared. In addition to single variables, Java supports groups of variables through several types of collections. Each collection type has its own strengths and weaknesses. 

Classes and objects represent a complex type of data. Some classes are provided in the Java SDK, while others are created and used by the developer as part of the application they are developing. There are several conventions around classes that a developer must be familiar with, from naming conventions to the file structure to the layout of the code inside the class. Classes are the blueprints used to create objects and consist of fields and methods.

Decisions can be made in code using logical expressions. This is done by evaluating a variable or other condition in a way that results in a true or false value. This is most often implemented with an if-else structure, although switch statements and ternary operators can also be used. In addition to making decisions, it is possible to run the same block of code multiple times using loops. Loops can be count controlled and run a set number of times, or condition controlled and run as few or as many times as needed. Processing collections is typically done with loops, although that is not the only use of loops. 

Methods are where the actions of an object are implemented. They consist of a method signature and a method body.

# Review Questions

1. What are the three components of structured programming? 
2. What is the main purpose of variables and data in structured programming? 
3. List and describe key components or rules of variables and data. 
4. Give an example or scenario where variables and data would be applied in Java. 
5. What is the main purpose of classes in structured programming? 
6. List and describe key components or rules of classes. 
7. Give an example or scenario where classes would be applied in Java. 
8. What is the main purpose of control structures in structured programming? 
9. List and describe key components or rules of control structures. 
10. Give an example or scenario where control structures would be applied in Java. 
11. What is the main purpose of collections in structured programming? 
12. List and describe key components or rules of collections. 
13. Give an example or scenario where collections would be applied in Java. 
14. What is the main purpose of loops in structured programming? 
15. List and describe key components or rules of loops. 
16. Give an example or scenario where loops would be applied in Java. 
17. What is the main purpose of methods in structured programming? 
18. List and describe key components or rules of methods. 
19. Give an example or scenario where methods would be applied in Java. 
20. What is the main purpose of style and comments in structured programming? 
21. List and describe key components or rules of style and comments. 
22. Give an example or scenario where style and comments would be applied in Java. 
23. What is the main purpose of advanced topics in structured programming? 
24. List and describe key components or rules of advanced topics. 
25. Give an example or scenario where advanced topics would be applied in Java.
