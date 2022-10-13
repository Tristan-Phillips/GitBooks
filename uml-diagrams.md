---
description: Everything you need to know about UML diagrams
---

# UML Diagrams

#### What are UML diagrams?

Unified Modeling Language (UML) is a standardized modeling language. It helps software developers visualize, construct, and document new software systems and blueprints

#### Basic structure of a UML diagram element

<figure><img src="https://i.imgur.com/jklTbSL.png" alt=""><figcaption></figcaption></figure>

#### Syntax

* _vis_ = Visibility (+ for public, - for private, # for protected)
* _attribute_ = Data member
* _operation_ = method

If you Italicize a method / class name, then it is virtual.

If you underline a method then it is static

To indicate a constant, use ALL CAPS

#### Types of relationships in a UML diagram

<figure><img src="https://i.imgur.com/JhPCY8c.png" alt=""><figcaption></figcaption></figure>

<details>

<summary>Association</summary>

If two classes in a model need to communicate with each other, there must be a link between them, and that can be represented by an association

</details>

<details>

<summary>Directed Association</summary>

Association can be represented by a line between these classes **with an arrow indicating the navigation direction**. In case an arrow is on both sides, the association is known as a bidirectional association

</details>

<details>

<summary>Reflexive Association</summary>

Links can exist between instances of the same class, for example, between nodes in a ring network or authors of a book. Associations that have the same class at both ends are known as reflexive associations

</details>

<details>

<summary>Multiplicity</summary>

Multiplicity can be set for attributes, operations, and associations in a UML class diagram. The multiplicity is an indication of how many objects may participate in the given relationship or the allowable number of instances of the element

</details>

<details>

<summary>Dependency</summary>

In UML, a dependency relationship is a relationship in which one element, the client, uses or depends on another element, the supplier. You can use dependency relationships to indicate that a change to the supplier might require a change to the client.

You can also use a dependency relationship to represent precedence, where one model element must precede another

</details>

<details>

<summary>Aggregation</summary>

**Aggregation** implies a relationship where the child can exist independently of the parent. Example: Class (parent) and Student (child). Delete the Class and the Students still exist

</details>

<details>

<summary>Composition</summary>

**Composition** implies a relationship where the child cannot exist independent of the parent. Example: House (parent) and Room (child). Rooms don't exist separate to a House

</details>

<details>

<summary>Inheritance</summary>

_Inheritance_, refers to the ability of one class (child class) to _inherit_ the identical functionality of another class (super class), and then add new functionality of its own

</details>

<details>

<summary>Implementation / Realization</summary>

A realization relationship is a relationship between two model elements, in which one model element (the client) realizes the behavior that the other model element (the supplier) specifies. Several clients can realize the behavior of a single supplier

</details>

#### Multiplicity

* 1..1: One and only one
* 0..\*: Zero or more
* 1..\*: One or more
* 0..1: Only none or one
* m..n: At least (m) and at most (n) where (m<=n)

