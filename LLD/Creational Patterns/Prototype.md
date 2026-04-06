# Prototype Pattern

Prototype is a creational design pattern that lets you copy existing objects without making your code dependent on their classes.
The Prototype pattern delegates the cloning process to the actual objects that are being cloned.
- An object that supports cloning is called a *prototype*.

### Real World Analogy
- Since industrial prototypes don’t really copy themselves, a much closer analogy to the pattern is the process of mitotic cell division
- Certain chess board state, which needs to be replicated for practise.

** Basically make the object clone itself so that the cloning process can be avoided from outside of the class, whihc avoids unwanted complexities of cloning
- Deep Cloning : clone everything , that include making new reference of the objects inside the object
- shallow cloning : clone the class , and new instances are not created for the object references inside the class.

```
// Online Java Compiler
// Use this editor to write, compile and run your Java code online

class Main {
    public static void main(String[] args) {
        Car car1 = new Car();
        car1.numOfTyres = 45;
        
        Car car2 = car1.clone();
        
        System.out.println(car2.numOfTyres);
    }
}

interface Vehicle{
    Vehicle clone();
}


class Car implements Vehicle{
    public int numOfTyres;
    String color;
    
    public Car(){
        this.numOfTyres = 4;
        this.color = "black";
    }
    
    private Car(Car car){
        this.numOfTyres = car.numOfTyres;
        this.color = car.color;
    }
    
    @Override
    public Car clone(){
        return new Car(this);
    }
}
```