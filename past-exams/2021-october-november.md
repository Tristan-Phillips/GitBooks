---
description: 80 Marks, 2h, Open Book, Written exam
---

# 2021 October November

All businesses need to manage their communication, and the simplified scenario used in this examination is based on communication strategies. The idea is that a user can select a type of communication channel and have a message sent out on that channel at some specific point in time. The application itself allows the user to set up the required options and just the strategy and message will be displayed for the purposes of a brief history of messages sent – See Figure 1

<figure><img src="https://i.imgur.com/tn5i7kd.png" alt=""><figcaption></figcaption></figure>

## Question 1

Apply the strategy design pattern to the scenario above that would also adhere to the following requirements.

1. There are currently 3 basic strategies/channels for communication: Signal, SMS, and WhatsApp. Your design should include a strategy for each channel
2. All that is needed to create one of these is a type name
3. Once an appropriate type has been created, a setUp() function would be used to populate object instance data members, and the communicate() function used to process the required communication

A CommunicationStrategy UML class diagram has already been drawn up – see Figure 2. Note that you may abbreviate this class name to ComStrat in your answers

<figure><img src="https://i.imgur.com/82gnsBu.png" alt=""><figcaption></figcaption></figure>

1.1 Considering the scenario given and design decisions listed above, draw a UML class diagram for the strategy pattern. You should include the necessary classes, class attributes, class constructors and operations, and class relationships to make it clear you understand how data will be managed and passed between classes. Label all relationships indicated; however, you do not have to include the Client/GUI class nor indicate access specifiers. \[You may use a software tool to create the UML class diagram. If you are hand drawing this answer, you can use an underline to indicate italics in the UML class diagram.]

<figure><img src="https://i.imgur.com/bZmzA0d.png" alt=""><figcaption><p>Answer</p></figcaption></figure>

1.2 The provided UML class diagram included some of the text in italics. What does this indicate?

<details>

<summary>Answer</summary>

* The class is abstract
* The method is pure virtual

</details>

1.3 Describe what the function of the communicate() function would be in this design pattern?

<details>

<summary>Answer</summary>

* Base class - Abstract, no implementation
* Derived classes - Implement actual sending of messages on appropriate platform

</details>

1.4 The decision has been taken to initially host this application using cloud computing. Would you recommend a public or private cloud model?

<details>

<summary>Answer</summary>

Public cloud: No capital expenditure, low initial cost and rapid deployment

</details>

## Question 2

This question relates to the code for creating and setting up of the required strategies.

The setUp() function in the CommunicationStrategy class (see Figure 2) is used to populate the data members in an instance object. This function does the following.&#x20;

* It first checks that the user code meets a particular pattern.
* If the user code does not meet requirements, the function returns false. If the user code does, the function returns true.
*   Additionally, if the user code meets requirements,&#x20;

    * all data member values are populated, and
    * a signal (created()) is emitted that sends the communication strategy type and the message (separate by a colon) as a QString.&#x20;

    See the viewing window in Figure 1

2.1 Write the code for the class definition for the CommunicationStrategy class (that is, what would be in the header file). Ensure that all functionality shown in Figure 2 and that given above is included

<details>

<summary>Answer</summary>

```cpp
//Definition
	class CommunicationStrategy : public QObject{
		Q_OBJECT
	public:
		CommunicationStrategy(QObject *parent = null);
		bool setUp(QString uc, QDateTime dt, QString m);
		virtual void communicate() = 0;
	signals:
		void created(QString);
	private:
		QString userCode;
		QDateTime send;
		QString message;
	};

```

</details>

2.2 Write the regular expression that can be used to check whether a string meets the following requirements:

* The first character should be a G, K, or W (for Gauteng, KwaZulu-Natal and Western Cape)
* The second character could be any uppercase alphabetic character
* This should be followed by one or more lowercase alphabetic characters or digits
* The final character should be the same as the first character

<details>

<summary>Answer</summary>

"(\[GKW])(\[A-Z])(\[a-z\d]+)\1"

</details>

2.3 Write the code for bool CommunicationStrategy::setUp(QString uc, QDateTime dt, QString m). Use the information you have so far in this question to guide you, where the regular expression in 2.2 will be used to check the user code

Note the structure of the signal sent out: “Strategy:message”. Without using a data member within the class, the type of strategy or class (Signal, SMS, or WhatsApp) should be indicated before the colon

<details>

<summary>Answer</summary>

```cpp
bool CommunicationStrategy::setUp(QString uc, QDateTime dt, QString m){
    QRegularExpression re("([GKW])([A-Z])([a-z\d]+)\1");
    QRegularExpressionMatch match(re.match(uc));
    
    if(match.hasMatch()){
        userCode = uc;
        send = dt;
        message = m;
        
        QString strategy(this->metaObject()->className());
        emit created((strategy+":"+m));
        return true;
    }
    return false;
}
```

</details>

2.4 The signal that is emitted by setUp() is picked up by the GUI/client code and used to populate the viewing window in Figure 1. What various widgets could be used to hold this information, explaining what would need to be in place to make such use possible?

<details>

<summary>Answer</summary>

