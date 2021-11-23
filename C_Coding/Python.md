## Table of Content
1) BEST PRACTICES
2) [BASICS](https://github.com/p-arrow/Red-Blue-Guide/blob/main/C_Coding/Python.md#basics)
3) [DATA STRUCTURES](https://github.com/p-arrow/Red-Blue-Guide/blob/main/C_Coding/Python.md#data-structures)
4) [CONTROL FLOW](https://github.com/p-arrow/Red-Blue-Guide/blob/main/C_Coding/Python.md#control-flow)
5) [FUNCTIONS](https://github.com/p-arrow/Red-Blue-Guide/blob/main/C_Coding/Python.md#functions)
6) SCRIPTING
7) EXAMPLES

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
