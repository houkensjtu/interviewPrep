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
* 
