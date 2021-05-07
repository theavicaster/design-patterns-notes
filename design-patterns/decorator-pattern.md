# Decorator Pattern

The **Decorator Pattern** attaches additional responsibilities to an object dynamically. Decorators provide a flexible alternative to subclassing for extending functionality.

* Decorators have the same supertype as the objects they decorate. 
* You can use one or more decorators to wrap an object. 
* Given that the decorator has the same supertype as the object it decorates, we can pass around a decorated object in place of the original \(wrapped\) object. 
* The decorator **adds its own behavior** before and/or after delegating to the object it decorates to do the rest of the job. 
* Objects can be decorated at any time, so we can decorate objects dynamically at runtime with as many decorators as we like

More details at [https://java-design-patterns.com/patterns/decorator/](https://java-design-patterns.com/patterns/decorator/)

```java
// component
public abstract class Beverage {
	String description = "Unknown Beverage";
  
	public String getDescription() {
		return description;
	}
 
	public abstract double cost();
}

// concrete component
public class Espresso extends Beverage {
  
	public Espresso() {
		description = "Espresso";
	}
  
	public double cost() {
		return 1.99;
	}
}
```

```java
// decorator
public abstract class CondimentDecorator extends Beverage {
	Beverage beverage;
	public abstract String getDescription();
}

// concrete decorator
public class Whip extends CondimentDecorator {
	public Whip(Beverage beverage) {
		this.beverage = beverage;
	}
 
	public String getDescription() {
		return beverage.getDescription() + ", Whip";
	}
 
	public double cost() {
		return .10 + beverage.cost();
	}
}
```

```java
	public static void main(String args[]) {
		Beverage beverage = new Espresso();
		beverage = new Whip(beverage);
		beverage = new Mocha(beverage);
		System.out.println(beverage.getDescription() 
				+ " $" + beverage.cost());
	}
```



