# Udemy Algorithm

## Section 1: Introduction

* Use Google Chrome's snippet console as environment

## Section 2: Big-O notation

* Comparing two add up functions:

```javascript
function addUp1(n)
{
  let s = 0;
  for (let i = 0; i <= n; i++){
    s += i;
  }
  return s;
}

function addUp2(n){
  return (n + 1) * n / 2;
}
```

* Which one is faster? We can time the code by:

```javascript
let t1 = performance.now();
addUp1(1000000000);
let t2 = performance.now();
console.log(t2-t1)
```

* But the time is different on different machine, for longer calculation it might take very long time, and the time is not accurate
* **Rather than counting seconds, let's count the number of simple operations the computer has to perform**!
* But counting is hard, sometimes you don't know the exact number or miss something. But regardless of the exact number, the number of operations roughly grow proportionally as n.
* **Big-O : how the runtime grows as the input size grows**.
* Big-O simplifying tips:
* * Constant don't matter \( O\(5n\) =&gt; O\(n\) \)
  * Smaller terms don't matter \( O\(n+10\) =&gt; O\(n\), O\(n^2 + 5n + 8\) =&gt; O\(n^2\) \)
  * Common constant runtime operation : 
  * * arithmetic operation
    * variable assignment
    * accessing elements in an array

## Section 3: Analyze performance

* Arrays; when are arrays slow? =&gt; **Access is quick \(O\(1\)\), insertion and removal is slow\(O\(n\)\); search is O\(n\) \(if the array is unsorted\)**

```javascript
let names = ["michael", "Julia", "mark"];
```

* Big-O of common array operations

![](.gitbook/assets/js_array.png)

## Section 4: Problem solving approach

#### Step 1: Understand the problem 初步理解问题

* * Can you re-phrase the problem in your own words?
  * What's the input and output of the problem?
  * How can I label the important data related in this problem?
* Example : write a addition function.
* * Ask yourself: what's the input ? Integer? Floats? How large?

#### Step 2: Concrete example 通过例子来深入理解问题的要求

* Write a function that counts each characters in a word
* Start with simple solutions, explore more complex ones, invalid inputs, empty inputs....

```javascript
char_count("aaaa"); // What should this return?
{a:4} // <= A dict with keys and values

char_count("My phone number is 129391923"); // Should we count space and numb?

char_count(); // What should we return? An empty dict? Zero? A bool false?
```

#### Step 3: Break it down 写作战计划

* Explicitly write down the steps you need to take
* Start with a skeleton of your code: 假设通过上个环节的沟通，我们已经确定了不需要考虑大小写，需要count数字但是不考虑符号和空格，我们也确定了准备用dict来返回结果

```javascript
function char_count(str){
// Do something
// 1. Make an object

// 2. Loop over the string
//    - If the char is already in the object, add 1 to the value
//    - If the char is not in the object, create the key, and add 1
//    - If the char is space or sign, do nothing
// 3. Return the object
}
```

* **在实际写代码之前，这样罗列解决问题的计划非常重要。**这不仅给了你自己一个可以遵循的骨架，也让面试官看到你思维的过程。假设最后你只进行到一半没有完成，有这个骨架也会让面试官看到你整体的思路，比一片空白要好很多！

#### Step 4: Solve / Simplify

* Solve the problem if you can / or solve a simplified problem!
* 如果题目中有一部分是你觉得特别难的，可以先忽略这个部分，求解剩下的问题，等到剩下的问题都解决以后，回过来再看是不是能把这个难题解决；避免被难关卡住而完全写不出一个字
* 比如说在上面的例子，你不知道如何转换大小写，不知道如何处理符号，那就先不考虑这些，先写一个单纯的loop

```javascript
// 先忽略大小写和符号的问题，仅仅计算每个字符的出现次数
function charCount(str){
  let result = {};
  for (let i = 0; i < str.length; i++){
    let char = str[i];
    if(result[char] > 0){
      result[char]++;
    }
    else{
      result[char] = 1;
    }
  }
  return result;
}
```

#### Step 5: Look back / refactor

* 检查你的代码，代码结果正确吗？可以提高性能吗？编写风格一致吗？有其他解法吗？

```javascript
// 用正则表达式检查char是不是字母或者字符
if (/[a-z0-9]/.test(char)){ ... }

// for loop不够 Javascript，可以改成更为简洁的形式
for (let char of str){
...
}
```

**再次强调理解问题很重要，必须要和面试官沟通好确认对问题的理解，并且用一些concrete example来确认理解**

### Section 5 : Problem solving pattern

面试中有存在一些常见的问题形式，这一节就具体来探索这些常见pattern的解法

#### Frequency Counter

* 
