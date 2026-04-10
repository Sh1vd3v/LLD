# Facade Pattern


### Implementation
```
class Main {
    public static void main(String[] args) {
        PizzaFacade pf  = new PizzaFacade();
        pf.makePizza();
    }
}

class PizzaFacade{
    Cheese cheese;
    PizzaBase pb;
    AddVeggies av;
    BakePizza bp;
    
    PizzaFacade(){
        cheese = new Cheese();
        pb = new PizzaBase();
        av = new AddVeggies();
        bp = new BakePizza();
    }
    
    public void makePizza(){
        pb.makeBase();
        cheese.addCheese();
        av.addVeggies();
        bp.addToOven();
        bp.removeFromOven();
    }
    
}

class Cheese {
    public void addCheese(){
        System.out.println("Adding cheese to base");
    }
}

class PizzaBase {
    public void makeBase(){
        System.out.println("making fresh base..");
    }
}

class AddVeggies{
    public void addVeggies(){
        System.out.println("sprinkling veggies on top");
    }
}

class BakePizza{
    public void addToOven(){
        System.out.println("In goes the pizza");
    }
    
    public void removeFromOven(){
        System.out.println("Coming out hot ....");
    }
}
```