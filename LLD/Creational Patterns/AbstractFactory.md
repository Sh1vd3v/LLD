# Abstract Factory Pattern

This is sort of an extension of factory pattern which allows users to generate specific types of classes as per need basis. (important to note **As per need basis**)

This is used when we need to create multiple products of similar category that are used together or function well together.

*Real World Analogy*
1. Buttons and menus for MAC vs Windows : the button types and menu buttons are specific to Mac and Windows respectively. The button and menu of Mac will not work with windows.
2. Furniture Factory : a old school factory would produce old style of table, cahr and sofas. Whereas a modern factory would produce modern style table, chair and sofas.


### Example Code

```
class Main {
    public static void main(String[] args) {
        FurnitureFactory fac = FactoryChooser.factorySelector("new");
         fac.chairMade().makeChair();
         // the above logic can be improved by using DI etc.
    }
}


//Factory selector : can be imprived using DI etc
class FactoryChooser{
    public static FurnitureFactory factorySelector(String type){
        if( type == "old") return new oldStyleFacotry();
        else if (type == "new") return new newStyleFacotry();
        else throw new RuntimeException();
    }
}

// Main Chair interface
interface Chair{
    void makeChair();
}

// Main Table interface
interface Table{
    void makeTable();
}

//Main Sofa interface
interface Sofa{
    void makeSofa();
}

//Concrete chair implementation 1
class OldStyleChair implements Chair{
    public void makeChair(){
        System.out.println("Old style Chair Made");
    }
}

//Concrete chair implementation 2
class newStyleChair implements Chair{
    public void makeChair(){
        System.out.println("New style Chair Made");
    }
}

//Concrete table implementation 1
class OldStyleTable implements Table{
    public void makeTable(){
        System.out.println("Old style table Made");
    }
}

//Concrete table implementation 2
class newStyleTable implements Table{
    public void makeTable(){
        System.out.println("New style table Made");
    }
}

//Concrete Sofa implementation 2
class oldStyleSofa implements Sofa{
    public void makeSofa(){
        System.out.println("old style table Made");
    }
}

//Concrete sofa implementation 2
class newStyleSofa implements Sofa{
    public void makeSofa(){
        System.out.println("New style table Made");
    }
}

//Interface to hold factory and its possible products that can be produced.
interface FurnitureFactory{
    Chair chairMade();
    Table tableMade();
    Sofa sofaMade();
}

//Concrete factory 1
class oldStyleFacotry implements FurnitureFactory{
    public Chair chairMade(){
        return new OldStyleChair();
    }
    public Table tableMade(){
        return new OldStyleTable();
    }
    public Sofa sofaMade(){
        return new oldStyleSofa();
    }
}

//Concrete factory 2
class newStyleFacotry implements FurnitureFactory{
    public Chair chairMade(){
        return new newStyleChair();
    }
    public Table tableMade(){
        return new newStyleTable();
    }
    public Sofa sofaMade(){
        return new newStyleSofa();
    }
}
```