# Facade Pattern

The **Facade Pattern** provides a unified interface to a set of interfaces in a subsystem. Facade defines a higher- level interface that makes the subsystem easier to use.

To use the Facade Pattern, we create a class that simplifies and unifies a set of more complex classes that belong to some subsystem.

More details at [https://java-design-patterns.com/patterns/facade/](https://java-design-patterns.com/patterns/facade/)

```java
public static void main(String[] args) {
    // instantiate components here
    HomeTheaterFacade homeTheater = 
        new HomeTheaterFacade(amp, tuner, player,projector, screen, lights, popper);
    homeTheater.watchMovie("Raiders of the Lost Ark");
}
```

