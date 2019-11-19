# 学堂在线C++ 初级

## 第一章 绪论

#### 计算机系统简介

* CPU &lt;-&gt; 内存 &lt;-&gt; 外存储，IO 的简单理解;程序都是从硬盘载入到内存里运行
* 计算机只能认识机器语言，机器语言指令是由2进制来编码的; 计算机所有能识别的机器指令的集合，叫做**计算机的指令系统，**指令系统是计算机硬件和软件的交流接口
* 软件是由程序和说明文档构成，要重视编写文档

#### 计算机程序设计方法的发展

* 最早的程序员直接写机器语言，也就是0和1
* 汇编语言，虽然并没有提高抽象程度，但是由于有助记符号，所以比机器语言容易阅读
* 高级语言，引入了类似英语的关键字，类似数学等式的语法结构，抽象层次更高
* 面向对象的高级语言\(c++\)，对象有属性，有行为能力

#### 面向对象的基本概念

* 类&lt;-抽象出同一类对象的共同属性和行为; 类-&gt;实例化成为对象，相当于模具
* 封装性的好处：隐蔽内部细节，对外只用接口交流，使用方便，安全性好
* 继承的好处：软件复用，改造扩展更加容易
* 多态的作用：同样的行为作用在不同的对象上，需要不同的方法; 同样叫“打”球，打篮球，打乒乓球的方法是不同的

#### 程序开发流程

* 源代码 -&gt; 编译器 -&gt; 目标文件
* 解释器 \(Java, Python\)，不翻译成目标文件，每次执行每次翻译
* 算法与数据结构设计 -&gt; 源代码编辑 -&gt; 编译 -&gt; 链接（程序库）-&gt; 测试 -&gt; 调试

#### 计算机中的信息与存储单位

* 计算机的基本功能：算数运算，逻辑运算
* 计算机中的信息：控制信息（这门课不讨论），数据信息（写程序需要关注的）
* 最小的存储单位bit，8bit = 1byte, 1KB = 1024B, 1 MB = 1024KB
* 计算机的数字系统是2进制的，基本符号只有0和1
* 八进制和十六进制的存在意义：比2进制容易读，但是又比10进制容易转换成2进制
* 十进制和2进制的转换
* 正整数和负整数的表示，补码，浮点数和定点数的概念
* 字符的编码表示：ASCII，GB18030等等

## 第二章 C++简单程序设计（一）

#### C++语言概述

* 由C语言发展而来，最初是在C上增加了类的功能。现在最新的版本是2014年发布的C++14
* C++完全兼容C，既可以面向过程，也可以面向对象
* cout是输出流类的一个对象，专门负责向显示器输出

#### C++基本字符集和语法记号

* C++固有关键字，变量名命名规则

#### 基本数据类型

* 整数，浮点数，字符，布尔
* 整数类型包括默认的int（基本整型，长度根据机器不同），signed / unsigned**（默认是signed\)**，short / long / long long
* 浮点数有float \(4 Byte\)和double类型\(8 byte\)
* 字符类型其实也是整数，只占一个Byte （8bit）。**基本数据类型中没有字符串**，**字符的数组可以用来表示字符串，称为C风格字符串**; 而C++中有一个**类型称为String**用来表示字符串
* 布尔值只能取真或者假，也占一个Byte
* **C风格的字符串用双引号表示**，"china"在内存中就是一个字符的数组，最后还有一个'\0'结束符号
* 变量和常量的初始化：

```cpp
int a = 0;
int a(0);  // <= 这个初始化写法比较奇怪
int a = {0};

const float pi = 3.1415;
```

#### 各类基础运算符

* 算术运算符
* 关系运算符，&lt; &gt; = !=
* 逻辑运算，!, && , \|\|
* 条件表达式：**等于是实现了一个简单的if语句**

```cpp
x = a>b?a:b;
```

* sizeof运算，**为什么要用sizeof求数据大小呢**？因为数据在不同机器上的时候，**字节数是可能不同的**

```cpp
sizeof(int);
sizeof x; // 求变量的大小，不加括号
```

* 位运算符：&,\|,^。用来把直接操作数据的位，比如说可以实现把数据的某个位置0，置1。

```text
c = a & 0xFF; // 取出最低8位
c = a | 0xFF; // 最低8位全部置1
c = a ^ 0xFF; // 最低8位翻转
c = ~a;       // 全部翻转
a >> 1;       // 高位是0补0，是1补1
a << 1;       // 低位补0
```

