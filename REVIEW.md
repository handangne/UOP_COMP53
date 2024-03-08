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

# Streams and Operator Overload
## Streams
cin and cout are basic instream and outstream predefined in iostream library
"<<" known as insertion operator, sends daa to outstream
">>" known as extraction operator, receives data from instream

## String Streams
sstream library includes istringstream and ostringstream
- istringstream allows you to use one long string to be used as an in stream

```Cpp
#include <iostream>
#include <sstream>
#include <string>

using namespace std;

int main()
{
string userInfo = "Amy Smith 19"; //  input string
istringstream inSS(userInfo); // input string stream
string firstName;
string lastName;
int userAge;

// Parse name and age values from input string
inSS >> firstName;
inSS >> lastName;
inSS >> userAge;
```

- ostringstream allows you to compile multiple data points into one string
```Cpp
#include <iostream>
#include <sstream>
#include <string>

using namespace std;

int main()
{
ostringstream infoOSS; // output string stream
string infoStr; // information string
string firstName; 
string lastName;
int userAge;

// prompt user for input
cout << "Enter \"firstname lastname age\": " << endl;
cin >> firstName;
cin >> lastName;
cin >> userAge;

// write user input to string stream
infoOSS << lastName << ", " << firstName;
infoOSS << " " << userAge;

// appends (minor) to string stream if less than 21
if (userAge < 21)
{
infoOSS << " (minor)";
}

// extract string stream buffer as a single string
infoStr = infoOSS.str();

cout << "Information: " << infoStr << endl;

return 0;
}
```

## File input
- input file stream declared as ifstream variable
- open file with .open() function
- will need to ensure file opened properly before extracting data
- ".isopen()" will return true uf file opened properly

```Cpp
int main()
{
ifstream inFS; // input file stream
int fileNum;

// open file
cout << "opening file myfile.txt" << endl;
inFS.open("myfile.txt");

if (!inFS.is_open())
{
cout << "could not open file myfile.txt." << endl;
return 1;
}
```

## File output
- output file stream declared as ofstream variable
- still opens with ".open()" function
- still need to ensure file opens properly before trying to write data

```Cpp
#include <iostream>
#include <fstream>

int main()
{
ofstream outFS; // output file stream

// open file
outFS.open("myfile.txt");

if (!outFS.is_open())
{
cout << "could not open file myoutfile.txt" << endl;
return 1;
}
```

## Operator overloading
C++ allows you to overload, or redefine, the behavior of many common operators in the language:
- unary: + - ++ -- * ! - new delete &
- binary: + - * / % += -= *= /= %= | || ^ == != < > <= >= = [] -> () , &&

Overuse of operator overloading can lead to confusing code.
- rule of thumb: do not abuse this feature. do not define an overloaded operator unless its meaning and behavior are completely obvious.

## Operator overload syntax
- declare your opeator in a ".h" file, implement it in a ".cpp" file
```Cpp
returnType operator op(parameters); // .h
returnType operator op(parameters); // .cpp
```

- where op is some operator like +, ==, <<, etc.
- the parameters are the operands next to the operator;
  for example, a+b becomes operator +(Foo a, Foo b)
- overloaded operators can also be declared inside a class.

### operator overload example
``` Cpp
// BankAccount.h
class BankAccount {
  bool operator == (BankAccount& ba1, BankAccount& ba2);
  bool operator != (BankAccount& ba1, BankAccount& ba2);
};

// BankAccount.cpp
bool operator == (BankAccount& ba1, BankAccount& ba2)
{
return (ba1.getName() == ba2.getName() && ba1.getBalance() == ba2.getBalance());
}
bool operator != (BankAccount& ba1, BankAccount& ba2)
{
return !(ba1 == ba2); // calls operator ==
}
```

### overload example
```Cpp
// BankAccount.h
class BankAccount
{
...
ostream& operator << (ostream& out, BankAccount& ba);
};

// BankAccount.cpp
ostream& operator << (ostream& out, BankAccount& ba)
{
out << ba.getName() << ": $" << setprecision(2) << ba.getBalance();
return out;
}


# Inheritance
When one class inherits from another class it automatically includes everything the parent class has
- Variables
- Functions
- Other inheritances

```Cpp
class Number
{
public:
  Number() = default;
  Number(Number const&) = default;
  virtual ~Number() = default;
  virtual bool isImaginaryNumber() const noexcept = 0;
  virtual bool isRealNumber() const noexcept = 0;
};

class ImaginaryNumber : public Number
{
public:
  ImaginaryNumber() : m_realComponent(0.0), m_imagComponent(0.0) {}
  ImaginaryNumber(ImaginaryNumber const& arg) : m_realComponent(arg.m_realComponent), m_imagComponent(arg.m_imagComponent) {}

  virtual ~ImaginaryNumber() = default;
  virtual bool isImaginaryNumber() const noexcept { return true; }
  virtual bool isRealNumber() const noexcept { return false; }
private:
  long double m_realComponent;
  long double m_imagComponent;
};

struct MenuOption { std::string title; };

// Menu is a vector of MenuOption: options can be inserted, removed, reordered,...
// and has a title

class Menu : public std::vector<MenuOption>
{
public:
  std::string title;

  void print const
  {
    std::cout << title << ":\n";
    for (std::size_t i = 0, s = size(); i < s; ++i)
      std::cout << "  " << (i + 1) << ". " << at(i).title << '\n';
  }
};

enum class Color { WHITE, RED, BLUE, GREEN };

void apply_terminal_corlor(Color) ( /* OS-specific */ }

// THIS IS BAD!
// ColorMenu is a Menu where every option has a custom color
class ColorMenu : public Menu
{
public:
  std::vector<Color> colors;
  void print() const
  {
    std:: cout << title << ":\n";
  }
}
```
- Inherited classes can overload functions defined in parent class
- They can also call the parent's version of the overload function
```Cpp
void childClass::print()
{
  parentClass::print();
  // whatever additional commands you want
}
```

