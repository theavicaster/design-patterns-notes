# Singleton Pattern

The **Singleton Pattern** ensures a class has only one instance, and provides a global point of access to it.

```java
public class Singleton {
    
    private static Singleton INSTANCE;
    
    private Singleton() {}
    
    public static synchronized Singleton getInstance(){
        if(INSTANCE == null)
            INSTANCE = new Singleton();
        return INSTANCE;
    }
}
```

Notice that we don't need `synchronized` every time, we only need it the first time Singleton is created. Hence there is unnecessary overhead.

```java
// both these interfaces have a chance of getting a new instance
public class Singleton implements Serializable, Cloneable {
    
    private volatile static Singleton INSTANCE;
    
    private Singleton() {
        // if Java reflection attempts to call this constructor
        if(INSTANCE != null) {
            throw new IllegalStateException("Already exists!");
        }
    }
    
    // since this method does not need to be synchronized
    // for every single call
    public static Singleton getInstance(){
        if(INSTANCE == null) {
            synchronized(this.class) {
                if(INSTANCE == null) {
                    INSTANCE = new Singleton();
                }
            }
        }
        return INSTANCE;
    }
    
    @Override // from Serializable
    protected Object readResolve() {
        return INSTANCE;
    }
    
    @Override // from Cloneable
    protected Object clone() throws CloneNotSupportedException() {
        throw new CloneNotSupportedException();
    }
}
```

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
