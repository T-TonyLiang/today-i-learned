# CS 247: Introduction to Software Principles

## Abstract Data Types (ADTs)

### "Outside-In Design"
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
  
```
attribute; //data
attribute(); //accessor
attributeIs(...); //mutator
```
