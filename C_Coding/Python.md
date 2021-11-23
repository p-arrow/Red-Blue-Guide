## Table of Content
1) [BEST PRACTICES](https://github.com/p-arrow/Red-Blue-Guide/blob/main/C_Coding/Python.md#best-practices)
2) [BASICS](https://github.com/p-arrow/Red-Blue-Guide/blob/main/C_Coding/Python.md#basics)
3) [DATA STRUCTURES](https://github.com/p-arrow/Red-Blue-Guide/blob/main/C_Coding/Python.md#data-structures)
4) [CONTROL FLOW](https://github.com/p-arrow/Red-Blue-Guide/blob/main/C_Coding/Python.md#control-flow)
5) [FUNCTIONS](https://github.com/p-arrow/Red-Blue-Guide/blob/main/C_Coding/Python.md#functions)
6) [SCRIPTING](https://github.com/p-arrow/Red-Blue-Guide/blob/main/C_Coding/Python.md#scripting)
7) [EXAMPLES](https://github.com/p-arrow/Red-Blue-Guide/blob/main/C_Coding/Python.md#examples)

<br />

## Best Practices

#### READABILITY IS IMPORTANT
```
# Good Examples

print((1 + 2 + 4)/13)
print(4/2 + 7*7)
```

#### BAD EXAMPLES OF BOOLEAN EXPRESSIONS 
- Don't use True or False as conditions, e.g. `if True`
- Be careful writing expressions that use logical operators
- Don't compare a boolean variable with `== True` or `== False`, e.g. `if is_cold == True`


#### ITERABLES VS. ITERATOR VS. GENERATOR
- **iterables** are objects that can return one of their elements at a time (e.g. list)
- **iterator** is an object that represents a stream of data
- **Generators** are a simple way to create iterators using functions


#### BUILT-IN OBJECTS THAT ARE CONSIDERED "FALSE" 
- Constants defined to be false: `None, False`
- Zero of any numeric type: `0, 0.0, 0j, Decimal(0), Fraction(0, 1)`
- Empty sequences and collections: `'"", (), [], {}, set(), range(0)`


#### DOCSTRING
```
def square_root(n):
"""
    Calculate the square root of a number.

    Args:
        n(int): the number to get the square root of.
    Returns:
        the square root of n.
    Raises:
        TypeError: if n is not a number.
        ValueError: if n is negative.
"""
```

#### AVOID EXECUTABLE RUNNING WHEN IT'S IMPORTED
- `if __name__ == "__main__":`
   - Ensure that variables that are created, functions that are called, operations that are done
   - ONLY executed when you directly run the file**, not when you import it into another
   - Example: modules like random, string, math etc.

#### FAVORITE MODULES
- **csv**: very convenient for reading and writing csv files
- **collections**: useful extensions of usual data types incl. OrderedDict, defaultdict, namedtuple
- **random**: generates pseudo-random numbers, shuffles sequences randomly and chooses random items
- **string**: more functions on string e.g. string.digits 
- **re**: pattern-matching in strings via regular expressions
- **math**: some standard mathematical functions
- **os**: interacting with operating systems
- **os.path**: submodule of os for manipulating path names
- **sys**: work directly with the Python interpreter
- **json**: good for reading and writing json files (good for web work)

#### IMPORT TECHNIQUES
```
1) from "module_name" import "object_name"
2) from "module_name" import "first_object", "second_object"
3) import "module_name" as "new_name" 
4) from "module_name" import "object_name" as "new_name" 
5) import "module_name.submodule_name"
6) from . import "object_name" as "new_name"
```

#### THIRD PARTY LIBRARIES
- Big projects often depend on dozens of third party packages
- Dependencies are summarized in requirements.txt:
   - beautifulsoup4==4.5.1
   - bs4==0.0.1
   - pytz==2016.7
   - requests==2.11.1
- `pip install -r requirements.txt`: Get all needed packages indicated in requirements.txt


#### USEFUL THIRD PARTY LIBRARIES 
- **Python/Jupyter**: A better interactive Python interpreter
- **Requests**: Provides easy to use methods to make web requests. Useful for accessing web APIs.
- **Flask**: A lightweight framework for making web applications and APIs.
- **Django**: A more featureful framework for making web applications. Django is particularly good for designing complex, content heavy, web applications.
- **Beautiful Soup**: Used to parse HTML and extract information from it (web scraping)
- **pytest**: extends Python's builtin assertions and unittest module.
- **PyYAML**: For reading and writing YAML files.
- **NumPy**: The fundamental package for scientific computing with Python. It contains among other things a powerful N-dimensional array object and useful linear algebra capabilities.
- **pandas**: A library containing high-performance, data structures and data analysis tools
- **matplotlib**: a 2D plotting library which produces publication quality figures
- **ggplot**: Another 2D plotting library, based on R's ggplot2 library.
- **Pillow**: The Python Imaging Library adds image processing capabilities to your interpreter.
- **pyglet**: A cross-platform application framework intended for game development.
- **Pygame**: A set of Python modules designed for writing games.
- **pytz**: World Timezone Definitions for Python

<br />

## Basics

#### ARITHMETIC OPERATORS
```
 + Addition
 - Subtraction
 * Multiplication
 / Division
 % Mod (the remainder after dividing)
** Exponentiation ("^" does not do this operation)
// Divides and rounds down to the nearest integer
== equal to
!= not equal to
\n new line
print(" ",end=" ") --> without newline
```

#### OPERATION MEANING
```
< 	strictly less than
<= 	less than or equal
> 	strictly greater than
>= 	greater than or equal
== 	equal
!= 	not equal
is 	object identity
is not 	negated object identity
<<	Binary Left Shift operator (Exp: x = 1010<<1 = 10100 = 20 (2^4 + 2^2)
>>	Binary Right Shift operator (Exp: x = 1010>>1 = 101 = 5 (2^2 + 2^0)
```

#### ASSIGNMENT OPERATORS
```
x+=2 --> x=x+2
x-=2 --> x=x-2
x*=2 --> x=x*2
x,y,z = 1,2,3 (simultaneous assignment)
```

#### RESERVED WORDS
```
false   class    finally  is       return
none    continue for      lambda   try
true    def      from     nonlocal while
and     del      global   not      with
as      elif     if       or       yield
assert  else     import   pass
break   except   in       raise
-----
and 	assert 	break 	class 	continue
def 	del 	elif 	else 	except
exec 	finally 	for 	from 	global
if 	import 	in 	is 	lambda
not 	or 	pass 	print 	raise
return 	try 	while 	
```

#### INTEGER VS. FLOAT
- Integer: 4, 10100
- Float: 4.0, 5.383647, 0.5, .1

#### IN / NOT IN
- **return bool value (false, true)**

```
Namen = ['kai', 'roy','bernd']
print('klaus' in Namen) 

#output: false
```

#### IS / NOT IS
- **identity operator**
- "is" evaluates if both sides have the same identity
- "is not" evaluates if both sides have different identities


#### == VS. IS (Equality vs Identity)
```
a = [1, 2, 3]
b = a
c = [1, 2, 3]

print(a == b) --> True
print(a is b) --> True
print(a == c) --> True
print(a is c) --> False

# List a and list b are equal and identical
# List c is equal to a (and b for that matter) since they have the same contents
# But a and c (and b for that matter, again) point to two different objects, i.e., they aren't identical objects.
```

#### EVERYTHING IS A OBJECT
```
a = 12.5
a.__add__(5)    --> 17.5
a.__sub__(7)    --> 5.5
s = "Hallo Welt"
s.__len__()     --> 10
```

<br />

## Data Structures

#### STRING METHODS
```
a = "meinefiesefresseausderschnauze"
    a.islower() --> True (all letters are small)
    a.count('z') --> 1
    a.find('z') --> 28
    a.capitalize() --> Meinefiesefresseausderschnauze
    a.upper()
    a.lower()
    a.startswith("m") --> True
    a.endswith("?") --> False
    a.index('z') --> 28 (Like find() but raise ValueError when substring is not found)
    a.strip("f")
    a.replace("m","D")
    len(a) --> 30
```

- Reverse String
   - `string_rev = string[::-1]`:  string[start,stop,step]
- Split/Strip
```
# Open file "filename", extract values (letter and flower) and add it to dictionary flowerdict

def create_flowerdict(filename):
   flower_dict = {}
   with open(filename) as f:
       for line in f:
           letter = line.split(": ")[0].lower() 
           flower = line.split(": ")[1].strip()
           flower_dict[letter] = flower
   return flower_dict
```

#### LISTS
- mutable sequence
- ordered sequence (zero index basing)
- `[ ]` or list()
- `List = [1.3,"hallo","3"]`
- Slicing: return certain range of data (will be a list too)
    - `list = [1,2,3,4]`
    - `print(list[1:3])`: [2,3] *lower value included, upper value excluded!
    - `print(list[-2:])`: [3,4] *slicing works also reversely
    - `print("Hallo Welt"[-4:])`: "Welt"


#### LIST METHODS
- `max(list)`: returns greatest element
- `min(list)`: returns smallest element
- `sorted(list, reverse=true)`: 
    - returns sorted list
    - leaves original list unchanged (!)
- `liste.sort(key="fkt.", reverse=true)`
    - changes original list (!)
- join method:
    - `new_str = "-".join(["fore", "aft"])`: fore-aft
- append method:
    - `letters = ['a','b','c']`
    - `letters.append('z') --> ['a','b','c','z']`
- format method: 
    - `maria_string = "Maria loves {} and {}"`
    - `print(maria_string.format("math","statistics"))`: Maria loves math and statistics
- `del list[3]`: Delete the 4th element of list


#### TUPLES
- immutable: you can't add, remove, sort items
- ordered sequence (zero index basing)
- ( ) or tuple()
```
tuple_a = 1,2    # parentheses can be omit
tuple_b = (1,2)

t = 1,2,3
x,y,z = t     # x=1, y=2, z=3  --> "tuple unpacking"   

# Put Tuples in lists
students = [("Max",23),("Kai",20)]
for name,age in students:
    print(name)
    print(age)
```

#### SETS
- mutable sequence 
- unordered (i.e. there is no last element, no index)
- set have only unique elements (no item twice!, quickly remove duplicates)
- { } or set()
```   
numbers = [1, 2, 6, 3, 1, 1, 6]
unique_nums = set(numbers)
print(unique_nums)   # (1, 2, 3, 6)
unique_nums.add(5)   # the "append" method is called "add" for sets
unique_nums.pop()    # remove last element
```

#### QUEUE/PRIORITYQUEUE
- Create queue filled with "value" and "priority"
- `pq.get()` returns values in ascending order 
- Use "priority" with "-" (Minus) for descending order 
```
import queue
pq = queue.PriorityQueue()
for name, number in names.items():
    pq.put((-number, name))              # hand over as tupel due to (( )) 
for i in range(0, 50):
    print(pq.get())
```

#### DICTIONARY 
- mutable data type that stores mappings of unique keys to values
- unordered: cannot be sorted
- Dictionary keys must be immutable (!)
   - Example: string, int, float 
- { } or dict()
```
elements = {"hydrogen": 1, "helium": 2, "carbon": 6}    # hydrogen = key, 1 = value
print(elements["helium"])                               # 2 
elements["lithium"] = 3                                 # add "lithium" with value 3 into dictionary
del elements["lithium"]                                 # delete the element lithium 
elements["helium"][0]                                   # refer to 0-index value of helium
print("carbon" in elements)                             # check existing key; "False"
print(elements.get("dilithium"))                        # None (i/o error message)
print(elements["dilithium"])                            # KeyError
elements.get("kryptonite", 'There\'s no such element!') # defined return value
```

```
# return both key and value
for key, value in elements.items():
     print("Key: {}    Value: {}".format(key, value))
```
-   `print(elements.keys())`
-   `print(elements.values())`
-   `sorted_keys = sorted(elements.keys())`
```
# use for-loop and dictionary to count entries in string "book_title"

word_counter = {}
for word in book_title:
    word_counter[word] = word_counter.get(word, 0) + 1  # if word_counter.get does not find "word" in book_title then return 0 (new entry). Otherwise +1 (increase counter)
```

#### COMPOUND STRUCTURES
- include containers in other containers, e.g. dictionary in a dictionary
```
elements = {"hydrogen": {"number": 1,
                         "weight": 1.00794,
                         "symbol": "H"},
hydrogen_weight = elements["hydrogen"]["weight"]   #1.00794
oxygen = {"number":8,"weight":15.999,"symbol":"O"}  #create oxygen 
elements["oxygen"] = oxygen  #add oxygen to dictionary
```

<br />

## Control Flow

#### IF/ELIF/ELSE
```
if "condition1" and "condition2":
   "code"
elif "condition":
   "code"
else:
   "code"
```

#### FOR LOOP
```
for i in range(3):
  print("Hello!")
  
# print output in one line (w/o newline)
for c in passw:
    print(chr(c), end="")
```

#### WHILE LOOP
- "break" terminates a loop
- "continue" skips one iteration of a Loop
```
card_deck = [4, 11, 8, 5, 13, 2, 8, 10]
hand = []
while sum(hand)  < 17:
    hand.append(card_deck.pop())
```

#### LIST COMPREHENSION
```
capitalized_cities = [city.title() for city in cities]
squares = [x**2 for x in range(9) if x % 2 == 0]
squares = [x**2 if x % 2 == 0 else x + 3 for x in range(9)]
```
<br />

## Functions
- Function names follow the same naming conventions as variables!
- We can add default arguments in a function to have default parameters
- Given parameters will overwrite default parameters
- If a variable is created inside a function, it can only be used within that function!
- **Examples**

```
def cylinder_volume(height, radius=5):
   pi = 3.14159
   return height * pi * radius ** 2

egg_count = 0
  def buy_eggs():
    egg_count += 12  --> Error: changing the global variable "egg_count"
  buy_eggs()  --> Error 
```


#### BUILT-IN FUNCTION: range
- range(start=0, stop, step=1)
    a) range(4) returns 0, 1, 2, 3  #stop
    b) range(2, 6) returns 2, 3, 4, 5   #start, stop
    c) range(1, 10, 2) returns 1, 3, 5, 7, 9    #start,stop,step
