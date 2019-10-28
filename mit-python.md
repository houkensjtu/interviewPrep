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

### Week 4 Good programming practices

#### Testing code

* Testing, debugging: expectation vs. reality
* Check the program -&gt; **testing**; keep lid closed -&gt; **defensive programming**; cleaning the kitchen -&gt; **debugging**
* Defensive programming -&gt; Write specifications + modularize + check input / output
* Testing : compare output with expected output
* Guidelines:
* * Break programs into modules that can be tested easily
  * Document constraints and assumptions of your code
* Steps:
* * First, make sure the code runs
  * Have a set of expected results with a set of inputs
* Class of tests:
* * **unit testing** : validate each piece of the program  &lt;= Make sure you do this before next step! don't rush!
  * **integration testing** : overall program work
* Blackbox testing : without looking at the implementation, compare program results with expectations

```python
def sqrt(x, eps):
""" Assume x, eps floats, x>=0, eps>0
    Returns res such that x-eps<=res*res<=x+eps. """
```

* Glassbox testing : use the code and test each path of the code, branches, for loops, while loops...

#### Debug tips

* Bugs : isolate the bug, eradicate the bug, retest
* Type of bugs : 
* * overt bug : cause code to crash or infinite loop
  * covert bug: runs normally, but return wrong value
  * persistent bug : occurs every time
  * intermittent : only occurs occasionally 
* Debugging : steep learning curve, use print function, use bisection method, test your function before finishing the whole program
* Remember to **backup your code before you modify**

#### Exceptions

* SyntaxError, IndexError, TypeError, NameError, TypeError...
* What to do when encounter an error? **Stop execution, signal error condition :=&gt; raise exception**

```python
try:
    a = int(input("Tell me one number:"))
    b = int(input("Tell me another number:")
    print(a/b)
except:
    print("Bug in user input.")
print("Finished.")
```

* 在上面的例子中，**try-except语句的存在可以捕获任何的意外，并且在意外发生时，执行except中的语句，使得错误仍然在控制之下**，而不会让程序自动崩溃失控
* 拓展上面的例子，我们可以对可能产生的意外做更精细的控制

```python
try:
    a = int(input("Tell me one number:"))
    b = int(input("Tell me another number:")
    print(a/b)
except ValueError:
    print("Bug in user input.")
except ZeroDivisionError:
    print("")
except:
    print("")
print("Finished.")
```

* Example exception usage:

```python
while True:
    try:
        n = input("Please enter an integer:")
        n = int(n)
        break
    except ValueError:
        print("Input is not an integer")
print("Finished.")
```

```python
data = []
file_name = input("Provide a name of file of data")

try:
    fh = open(file_name, 'r')
except IOError:
    print("Cannot open", file_name)
else:
    for new in fh:
        if new != '\n':
            addIt = new[:-1].split(',')
            data.append(addIt)
finally:
    fh.close()
```

* **Exception可以经常用在处理一些大量的数据，或者用户的输入，这些处理在设计时就预先知道，可能会有各种各样的缺陷或者意外，**所以可以在程序中预先用try来给予处理
* Exception as control flow: we can **raise an exception** when unable to produce a result consistent with function's spec.

```python
raise ValueError("Something is wrong.")
```

```python
def get_ratios(L1, L2):
    ratio = []
    for index in len(L1):
        ratio.append(L1[index] / L2[index])
    except ZeroDivisionError:
        ratio.append( float('NaN') )
    except:
        raise ValueError ("Bad input value")
    return ratio

```

* Assertion: 断言比例外更进一步: 在所有你断言是真的情况之外，都会抛出AssertionError。一个通常的应用就是用来检查函数的输入和输出，是否符合编写时的意图

```python
def avg(grades):
    assert not len(grades) == 0, 'no grades data'
    return sum(grades)/len(grades)
```

### Week 5 Object oriented programming

#### OOP programming

* Everything is an object. Each object has **a type, an internal data representation, and a set of procedures.**
* Objects are a data abstraction that capture:
* * internal data representation through data attributes
  * interfaces for interacting with objects
* Some objects types built in to Python: list, tuple, dict
* **\[1,2,3,4\] is of type list. How are lists represented internally? -&gt; Linked list of cells.**
* **Internal representation should be private.**

#### A concrete example

* Define a class.

```python
class Coordinate(object):
    def __init(self, x, y):
        self.x = x
        self.y = y
    def distance(self, other):
        x_diff = self.x - other.x
        y_diff = self.y - other.y
        return (x_diff**2 + y_diff**2)**0.5
        
c = Coordinate(3,4)
origin = Coordinate(0,0)
```

* **\_\_init\_\_\(\)** is a special method. self refer to an instance of the class. self is automatically passed to the method. self不管是在什么method的定义中，永远都是第一个参数
* print representation of an object: **the \_\_str\_\_ method**.

