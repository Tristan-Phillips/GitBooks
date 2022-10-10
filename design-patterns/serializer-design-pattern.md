---
description: Lets read and write
---

# Serializer Design Pattern

### Intent

Used to serialize / stream the state of an object into / out of, other objects

### Applicability

Primarily used for communication

* Not intended for general input / output, or save / restore
* The class to be serialized / de-serialized does not participate in the process
* The subject class must be able to provide its state, and allow its state to be set
* Implements 2 classes
  * classReader - With a read() method
  * classWriter - with a write() method
* Should not be implemented as a single class, have separate read / write classes

### Comment

There are some variations in the use of the Serializer pattern

* Constructor - you can pass an argument in the constructor, often a file name
  * SerialClass myObj(QString fileName = "myFile.txt");
* Write method
  * Passes the object to be serialized by value or by reference / pointer
  * write(MyClass \*obj);
  * Can return a bool to confirm if the write was successful or not
* Read method
  * Can pass an object to be de-serialized as a reference, or return the object
  * void read(MyClass \&myObj);