* QTextEdit / QPlainTextEdit - Can be used directly
* QListWidget - Convenience class, model and view combined
* QTableView - Requires a suitable model (QStandardItemModel) to be linked to the view

</details>

2.5 The signal that is emitted by setUp() could be seen as an implementation of which design pattern? Explain why you say so

<details>

<summary>Answer</summary>

* QT's Signals and Slots is an implementation of the Observer Pattern
* CommunicationStrategy object is the 'observed' object that notifies when something happens
* Other connected objects are the 'Observers' that react / respond to the signal emitted by setup()

</details>

2.6 Based on the CommunicationStrategy class set up in 2.1, would the following code be legal? Explain why or why not. Note that marks are allocated only for the reason given

```cpp
// assume cs is a pointer to some valid CommunicationStrategy
object
cs->setProperty("priority","high");
```

<details>

<summary>Answer</summary>

* Yes, it is legal
* CommunicationStrategy inherits QObject, so properties can be set
* No fixed properties defined, so would set a dynamic property named "priority"

</details>

## Question 3

This question relates to the writing of the data in the viewing window to an XML file.&#x20;

Assume that the data in the viewing window can be stored in QStringList list for use in the writing-to-XML process, where each line consists of the string of characters as seen in the viewing window in Figure 1. This list must be passed to an object instance of a class that should be run as a thread.&#x20;

The XML file should take the following format

```xml
<communications>
    <communication channel="Signal">
        <message>Remember to get your COVID19 vaccination.</message>
    </communication>
    <communication channel="SMS">
        <message>Wishing you a happy festive season.</message>
    </communication>
    <communication channel="WhatsApp">
        <message>Good luck for the exams!</message>
    </communication>
</communications>
```

3.1 The following code has been provided for the class header file. However, this is not considered good practice. Change the code so that it meets what is considered good practice and will support being run as a thread

<pre class="language-cpp"><code class="lang-cpp">class WriteToXML: public QThread
{
public:
    WriteToXML(QStringList s);
    void doWrite(); // does the write to file in XML
private:
<strong>    QStringList strlist;
</strong>}
</code></pre>

<details>

<summary>Answer</summary>

```cpp
class WriteToXML : public QObject{
    Q_OBJECT
public:
    WriteToXML(QStringList s);
public slots:
    void doWrite(); //Writes to file in XML
signals:
    void finished();
private:
    QStringList strList;
};
```

</details>

3.2 Assuming that the string list passed to WriteToXML has been saved to strList in the class constructor, write the code for the doWrite() function so that each line in the string list is written to file in the format above, using DOM. A portion of the code is given below and you have to add the missing parts in the appropriate places

```cpp
void WriteToXML::doWrite()
{
    QDomDocument doc;
    foreach(QString s, strlist)
    {
    
    }
    QFile file("data.xml");
    file.open(QIODevice::WriteOnly);
    file.close();
}
```

<details>

<summary>Answer</summary>

```cpp
void WriteToXML::doWrite(){
	QDomDocument doc;
	QDomElement root = doc.createElement("communications");
	doc.appendChild(root);
	
	foreach(QString s, strlist){
		QStringList listSplit = s.split(":");
		QDomElement channel = doc.createElement("communication");
		channel.setAttribute("channel", listSplit[0]);
		QDomText message = doc.createTextNode(listSplit[1]);
		
		channel.appendChild(message);
		root.appendChild(channel);
	}
	
	QFile file("data.xml");
	file.open(QIODevice::WriteOnly);
	QTextStream out(&file);
	out << doc.toString();
	file.close();
}

```

</details>

3.3 Write the code that would be included in the GUI/client code that would run an instance of this class as a thread. There is no output that needs to be handled as the output is written to file. Assume that no object instances have been created yet

<details>

<summary>Answer</summary>

```cpp
QStringList strlist;
WriteToXML *xml(new WriteToXML(strlist));
QThread *thread(new QThread);

xml->moveToThread(thread);

connect(thread, &QThread::started, xml, &WriteToXML::doWrite);
connect(xml, &QThread::finished, thread, &QThread::quit);
connect(xml, &QThread::finished, xml, &QObject::deleteLater);
connect(thread, &QThread::finished, thread, &QObject::deleteLater);

thread->start();
```

</details>

3.4 When running the code that had been set up by a novice, the IDE gave the message “QThread: Destroyed while thread is still running” and no data was written to file.&#x20;

Explain what the problem could be and how to solve it

<details>

<summary>Answer</summary>

* Thread declared with local scope, and gets destroyed when method returns before thread has finished / been destroyed
* Solution -
  * Declare thread object as class member (Global scope within class)
  * Implement worker 'Finished' signal to be emitted when worker task is completed and connect to thread quit() slot
  * Connect finished signals to thread and worker deleteLater() slots

</details>

3.5 Suppose that this XML file were to be read in to another application. One developer noted that as DOM was used to write the file, DOM will have to be used to parse it again. Comment on this statement

<details>

<summary>Answer</summary>

* Not necessary, can use SAX, DOM or Stream Reader
* XML is a standard specification, and can therefore be parsed by any method

</details>
