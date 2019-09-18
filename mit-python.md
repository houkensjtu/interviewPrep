---
description: Introduction to Computer Science and Programming Using Python
---

# MIT 6.001x

### Week 1 Python Basics

#### Python Install

Use Anaconda, Spyder as environment.

#### Overview

* Think computationally, not only teach Python language.
* Topics : data structure, iteration and recursion, abstraction, modularize, algorithms
* **Declarative knowledge** : matter of fact; **Imperative knowledge** : a recipe, algorithm
* **Example : square root of a number is defined as y such that y\*y = x; this is declarative.**
* **But how to find the root? Newton method, this is imperative knowledge.**

#### Basic machine architecture

* Memory &lt;=&gt; \( Arithmetic Logic Unit + Control Unit \) &lt;=&gt; Input, Output
* Basic primitives : **Turing showed that you can compute anything using 6 primitives.**
*  We want to **abstract methods to create new primitives**

#### Creating recipes / Aspects of language

* Language syntax : like grammar in natural language.
* Static semantics : 是否有意义
* **Syntactic error, Static semantic error** \(Example, type check, does type match each other?\), **Meaning error** : does not do what you want
* Our goal : **Learn the syntax and semantics of Python, build useful recipes and models**

#### Types

* Every object in a program has a **type**
* Primitive in Python: int, float, bool, NoneType; **can use type\(\) to see the type of an object**

```python
type(5) # => int
type(3.0) # => float

# Casting
float(5) # => 5.0
int(3.0) # => 3
```

#### Variables

* binding values and variables is the first level **abstraction.**

```python
pi = 3.1415
radius = 2.2
area = pi * (radius ** 2)
```

* This abstraction makes reuse of value easier.

#### Operators and branching

* &gt;,&lt;,==,!=, returns True or False.
* Logic combination : and, or, not.

```python
x = int(input("Enter a number.")
if x%2==0 :
    print("Even.")
else:
    print("Odd.")
```

* These programs **run in constant time,** because each expression run at max 1 time.

#### Strings

* int, float, bool, string &lt;- NEW

```python
hi = "Hello there."
name = "Brian"

# Concanation
hi + name
# Repeat
name * 3
# Length
len(name)
# Indexing
name[0]
# Slicing
name[0:2]
```

#### I/O

* print function can take multiple expressions, 但是自动会给加空格

```python
print("my fav", " num", "is", number)
print("my fav" + " num" + "is", number)
```

* 你也可以用加号string，这样就不会有自动空格
* input function

```python
text = input("Please enter something") # <= this is a string
num = int(text)
```

#### Control flow

* while loop, for loop

```python
n = 0
while n<5:
  print(n)
  n = n + 1
# or
for n in range(5):
  print(n)
```

#### Class of algorithms

* Guess and check: exhaustive enumeration

### Week 2 Simple programs

* String is immutable, but can be reassigned

```python
s = 'Hello'
s[0] = 'S' # => Error
s = 'World'# => This is ok.
```

* Loop over String

```python
s = 'abcdef'
for char in s:
    if char == 'i' or char == 'u':
        print("There is an i or u")
```

* Approximate solution method : find the square root of any non negative number

```python
cube = 27
epsilon = 0.0001
increment = 0.0001
result = 0

while abs(result ** 3 - cube) >= epsilon and result <= cube:
    result += increment
if abs(result ** 3 - cube) <= epsilon:
    print("The cubic root of", cube, " is ", result)
else: 
    print("Failed to find the root.")
```

* A more effective method : bisection search. We know the root of x lies between 1 and x, from Math.
* if guess \*\*2 &gt; x, we know guess is too big; else, is too small.

```python
x = 18
epsilon = 0.0001
upper = x
lower = 1
guess = (upper + lower) / 2
while abs(guess ** 2 - x > epsilon):
    if guess**2>x:
        upper = guess
    else: 
        lower = guess
    guess = (upper + lower) / 2
print("The square root of x is ", guess)
```

* Float number : In computer, numbers are represented in binary form.
* A even better algorithm : Newton-Raphson method to find the root

### Week 3 Tuples and lists

* Tuples are **immutable**. Used to return more than one value!

