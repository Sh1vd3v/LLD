


```
// Online Java Compiler
// Use this editor to write, compile and run your Java code online
import java.util.List;
import java.util.ArrayList;
class Main {
    public static void main(String[] args) {
        Employee emp1 = new IndividualContributor("a");
        Employee emp2 = new IndividualContributor("2");
        Employee emp3 = new IndividualContributor("3");
        Employee emp4 = new IndividualContributor("4");
        Employee emp5 = new IndividualContributor("5");
        Employee emp6 = new IndividualContributor("6");
        Employee emp7 = new IndividualContributor("7");
    
        Employee m1 = new Manager("m1");
        Employee m2 = new Manager("m2");
        
        m2.addEmployee(emp7);
        m2.addEmployee(emp3);
        m2.addEmployee(emp1);
        m1.addEmployee(emp2);
        m1.addEmployee(emp4);
        m1.addEmployee(emp5);
        m1.addEmployee(emp6);
        
        m1.addEmployee(m2);
        
        m1.getDescription();
     
    }
}

interface Employee{
    void getDescription();
    void addEmployee(Employee zzz);
    //removeemp etc....
}

class IndividualContributor implements Employee{
    String name;
    
    IndividualContributor(String name){
        this.name = name;
    }
    
    @Override
    public void getDescription(){
        System.out.println("Employee Name : " + this.name  );
    }
    
    @Override
    public void addEmployee(Employee emp){
      System.out.println("aa");
    }
}

class Manager implements Employee{
    String name;
    List<Employee> reportees;
    
    Manager(String name){
        this.name = name;
        reportees = new ArrayList<>();
    }
    @Override
    public void addEmployee(Employee emp){
        reportees.add(emp);
    }
    
    @Override
    public void getDescription(){
        System.out.println("Manager name :" + name);
        for(Employee emp : reportees){
            emp.getDescription();
        }
    }
    
}
```