# Being a Successful Software Developer

# Introduction

> “Success is no accident. It is hard work, perseverance, learning, studying, sacrifice and most of all, love of what you are doing or learning to do.”
> 
> **Pele, Brazilian Soccer Player**

If you are here reading this, then it is likely because you have a goal you are trying to achieve. Most likely that goal is to eventually step into a career as a software developer or software engineer. These are careers that are in high demand and require a lot of skill. Because of this, they command high salaries. 

No matter what your motivation is, to succeed in this field you need to build a strong foundation by understanding not just how to write code, but more importantly understanding the way of thinking that is involved in creating code and computer programs. While this book teaches programming using Java, on a bigger picture level it is only using Java to teach how to program. To be successful you should focus on logical thinking, such as how to solve problems step by step and understanding algorithms instead of memorizing syntax. Different languages have different syntax, but at their heart they all use the same basic structures to operate. 

## Learning Objectives
- [Realistic Expectations](#realistic-expectations)
- [Plan First](#plan-first)
- [What is Object-Oriented Programming](#what-is-object-oriented-programming)
- [Tools of the Trade](#tools-of-the-trade)
- [Never Stop Learning](#never-stop-learning)

# Realistic Expectations

Programming a computer is hard at first, so don’t expect to master everything the first time you see it or use it. One of the most important skills any developer can master is debugging errors and solving unexpected problems. Becoming proficient can take months or years and it can be frustrating at times. A lot of people give up because it is not easy, but sticking with it will pay off. 

Estimating how long writing a program will take is one of the most difficult things to do in this field, because it’s impossible to estimate how long it will take to troubleshoot a problem or even estimate what problems will crop up. Almost always when we are asked how long it will take to do something the first estimate assumes there will be no problems along the way, but realistically very few things work the first time. 

This is an expectation that new students often have, that a program will run correctly the first time they write some code. Almost nothing works perfectly on the first attempt. It is a lot like writing a paper for school. An outline is like the planning phase where you figure out what parts of the code will implement different parts of the program. The first time the code is written is like a rough draft. To get an A paper, you would likely have to revise the draft several times to improve it. Writing software is the same way. This is normal and not something to get frustrated about, it is just part of the process.

# Plan First

Most software is developed with a structured approach called a ***Software Development Life Cycle (SDLC)***. The SDLC is a methodology used to plan, design, develop, test, and maintain software applications. It consists of several phases that guide the development process from inception to deployment and maintenance. Regardless of the exact approach used, all variations of the SDLC share some common aspects. 

Software is typically developed in phases. The first phase involves gathering requirements and analyzing the software and customer needs. The second phase involves designing the solution both at a high level, known as architecture, and at a lower level. Once the requirements and the initial design are known, the next phase is to begin implementation of the software. This is where developers write code, turning the design into a working software application. As the software is written and once it is completed the application will be tested to make sure the implementation meets the specifications. The testing phase is often intermingled with the implementation phase. Once all parts of the application are shown to work, the application is deployed so people can use the software application. This phase may involve training users and transitioning from an old system, known as a legacy system, to the new system. After deployment, the software enters the maintenance phase. This is where developers monitor its performance, fix any issues that arise, and implement updates or new features as needed. 

The common System Development Lifecycle models are ***waterfall***, ***agile***, and ***spiral***. The waterfall model was first described in the early 1970’s as an idealized approach to software development. It tries to do each phase once with the goal of creating a complete piece of software at the end that meets all the requirements. This is extremely difficult, and realistically as software engineers and developers understand the problem better it is not unusual to go back and re-work previous phases. This model should only be used for small applications. 

The agile model was first recognized with the release of the Agile Manifesto in 2003. There are many different variations of agile, but they all prioritize having several small updates to software and letting customers guide development priorities. Instead of having one release of a completed project, agile will attempt to release a working application that is good enough to get started and continuously evolve it with small incremental updates based on the business needs of the organization. This works well for small and medium sized projects. 

The third approach is the spiral model, first described in 1986 by Barry Boehm. The spiral model also uses an iterative approach and includes a risk assessment phase in each iteration. This is a carefully planned approach that does well with medium and large projects with a lot of risk but is overkill for small projects. 

Regardless of the model used, each approach provides structure to the software development process. By following an SDLC methodology, development teams can produce high-quality software that meets user needs while minimizing risks and optimizing resources throughout the development process. 

It is important to note that each model starts first with planning. Planning is vital to successful software development. It’s often very tempting to just jump in and start writing code, after all, that’s the fun part! On all but the smallest of programs this is not a successful approach. Planning what objects will be needed and how they will interact makes the development process much smoother and more likely to succeed. One of the best things a developer can do is to write the ***Javadoc*** of a class or method first. This helps put in context what a class or a method will need to do before figuring out how it will do it. 

The best recipe for success is to set several small, achievable goals as you write a program, and test frequently. Also, don’t move forward with the next thing until the component you are working on now is done. Moving forward to something else when the current component is still broken simply compounds the first problem because you often cannot test the next piece of the program without going back to fix the part that was skipped over. Divide and conquer is the name of the game. 

There are two ways this applies to you as a student. First, be sure to give yourself plenty of time to work on exercises and assignments. Do not wait until the last hour before an assignment is due to start it. The best thing you can do is start the assignment before your last class in each lesson. This way if there are unforeseen problems you can ask for help. The other way this applies is when looking at other students in the class. Everyone learns at their own pace and develops their own style over time. Focus on improving your own skills as you learn and do not worry about anyone else.

# What is Object-Oriented Programming

***Object-Oriented Programming (OOP)*** is an approach to programming that organizes code around the concept of objects, which are instances of classes. A good way to think of an object is like a noun in English: it is a software representation of a person, place, thing, or idea. This approach helps create reusable, modular code by representing real-world entities as objects that contain both data (attributes) and behavior (methods).

## Disadvantages of Object-Oriented Programming
Despite these advantages, object-oriented programming does have some challenges as well. Concepts like classes, objects, inheritance, abstraction, and polymorphism can be complex and challenging for new programmers to grasp and apply effectively. The thought process involved in object-oriented programming may not be natural for some people, requiring abstract thinking in terms of objects.

In addition to object-oriented design, object-oriented languages often do not run as fast compared to procedural or functional languages. There are additional abstraction layers such as the Java Virtual Machine and the fact that objects store both data and methods. That means the object-oriented programming approach can consume more memory and CPU resources than other approaches. Given ***Moore's Law*** and the current hardware capabilities of most computers the practical impact of this is negligible in most situations though.

Object-oriented programming may not be suitable for all types of problems, as it's not a universal approach. For instance, no major operating system is written in an object-oriented language. It is very powerful and flexible though and is effective at solving most software development problems.

## Advantages of Object-Oriented Programming
Object-oriented programming has several advantages when it comes to solving problems in software development compared to other approaches. Object-oriented programming helps with code reusability. An object can be reused across different parts of a program or even in different projects if it is designed and implemented well. This is possible because object-oriented programming lends itself to ***modularity***. Programs are divided into smaller, manageable units, making development, maintenance, and teamwork easier. The modular nature of object-oriented programming facilitates collaborative development among teams, and this also makes this approach well-suited for large, complex software systems. In fact, this approach has been so successful it has been implemented in most popular programming languages, including Java. 

The key concepts of object-oriented programming include ***classes***, ***objects***, ***encapsulation***, ***abstraction***, ***inheritance***, and ***polymorphism***. Classes are the blueprints or templates for creating objects. A class defining the structure (***attributes***) and behavior (***methods***) of that type of object. A class is essentially a complex custom data type that a developer creates. An ***object*** on the other hand is an ***instance*** of a class that encapsulates data and functionality. 

As an analogy, think of a Car class, with a Make, Model, and Year attribute. Every car object will have these three attributes. Imagine what a car can do: it can start, stop, and drive. The class defines these attributes as field variables and implements these actions as methods. This is the template for a car, but it isn’t a car. Now imagine a developer creates a Car instance from the blueprint Car class. Say it’s a 2024 Chevrolet Corvette. That Corvette object instance will have its own make (Chevrolet), model (Corvette), and year (2024). Next the developer creates a 2025 Buick Regal instance of a Car. This Regal instance also has a make (Buick), a model (Regal), and a year (2025). 

Both cars can start, stop, and drive, but if the Corvette drives, that doesn’t mean the Regal also drives. They both can take the same action because as instances of Car they have the same methods, but running a method on one object instance only affects that specific instance. This is the concept known as encapsulation, which is a key feature of object-oriented programming. Encapsulation is the bundling of data and methods that operate on that data within a single object instance. 

Object-oriented programming also facilitates abstraction. Abstraction is the simplification of complex systems by creating classes that only have the information the application needs to solve its problems. This is done by only creating the properties and behaviors the application needs and ignoring real-world things that are not needed for the application. A good example of this is to think of all the things that are on a real car that are not represented by these three properties and these three methods. 

Object-oriented programming has multiple ways to reuse code. This is a very important capability that makes object-oriented programming very effective and efficient at solving similar problems. One of the most important ways to do this is through something called inheritance. Inheritance is a way to let a new class (a ***subclass*** or ***child class***) add to an existing class (a ***superclass*** or ***parent class***) without having to re-write everything already created in the existing class. 

Inheritance also leads to another capability with a weird name, polymorphism. This is the ability of objects to change between types of classes, assuming they are part of the same inheritance hierarchy. In other words, if one class inherits from another and adds extra attributes and methods, it still has everything the parent class has in terms of attributes and methods. A subclass or child class can therefore substitute in anywhere the superclass or parent class is needed because it has everything it needs to be an instance of the parent class; it just also has a few extra things. 

In short, object-oriented programming provides a structured approach to software development that aligns closely with how we perceive and interact with objects in the real world. This makes it an intuitive and powerful paradigm for creating robust and flexible software systems.

# Tools of the Trade

Earlier it was stated that this book teaches programming using Java, but on a bigger-picture level it is only using Java to teach how to program. Writing software involves using several tools, and while the particular tool may be specific to a language or environment pretty much all software development will involve the same types of tools. Becoming proficient in the use of the tools is vital to a successful career. 

An ***Integrated Developer Environment (IDE)*** is probably the most common tool every developer will use regardless of the language or type of application being developed. An IDE is a single piece of software that helps write, document, debug, test, and deploy code through the software development process. It provides a single, cohesive interface for all the development tasks, making it easier for developers to manage their work. Features include a source code editor where developers write and edit source code. This may include syntax highlighting and intelligent code completion. A compiler or interpreter is also readily available in an IDE, to convert the source code into machine-readable format. 

One of the most useful tools in any IDE is the ***debugger***, which allows a developer to pause the execution of the code and inspect the values in variables at that spot, known as a ***breakpoint***. A good debugger will let the developer change these values to test their impact on the code, move forward one line at a time, move forward to the next breakpoint, or even move into a method or function being called. This ability to watch what happens line by line as the code executes is invaluable to troubleshooting. 

***Unified Modeling Language***, or ***UML diagrams***, are a key tool in software development to quickly communicate the design of a piece of software. There are many different diagrams in the UML standard, but the most used include ***Class diagrams***, ***Sequence diagrams***, ***Use Case diagrams***, and ***Activity diagrams***. Creating a complex piece of software often starts with creating UML diagrams. 

***Code comments*** are something every language supports. Code comments are text in the source code of a program that the compiler or interpreter ignores so they have no impact on the functionality of the code. These are added by developers to enhance the understanding of the code, for themselves and for others who will read the code later. Students often hate writing code comments, but they are absolutely vital for creating high-quality applications that are easy to understand, maintain, and enhance in the future. Most languages support C-style code comments, which come in two flavors. These are end-of-line comments and multi-line comments.

<caption><strong>Code Example: Single line comments</strong></caption>

```java
// Everything after // is ignored
```

<caption><strong>Code Example: Multi-line comments</strong></caption>

```java
/* 
* Everything between the '/*' 
* and '*/' is ignored 
* even across multiple lines 
*/
```

Source code documentation tools are also a key feature of most developer environments. In Java, the standard way to write documentation is in a format known as ***Javadoc***, although many other languages have a similar format and capability. The classes and methods documented this way can then have these code comments interpreted by the ***Javadoc tool***, which will then generate static web pages any developer can then read in a web browser while trying to understand and use those classes or methods. In addition, there are tools that can interpret source code and automatically build UML diagrams such as Class and Sequence diagrams.

***Source code management (SCM)*** or ***version control*** tools are also available as both standalone tools and components built into the IDE. The most widely used tool for this is ***git***, but there are others as well, including ***Subversion*** and ***Mercurial***. Each of these tools manages and tracks changes to source code, including who made the changes, when, and why. This creates a comprehensive history of the source code and allows the code to be rolled back to previous versions if a bug or error is accidentally introduced. IDEs almost always have this capability integrated into them, but there are also stand-alone tools that can be used as well. The git tool has a very powerful command-line interface.

***Generative AI*** is another tool that is becoming more prominent in the industry. Generative AI is a form of AI that can create content, including writing code. These are relatively new, disruptive technologies in the industry, and while they seem great on the surface they come with several potential pitfalls, including security, quality, and intellectual property issues. For students, using AI-generated code will hinder the learning process. AI generated code seems like a quick shortcut, but it will prevent developing a deep understanding of programming principles, debugging skills, and the ability to write high-quality, maintainable code. Students need to understand the underlying logic and structure of code. Generative AI has a place in the industry and may have a place in your career, but for the sake of learning do not use generative AI in this course. 

Along with these there are several other tools developers will need to learn to use to master their trade. These include testing suites, logging frameworks, configuration management, 3rd party library management, and automated build tools. Managing secrets such as passwords and API keys is also important because these are sensitive and shouldn’t be readily shared but still need to be accessible. Static code analysis and security scanning are also important. All these things are broadly encapsulated under the umbrella of Software Engineering. In short, there is a lot to being a developer beyond just writing code!

# Never Stop Learning

A popular quote says, “repetition is the mother of skills.” What does that really mean though? In short, it means that to really learn anything you must work with it, review it, study it, and apply it several times. Learning to be a software developer is no exception to this. Nobody can learn to be a developer by sitting and listening to a lecture on a topic once, take no notes and not actively participate, and expect to apply anything later. 

To really learn what is presented in this book or any book, a student should read the chapter before the lecture, take notes on it, then listen and actively participate in the lecture by asking questions and adding to their notes, and then applying what they learned by writing code. This constant immersion is what it takes to master anything, especially this. As an analogy, think about your favorite movie. You have likely watched it multiple times, and each time you watched it you probably noticed something new in it, details that you missed the first time. 

There are a lot of people who have five years’ worth of one year of experience, meaning they start in their career and never question if there is a better way or a newer technology that will improve what they are doing. In short, these people never grow or learn once they start in their career. They are often the first to be let go when a company needs to lay someone off. To be successful you should embrace challenges. This career is one of the best because you will get to solve interesting problems and implement some fascinating ideas. Do not be afraid to ask and offer help. You won’t know everything because the tech industry is ever evolving and changing. You will never be bored in this field! Staying curious and never stopping learning are the keys to success and growth.

# Summary

Being a successful software developer is much more than learning to write code in one programming language. A successful software developer is a problem solver who likes challenges and wants to understand why something works, not just how to do it. Understanding this and understanding that it takes time to create a good piece of software, often revising parts of the program more than once to get it just right is important. Knowing how to plan before trying to write a piece of software will also lead to much better results than just diving in headfirst. 

Of course, to be effective it is also important to know what the tools of the trade are and how to use them. There are a lot of common tools used to develop software, regardless of the language the software is written in. Understanding what each tool does and how they relate to each other is important. More important though is to never stop learning and improving.Being a successful software developer is much more than learning to write code in one programming language. A successful software developer is a problem solver who likes challenges and wants to understand why something works, not just how to do it. Understanding this and understanding that it takes time to create a good piece of software, often revising parts of the program more than once to get it just right is important. Knowing how to plan before trying to write a piece of software will also lead to much better results than just diving in headfirst. 
Of course, to be effective it is also important to know what the tools of the trade are and how to use them. There are a lot of common tools used to develop software, regardless of the language the software is written in. Understanding what each tool does and how they relate to each other is important. More important though is to never stop learning and improving.

# Review Questions

1. Research three different Java IDEs. List the following information about each of them: 
	- Name 
	- Version 
	- Website 
	- Features
      
2. Watch the following YouTube video from Lucid Software titled [UML Class diagrams](https://www.youtube.com/watch?v=6XrL5jXmTwM), and answer the following:
	- Explain what a class diagram is and what it looks like 
	- Explain the three sections of a class diagram and what information is in each 
	- Explain the visibility of items in a class diagram 
	- Explain the difference between class properties and methods 

3. Watch the following YouTube video from Smart Draw titled [All About UML Activity Diagrams](https://www.youtube.com/watch?v=Wf_xlagfHmg), and answer the following:
	- Explain what an activity diagram is intended to show and communicate 
	- Explain each of the components on an activity diagram 
	- What can an Activity Diagram show that a traditional flow chart cannot 

4. Read Oracle's [How to Write Doc Comments for the Javadoc Tool](https://www.oracle.com/technical-resources/articles/java/javadoc-tool.html), and answer the following:
	- Explain the syntax of a Doc comment, including what starts and ends a ***Javadoc*** comment, and how it differs from a regular multi-line comment in Java. 
	- List and explain where these comments go in the source code 
	- List and explain the two parts of a Doc comment. 
	- Explain what a block tag is with examples. 
	- What is significant about the first sentence in a Javadoc comment? 
	- Why should descriptions go beyond just the API name? Provide a good and a bad example of this to illustrate the point. 
	- What is the order of tags and where does each tag go? 
	- Which tags are required and which are optional? 

5. Read JetBrains' [Javadocs](https://www.jetbrains.com/help/idea/javadocs.html#javadoc-code-style) article, and answer the following:
	- Describe two ways IntelliJ helps write Javadoc comments.
