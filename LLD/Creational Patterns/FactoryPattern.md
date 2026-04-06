# Factory Pattern
This creational pattern let's you create a instance of object at runtime (based on various factors like environment, user requirements etc).

*Real World Analogy*
1. **Payment System** : different types of payment system unified under a single interface
2. **Delivery Logistics** : different ways to ship a parcel, unified under a single interface

Advanced Techniques implement a registry of different implementations of objects(shown below in example), this allows the registration to happen in individual implementations.


### Sample Code
The below code uses a registry which replaces the need for a if - else in the factory class. Each new class can register itself in the registry.
this implementation uses a supplier which is a abstract class starting from java 8 which provides a get methid that returns a object of type T (Supplier < T >)

```
import java.util.function.Supplier;
import java.util.Map;
import java.util.HashMap;

//Main method
class Main {
    public static void main(String[] args)  throws ClassNotFoundException {
        
        Class.forName("SMSNotification");
        Class.forName("EmailNotification");
        Class.forName("LetterNotification");
        
        Notifications notification = NotificationFactory.getInstance("SMS");
        notification.notifyUser("this might be a factory but its great");
        
        
    }
}

//Notification interface : used for abstracting notification types.
interface Notifications{
    void notifyUser(String message);
}

//Concrete class 1 : implements the interface
class SMSNotification implements Notifications{
     static{
        NotificationFactory.addNotificationType("SMS", SMSNotification::new);
    }
    @Override
    public void notifyUser(String message){
        System.out.println("notified user through SMS : " + message );
    }
}

//Concrete class 2 : implements the interface
class EmailNotification implements Notifications{
     static{
        NotificationFactory.addNotificationType("EMail", EmailNotification::new);
    }
    @Override
    public void notifyUser(String message){
        System.out.println("notified user through Email :" + message);
    }
}

//Concrete class 3 : implements the interface
class LetterNotification implements Notifications{
    static{
        NotificationFactory.addNotificationType("Letter", LetterNotification::new);
    }
    @Override
    public void notifyUser(String message){
        System.out.println("notified user through Letter : " + message);
    }
}

//Factory class : responsible for generating and returning an instance.
class NotificationFactory {
    
    private static Map<String, Supplier<Notifications>> registry = new HashMap<>();
    
    public static void addNotificationType(String type, Supplier<Notifications> supplier){
        registry.put(type, supplier);
    }
    
    public static Notifications getInstance(String instanceType){
        Supplier<Notifications> notifications = registry.get(instanceType);
        if(notifications == null){
            System.out.println("not there");
            throw new RuntimeException();
        } else
        return notifications.get();
    }
}
```