# Singleton Pattern

Let's you create a class which only has **one instance** and the class also provides a **global access point** to this *instance*.

- in a way we can say that *Singleton pattern* solves two problems at the same time, violating the Single Responsibility Principle (SRP).
    1. Returning the same obhect instance whenever a instance is requested.
    2. Providing a global access point to it.

### Implementation
- Each singleton clas will have a default constructor that is private, so that instnaces can not be created from outside of the class.
- A static maethod to get the instance of the object, this method under the hood generates the required instance if not present or return the instance if it has been already created.


1. Basic Implementation

```
// Online Java Compiler
// Use this editor to write, compile and run your Java code online

class Main {
    public static void main (String [] args){
        Singleton singleton = Singleton.getInstance();
        System.out.println(singleton.hashCode());
        Singleton singleton2 = Singleton.getInstance();
        System.out.println(singleton2.hashCode());
        
    } 
}

class Singleton{
    private static volatile Singleton instance;
    
    private Singleton(){}
    
    public static Singleton getInstance(){
        if(instance == null){
            instance = new Singleton();
        }
        return instance;
    }
}
```
- this is not thread safe , two threads reaching at the same time will end up creating two different instances.

2. Thread Safe Implementation

```
// Online Java Compiler
// Use this editor to write, compile and run your Java code online

class Main {
    public static void main (String [] args){
        Singleton singleton = Singleton.getInstance();
        System.out.println(singleton.hashCode());
        Singleton singleton2 = Singleton.getInstance();
        System.out.println(singleton2.hashCode());
        
    } 
}

class Singleton{
    private static volatile Singleton instance;
    
    private Singleton(){}
    
    public static Singleton getInstance(){
        if(instance == null){
            synchronized(Singleton.class){
                if(instance == null){
                    instance = new Singleton();
                }
            }
        }
        return instance;
    }
}
```

- this uses double checked locking, by using synchronized block, which locks the block on the given parameter Singleton.class in this scenario.
- this is thread safe.


3. Bill Pugh

```
// Online Java Compiler
// Use this editor to write, compile and run your Java code online

class Main {
    public static void main (String [] args){
        Singleton singleton = Singleton.getInstance();
        System.out.println(singleton.hashCode());
        Singleton singleton2 = Singleton.getInstance();
        System.out.println(singleton2.hashCode());
        
    } 
}

class Singleton{
    
    
    private Singleton(){}
    
    private static class Holder{
        private static  Singleton instance = new Singleton();
    }
    
    public static Singleton getInstance(){
        return Holder.instance;
    }
}
```
- this uses the rule that java implicitly takes care of thread safety while loading class.
- The inner Holder class is not loaded until getInstance() is called
- When it is loaded, the JVM initializes it in a thread-safe way
- That guarantees only one instance is created


4. Enum way

```
class Main {
    public static void main(String [] args){
    Singleton.Instance.instanceWork();
}}

enum Singleton{
    Instance;
    
    void instanceWork(){
        System.out.println("Instance work");
    }
}
```

🔥 Why enum Singleton is special
1. Reflection-safe

You cannot do:

Constructor<Singleton> c = Singleton.class.getDeclaredConstructor();

👉 It will fail

2. Serialization-safe

Normal Singleton breaks like this:

ObjectOutputStream → ObjectInputStream

👉 Creates a new object ❌

Enum:
👉 JVM ensures same instance ✅

3. Thread-safe by design

No need for:

volatile
synchronized
double-checked locking
🧩 When NOT to use enum Singleton
When you need lazy initialization with parameters
When Singleton must extend a class (enum cannot extend other classes)