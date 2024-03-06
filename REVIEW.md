# CLASS AND OBJECT
## class
- class: A program entity that represents a template for a new type of object
- object: entity that combines state and behavior
- object - oriented programming (OOP): programs that perform their behavior as interactions between objects
- abstraction: seperation between concepts and details. Objects provide abstraction in programming.

## elements of a class
- member variables: state inside each object
also called "instance variables" or "fields".
declared as "private".
each object created has a copy of each field.

- member functions: behavior that excutes inside each object
also called "methods".
each object created has a copy of each method.
the method can interact with the data inside that object.

- constructor: initializes new objects as they are created
set the initial state of each new object.
often accepts parameters for the initial state of the fields.

## interface vs. code
- interface: declarations of functions, classes, members, etc. -> .h: a "header" file containing only interface.
- implementation: definitions of how the above are implemented. -> .cpp: a "source" file containing definitions.

- The content of .h files is "#included" inside .cpp files
  makes them aware of declarations of code implemented elsewhere
  at compilation, all definitions are linked together into an executable.

## Structure of a header file
```Cpp
#ifndef CLASSNAME_H
#define CLASSNAME_H

class declaration;

#endif;
```
the "#ifndef" and "endif" are protection in case multiple .cpp files include this .h, so that its contnts wont get declared twice.

## A class declaration
```Cpp
class ClassName
{
public:
  ClassName(parameters); // constructor

  returnType name(parameters; // member function
  returnType name(parameters; // member function
  returnType name(parameters; // member functions
private:
  type name; // member variables
  type name; // data inside each object
};
```

## Using objects
```Cpp
BankAccount bal1;
ba1.name = "Marty";
ba2.balance = 1.25;
```

## Member func. bodies
In .cpp file, we write bodies (definitions) for the member functions that were declared in the .h file:
```Cpp
#include "ClassName.h"

returnType ClassName::methodName(parameters)
{
  statements;
}
```

- Member functions/constructors can refer to the object's fields.

## Initializing obejcts
It's bad to take 3 lines to create a BankAccount and initialize it
It's better if: BankAccount ba("Marty", 1.25); 

## Constructors
```Cpp
ClassName::ClassName(parameters)
{
  statements to initialize the objects;
}
```
- Constructor: initializes state of new objects as they are created.
  runs when the client declares a new object
  no return type is specified; it implicitly "returns" the new object being created
  if a class has no constructor, c++ gives it a default constructor with no parameters that does nothing.

```Cpp
BankAccount::BankAccount(string n, double b)
{
  name = n;
  balance = b;
}

/*
Client program:
BankAccount b1("han", 1.25);
BankAccount b2("quyen", 9999);
*/
```

## Private data
```Cpp
private:
  type name;
```
encapsulation: hiding implementation details of an object from its clients
- an encapsulation provides abstraction.

seperates external view (behavior) from internal view (state) - encapsulation protects the integrity of an object's data.

A class's data members should be declared private
- No code outside the class can access or change it.

## Accessor functions
```Cpp
double BankAccount::getBalance()
{
  return balance;
}

void BankAccount::setName(string newName)
{
  name = newName;
}
```

client code will look like this:
```Cpp
cout << ba.getName() << " : $" << ba.getBalance() << endl;
ba.setName("Cynthia");
```

### Encapsulation benefit
- provide abstraction between an object and its clients
- protect an object from unwanted access by clients
- allow you to change the class implementation
- allow you to constrain objects' state