```python
t = ()  # <= An empty tuple
t = (2,) # <= 只有一个元素的时候，要加逗号！如果不加逗号，t就变成了一个单元素，而不是tuple
t = (2,4,"one")
t[1] = 5 #=> Error!
def quotient_and_remainder(x,y):
    q = x//y
    r = x%y
    return (q,r)
```

* iterate over tuples

```python
for t in a_Tuple:
    ...
```

* An exercise : Write a procedure called `oddTuples`, which takes a tuple as input, and returns a new tuple as output, where every other element of the input tuple is copied, starting with the first one. So if test is the tuple `('I', 'am', 'a', 'test', 'tuple')`, then evaluating `oddTuples` on this input would return the tuple `('I', 'a', 'tuple')`.Code Editor1 

```python
def oddTuples(aTup):
    # a placeholder to gather our response
    rTup = ()
    index = 0

    # Idea: Iterate over the elements in aTup, counting by 2
    #  (every other element) and adding that element to 
    #  the result
    while index < len(aTup):
        rTup += (aTup[index],)
        index += 2

    return rTup

def oddTuples2(aTup):
    return aTup[::2]

```

* List is a lot like tuples, but lists are **mutable.**

```python
# A traditional way to iterate over list
total = 0
for i in range(len(list)):
    total += list[i)
return total

# A cleaner way
total = 0
for i in list:
    total += i
return total
```

* List operations: L.append\(element\), del\(L\[index\]\), L.pop, L.remove \(element\)
* split method on a string return a string
* sorted\(L\), L.sort\(\) &lt;- mutate the list, L.reverse\(\); **L.sort\(\)会修改原来的list，L.sorted\(\)则只是返回一个排序好的list，原来的list不变**
* Mutation, aliasing, cloning : **list可以有不同的别名，其实就是指针，指向同一个内存同一个list内容**

```python
# 这就是把A和B都指向了同一个list，修改其中之一，另外一个也被修改
listA = listB

# 这是拷贝了一个list，此时两个list不再互相关联
listA = listB[:]

# 这里不论是拷贝，还是别名，都会返回True
listA == listB

# 这里只有别名才会返回True，如果是拷贝返回False
listA is listB
```

* **Function as object** : have types, can be element of data structures like lists, can appear in exp

```python
def applyFunction(L, f):
    for i in range(len(L)):
        L[i] = f(L[i])
```

* **Python map : 注意map返回的是一个iterable, 而不是一个list; map也可以接受两个参数**

```python
map(abs, [1,2,3,-4.-6])
for e in map(abs, [1,2,3,-4,-6]):
    print(e)
map(min, listA, listB) # 这里返回的是两个list的最小值
```

#### Sequences common operations

* Common operations : strings, tuples, ranges, lists
* **seq\[i\] , len\(seq\), seq1+seq2, seq\[start:end\], e in seq, e not in seq, for e in seq**

#### Dictionaries

* store pairs of data, key and value

```python
mydict = {}
grades = {'Ana':'B', 'John':'A','Katy':'A'}

>>> grades['Ana'] # => 'A'
>>> grades['Sylvia'] = 'A+' # Added an entry
>>> 'John' in grades # => True
>>> grades.keys() # => Return a List of keys
>>> grades.values()
```

* **Key can be any immutable type \(int, float, string, tuple, bool\)**
* Values can be any type \(mutable or immutable\)
* Application of a dictionary:

```python
def lyrics_to_frequency(lyrics):
    mydict = {}
    for word in lyrics:
        if word in mydict:  # <= 这里也可以写mydict.keys()
            mydict[word] += 1
        else:
            mydict[word] = 1
    return mydict
    
def most_common(frequency_dict):
    values = frequency_dict.values()
    best = max(values)  # <= 这里也可以用一个循环体来找出最大，但是max这个方法更为简洁，易读
    
    words = []
    for k in frequency_dict:  # <= 和上面一样，dict的循环默认是循环key，也可以明写.keys()
        if frequency_dict[k] == best:
            words.append(frequency_dict[k])
    return (words, best)
```

* 一个用dict来存储计算过程中结果的dynamic programming例子\(fibonacci number\)

