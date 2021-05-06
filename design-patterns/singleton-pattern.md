# Singleton Pattern

The **Singleton Pattern** ensures a class has only one instance, and provides a global point of access to it.

```java
public class Singleton {
    
    private static Singleton INSTANCE;
    
    private Singleton() {}
    
    public static synchronized getInstance(){
        if(INSTANCE == null)
            INSTANCE = new Singleton();
        return INSTANCE;
    }
}
```

Notice that we don't need `synchronized` every time, we only need it the first time Singleton is created. Hence there is unnecessary overhead.

An effective way to create Singletons -

```java
public enum Singleton{
    INSTANCE;
    
    // other methods
    public void sayHello(){
        System.out.println("Hello");
    }
}

public static void main(String[] args){
    Singleton singleton = Singleton.INSTANCE;
    singleton.sayHello();
}
```

