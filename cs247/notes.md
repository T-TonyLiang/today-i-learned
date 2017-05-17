## CS 247: Introduction to Software Principles

# Abstract Data Types (ADTs)

## "Outside-In Design"
  1) start with client use cases & environment
  2) interface code, and test cases
  3) define class functionality

  - In each phase, test and refine.
  - Ensuring consistency across interfaces when designing; complete? encapusulated? meets needs?

### Rational Number ADT
  - legal default value? (0)
  - math ops, using operators +-*/% instead of method names
  - I/O operators
  - copy operator, copy constructor

### Legal Values
Q: How to deal with illegal values?
A:  
  - Error message
  - set to legal value(?)
  - ext pgm
  - exceptions
  - return code (not on constructor)
  
## Public Accessors and Mutators

### const method:
  - use liberally
  - let compiler help you catch mistakes
  - pass parameters by const reference (most flexible approach)

*use const_cast for casting types instead of (type) in parentheses
  
```cpp
attribute_; //data
attribute(); //accessor
attributeIs(...); //mutator
```

## Operator Overloading
First be aware of factors over which you have no control:
  - can't introduce new operators. eg. no "++" for exponents
  - can't change order of operator evaluation
  - can't change # of arguments

However, we can choose in the signature:
  - return type
  - argument types (within limits)
  - whether to pass by reference or pass by value
  - whether or not its a constructor or not
  - whether or not its a member (once again, within limits)
  - N.B. don't change the operator meaning i.e. dont make

#### Counter-intuitive:
C++ 11 introduced "move" semantics: compilers had "return value optimization" => write temporary object directly into "assigned space".

### operator>>, operator<<
```cpp
ostream& operator<< (ostream &os, const RationalNumber &r) {
  const char slash = '/';
  os << r.numerator_ << slash << r.denominator_;
  
  return os;
}

istream& operator>> (istream &is, RationalNumber &r) {
  int num, denom;
  char slash;
  is >> num >> slash >> denom;
  
  // catch any errors with input, but no specific validators for the slash
  if (is.fail()) return is;
  r.numeratorIs(num);
  r.denominatorIs(denom);
}
```

#### Q: What has to be a member?
  - accessors & mutators
  - constructors (incl. copy, move and [] indexing which are assignments)
  - destructor
  - virtual methods

#### Q: What cant be a member?
  - I/O operators
  - more generally, any operation where we don't want the first argument to be the class type (i.e. `int i; RationalNumber r` where we output i+r )
  
**Otherwise**, perfer non-member and non-friend:
  - less code affected if implementation changes
  - more secure since it has to use accessors/mutators
  
### Type Conversion of ADT objects
Q: How does a compiler find a conversion function?
  1) Exact match
  2) Lossless conversion via "promotion" (i.e. bool => int, float => double)
  3) standard conversions eg. double => int, int => double (might lose some data)
  4) user defined conversions

Q: What happens if theres more than 1 match?
  - if 2 or more matches are at the same level, choice is ambiguous, so compiler stops with error
  - otherwise, find the best possible match on argument basis
    - if one function is at least as good for all arguments and better than all for one, it wins
    - otherwise it's ambiguous

Examples:
```cpp
class X {public : X(int); X(string); };
class Y {public : Y(int); };
class Z {public : Z(X); };
public X f(X);
public Y f(Y);
public Z g(Z);
public X operator+(X, X);

string s {"mack"}; // new constructor syntax
f(X(1)); // ok
f(1); // ambiguous, compiler doesnt know whether '1' is of class X or Y
g(X(s)); // ok, X(s) -> Z implicitly via the constructor of Z
g(Z(s)); // ok, s -> X(s) implicitly
g(s); // not ok, can't implicitly invoke two constructors (creates X from s and Z from X to satisify g(Z))
X x1 = 1 + 1; // ok, implicitly creates X from '1' twice and invokes the + operator
```

## Helper Functions
  - use private methods or anonymous functions for helper functions
  
## Attribute-based ADTs
  - ADT primarily composed of "virtual data members", accessors & mutators
  - All other functions are non-member
  => makes it easy to write the contract for the ADT
  - Virtual data members: may not have actual storage, since it could be computed from other values. Changing an attribute may also cause a (re)computation to other attributes as a side effect.
  
### Safety
  - enforces rage of legal values
  - compiler reports type of incompatibilities

### Evolvability
  - ADT is stable ie. client code needen't chant if implementation changes
  
### Efficiency
  - only areas we need to check for legal values are: constructors and mutators (both member and non-member)

_**Exercise:**Design an ADT for Date, Money or SIN_

# Value vs. Entity Objects, Information Hiding

## Entity
  - has a unique identity
    - even if we have same data, if objects are distinct, they're different entities
  - has a lifespan/continuity; can change over time & over implementation
  - references (smart pointers?) or pointers

## Value
  - data immutable (faked in c++) eg. Java strings
    - c++ returns new object by value & over-write (or rather move) of contents rather than modify "this"
  - we don't care which one it is, given the data is identical

