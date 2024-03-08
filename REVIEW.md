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

```Cpp
#include <iostream>
#include <string>
using namespace std;

class Restaurant {
   public:
      Restaurant();
      void SetName(string restaurantName);
      void SetRating(int userRating);
      void Print();
   private:
      string name;
      int rating;
};

Restaurant::Restaurant() {  // Default constructor
   name = "NoName";         // Default name: NoName indicates name was not set
   rating = -1;             // Default rating: -1 indicates rating was not set
}

void Restaurant::SetName(string restaurantName) {
   name = restaurantName;
}

void Restaurant::SetRating(int userRating) {
   rating = userRating;
}

// Prints name and rating on one line
void Restaurant::Print() {
   cout << name << " -- " << rating << endl;
}

int main() {
   Restaurant favLunchPlace;  // Automatically calls the default constructor

   favLunchPlace.Print();

   favLunchPlace.SetName("Central Deli");
   favLunchPlace.SetRating(4);
   favLunchPlace.Print();

   return 0;
}
/*
NoName -- -1
Central Deli -- 4
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

```Cpp
#include <iostream>
#include <string>
using namespace std;

class Restaurant {
   public:
      void   SetName(string restaurantName); // Mutator
      void   SetRating(int userRating);      // Mutator
      string GetName() const;                // Accessor
      int    GetRating() const;              // Accessor
      void   Print() const;                  // Accessor

   private:
      string name;
      int rating;
};

void Restaurant::SetName(string restaurantName) {
   name = restaurantName;
}

void Restaurant::SetRating(int userRating) {
   rating = userRating;
}

string Restaurant::GetName() const {
   return name;
}

int Restaurant::GetRating() const {
   return rating;
}

void Restaurant::Print() const {
   cout << name << " -- " << rating << endl;
}

int main() {
   Restaurant myPlace;

   myPlace.SetName("Maria's Diner");
   myPlace.SetRating(5);

   cout << myPlace.GetName() << " is rated ";
   cout << myPlace.GetRating() << endl;

   return 0;
}
/*
Maria's Diner is rated 5
*/
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

# Pointer
## Pointer variables
A pointer is a variable that holds a memory address, rather than holding data like most variables. A pointer has a data type, and the data type determines what type of address is held in the pointer.
A pointer is declared by including "*" before the pointer's name:
```Cpp
int* pointer1;
void* pointer2;
char* pointer3;
// pointer is just a variable that holds a memory address
// types does not matter
```

### Reference
Reference needs to assign immediately.
The reference operator "&" obtains a variable's address:
```Cpp
int var;
void* ptr;
ptr = &var; // ptr holds memory address of var
```
```Cpp
#include <iostream>

using namespace std;

int main() {
   int someInt = 5;
   int* valPointer = nullptr;

   valPointer = &someInt;
   cout << valPointer << endl;
   cout << *valPointer << endl;

   return 0;
}
/*
0x16f46b288
5
*/
```

```Cpp
int a = 5;
int& ref = a;
ref = 2;
cout << a << endl; // 2
```
```Cpp
int a = 5;
int b = 8;
int* ref = &a; // ref holds memory address of a
*ref = 2; // ref changes the value of a to 2
ref = &b; // now ref holds memory address of b
*ref = 1; // ref changes the value of b to 1

cout << a << endl; // 2
cout << b << endl; // 2
```
```Cpp
void Increment(int* value)
{
  (*value)++;
}

int main()
{
  int a = 5;
  Increment(&a);
  cout << a << endl; // 6
}
```
or
```Cpp
void Increment(int& value)
{
  value++;
}

int main()
{
  int a = 5;
  Increment(a);
  cout << a << endl; // 6
}
```

### Dereferencing a pointer
```Cpp
int var = 8;
int* ptr = &var;
*ptr = 10; // we have access to change the value of var from 8 to 10
```

### Null pointer
When a pointer is declared, the pointer variable holds an unknown address until the pointer is initialized.
A programmer may wish to indicate that a pointer points to "nothing" by initializing a pointer to "null". "Null" means "nothing"
```Cpp
int* maxValPtr = nullptr; // makes maxValPtr null
```

### The new operator
It allocates memory for the given type and returns a pointer to the allocated memory. If the type is a class, the new operator calls the class's constructor after allocating memory for the class's member variables
```Cpp
class Point{
public:
  Point();
  double x;
  double y;
};

Point::Point()
{
cout << "in Point default constructor" << endl;
x = 0;
y = 0;
}

int main()
{
Point* sample = new Point;
cout << "Exiting main() << endl;
return 0;
}
```

### The member access operator
```Cpp
// display point1's Y member value with cout
// syntax with deferencing
cout << (*point1).Y; 
// syntax with member access operator
cout << point1->Y;

// call point2's Print() member function
// syntax with deferencing
(*point2).Print(); 
// syntax with member access operator
point2->Print();
```

### The delete operator
It deallocates ) or frees a block of memory that was allocated with the new operator.
After delete, the program should not attempt to dereference pointerVariable since pointerVariable points to a memory location that is no longer allocated for use by pointerVariable.

```Cpp
int main()
{
Point* point1 = new Point(73,19);
cout << "X = " << point1->X << endl;
cout << "Y= " << point2->Y << endl;

delete point1;

point1 -> Print(); // ERROR: cant use point1 after deletion
}
```

# Array
Arrays are used to store multiple values in a single variable, instead of declaring separate variables for each value.
To declare an array, define the variable type, specify the name of the array followed by square brackets and specify the number of elements it should store:
```Cpp
string cars[4] = { "Volvo", "BMW", "Ford", "Mazda" };
int myNum[3] = { 10, 20, 30 };
```
```Cpp
// To change the value of a specific element, refer to the index number:
string cars[4] = { "Volvo", "BMW", "Ford", "Mazda" };
cars[0] = "Opel";
cout << cars[0];
// Now outputs Opel instead of Volvo
```

# Vectors
```Cpp
 // vector<dataType> vectorName(numElements);
vector<int> gameScores(4); // declares a vector gameScores with 4 integer elements
```
```Cpp
vector<int> yearList(4);

yearList.at(0) = 1999;
yearList.at(1) = 2012;
yearList.at(2) = 2025;

currYear = yeaList.at(4); // this will cause an error because  yearList.at(4) does not exists
```
- A vector's elements are automatically initialized to 0 during the vector declaration.
- All of a vector's elements may be initialized to another single value.

```Cpp
vector<int> myVec(3, -1); // creates a vector named myVec with 3 elements, each with value -1
vector<int> carSales = {5, 7 ,11}; // creates a vector of 3 integers elements initialized with values 5, 7, and 11
```
- A common error is to forget the "#include <vector>" at the top of the file when using vector.

- Iterating through vectors using loops
```Cpp
for (int i = 0; i < myVector.size(); i++)
{
// loop body
}
```

## vector resize()
```Cpp
userVals.resize(numVals);
```

## vector push_back()
- append a new element to the end of an existing vector using a vector's push_back() function
```Cpp
vector<int> dailySales;

dailySales.push_back(521);
dailySales.push_back(440);
dailySales.push_back(317);
```






