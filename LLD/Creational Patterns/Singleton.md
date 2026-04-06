# Singleton Pattern

Let's you create a class which only has **one instance** and the class also provides a **global access point** to this *instance*.

- in a way we can say that *Singleton pattern* solves two problems at the same time, violating the Single Responsibility Principle (SRP).
    1. Returning the same obhect instance whenever a instance is requested.
    2. Providing a global access point to it.

### Implementation
- Each singleton clas will have a default constructor that is private, so that instnaces can not be created from outside of the class.
- A static maethod to get the instance of the object, this method under the hood generates the required instance if not present or return the instance if it has been already created.