- names = ["Joey Tribbiani", "Monica Geller", "Chandler Bing", "Phoebe Buffay"]
  usernames = []
  for index in range(len(names)):
    usernames.append(names[index].lower().replace(' ','_')
  print(usernames)
- items = ['first string', 'second string']
  html_str = "<ul>\n"  
  for index in range(len(items)):
    html_str += '<li>'+items[index]+'</li>\n'
  html_str += '</ul>'


#### BUILT-IN FUNCTION: zip (Matrix transponieren)
- letters = ['a', 'b', 'c']
  nums = [1, 2, 3]
  for letter, num in zip(letters, nums):
    print("{}: {}".format(letter, num))
  --> [('a', 1), ('b', 2), ('c', 3)]

- unzip (via asterisk): 
  some_list = [('a', 1), ('b', 2), ('c', 3)]
  letters, nums = zip(*some_list)
- Transpose a 4x3 matrix to 3x4 matrix
  data = ((0, 1, 2), (3, 4, 5), (6, 7, 8), (9, 10, 11))
  data_transpose = tuple(zip(*data))


#### BUILT-IN FUNCTION: enumerate
- letters = ['a', 'b', 'c', 'd', 'e']
  for i, letter in enumerate(letters):
    print(i, letter)
    -->
    0 a
    1 b
    2 c
    3 d
    4 e
- for i, letter in enumerate(letters,2):
    print(i, letter)
    2 a
    3 b
    4 c
    5 d
    6 e
- for i, letter in enumerate(letters):
    letters[i] += ' ' + str(99)

#### LAMBDA FUNCTION
- creates quickly anonymous functions (w/o function name)
- not ideal for complex functions
- def multiply(x, y):
    return x * y
--> can be reduced to: multiply = lambda x, y: x * y

#### GENERATOR FUNCTION
- return keyword: yield
- "yield" keyword is difference between generator and typical function
def my_range(x):
    i = 0
    while i < x:
     yield i
     i += 1
- Why Generators i/o lists?
    *Generators are a lazy way to build iterables
    *They are useful when fully realized list would not fit in memory
    *Or when the cost to calculate each list element is high 
    !But generators can only be iterated over once

#### GENERATOR EXPRESSION
    *combines generators and list comprehensions
    *Only idfference is you use square brackets (i/o parentheses)
    sq_list = [x**2 for x in range(10)]      --> list of squares
    sq_iterator = (x**2 for x in range(10))  --> iterator of squares

#### BUILT-IN FUNCTION: map
- takes function and iterable as inputs
- returns an iterator that applies the function to each element of the iterable
- Calculate average number in each row:
  numbers = [
              [34, 63, 88, 71, 29],
              [90, 78, 51, 27, 45],
              [63, 37, 85, 46, 22],
              [51, 22, 34, 11, 18]
           ]
  def mean(num_list):
    return sum(num_list) / len(num_list)
  averages = list(map(mean, numbers))
- Same as Lambda function:
  averages = list(map(lambda nl: sum(nl)/len(nl), numbers))
  print(averages)


#### BUILT-IN FUNCTION: filter
- takes a function and iterable as inputs
- returns an iterator with iterable-elements where function returns "True"
- cities = ["New York City", "Los Angeles", "Chicago", "Mountain View", "Denver", "Boston"]
  def is_short(name):
    return len(name) < 10
  short_cities = list(filter(is_short, cities))
  print(short_cities)
  
#### BUILT-IN FUNCTION: input
- utilize raw input from user
- you can use optional string argument to specify a message
  name = input("Enter your name: ")
  print("Hello there, {}!".format(name.title()))
  num = int(input("Enter an integer"))


#### BUILT-IN FUNCTION: eval
- interpret user input as a Python expression
- this function evaluates a string as a line of Python
  result = eval(input("Enter an expression: "))
  print(result)
  Bsp: Enter an expression: 67*45 --> output:3015

<br />

## Scripting

#### ERRORS
- Syntax errors:
    *occur when Python can’t interpret our code,
    *These are errors you’re likely to get when you make a typo, or starting to learn Python
- Exceptions:
    *occur when unexpected things happen during execution of a program (even syntactically correct)     
    *Different types of built-in exceptions available 
    a)ValueError:
        *An object of the correct type but inappropriate value 
    b)AssertionError:
        *An assert statement fails
    c)IndexError:
        *A sequence subscript is out of range
    d)KeyError:
        *A key can't be found in a dictionary
    e)TypeError:
        *An object of an unsupported type is passed as input to an operation or function.
    f)ZeroDivisionError
    g)FileNotFoundError

