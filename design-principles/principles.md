# Principles

* **Identify the aspects of your application that vary and separate them from what stays the same**
  * Take the parts that vary and encapsulate them, so that later you can alter or extend the parts that vary without affecting those that don’t.
* **Strive for loosely coupled designs between objects that interact**
  * Entities interact, but have little knowledge of each other, outside the contract of an interface
* **Program to an interface, not an implementation**
* **Favor composition over inheritance**
  * The HAS-A relationship can be better than IS-A. It lets you change behavior at runtime.
* **Dependency Inversion** 
  * Depend upon abstractions. Do not depend upon concrete classes.
  * Both the high-level and low-level components should depend on abstractions.
  * No variable should hold a reference to a concrete class \(use a factory when you need `new()`\)
  * No class should derive from a concrete class \(derive from an absraction instead\)
  * No method should override an implemented method of any of its base classes. 



