# Memento Design Pattern

### Intent

Save and restore the previous state of an object, without breaking encapsulation&#x20;

( _Encapsulation may also refer to a mechanism of restricting the direct access to some components of an object, such that users cannot access state values for all of the variables of a particular object. Encapsulation can be used to hide both data members and data functions or methods associated with an instantiated class or object_. )

### Applicability

Is used when the state of an object needs to be saved, such that it can later be restored, without breaking encapsulation. ("Undo" or "Backup / Restore")

* Memento - an object that stores a 'snapshot' of the state of another object
* Memento can only be set / read by the originator&#x20;
* The originator has to be involved in saving and restoring its state

### Participants

<figure><img src="https://i.imgur.com/AhPwb9s.png" alt=""><figcaption></figcaption></figure>

* Originator - The object that's state is saved
  * Saves itself - Memento createMomento() returns a new Memento(state)
  * Restores itself - void setMemento(Memento m)&#x20;
* Caretaker - The object that stores / initiates Mementos - it cannot access the Memento
* Memento - Object that stores / re-stores the state of the Originator object
  * Sets the state of the Memento - void memento(state);
  * Retrieves the state of the Memento - State getState();
  * All methods and properties are private
  * Must declare the originator to be a friend of the Memento, such that it can have access to the Memento