##EIGENE EXCEPTION AUFRUFEN
#Die Klasse Exception mit eigenem "InvalidEmailError" ergänzen dank Vererbung "(Exception)"
class InvalidEmailError(Exception):
    pass

#Beispielfkt. mit individueller raise-Meldung
def send_mail(email, subject, content):
    if not "@" in email:
        raise InvalidEmailError("email does not contain an @")
try:     
    send_mail("hallo", "Betreff", "Inhalt")
except InvalidEmailError:
    print("Bitte gebe eine gültige E-Mail ein")


#### TRY STATEMENT
- use try statements to handle exceptions
- four clauses can be used:
a)try:
This is the only mandatory clause in a try statement
The code in this block is the first thing that Python runs in a try statement
b)except:
Switch to "except statement" when an exception occurs while running try block
c)else:
If Python runs into no exceptions while running the try block
Then it will run the else block 
d)finally:
Before Python leaves try block, it will run the code in finally block under any condition, even if it's ending the program if Python runs into error while running except or else block, this finally block will still be executed before stopping the program
```
# Example
while True: 
   try:
    x = int(input('Enter a number:  '))
      break
   except ValueError: 
      print('That\'s not a valid number!')
   except KeyboardInterrupt:
      print('\n No input taken')
      break 
   finally:
      print('\n Attempted Input\n')

# while-Schleife lohnt sich nur bei Input-Aufforderung mit "try"
# ansonsten Dauerausführung von "except" möglich
```

