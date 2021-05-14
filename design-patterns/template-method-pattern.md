# Template Method Pattern

The **Template Method Pattern** defines the skeleton of an algorithm in a method, deferring some steps to subclasses. Template Method lets subclasses redefine certain steps of an algorithm without changing the algorithm’s structure.

Hooks can be used to plug in custom functionality.

A practical example is `Arrays.sort()`

More details at [https://java-design-patterns.com/patterns/template-method/](https://java-design-patterns.com/patterns/template-method/)

```java
public abstract class CaffeineBeverageWithHook {
 
  // this is the template method
	final void prepareRecipe() {
		boilWater();
		brew();
		pourInCup();
		if (customerWantsCondiments()) {
			addCondiments();
		}
	}
 
 	// primitive operations to be
  // implemented by subclasses
	abstract void brew();
	abstract void addCondiments();
 
  // concrete operations which are
  // common across subclasses
	void boilWater() {
		System.out.println("Boiling water");
	}
	void pourInCup() {
		System.out.println("Pouring into cup");
	}
 
  // this is a hook!
  // it can be overriden if subclass wants to customize
	boolean customerWantsCondiments() {
		return true;
	}
}

public class CoffeeWithHook extends CaffeineBeverageWithHook {
 
	public void brew() {
		System.out.println("Dripping Coffee through filter");
	}
 
	public void addCondiments() {
		System.out.println("Adding Sugar and Milk");
	}
 
  // override the hook!
	public boolean customerWantsCondiments() {

		String answer = getUserInput();

		if (answer.toLowerCase().startsWith("y")) {
			return true;
		} else {
			return false;
		}
	}
 
	private String getUserInput() {
		// returns "yes" or "no"
	}
}
```



