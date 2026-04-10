# Flyweight Pattern

an object that only stores the intrinsic state is called a flyweight.

Where does the extrinsic state move to? Some class should still store it, right? In most cases, it gets moved to the container object, which aggregates objects before we apply the pattern.

- intrinsic state - read only properties 
- extrinsic state - properties that keep changing, by iteraction from outside by other objects.

### Flyweight and immutability
Since the same flyweight object can be used in different contexts, you have to make sure that its state can’t be modified. A flyweight should initialize its state just once, via constructor parameters. It shouldn’t expose any setters or public fields to other objects



```
import java.util.*;

// Flyweight (Intrinsic State)
class Car {
    private String brand;
    private String engine;

    public Car(String brand, String engine) {
        this.brand = brand;
        this.engine = engine;
    }

    public void display(CarContext context) {
        System.out.println(
            "Brand: " + brand +
            ", Engine: " + engine +
            ", NumPlate: " + context.getNumPlate()
        );
    }
}

// Extrinsic State (Context)
class CarContext {
    private String numPlate;

    public CarContext(String numPlate) {
        this.numPlate = numPlate;
    }

    public String getNumPlate() {
        return numPlate;
    }
}

// Flyweight Factory
class CarFactory {
    private static Map<String, Car> carPool = new HashMap<>();

    public static Car getCar(String brand, String engine) {
        String key = brand + "-" + engine;

        if (!carPool.containsKey(key)) {
            System.out.println("Creating new Car object for: " + key);
            carPool.put(key, new Car(brand, engine));
        }

        return carPool.get(key);
    }
}

// Client
public class Main {
    public static void main(String[] args) {

        Car car1 = CarFactory.getCar("BMW", "26BET");
        CarContext ctx1 = new CarContext("KA01AB1234");
        car1.display(ctx1);

        Car car2 = CarFactory.getCar("BMW", "26BET");
        CarContext ctx2 = new CarContext("KA02CD5678");
        car2.display(ctx2);

        Car car3 = CarFactory.getCar("Audi", "XYZ123");
        CarContext ctx3 = new CarContext("KA03EF9999");
        car3.display(ctx3);
    }
}
```