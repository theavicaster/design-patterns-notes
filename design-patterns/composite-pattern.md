# Composite Pattern

The **Composite Pattern** allows you to compose objects into tree structures to represent part-whole hierarchies. Composite lets clients treat individual objects and compositions of objects uniformly.

It allows us to build structures of objects in the form of trees that contain both compositions of objects and individual objects as nodes.

The leaf nodes are objects \(**Leaf**\). The non-leaf nodes are collections of objects \(**Composite**\). They are both **Components** of our tree.

```java
// Component
public abstract class MenuComponent {
  
  // some make sense for leaves, other for composites
  // so they are unsupported by default 
	public void add(MenuComponent menuComponent) {
		throw new UnsupportedOperationException();
	}
	public void remove(MenuComponent menuComponent) {
		throw new UnsupportedOperationException();
	}
	public MenuComponent getChild(int i) {
		throw new UnsupportedOperationException();
	}
    
	public void print() {
		throw new UnsupportedOperationException();
	}
}
```

```java
// Leaf
public class MenuItem extends MenuComponent {

	double price;
    
	public MenuItem(double price) { 
		this.price = price;
	}
  
	public double getPrice() {
		return price;
	}
	public void print() {
		System.out.println(", " + getPrice());
	}
}
```

```java
// Composite
public class Menu extends MenuComponent {
	ArrayList<MenuComponent> menuComponents = new ArrayList<MenuComponent>();
  
	public void add(MenuComponent menuComponent) {
		menuComponents.add(menuComponent);
	}
 
	public void remove(MenuComponent menuComponent) {
		menuComponents.remove(menuComponent);
	}
 
	public MenuComponent getChild(int i) {
		return (MenuComponent)menuComponents.get(i);
	}
 
	public void print() {
		Iterator<MenuComponent> iterator = menuComponents.iterator();
		while (iterator.hasNext()) {
			MenuComponent menuComponent = 
				(MenuComponent)iterator.next();
			menuComponent.print();
		}
	}
}
```

