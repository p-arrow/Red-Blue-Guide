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