#### ACCESSING ERROR MESSAGE
```
try:
 #some code
except ZeroDivisionError as y:
 #some code
print("ZeroDivisionError occurred: {}".format(y))

# Output: "ZeroDivisionError occurred: integer division or modulo by zero"
#If you don't have specific error, you can still access the message like this:

try:
 #some code
except Exception as y:
 #some code
print("Exception occurred: {}".format(y))
```

#### READING FILES
```
f = open('my_path/my_file.txt', 'r')
  file_data = f.read()
  f.close()
with open('my_path/my_file.txt', 'r', encoding='utf8') as f:
    file_data = f.read()
with open("camelot.txt") as f:
    camelot_lines = []
    for line in f:
        camelot_lines.append(line.strip())
```

#### WRITING FILES
- Overwrite existing content with `'w'` (!)
- Adding content is done in append mode `'a'` (!) 
```
f = open('my_path/my_file.txt', 'w')
  f.write("Hello there!")
  f.close()
```


#### YOUR OWN PROJECT
```
# create project file xyz
# create virtual environment
python -m venv [source/repos/projects/xyz]

# choose corresponding Interpreter in VS Code
xyz/scripts/python.exe

# install needed packages
.projects/xyz pip install [package]

# create requirements.txt
pip freeze > requirements.txt

# Finally, install all the dependencies listed in this file
pip install -r requirements.txt
```

