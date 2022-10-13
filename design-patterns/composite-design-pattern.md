# Composite Design Pattern

### Intent

To compose an object into a tree like structure, in order to represent part-whole hierarchies.

The composite lets a client treat individual objects and compositions of objects uniformly

### Applicability

* To represent part-whole hierarchies
* All objects in the composite structure are treated uniformly - the differences between compositions of objects and individual objects are ignored
*

    <figure><img src="https://i.imgur.com/h6rJjYN.png" alt=""><figcaption></figcaption></figure>

### Participants

* A **composite** contains 'components' - a set of children - in a tree structure
* A **component** can either be another 'composite' or a leaf
* A **leaf** has no children

### QT's implementation

Utilizes QT's parent-child relationships

* QObject(QObject \*parent = nullptr)
* QWidget(QWidget \*parent = nullptr, Qt::WindowFlags f = Qt::WindowFlags())
* QPushButton(const QIcon \&icon, const QString \&text, QWidget \*parent = nullptr)
* QGridLayout(QWidget \*parent)
