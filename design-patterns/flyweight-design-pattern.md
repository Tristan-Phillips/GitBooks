---
description: Same-Same, but different
---

# Flyweight Design Pattern

### Intent

To use memory sharing to support a large numbers of objects efficiently

### Applicability

* When an application requires a large amount of objects
* When storage costs are high due to the quantity of objects
* When most object states can be mate extrinsic (External)

### Comment

* Avoids the need to store multiple copies of the same object
* A 'Wrapper' object holds pointers to the shared data, instead of an actual copy of the data
* Uses 'reference-counting' through the use of smart pointers, or shared pointers

### QT's implementation

Utilizes QT's container classes - such as templates: QList\<QString>

* Sequential - QList, QLinkedList, QVector, QStack, QQueue
* Associative (Key / value pair) - QMap, QMultiMap, QHash, QMultiHash, QSet

QT containers are implicitly shared - (Simplified implementation of Flyweight Pattern)

* Only a pointer to the data is passed around
* Data is copied only if and when a function writes to it - copy-on-write
* Assignment is done using shallow copy - pointer to shared data is copied
  * Shallow copy is a reference copy - pointer to shared data
  * Deep copy - duplicates an object
