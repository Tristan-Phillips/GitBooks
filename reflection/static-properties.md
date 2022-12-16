# Static Properties

A static property is a property that is shared by all instances of a class.

```cpp
#include <QObject>

class MyClass : public QObject {
    Q_OBJECT
    Q_PROPERTY(int staticProperty READ staticProperty WRITE setStaticProperty NOTIFY staticPropertyChanged)

public:
    static int staticProperty();
    static void setStaticProperty(int value);

signals:
    void staticPropertyChanged();

private:
    static int m_staticProperty;
};

int MyClass::staticProperty()
{
    return m_staticProperty;
}

void MyClass::setStaticProperty(int value)
{
    if (m_staticProperty == value)
        return;

    m_staticProperty = value;
    emit staticPropertyChanged();
}

int MyClass::m_staticProperty = 0;

```

In this example, the `staticProperty` property is a static property that is shared by all instances of the `MyClass` class. The property is defined using the `Q_PROPERTY` macro, and its getter and setter methods are implemented as static member functions. The property value is stored in a private static member variable `m_staticProperty`.