#### DECLARE ENCODING
- At top of file.py:
- `#!/usr/bin/env python`
- `# -*- coding: utf-8 -*-`

<br />

## Examples

#### GRAPHICS WITH MATPLOT
```
import matplotlib.pyplot as plt
xs = [1, 2, 5]
ys = [4, 7, 5]
plt.plot(xs, ys)
plt.show()
```

#### OBJECT ORIENTATION AND INHERITANCE
#Klasse FileReader besitzt einen Kosntruktor und eine Funktion
class FileReader():
    #Der Konstruktor legt nur ein Attribut "filename" fest
    def __init__(self, filename):
        self.filename = filename
    
    def lines(self):
        lines = []
        with open(self.filename, "r") as file:
            for line in file:
                lines.append(line.strip())
        return lines
#Die Klasse CsvReader erbt von der "Mutter" FileReader
class CsvReader(FileReader):
    #Der Konstrukor legt kein eigenes Attibut fest sondern erbt via "super()" das Attribut
    def __init__(self, filename):
        super().__init__(filename)
    #Auch die Funktion "lines" wird von FileReader geerbt
    def lines(self):
        lines = super().lines()


#### WEB CRAWLER
```
import requests
from bs4 import BeautifulSoup
from urllib.parse import urljoin
import time
import csv
class CrawledArticle():
    def __init__(self, title, emoji, content, image):
        self.title = title
        self.emoji = emoji
        self.content = content
        self.image = image
class ArticleFetcher():
    def fetch(self):
        url = "http://python.beispiel.programmierenlernen.io/index.php"
        while url != "":
            time.sleep(1)        //Verzögere Ausführung um 1s
            r = requests.get(url)
            doc = BeautifulSoup(r.text, "html.parser")
            
            for card in doc.select(".card"):
                emoji = card.select_one(".emoji").text
                content = card.select_one(".card-text").text
                title = card.select(".card-title span")[1].text
                image = urljoin(url, card.select_one("img").attrs["src"])

                #Erstelle Generator mit allen gecrawlten Attributen
                yield CrawledArticle(title, emoji, content, image)
               
            #Falls es "next button" gibt dann ändere url und gehe zur nächsten Seite
            next_button = doc.select_one(".navigation .btn")
            if next_button:
                next_href = next_button.attrs["href"]
                next_href = urljoin(url, next_href)            
                url = next_href
            else:
                url = ""
        return articles

#Öffne leere Datei zum beschreiben 
with open('datei.csv', 'w', newline='') as csvfile:
    articlewriter = csv.writer(csvfile, delimiter=';', quotechar='"')
    #Schreibe die gecrawlten Daten via writerow-Methode in articlewriter, Zeile für Zeile
    for article in ArticleFetcher().fetch():
        articlewriter.writerow([article.emoji, article.title, article.image, article.content])
```



