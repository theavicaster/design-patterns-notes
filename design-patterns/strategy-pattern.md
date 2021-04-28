---
description: 'More details at https://java-design-patterns.com/patterns/strategy/'
---

# Strategy Pattern

The **Strategy Pattern** defines a family of algorithms, encapsulates each one, and makes them interchangeable. Strategy lets the algorithm vary independently from clients that use it.

Strategy pattern allows choosing the best suited algorithm or best **behavior** at runtime. We are composing a class by injecting behaviors.

```java
public abstract class Duck {
	FlyBehavior flyBehavior;
	QuackBehavior quackBehavior;

	public Duck() {
	}

	public void setFlyBehavior(FlyBehavior fb) {
		flyBehavior = fb;
	}

	public void setQuackBehavior(QuackBehavior qb) {
		quackBehavior = qb;
	}

	abstract void display();

	public void performFly() {
		flyBehavior.fly();
	}

	public void performQuack() {
		quackBehavior.quack();
	}

	public void swim() {
		System.out.println("All ducks float!");
	}
}

public class MallardDuck extends Duck {

	public MallardDuck() {

		quackBehavior = new LoudQuack();
		flyBehavior = new FlyWithWings();

	}

	public void display() {
		System.out.println("I'm a real Mallard duck");
	}
}
```

```java
public interface FlyBehavior {
	public void fly();
}

public class FlyWithWings implements FlyBehavior {
	public void fly() {
		System.out.println("I'm flying!!");
	}
}
```

```java
public interface QuackBehavior {
	public void quack();
}

public class LoudQuack implements QuackBehavior {
	public void quack() {
		System.out.println("Loud Quack");
	}
}
```

```java
public static void main(String[] args) {
 
		MallardDuck	mallard = new MallardDuck();
		mallard.performQuack();
 
		Duck model = new ModelDuck();
		model.performFly();	
		// setting behaviors at runtime!
		model.setFlyBehavior(new FlyRocketPowered());
		model.performFly();
		
	}
```



