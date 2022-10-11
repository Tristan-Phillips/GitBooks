# Strategy Design Pattern

### Intent

A Family of algorithms that need to be made interchangeable, based on the context.

The strategy pattern is intended to provide a means to define a family of algorithms, encapsulate each one as an object, and make them interchangeable.

### Applicability

* Enables the selection of an algorithm at runtime
* Defines a family of algorithms, encapsulate each one (Class)
  * Abstract base class, inheritance for concrete classes
* Make them interchangeable - Context keeps reference / pointer to the strategy objects
  * Composition and polymorphism
* Allows the algorithm used to vary independently from clients that use it

### Participants

<figure><img src="https://i.imgur.com/qn5TkDa.png" alt=""><figcaption></figcaption></figure>

* **Strategy** (Abstract) - Declares a common interface for all algorithms (Sub-classes)
* **Context** - uses this interface to call the algorithm as defined by a ConcreteStrategy
  * Passes data to Strategy when instantiated / algorithm is called
  * Forward requests from Client to Strategy
* **ConcreteStrategy** - Implements an algorithm using interfaces defined by the Strategy
* **Client** - Instantiates and passes a ConcreteStrategy object to Context
  * Interacts with Context

### Code Example 1 : Strategy Pattern

```cpp
#include <iostream>
using namespace std;
 
class SortBehavior 
{
    public:
        virtual void sort() const = 0;
};
 
class Merge: public SortBehavior 
{
    public:
        virtual void sort() const {
            cout << "Merge sort()\n";
        }
};
 
class Quick: public SortBehavior {
    public:
        virtual void sort() const {
            cout << "Quick sort()\n";
        }
};
 
class Heap: public SortBehavior
{
    public:
        virtual void sort() const {
            cout << "Heap sort()\n";
        }
};
 
class SearchBehavior 
{
    public:
        virtual void search() const = 0;
};
 
class Sequential: public SearchBehavior 
{
    public:
        virtual void search() const {
            cout << "Sequential search()\n";
        }
};

class BinaryTree: public SearchBehavior 
{
    public:
        virtual void search() const {
            cout << "BinaryTree search()\n";
        }
};

class HashTable: public SearchBehavior 
{
    public:
        virtual void search() const {
            cout << "HashTable search()\n";
        }
};

// Context
class Collection 
{
    private:
        SortBehavior* m_sort;
        SearchBehavior* m_search;
    public:
        Collection(){}
        void set_sort(SortBehavior* s){
            m_sort = s;
        }
        void set_search(SearchBehavior* s){
            m_search = s;
        }
        void sort() const {
            m_sort->sort();
        }
        void search() const {
            m_search->search();
        }
};
 
 
int main(int argc, char *argv[])
{
    Merge merge;
    Quick quick;
    Heap heap;

    Sequential sequential;
    BinaryTree binaryTree;
    HashTable hashTable;
 
    Collection colA;
    colA.set_sort(&merge;);
    colA.sort();

    Collection colB;
    colB.set_search(&binaryTree;);
    colB.search();

    return 0;
}
```

> Output
>
> ```
> Merge sort()
> BinaryTree search()
> ```

In the above we have two interfaces: SortBehavior and SearchBehavior

With this design, other types of objects can reuse our search and sort behaviors because these behaviors are no longer hidden away in our Collection classes

We can also add new behaviors without modifying any of our existing behavior classes

1 - Our instance variables hold a pointer to a specific behavior at runtime

```cpp
class Collection {
    private:
        SortBehavior* m_sort;
        SearchBehavior* m_search;
```

2 - Using the pointer, we can implement each behavior

```cpp
       void sort() const {
            m_sort->sort();
        }
	  void search() const {
            m_search->search();
        }
```

3 - Rather than handling the sort behavior itself, the Collection object delegates that behavior to the object pointed to by **m\_sort**

```cpp
colA.set_sort(&merge;);
colA.sort();
=>
Collection::m_sort->sort();
==>
virtual void sort() const{
    cout << "Merge sort()\n";
}
```

This allows us to change behavior at runtime.

### Code Example 2 : Strategy Pattern

In this example, we have two ways of recording contact information: stream & database.&#x20;

The two classes (**StreamRecord** and **DatabaseRecord** share the same interface for their own implementation of recording data via baseclass member function **store()** which has all the shared implementation methods (actually, api)

```cpp
#include <cassert>
#include <iostream>
#include <string>
using namespace std;

class Record
{
public:
    virtual void start_record() = 0;
    virtual void store_field(const string &name;, const string &value;) = 0;
    virtual void finish_record() = 0;
    virtual ~Record() { }
};

struct ContactData
{
    string first_name, last_name, phone, email;
};

class ContactRecorder
{
public:
    ContactRecorder(Record *a) : m_Record(a)
    {
        assert(a != 0);
    }

    void store(const ContactData &data;)
    {
        assert(m_Record != 0);

        m_Record->start_record();
        m_Record->store_field("first name", data.first_name);
        m_Record->store_field("last name", data.last_name);
        m_Record->store_field("phone", data.phone);
        m_Record->store_field("email", data.email);
        m_Record->finish_record();
    }

private:
    Record *m_Record;
};

class StreamRecord : public Record
{
public:
    StreamRecord(ostream &s;, const string &record;_name = string())
        : m_ostream(s), m_record_name(record_name)
    { }

    void start_record() { m_ostream << m_record_name << "( "; }

    void store_field(const string &name;, const string &value;)
    {
        m_ostream << name << ": " << value << "; ";
    }

    void finish_record() { m_ostream << ")" << endl; }

    void set_record_name(const string &name;) { m_record_name = name; }

private:
    ostream &m;_ostream;
    string m_record_name;
};

class MySql {};

class DatabaseRecord : public Record
{
public:
    DatabaseRecord() : m_dbConnection(new MySql) {}

    void start_record() { cout << "start transaction\n"; }

    void store_field(const string &name;, const string &value;)
    { cout << "insert into table\n"; }

    void finish_record() { cout << "finish transaction\n"; }

private:
    MySql *m_dbConnection;
};

int main()
{
	ContactData data = {"Black", "Smith", "415-675-1874", "adams@email.com"};
	StreamRecord sRecord(std::cout);
	ContactRecorder contact(&sRecord;);
	contact.store(data);

	DatabaseRecord dbRecord;
	ContactRecorder contact2(&dbRecord;);
	contact2.store(data);
	return 0;
}
```

> Output
>
> ```
> ( first name: Black; last name: Smith; phone: 415-675-1874; email: smith@email.com; )
> start transaction
> insert into table
> insert into table
> insert into table
> insert into table
> finish transaction
> ```
