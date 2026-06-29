# Module 8: Graphical User Interfaces

# Introduction

> "A user interface is like a joke. If you have to explain it, it’s not that good." 
> 
> **Martin LeBlanc**


***Graphical User Interfaces*** (GUIs) revolutionized how people interact with computers. These interfaces have made technology more accessible, intuitive, and efficient. GUIs replace complex text-based commands with visual elements like icons, menus, and buttons, enabling users to interact with devices intuitively. They also significantly reduce the learning curve, allowing even nontechnical users to operate computers without prior knowledge of programming languages or commands. The development of GUIs was a key turning point in computing history, making computers accessible to a broader audience, including individuals with limited technical expertise. 

GUIs help streamline tasks by providing clear visual cues, simplifying many operations compared to command-line interfaces (CLIs). User multitasking is simplified through features like window management and tabs, enabling users to work on multiple applications simultaneously. GUIs are aesthetically pleasing because they often implement designs that make user interactions more enjoyable. Their engaging visuals encourage users to explore and interact with devices more frequently. Modern operating systems have helped introduce consistent design principles across software applications and platforms, enhancing usability and familiarity for users across different devices. 

The introduction and evolution of GUIs transformed computers from tools for experts into everyday devices accessible to all. They fostered widespread adoption of technology by simplifying interactions and enabling creativity across industries.

