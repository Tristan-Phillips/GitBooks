# Abstract Factory Design Pattern

### Intent

Provides an interface for defining factories that share abstract features, but differ in concrete details

**The Abstract Factory** - Provide an interface for creating families of related or dependent objects without specifying their concrete classes

### Applicability

Used when there is a need to create families or related, or dependent objects

Two hierarchies exist

* Hierarchy of Product Classes
* Hierarchy of Factory Classes

<figure><img src="https://i.imgur.com/ETbxBUr.png" alt=""><figcaption></figcaption></figure>

#### Where could it be beneficial

If we wanted to create a Mac style scroll bar, we could write the following code

```cpp
ScrollBar *sb = new MacScrollBar;
```

However, to make this cross-platform, the following would be better

```cpp
ScrollBar *sb = guiFactory->createScrollBar();+
```

### Code Example : Abstract Factory

A factory method, is simply a normal method call which can return an instance of a class. But they are often used in combination with inheritance such that a derived class overrides the factory method and returns an instance of the derived class. More often, we implement factories using abstract base classes

In the following example, we want to render 3D scenes using OpenGL, DirectX, oretc.&#x20;

First, we write a base class where derived classes provide the implementation of the pure virtual methods

```cpp
#include <iostream>

class Renderer
{
public:
	virtual ~Renderer() {};
	virtual void RenderIt() = 0;
};

class OpenGLRenderer : public Renderer 
{
	void RenderIt() {
		std::cout << "OpenGL render \n";
	}
};

class DirectXRenderer : public Renderer 
{
		void RenderIt() {
		std::cout << "DirectX render \n";
	}
};

#include <string>

class RendererFactory
{
public:
	Renderer *createRenderer(const std::string& type) 
	{
	if(type == "opengl") 
		return new OpenGLRenderer();
	else if(type == "directx") 
		return new DirectXRenderer();
	else return NULL;
	}
};


int main()
{
	RendererFactory *factory = new RendererFactory();
	factory->createRenderer("opengl")->RenderIt();
	factory->createRenderer("directx")->RenderIt();
	return 0;
}
```

The method createRenderer() cannot return an instance of the specific type Renderer because it is an abstract base class, thus it can not be instantiated. It can, however, return instances of the derived class.&#x20;

We use a string argument in this method to create an instance of the derived class

```cpp
Renderer *createRenderer(const std::string& type);
```

We have two concrete classes derived from the Rendered class:

```cpp
class OpenGLRenderer : public Renderer {};
class DirectXRenderer : public Renderer {};
```

Thus we provide the following factory method implementation

```cpp
Renderer *RendererFactory::createRenderer(const std::string& type)
{
	if(type == "opengl") 
           return new OpenGLRenderer();
	else if(type == "directx") 
           return new DirectXRenderer();
	else return NULL;
}
```