#### CALL MODULE FROM OTHER PROJECT FILES
```
# Option A 
# No extra configuration necessary
from "project_file" import "file"`


# Option B
from "project_file" import *
file.f()
# additionally you have to write "__all__ = ["file"]" under "__init__"

# Option C
import "project_file"
project_file.file.f()
# Additionally you have to write: "from . import datei" under "__init__" 
```

#### TRANSFER VARIABLE FUNCTION PARAMETER
```
# mithilfe von * werden Parameter in einer Tupel übergeben
def calculate_max(*params):
    print(params)
    current_max = params[0]
    for item in params:
        if item > current_max:
            current_max = item
    return current_max
calculate_max(1, 2, 3)

#mithilfe von ** werden Parameter in einem Dictionary übergeben
def f(**args):
    print(args)
f(key="value", key2="Value 2")

#Beispiel mit matplot, wo plot-parameter variabel übergeben werden
import matplotlib.pyplot as plt
def create_plot(**plot_params):
    print(plot_params)   
    plt.plot([1, 2, 3], [5, 6, 5], **plot_params)
    plt.show()
create_plot(color="r", linewidth=10, linestyle="dashed")
```


#### DATE AND TIME 
```
import datetime
now = datetime.now()
print(now)
print(now.strftime("%d.%m.%Y"))  # 18.07.2017
print(now.strftime("%Y-%m-%d"))  # 2017-07-18
print(now.strftime("%Y%m%d"))    # 20170718

