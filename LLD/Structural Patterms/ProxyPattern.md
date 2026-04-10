# Proxy Pattern
**Proxy** is a structural design pattern that lets you provide a substitute or placeholder for another object. A proxy controls access to the original object, allowing you to perform something either before or after the request gets through to the original object.



```
// Online Java Compiler
// Use this editor to write, compile and run your Java code online

class Main {
    public static void main(String[] args) {
        Task t  = new ProxyTask();
        t.heavyTask();
    }
}

interface Task{
    void heavyTask();
}

class HeavyObject implements Task{
    @Override
    public void heavyTask(){
        //supposedly heavy task
        System.out.println("HeavyTask");
    }
}

class ProxyTask implements Task{
    private Task task ;
    
    private Task getInstance(){
        if(task == null){
            task = new HeavyObject();
        }
        
        return task;
    }
    
    @Override
    public void heavyTask(){
        //loggin
        System.out.println("logging heacy task");
        System.out.println("check privs...");
        this.getInstance().heavyTask();
    }
}
```