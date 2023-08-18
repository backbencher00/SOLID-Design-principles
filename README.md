# SOLID-Design-principles
## S : Singleton Design principle
Defination :
    A class or a function should encapsulate one and only one aspect of functionality, ensuring that it doesn't become too complex or           tightly coupled.
    Normal Implementation : 
```
 class UserProfile {
    private String username;
    private String email;

    public UserProfile(String username, String email) {
        this.username = username;
        this.email = email;
    }

    public void displayProfile() {
        System.out.println("Username: " + username);
        System.out.println("Email: " + email);
    }

    public void saveProfileToDatabase() {
        // Code to save the profile to a database
    }
}
```
SDP implementation : 
```
class UserProfile {
    private String username;
    private String email;

    public UserProfile(String username, String email) {
        this.username = username;
        this.email = email;
    }

    public String getUsername() {
        return username;
    }

    public String getEmail() {
        return email;
    }
}

class UserProfileDisplay {
    public void displayProfile(UserProfile userProfile) {
        System.out.println("Username: " + userProfile.getUsername());
        System.out.println("Email: " + userProfile.getEmail());
    }
}

class UserProfileDatabaseManager {
    public void saveProfileToDatabase(UserProfile userProfile) {
        // Code to save the profile to a database
    }
}
```

## O : Open/Closed Principle 
Defination :
The Open/Closed Principle states that software entities (classes, modules, functions, etc.) should be open for extension but closed for modification. This means that you can add new functionality by creating new classes or modules without altering existing ones. In Java, you achieve this by using interfaces, abstract classes, and proper inheritance.
```
abstract class Shape {
    public abstract double calculateArea();
}

class Circle extends Shape {
    private double radius;

    public Circle(double radius) {
        this.radius = radius;
    }

    @Override
    public double calculateArea() {
        return Math.PI * radius * radius;
    }
}

class Rectangle extends Shape {
    private double width;
    private double height;

    public Rectangle(double width, double height) {
        this.width = width;
        this.height = height;
    }

    @Override
    public double calculateArea() {
        return width * height;
    }
}

class Triangle extends Shape {
    private double base;
    private double height;

    public Triangle(double base, double height) {
        this.base = base;
        this.height = height;
    }

    @Override
    public double calculateArea() {
        return 0.5 * base * height;
    }
}

public class AreaCalculator {
    public static double calculateTotalArea(Shape[] shapes) {
        double totalArea = 0;
        for (Shape shape : shapes) {
            totalArea += shape.calculateArea();
        }
        return totalArea;
    }

    public static void main(String[] args) {
        Shape[] shapes = {
            new Circle(5),
            new Rectangle(4, 6),
            new Triangle(3, 7)
        };

        double totalArea = calculateTotalArea(shapes);
        System.out.println("Total area: " + totalArea);
    }
}


```
### In this implementation:
The Shape class is an abstract base class that defines the contract for calculating the area of a shape.
Subclasses (Circle, Rectangle, Triangle) extend the Shape class and provide their specific implementations of the calculateArea method.
The AreaCalculator class has a calculateTotalArea method that accepts an array of shapes and calculates the total area by iterating through the array and invoking the calculateArea method on each shape.
If you want to add a new shape, such as a square, you can extend the Shape class and provide its implementation of the calculateArea method without modifying existing code.

## L : Liskov Substitution Principle
Defination :
)bjects of a derived class should be able to replace objects of the base class without affecting the correctness of the program
```
class Shape {
    // Common properties and methods for all shapes
    public double calculateArea() {
        // Default implementation, to be overridden by subclasses
        return 0.0;
    }
}

class Rectangle extends Shape {
    private double width;
    private double height;

    public Rectangle(double width, double height) {
        this.width = width;
        this.height = height;
    }

    @Override
    public double calculateArea() {
        return width * height;
    }
}

class Circle extends Shape {
    private double radius;

    public Circle(double radius) {
        this.radius = radius;
    }

    @Override
    public double calculateArea() {
        return Math.PI * radius * radius;
    }
}

```
In this example, both Rectangle and Circle are subclasses of Shape. They override the calculateArea method to provide their own implementations of area calculation.

Now, let's demonstrate the Liskov Substitution Principle by using these classes:

```
public class LSPDemo {
    public static void printArea(Shape shape) {
        System.out.println("Area: " + shape.calculateArea());
    }

    public static void main(String[] args) {
        Shape rectangle = new Rectangle(5, 10);
        Shape circle = new Circle(7);

        printArea(rectangle); // Output: Area: 50.0
        printArea(circle);    // Output: Area: 153.93804002589985
    }
}
```

