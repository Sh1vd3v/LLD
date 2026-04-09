


```
// Online Java Compiler
// Use this editor to write, compile and run your Java code online

class Main {
    public static void main(String[] args) {
        Charger apple = new androidChargerAdapter();
        apple.chargeDevice();
    }
}


interface Charger {
    void chargeDevice();
}

//Client implementations
class appleCharger {
    public void lightningCharger(){
        System.out.println("Charging apple devices....");
    }
}

class androidCharger{
    public void typeCCharger(){
        System.out.println("Charging android devices...");
    }
}

//Adadpter classes
class appleChargerAdapter implements Charger{
    public void chargeDevice(){
        appleCharger app = new appleCharger();
        app.lightningCharger();
    }
}

class androidChargerAdapter implements Charger{
    public void chargeDevice(){
        androidCharger and = new androidCharger();
        and.typeCCharger();
    }
}
```