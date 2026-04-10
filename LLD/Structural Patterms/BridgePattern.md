# Bridge Pattern

Separates out *Abstraction* and *Implementation*. It create a bridge between the abstraction and implementation.

Example : Remote are the Abstraction and devices are implementations. Remote define at high level what the button shoud do (volume up/down etc), but it is upto the device to implement the actual functionality.

The Remote holds a reference to a device type, rather than doing all of the implementations itself. As that would mean us needing to create many different variants of classes for each combination.


### Implementation
```
// Online Java Compiler
// Use this editor to write, compile and run your Java code online

class Main {
    public static void main(String[] args) {
        GUI gui = new Mac(new PaintForMac());
        gui.displayApp();
    }
}

interface GUI {
    void displayApp();
}

class Windows implements GUI{
    App app;
    
    Windows(App app){
        this.app = app;
        
    }
    public void displayApp(){
        app.doTheActualApp();
    }
    
}

class Mac implements GUI{
    App app;
    
    Mac(App app){
        this.app = app;
    }
    
    public void displayApp(){
        app.doTheActualApp();
    }
    
}

interface App{
    void doTheActualApp();
}

class PaintForMac implements App{
    public void doTheActualApp(){
        System.out.println("Drawing paint for Mac..");
    }
}

class PaintForWin implements App{
    public void doTheActualApp(){
        System.out.println("Drawing paint for windows..");
    }
}
```