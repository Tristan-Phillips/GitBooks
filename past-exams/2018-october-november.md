---
description: 75 Marks, 2h, Closed Book, Written Exam
---

# 2018 October November

## Question 1

Use the following code to answer the questions that follow

```cpp
//class definition
class Counter{
public:
    Counter(int i);
    void increment(int i);
    voide decrement(int i);
    void displayState(QString message = "Current value") const;
private:
    int num;
};

//class implementation
Counter Counter(int i) : num(i){
}

void Counter::increment(int i){
    num += 1;
    displayState("Number incremented to");
}

void Counter::decrement(int i){
    num -= 1;
    displayState("Number decremented to:";
}

void Counter::displayState(QString message) const{
    QMessageBox::information(0, "Information", QString("%1 %2").arg(message).arg(num), 0, 0);
}
```

1.1 Explain why only the function displayState() is made const in Counter?

1.2 The Counter class is an example of the God Object anti-pattern. Explain two responsibilities that are handled by Counter

1.3 Write code to restructure Counter in order to handle its responsibilities in two different classes without changing its overall functionality. These two classes must be decoupled from one another (independent of each other) by using signals and slots

1.4 Write a few lines of code to demonstrate how the two classes in 1.3 can be used together

1.5 Modify Counter (either the given one or the modified one in 1.3) so that the state of a Counter object can be accessed via the QMetaObject interface

1.6 Demonstrate how a dynamic property can be added to a Counter object. Provide code to instantiate the object and the line of code to add the dynamic property

1.7 List one similarity and one difference between dynamic properties and properties accessed via the QMetaObject interface in the Qt framework

## Question 2

2.1 Explain the three components of the MVC pattern

2.2 Refer to the code below to answer the questions that follow

A staff member is modelled using their name, staff number and performance rating in the class Staff. The class StaffModel is used to set up a model to store a set of staff names, numbers and performance ratings

```cpp
class StaffModel : public QAbstractTableModel {
public:
    StaffModel(QObject *parent=0);
    QVariant data(const QModelIndex &index, int role) const;
    bool setData(const QModelIndex &index, const QVariant &value, int role);
    void addRow(Staff *s);
    void deleteRow(int row);
private:
    QList<QString> names;
    QList<int> numbers;
    QList<int> performance;
};
```

2.2.1 What is the purpose of the data() function in the StaffModel class?

2.2.2 Write code for the data() function. You only need to provide code for Qt::DisplayRole functionality

2.3 Qt includes delegates as part of its model-view framework

2.3.1 Explain the use of delegates in the Qt implementation of the model-view framework

2.3.2 Given the code snippet below and the StaffModel class in 2.2, add the necessary code to show how you would use a delegate named MyDelegate for the performance column.

```cpp
StaffModel *myModel = new StaffModel();
QTableView *myTableView = new QTableView();
myTbaleView->setModel(myModel);
//Add code here to use the delegate
```

2.3.3 Assuming that the definition of MyDelegate is as follows, what functionality does the QStyledItemDelegate class provide?

```
class MyDelegate : public QStyledItemDelegate{
public:
    MyDelegate(QObject *parent=0);
};
```

## Question 3

The Memento pattern is used for capturing and externalizing the internal state of an object

3.1 When would the ability to hold the internal state of an object be useful?

3.2 Draw a UML diagram to illustrate the key classes, its data members and member functions, and the relationships between these key classes in the Memento pattern

3.3 Describe the main roles of the classes in the UML diagram given as answer to 3.2

3.4 Assume that a Staff object can store its state in a QStringList named state, and a StaffMemento needs to be created to hold this state

3.4.1 Write the class definition of StaffMemento that would allow only a Staff object to have access to it. Do not write implementations for any functions that you include

3.4.2 Write code to implement the appropriate function of the Staff class that will be used to create StaffMemento

## Question 4

Refer to the following UML class diagram to answer the questions that follow

<figure><img src="https://i.imgur.com/kT5GOKv.png" alt=""><figcaption></figcaption></figure>

In the UML diagram Client is coupled with the concrete classes MergSort, InsertionSort and BubbleSort. Even though the solution provided in the class diagram works, it has some disadvantages,&#x20;

1. Client is aware of all the concrete sort classes
2. Client is not able to use these concrete sort algorithms interchangeably without knowing all the concrete sort classes and
3. Client needs to be changed if new concrete displays are added

To overcome these issues the Abstract Factory design pattern can be used so that the creation of the concrete algorithms, particularly sort algorithms in this case, is completely decoupled from Client

4.1 Re-draw the given class diagram to incorporate the suggested design pattern. Indicate the key functions as indicated in the given diagram

4.2 Explain briefly how the revised structure solves problems (1), (2) and (3) given in the introduction of the question
