# SOLID-Design-principles
## S : Singleton Design principle
Defination :
    A class or a function should encapsulate one and only one aspect of functionality, ensuring that it doesn't become too complex or           tightly coupled.
``` class UserProfile {
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
} ```

## O : Open/Closed Principle 
Defination :

## L : Liskov Substitution Principle
Defination :

## I : Interface Segregation Principle
Defination :

## D : Dependency Inversion Principle
Defination :
