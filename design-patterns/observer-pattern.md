# Observer Pattern

The **Observer Pattern** defines a one-to-many dependency between objects so that when one object changes state, all of its dependents are notified and updated automatically.

We have one subject, who notifies many observers when something in the subject changes. The observers are dependent on the subject — when the subject’s state changes, the observers are notified.

More details at [https://java-design-patterns.com/patterns/observer/](https://java-design-patterns.com/patterns/observer/)

* Every Subject has a list of Observers, to which Observers can be registered or deregistered.
* On a change in the Subject, it notifies every Observer in it's list, and each Observer is updated
* The notification may contain the Subject's state - **push based**
* Or it may simply notify change, and the Observers **pull in** the state from the Subject

```java
public interface Subject {
	public void registerObserver(Observer o);
	public void removeObserver(Observer o);
	public void notifyObservers();
}

public class SimpleSubject implements Subject {
	private List<Observer> observers;
	private int value = 0;
	
	public SimpleSubject() {
		observers = new ArrayList<Observer>();
	}
	
	public void registerObserver(Observer o) {
		observers.add(o);
	}
	
	public void removeObserver(Observer o) {
		observers.remove(o);
	}
	
	public void notifyObservers() {
		for (Observer observer : observers) {
			observer.update(value);
		}
	}
	
	public void setValue(int value) {
		this.value = value;
		notifyObservers();
	}
}
```

```java
public interface Observer {
	public void update(int value);
}

public class SimpleObserver implements Observer {
	private int value;
	// why a reference to subject?
	// to deregister itself, pull in state etc.
	private Subject simpleSubject;
	
	public SimpleObserver(Subject simpleSubject) {
		this.simpleSubject = simpleSubject;
		simpleSubject.registerObserver(this);
	}
	
	public void update(int value) {
		this.value = value;
		display();
	}
	
	public void display() {
		System.out.println("Value: " + value);
	}
}
```

