# Java

### 番外篇：魔乐科技 第一行代码Java

* 最简单的Hello world程序结构，Java程序的编译执行方法
* 基本数据类型int, float, double, char, boolean, String
* 条件控制语句
* 函数（方法）的定义方法

```java
public static void func(int par1, int par2)
{
  ...;
  return;
}
```

* 对象的声明与实例化：对象的名字实际是一个指向对象的指针，指针保存在stack中；而对象本身则保存在另外的heap空间中。实际使用对象需要先在heap中开辟内存，这就是new关键字的作用。想象Book bk在一个stack中添加了一个指针bk，new Book\(\)则在堆空间中添加了一块Book类型的内存，bk = new Book\(\)就是把这两个东西关联起来。

```java
/* 假设有Book这样一个类 */
Book bk = null; // 这是声明了一个指向对象的指针
bk = new Book(); // new语句用来为对象开辟内存空间

Book bk = new Book(); // 指针与对象之间建立关联
```

* 数组也是一种引用型数据，因此也需要用new关键字开辟内存

```java
int[] data = null;
data = new int[100];

// 两种写法都可以
int[] num = new int[4];
int num[] = new int[4];

int num[] = new int[4]{1,2,3,4};
```

* 2维数组

```java
int[][] num = new int[4][4];
```

* 类的定义

```java
public class Book extends something
{
    private String title;
    private double price;
    
    // 构造方法，与类名同名，不需要返回值类型！
    public Book(String title, double price)
    {
        // 用this表示等式左边是对象的属性，而不是参数
        this.title = title;
        this.price = price;
    }
}
```

* 一个好应用：链表结构中的node。

这个例子中有一些值得注意的点。

首先，Node这个类不是public的，这意味的是这段代码必须和main函数在同一个文件内，如果是一个单独的Node.java文件的话，这里就需要写成public class Node了。

然后，Node里除了一个属性data以外，最特殊的就是有一个Node类的属性next，指向下一个节点。这是一个递归的定义。

```java
 class Node
 {
    private String data;
    private Node next;
    public Node(){}
    public Node(String data)
    {
        this.data = data;
    }
    public void setData(String data)
    {
        this.data = data;
    }
    public void setNext(Node next)
    {
        this.next = next;
    }
    public String getData()
    {
        return this.data;
    }
    public Node getNext()
    {
        return this.next;
    }

    public void addNode(String data)
    {
        if(this.next == null){
            Node next = new Node();
            this.next = next;
            next.setData(data);
        }
        else{
            this.next.addNode(data);
        }
    }
}

```