* 类型转换：explicit, implicit; 上面这些基本运算都**要求两边数据类型一致**，如果不一致，**默认的行为就是把低类型转换成高类型**
* 浮点数赋值给整数时，小数部分直接丢失
* explicit类型转换语法：

```cpp
(int) f;
int (f);  
static_cast<int>(f); // C++风格的类型转换
```

## 第三章 C++简单程序设计（二）

#### C++输入输出流

* 将信息从程序空间外，输入程序空间内，称为输入流; 反之就是输出流
* 使用信息流，需要建立流对象，**cin，cout都是预先定义好的标准输入输出流的对象**（也就是从键盘读取，从屏幕输出）。本章仅介绍cin / cout。在后续课程会介绍，给文件输入输出时使用的流对象
* **插入运算符&lt;&lt;，作用在输出流对象cout上**，就可以实现标准输出功能。

```cpp
int a, b;
cin >> a >> b;

// I/O流类库的操作符
cout << setw(5) << setprecision(3) << 3.1415926;
```

#### if语句

* if语句的单选择，双选择，多重选择

```cpp
if (x > y) cout << x;

if (x > y) 
  cout << x;
else 
  cout << y;
  
if (expr1)
  statement1;
else if (expr2)
  statement2;
...
else
  statementn;

```

#### switch语句

```cpp
#include <iostream>
using namespace std;
int main()
{
  int n;
  cout << "Enter a number" << endl;
  cin >> n;
  switch(n){
  case 0:
    cout << "Sunday" << endl;
    break;  // <= break是必须的
  case 1:
    cout << "Monday" << endl;
    break;
  case 2:
    cout << "Tuesday" << endl;
    break;  
  ...
  }
}
```

* 注意在switch结构中，break是必须的，不然会自动falldown执行所有下面的语句

#### while语句，do-while语句，for语句

* for语句处理循环次数已知的语句，while则处理中止情况已知的情况
* **break用于直接跳出最接近的一层循环**，continue用于**跳过当前循环步**，进入下一个循环步骤

#### typedef关键字

```cpp
typedef double Area;
using Area = double;

enum Weekday {sun, mon, tue, wed, thu, fri, sat};
// 默认情况下sun = 0, mon = 1, tue = 2...
enum Weekday {sun = 7, mon = 1, tue, wed, thu, fri, sat};

auto var1 = var2 + var3;
// var1的类型会自动由后面表达式的类型决定
```

## 第四章 函数

* 导学：函数-&gt;程序的功能模块，函数的定义与调用，内联函数，constexpr函数，带默认参数的函数，函数的重载，C++系统函数

#### 定义函数

* 返回值类型 函数名（参数列表） {函数体}
* 函数调用：在调用之前必须要声明函数原型（函数定义在别的文件中，或者函数定义在调用之后）。

```cpp
double power (double x, int n)
{
  double val = 1.0;
  while (n--)
    val *= x;
  return val;
}
```

#### 内联函数

内联函数关键字inline：节省参数传递，控制转移等计算开销。内联函数不能有循环语句，函数定义必须在调用之前。编译器的优化会自动选择在编译时要不要转换成inline函数，因此定义未必100%有效。

```cpp
#include <iostream>
using namespace std;

inline double area(double r)
{
  return 3.14*r*r;
}

int main()
{
  double r = 3.0;
  double a = area(r);
  cout << a << endl;
  return 0;
}
```

#### 嵌套与递归

* 嵌套：函数中调用别的函数。调用时保存调用现场（stack的概念会在第9章学习），呼叫目标函数
* 递归：自己呼叫自己的过程

```cpp
unsigned fac(unsigned n)
{
  unsigned f;
  if (n==0) return 1;
  else 
    f = n * fac(n-1);
  return f;
}
```

* 典型递归例题：从n个人当中选出k个人作为委员会，有多少种选法？

```cpp
int selection(int n, int k)
{
  if (k==1)
    return (n - k + 1);
  else
    return n / k * selection(n-1, k-1);
}
```

* Hanoi tower

```cpp
void move(char src, char dest)
{
  cout << src << "->" << dest << endl;
}
void hanoi(int m, char src, char medium, char dest)
{
  if (m==1)
    move(src,dest);
  else{
    hanoi(m-1, src, dest, medium);
    move(src, dest);
    hanoi(m-1, medium, src, dest);
  }
}
```