#### Q: You are implementing a video game version of a card game. Which classes are Entity-based, which are Value-based ADT's?

Class | Entity | Value  
------|--------|--------
Score |   | Y
Player| Y |        
Hand  | Y |        
Deck  | Y |
Card  | Y |

#### Q: How do we restrict certain constructors or methods of an object?
```cpp
class X {
  public:
    X(const X&) = delete;
    X&operator = (const X&) = delete;
}
```

### Mutable Objects

#### Q: How to make things immutable?
A:
  - remove all mutators
  - make data members private
  - ensure classes cannot be derived from (ie. "final") or make methods final
  - whenever we receive or return a reference/pointer, make a copy instead of modifying the original

Note: In C++, fake via deep copy + over-writing original object data via operator=

### PImpl Idiom
```c++
class Rational::Impl {
    int numerator_, denominator_;
  public: 
    Impl(int n, int d): numerator {n}, denominator {d} {}
    ...
};

Rational::Rational(int n, int d): rat_ {new Rational::Impl {n,d}} {
  if (d==0) throw "Panic! denominator = 0";
  reduce();
}
```

### rvalues
> Every C++ expression is either an lvalue or an rvalue. An lvalue refers to an object that persists beyond a single expression. You can think of an lvalue as an object that has a name. All variables, including nonmodifiable (const) variables, are lvalues. An rvalue is a temporary value that does not persist beyond the expression that uses it. 

### Why do we need destructors?
  - if an object requires resources
  - may want a destructor for other purposes eg. logging
  - virtual destructor to ensure inherited objects will implement one
  - `virtual ~MyClass() = defualt`
  
### Copy and Swap
Goal: provide a "safe" copy ie. if we run out of heap space, the original object is left unchanged.
  1) make deep copy of RHS in temporary local object (temp)
  2) swap info between LHS(this) and temp
  3) temp's destruction cleans up original data

# Modules
Q: Why do we want to be able to decompose our program into multiple source files?
A:
  1) Allows work to be done independently and in parallel
  2) allows recompilation of only what changed and then re-link
  3) makes it easier to reuse components
  4) allows code to evolve

**Module Declaraction**: 
  - tells the compiler of a name. eg. type or constant
  - if compiler has no declaration, compilation stops
  - can be repeated
  
**Module Definition**:
  - tells compiler amout of space to allocate
  - tells compiler what ADT methods exist & their signatures
  - there can only be 1 definition or else the compilation stops
  
Rule of thumb: perfer declarations (as in forward decl.) over definitions, where you can

**Global constants** declared, possibly in multiple header files but defined in one location.
  - ex. `extern const double PI;` can occur in multiple header files
  - ex. `const double PI = 3.14159;` defined in 1 .cc file

/*/* compiling with `g++-5 -E` shows the preprocessor output

**Q: when must you include?**
A: when compiler needs to know amount of space. eg. inheritance or inlined code
  - cant fix inheritance but can turn an object into a pointer/reference & move inlined code into implementation file

/*/* NEVER NEVER: put `using namespace std;` in your .h file

# Namespaces

  - can be defined globally or nested inside eath other (can't be placed inside functions or classes)
  - definition supercedes (hides) previous definition.
  - multiple namespace declarations are incremental ie. adds to previous def
  - it is considered a best practice to not re-open the namespace to implement/define; use the `::` scope operator
    - ie. `RadAdT::Rational::Rational(...)`
  - can't put definition in an unrelated namespace


Q: what is namespace pollution
A: clashes among global names in large, multi module systems with multiple developers
  - names must be unique
  - problem increases once libraryes are brought in since they define constants, types, templates, functions etc...
  - old solution: prefix all related info with a (hopefully unique) string
  - use namespace to create a local scope: use it to package related info eg. types classes, free routines, constants, etc.
    - if the namespace spans multiple files, need to include all files if you want all; otherwise we only see what is included since visibility is local to file. ie. `include <iostream>` for std::cout, but std::string will not be included.
    
 Q: Why use local namespaces?
 A:
  - prevents export of names
  - protects local names from clashes
  - visible in file without qualification for ease-of-use
  
```cpp
namespace X {
  int i, j, k;
}
int K;
void f() {
  int i = 0;
  using namespace X;
  i += 1; // local i, superceded
  j += 1; // X's j
  k += 1; // ambiguous
  ::k += 1; // global k
  x::k += 1; // X's k
}

void f2() {
  int i = 0;
  using X::i; // second def of i
  using X::j;
  using X::k;
  i += 1; // local
  j += 1; // x::j
  k += 1; // x::k
}

//header1.h
namespace A {
  int f(double);
}
//header2.h
namespace B {
  using A::f;
  void g() { f(1) };
}
//header3.h
namespace A {
  int f(int);
}
```
What gets used depends on order of includes!!!
  - 1,2,3 => f(double)
  - 2,1,3 => none because f is not included yet
  - 1,3,2 => both visible, pick the better match
  - 3,2,1 => f(int)