# extract data from string 
d = "18.07.2017"
print(datetime.strptime(d, "%d.%m.%Y"))
```


#### DEFAULTDICT MODULE
```
# Dictionary get initialized automatically with values 
p = defaultdict(int)
words = ["Hello", "Hello", "World"]
for word in words:
    p[word] = p[word] + 1        //p[word] startet mit 0
```


#### REGEXP
```
import re
sentence = "I have 30 dogs, and all consume 4 liter water and 2 kg food respectively."
re.findall("[0-9]+", sentence)
#output: ['30', '4', '2']

re.search("[0-9]+", sentence)
#output: <_sre.SRE_Match object; span=(9, 11), match='30'>
```


#### CSV MODULE
```
import csv    
with open('../data/names.csv', newline='') as csvfile:
    namereader = csv.reader(csvfile, delimiter=',', quotechar='"')
```


#### PROXY SERVER 
```
from http.server import HTTPServer, BaseHTTPRequestHandler
from socketserver import ThreadingMixIn
import urllib
import requests
import random

class MyRequestHandler(BaseHTTPRequestHandler):
    def do_POST(self):
        print(self.path)           #Vom Browser gesendeter Path
        print(self.headers)        #Vom Browser gesendeter Header
        if self.headers["content-type"] == "application/x-www-form-urlencoded":
            length = int(self.headers["content-length"])      #Hole Eingabevariable aus Header
            form = str(self.rfile.read(length), "utf-8")      #Lese Eingabevariable
            data = urllib.parse.parse_qs(form)                #Zerlege Eingabevariable 
        
            #Leite Daten an Server weiter
            with requests.post(self.path, data = data, stream=True) as res:      
                #ResponseCode an Browser, sonst kann Browser nicht richtig interpretieren
                self.send_response(res.status_code)     
                for key,value in res.headers.items():
                    self.send_header(key, value)        #Headerinfo an Browser übergeben
                self.end_headers()                      #Proxy Header beenden
                self.wfile.write(res.raw.read())        #Übergebe von res.raw an Browser

    def do_GET(self):
        #Bildmanipulation ausführen
        if self.path[-4:] == ".jpg":
            images = ["./cats/1.jpg", "./cats/2.jpg"]
            self.send_response(200)                         
            self.send_header("Content-Type", "image/jpg")   
            self.end_headers()                              
            with open(random.choice(images), "rb") as file:     #"rb" = read binary
                self.wfile.write(file.read())                   #wfile erwartet byte-input 
        else: 
            with requests.get(self.path, stream=True) as r: 
                self.send_response(r.status_code) 
                #Textmanipulation ausführen
                if "text/html" in r.headers["content-type"]:
                    self.send_header("Content-Type", "text/html")   
                    self.end_headers()
                    content = str(r.content, "utf-8")
                    content = content.replace("Bilder", "Wazzup?")
                    content = content.replace("Lorem", "FUCK YOU!")
                    self.wfile.write(content.encode())
                else:
                    #Keine Manipulation, sondern normale Datenübermittlung
                    self.send_response(r.status_code)
                    for key,value in r.headers.items():
                        self.send_header(key, value)
                    self.end_headers()
                    self.wfile.write(r.raw.read())        

#Sequentiell arbeitenden HTTPServer mittels Vererbung mit Threadingfunktionalität ausstatten
class ThreadingHTTPServer(ThreadingMixIn, HTTPServer):
    pass

address = ("127.0.0.1", 10080)                            #Proxy eine IP und Port zuweisen
server = ThreadingHTTPServer(address, MyRequestHandler)   #Serverinstanz erstellen
server.serve_forever()                                    #Server laufen lassen
```


#### XOR OPERATION
```
# chr() = convert int to Unicode letter
# ord() = convert Unicode letter to int
# ^ = Bitwise Exclusive XOR

def xor(str1, str2):
  result = []
  for i, j in zip(str1, str2):
    result.append(chr(ord(i) ^ ord(j))
  return ''.join(result)
```

#### HTTP SERVER
- py2: `python -m SimpleHTTPServer`
- py3: `python -m http.server`
