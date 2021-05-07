# Command Pattern

The **Command Pattern** encapsulates a request as an object, thereby letting you 

* Parameterize other objects \(Receivers\) with different requests
* Queue or log requests
* Support undoable operations.

It allows you to decouple the requester of an action from the object that actually performs the action.

The Command object encapsulates the **Receiver**, who is the object that carries out the command. When `execute()` is called, actions are executed upon the receiver. The **Invoker** stores created command objects, and may invoke them when necessary.

The command can also have an `undo()` method. To have multiple undos, we can keep a stack of commands, and call `undo()` on the most recent command.

A database can be recovered from logs in the form of Commands, by sequentially running each command. This is better than storing the entire state of the database at every stage.

Note that commands are independent of the object invoking them. Hence they may be used as callbacks long after the invoker is gone.

We can also replace a long list of IF statements [https://stackoverflow.com/a/1199677/8484655](https://stackoverflow.com/a/1199677/8484655)

More details at [https://java-design-patterns.com/patterns/command/](https://java-design-patterns.com/patterns/command/)

```java
public interface Command {
	public void execute();
}

public class LightOnCommand implements Command {
	
	// the Receiver of the Command!
	Light light;

	public LightOnCommand(Light light) {
		this.light = light;
	}

	public void execute() {
		light.on();
	}
}

// similar LightOffCommand

public class Light {

	String status = "off";

	public void on() {
		System.out.println(location + " light is on");
		status = "on";
	}

	public void off() {
		System.out.println(location + " light is off");
		status = "off"
	}
}
```

```java
// This is the invoker
public class SimpleRemoteControl {
	
	Command slot;
	public SimpleRemoteControl() {}
	
	public void setCommand(Command command){
		slot = command;
	}
	
	public void buttonWasPressed() {
		slot.execute();
	}
}

public class RemoteLoader {
 
	public static void main(String[] args) {
		
		SimpleRemoteControl remoteControl = new SimpleRemoteControl();
 
		Light myLight = new Light();
		LightOnCommand lightOn = 
				new LightOnCommand(myLight);
		LightOffCommand lightOff = 
				new LightOffCommand(myLight);
 
		remoteControl.setCommand(lightOn);
		remoteControl.buttonWasPressed();

	}
}
```



