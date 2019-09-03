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



