# C and C++ Interview Questions

## 1. What is the difference between C and C++?
Answer: C is a procedural programming language, while C++ is an object-oriented programming language that also supports procedural programming. C++ provides features like classes, inheritance, polymorphism, and encapsulation.

## 2. What are constructors and destructors in C++?
Answer:
Constructor: A special member function that is automatically called when an object of a class is created. It initializes the object's attributes.
Destructor: A special member function that is automatically called when an object is destroyed. It cleans up resources allocated to the object.

### Code Example:

```c++
#include <iostream>
using namespace std;

class Sample {
public:
    Sample() { // Constructor
        cout << "Constructor called!" << endl;
    }
    
    ~Sample() { // Destructor
        cout << "Destructor called!" << endl;
    }
};

int main() {
    Sample obj; // Constructor is called
    return 0; // Destructor is called when obj goes out of scope
}
```

## 3. What is a pointer in C? How do you use it?
Answer: A pointer is a variable that stores the memory address of another variable. Pointers are used for dynamic memory allocation, arrays, and functions.

### Code Example:


```c
#include <stdio.h>

int main() {
    int var = 10;
    int *ptr = &var; // Pointer to var

    printf("Value of var: %d\n", var);
    printf("Address of var: %p\n", (void*)&var);
    printf("Value pointed by ptr: %d\n", *ptr);
    printf("Address stored in ptr: %p\n", (void*)ptr);

    return 0;
}
```

## 4. Explain the concept of a structure in C.
Answer: A structure is a user-defined data type that allows grouping different data types under a single name. It is useful for organizing complex data.

### Code Example:

```c
#include <stdio.h>

struct Student {
    char name[50];
    int age;
    float gpa;
};

int main() {
    struct Student student1;
    
    // Assigning values
    snprintf(student1.name, sizeof(student1.name), "Alice");
    student1.age = 20;
    student1.gpa = 3.5;

    // Printing values
    printf("Name: %s\n", student1.name);
    printf("Age: %d\n", student1.age);
    printf("GPA: %.2f\n", student1.gpa);

    return 0;
}
```

## 5. Explain inheritance in C++. What are its types?
Answer: Inheritance allows a class to inherit properties and methods from another class. The class that inherits is called the derived class, and the class from which it inherits is called the base class. 

#### Types of inheritance include:
- Single Inheritance
- Multiple Inheritance
- Multilevel Inheritance
- Hierarchical Inheritance
- Hybrid Inheritance


### Code Example:


```c++
#include <iostream>
using namespace std;

// Base class
class Animal {
public:
    void speak() {
        cout << "Animal speaks!" << endl;
    }
};

// Derived class
class Dog : public Animal {
public:
    void bark() {
        cout << "Dog barks!" << endl;
    }
};

int main() {
    Dog myDog;
    myDog.speak(); // Inherited method
    myDog.bark();  // Dog's own method
    return 0;
}
```

## 6. Explain polymorphism in C++. What are its types?
Answer: Polymorphism allows methods to do different things based on the object it is acting upon. There are two types of polymorphism in C++:
Compile-time Polymorphism: Achieved through method overloading and operator overloading.
Runtime Polymorphism: Achieved through function overriding using virtual functions.

## Code Example (Runtime Polymorphism):

```c++
#include <iostream>
using namespace std;

class Base {
public:
    virtual void show() { // Virtual function
        cout << "Base class show function called." << endl;
    }
};

class Derived : public Base {
public:
    void show() override { // Overriding base class function
        cout << "Derived class show function called." << endl;
    }
};

int main() {
    Base* b;           // Base class pointer
    Derived d;        // Derived class object
    b = &d;           // Assigning derived class object to base pointer

    b->show();        // Calls Derived's show() due to runtime polymorphism
    return 0;
}
```

## 7. What is a template in C++? Provide an example.
Answer: Templates allow functions and classes to operate with generic types. This enables code reusability by allowing one function or class to work with different data types.

### Code Example:

