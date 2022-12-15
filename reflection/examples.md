# Examples

```cpp
#ifndef ANOTHERCLASS_H
#define ANOTHERCLASS_H

#include <QObject>
#include <QString>
//Q_PROPERTIES work with QVariant
#include <QVariant>

class AnotherClass : public QObject
{
    //Reflection requires the Q_OBJECT to be defined in all classes that use QProperties
    //Q_PROPERTIES must be defined in the header file and at the top of the class under the Q_OBJECT
    //Macros do not end with a semicolon
    //Use CONSTANT to remove the annoying warning about the property being read-only
    //You can use NOTIFY to specify a signal to be emitted when the property changes
    //Macro variables do not represent the actual variable name, but rather the name of the property
    Q_OBJECT
    Q_PROPERTY(QString name READ getName WRITE setName NOTIFY valueChanged(QString))
    Q_PROPERTY(int age READ getAge WRITE setAge NOTIFY valueChanged(QString))

public:
    explicit AnotherClass(QObject *parent = nullptr);
    
    void setName(QString &name);
    QString getName() const;

    void setAge(int age);
    int getAge() const;

signals:
    //Signals are used to notify other classes that a property has changed
    //This signal will be connected to both Q_PROPERTIES
    //And the signal will be connected to a function in the main.cpp file
    //Signals do not have implementations
    void valueChanged(QString value);

private:
    QString m_name;
    int m_age;
};

#endif // ANOTHERCLASS_H

//Example of emit()
void AnotherClass::setAge(int age)
{
    m_age = age;
    //Required because the Q_PROPERTY ends with CONSTANT
    emit valueChanged(" Age: " + this->property("age").toString());
}

//Example of getting data from a QMetaObject and seting data
void setProperty(QObject *object, QString propertyName, QVariant value)
{
    //Get the index of the property
    int index = object->metaObject()->indexOfProperty(propertyName.toStdString().c_str());

    //Set the property
    object->metaObject()->property(index).write(object, value);
}

//Example of cycling through QMetaObject w/ QMetaProperty
void cycleThroughProperties(QObject *object)
{
    const QMetaObject *metaObject = object->metaObject();
    //Start at 1 to skip the QObject object name property
    for (int i = 1; i < metaObject->propertyCount(); ++i)
    {
        QMetaProperty metaProperty = metaObject->property(i);
        qDebug() << "";
        qDebug() << "Property name:" << metaProperty.name();
        qDebug() << "Property type:" << metaProperty.typeName();
        qDebug() << "Property value:" << metaProperty.read(object);
        qDebug() << "";
    }
}

//How to emit through a connect when it has a value
    QObject::connect(anotherClass, &AnotherClass::valueChanged, [&variableAlteredBySignal](QString value)
    {
        variableAlteredBySignal += value;
    });
	
//How a normal connection looks
	connect(pushButton, &QPushButton::clicked, this, &MainWindow::action);

//Get class name using QMetaObject
	QString className = (QObject)->metaObject()->className();
	
//Get the name of a QObject sender
	QString sender = QObject::sender()->objectName();
```
