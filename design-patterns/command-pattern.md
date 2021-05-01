# Command Pattern

The **Command Pattern** encapsulates a request as an object, thereby letting you parameterize other objects with different requests, queue or log requests, and support undoable operations.

The Command object encapsulates the **Receiver**, who is the object that the command affects. When `execute()` is called, actions are executed upon the receiver.

Note that commands are independent of the object invoking them. Hence they may be used as callbacks long after the invoker is gone.

We can also replace a long list of IF statements [https://stackoverflow.com/a/1199677/8484655](https://stackoverflow.com/a/1199677/8484655)

More details at [https://java-design-patterns.com/patterns/command/](https://java-design-patterns.com/patterns/command/)

```java
public interface Command {
	public void execute();
}

public class LightOnCommand implements Command {
	Light light;

	public LightOnCommand(Light light) {
		this.light = light;
	}

	public void execute() {
		light.on();
	}
}

public class LightOffCommand implements Command {
	Light light;
 
	public LightOffCommand(Light light) {
		this.light = light;
	}
 
	public void execute() {
		light.off();
	}
}

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
//
// This is the invoker
//
public class RemoteControl {
	Command[] onCommands;
	Command[] offCommands;
 
	public RemoteControl() {
		onCommands = new Command[7];
		offCommands = new Command[7];
 
		Command noCommand = new NoCommand();
		for (int i = 0; i < 7; i++) {
			onCommands[i] = noCommand;
			offCommands[i] = noCommand;
		}
	}
  
	public void setCommand(int slot, Command onCommand, Command offCommand) {
		onCommands[slot] = onCommand;
		offCommands[slot] = offCommand;
	}
 
	public void onButtonWasPushed(int slot) {
		onCommands[slot].execute();
	}
 
	public void offButtonWasPushed(int slot) {
		offCommands[slot].execute();
	}
}

public class RemoteLoader {
 
	public static void main(String[] args) {
		RemoteControl remoteControl = new RemoteControl();
 
		Light livingRoomLight = new Light("Living Room");

		LightOnCommand livingRoomLightOn = 
				new LightOnCommand(livingRoomLight);
		LightOffCommand livingRoomLightOff = 
				new LightOffCommand(livingRoomLight);
 
		remoteControl.setCommand(0, livingRoomLightOn, livingRoomLightOff);
 
		remoteControl.onButtonWasPushed(0);
		remoteControl.offButtonWasPushed(0);

	}
}
```



