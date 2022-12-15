# Singleton Design Pattern

### Intent

To ensure that a class has one and only one instance, and provides a central point of access

### Applicability

Use singleton when there can / must only be one instance of a class, and it must be accessible from a well known, easily accessible, access point

### Participants

<figure><img src="https://i.imgur.com/ZmGia5V.png" alt=""><figcaption></figcaption></figure>

* **Constructor** - Singleton() - is private
* **Data member** - singleton (is static) - stores a pointer to the singleton object (optional)
* **Method** - getInstance() (is static) - returns a pointer to a new instance if one does not exist, or a pointer to the existing instance, if one does exist

### Advantages of a Singleton Implementation

A **Singleton** is an elegant way of maintaining global state, but we should always question whether we need global state. Singleton pattern offers several advantages over global variables because it does the following

1. Enforces that only one instance of the class can be instantiated
2. Allows control over the allocation and destruction of the object
3. Provides thread-safe access to the object's global state
4. Prevents the global namespace from being polluting

### Code Example : Singleton

```cpp
#include <iostream>

class Singleton
{
public:
	static Singleton& getInstance(); 

private:
	Singleton() {std::cout << "Ctor\n";};
	~Singleton() {std::cout << "Dtor\n";};
	Singleton(const Singleton&);
	const Singleton& operator=(const Singleton&);
};

Singleton& Singleton::getInstance() 
{
	static Singleton instance;
	return instance;
}

int main()
{
	Singleton &s1; = Singleton::getInstance();
	Singleton &s2; = Singleton::getInstance();
	return 0;
}
```

### Code Example : Thread Safe Singleton

The above version is not thread safe because there could be a race condition during the initialization of the static Singleton, **Singleton& Singleton::getInstance()**. But we can make the method thread safe by adding a mutex lock:

```cpp
Singleton& Singleton::getInstance() 
{
        Mutex mutex;
        ScopedLock(&mutex;);  // to unlock mutex on exit
	static Singleton instance;
	return instance;
}
```
