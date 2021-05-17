# State Pattern

The **State Pattern** allows an object to alter its behavior when its internal state changes. The object will appear to change its class.

It appears to change it's class by changing it's state. Each state will have it's own unique methods.

The Context is an object which can have multiple States. Whenever there is a request to the Context, it delegates the request to the current State to handle. The States themselves can change the current State of the Context when handling a request, thereby doing state transitions.

```java
public interface State {
 
	public void insertQuarter();
	public void ejectQuarter();
	public void turnCrank();
	public void dispense();
	
	public void refill();
}

public class NoQuarterState implements State {
    GumballMachine gumballMachine;
 
    public NoQuarterState(GumballMachine gumballMachine) {
        this.gumballMachine = gumballMachine;
    }
 
		public void insertQuarter() {
			System.out.println("You inserted a quarter");
			gumballMachine.setState(gumballMachine.getHasQuarterState());
		}
	 
		public void ejectQuarter() {
			System.out.println("You haven't inserted a quarter");
		}
	 
		public void turnCrank() {
			System.out.println("You turned, but there's no quarter");
		 }
	 
		public void dispense() {
			System.out.println("You need to pay first");
		} 
		
		public void refill() { }
	 
		public String toString() {
			return "waiting for quarter";
		}
}

public class HasQuarterState implements State {
	GumballMachine gumballMachine;
 
	public HasQuarterState(GumballMachine gumballMachine) {
		this.gumballMachine = gumballMachine;
	}
  
	public void insertQuarter() {
		System.out.println("You can't insert another quarter");
	}
 
	public void ejectQuarter() {
		System.out.println("Quarter returned");
		gumballMachine.setState(gumballMachine.getNoQuarterState());
	}
 
	public void turnCrank() {
		System.out.println("You turned...");
		gumballMachine.setState(gumballMachine.getSoldState());
	}

  public void dispense() {
    System.out.println("No gumball dispensed");
  }
    
    public void refill() { }
 
	public String toString() {
		return "waiting for turn of crank";
	}
}
```

```java
public class GumballMachine {
 
	State soldOutState;
	State noQuarterState;
	State hasQuarterState;
	State soldState;
 
	State state;
	int count = 0;
 
	public GumballMachine(int numberGumballs) {
		soldOutState = new SoldOutState(this);
		noQuarterState = new NoQuarterState(this);
		hasQuarterState = new HasQuarterState(this);
		soldState = new SoldState(this);

		this.count = numberGumballs;
 		if (numberGumballs > 0) {
			state = noQuarterState;
		} else {
			state = soldOutState;
		}
	}
 
	public void insertQuarter() {
		state.insertQuarter();
	}
 
	public void ejectQuarter() {
		state.ejectQuarter();
	}
 
	public void turnCrank() {
		state.turnCrank();
		state.dispense();
	}
 
	void releaseBall() {
		System.out.println("A gumball comes rolling out the slot...");
		if (count > 0) {
			count = count - 1;
		}
	}
 
	int getCount() {
		return count;
	}
 
	void refill(int count) {
		this.count += count;
		System.out.println("The gumball machine was just refilled; its new count is: " + this.count);
		state.refill();
	}
}
```