## I : Interface Segregation Principle
Defination :
clients should not be forced to depend on interfaces they do not use. In other words, you should design your interfaces in a way that each client (class) only needs to implement the methods that are relevant to its specific requirements. 
we're designing an interface for a document management system. We want to ensure that different types of clients can interact with the system using interfaces that are tailored to their needs. 
#### Initial Design (Violating ISP):
```
interface Document {
    void open();
    void save();
    void print();
}

class TextDocument implements Document {
    @Override
    public void open() {
        System.out.println("Opening text document");
    }

    @Override
    public void save() {
        System.out.println("Saving text document");
    }

    @Override
    public void print() {
        // Text document printing logic
    }
}

class PdfDocument implements Document {
    @Override
    public void open() {
        System.out.println("Opening PDF document");
    }

    @Override
    public void save() {
        System.out.println("Saving PDF document");
    }

    @Override
    public void print() {
        // PDF document printing logic
    }
}

```
In this initial design, both TextDocument and PdfDocument are forced to implement the print() method even though the printing logic is different for each type of document. This violates the Interface Segregation Principle because clients that only need to work with specific document types are forced to implement methods that are irrelevant to them.

#### Refactored Design (Adhering to ISP):
```
interface Openable {
    void open();
}

interface Savable {
    void save();
}

interface Printable {
    void print();
}

class TextDocument implements Openable, Savable {
    @Override
    public void open() {
        System.out.println("Opening text document");
    }

    @Override
    public void save() {
        System.out.println("Saving text document");
    }
}

class PdfDocument implements Openable, Savable, Printable {
    @Override
    public void open() {
        System.out.println("Opening PDF document");
    }

    @Override
    public void save() {
        System.out.println("Saving PDF document");
    }

    @Override
    public void print() {
        System.out.println("Printing PDF document");
    }
}

```

In this refactored design, we have separate interfaces (Openable, Savable, and Printable) that clients can implement based on their specific requirements. This adheres to the Interface Segregation Principle, as clients are not forced to implement methods that they don't need.

## D : Dependency Inversion Principle
Defination :
1. High level module should not Dependent on low - level module, Both should dependent on Abstraction
2. It focuses on decoupling high-level modules from low-level modules by introducing abstractions (usually interfaces or abstract classes) in between. 
3. This allows you to depend on abstractions rather than concrete implementations, which makes your code more flexible and easier to maintain.
```
class EmailService {
    public void sendEmail(String message) {
        System.out.println("Sending email: " + message);
    }
}

class SMSService {
    public void sendSMS(String message) {
        System.out.println("Sending SMS: " + message);
    }
}

class MessagingApp {
    private EmailService emailService;
    private SMSService smsService;

    public MessagingApp() {
        emailService = new EmailService();
        smsService = new SMSService();
    }

    public void sendMessage(String message, String channel) {
        if (channel.equals("email")) {
            emailService.sendEmail(message);
        } else if (channel.equals("sms")) {
            smsService.sendSMS(message);
        }
    }
}

```
In this initial design, the MessagingApp directly depends on the concrete implementations of EmailService and SMSService. This violates the Dependency Inversion Principle because the high-level MessagingApp depends on low-level implementations.
```
interface MessageSender {
    void sendMessage(String message);
}

class EmailService implements MessageSender {
    @Override
    public void sendMessage(String message) {
        System.out.println("Sending email: " + message);
    }
}

class SMSService implements MessageSender {
    @Override
    public void sendMessage(String message) {
        System.out.println("Sending SMS: " + message);
    }
}

class MessagingApp {
    private MessageSender messageSender;

    public MessagingApp(MessageSender messageSender) {
        this.messageSender = messageSender;
    }

    public void sendMessage(String message) {
        messageSender.sendMessage(message);
    }
}

```
In this refactored design, we've introduced the MessageSender interface that both EmailService and SMSService implement. The MessagingApp now depends on the abstraction (MessageSender) rather than concrete implementations.

Now, when you use the MessagingApp, you can inject different implementations of MessageSender without modifying the MessagingApp class:

```
public class DIPDemo {
    public static void main(String[] args) {
        MessageSender emailSender = new EmailService();
        MessageSender smsSender = new SMSService();

        MessagingApp app1 = new MessagingApp(emailSender);
        MessagingApp app2 = new MessagingApp(smsSender);

        app1.sendMessage("Hello via email");
        app2.sendMessage("Hello via SMS");
    }
}

```
