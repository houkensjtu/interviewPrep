# Frequency counter

#### 问题描述

* 写一个function, 接收两个数组或者字符串，比较其中各个元素是否匹配且出现次数是否相同
* Naive solution：一个一个遍历第一个组，每次取一个元素，再到第二个组中遍历，查找是否存在这个元素。
* Better solution：建立两个frequency counter（Javascript中的Object，或者Python中的dict），分别统计两个组中的元素出现次数，然后遍历一次counter，看key-value是否一致

#### 编程技巧

Javascript篇

```javascript
let frequencyCounter = {} // 建立object

// Naive的数组遍历
for(let i = 0; i < arr.length; i++){
  arr[i] = ...
}

// 更好的数组遍历
// of用于取出iterable的每个元素，比如数组和字符串
for(let ele of arr){
  ele = ...
}

// in用于取出object的key，或者是数组的下标index
for(let i in arr){
  arr1[i] = ... // 这里i将等于1，2，3，4...
}

arr1.indexOf('xxx') // 返回某个元素的index

// 如果某个元素存在则加1，否则将其定义为1
frequencyCounter[k] = (frequencyCounter[k] || 1) + 1
```

