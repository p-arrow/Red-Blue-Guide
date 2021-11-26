## TABLE OF CONTENT
1. [BASICS](https://github.com/p-arrow/Red-Blue-Guide/blob/main/C_Coding/C++.md#basics)
2. [DATA TYPES](https://github.com/p-arrow/Red-Blue-Guide/blob/main/C_Coding/C++.md#data-types)
3. [DATA CONTROL FLOW](https://github.com/p-arrow/Red-Blue-Guide/blob/main/C_Coding/C++.md#data-control-flow)
4. [COMMON FUNCTIONS](https://github.com/p-arrow/Red-Blue-Guide/blob/main/C_Coding/C++.md#common-functions)
5. [OBJECT ORIENTATION](https://github.com/p-arrow/Red-Blue-Guide/blob/main/C_Coding/C++.md#object-orientation)
6. [EXAMPLES](https://github.com/p-arrow/Red-Blue-Guide/blob/main/C_Coding/C++.md#examples)

<br />

## BASICS

### Common Headers 
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

### Arithmetic Operators
- && : and
- || : or
- == :  equal
- ! : Negation (e.g. !a && !b)
- 5 % 2 = 1 (Modulo)

<br />

## DATA TYPES
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


<br />

## DATA CONTROL FLOW
```
for (int i = 0; i < 20; i++){}

# Loop through "names" but use dereferenced/original data &name (i/o making copy of "names" and process copied data)
for (string &name : names) { }

# const = no change of &name
# auto = C++ identifies automatically the correct data type of "names"
for (const auto &name : names) { }

while () {}

while (!cin.eof()){}

if () {}
```

<br />

## COMMON FUNCTIONS

<br />

## OBJECT ORIENTATION

### Public / Private / Protected 
public: Von überall aus zugreifbar (innerhalb/außerhalb der Klasse)
private: Nur innerhalb der Klasse, in der private erstellt wurde, zugreifbar
protected: Nur innerhalb der Klasse und Klassen, die daraus erben, zugreifbar
--> private Variablen werden per Konvention mit _ geschrieben
--> player1 --> player1_

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
