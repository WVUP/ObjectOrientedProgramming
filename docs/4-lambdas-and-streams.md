# Module 4: Lambdas and Streams

# Introduction

> “You can’t allow tradition to get in the way of innovation.”
>
> **Bob Iger**

***Lambda*** expressions, introduced in Java 8, provide a clear and compact syntax for writing functions. Lambdas in Java provide a powerful tool for writing more expressive code. Lambdas also enable functional programming constructs which facilitates both parallel processing and helps streamline operations on collections.

Java ***streams*** are a powerful feature introduced in Java 8. Streams provide a declarative approach to processing collections of data. They represent a sequence of elements and support various operations that can be pipelined to produce desired results. Streams offer several advantages over traditional types of collections, including improved code readability and maintainability. They support functional-style operations through lambdas on collections, which makes ***parallel processing*** easier. They also reduce ***boilerplate code*** compared to traditional iteration over collections. In short, streams provide a more expressive and often more efficient way to process data, especially when dealing with large collections or complex operations.

## Learning Objectives
- [Lambdas](#lambdas)
- [Streams](#streams)
- [Processing Streams](#processig-streams)
- [Advanced Topics](#advanced-topics)

# Lambdas

Lambdas provide a functional processing capability to Java. Prior to lambdas, Java was purely object-oriented. Lambdas provide a way to pass a small section of code as a parameter to a method. That method can then execute the code passed as a parameter as part of its own method body. They are particularly useful with the Collections framework for operations like ***filtering*** and ***mapping*** and are incredibly useful in GUI programming as a way of implementing an ***event listener***. 

## Processing Collections 
Traditional approaches to processing a collection involve using a loop to get each element one at a time from a collection, then processing that one element in some way. 

<caption><strong>Code Example: Loop pseudocode</strong></caption>

```
Loop over each element in the collection 
  Get that element 
  Process the element 
End the loop 
```

The particular loop construct does not matter, the algorithm is the same. Lambdas can approach this problem in a different fashion though. With a lambda the function is passed to the collection and the collection is told to execute that code on each element in the collection.

<caption><strong>Code Example: Lambda pseudocode</strong></caption>

```java
collection.forEveryElement(lambda code); 
```

This is simpler to write and easier to understand. The same processing of each element in the first approach still happens, but the boilerplate looping code has been moved into the method on the collection instead of the developer having to create that loop themselves every time it is needed. The collection itself is now able to run the code on each element itself instead of just holding onto each element. 

Imagine there is a sink full of dishes that need to be washed. The sink represents the collection in this analogy. In the traditional approach the developer would get a dish from the sink, wash and dry it, then get the next dish from the sink until the sink was empty. This is the traditional processing of a collection where one element is retrieved and processed, then the next is retrieved and processed, et cetera until there are no more elements left. 

With lambdas the instructions for washing dishes are given to the sink and the sink is told to carry out the instructions for every dish. Interestingly enough, the developer does not need to know how this is done by the sink, instead the developer is just saying make this happen. The sink could wash the dishes itself or put them in a dishwasher. This makes the developer’s job much easier! Of course, this analogy is a hardware problem and not one a developer would handle…

## Syntax 
Lambdas are remarkably similar to methods. They have a block of code that will do something with data. Lambdas do not belong to a class though, so it does not have a name. This is why they are referred to as anonymous. A traditional method has a visibility, return type, method name, and parameter list in its method signature, and a body of code. 

<caption><strong>Code Example: Traditional method for printing data from a  collection</strong></caption>

```java
public void printDetails(List students) 
{ 
  for (int i = 0; i < students.size(); i++) 
  { 
    Student s = students.get(i); 
    System.out.println(s.getDetails()); 
  } 
} 
```

A lambda only has a parameter list and a body of code. 

<caption><strong>Code Example: Basic syntax of a lambda</strong></caption>

```java
(parameters) -> single expression

//or

(parameters) -> { statements; } 
```

Here is a basic example of a lambda that will print the details of a student: 

<caption><strong>Code Example: Printing data from a collection using a lambda expression</strong></caption>

```java
(students) -> { 
    for (int i = 0; i < students.size(); i++) 
    { 
      Student s = students.get(i); 
      System.out.println(s.getDetails()); 
    } 
} 
```

Clearly there are several differences and similarities. A method uses the word public to expose the method to the rest of Java outside of its class, whereas the lambda is always implicitly public. The method explicitly states that it is returning a String, whereas the compiler can figure out that the lambda is returning a String from the return statement in the lambda, so the lambda doesn’t need a return type. The method has a name, *printDetails*. Lambdas are anonymous though, so it has no name, it simply starts with the parameter list. The arrow (->) separates the parameters from the body of code in the lambda, which is unique to lambdas and was added in Java version 8. 

Lambdas shine in situations where there is a simple, one-off task that does not require complex operations. There are no instance fields and no constructor though, so they are not as powerful as a class. They are specialized in when and where they are useful, but in those situations, they are a great choice.


## The forEach Method
Earlier when describing lambdas, the pseudocode example called a fictitious method *forEveryElement()*. Java actually has a method that does this operation on collections, called *forEach()*. 

<caption><strong>Code Example: forEach() format</strong></caption>

```java
someCollection.forEach(code to apply to each element); 
```

Remember the earlier analogy of the kitchen sink and the dishes. Using the *forEach()* method might look like this: 

<caption><strong>Code Example: forEach() method analogy</strong></caption>

```java
kitchenSink.forEach(code explaining how to wash dishes); 
```

Earlier a method printing the details of a student object was shown along with a lambda equivalent. That lambda can be rewritten using the *forEach()* method, like this: 

<caption><strong>Code Example: Updated lambda expression using forEach()</strong></caption>

```java
students.forEach((Student s) -> 
    { 
      System.out.println(s.getDetails()); 
    } 
)
```

This does not look much simpler or different than the earlier version but notice that there is no explicit for loop iterating over each student. The *forEach()* method processes each student one at a time. The iteration over each element was done inside the *forEach()* method and not explicitly written here. The parameter to the *forEach()* method is a lambda telling it what to do to each element on each iteration. While the functionality of this code is the same as the earlier example, the syntax is not like traditional Java methods. 

## Simplifying Lambda Statements
Lambdas help write more concise, clear code. Looking at the two examples above, they really are not that different. The visibility and method name are eliminated in the lambda, but really not much else is different. Fortunately, this is not the only way to write a lambda. 

Since the collection already knows what type of elements it is holding, the data type can be omitted. That means the code can be simplified to this: 

<caption><strong>Code Example: Lambda simplification - omit data type</strong></caption>

```java
students.forEach((s) -> 
	{ 
		System.out.println(s.getDetails()); 
	} 
}
``` 

Since there is only one parameter, the parentheses around the lambda variable is also not needed.

<caption><strong>Code Example: Lambda simplification - omit extra parentheses</strong></caption>

```java
students.forEach(s -> 
	{ 
		System.out.println(s.getDetails()); 
	} 
} 
```

Within the *forEach()* method there is only one line being executed for each element, so the curly braces can also be eliminated. The updated version now looks like this, which is a great deal more concise and clearer: 

<caption><strong>Code Example: Lambda simplification - omit lambda code block brackets</strong></caption>

```java
students.forEach(s -> 
	System.out.println(s.getDetails()) 
); 
```

Which can then be shortened to just this: 

<caption><strong>Code Example: Lambda simplification - final version</strong></caption>

```java
students.forEach(s -> System.out.println(s.getDetails()));
```

### The Function Object
While lambdas themselves are anonymous, Java does provide the *Function* object to encapsulate a lambda function. This allows a developer to encapsulate a lambda into an object to pass it as an argument, return it from a method, and store it in a variable. The object takes two generic types, much like a Map. The first type is the parameter to the function, and the second type is the return type of the function. 

#### Function Object Methods
The *Function* object has four methods associated with it.

<caption><strong>Table 5.1: Function object methods</strong></caption>


| Method     | Description                                                                                                                                               |
| ---------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| apply()    | This takes the function’s parameter, then runs the function with it                                                                                       |
| andThen()  | This method returns a composed function that applies the current function first, and then this function. Essentially it daisy-chains two lambdas together |
| compose()  | This method is like the andThen() method, but this one runs first, then the first method is executed. The order is reversed from andThen()                    |
| identity() | This method returns the method’s argument                                                                                                                 |

<caption><strong>Code Example: Function object method usages</strong></caption>

```java
Function<Integer, Integer> square = x -> x * x;

// Running the function - result will have the value 25
int result = square.apply(5);

// Adding andThen() to run a second lambda after the first
square.andThen(x -> x * 2);
result = square.apply(5); // 5 * 5 runs first returning 25, then 25 * 2 returns 50

// Instead of andThen, using compose to run the second lambda first
Function<Integer, Integer> square = x -> x * x;
square.compose(x -> x * 2);

square.apply(5); // 5 * 2 runs first returning 10. Then 10 * 10 returns 100

Function identity = Function.identity(); 
identity.apply(5); // Returns 5
```

#### Other Functional Types 
There are other similar objects that can encapsulate a lambda. 

<caption><strong>Table 5.2: Functional types</strong></caption>

| Object              | Description                                                                        |
| ------------------- | ---------------------------------------------------------------------------------- |
| Consumer<T>         | Represents an operation that accepts a single input argument and returns no result |
| Predicate<T>        | Represents a predicate (boolean-valued function) of one argument                   |
| Supplier<T>         | Represents a supplier of results                                                   |
| BiFunction<T, U, R> | Represents a function that accepts two arguments and produces a result             |

All of these are in the *java.util.function* package and require an import statement. 

### Method Reference
In addition to writing your own lambdas as functional code, it is possible to reference other methods in a similar fashion, using the :: syntax. The :: syntax in Java is known as the method reference operator and it separates the class or object from the method name. It was introduced in Java 8 and provides a way to refer to methods or constructors without executing them. This makes them ideal for streams and lambdas. 

A ***method reference*** is a shorthand for a lambda expression that simply calls a specific method. For example, `Integer::sum` 
is equivalent to the lambda `(a, b) -> Integer.sum(a, b)`

<caption><strong>Code Example: Method reference using System.out.println()</strong></caption>

```java
List numbers = Arrays.asList(1, 2, 3, 4, 5);
numbers.forEach(System.out::println);
```

There are four types of method references: 
- Static 
- Instance references for an object 
- Instance references for a class 
- Constructor references

Static method reference refers to a static method in a class, such as the *Integer* class’s *sum()* method. The instance method reference of a specific object refers to the method tied to a specific object instance. If there was a String object called *name*, then referring to that instance’s *toUpperCase()* method would be `name::toUpperCase`. Similarly, instance methods can be referenced from the class as well, which looks like the static reference, but the method is an instance method and not a static method. The equivalent of the earlier example would be `String::toUpperCase`. The last one is the constructor reference, which is done with `ClassName::new`. 

Method references improved readability by reducing boilerplate code compared to lambda expressions. They also closely align with Java’s functional programming paradigm introduced with Lambdas in Java 8. Method references also make the intention clearer when the method is used without additional logic.

# Streams

Java Streams provide a powerful and expressive way to process collections of data. Introduced in Java 8, the Stream API is part of the *java.util.stream* package and is used to perform operations on a collection of elements in a functional and declarative style, using lambdas. 

There are several components of a stream. Streams have a data source, such as a collection (List, Set), an array, or an I/O channel. Once there is a stream, some operation or set of operations will be done on the stream. These are divided into two categories, intermediate and terminal operations. Intermediate operations will transform the source stream in some way and create a new stream. Terminal operations are the last operation done and produce a result or side-effect. 

Streams have several features. They use declarative programming through lambdas, which puts the focus on "what" to do rather than "how" to do it. They support what is known as ***Lazy Evaluation***. With lazy evaluation, intermediate operations are evaluated only when a terminal operation is invoked, so they are more efficient when several stages of an operation need to be done. Streams can also process data in parallel to improve performance with ***multi-threading***. Streams are also ***immutable***, so they do not modify the original data source.

# Processing Streams

Streams and other collections like Lists, Sets, and Maps have different purposes. Streams operate on data without storing it. The focus of a stream is performing data processing operations, whereas the focus of these other collection types is to store and group elements in memory. A stream in Java supports running operations on those elements. Because of this, streams do not change the original structure where the stream came from. 

Streams can be created from collections, arrays, or other sources, and they allow for both ***sequential*** and ***parallel processing*** of data. Streams can also process data on the fly, which can reduce memory for large amounts of data. Streams can also be continuous or infinite. A good example of this is the *System.in* stream used with the *Scanner* object. This treats the keyboard as a stream of characters. 

## Stream Pipeline
A typical stream pipeline consists of three parts: 
- **Source**: The data source, such as a collection or an array 
- **Intermediate Operations**: These operations transform or filter the stream and return a new stream 
- **Terminal Operation**: This operation produces a result or a side-effect and terminates the stream 

### Creating a Stream 
Streams can be created from any other collection type. One of the easiest ways is to use the Stream object’s static of() method. It creates a finite stream of elements which is sequential and ordered. It works with any data type that supports Iterable. There are two overloaded versions: 

- *of(T t)*: Creates a sequential stream containing a single element. 
- *of(T... values)*: Creates a sequential ordered stream from the specified values. 

Other collection types such as Java’s lists and sets support the *stream()* method which returns a stream with all of the elements in the collection in the stream. It does not convert the collection into a stream, it creates a stream from the collection but leaves the original collection intact. 

<caption><strong>Code Example: Creating a Stream from a List</strong></caption>

```java
List list = Arrays.asList("java", "python", "node"); 
Stream stream = list.stream();
```

Maps also support the *stream()* method, but indirectly. There are three ways to create a stream from a map such as *HashMap*. 

<caption><strong>Code Example: Stream of key-value pairs</strong></caption>

```java
HashMap map = ...; 
Stream> entryStream = map.entrySet().stream(); 
```

<caption><strong>Code Example: Stream of keys</strong></caption>

```java
Stream keyStream = map.keySet().stream(); 
```

<caption><strong>Code Example: Stream of values</strong></caption>
 
```java
Stream valueStream = map.values().stream(); 
```

These methods allow you to perform intermediate and terminal stream operations on the map's entries, keys, or values. 

## Intermediate Operations
Intermediate operations are ***lazy*** and do not process the elements until a terminal operation is invoked. Common intermediate operations include: 

### Filters: 
*filter()*: Selects elements based on a predicate 

<caption><strong>Code Example: filter()</strong></caption>

```java
List filtered = Stream.of(1, 2, 3, 4, 5) 
    .filter(n -> n % 2 == 0) 
    .collect(Collectors.toList()); 
```

*map()*: Transforms elements from one form or data type to another 

<caption><strong>Code Example: map()</strong></caption>

```java
List mapped = Stream.of(1, 2, 3, 4, 5) 
    .map(n -> "Number " + n) // Implicitly converted to a String 
    .collect(Collectors.toList()); 
```

*flatMap()*: Flattens nested streams into a single stream 

<caption><strong>Code Example: flatMap()</strong></caption>

```java
List flattened = Stream.of(List.of(1, 2), List.of(3, 4)) 
    .flatMap(List::stream) 
    .collect(Collectors.toList());
```


### Ordering and Uniqueness: 

*sorted()*: Sorts the elements of the stream 

<caption><strong>Code Example: sorted()</strong></caption>

```java
List sorted = Stream.of(5, 2, 4, 1, 3) 
    .sorted()
    .collect(Collectors.toList());
```

*distinct()*: Removes duplicate elements from the stream 

<caption><strong>Code Example: distinct()</strong></caption>

```java
List unique = Stream.of(1, 2, 2, 3, 3, 4, 5) 
    .distinct() 
    .collect(Collectors.toList()); 
```

### Limiting and Skipping (paging): 
*limit(n)*: Restricts the stream to a specific number of elements 

<caption><strong>Code Example: limit(n)</strong></caption>

```java
List limited = Stream.of(1, 2, 3, 4, 5) 
    .limit(3) 
    .collect(Collectors.toList()); 
```

*skip(n)*: Discards the first n number of elements in the stream 

<caption><strong>Code Example: skip(n)</strong></caption>

```java
List skipped = Stream.of(1, 2, 3, 4, 5) 
    .skip(2) 
    .collect(Collectors.toList()); 
```

### Peeking: 
*peek()*: Allows performing an action on each element without modifying the stream 

<caption><strong>Code Example: peek()</strong></caption>

```java
List peeked = Stream.of(1, 2, 3, 4, 5) 
    .peek(System.out::println) 
    .collect(Collectors.toList()); 
```


## Terminal Operations
Terminal operations trigger the processing of the stream pipeline. They are often used with the *Optional\<T>* object. *Optional* is a class from the *java.util* package that will hold an object. It is used when a method’s return value may or may not be present. This helps avoid ***null pointer exceptions*** and provide a more expressive way to handle potentially absent values.

### Terminal operations:
*forEach()*: Performs an action for each element in the stream

<caption><strong>Code Example: forEach()</strong></caption>

```java
Stream.of(1, 2, 3, 4, 5)
    .forEach(System.out::println);
```

*collect()*: Accumulates elements into a collection or a single result

<caption><strong>Code Example: collect()</strong></caption>

```java
List<String> list = Stream.of("a", "b", "c")
    .collect(Collectors.toList());
```

*count()*: Returns the number of elements in the stream as a long value

<caption><strong>Code Example: count()</strong></caption>

```java
long count = Stream.of(1, 2, 3, 4, 5)
    .count();
```

*reduce()*: Combines the elements of the stream into a single value

<caption><strong>Code Example: reduce()</strong></caption>

```java
Optional<Integer> sum = Stream.of(1, 2, 3, 4, 5)
    .reduce((a, b) -> a + b);
```

*min()*: Returns the minimum element of the stream according to a provided comparator

<caption><strong>Code Example: min()</strong></caption>

```java
Optional<Integer> min = Stream.of(1, 2, 3, 4, 5)
    .min(Integer::compare);
```

*max()*: Returns the maximum element of the stream according to a provided comparator

<caption><strong>Code Example: max()</strong></caption>

```java
Optional<Integer> max = Stream.of(1, 2, 3, 4, 5)
    .max(Integer::compare);
```

*anyMatch()*: Checks if any elements of the stream match a given predicate

<caption><strong>Code Example: anyMatch()</strong></caption>

```java
boolean anyEven = Stream.of(1, 2, 3, 4, 5)
    .anyMatch(n -> n % 2 == 0);
```

*allMatch()*: Checks if all elements of the stream match a given predicate

<caption><strong>Code Example: allMatch()</strong></caption>

```java
boolean allPositive = Stream.of(1, 2, 3, 4, 5)
    .allMatch(n -> n > 0);
```

*noneMatch()*: Checks if no elements of the stream match a given predicate

<caption><strong>Code Example: noneMatch()</strong></caption>

```java
boolean noneNegative = Stream.of(1, 2, 3, 4, 5)
    .noneMatch(n -> n < 0);
```

*findAny()*: Returns any element from the stream

<caption><strong>Code Example: findAny()</strong></caption>

```java
Optional<Integer> any = Stream.of(1, 2, 3, 4, 5)
    .findAny();
```

*findFirst()*: Returns the first element of the stream

<caption><strong>Code Example: findFirst()</strong></caption>

```java
Optional<Integer> first = Stream.of(1, 2, 3, 4, 5)
    .findFirst();
```

*toArray()*: Collects the elements of the stream into an array

<caption><strong>Code Example: toArray()</strong></caption>

```java
Integer[] array = Stream.of(1, 2, 3, 4, 5)
    .toArray(Integer[]::new); 
```

These terminal operations are ***eager*** and consume the stream, meaning that once a terminal operation is invoked, the stream can no longer be used. They typically return a single value or perform a side effect, and they initiate the processing of the entire stream pipeline. 

<caption><strong>Code Example: Stream pipeline</strong></caption>

```java
//Filter even numbers, square them, and then prints the results 
List numbers = Arrays.asList(1, 2, 3, 4, 5, 6); 

numbers.stream() 
    .filter(n -> n % 2 == 0) 
    .map(n -> n * n) 
    .forEach(System.out::println); 
```


## Advantages of Streams 
Stream intermediate operations can support ***lazy processing***. Lazy processing in streams means that operations are deferred until a result is needed, so the elements of the stream are only processed once. This also means streams can be infinite, like System.in. Lazy processing significantly improves the performance of the entire pipeline of operations. ***Eager processing*** occurs when operations are executed immediately. This is associated with terminal operations. 

In addition to being lazy and eager, some stream operations are ***short-circuiting operations***, meaning they can terminate the processing early. For example, *limit()* and *skip()* are short-circuiting intermediate operations, while *findFirst()* is a short-circuiting terminal operation. 

## Summing It Up
Using streams allows developers to create more concise and efficient code for data processing tasks, especially when dealing with large collections or complex transformations. They allow declarative operations at a higher level of abstraction. This puts the focus more on what is happening and less on how to do it. They also improve code readability and provide a single approach for processing data regardless of the source.

# Advanced Topics

## Parallel Processing 
One of the key advantages of Java streams is the ability to easily switch between sequential and parallel processing. ***Parallel streams*** can utilize multiple threads to process data ***concurrently***. In other words, instead of processing one element at a time, streams make it possible on the right kind of CPU to process two or more elements at the same time. This can lead to significantly better performance on multi-core CPU systems, and are particularly useful when the order of execution doesn't affect the final result, and when elements are independent of each other.

<caption><strong>Code Example: Parallel processing</strong></caption>

```java
import java.util.List;
import java.util.Arrays;

...

List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

// The numbers will print in a random order due to parallel processing
numbers.parallelStream().forEach(n -> System.out.print(n + " ")); 
```

Parallel processing is an advanced topic and beyond the scope of this book. This was a major motivation for the introduction of lambdas and streams in Java 8.

# Summary

Lambdas and Streams were introduced in Java 8 and provide new language mechanisms and new ways to process collections. Lambdas allow small anonymous functions to be declared and executed without being tied to an object instance. They can be passed as a parameter to a method, or they can be returned from a method. They are also extremely useful for processing streams. 

Streams are a collection type intended for processing the data in the collection, not storing the data. All other collection types can generate a stream from their elements. Streams have a source, intermediate operations, and terminal operations. The stream does not actually process anything until the terminal operation which makes it very efficient. Some operations can also short-circuit which also makes them very efficient. 

Processing data in collections using lambdas and streams is more expressive and concise, which simplifies and clarifies the application code. Overall, they are a significant improvement to the language and a nice tool for any developer to add to their toolbox.

# Review Questions

## Short Answer
1. What are lambda expressions in Java, and why are they useful? 
2. Explain the differences between a traditional for loop and the forEach() method. 
3. What is lazy evaluation in streams, and why is it beneficial? 
4. How does the map() operation in streams differ from the filter() operation? 

## Code-based Questions
1. Write a lambda expression to calculate the square of a number. 
2. Given a list of numbers, use a stream to: 
	- Filter out even numbers.  
	- Square the remaining numbers. 
	- Collect the result into a list. 
3. Transform this method into a lambda expression: 
```java
public void printNames(List<String> names)
{
	for (String name : names)
	{
		System.out.println(name);
	}
}
``` 

4. Create a stream pipeline to: 
	- Sort a list of integers. 
	- Remove duplicates. 
	- Print the first three numbers. 

## True/False
1. Lambda expressions can have multiple return types. 
2. Streams modify the original data structure they are derived from. 
3. A method reference can be used as a shorthand for a lambda that calls a specific method. 
4. Intermediate operations in a stream are executed as soon as they are encountered. 

## Discussion 
1. Discuss the advantages of using lambdas and streams in modern Java development. 
2. When should you use a parallel stream over a sequential stream? What are the risks?
