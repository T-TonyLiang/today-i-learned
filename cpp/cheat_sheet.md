## C++ Cheat Sheet

# Table of Contents
  1) [OOP](#object-oriented-programming)
    - Defining Classes
    - Constructors
    - Accessors and Mutators
    

# Object Oriented Programming
## Defining Classes
```cpp
class foo {
public:
  foo(); // constructor
private:
  int bar_; // member variables
}
```

### Member functions vs. Non-member functions
Member functions:
  - functions declared within the class
  - constructors, accessors, mutators, destructors
  - virtual methods
  
Non-member functions: 
  - critical functions of the class that is declared outside of the class
    - reduces number of functions with direct access to private data members
    - some functions has to be non-member
  - I/O operators has to be non-member
  - generally, any operation where one of the arguments is not of the class type should be a non-member function
  
## Constructors
  - a default constructor is defined by the compiler if no constructor is specified
    - initializes member variables to their default value
  - multiple constructors can be defined with different numbers of parameters and types -- overloading

### List Initialization
  - a method of initializing member variables
  - for constructors only
  - generally makes no difference if the member variable is of a default type (ie. bool, int ...)
  - for object types, you would have to use a list initialization if there is a const member variable, since assigning it would cause the compiler to error
  - also for object types, its more efficient to just call the specified object constructor with an argument rather than call the default constructor and then assign the argument. ie. (for an object a which has a member variable int: `a(3) instead of a(); a.x = 3`)
```cpp
foo::foo() : bar_(1) {} // list initialization

// same effect but wihtout list initialization
foo::foo() {
  this->bar_ = 1;
}
```

### Type conversions
  - by default, the compiler uses constructors that have one argument to perform implicit type conversion
    - a maximum of one implicit type conversion is performed
    - this is also true of constructors that have more than one argument, if the rest of the arguments have default values
    - the `explicit` keyword prevents any implicit type conversions. (ie. the types have to match exactly for the parameters)
    ```cpp
    class A {
    public:
      A(int x) {}
    }
    
    class B {
    public:
      B(A a)
    }
    
    int main() {
      B(1); // okay, since B will implicitly convert x to the required a object by using A's constructor for int
    }
    ```
    
## Accessors and Mutators
  - accesses or changes private member variables of the class
  - naming convention:
    - use attribute\_ for the name of a private member variable
    - use attribute() as the accessor name
    - use attributeIs() as the mutator name
  - best practices:
    - mutators should validate client provided values
    - pass parameters by const reference
    - use const member functions

## Default Arguments
  - can be used in constructors and mutators
  - must appear only in function declaration
  - only trailing parameters may have default values
  - once one default argument is used in a function call, all subsequent arguments in call must be defaults
  
## Operator Overloading
  - define an operator action on a class
  - cant create new operations
  - cannot change the number of arguments of an operation
  - best practice:
    - use return types that the client is used to (ie. == returns bool)
  ```cpp
  foo foo::operator+ (const foo &a) const {
    return foo(this->bar() + a.bar());
  }
  ```
