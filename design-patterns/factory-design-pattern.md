---
description: Lets make a baby
---

# Factory Design Pattern

### Intent

Provides an interface for creating (instantiating) objects in a superclass, but allows sub-classes to actually create the objects

Factory Method lets a class defer instantiation to subclasses. To name the method more descriptively, it can be named as **Factory and Product Method** or **Virtual Constructor**

### Applicability

* Provides a common interface for instantiating related objects
* The responsibility for creating objects is transferred to a separate factory method class (Single purpose - separates object creation from object use)

### Comment

* Makes extensive use of abstract base classes, inheritance and polymorphism

### Participants

<figure><img src="https://i.imgur.com/c6qGwxo.png" alt=""><figcaption></figcaption></figure>

* **Product** - Abstract base class for Products
* **ConcreteProduct** - Concrete class that implements Products
* **Creator** (optional) - Abstract base class, optional and not always used
* **ConcreteCreator** - Concrete class that implements the factoryMethod()
  * returns - new ConcreteProduct

### Benefits

The factory design pattern allows us to circumvent the following limitations of the C++ constructor

* No return type - A constructor cannot return a result, which means that we cannot signal an error during object initialization. The only way of doing it is to throw an exception from a constructor
* Naming - A constructor should have the same name as the class, which means we cannot have two constructors that both take a single argument
* Compile time bound - At the time when we create an object, we must specify the name of a concrete class which is known at compile time. There is no way of dynamic binding constructors at run time
* There is no virtual constructor - We cannot declare a virtual constructor. We should specify the exact type of the object at compile time, so that the compiler can allocate memory for that specific type.&#x20;

#### Where could it be beneficial

If we wanted to create an OSX style button, we can write the following code

```cpp
Button *btn = new OSXButton;
```

However, if we wanted this to work across any platform, we should do something similar to the following

```cpp
Button *btn = guiFactory->createButton();
```

If guiFactory is an instance of the Factory class, then the createButton() method returns a new instance of the OSX style button, after having selected the appropriate button to create.

#### The two main, major variations of the Factory Method Design pattern

1. When the creator class is an Abstract class and does not provide implementation for the factory methods it declares. Thus, subclasses must define an implementation, as there is no reasonable default.
2. When the concrete creator uses the factory method primarily for flexibility. Thus, designers of subclasses can change the class of objects their parent class instantiates if necessary

### Code Example 1 : Abstract Creator Class

```cpp
#include <iostream>

class Button {
public:
	virtual void paint() = 0;
};
 
class OSXButton: public Button {
public:
	void paint() {
		std::cout << "OSX button \n";
	}
};
 
class WindowsButton: public Button  {
public:
	void paint() {
		std::cout << "Windows button \n";
	}
};
 
class GUIFactory {
public:
	virtual Button *createButton(char *) = 0;
};

class Factory: public GUIFactory {
public:
	Button *createButton(char *type) {
		if(strcmp(type,"Windows") == 0) {
			return new WindowsButton;
		}
		else if(strcmp(type,"OSX") == 0) {
			return new OSXButton;
		}
	}
};

int main()
{
	GUIFactory* guiFactory;
	Button *btn;

	guiFactory = new Factory;

	btn = guiFactory->createButton("OSX");
	btn -> paint();
	btn = guiFactory->createButton("Windows");
	btn -> paint();

	return 0;
}
```

> Output
>
> ```
> OSX button
> Windows button
> ```

Here we made two types of buttons without knowing their specific class names.

In essence, a factory method is a normal method which returns an instance of a class.

### Code Example 2 : Concrete Creator Class

```cpp
#include <iostream>

class Button {
public:
	virtual void paint() = 0;
};
 
class OSXButton: public Button {
public:
	void paint() {
		std::cout << "OSX button \n";
	}
};
 
class WindowsButton: public Button  {
public:
	void paint() {
		std::cout << "Windows button \n";
	}
};
 
class iPhoneButton: public Button {
public:
	void paint() {
		std::cout << "iPhone button \n";
	}
};

class GUIFactory {
public:
	virtual Button *createButton(char *type) {
		if(strcmp(type,"Windows") == 0) {
			return new WindowsButton;
		}
		else if(strcmp(type,"OSX") == 0) {
			return new OSXButton;
		}
		return NULL;
	}
};

class Factory: public GUIFactory {
		Button *createButton(char *type) {
		if(strcmp(type,"Windows") == 0) {
			return new WindowsButton;
		}
		else if(strcmp(type,"OSX") == 0) {
			return new OSXButton;
		}
		else if(strcmp(type,"iPhone") == 0) {
			return new iPhoneButton;
		}
	}
};

int main()
{
	GUIFactory* guiFactory;
	Button *btn;

	guiFactory = new Factory;

	btn = guiFactory->createButton("OSX");
	btn -> paint();
	btn = guiFactory->createButton("Windows");
	btn -> paint();
	btn = guiFactory->createButton("iPhone");
	btn -> paint();

	return 0;
}
```

> Output
>
> ```
> OSX button
> Windows button
> iPhoneButton
> ```