## Learning Objectives
- [What is a graphical user interface?](#what-is-a-graphical-user-interface) 
- [Constructing GUIs](#constructing-guis) 
- [GUI Components](#gui-components) 
- [GUI Layout](#gui-layout) 
- [Event Handling](#event-handling) 
- [Advanced Topics](#advanced-topics)

# What is a Graphical User Interface

Before graphical user interfaces, modern computers used (and still can use) a command line. When a developer uses an instance of a *Scanner* object to get input from the user, or prints output to the screen using *System.out.println()*, they are providing a command-line interface (CLI) for the application. This is because CLIs use a text-based interface, requiring users to type commands. In contrast, a GUI uses visual elements like icons, drop down menus and window elements to handle input and output. Because of this, GUI applications tend to have a much lower learning curve and be less error prone than CLI applications, although CLI applications tend to be faster and take fewer resources. 

In short, CLIs are ideal for advanced users, while GUIs are more accessible for beginners and casual users due to their ease of use and visual design. The choice between the two depends on the application requirements and the user's expertise.

# Constructing GUIs

In Java, there are three different libraries that can be used to construct GUIs. The original library was the ***Advanced Windowing Toolkit***, or AWT. AWT is part of the ***Java Foundation Classes*** (JFC) and provides a set of APIs for building platform-dependent GUI applications. One of the primary goals of Java though is to be platform independent. Because of this platform dependence in AWT, it was quickly superseded by the ***Swing*** library. 

The Swing library is a graphical user interface (GUI) toolkit for Java that is also part of the Java Foundation Classes (JFC), so it is bundled in the standard JDK. While Swing is built on top of AWT, it achieves platform independence by providing a standard cross-platform library for building GUIs in Java. Swing is considered the successor to AWT, and it allows developers to create desktop applications with rich and interactive user interfaces. 

The third library available for GUI development is ***JavaFX***. JavaFX was initially conceived as an upgrade to Swing but later became a standalone library that is not bundled with the JDK. This was done in Java 11 as part of Oracle’s attempt to implement a more modular architecture for Java and the JDK. JavaFX provides a set of APIs and tools for creating cross-platform GUI applications that support rich graphics, animations, and media playback, making it suitable for modern desktop applications needing these features. Despite this, JavaFX did not gain widespread adoption which also factored into its removal from the JDK. 

Regardless of the library used, a graphical application provides a user interface made of menus, components, layouts, and windows. These are the types of applications users are used to working with on modern computers. 

The process of creating a graphical user interface for an application is quite a bit different from a standard class and command line interface. GUIs take a lot more planning to get right because of this. In general, a developer needs to plan what components will be used on the screen, how those elements are arranged, and how the application will react to user input.

<section class="callout info">
Swing remains the most widely used GUI framework in Java and is the focus of this chapter.
</section>

# GUI Components

The **components** of a graphical user interface consist of all the individual parts that make up the entire user interface. These include things like menus, menu items, buttons, text fields, etc. There are many pre-made components in the Swing library for the most used GUI components, and developers can even create their own components. Learning these components and how to use them is a critical part of developing a GUI application. 

Arguably, the most important component of any GUI application is the ***Frame***. The Swing designers used a real-world analogy for the library, a literal window. Just like a real window frame, here a frame will hold everything in the GUI application. A frame is the root object that all other components are built on. In the swing library, this class is called ***JFrame***. The *JFrame* constructor takes a String as a parameter, which will be the title of the window. There are three parts to a frame, the title bar, an optional menu bar, and the content pane. 

To create a *JFrame* instance, the following packages should be imported:

<caption><strong>Code Example: Package imports for GUI development</strong></caption>

```java
import javax.swing.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener; 
```

Once these are imported, then a JFrame instance must be created and configured:

<caption><strong>Code Example: JFrame declaration and configuration</strong></caption>

```java
JFrame frame = new JFrame("Menu Example");
frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
frame.setSize(400, 300);
frame.setVisible(true); 
```

The methods listed may need a bit of explanation. The *setDefaultCloseOperation()* method takes an integer which will configure how the GUI will behave on close actions such as clicking the X on the title bar. There are several constants defined in *JFrame* to provide developer friendly names such as this one, *EXIT_ON_CLOSE*. The *setSize()* method will set the default window size when the application opens. This is in pixels for width and height. The last method, *setVisible()*, takes a boolean that controls if the frame is drawn on the screen or hidden. 

A *JFrame* instance has a container that holds the components of the user interface. This is called a content pane. Again, this comes from the real-world analogy of a window. In a real window the glass is known as a windowpane. The content pane of a *JFrame* is an instance of a class called ***Container***. Adding graphical components to the content pane is how they are added to the frame.

<caption><strong>Code Example: Retrieving the Container from a JFrame instance</strong></caption>

```java
Container contentPane = frame.getContentPane();
```

A wide variety of components are available in the Swing library to build graphical applications. Some of the most used components include: 
- **JMenuBar**: This class represents the menu bar displayed at the top of a window or frame. It serves as a container for menus. It can hold multiple menus. 
- **JMenu**: This class represents a pull-down menu that appears when clicked on the menu bar. It can contain menu items (JMenuItem) and separators to organize menu items visually. It can hold other instances of JMenu for sub menus, and menu items. 
- **JMenuItem**: This class represents individual menu items within a menu. These are actionable elements that perform specific tasks when clicked. Each instance functions like a button within the menu. 
- **JLabel**: This class is used to display a single line of text, an image, or both. It is a read-only component that cannot be edited by the user. 
- **JTextField**: This class is used to allow users to input and edit single-line text. It can initially be empty, or it can have initial text added that the user can then edit. 
- **JButton**: This class is used to create clickable buttons that perform actions when pressed. It can display text or an image icon, or both. 
- **JDialog**: This class is used to create custom dialog pop-up windows that can display information or gather input from the user. 
- **JOptionPane**: This is a utility class used to create standard dialog boxes such as message dialogs, confirmation dialogs, and input dialogs without needing extensive customization.

## Building a Menu Bar
Adding a menu bar to an application provides drop-down menu items for users to work with the application. They are very common but creating them is a multi-step process. This is because a menu bar consists of several related components working together to create the overall menu. An application typically only has one menu bar. 

<caption><strong>Code Example: Creating a menu bar</strong></caption>

```java
// Create the menu bar
JMenuBar menuBar = new JMenuBar();

// Create the menus to go on the menu bar
JMenu fileMenu = new JMenu(“File”); // File is what will be displayed for this menu
JMenu editMenu = new JMenu(“Edit”);
...

// Create the items for each element on the file menu
JMenuItem openItem = new JMenuItem(“Open”);
JMenuItem saveItem = new JMenuItem(“Save”);
JMenuItem exitItem = new JMenuItem(“Exit”);
...

// Associate an action with selecting the menu item
exitItem.addActionListener(event -> System.exit(0));
...

// Add menu items to the File menu
fileMenu.add(openItem);
fileMenu.add(saveItem);
fileMenu.addSeparator(); // Add separator
fileMenu.add(exitItem);
...

// Put the menu on the bar
menuBar.add(fileMenu);
...

// Put the menu bar on the frame
frame.setJmenuBar(menuBar); 
```

Associating the action taken with selecting the menu item involves registering an ***ActionListener*** to the component. This will be covered extensively later in the chapter, but for now, this line of code shows how to define an action using a lambda that will execute when the menu item is clicked:

<caption><strong>Code Example: Adding an ActionListener</strong></caption>

```java
exitItem.addActionListener(event -> System.exit(0));
```

To facilitate ***clean code***, these steps are best encapsulated into a private method, which could then be called from the main application class’s constructor:

<caption><strong>Code Example: Clean code - menu bar</strong></caption>

```java
private void addMenuBar()
{
  JMenuBar menuBar = new JMenuBar();
  ...
  frame.setJMenuBar(menuBar);
} 
```


## Creating Components
Each component in a GUI application needs to be built according to its own structure. Once created and configured, it can then be added to the content pane of the frame. Any graphical application will consist of several components working together in concert to support the overall application.

### JLabel
The ***JLabel*** object is used to display text and/or images in the window. The alignment can also be configured. Each of these properties can be changed using the corresponding set method. For instance, text can be changed by calling the label’s *setText()* method. To make any of these changes display on the screen, the application would need to call *JFrame*’s *repaint()* method. 

For a *JLabel* to display an image, pass the *JLabel* constructor an instance of an *ImageIcon*, instead of a String.

<caption><strong>Code Example: Display JLabel image</strong></caption>

```java
ImageIcon image = new ImageIcon("path/to/image.png"); 
JLabel imagelabel = new JLabel(image);
```

When added to the content pane, the image will be displayed in the window. Loading the image from the path should be wrapped in a try-catch in case the image is not on the filesystem. This will work with JPG and PNG images. This image can be changed using the *setIcon()* method in the same way the *setText()* method can change the text of a label. A *JLabel* instance can have both text and an icon. 

Several other aspects of a label can be customized. A label’s horizontal alignment can also be set using the *setHorizontalAlignment()* method. This takes a constant defined on the *JLabel* class such as *JLabel.CENTER*. The font used by a label can also be changed, by calling the *setFont()* method and passing a new font, including the size. A label can also display text in colors, using the *setForeground()* method.

<caption><strong>Code Example: Change JLabel font</strong></caption>

```java
JLabel label = new JLabel("My label");
label.setHorizontalAlignment(JLabel.CENTER)
label.setFont(new Font("Serif", Font.PLAIN, 14));
label.setForeground(Color.green);
```

### JTextField
The ***JTextField*** class allows users to input and edit single-line text into the application. The method *getText()* allows the developer -to retrieve the text a user typed, and the method *setText()* enables putting text into the text field programmatically. The width of the text field can be set using the constructor, by setting how many columns the field will display. 

If prompting the user for a particular type of data such as a number, the field will need to be read as a string using *getText()*, then parsed into the appropriate type.

<caption><strong>Code Example: JTextField</strong></caption>

```java
// Creates an empty text field.
JTextField defaultField = new JTextField();

// Creates a text field with specified width (in columns).
JTextField twentyColumnField = new JTextField(columns);

// Creates a text field initialized with specified text.
JTextField fieldWithInitialText = new JTextField(text); 
```

### JButton
A ***JButton*** is used to create clickable buttons that perform actions when pressed. Adding an action to a button click will be described in the Event Handling section. It can display text, an image (icon), or both. When the user clicks the button, it will generate an *ActionEvent*, which is sent to an *ActionListener* method, covered later. The *JButton* class also supports customization such as enabling/disabling states and adding tooltips.

<caption><strong>Code Example: JButton</strong></caption>

```java
// Creates a button without text or icon
JButton defaultButton = new JButton();

// Creates a button with specified text
JButton textButton = new JButton(String text);

// Creates a button with an image (icon)
JButton imageButton = new JButton(Icon icon); 
```

A button can also be deactivated and reactivated through the *setEnable()* method, which takes a boolean parameter. If set to false, the button is unclickable and greyed out. If set to true (the default) then the button is clickable and not greyed out.

<caption><strong>Code Example: JButton enable/disable</strong></caption>

```java
JButton button = new JButton(“Select”);

// After this, the button will be unclickable and greyed out
button.setEnable(false);

// After this, the button will be clickable again
button.setEnable(true); 
```

### Dialogs
A dialog is a pop-up window. The main Swing class to create dialogs is ***JDialog***. There are two general categories of dialogs: ***modal dialogs*** and ***non-modal dialogs***. A modal dialog blocks interaction with the application until the pop-up is closed, whereas a non-modal dialog does not block interaction. A common example of a modal dialog would be an open file dialog, where the application is behind the file open window until the user selects a file or closes the pop-up. Similarly, a common example of a non-modal dialog would be the help menu. Users likely want to use the system while also reading the help text, so it would make no sense to have this as a blocking popup. 

The ***JOptionPane*** class is a utility class with several static methods that help create standard dialog boxes. These include message dialogs, confirmation dialogs, and input dialogs. Each dialog also has an icon associated with it.

<figure>
  <img class="align-center" src="https://computing.wvup.edu/bookstack/uploads/images/gallery/2026-06/image-1781547515368.png" alt="">
  <figcaption class="align-center">Figure 9.1: Dialog Icons</figcaption>
</figure>

For most simple modal dialogs, you create and show the dialog using one of *JOptionPane*'s showXXXDialog methods, such as *showMessageDialog()*. This method displays a message and has an OK button as shown in figure 9.2.

<figure>
  <img class="align-center" src="https://computing.wvup.edu/bookstack/uploads/images/gallery/2026-06/image-1781547462642.png" alt="">
  <figcaption class="align-center">Figure 9.2: The showMessage() Dialog Box</figcaption>
</figure>

<caption><strong>Table 9.1: JoptionPane methods</strong></caption>

| JOptionPane Method  | Description                                                                                                                                            |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| showMessage()       | Show a modal information message. The icon can be changed by passing a constant from JOptionPane to the constructor, such as JOptionPane.ERROR_MESSAGE |
| showConfirmDialog() | Show a modal message with confirmation buttons (Yes/No/Cancel). Returns which button the user selected                                                 |
| showInputDialog()   | Show a modal message with a text input. Returns the string the user typed                                                                              |
| showOptionDialog()  | Shows a modal with multiple choices, returns the array index of the button the user selected                                                           |

A [full tutorial of using JOptionPane](https://docs.oracle.com/javase/tutorial/uiswing/components/dialog.html) and its methods is available from Oracle.

## Adding Components to the Window
Once components are created, they must then be added to the frame’s content pane. The order they are added in typically dictates where the components are in relation to each other. An example of adding a *JLabel* to display text on the screen would be:

<caption><strong>Code Example: Adding GUI components to the JFrame instance</strong></caption>

```java
JFrame frame = new JFrame(“Example app with components”);
Container contentPane = frame.getContentPane();
JLabel label = new JLabel(“Hello world!”);
contentPane.add(label);
frame.setSize(400, 300);
frame.setVisible(true); 
```

When executed, this code creates the window in figure 9.3.

<figure>
  <img class="align-center" src="https://computing.wvup.edu/bookstack/uploads/images/gallery/2026-06/image-1781547587566.png" alt="">
  <figcaption class="align-center">Figure 9.3: A basic Swing application running</figcaption>
</figure>

# GUI Layout

A layout manager can be applied to a content pane, which will help structure where components will be displayed. The content pane is a container and can have individual graphical elements added to it, much like an ArrayList can have elements added to it. When a layout manager is applied, the content pane uses the layout manager to arrange these elements on the screen. Deciding where the different components of an application will appear on the screen can be just as important as deciding which components to use. 

The Swing library provides several layout managers that can customize where components appear on the screen in different ways. For complex layouts, they can even be combined. 

The ***FlowLayout*** arranges components in a flow (left-to-right, top-to-bottom). Components wrap to the next row if there isn't enough space, much like text in a word processor. This is suitable for simple layouts with evenly spaced components. It is easy to use but offers no control over the wrapping of components.

<caption><strong>Code Example: FlowLayout</strong></caption>

```java
container.setLayout(new FlowLayout());
container.add(new JButton("Button 1"));
container.add(new JButton("Button 2")); 
```

The ***GridLayout*** will arrange components in a rectangular grid with equal-sized cells. All cells have the same dimensions. This is useful for layouts like calculators or forms with evenly spaced elements.

<caption><strong>Code Example: GridLayout</strong></caption>

```java
container.setLayout(new GridLayout(2, 2)); // Rows and columns
container.add(new JButton("1"));
container.add(new JButton("2")); 
```

The ***BoxLayout*** arranges components either vertically (*BoxLayout.Y_AXIS*) or horizontally (*BoxLayout.X_AXIS*). It defaults to vertical arrangement. Unlike the *FlowLayout*, it will not “wrap” components if they do not fit on the screen. This layout manager is used to align components in a single row or column.

<caption><strong>Code Example: BoxLayout</strong></caption>

```java
container.setLayout(new BoxLayout(container, BoxLayout.Y_AXIS));
container.add(new JButton("Button"));
```

The ***BorderLayout*** is a more complex layout and divides the container into five regions: North (header), South (footer), East (right sidebar), West (left sidebar), and Center (main content). Components are placed in one of these regions. Each region can have its own layout within the region as well. This is ideal for creating a main application window with multiple related components.

<caption><strong>Code Example: BorderLayout</strong></caption>

```java
container.setLayout(new BorderLayout()); 
container.add(new JButton("North"), BorderLayout.NORTH);
```

<figure>
  <img class="align-center" src="https://computing.wvup.edu/bookstack/uploads/images/gallery/2026-06/image-1781547714079.png" alt="">
  <figcaption class="align-center">Figure 9.4: BorderLayout Example</figcaption>
</figure>

In addition to these there are a few others for specialized situations, including: ***GridBagLayout*** (Complex layouts requiring precise control), ***CardLayout*** (Wizards), ***GroupLayout*** (GUI Builders), and ***SpringLayout*** (dynamic layouts based on runtime conditions). Layout managers are applied to a content pane. Once applied, anything added to the content pane will be placed on the screen using the layout’s structure automatically.

## Nesting Layouts
Complex layouts can be created by combining layouts together in different areas of the window. A simple example of this involves using nested layouts inside a BorderLayout. The BorderLayout uses four borders and a center. To achieve this, a new component is needed, the ***JPanel***. A JPanel is used as a windowpane for part of the application, so it is effectively a smaller container on the application window. 

A JPanel instance takes a layout manager as a parameter to its constructor. Elements are added to the panel, then the panel is added to the master panel where the nested layout is needed.

<caption><strong>Code Example: JPanel</strong></caption>

```java
JFrame frame = new JFrame("Nested Layouts Example");
frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
frame.setSize(600, 400);
frame.setLayout(new BorderLayout());

// NORTH: Panel with FlowLayout
JPanel northPanel = new JPanel(new FlowLayout());
northPanel.add(new JButton("North Button 1"));
northPanel.add(new JButton("North Button 2"));
northPanel.add(new JButton("North Button 3"));
frame.add(northPanel, BorderLayout.NORTH);

// Repeat for south
...

// EAST: Panel with BoxLayout (Vertical alignment)
JPanel eastPanel = new JPanel();
eastPanel.setLayout(new BoxLayout(eastPanel, BoxLayout.Y_AXIS));
eastPanel.add(new JButton("East Button 1"));
eastPanel.add(Box.createVerticalStrut(10)); // Add spacing
eastPanel.add(new JButton("East Button 2"));
eastPanel.add(Box.createVerticalStrut(10));
eastPanel.add(new JButton("East Button 3"));
frame.add(eastPanel, BorderLayout.EAST);

// Repeat for west
...

// CENTER: Panel with GridLayout
JPanel centerPanel = new JPanel(new GridLayout(2, 2)); // 2 rows, 2 columns
centerPanel.add(new JLabel("Label 1", SwingConstants.CENTER));
centerPanel.add(new JLabel("Label 2", SwingConstants.CENTER));
centerPanel.add(new JLabel("Label 3", SwingConstants.CENTER));
centerPanel.add(new JLabel("Label 4", SwingConstants.CENTER));
frame.add(centerPanel, BorderLayout.CENTER);

// Display the frame
frame.setVisible(true);
```

In this example code, the *BorderLayout* is applied to the main application, and then a *JPanel* instance is created with a *FlowLayout*. Components are added to this panel, then the panel itself is added to the frame’s North. This would be duplicated with a second panel for the South, so that both the application’s header and footer would use a horizontal layout and wrap any elements that may otherwise go off the screen. 

Another *JPanel* is then created using a *BoxLayout* with vertical alignment. Components are added to this panel, then the panel is applied to the frame’s East location. This would be duplicated for the West, so that both application’s sidebars would use vertical layout for their respective elements. 

The center then uses another *JPanel* with a 2x2 grid layout. Four elements are added, which will be placed in each cell of the 2x2 grid. When this panel is added to the frame’s center location, the grid will be displayed in the center of the window. 

This type of nested layout takes planning and forethought. A whiteboard, sketch paper, or even a napkin can be invaluable when planning. Complex layouts can be achieved using this technique if carefully planned and implemented.

# Event Handling

To understand the difference between a console application’s processing and a GUI application’s processing, consider how a command-line application gets information from the user: First a prompt is displayed asking for one specific variable, then the application waits for the user to provide a response. This repeats for the second variable, then the third variable, etc. until all the things needed to perform an action are collected. As soon as the last piece of information is provided, then the application processes that information and typically produces output. The user cannot change the order of the prompts to provide information in a different order. This is known as ***imperative programming***. 

Next, consider how a graphical application gets information from the user: Typically, there will be multiple form fields with labels, and the user can fill them out in any order. Nothing happens with these fields until the user clicks a button typically. That button click creates an event, which is passed to a method that will do the business logic associated with that event (processing the fields of a form in this example). This is known as ***event driven programming***. Examples of events in an application may include button clicks, mouse movements, and keyboard input. 

While creating components and laying them out on the window are important and sometimes challenging, a GUI application is still effectively useless unless it can do something for the user. Events are created through user interaction with the GUI environment. A key aspect of event driven programming is the Event Source. Essentially this is the Swing component that generates an event. Examples of components that can generate events are the *JButton*, *JTextField*, and *JFrame*. In most circumstances, the event source is what will determine the action the application will take when the event happens. Swing has objects to represent these, known as ***ActionEvent*** and ***MouseEvent***. 

If a component can create an event when a user interacts with the system, then something needs to receive that event to take the appropriate action. This is known as an ***event listener***. An event listener is an object that waits for and responds to events, and this is where a graphical application’s business logic is implemented. To handle an event, a listener must implement a specific interface such as *ActionListener* or *MouseListener* and register it with the event source (an instance of a *JButton* for example). Registering the listener with the source simply associates the listener with the source so the source knows where to send the event when it is generated. 

The event listener will then implement event handlers. An event handler is a method or set of methods in listeners that define how to respond to an event. For example, the *actionPerformed()* method implemented for an *ActionListener* interface is intended to process button click events.

## Implementing Event Listeners
When a button is clicked or a menu item selected, the component in question raises an *ActionEvent*. If a mouse button is clicked or the mouse is moved, a *MouseEvent* is raised. Similarly, when a frame is maximized, minimized, or closed, a *WindowEvent* is raised. These are the most common, but certainly not all the event types that are possible through Swing. 

Any object can become an event listener for any of these events if it implements the appropriate interface. If an object is registered as a listener, then it will be notified about any events it listens to. Essentially this means an instance of the object will be created and the registered event handler will be called, passing the event object as a parameter. Once the listener correctly implements the interface, it can be registered with the component it needs to listen to. 

There are three different approaches to creating listeners, each with their own strengths and weaknesses. These are: 
- Centralized event listener 
- Lambda event listeners 
- Nested class event listeners 

### Centralized Event Listeners 
The ***centralized event listener*** approach is the simplest. Essentially one class implements the event listener for the entire application. For small applications such as Windows Notepad with only a very few actions total this can work very effectively. This does not scale up very well though. Imagine a piece of software like Word or Excel, or your favorite video game. How many different individual actions can each of those pieces of software do? It would be thousands of different actions at a minimum. With this approach, handling all of that would be done in one method, most likely via an enormous if-else-if or switch statement. 

To use a centralized event handler, one class will implement the appropriate *Listener* interface. For the *ActionListener* interface, this means implementing the *actionPerformed()* method in the class. This method takes an *ActionEvent* object that was created by the user when a button or menu was clicked as the only parameter. Using that parameter, the method will determine which component created the event, and then take the appropriate action. 

On the component in question, registering the listener is done with the *addActionListener()* method. This method takes the class implementing the listener as its parameter. Essentially this tells the component where to send an event. Assuming the GUI layout and *actionPerformed()* method were all in the same class, registering the event listener would look like this:

<caption><strong>Code Example: Centralized event handler</strong></caption>

```java
JButton button = new JButton();

// Register this class as the listener
button.addActionListener(this);
...

public void actionPerformed(ActionEvent event)
{
  if(event.getSource() == button)
  {
    // Do button click things
    ...
  }
  ...
}
```

Any time the button component was clicked, an event from the button instance would be passed to the *actionPerformed()* method as the source of the event. This method would then test if the event source was that specific button, and if it is then run the code associated with that button click. 

Think back to the earlier example regarding scalability. On a large application every single component instance would have to be uniquely named across the entire application, even if they were in different packages. This is why the centralized event listener is rarely used.

### Lambda Event Listeners
One alternative to the centralized event handler is to instead use lambdas. Lambdas have several advantages and only a few disadvantages as event handlers. Lambdas are declared as part of the component itself, so the action taken by the component is directly implemented as part of the component when it is created. Since lambdas are anonymous, there is no danger of a name conflict or other overlap with different components. These together mean that using lambdas is extremely flexible and scalable. 

Declaring a lambda as an action listener is done directly in the listener method. For the *addActionListener()* method it looks like this: 

<caption><strong>Code Example: Lambda event listener</strong></caption>

```java
component.addActionListener(event -> 
  // Do the action for this event 
); 
```

With this approach, there is no need to test the source of the event, because the lambda is declared directly on the source of the event. 

Unfortunately, as anonymous methods there is not an easy way to use a lambda in more than one place. If the same action were going to be coded on more than one component, then due to the anonymous nature of lambdas the same implementation would have to be written twice. This is one of the disadvantages of the lambda approach to event handling. Despite this, using lambdas is a widely used approach for implementing listeners.

### Nested Class Event Listeners
There are some listener interfaces that require more than one method. These include ***KeyListener***, ***MouseListener***, and ***MouseMotionListener***. Because of this, none of these can be implemented as a lambda function. There are two approaches for this, both of which create a class just for implementing the interface in question. They are named inner classes and anonymous inner classes.

#### Named Inner Classes
The obvious approach to the problem these interfaces present is to create a separate class and implement the required interface. An instance of this class would be created and registered as the listener. There are some drawbacks to creating such a regular class in a project on par with the other application classes. 
- This separate class would have no access to private fields in the class that generates the event 
- The separate class is very tightly coupled to the class using it as a listener. In fact, it is highly likely that this class will only ever be used by the specific class using it as a listener

Java does provide a nice alternative to this that provides the best of all worlds though, known as an ***inner class***. An inner class is declared inside of another class, like this:

<caption><strong>Code Example: Inner class declaration format</strong></caption>

```java
public class OuterClass
{
  ...
  class InnerClass
  {
    ...
  }
  ...
} 
```

An instance of an inner class is automatically attached to instances of the outer class. In fact, they can only exist together because the inner class exists only inside of the outer class. The inner class is considered a direct component of the outer class. The inner class can also see and access private fields and methods of the outer class, just like the other two approaches.

<caption><strong>Code Example: Inner class declaration</strong></caption>

```java
public class OuterClass
{
  ...
  private class MouseHandler implements MouseListener
  {
    public void mouseEntered(MouseEvent event)
    {
      ...
    }
    
    public void mouseClicked(MouseEvent event)
    {
      ...
    }
  }
  ...
} 
```

Using the private inner class as an event listener would be done the same as using any other class instance. An instance of the inner class is created just like a regular class when used as an event listener. In this example the class is anonymously created when it is registered:

<caption><strong>Code Example: Adding event listener to a component - nested inner class</strong></caption>

```java
component.addMouseListener(new MouseHandler());
```

<section class="callout info">
Named inner classes are implemented at the bottom of the outer class as a general best practice for code style.
</section>

#### Anonymous Inner Classes
Using an inner class to solve the problem of multi-method interfaces works well. Since there is almost always only one instance of the inner class used due to its tight coupling to the component it handles events for, there is an alternative approach. This approach involves creating an anonymous inner class when registering the event listener. Essentially this declares the class method in place as part of the interface:

<caption><strong>Code Example: Anonymous inner class</strong></caption>

```java
component.addMouseListener(new MouseListener() {
  public void mouseEntered(MouseEvent event)
  {
    ...
  }
  public void mouseClicked(MouseEvent event)
  {
    ...
  }
  // Other methods in the MouseAdapter that need to be overridden
});
```

This works very well, allowing the implementation of the listener to be written as though it was part of the component it receives the event from. Of course, implementing an interface means every method must be implemented, whether this particular component uses them or not. Such is the nature of interfaces. 

Recognizing this as a potential problem, the Java API provides a non-operational implementation of these interfaces via abstract ***Adapter*** classes. One such example is the ***MouseAdapter*** class. This can be subclassed and just the methods needed for a particular component can be written. This gives the best of both worlds!


<caption><strong>Code Example: MouseAdapter</strong></caption>

```java
component.addMouseListener(new MouseAdapter() {
  public void mouseClicked(MouseEvent event)
  {
    ...
  }
  // Other methods in the MouseListener don’t need to be implemented if not needed
});
```

This looks a lot like lambdas because it is implemented as a part of the component instead of as a separate class and therefore has all the same advantages. 

This is no doubt confusing because the class implementation is being written inside the component’s *addMouseListener()* method much like lambdas are. And just like lambdas, this cannot be reused elsewhere. This is acceptable in this situation though because these handlers are almost always specifically for the component they are being registered on, so there would never be more than one instance anyway. Since inner classes are almost always only used only once, why not declare it in the one place it is used? Named inner classes are implemented at the bottom of the outer class as a general best practice for code style. 

The result is the same as a named inner class, but here the need to declare it separately is bypassed. This created a class and its implementation without naming it. In the above example a subclass of *MouseAdapter* was declared and the *mouseClicked()* method was implemented. All other methods from the interface used the non-operational implementation from *MouseAdapter* so there was no need to implement them to satisfy the interface contract. 

An anonymous inner class has all the advantages of named inner classes and lambdas. They can work with private fields and methods of the outer class, and they can use local variables and method parameters in their methods just like any other implementation. 

This approach has the disadvantage of making code hard to read and confusing. After all, an entire class is being declared as a parameter to a method! Generally, these should be used for short classes and clear, well understood implementations. If every method in an interface needed an override, it would be better to do that in a named inner class for clarity.

## Quick Review
To summarize, the steps needed to create a functional GUI using Swing are: 
- Create a JFrame with a layout 
- Create GUI components and add them to the window container 
- Implement an event listener interface such as ActionListener or MouseListener 
	- This can be centralized, lambdas, inner classes, or some combination 
- Register the listener with the component that will generate the events

# Advanced Topics

## Customer Graphics and Painting
Developers can use the Graphics and Graphics2D classes to create custom drawings, animations, or visual effects in a graphical application. These classes make it possible to draw shapes like lines, rectangles, and circles. They can also apply transformations such as scaling the graphics and rotating them. In addition, these classes make it possible to use colors, gradients, and textures for advanced visual effects. Overall, these are extremely useful for custom charts, game graphics, or artistic designs among other things.

## Pluggable Look-and-Feel
Swing supports an approach known as ***pluggable look-and-feel*** (PLAF), which allows developers to change the appearance of their applications dynamically. This enables applications to have different themes, allowing a custom look and feel for different users on the same application. This is extremely handy when creating applications that require branding or a consistent design across platforms.

## Advanced Components
In addition to the components described in the chapter, Swing provides several advanced components for complex user interfaces. These include: 
- **JTree**: Displays hierarchical data structures 
- **JTable**: Creates tables with customizable models for data display 
- **JSpinner**: Provides a numeric or object-based spinner control 
- **JEditorPane**: Displays rich text or HTML content 

These components are especially effective when developing file explorers, spreadsheet applications, or web-based GUIs.

## Drag-and-Drop Functionality
Swing can also implement drag-and-drop interactions using the ***TransferHandler*** class. This functionality enables dragging files or objects between components or external applications, which is useful for file upload systems or interactive dashboards.

## Accessibility and Internationalization
Two major concerns for modern applications are accessibility and internationalization. Accessibility refers to the application’s ability to support screen readers and high-contrast visibility for users who have a physical disability. Swing integrates APIs for creating accessible GUIs that support screen readers and keyboard navigation using the ***AccessibleContext*** class. 

Internationalization on the other hand refers to the ability of an application to support country and region-specific language and symbology for things such as dates, times, and money. Swing provides the ***ResourceBundle*** class to load localized strings dynamically based on the current user’s locale.

<section class="callout info">
Since the word is spelled differently in the United States and Great Britian, it is often abbreviated as <strong>i18n</strong> because both spellings have 18 characters between the first and last letter.
</section>
