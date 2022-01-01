## TABLE OF CONTENTS
1. [BASICS](https://github.com/p-arrow/Red-Blue-Guide/blob/main/Coding/C++.md#basics)
2. [DATA TYPES I](https://github.com/p-arrow/Red-Blue-Guide/blob/main/Coding/C++.md#data-types-I)
3. [DATA TYPES II](https://github.com/p-arrow/Red-Blue-Guide/blob/main/Coding/C++.md#data-types-II)
4. [DATA CONTROL FLOW](https://github.com/p-arrow/Red-Blue-Guide/blob/main/Coding/C++.md#data-control-flow)
5. [COMMON FUNCTIONS](https://github.com/p-arrow/Red-Blue-Guide/blob/main/Coding/C++.md#common-functions)
6. [OBJECT ORIENTATION](https://github.com/p-arrow/Red-Blue-Guide/blob/main/Coding/C++.md#object-orientation)
7. [CODE EXAMPLES](https://github.com/p-arrow/Red-Blue-Guide/blob/main/Coding/C++.md#code-examples)

<br />

## BASICS

### Common Headers 
- A header file is a file with extension .h
- It contains C function declarations and macro definitions to be shared between several source files
- There are two types of header files: the files that the programmer writes and the files that comes with your compiler

```
#include <stdio.h> --> standard input/output
#include <iostream> --> input/output stream: cin, cout
#include <fstream> --> file stream (read in data)
#include <string> --> C++ String
#include <cstring> --> C String
#include <algorithm> --> functions like max/min/sort 
#include <iomanip> --> input/output manipulaton, e.g. setprecision)
#include <array> --> array functions
#include <vector> --> vector function
#include <file.cpp> --> import other file.cpp into main.cpp
#include <sstream> --> string stream
#include <list>
#include <set>
#include <utility> --> for data type "Pair"
#include <map>
#include <queue>
#include <stdexcept> --> for standard exceptions: try/catch
```

### Common Commands
- `sizeof()`: returns size of file in byte
- `system("pause")`: pause output terminal

### Common Keywords
- **auto**
- **const**
- **volatile**:
   - tells the compiler that the value of the variable may change at any time
   - without any action being taken by the code the compiler finds nearby

### Arithmetic Operators
- && : and
- || : or
- == :  equal
- ! : Negation (e.g. !a && !b)
- 5 % 2 = 1 (Modulo)

<br />

## ADVANCED

### Structure of Main
```
int main(int argc, char *argv[]) {  }

# If argc > 0, then argv[0] represents the program name
# If argc > 0, then argv[1] represents the program parameters
# char *argv[] (array of pointers) = char **argv (pointer to a pointer to a character)
```

### Why do we need Headers (.h)?
- With headers we avoid dependencies between .cpp files 
- Example:
   - a.cpp does not work without b.cpp and vice versa
   - Consequently neither a nor b get compiled correctly 
   - Solution:
   - a.cpp has access to b.h, b.cpp has access to a.h
   - a.h and b.h indicate which classes/functions/methods they use (but without coding content)
   - This resolves the dependencies, thus a.cpp and b.cpp get compiled correctly

### Stack vs Heap 
- C manages the stack automatically 
- Stack grows from top to bottom
- Not needed functions/variables get deleted after call 
- Stack has limited size 
- Example Array: `int a[3] = {1, 2, 3};`

<br />

- The coder manages the heap manually
- Heap grows from bottom to top
- Heap is bigger than stack (good for big and growing data sets)
- Example:
```
#Pointer in stack, but array in heap with Keyword "new"
#Array is only reserved, but not filled 
#Array must be closed manually, but only with keyword "new"!

int *a = new int[3]; 
delete [] a;
```

### C-String vs C++-String
- Back then, C had no comfortable data type "string"
- Instead C used char-Arrays
- Problem: 
   - No simple passing of char-array to functions
   - That's why they used pointers (referring to array-beginning and array-end)
   - Array-end with special character: `\0`
   - This made C vulnerable for string-exploits by implementing `\0` maliciously (DoS, Buffer Overflow etc.)
- With C++ the string functionality (as we know it today) was implemented (std::string)
- C++ String does not need `\0` 



### Pointer (C-Relict) vs References (C++)
- Both hand over data to functions (copy/original data possible) 
- Both represent an internal memory address 
```
void doSomething(int *a){} --> Pointer (*)
void doSomething(const vector<int> &a) {} --> Referenz (&)
```
- Difference:
   - Pointer only points to array-beginning (out-of-range memory access possible !)
   - Reference hands over complete object (more comfortable)
   - Conclusion: Use References whenever possible (less error prone) 

### Vector vs List 
- Vectors save elements in a row 
- Vectors can deal with single elements more efficiently 
- Lists don't save elements in a row but only connected to each other
- Lists are preferred when other data can be saved in between the list-data 
```
it < a.end()     // Vector style
it != a.end()    // List style, because "<" is less efficient (because elements are far from each other)
a.at()           // Vector style
a[]              // Vector style
```

### Pragma Once (Präprozessordirektive)
- Ensures that #include-calls only appear once in compiled object (after compilation) 
- Even if several .cpp files have same call (e.g. #include <iostream>)


<br />

## DATA TYPES I
- **unsigned int**: only positive numbers
- **signed int**: positive/negative numbers
- **integer**: 4 byte, whole number
- **long**: 4 byte
- **float**: 4 byte
- **double**: 8 byte, decimal
- **string**: " ", 24 byte
- **char**: ' ', 1 byte, single character 
- **struct** 
   - Small version of class (no inheritance, no public/private)
   - C relict
   - Useful when object has limited amount of properties
   - Useful if you temporarily want to bundle data inside a function

## DATA TYPES II

### Array (C-relict)
```
array.size()                  --> arraygröße anzeigen
array[i]                      --> show element i; without error warning if "out of range" memory access happens 
array.at()                    --> show element i; with error warning 
array<int, 3> = {1, 3, 5};    --> C++ convention
int a[3] = {1, 2, 3};         --> C convention
cout << a;                    --> Print first element of array a
cout << a + 1;                --> Print memory address of second element of array a
cout << a + 2;                --> Print memory address of third element of array a
cout << *(a + 2);             --> 3
```

```
# Pass array to function incl. array pointer and array size

int a[3] = {1, 2, 3};
void doSomething(int *a, int size){
    for(int i = 0; i < size; i++){
    cout << a[i] << endl;
    }
}
```

```
# Pass Array as reference
void doSomething(const array<int> &a){ }

# const: array "a" stays constant 
# "&": array "a" is passed as reference (= original data) 
# without "&": C++ pass array-copy to function (less efficient)
```
```
# Multi-dimensional Array
array<array<int, 2>, 3> a = {{ }}
```

#### Disadvantages of Arrays
- Arrays allow buffer overflow
- No memory border check (more efficient though, but security critical 
- Arrays have fixed size (no automatic adjustment like vectors)


### Vector (C++ Feature)
```
vector<int/string> names = { };        --> Vector resides in heap! Deletes itself after call 
vector.push_back()                     --> add element
vector.pop_back()                      --> remove element 
vector.front()                         --> choose first element
vector.back()                          --> choose last element 
vector.splice(vector.end(), b)         --> joint vector-end "a" with vector-beginning "b"
sort(vector.begin(), vector.end());    --> you need "#include <algorithm>" at top of file
```


### Pointer
```
int a = 123;
cout << a;   --> 123
cout << &a;  --> memory address like 0x2c3c64f6
cout << *&a; --> 123

# "*" = Pointer, which calls data from specific memory address 
```


### Iterator
- An iterator is an abstraction of a pointer 
   - Dereferencing possible 
   - Can be increased by 1 (points to next memory address; iterator can "jump" too)
   - Can be passed to function 
   - Can be used for high level functions like vectors or lists 
   - Can delete, sort and add data in/from vectors 

```
vector<int> a = {1, 2, 3, 4};
a.insert(a.begin() + 2, 123);                --> a = 1, 2, 123, 4
a.erase(a.begin() + 2);                      --> a = 1, 2, 4
a.erase(a.begin(), a.end() - 2);             --> a = 3, 4    (a.end() points AFTER last element)

# for loop with iterator must not contain "const" input parameter (!)
# counter inside for loop often "++it" instead of "it++" (more efficient)
int doSomething(vector<int> &vec){
    for (vector<int>::iterator it = vec.begin(); it != vec.end(); ++it){}
}
```

<br />

## DATA CONTROL FLOW
```
# Standard for loop
for (int i = 0; i < 20; i++){
   command;
};


# Loop through "names" but use dereferenced/original data &name (i/o making copy of "names" and process copied data)
for (string &name : names) {
   command;
};


# const = no change of &name
# auto = C++ identifies automatically the correct data type of "names"
for (const auto &name : names) {
   command;
};
```
```
while ( condition ) {
   command;
};

while (!cin.eof()){
   command;
};
```
```
if ( condition ) {
   command;
};
```

<br />

## COMMON FUNCTIONS

### Function GETS
- `gets()`: 
   - Reads characters from the standard input (stdin) and stores them as a C string into
   - Until a newline character or the end-of-file is reached 
   - It does not allow to specify a maximum size for str - which can lead to buffer overflows !
   - Better alternative: `fgets()`

```
#include <stdlib.h>
#include <unistd.h>
#include <stdio.h>

int main(int argc, char **argv)
{
  volatile int modified;
  char buffer[64];

  modified = 0;
  gets(buffer);                       <-- gets()

  if(modified != 0) {
      printf("you have changed the 'modified' variable\n");
  } else {
      printf("Try again?\n");
  }
}
```

### Function STRING
```
" "                                 --> means C-String 
string.length()                     --> C++ String functionality
string.size()                       --> C++ String functionality
strlen()                            --> C String functionality
string[4]
string.at(4)                        --> slower than [], but including error message if char does not exist 
string.substr(0, 4)                 --> access part of string 
string.find(" ")                    --> search char in string; output numbers if char does not exist
                                    --> same like "string::npos" (no position)
string.append(" ")
string.insert(4, ",")               --> insert "," at position 4 
string.erase(5, 3)                  --> remove 3 chars starting from location 5th 
string.count()
stringstream.str()                  --> Print saved strings from stringstream 
```

### Function ENUM
- Different states can be saved in one variable 
- C++ handles internally the state as numbers
```
# Example 1
enum Status {offline, online, away, busy};
Status status = Status::busy;
if (status == Status::busy){
cout << "Der Benutzer ist gerade beschäftigt." << endl;
cout << status << endl; --> 3
```
```
# Example 2
enum Status {offline, online, away, busy};
Status status = Status::busy;
switch (status) {
    case offline:
            cout << "Der Benutzer ist gerade offline." << endl;
            break;
    case online: 
    case away:
    case busy:
            cout << "Der Benutzer ist gerade online." << endl;
            break;
    default:
            cout << "Ich bin Default Case." << endl;
}
```


### Function PAIR
- Useful for small code snippets 
- Not useful when different functions are used at different places (then struct/class better)
```
pair<string, int> p("Hallo Welt", 42);
cout << p.first << endl;
cout << p.second << endl;
```

### Function MAP
- Like "dictionary" in Python
```
map<string, int> m = {"test", 123};
m.insert(pair<string, int>("test", 123);
m.size()                                     --> 1
m.at("test")                                 --> 123 (mit Fehlermeldung, falls Element nicht in m vorhanden)
m.["test"]                                   --> 123 (ohne Fehlmerldung, nur Null-Ausgabe)
```
```
# Standard call of for loop 
for (map<string, int>::iterator it = m.begin(); it != m.end(); ++it){
    cout << (*it).first << endl;             --> Dereferencing with "*"
    cout << it->second << endl;              --> Dereferencing with "->"

# Shorter for loop (possible form C++ Version 11 )
for (const auto &it : m)
{   cout << it.first << ":" << it.second << endl; }
```


### Function PRIORITY QUEUE
```
priority_queue<int> pq;
priority_queue<pair<int, string>> pq;
pq.push(123);
pq.push(321);
cout << pq.top()                             --> 321 (values automatically sorted in pq, thus biggest element is print out first 
pq.pop()                                     --> removes top-element 

pq.push(pair<int, string>(555, "Hallo"));
cout << pq.top().first << ":" << pq.top().second    --> 555 : Hallo
```


<br />

## OBJECT ORIENTATION

### Public / Private / Protected 
- **public**: Accessible from inside and outside of class 
- **private**: Accessible only from inside the class where the private instance was created 
   - private variables are normally written with underscore: `player1 --> player1_`
- **protected**: Accessible only from inside the class and classes that inherit from it


### Constructor
- The Constructor has normally the same name like the corresponding class 
```
class Animal {
pulic:
    Animal(double weight, int legs, string name) {
        this->weight = weight;
        this->legs = legs;
        this->name = name;
    }
};


# Alternative Constructor Definition (i/o this->name = name;)
class Animal {
pulic:
    int legs;
    string name;
    Animal(int legs, string name) : legs(legs), name(name) {}

# Create instance with parameters 
Animal Tiger(8, 4, "Ryo");

# Create instance without parameters 
Animal Tiger;
Tiger.weight = 8;
Tiger.legs = 4;
Tiger.name = "Ryo";
```

### Inheritance 
```
class Animal {
pulic:
    double weight;
    int legs;
};


# Cat inherit from Animal, but has additional "string name"
class Cat: public Animal {
public:
    string name;
};
```

### Parent Method 
- Requirement: Class2 inherits from Class1 
- If so: Methods are also inherited
```
string Class2::Method2(){
    result << Klasse1::Method1;
}
```

### What belongs into the Header? 
- Classes, Attributes, Methods: All except the body (!)
```
#pragma once
#include <vector>
#include <string>
#include <sstream>
#include "TicTacToeGame.h"
class TicTacToeField {
private:
    std::vector<std::vector<int>> field;
public:
    TicTacToeField();
    int calculateWinner();
    std::string getFieldStr(); 
};
```

### Difference between "this->property" and "c.property"
- `this->ps` = `(*this).ps`
- `this` is a pointer 
```
class Car {
public: 
    int ps;
    int getPS() {
        return this->ps;    // output: 123
        return (*this).ps;  // output: 123
}
Car a;
a.ps = 123;
```

### Deconstructor
- The Deconstructor is the opposite of the Constructor
- The Deconstructor gets marked with it "~"
- The Deconstructor terminates a class after the program has finished
```
class Car {
public:
    Car() {
        a = new int[10];
        cout << "Constructor";
    }
    ~Car(){
        delete [] a;
        cout << "Deconstructor";
    }
};
```

<br />

## EXAMPLES

### Interactive Input/Output
```
#include <iostream>
cin >> x;
cout << y;

# newline with "endl"
cout << "hello" << endl;

# read line by line
getline (cin, string x);
```

```
# WITHOUT "using namespace std"
std::cout << "hello world";

# WITH "using namespace std"
cout << "hello world";
```

```
# Escape Characters
"Hello\" \\World"

# Output: Hello" \World
```

### Interaction with file
```
# read from file 
ofstream file ("path/to/file"); 

# write to file
ifstream file ("path/to/file"); 

# if file is open then do ...
if(file.is_open()){} 

# close file
file.close()

# use file until you reach EOL
while(!file.eof()){}

# printf (relict from C); can provide more data type info than cout
printf("Hello World:  %.2f", age);
printf("Hello World:  %s", name); --> does not work because "name" is C++ string
printf("Hello World:  %s", name.c_str()); --> works because ".c_str()" implements C++ string functionality 
```
