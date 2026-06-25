# Module 3: Defensive Programming

# Introduction

> "One is not exposed to danger who, even when in safety is always on their guard."
> 
> **Publilius Syrus**

Defensive programming is an approach to software development that prioritizes anticipating and addressing potential problems before they happen. This involves writing code that can handle unexpected inputs or unforeseen processes without crashing or encountering errors.

The main goals of defensive programming include reducing bugs and problems, enhancing code comprehensibility and maintainability, and ensuring predictable software behavior despite unexpected inputs or user actions. Developers try to consider all possible scenarios that could lead to issues. Developers can also ensure code is of high quality by writing code in a clear, simple, and purposeful way and following best practices.

Another vital principle is input validation. Any time data comes from anywhere else reliable code will validate those inputs and ensure methods execute only with correct data. This includes checking if a variable is null before using it, among many other techniques. Handling errors gracefully when things do not go according to plan is also vital to keeping the application running.

## Learning Objectives
- [Defensive Programming](#defensive-programming)
- [Clean Code](#clean-code)
- [Input Validation](#input-validation)
- [Handling Errors](#handling-errors)
- [Exception Handling](#exception-handling)
- [Logging](#logging)
- [Advanced Topics](#advanced-topics)

# Defensive Programming

Most developers take the approach when they are first learning to write code of “just make it work.” As soon as the code does what is expected when everything is well behaved the code is considered "done". Unfortunately, nothing could be further from the truth.

While software absolutely must meet the requirements and work to be successful, it's also important to consider what could go wrong. Here are just a few examples:
- What if null was passed instead of an object instance?
- What if a user types a string when a number is expected?
- What if an empty collection or an empty string was passed to a method?
- What if a value is passed in that is not valid for the business rules?
- What if the network is down and the code tries to make a network connection?
- What if the code tries to read a file and the file is missing or inaccessible?

Anticipating what could go wrong and writing code that can gracefully handle those errors is a best practice and is known as ***defensive programming***. Defensive programming is a software development approach that aims to create robust, reliable, and secure code by anticipating and addressing potential issues before they happen. The primary goals of defensive programming are to:
1. Improve overall software quality by reducing bugs and vulnerabilities
2. Enhance code comprehension and readability
3. Ensure predictable software behavior, even under unexpected circumstances

There are a wide variety of things that can be done to achieve these goals. These include:
- **Input validation**: Thoroughly checking and sanitizing all inputs to prevent errors and security vulnerabilities
- **Anticipating edge cases**: Considering and addressing all possible scenarios, including unlikely ones, to prevent crashes or unexpected behavior
- **Code clarity**: Writing clear, easily understandable code that follows best practices such as the Single Responsibility Principle and Don't Repeat Yourself (DRY)
- **Error handling**: Implementing comprehensive error detection and handling mechanisms to gracefully manage unexpected situations
- **Secure coding practices**: Implementing measures to protect against common security vulnerabilities
- **Thorough testing**: Employing extensive unit testing, code reviews, and static code analysis to identify and fix potential issues early in the development process
- **Consistent error checking**: Regularly verifying the state of variables, function returns, and system resources throughout the code

Defensive programming is particularly crucial in high-stakes environments where software failures can have severe consequences, such as in aerospace, medical devices, or financial systems. If the code being developed has the potential to harm human life or cause large financial impact, then it should be subject to thorough defensive programming, testing, and debugging.

While defensive programming shares some similarities with normal good coding practices, it goes beyond standard practices by emphasizing ***fault tolerance*** and resilience in the face of unexpected inputs or system states. By adopting defensive programming techniques, developers can create more reliable and secure software that is better equipped to handle real-world challenges and maintain long-term stability.

# Clean Code

Clean, well-written code that is easy to understand, follows best practices, and is documented is vital. Code is written once, but it is read several times, often by several different developers.

## The DRY Principle
One of the biggest mistakes made in application development is writing the same logic in multiple places. Not doing this is known as the DRY principle (Don't Repeat Yourself). One of the biggest problems with this is when that logic needs to be updated to fix a bug or add a feature. If the same thing needs to be updated in multiple places, it's both tedious and error prone. The updates need to be applied to all instances of that code, and it's possible to forget to update it in one or more places. This can lead to intermittent bugs which are difficult to fix. Testing the application is more difficult sometimes too since the same block of code may need to be tested in multiple places.

## Self-Documenting Code
Another best practice for high quality code is to write it in such a way to be "self-documenting." This does not mean code with no code comments or Javadoc! ***Self-documenting*** code refers to code that is written in a way that clearly conveys what and how it works without the need for extensive comments or external documentation. In Java, this can be achieved through several techniques. 

One of the simplest things a developer can do to create self-documenting code is to use good names for variables and methods. 

Consider the following examples:

<caption><strong>Code Example: Variable names</strong></caption>

```java
// elapsed time in days 
int d; // Poor naming 
int elapsedDays; // Self-documenting 
```

<caption><strong>Code Example: Method names</strong></caption> 

```java
// Unclear 
public void process() 
{ 
  ...
} 

// Self-documenting 
public void calculateMonthlyRevenue() 
{ 
  ...
} 
```

Self-documenting code improves readability, maintainability, and reduces the need for extensive comments. It makes the code easier to understand for both the original author and other developers who may work on it in the future. While it doesn't eliminate the need for documentation, it should reduce the need for in-line comments and makes the code more intuitive to follow. 

Another important aspect of clean, high-quality code is the length of methods. One method should do one thing. If a method is doing a complex operation, break down the complex method into smaller, well-named methods. A good general rule of thumb is a method should be able to fit on the screen without scrolling. Here is an example where each step is separated into a helper method:

<caption><strong>Code Example: Helper methods</strong></caption>

```java
public void processOrder(Order order)
{
  if (isValidOrder(order))
  {
    applyDiscount(order);
    calculateTax(order);
    updateInventory(order);
    notifyCustomer(order);
  }
}
...
```

## Documentation
Documentation is also an important part of defensive programming because it helps communicate to other developers what the intention of the code is. Good documentation also outlines what valid inputs and ranges are. Explaining the result when valid and invalid inputs happen, such as return null, a sentinel value, or throwing an exception is also a vital component of good documentation. In Java, this is done with the language standard known as Javadoc.

<section class="callout info">
Oracle has an excellent Technical Article titled [How to Write Doc Comments for the Javadoc Tool](https://www.oracle.com/technical-resources/articles/java/javadoc-tool.html)
</section>

## Consistent Formatting
Consistent formatting is another aspect of high-quality code. Organizations will often have a style guide for a project. This document outlines what the look and feel of the code should be so any developer can read the code and know what structure to expect. This increases readability and therefore understanding. Consider this example versus the same code just shown and consider which is easier to read and understand.

<caption><strong>Code Example: Terrible formatting</strong></caption>

```java
public void processOrder(Order order) {
if (
isValidOrder(order))
{ applyDiscount(order);
    calculateTax(order);
      updateInventory(order);
  notifyCustomer(order);}

}
```

## Magic Numbers
Avoid using hard coded values in application code as well. Often called magic numbers, these are values that are too ambiguous in what they represent and could even change in the future. Instead, use named constants, which have two advantages:
- The name of the constant clearly describes its purpose.
- Changing its value is done in one place.

<caption><strong>Code Example: Using a magic number</strong></caption>

```java
// Poor practice 
if(employee.getDaysWorked() > 260) 
{ 
  ...
} 
```

<caption><strong>Code Example: Using a named constant</strong></caption> 

```java
// Using a named constant 
private static final int WORKING_DAYS_PER_YEAR = 260; 
if(employee.getDaysWorked() > WORKING_DAYS_PER_YEAR) 
{ 
  ...
} 
```

Now, if this value is needed in more than one place, the constant can be used everywhere, and if the value needs to be updated, then only the constant declaration would need to be updated. If magic numbers are scattered throughout the code, updating them everywhere is very difficult.


## Clever Code
If code is written in a "clever" way that shows off a developer's ingenuity but is difficult to understand, then it is more likely to lead to errors and mistakes. Clean, well-written code that is easy to understand is considered high quality, in part because it is easier to understand and maintain. Clever code, while often impressive to another skilled developer, can have significant drawbacks in real-world software development. A good measuring stick is to ask, "would I be able to read this in a year and understand what it is doing and why?"

<section class="callout info">
Clever code is often compact, with intricate functions performed in just a few lines, or uses a novel language construct to function. If the comments are longer than the code, rewrite it.
</section>

<caption><strong>Code Example: Clever code</strong></caption>

```java
int score = 75;
// Assign a letter grade using ternary statements
String grade = (score >= 90) ? "A" : (score >= 80) ? "B" : (score >= 70) ? "C" : (score >= 60) ? "D" : "F";
```

## Clear Code 

Clever code is often unreadable except to the person who wrote it, which increases application complexity and often tightly couples the components together. This makes it more difficult to debug and test. Maintaining software written in this fashion is more difficult, in part because as software evolves and changes these components often need to be rewritten. This approach also makes onboarding new developers to a team more difficult because of the challenges this adds to program comprehension.

<caption><strong>Code Example: Clear code</strong></caption>

```java
String grade;
// Assign a letter grade using if-else statements
if (score >= 90)
{
  grade = "A";
}
else if (score >= 80)
{
  grade = "B";
}
else if (score >= 70)
{
  grade = "C";
}
else if (score >= 60)
{
  grade = "D";
}
else
{
  grade = "F";
} 
```

# Input Validation

Input validation is an important best practice in software development that involves first checking any incoming data before using it. Input can come from several places, including method parameters, user input, files, or the network, among others. Checking these inputs ensures the incoming information meets expectations before being processed by an application.

Input validation is the process of verifying that data entering a software system meets expectations, is properly formatted, within an acceptable range, and free from potentially malicious content.

There are two general approaches to validating inputs. They are generically known as white-listing and blacklisting. With whitelisting, the application code defines and allows only known good inputs. With blacklisting, the application code tries to only block known bad inputs but allows everything else. Whitelisting is the recommended approach.

A very good example of the need to do this kind of validation happened on September 21st, 1997, in the United States Navy. The Cruiser USS Yorktown was participating in a training exercise off the coast of Virginia testing the integration of a new information system for the ship based on Windows NT. A crew member began troubleshooting a fuel valve that was physically closed but registered in the software as open. The technician tried to reset the fuel valve by entering a zero for one of the valve’s component properties into the system. The software recorded this value in the database and then attempted to perform a division operation by the valve property; a divide-by-zero arithmetic exception was thrown, not handled by the program, and the software system crashed. Since other ship systems depended on that piece of software, each of them, including those controlling the ship’s propulsion began to fail in a domino-like sequence until the ship stopped dead in the water. A complete reboot of the systems did not fix the problem either since the value was already accepted and stored in the database. The ship had to be towed back to port as a result. Had this happened during combat the ship likely would have been sunk with significant loss of life. Input validation would have prevented this.

Input validation is achieved by first examining the input before using it. One common real-world example involves validating that a string meets the correct format for a given type of information. For instance, a program would likely store an email address in a String object. There is nothing about a String object that would guarantee its value was an email address though, so before using that value as an email address the code should verify that it is formatted as an email address. Phone numbers are another type of data that would also be subject to this kind of validation. These are typically validated using ***regular expressions***, known as ***RegEx***.

<section class="callout info">
Regular expressions are a way to do pattern matching on strings.
</section>

Range checks are another common place to do input validation. Imagine giving a user a menu and asking them to choose options 1 - 5. Likely the code would read input from the keyboard and save it to an integer variable. Integers can have a huge range of positive and negative values in Java, but for the application logic the value needs to be between 1 and 5, inclusive.

<caption><strong>Code Example: User input without data validation</strong></caption>

```java
public int getUserInput()
{
  int input = 0;
  Scanner scan = new Scanner(System.in);

  System.out.print(“Enter a number between 1 - 5: “);
  input = scan.nextInt();
  return input();
} 
```

In this example the user is told to enter a number between 1 - 5, but there is no guarantee that they do. If the user types -11, then -11 is what is read into the input variable and returned. Likewise, if the user types 6, then 6 will be assigned and returned even though it isn’t correct for the application. There is no guarantee that the user will do what is expected. In fact, a malicious user trying to hack the system is very likely to deliberately provide invalid input. A simple check can be done like this:

<caption><strong>Code Example: User input with data validation</strong></caption>

```java
public int getUserInput()
{
  int input = 0;
  Scanner scan = new Scanner(System.in);
  
  do
  {
    System.out.print(“Enter a number between 1 - 5: “);
    input = scan.nextInt();
    scan.nextLine(); // flush the \n from the scanner
    
    if(input < 1 || input > 5)
    {
      System.err.println(“Invalid selection, try again”);
    }
  }while(!(input >= 1 && input <= 5));
  
  return input;
} 
```

Some other examples would be making sure an object has been initialized or that a collection has elements in it. Consider the following example:

<caption><strong>Code Example: Without object initialization check</strong></caption>

```java
public double calculateAverage(ArrayList<Integer> numbers)
{
  int sum = 0;
  double avg = 0.0;
  
  for(Integer i : numbers)
  {
    sum += i;
  }
  avg = (double) sum / list.size();
  
  return avg;
} 
```

This example will work well to calculate the average of a list of numbers, assuming that everything does what is expected. If the numbers parameter is an initialized list that is empty though, this will result in a ***divide by zero runtime error***. Similarly, if the numbers parameter is null, the result will be a null pointer runtime error. Input validation can prevent both errors.

<caption><strong>Code Example: Without object initialization check</strong></caption>

```java
public double calculateAverage(ArrayList<Integer> numbers)
{
  double avg = 0.0;
  
  if (numbers != null && numbers.size() > 0)
  {
    int sum = 0;
    
    for(Integer i : numbers)
    {
      sum += i;
    }
    
    avg = (double) sum / list.size();
  }
  
  return avg;
} 
```

Here the check is done as a single compound if statement. It’s important to do the null check first, where short circuit evaluation would skip the size check, since a call to *size()* would fail if the object is actually null.

<section class="callout info">
<strong>Short circuit evaluation</strong> is used in compound conditions such as this. If the condition is an AND ( && ), and the first one is false, then the compound statement will be false and there is no need to check the second condition. If the condition is an OR ( || ) and the first one is true, then the compound statement will be true and there is no need to check the second condition.
</section>

<caption><strong>Code Example: Incorrect (backwards) short circuit evaluation</strong></caption>

```java
if (numbers.size() > 0 && numbers != null) 
```

When evaluated in this order, if the numbers object was null then the *size()* method call would fail with a null pointer runtime error. 

The business requirements of the software would be used to determine what the correct behavior should be in this situation. In this example the result will be 0 if there are no numbers provided. Another reasonable alternative might be to pass the error to the block of code that called this method so the author of that block can choose how to deal with it. This is known as throwing an exception. Exception handling is discussed later in this chapter, and handling different types of exceptions is covered in an upcoming chapter.

## Input Validation Recap

### Best Practices
Some of the best practices of doing input validation include: 
- All inputs should be validated, regardless of where they come from 
- Check for null values first when dealing with objects 
- Implement validation as early as possible in the data flow 
- Leverage built-in validation functions and libraries when available 

### Benefits
There are many benefits to doing input validation, including: 
- Improved security against various attacks 
- Enhanced data integrity 
- Reduced risk of application errors and crashes 
- Improved user experience 
- Reduced debugging and troubleshooting 
- Compliance with security standards and regulations 

### Challenges
Sometimes doing input validation can be difficult. Some of the challenges include: 
- Balancing security with user experience 
- Knowing what the application should do for a particular invalid input 
- Handling complex or free-form inputs 
- Maintaining consistent validation across different parts of an application

# Handling Errors

Sometimes despite a developer's best efforts, things go wrong when an application is running. Most often this is due to an environmental factor that is outside the developer's control. Examples would include trying to open a file that was moved or had permissions locked down, trying to connect to a network resource when the service or network is down, or getting invalid or malformed input from the user or some other source. 

To provide the best experience possible to users, it is important to anticipate what can go wrong and try to work around them as much as possible to keep the application running smoothly. After an error has occurred there are generally two approaches to managing them: returning a sentinel value or throwing an exception.

## Sentinels
A ***sentinel value*** can be thought of as a message saying the code in question ran successfully or failed. Consider this example where *employees* is an ArrayList that has been initialized with *Employee* objects:

<caption><strong>Code Example: Sentinel value</strong></caption>

```java
public class EmployeeManagement
{
  ...
  public void removeEmployee(Employee employee)
  {
    employees.remove(employee);
  }
} 
```

Here the method accepts an *Employee* object as a parameter, and passes it to the remove method of a List. If the employee object is in the list, it will be removed, and the method will return control back to where the method was called. This would be the expected behavior under normal circumstances. 

What happens if the employee passed as a parameter is not in the list though? The control would still return to where the method was called, but there would be no indication that the employee passed as a parameter wasn't removed. 

As it turns out, the Java List's return type is a boolean. This boolean is a sentinel value that indicates if the operation was successful or not. The code could be updated as follows to use this:

<caption><strong>Code Example: Using a sentinel value</strong></caption>

```java
public static void main(String[] args)
{
  Scanner scan = new Scanner(System.in);
  EmployeeManagement em = new EmployeeManagement();
  
  boolean status = false;
  do
  {
    System.out.print("Enter first name: ");
    String first = scan.nextLine();
    
    System.out.print("Enter last name: ");
    String last = scan.nextLine();
    
    Employee emp = em.search(first, last);
    
    status = em.removeEmployee(emp);
    
    if (status == false)
    {
      System.out.println("Employee not removed. Try again.");
    }
  }while(status != true);
}
```

Any code calling this method could use this return value to check if the operation was successful.

<section class="callout info">
This is an example of Client-Server object interaction. Client code uses other objects to do their business logic, and Server objects provide a service to other pieces of code. 

In this example, the <em>EmployeeManagement</em> class is a client of the ArrayList, using it to complete its business logic. <em>EmployeeManagement</em> is also a server object for the class where the static main method is declared.
</section>

Here, the boolean indicator from the List object telling if the remove operation was successful or not is used to make sure that what the user wants to do happened. The code using the *EmployeeManagement* object uses this to track the operation and make sure it succeeded. 

This can work and is used in a lot of situations. This approach has two weaknesses though. The first one is rather obvious. If a method is already returning some piece of information, the return type can't be changed to a sentinel value. In the above example, it's implied that the `search` method would return an instance of an *Employee* object. There really isn't a way to add a boolean to that indicating success or not.

This can sometimes be worked around by returning null which can indicate a failure if the return type is an object. The application code then would check for null to indicate success or failure. Methods that return primitives cannot leverage this though because primitive data types cannot be null. 

The second aspect of this approach is that the return value can be ignored in a client class. Look at the first example again, where the remove method was called without using its return value:

<caption><strong>Code Example: Sentinel value</strong></caption>

```java
public class EmployeeManagement
{
  ...
  public void removeEmployee(Employee employee)
  {
    employees.remove(employee);
  }
} 
```

Here the *remove()* method did return a boolean value, but it wasn't assigned to a variable or used. When that happens, the return value is simply thrown away by the Java Runtime. 

In short, sentinel values can be a good approach to monitoring for errors, but this approach is not a guarantee that an error will be handled or even recognized. The error value can be completely ignored. To force a client class to deal with an error, another approach is needed.

# Exception Handling

Exception handling in Java is a way to deal with runtime errors and unexpected events. Essentially it allows a block of code to return a special object called an Exception that indicates there was a problem, instead of the code's normal return value when something unexpected happens. 

Since the return type of a method is already declared in the signature, returning an instance of this Exception object requires a new syntax. To return an Exception instance when something goes wrong, the throws keyword is used. Unlike sentinel values, exceptions cannot be ignored by a client class when they are thrown.

<section class="callout info">
<strong>Exception handling</strong> is a process of responding to and managing runtime errors or exceptional conditions in a program by transferring control to special handling code.
</section>

When one of these errors occurs in a server class, Java creates an instance of an Exception object. This object contains information about the error, including its type of error and the state of the program when it occurred. That exception is then passed back up the call stack to the application's client class where the method was called. This process is called ***throwing an exception.***

<section class="callout info">
There are many different types of exceptions, and they will be covered in more detail after the concept of inheritance is introduced.
</section>

## Try-Catch
A client class can intercept an exception when it is thrown and try to figure out the best way to handle the error. This is done with another new code construct, called a ***try-catch block***. Try-catch blocks are the main mechanism for handling exceptions and involve enclosing potentially error-prone code in a try block, followed by a catch block to handle if the exception is thrown. 

<caption><strong>Code Example: Try-catch statement format</strong></caption>

```java
try 
{ 
  // Code that may throw an exception 
} 
catch(Exception e) 
{ 
  // Handle the exception 
} 
```

The code in the try block will run until there is an exception thrown. If an exception is thrown, the control immediately drops into the catch block. This means any lines of code in the try block after the line that threw the exception get skipped. If no exception is thrown, then the catch block is completely skipped. 

Sometimes there will be things that need to happen regardless of whether there was an exception or not. The try-catch syntax can also have an optional block labeled ***finally***. The finally block is added after the try-catch and has any code that should run regardless of whether an exception was thrown or not. 

<caption><strong>Code Example: Try-catch statement format with finally</strong></caption>

```java
try 
{ 
  // Code that may throw an exception 
} 
catch(Exception e) 
{ 
  // Handle the exception 
}
finally
{
  //Code that should run either way
} 
```

<section class="callout info">
Examples of code in a finally block may include things like closing a file object or closing a network socket.
</section>

## Try-With-Resource
An alternative to the finally block that was introduced in Java version 7 is the ***try-with-resource*** construct. This simplifies resource management and exception handling by automatically closing resources, so long as they implement the *AutoCloseable* interface. This reduces the need for explicit resource cleanup in a finally block. Typical resources used this way include files and network connections.

<caption><strong>Code Example: Try-with-resource statement format</strong></caption>

```java
try (Resource resource = new Resource())
{
  // Use the resource
}
catch (Exception e)
{
  // Handle exceptions
} 
```

With this structure, the resource is declared and initialized within the parentheses following the try keyword. Another benefit is that the try-withresources approach automatically checks for null resources before attempting to close them. Assuming the resource is not null, the resource is automatically closed when the try block exits. This happens whether the code completed normally or encountered an exception, so no finally block or explicit closing of resources is required. 

If a client class does not wrap exception throwing code in a try-catch block, the exception will continue to be passed up the call stack. If no code catches the exception, then the Java Runtime will stop the application and try to print the exception information to the console. This provides a low-quality experience to users of the software.

## Throwing an Exception
Methods that might throw exceptions must declare this using the ***throws*** keyword in the method signature. As mentioned before, there are many different specialized types of Exception objects that will make more sense once the concept of inheritance is covered, but they all can be identified as instances of *Exception*. The syntax for writing a method with *throws* in the signature is like this:

<figure>
  <img class="align-center" src="https://computing.wvup.edu/bookstack/uploads/images/gallery/2026-05/image-1779216254653.png" alt="">
  <figcaption class="align-center">Figure 4.1: Method header format with throws</figcaption>
</figure>

Any client class code using this object and method would wrap the call to *calculateAverage()* in a try block, and in the catch block would handle the error. The exception object passed to the catch block would have the message "List is null or empty" in this example, which is available by calling the Exception parameter's *getMessage()* method. 

Some useful methods that are available from Exception include: 
- ***getMessage()***: Returns the string message from the code throwing the exception. Usually this has a user-friendly description of what went wrong. 
- ***getStackTrace()***: Gives access to the stack trace information printed by *printStackTrace()*. Returns an array of stack trace elements. 
- ***printStackTrace()***: This method prints a stack trace for this object on the error output stream.


<section class="callout info">
A <strong>stack trace</strong> is a snapshot of a program's execution at a specific moment, typically when an exception occurs.
</section>

Leveraging exception handling allows programs to gracefully manage errors, which improve code quality and user experience. They provide a way to recover from errors and give meaningful feedback when issues occur during program execution.

# Logging

***Logging*** in software development is the practice of recording events, actions, and information when an application is running. These can then be saved or sent somewhere for review either while the program is running or after it has finished. 

Logging does several important things for an application and the developers. Logs provide detailed information about the application’s behavior, making it easier to identify and fix issues. They capture errors, exceptions, and unexpected behaviors that occur while the application is running and write them out to a place where they can be accessed and reviewed after the application is done running. These logs can even be sent to someone else for review. 

Logs can also help track application performance, resource usage, and user activities. This information is crucial for optimizing the application and ensuring it meets performance requirements. In addition to performance monitoring, logs also play a critical role in security and auditing by creating a record of user actions, system events, and access attempts. These are essential for security monitoring and compliance with regulations. 

Logs also help developers to understand the flow of an application. Logs offer insights into the sequence of events and the flow of execution within an application as end users use the software. This helps developers understand how different components interact. Logs can also record how new features are being used, providing valuable data for product development and user experience improvements. If a user ran into a problem, the logs can be sent to the developer for review even though the developer wasn’t present when the user ran the program.

## Log Structure
Logging is a technique that has been around for decades, and there are many different tools that help solve this problem. No matter what tool is used for logging, there are several common components. A log entry typically includes a Log Level, which indicates what kind of message is sent. Examples of levels include Information, Warnings, Errors, and Debug information. This helps categorize log entries based on their importance.

<section class="callout info">
Most logging systems use the standard levels from the Syslog tool. Syslog has eight levels of log messages, which are Emergency, Alert, Critical, Error, Warning, Notice, Information, and Debugging.
</section>

Log entries also include a ***timestamp***. Timestamps record the date and time when the event being logged happened. This can be important for tracking down a sequence of events. In addition, a log entry typically includes details about the event being logged, such as user IDs, exception or error messages, or relevant data values such as parameters or other important variables. 

Logs are written in a structured format, which puts the same pieces of information in the same place for each log entry. This makes logs easier to search and analyze. 

The *java.util.logging* library’s *SimpleFormatter* will structure logs on two lines of a plain text document. The first line is a date time stamp and includes the class and method that generated the log message. The second line includes the log level and the log message.

<caption><strong>Logging Output:</strong></caption>

```
Jul 03, 2024 7:31:25 AM Main main 
INFO: This is an info message 
Jul 03, 2024 7:31:25 AM Main main 
WARNING: This is a warning message
```

It is important to strike an effective balance when logging. Too much general information can bury a log message that might be critical to fixing a problem, but too little logging might not log that same message. To be most effective, be sure to log meaningful information without exposing sensitive data such as database connection strings or passwords. Be sure to use appropriate log levels to balance verbosity and performance. Also, regularly rotate or replace log files to manage their storage effectively. A log that includes entries from five years ago through today will be more difficult to search through and will take up unnecessary space on the hard drive. 

Some logging libraries enable logging to a network destination. This enables several instances of the application to share logs which can help simplify managing logs across multiple installations, such as a desktop application in a company.

## Using java.util.logging
The built in libraries included in *java.util.logging* as part of the Java SDK provide an effective way to start logging. This package typically reads a configuration file for its settings, and then creates an instance of a *Logger* object.

The *logging.properties* file has a set of variables and their values to configure the Logger object. Using a file such as this enables the logging configuration to change without having to rebuild and redeploy the application. All that needs done is to update the file and restart the application.

<caption><strong>Code Example: logging.properties</strong></caption>

```
handlers=java.util.logging.FileHandler
java.util.logging.FileHandler.pattern = ./logfile.log
java.util.logging.FileHandler.limit = 50000
java.util.logging.FileHandler.append = true
java.util.logging.FileHandler.count = 1
java.util.logging.FileHandler.formatter = java.util.logging.SimpleFormatter
```

The fields in the file are:
- ***handlers***: Specifies where the log will be written
- ***java.util.logging.FileHandler.pattern***: Specifies the pattern for the log file names.
- ***java.util.logging.FileHandler.limit***: Sets the maximum size (in bytes) of each log file.
- ***java.util.logging.FileHandler.count***: Defines the number of log files to be used in rotation. If set to 1, only one log file should be used.
- ***java.util.logging.FileHandler.append***: Determines whether to append to existing log files or overwrite them.
- ***java.util.logging.FileHandler.formatter***: Specifies the formatter class to use for formatting log messages.
- ***SimpleFormatter*** writes the log as two lines in a text file
	- Formatter will write the log entry as an **XML document**

Once this file is created, the code can be added in a class to create and use the logger. This involves reading the *logging.properties* file, and creating an instance of a Logger object. This can be done in an object’s constructor or coded into the static main method.


```java
import ...

public class Main
{
  public static void main(String[] args)
  {
    // Read logging properties from the file
    try (InputStream is = Main.class.getClassLoader().getResourceAsStream("logging.properties"))
    {
      LogManager.getLogManager().readConfiguration(is);
    }
    catch (IOException e)
    {
      e.printStackTrace();
    }
    		
    // This creates a logger for the Main class, but changes if the class is ever renamed
    Logger log = Logger.getLogger(Main.class.getName());
    		
    log.info("This is an info message");
    log.warning("This is a warning message");
  }
}
```

<section class="callout info">
By using the Class object instance that is accessible from <em>this.getClass()</em> or <em>[ClassName].class</em>, this code will automatically update if the class is ever renamed. This is much more robust than hard coding the name of the class as a string
</section>

This general approach can be used in all the application’s classes and provide an effective way of recording exceptions in a catch block as well as recording other important information about the program’s performance and status.

## Logging Review
Logging is an essential practice throughout the software development lifecycle, from development and testing to production deployment and maintenance. It provides valuable insights that help improve software quality, performance, and reliability.

# Advanced Topics

## Static Code Analysis
In 1996, the Arian 5 rocket had its maiden launch, flight 501. This launch of a new heavy lift rocket went without a hitch until 37 seconds into the flight. This is when the rocket veered hard onto its side and controllers self-destructed the rocket as a safety precaution. 

The investigation into what went wrong was very detailed, but the key finding of the cause of the crash turned out to be an upgraded sensor that reported its value in a 64-bit float. This sensor sent its value to a computer system that was re-used from the Arian 4 rocket and was considered extremely reliable. The Arian 4 sensor and the computer that used that value worked with a 16-bit integer though. 64-bit information will only fit in a 16-bit field if the 64-bit value has 48 leading zeros. It took 37 seconds for the sensor to record a value that exceeded this and for the computer to crash.

This mismatch in data types was discovered through a process now known as ***static code analysis***. In fact, the investigation into this incident is where static code analysis was invented. Static code analysis involves examining source code without executing the program. It analyzes the code for potential issues, vulnerabilities, and adherence to coding standards early in the development process and can significantly reduce errors and improve code quality. 

Much has changed since 1996, including how static code analysis is carried out. Today, this is an automated process that uses specialized tools called ***static analyzers***. These scan the code automatically and help developers detect issues early in the development process. Often these tools are available in the developer environment.

## Logging Handler
Logging can be incredibly useful, but if an application is deployed in many locations on many computers, collecting and analyzing the logs can be extremely difficult or impossible. Because of this it is common to send logs to other places besides a file. Logs are sent to a destination through a log handler. Some common destinations include the console, a database, or a Syslog server on the network. 

## Logging Libraries
There are many different logging libraries in addition to the built-in *java.util.logging* package. Each of them has specific features and capabilities that enhance a developer’s ability to work with logs in some fashion. Since they are not part of the Java SDK, they must be added to the project through a package manager such as Maven or Gradle, or by providing the package’s JAR file directly and configuring the application to use this. 

Using 3rd party libraries opens the potential for a lot of functionality but comes with a risk. In 2021 the Log4J logging library was exploited in a vulnerability known as Log4Shell. Any Java application that used this logging library was potentially vulnerable. This is known as a ***Software Supply Chain attack***. 

Some of the most common 3rd party logging libraries include: 
- **Log4J2**: A logging library from the Apache foundation. Log4J2 is an updated version of the original Log4J logging framework, designed to provide improved performance, flexibility, and usability for Java applications.
- **Logback**: Logback is a powerful and flexible logging framework for Java applications, designed as a successor to the popular Log4J framework. It is developed by the same team that created Log4J and aims to provide a more reliable and efficient logging solution. 
- **tinylog**: tinylog is a lightweight, open-source logging framework designed for Java, Kotlin, Scala, and Android applications. It emphasizes simplicity, performance, and ease of use, making it an attractive option for developers who need a straightforward logging solution without the overhead of more complex frameworks.

## Log Analysis
Recording logs is a best practice, but that is only part of the logging equation. The other part, and arguably the most important part is analyzing and understanding what the logs are saying. 

***Log analysis*** is the process of reviewing and interpreting log data generated by applications. This is done to gain insights into the application’s performance, security, and operational issues. It is a critical component of system monitoring and management, and helps identify and troubleshoot problems, optimize performance, and enhance security. 

Log analysis typically involves log parsing, which means identifying only the logs that are of interest and filtering out the other logs. Once the logs that are relevant to the current situation are identified, the next step is to analyze this log data and try to identify patterns, anomalies, and trends. Tools that help visualize this information can be extremely valuable. 

Many tools and frameworks are available for log analysis, ranging from simple command-line utilities to comprehensive log management platforms. Some popular options include: 
- **ELK Stack (Elasticsearch, Logstash, Kibana)**: A powerful combination for collecting, storing, and visualizing log data. 
- **Splunk**: A commercial platform that provides advanced log analysis capabilities and real-time monitoring. 
- **Graylog**: An open-source log management tool that allows for centralized log collection and analysis. 
- **Prometheus and Grafana**: Often used for monitoring and alerting, these tools can also analyze log data when integrated with logging solutions.

# Summary

Defensive programming helps developers write code that is robust and reliable, even when unexpected things happen. By anticipating what might go wrong and gracefully recovering, an application can provide users with a much higher quality experience. In addition to ensuring predictable behavior, it also helps reduce bugs and improve maintainability. 

The key concepts of defensive programming include writing code in a clear, easily understood manner. Even more importantly though developers can improve the application by anticipating errors and unexpected inputs, managing exceptions effectively, and logging events when the application runs. These and other techniques help improve code quality and the end user’s experience when using the application.

# Review Questions

1. What is the primary goal of defensive programming? 
2. How does input validation improve software security? 
3. Explain the DRY principle and its importance. 
4. What are the key differences between whitelisting and blacklisting in input validation? 
5. Why should developers avoid magic numbers in code? 
6. What is the difference between a sentinel value and an exception for error handling? 
7. Describe a real-world example where lack of input validation caused a major system failure. 
8. What is a try-catch block, and how does it help in exception handling? 
9. List and explain at least three best practices for writing clean code. 
10. Why is logging important in software development? 
11. What are log levels, and how do they help in debugging? 
12. What are the advantages of using third-party logging libraries? 
13. How does static code analysis help prevent software failures? 
14. What is a log handler, and why is it useful? 
15. Describe two tools used for log analysis and their purposes.
