# Dynamic Properties

```cpp
#include <QObject>

class MyClass : public QObject {
    Q_OBJECT

public:
    MyClass(QObject *parent = nullptr);
    Q_INVOKABLE void setDynamicProperty(const QString &name, const QVariant &value);
    Q_INVOKABLE QVariant dynamicProperty(const QString &name) const;

private:
    QHash<QString, QVariant> m_dynamicProperties;
};

MyClass::MyClass(QObject *parent) : QObject(parent)
{
}

void MyClass::setDynamicProperty(const QString &name, const QVariant &value)
{
    m_dynamicProperties[name] = value;
    setProperty(name.toUtf8().constData(), value);
}

QVariant MyClass::dynamicProperty(const QString &name) const
{
    return m_dynamicProperties.value(name);
}

```

In this example, the `MyClass` class has two public methods: `setDynamicProperty()` and `dynamicProperty()`. The `setDynamicProperty()` method sets the value of a dynamic property with the given name, and the `dynamicProperty()` method returns the value of the dynamic property with the given name.

The dynamic properties are stored in a private `QHash` object, and the `setProperty()` method is used to set the property values in the object.
