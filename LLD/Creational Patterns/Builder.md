# Builder Pattern




```
class Main {
    public static void main(String[] args) {
        Order order =new Order.Builder().amount(100.98).numOfItems(2).buyerName("goonda")
                        .orderId("1234").build();
        order.printOrderDeets();
    }
}

class Order{
    String orderId;
    double amount;
    int numOfItems;
    String buyerName;
    
    public Order(Builder builder){
        this.orderId = builder.orderId;
        this.amount = builder.amount;
        this.numOfItems = builder.numOfItems;
        this.buyerName = builder.buyerName;
    }
    public void printOrderDeets(){
        System.out.println(orderId + "\n" +amount + "\n" +numOfItems + "\n" +buyerName + "\n" );
    }
    
    public static class Builder{
        String orderId;
        double amount;
        int numOfItems;
        String buyerName;
        
        public Builder amount(double amount){
            this.amount = amount;
            return this;
        }
        
        public Builder numOfItems(int numOfItems){
            this.numOfItems = numOfItems;
            return this;
        }
        
        public Builder buyerName(String buyerName){
            this.buyerName = buyerName;
            return this;
        }
        public Builder orderId(String orderId){
            this.orderId = orderId;
            return this;
        } 
        
        
        public Order build(){
            return new Order(this);
            
        }
        
    }
}
```