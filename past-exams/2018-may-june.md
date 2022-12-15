---
description: 80 Marks, 2h, Closed Book, Written Exam
---

# 2018 May June

A film production company approached a group of final-year students with some questions surrounding their software needs

## Question 1

1.1 The company requires all their information to be saved to, and read from, file. the following has been suggested as a basic class structure to their software needs, but they have been told that it requires a redesign

<figure><img src="https://i.imgur.com/mHKIurt.png" alt=""><figcaption></figcaption></figure>

Redesign the UML class diagram so that it represents the use of better design principles. Class names should be descriptive of their function / responsibility, and no data members are required

1.2 For a simple prototype of the system a film just has two (2) pieces of information associated with it: title and running time (in hours, expressed as a decimal). Write the class definition for this film class, so that reflective programming for both input and output will be supported. You are not required to provide the class implementation. Consider the following when designing this class

* Data members should not have to be repeated in sub-classes
* No constructors are required

1.3 Write code that would be used to write, and then read, the value of the Film title property, using reflective techniques, for a Film object named filmObject (where 007 is the film title)

1.4 What do you understand by the term "reflective programming"?

1.5 To retrieve the value of an unknown property in reflective programming, you would use the following code&#x20;

```cpp
QMetaProperty mp = filmObject->metaObject()->property(someIndex);
QVariant v = mp.read(filmObject);
```

1.5.1 What is the role of QVariant in such reflective code

1.5.2 How can QVariant(s) be used in a strongly typed language like C++ where an int or QString may be required?

1.6 Regular expressions will be used to determine that correct data will be entered before it is included in the list of productions. Indicate what sort of text will be accepted by the following regular expressions. Minimal marks will be awarded for simply describing the regular expression components

1.6.1 \[a-zA-Z]\*\[0-9]+\[A-Za-z]\*

1.6.2 \d+(\[.]\d)?

## Question 2

2.1 Qt's approach to the MVC design pattern is model / view programming. Briefly describe Qt's model / view architecture by referring to the MVC design pattern and how the handling of the user interface is managed

2.2 Distinguish between QAbstractTableModel, QStandardItemModel, QTableView, QTableWidget, and QAbstractProxyModel by explaining how and / or where each is used to manage tabular data

2.3 Consider the code below

```cpp
MainWindow::MainWindow(QWidget *parent) : QMainWindow(parent){
    tableModel = new QStandardItemModel(this); //Declared in header
    QTableView tableView = new QTableView(this);
    //add code here
    connect(tableModel, SIGNAL(itemChanged(QStandardItem*)), this, SLOT(update(QStandardItem*)));
}

void MainWindow::update(QStandardItem *selectedItem){
    int col = selectedItem->column();
    if(col == 2){
        float runTime = selectedItem->data(Qt::DisplayRole).toFloat();
        selectedItem->setData(QString::number(price, 'f', 2), Qt::DisplayRole);
        //add code here
    }
}
```

Here are some member functions that you could consider using in your answers to the questions below

```cpp
QColor /* can be */ Qt::white, Qt::yellow /* and so on*/
void QStandardItem::setbackground(QBrush)
int QStandardItem::row()
int QStandardItem::column()
int QStandardItemModel::columnCount()
int QStandardItemModel::rowCount()
QStandardItem QStandardItemModel::item(int row, int column)
```

2.3.1 What is the main benefit of using "this" in lines 3 and 4?

2.3.2 Provide code for line 5 that will allow updates in the model to be automatically visible in the view

2.3.3 Describe the purpose of lines 13 and 14

2.3.4 Write code at line 15 that would highlight a row in yellow where the running time is greater than 2 hours, and in white otherwise. You should not use delegates to achieve this.

## Question 3

A list of actors is maintained by a class named ActorList. It has been determined that several output procedures are required, that is, output to a console, human-readable text file, and XML file

3.1 Provide a UML class diagram that presents the above proposal in the form of a strategy design pattern. Include the relationship with ActorList and the client application / GUI (which contains an instance of the ActorList)

3.2 What two benefits does using a strategy provide in this scenario?

3.3 Write the code for the base class of the strategy pattern. This class should not allow implementations of the functions that form its interface

3.4 Consider the ActorList class below

```cpp
class ActorList{
public:
    ~ActorList();
    static ActorList *getActorList();
    bool addActor(Actor *a);
    int size() const;
    Actor *getActor(int i);

private:
    ActorList();
    static ActorList *actorList;
    QList<Actor*> list;   
};
```

3.4.1 Which design pattern has been implemented here?

3.4.2 Why is the getActorList() function static?

3.4.3 Write the necessary implementation code for this class. You do not need to include code for the addActor(), size(), getActor(), or ActorList() functions

3.5 Since one of the strategies is to generate output in XML, complete the following code, which uses DOM to write an ActorList instance to XML. Assume that this class has access to the ActorList list instance containing the data to be written. Use the ActorList class in 3.4 in this answer

```cpp
QDomDocument OutputToXml::generateXML(){
    QDomDocument doc;
    QDomElement root = doc.createElement("ActorList");
    for(counter = 0; counter < list.size(); counter++){
        QString name = list.getActor(counter).getName();
        //add code here
    }
    return doc;
}
```

It should generate the XML in the following format

```xml
<ActorList>
    <Actor>
        <Name>actorname</Name>
    </Actor>
</ActorList>
```

## Question 4

A WriteToFile class has been added to manage the process of writing text to file.

```cpp
class WriteToFile{
public:
    WriteToFile(QStringList t, QString f);
    bool write() const; //This function does the actual writing to file
private:
    QStringList textToWrite;
    QString fileName;
};
```

As disk I/O is a comparatively slow process, it has been decided to run the write to file process in a separate thread.

4.1 rewrite the WriteToFile class so that it can be used in a thread (using the recommended approach to threading)

4.2 Assuming that the variables QStringList tTW contains all the data to be written to file and QString fn holds the name of the file to write to, write code that will allow the data to be written to the appropriate file using WriteToFile::write() in a thread. You need to instantiate all the necessary objects

4.3 UDP stands for User Datagram Protocol

4.3.1 What is a datagram?

4.3.2 How does this approach differ from the way TCP sockets work?
