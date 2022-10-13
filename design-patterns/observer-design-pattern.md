---
description: Hey, I saw that!
---

# Observer Design Pattern

### Intent

Defines a one-to-many dependency between objects, such that when one object (The Subject) changes its state, all its dependents (The Observers) are notified and update automatically

### Applicability

Communication between objects -

* When a change to one object (The Subject) requires changes in other objects (The Observers), and the number of other objects is not known
* Loosely coupled - The subject does not know anything about the observers, other than that they have an update() interface. You should be able to add / remove observers at will

### Comment

A very commonly used design pattern, especially with MVC

### QT's implementation

Relies on signals and slots

* Uses the QObject connect() method



<figure><img src="https://i.imgur.com/CjWSjRm.gif" alt=""><figcaption></figcaption></figure>

### Participants

* Subject - knows its observers, it can be any number of observers
  * Can attach / detach observer objects
* Observer - defines an interface (Abstract) for updating observers
* ConcreteSubject - stores the state of the subject
  * Notifies observers when the subjects state changes
* ConcreteObserver - maintains a reference to the subject, and stores the state consistent with the subject state
  * Implements an update()  interface to keep the state consistent with the subject state