#### 函数的参数传递：单向传递与双向传递

* 函数的参数传递。函数在被调用时才给参数分配空间，接收实际的参数。参数的接收有单向和双向。**默认情况下是单向的，也就是传值**。在单向的时候，参数只能作为辅助函数用，而不能被修改。
* 有时候，**函数想要返回多个值，而返回值只能返回一个值，这个时候就需要双向传递**，传引用。另外，有时候传给函数的参数本身非常庞大，不希望通过传值而希望**传引用**，这个时候也用到传递引用，但是又不希望函数修改这个参数本身。

#### 引用类型

* 引用可以理解为，给变量取一个别名，所以**引用类型在声明时必须要声明是哪个变量的别名**。另外，引用类型的符号&可以跟在类型后，也可以写在变量前，并不影响。

```cpp
#include <iostream>
using namespace std;
{
    int a = 3;
    int &b = a;  //b就是a的引用，即b是a的一个别名。引用必须初始化，否则编译会报错

    b = 10;
    cout<< a << endl; //此时a 的值，已由原来的3变成了10.
    //因为我们无论对别名做什么操作，其实都是对变量的本身做操作。
    return 0;
}
```

* 引用类型实现了类似指针的操作，通过函数反过来操作参数。但是引用类型的灵活性肯定是低于指针。定义函数的时候，定义参数类型为引用类型，

```cpp
// 这个函数是没效果的
void swap(int a, int b)
{
  int temp = a;
  a = b;
  b = temp;
}

// 这样就可以了，因为进行了双向传递
void swap(int &a, int &b)
{
  int temp = a;
  a = b;
  b = temp;
}

// 调用的时候
int main()
{
  int a = 1;
  int b = 3;
  swap(a, b); // <= 调用的时候并不需要声明引用类型的，因为调用的时候行参实参会结合
}
```

#### 带有可变参数长度的函数\(C++11\)

* initialization\_list &lt;T&gt; var;

#### constexpr函数

* constexpr是一个前缀修饰，是c++11的新功能。比如下面的例子，constexpr的返回值必须是常量，在编译时就可以计算出来。

```cpp
constexpr int get_size(){ return 20;}
```

#### 带默认参数值的函数

* 在定义函数时，预先给参数设置默认值的方式

```cpp
int add(int a = 5, int b = 6)
{
  return a + b;
}

add(10,20) // => 30
add(10) // => 16, because a = 10 now
```

#### 函数重载

* 函数重载是多态的一个体现。**比如现在写一个返回绝对值的函数，我们希望他可以处理整数和小数，于是我们就需要写两个函数定义**，但是函数的名字是可以一样的，只是参数表不同

```cpp
int abs(int x)
{
  return x<0? -x:x;
}

double abs(double x)
{
  return x<0? -x:x;
}
```

#### C++系统函数

* 使用系统函数时要包括相应的头文件，比如数学函数在cmath中

```cpp
#include <iostream>
#include <cmath>

using namespace std;

int main()
{
  double angle;
  cin >> angle;
  cout << sin(angle) << endl;
  return 0;
}
```

## 第五章 类与对象

#### 面向对象编程的特点

* 抽象：数据抽象和代码抽象
* 例子：钟表

```cpp
class Clock
{
  public:
    void setTime(int hour, int minute, int second);
    void getTime();
  private: int hour, minute, second;
}; // <= 注意这里要分号，因为这是一个声明而不是定义
```

* 封装：接口与隐藏细节
* 继承：第七章介绍
* 多态：第八章介绍

#### 类与对象的定义

* 定义一个类的基本语法

```cpp
class name{
  public:
         公有成员（外部接口）
  private:
         私有成员
  protected:
         保护成员
};// <= 注意这里要分号，因为这是一个声明而不是定义
```

* 公有成员：与外部接口。
* 私有成员：只允许本类中的函数访问，类外部不能访问。
* 对象定义的语法：

```cpp
Clock myClock;
myClock.getTime();
```

* 类的成员函数定义两种方式：
* * **可以在类内给出函数体**
  * **也可以在类内只声明，在类外来定义函数体**。类外定义时需要在函数名前注明类的名字（ **:: 在这里称为作用域限定符**）：

