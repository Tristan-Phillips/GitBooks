# Facade Design Pattern

### Intent

Hides the complexity of a system by providing a simplified interface for the client to access

### Applicability

* Used to provide a simplified interface to a complicated set of systems
* The facade interacts with the sub-systems, based on a request from client(s)
* A higher level interface that makes sub-systems easier to use

<figure><img src="https://i.imgur.com/oZ2dX4u.png" alt=""><figcaption></figcaption></figure>

### Code Example : Facade Pattern

The **Façade** pattern is a way to structure our API into subsystems to reduce ever growing size and complexity of interfaces of API.

```cpp
#include <iostream>

// Subsystem 1
class SubSystemOne
{
public:
	void MethodOne(){ std::cout << "SubSystem 1" << std::endl; };
};

// Subsystem 2
class SubSystemTwo
{
public:
	void MethodTwo(){ std::cout << "SubSystem 2" << std::endl; };
};

// Subsystem 3 
class SubSystemThree
{
public:
	void MethodThree(){ std::cout << "SubSystem 3" << std::endl; }
};


// Facade
class Facade
{
public:
    Facade()
    {
	pOne = new SubSystemOne();
	pTwo = new SubSystemTwo();
	pThree = new SubSystemThree();
    }

    void MethodA()
    {
	std::cout << "Facade::MethodA" << std::endl;
	pOne->MethodOne();
	pTwo->MethodTwo();
    }

    void MethodB()
    {
	std::cout << "Facade::MethodB" << std::endl;
	pTwo->MethodTwo();
	pThree->MethodThree();
    }

private:
    SubSystemOne *pOne;
    SubSystemTwo *pTwo;
    SubSystemThree *pThree;
};

int main()
{
    Facade *pFacade = new Facade();

    pFacade->MethodA();
    pFacade->MethodB();

    return 0;
}
```

> Output
>
> ```
> Facade::MethodA
> SubSystemOne: 1
> SubSystem 2
> Facade::MethodB
> SubSystem 2
> SubSystem 3
> ```
