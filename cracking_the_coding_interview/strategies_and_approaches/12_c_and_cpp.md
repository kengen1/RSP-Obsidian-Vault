# C and C ++

### Classes and Inheritance 
```cpp
#include <iostream>
using namespace std;

#define NAME_SIZE 50 // Defines a macro

class Person {
    int id; // all members are private by default
    char name[NAME_SIZE];

    public:
        void aboutMe() {
            cout << "I am a person.";
        }
};

class Student : public Person {
    public:
        void aboutMe() {
            cout << "I am a student.";
        }
};

int main() {
    Student * p = new Student();
    p->aboutMe(); // prints "I am a student"
    delete p;
    return 0;
}
```

### Constructors and Destructors

```cpp
// Constructors

Person(int a) {
    id = a;
}

// OR ~

Person(int a) : id(a) {
    //...
}

// Destructors
~Person() {
    delete obj;
}
```


### Virtual Fucntions
- allow you to achieve runtime polymorphism by deferring function resolutions until runtime rather than compile-time

```cpp
// Static Binding (default behaviour)
class Person {
public:
    void aboutMe() {
        cout << "I am a person." << endl;
    }
};

class Student : public Person {
public:
    void aboutMe() {
        cout << "I am a student." << endl;
    }
};

int main() {
    Person *p = new Student();
    p->aboutMe(); // Prints: "I am a person."
    delete p;
    return 0;
}
```

```cpp
//Dynamic Binding (with virtual functions)
class Person {
public:
    virtual void aboutMe() {
        cout << "I am a person." << endl;
    }
};

class Student : public Person {
public:
    void aboutMe() override { // `override` ensures you're correctly overriding a base virtual function.
        cout << "I am a student." << endl;
    }
};

int main() {
    Person *p = new Student();
    p->aboutMe(); // Prints: "I am a student."
    delete p;
    return 0;
}
```

### Virtual Destructors
- when a base class destructor is not virtual, deleting a derived object using a base class pointer will only call the desctructor of the base class
- this leads to resource leaks or undefined behaviour

```cpp
// Example Without Virtual Destructor
#include <iostream>
using namespace std;

class Person {
public:
    ~Person() { // Not virtual
        cout << "Person destructor called." << endl;
    }
};

class Student : public Person {
public:
    ~Student() {
        cout << "Student destructor called." << endl;
    }
};

int main() {
    Person* p = new Student();
    delete p; // Only Person destructor is called
    return 0;
}

// Output:
// Person destructor called.
```

```cpp
// Correct Deallocation of Memory With Virtual Desctructor
#include <iostream>
using namespace std;

class Person {
public:
    virtual ~Person() { // Virtual destructor
        cout << "Person destructor called." << endl;
    }
};

class Student : public Person {
public:
    ~Student() {
        cout << "Student destructor called." << endl;
    }
};

int main() {
    Person* p = new Student();
    delete p; // Both Student and Person destructors are called
    return 0;
}

// Output:
// Student destructor called.
// Person destructor called.

```

### Default Values
```cpp
int func(int a, int b = 3) {
    x = a;
    y = b;
    return a + b;
}

w = func(4);
z = func(4, 5);
```

### Operator Overloading
- enables us to apply operators like  + to objects that would otherwise not support these operations

```cpp
//Example
Bookshelf Bookshelf::operator+(Bookshelf &other) {
    //add another bookshelf ...
}
```

### Pointers and References

```cpp
// Passing by Pointer vs. Reference
#include <iostream>
using namespace std;

void modifyByPointer(int* ptr) {
    *ptr = 20; // Modify the value at the pointer's address
}

void modifyByReference(int& ref) {
    ref = 30; // Modify the value through the reference
}

int main() {
    int x = 10;

    modifyByPointer(&x);
    cout << "After modifyByPointer: " << x << endl; // 20

    modifyByReference(x);
    cout << "After modifyByReference: " << x << endl; // 30

    return 0;
}
```

### Templates
- a way of reusing code to apply the same class to different data types

```cpp
// Example for swapping two variables with unknown datatypes

#include <iostream>
using namespace std;

template <typename T> // Template declaration
void swapValues(T& a, T& b) {
    T temp = a; // Use the type T for the temporary variable
    a = b;
    b = temp;
}

int main() {
    int x = 10, y = 20;
    cout << "Before swap: x = " << x << ", y = " << y << endl;
    swapValues(x, y); // Works with integers
    cout << "After swap: x = " << x << ", y = " << y << endl;

    double a = 1.1, b = 2.2;
    cout << "Before swap: a = " << a << ", b = " << b << endl;
    swapValues(a, b); // Works with doubles
    cout << "After swap: a = " << a << ", b = " << b << endl;

    return 0;
}
```