```cpp
class Clock
{
  public:
    void setTime(int newH=0, int newM=0, int newS=0);
    void getTime();
  private: int hour, minute, second;
};// <= 注意这里要分号，因为这是一个声明而不是定义

// 注意这里定义成员函数的语法
void Clock::setTime(int newH, int newM, int newS)
{
  hour = hour;
  minute = newM;
  second = newS;
}

void Clock::getTime()
{
  cout << hour << ":" << minumte << ":" << second << endl;
}

int main()
{
  Clock myClock;
  myClock.setTime(8,30,30);
  myClock.getTime();
  return 0;
}
```

#### 构造函数

* **函数名与类名相同**，构造函数不可以定义返回值语句; 构造函数在建立对象时自动被调用
* **允许不定义构造函数**; 没有定义构造函数的时候，编译器会自动给出一个默认的构造函数

```cpp
class Clock
{
  public:
    // 构造函数，没有返回值类型
    Clock(int newH, int newM, int newS);
    Clock();  // 提供一个默认构造函数，可以不给参数
    void setTime(int newH=0, int newM=0, int newS=0);
    void getTime();
  private: int hour, minute, second;
};// <= 注意这里要分号，因为这是一个声明而不是定义

Clock::Clock(int newH, int newM, int newS):
  hour(newH), minute(newM), second(newW){
}

Clock::Clock(): hour(0), minute(0), second(0){
}

int main()
{
  Clock c1(8,30,0); // <= 第一种调用构造的方法
  Clock c2;  // <- 此处调用无参数的构造函数
  ...
}
```

* 构造函数**初始化列表的方法**（看上面的例子）

#### 复制构造函数

* 用一个对象复制一个新的对象时用到的构造函数

```cpp
class Book
{
  public:
    Book(int p);
    Book(const Book &b); // <= 复制构造函数
  private:
    int price;
}
Book::Book(const Book &b)
{}
```

* 这里的**const是希望保护原来的对象**，因为引用对象是存在修改原来对象的可能性的
* 复制构造函数被调用的三种情况：

1. **用一个对象初始化另一个对象**

```cpp
Clock a(0,0,0);
Clock b(a); // <- 用a初始化b
```

2. 函数的参数有一个对象，那么在呼叫函数的时候，就会调用复制构造，复制一个对象传递给函数。想一下这个和传递基本型给函数是一样的，**函数传递的总是复制**，而不是对象本身。

```cpp
void func(Point p)
{
  ...;
}

Point p;
func(p); //<- 这里会调用复制构造来构造一个对象传递给函数的
```

```cpp
class Point
{
  public:
    Point(int xx=0, int yy =0){ x = xx; y = yy;}
    Point(const Point& p) = delete; // <= C++11的新关键字delete
  private:
    int x,y;
}
```

* 默认构造函数的无效化，使用C++11的新关键字delete

#### 析构函数

* 对象生命周期结束时调用的函数，用来做对象消灭后的善后工作。**析构函数用波浪符号开始，不能有返回值，也不能有参数列表**

```cpp
class Point
{
  public:
    Point(int xx=0, int yy =0){ x = xx; y = yy;}
    ~Point(); // <= 析构函数不可以有参数
  private:
    int x,y;
}

Point::~Point(){
}
```

#### 类的组合

#### 前向引用声明

```cpp
class B; // 前向引用声明

class A
{
  public:
  void f(B b);
};

class B
{
  public:
  void g(A a);
};
```

#### UML简介

* 三个基本部分：事物，关系，图
* UML图标的简介，各种类的依赖关系

#### 结构体struct

* 结构体在C++中是一种特殊类，默认成员变量都是public。（一般类默认是private）
* 对于一组组合在一起的数据，而没有太多的操作函数，就可以考虑使用struct
* 结构体的声明和类基本类似，关键字使用struct而不是class
* C++中的struct也可以定义函数成员，C中是不可以的

```cpp
struct Student
{
  int num;
  string name;
  char sex;
  int age;
};

Student stu = {98001, "Lin Lin", 'F', 19};
cout << stu.name << endl;
```

#### 联合体union

* 联合体的定义也和struct很相似，不同之处是联合体的所有成员都共用一个内存，不能同时存在

```cpp
union Mark
{
  // 以下三个成员只能存在一个
  char grade;
  bool pass;
  int percent;
};
```