```python
def __str__(self):
    return '(' + self.x +',' + self.y + ')'
```

* 接下来给出了一个分数的例子，这个例子我已经比较熟悉了

```python
class Fraction:
    def __init__(self, numer, denom):
        self.numer = numer
        self.denom = denom
    def __str__(self):
        return str(self.number) + '/' + str(self.denom)
    def getNumer(self):
        return self.number
    def getDenom(self):
        return self.denom
    def __add__(self, other):
        ...
```

* 第二个例子是一个integer set，特殊的地方在于要确保set中没有重复的数字。同时，提供insert和remove方法作为interface。在insert的时候，要**确保到data structure invariant，也就是不能有重复**

```python
class integerSet:
    def __init__(self):
        self.val = []
    def insert(self, e):
        if not e in self.val:
            val.append(e)
    def remove(self, e):
        try:
            self.val.remove(e)
        except:
            raise ValueError(str(e) + "not found")
```

#### Why OOP?

* Bundle together objects that **share common attributes**. Build **abstractions to make distinction between implementation and usage**.
* Create our own class of objects on top of Python's basic classes
* Python并没有强制保护class内部数据，你**不能设置数据为private**，但是更好的做法是不要直接访问类内部数据，而是用getter和setter方法来修改，**保持内部数据和外部接口的分离**

**Inheritance**

* 继承类的写法，覆盖父类的方法。不同的子类可以有不同的父类方法，

#### Class variables

* 类可以有自己的变量，定义在\_\_init\_\_方法的外面。所有的instance将共享这个variable，就类似于Java中的static变量

```python
class Rabbit(Animal):
    tag = 1  # <= class variable
    def __init__(self, age, parent1 = None, parent2 = None):
        Animal.__init__(self,age)
        self.parent1 = parent1
        self.parent2 = parent2
        self.rid = Rabbit.tag  # <= Access the class variable
        Rabbit.tag += 1
        
```

#### Building a class : an extended example

* Build the Person class:

```python
class Person(object):
    def __init__(self):
        self.name = name
        self.birthday = None
        self.lastName = name.split(' ')[-1]
    def getLastname(self):
        return self.lastName
    def __str__(self):
        return self.name
```

* 继续扩展这个类，建立MITPerson，Undergraduate student和Graduate student类。

### Week 6 Algorithmic complexity

#### Program efficiency

* How do we decide which program is most efficient : time and space efficiency
* How to ? Measure the time, count the operations, abstract notion of order of growth

```python
import time

t0 = time.clock()
do some thing
t1 = time.clock - t0
print(t1)

# Time measurement depends on the machine!
```

* Why not count the operations? -&gt; Don't need to be precise

```python
def search(L,e):
    for i in L:
        if i == e:
            return True
    return False
```

* 上面这个例子，如果第一次就找到e，那就是一个best case，相反如果找了整个list，那就是worst case。worst case时这个算法需要o\(n\)的时间。
* 典型的order：constant, linear, quadratic, logarithmic, nlogn, exponential ...

#### Big-O notation

* Big O measures **the upper bound on the asymptotic growth**
* **Big O is used to describe worst case**

```python
def factorial(x):
    result = 1
    while x > 0:
        result *= x
        x -= 1
    return result
```

* 上面这个例子中，如果数operation的话，结果是1+5n+1。去掉常数和整数系数的话，这个算法就是O\(n\)。同样的，在求Big-O的时候，通常忽略阶数比较低的项而只留下最高次数项

#### Complexity classes

* Constant runtime : O\(1\): not so interesting
* Logarithmic O\(logn\) : binary search

#### Analyzing complexity

* Polynomial complexity : nested loops

```python
def isSubset(L1, L2):
    for e1 in L1:
        matched = False
        for e2 in L2:
            if e1 == e2:
                matched = True
                break
        if not matched:
                return Flase
    return True
```

#### Recursion complexity

```python
def fib(n):
    if n == 0:
        return 0
    elif n == 1:
        return 1
    else:
        return fib(n-1) + fib(n-2)
```

* Fibnacci数的递归算法，如果不做加工是O\(2^n\)的exponential复杂度，因为每进一层，呼叫都是前面的两倍

## Week7 Search and sorting algorithms

#### Search algorithms

* Brute force : linear search. vs. Binary search : the list must be sorted.

```python
// 一个稍稍改良的线性搜索
def linear_search(L,e):
    for i in L:
        if e == i:
            return True
        elif i > e: // <- 这里利用了list已经排序的特性
            return False
    return False // <- 但是最终的big-O还是线性的
```

```python
// 自己写的二分查找 :P
def binary_search(L,e):
    lo = 0
    hi = len(L)
    while mid > lo:
        mid = (lo + hi) / 2
        if L[mid] == e:
            return True
        elif L[mid] > e:
            hi = mid
        else:
            lo = mid
    return False
```

akkasdfiej

a

sdf\[e







adsfasdfs