```c++
#include <iostream>
using namespace std;

// Function template
template <typename T>
T add(T a, T b) {
    return a + b;
}

int main() {
    cout << "Add integers: " << add(5, 10) << endl; // Using template with int
    cout << "Add doubles: " << add(5.5, 2.2) << endl; // Using template with double
    return 0;
}
```

## 8. Explain the difference between struct and union.
Answer:
Struct: A struct allocates memory for all its members, allowing them to hold different values simultaneously.
Union: A union allocates memory equal to the size of its largest member, meaning only one member can hold a value at any time.

### Code Example:


```c
#include <stdio.h>

struct MyStruct {
    int a;
    float b;
};

union MyUnion {
    int a;
    float b;
};

int main() {
    struct MyStruct s;
    union MyUnion u;

    s.a = 10;
    s.b = 20.5;
    u.a = 10; // Only u.a is valid here

    printf("Struct: a = %d, b = %.2f\n", s.a, s.b);
    printf("Union: a = %d\n", u.a);

    u.b = 20.5; // Now u.b is valid
    printf("Union after assigning b: a = %d, b = %.2f\n", u.a, u.b); // a is now undefined

    return 0;
}
```

## 9. What is the purpose of the static keyword in C?
Answer: The static keyword has two primary uses:
When applied to a variable inside a function, it retains its value between function calls.
When applied to a global variable or function, it restricts its visibility to the file in which it is declared.


### Code Example:


```c
#include <stdio.h>

void staticExample() {
    static int count = 0; // Retains its value between calls
    count++;
    printf("Count: %d\n", count);
}

int main() {
    for (int i = 0; i < 5; i++) {
        staticExample();
    }
    return 0;
}
```

## 10. What is the purpose of the virtual keyword in C++?
Answer: The virtual keyword is used to declare a virtual function, which allows derived classes to override it. This enables runtime polymorphism, allowing the program to determine which function to call at runtime based on the object type.


### Code Example:


```c++
#include <iostream>
using namespace std;

class Base {
public:
    virtual void display() {
        cout << "Display from Base class" << endl;
    }
};

class Derived : public Base {
public:
    void display() override {
        cout << "Display from Derived class" << endl;
    }
};

int main() {
    Base* b = new Derived();
    b->display(); // Calls Derived's display() due to virtual function
    delete b;
    return 0;
}
```

## 11. What is the difference between malloc() and calloc()?
Answer:
malloc() allocates a specified number of bytes and returns a pointer to the first byte. It does not initialize the allocated memory.
calloc() allocates memory for an array of elements, initializing them to zero.

### Code Example:

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int *arr1, *arr2;
    int n = 5;

    // Using malloc()
    arr1 = (int*)malloc(n * sizeof(int));
    if (arr1 == NULL) {
        printf("Memory allocation failed\n");
        return 1;
    }

    // Using calloc()
    arr2 = (int*)calloc(n, sizeof(int));
    if (arr2 == NULL) {
        printf("Memory allocation failed\n");
        free(arr1);
        return 1;
    }

    printf("Array using malloc: ");
    for (int i = 0; i < n; i++) {
        printf("%d ", arr1[i]); // Uninitialized values
    }

    printf("\nArray using calloc: ");
    for (int i = 0; i < n; i++) {
        printf("%d ", arr2[i]); // All values initialized to 0
    }

    free(arr1);
    free(arr2);
    return 0;
}
```

## 12. Explain the concept of dynamic memory allocation in C.
Answer: Dynamic memory allocation allows you to allocate memory at runtime using functions like malloc(), calloc(), realloc(), and free(). This is useful for creating data structures whose size can change during execution.

### Code Example:


```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int *arr;
    int n = 5;

    // Allocating memory
    arr = (int*)malloc(n * sizeof(int));
    if (arr == NULL) {
        printf("Memory allocation failed\n");
        return 1;
    }

    // Initializing and printing the array
    for (int i = 0; i < n; i++) {
        arr[i] = i + 1;
        printf("%d ", arr[i]);
    }

    // Freeing allocated memory
    free(arr);
    return 0;
}
```
