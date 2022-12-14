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

### Example Code : Memento Pattern

```cpp
// Originator Header
class Originator
{
public:
    Originator();
    void setMemento(Memento *m);
    Memento * createMemento();
private:
    // State values
    QString m_name;
    QString m_code;
    QString m_value1;
    QString m_value2;
};

//Originator Source
void Originator::setMemento(Memento *m)
{
    QStringList state = m->getState();
    m_name = state.at(0);
    m_code = state.at(1);
    m_value1 = state.at(2);
    m_value2 = state.at(3);
}

Memento * Originator::createMemento()
{
    QStringList state;
    state << m_name << m_code << m_value1 << m_value2;
    Memento *memento = new Memento;
    memento->setState(state);
    return memento;
}

//Memento Header
class Memento
{
private:
    friend class Originator;
    Memento();
    QStringList getState();
    void setState(QStringList state);
    QStringList m_state;
};

//Memento Source
QStringList Memento::getState()
{
    return m_state;
}

void Memento::setState(QStringList state)
{
    m_state = state;
}

//Caretaker Header
class Caretaker
{
public:
    Caretaker(Originator *origin);
    void saveState();
    void restoreState();
private:
    Memento *m_state;
    Originator *m_origin;
};

//Caretaker Source
Caretaker::Caretaker(Originator *origin)
: m_origin(origin)
{ }

void Caretaker::saveState()
{
    m_state = m_origin->createMemento();
}

void Caretaker::restoreState()
{
    m_origin->setMemento(m_state);
}
```
