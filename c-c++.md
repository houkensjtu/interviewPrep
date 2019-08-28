# C/C++

### 背景和历史

C语言是为了帮助Unix开发而发明的语言。C语言相比它的前身B语言，有了型的概念。C语言中有字符，整数，浮点数这几种基础数据类型，并有指针，数组，结构体等衍生数据类型。C语言提供了基本的条件判断\(if-else\)和循环体\(while, for\)语句。C的函数可以返回任何基础数据类型，或者指针，或者结构体**\(不能直接返回数组\)。**

从语言特征上看，C语言很接近底层硬件，因为C可以直接操作内存。C语言也很精简，没有包括很多库，也没有提供并行运算等高级功能。这些都是为了保持语言本身小而美做出的牺牲。

C语言是跨平台的，可以在多种电脑架构上运行。C语言并不是非常强的型语言\(not a strongly-typed language\)，但是在C标准的发展过程中，对于型转换的规定越来越严格，比如早期指针和整数的转换是自由的，但是现在需要明确的声明才可以进行。

### 基本程序结构

每个C程序都需要有一个main函数，printf这个函数来自于stdio.h头文件，所以需要在程序开始的时候导入。一个小细节，K&R书中的风格是把函数体的花括号自成一行编写的~~，这样比较有逼格~~。另外，缩进并没有严格的规定，这里采用2格使得文面更加整洁紧凑。

```c
#include <stdio.h>

int main()
{
  printf("Hello world!\n");
}
```

#### 循环体

第二个程序是打印一个摄氏温度与华氏温度的转换表，需要用到基本的变量声明语句，基本的循环体和格式打印语句。

```c
#include <stdio.h>

int main()
{
  float celsius, fahr;
  int upper, lower, step;
  lower = 0;
  upper = 300;
  step  = 10;
  
  fahr = lower;
  
  // while循环体版本
  while(fahr <= upper) {
    celsius = (5.0/9.0)*(fahr-32.0);
    printf("%3.0f\t%6.1f\n",fahr,celsius)
    fahr += step;
  }
  
  // for 循环体版本
  for(fahr=lower; fahr<=uppper; fahr+=step) {
    celsius = (5.0/9.0)*(fahr-32.0);
    printf("%3.0f\t%6.1f\n",fahr,celsius)
  }
}
```

这里我们再次观察到几个细节：

* 同类型变量声明可以放在同一行，用逗号隔开
* fahr = lower这个语句事实上发生了浮点数与整数的自动转换，C语言会负责自动将lower转成浮点数然后代入fahr
* printf中的%是一个占位符，用来吸收逗号后面的变量；%f是浮点数，%d是整数
* while循环体后面的花括号是不换行的，这和主函数的声明不一样

另外，注意到0,300,20这些数字，其实并不需要是变量，但是在程序中用一些意味不明的魔法数字又是不好的习惯，所以我们可以用符号常量的方法：

```c
#include <stdio.h>

// 符号常量习惯上用大写表示，以便与变量区分
// 另外，define语句的末尾没有分号
#define UPPER 300
#define LOWER 0
#define STEP 20

int main()
{  
  float celsius, fahr;
  fahr = LOWER;
  ...
}
```

#### 简单的输入输出程序

K&R的书中在这里开始介绍了一些比较难解的文件IO程序例子，这里仅仅列举第一个作介绍：

```c
#include <stdio.h>

int main()
{
  int c;
  while((c=getchar()) != EOF)
    putchar(c);
}
```

getchar\(\)这个函数的作用，是从标准输入中读取一个字符，每次读取结束由键盘的回车来决定，如果回车之前输入了多个字符，那getchar\(\)仅仅返回第一个字符。这个程序难解的原因之一是，**实际运行时每输入一个字符并不会直接打印出来，而是会进入line buffer**，等到回车以后再打印出。这个buffer的动作在这段代码里是看不出来的\(这是操作系统terminal提供的功能\)，K&R书中也没有做介绍，所以让读者容易陷入困惑。

另外值得注意的一个技巧是，**在C中所有的赋值表达式本身，也都是有值的**，比如c=getchar\(\)这个语句的值，就是赋值后c的值。因此，可以用语句来作为while条件判断的一部分。

最后，如果你感到疑惑，getchar\(\)和scanf\(\)都是从stdin中读取数据，不同的是scanf是带有格式指定的，而getchar\(\)没有。

#### 数组

我们要浅尝一下数组的使用，数组的基本使用无非有几个点：数组的声明，数组的初始化，数组的取用。

```c
int i;
int ndigit[10];

// 逐一赋值
for (i=0; i<10; i++){
  ndigit[i] = 0;
}
// 作为数组赋值
ndigit[] = {0,1,2,3,4,5,6,7,8,9};
ndigit[10] = {0,1,2,3,4,5,6,7,8,9};

// 奇技淫巧: 生成一个10个元素的数组，最后一个是10，其他默认都是0
ndigit[] = {[9] = 10};
```

数组声明的方法就是在变量名后面加上方括号和数组的大小，数组的index在C中是从0开始的。数组赋值的方法，除了逐一赋值，也可以用给定数组的方法赋值，**注意到数组常量的表示法是用花括号而不是方括号。**这里的原因有很多，首先需要认识到的是，**C语言中并没有数组字面值这个东西，数组的变量是一个指针，如果说数组要赋值，那也只能赋值一个指针**。所以这里的花括号表示的并不是数组本身，而是一个初始化写法。

#### 简单函数声明

函数的**调用如果在定义之前**，那么是需要像下面这样先声明，不然的话目前的gcc会报warning，不过可以运行。**调用如果在定义之后**，那么事实上是不需要再次另外声明的。另外一个基本概念是，**C中的函数都是传值的**，也就是说给函数的参数都是一个拷贝，而不是对原对象的直接操作。（当然直接操作可以通过指针实现，这是后话）

```c
#include <stdio.h>

// 函数需要事先声明
int power(int m, int n);
// 声明的时候可以只给出参数的类型，不需要赋予名字
int power(int, int);

int main()
{
  int i = 0;
  for (i=0; i<10; i++)
    printf("%6d \n",power(i));
}

int power(int base, int n)
{
  int i,p;
  
  p = 1;
  for (i=n; i>0; i--)
    p = p*base;
  return p;
}

```

#### extern关键词

extern表示的是外部变量。在C中可以在函数体之外声明一些公共的变量，在函数体内调用这些公共变量之前，需要先声明extern。所以，**看到extern就知道表明，这是一个共有的变量**。

```c
int m,n;
int main()
{
  extern int m,n;
  ...
}

int func()
{
  extern int m,n;
}
```

### 基础变量类型

C语言中的变量类型并不多：

```c
int i; // int还有long int, short int等变化，可以加signed或者unsigned修饰符
char c; // unsigned char表示0-255的整数值，sign则是-128-127
float f;
double d;
```

C中并没有字符串这个类型，所谓string就是字符的数组char\[ \]。**注意在C当中，双引号和单引号是不同的，单引号是字符**。

```c
char c[5] = "Hello";
```

另外提一下enum枚举常量。enum在声明过后，就像一个新的类型一样，不同之处是，enum只能容纳在声明时初始化列表中的那些值，而且这些值如果没有特别声明，就是从0开始的一串整数。

```c
// enum会自动赋予值，第一个为0，第二个为1，以此类推
// 自动赋值是用enum的一大便利之处
enum boolean {NO, YES};
enum months {JAN = 1, FEB, MAR, APR, MAY, JUN, JUL, AUG, SEP, OCT, NOV, DEC};
```

```c
#include <stdio.h>

int main()
{
  enum suit {club, diamond, heart, spade};
  
  // enum 配合tag名字，就好像是一个新的类型。其取值就是只能是上面声明时的这些中的一个
  enum suit card;
  card = heart;
  
  printf("Heart is the %d th suit.\n", card);
  // => Heart is the 2 th suit.
}
```

最后是const修饰符，如果变量用const修饰，就说明不能修改。一个重要应用是在传给函数数组时添加const，防止函数修改数组

```c
int func(const char c[]);
```

#### 型转换

型转换有两种，显示\(也叫cast\)，或者隐式。

**隐式的型转换发生在两种数据类型出现在同一个表达式中时**，往往C的规则是把数据统一向更大的数据类型，比如，浮点数和整形在一起的表达式，C倾向于把整形变成浮点数。

**显示的转换也叫cast**，用来表示用户有意图地要转换变量类型。比如double sqrt\(double n\)这个函数，说了传递参数必须是一个double类型，于是我们可以这样做

```c
int i = 2;
return sqrt((double) i); // 强制cast了i这个变量
```

#### 位操作运算

```c
& // bitwise AND
| // bitwise OR
^ // bitwise XOR
~ // bitwise NOT ( 0011-> 1100)
<< // left shift
>> // right shift

/* These operators are not bitwise */
&& // logic AND
|| // logic OR
```

在位操作中用一个flag变量来和对象做AND运算以实现mask一些位是常用技巧。

```c
int SET_ON = 0x0011;
int n = n & SET_ON;
```

#### 条件表达式

```c
// expr1 ? expr2 : expr3
int z = (a>b)? a : b;

//相当于下面的代码
int z;
if (a>b)
  z = a;
else 
  z = b;
```

### 条件控制语句

C语言中的条件控制大多数都是遵循比较旧的代码风格：条件本身用小括号表示，处理部分用花括号括起。下面结合K&R中的实例解释几种条件语句。

#### if-else语句

这里对于if-else的功能本身不再作赘述，只是K&R中给出了一个binary search的例子非常优美因此在此借用：

```c
// 我在看之前自己考虑的版本，假设给定的数组已经sort好了
#include <stdio.h>

int binary_search(int num[], int len, int target)
{
  int lower = 0;
  int upper = len-1;
  int current = 0;
  while (upper > lower + 1) { // 当upper和lower中间已经没有数字时
    current = (upper + lower) / 2;
    if (num[current] > target) 
      upper = current;
    else if (num[current] < target) 
      lower = current;
    else if (num[current] == target) 
      return num[current];
  }
  return -1;
}

int main()
{
  int num[] = {1,3,5,7,9,11,13,15};
  int len = 8;
  printf("4 is the %d th element of the list.\n", binary_search(num[],len,4));
}
```

```c
// 以下K&R的版本
int binarysearch(int x, int v[], int n)
{
  int low, high, mid;
  
  low = 0;
  high = n - 1;
  while (low <= high) {
    mid = (low+high) / 2;
    if (x < v[mid]) 
      high = mid -1;
    else if (x > v[mid])
      low = mid + 1;
    else 
      return mid;
  }
  return -1;
}
```

#### switch语句

这里用一个统计输入中字符类型的片段来作为例子：

```c
while ((c = getchar()) != EOF) {
  switch (c) {
    case '0': case '1': case '2': case '3': case '4': case '5': 
    case '6': case '7': case '8': case '9': 
      ndigit[c-'0']++;
      break;
    case '\t':
      nwhite++;
      break;
    case '\n':
      nline++;
      break;
    default:
      nother++;
      break;
  }
}
```

break的作用是立即退出switch，因为这里如果一个条件满足了就没有必要再执行switch中剩下的部分。break也可以用来退出while,for等其他循环体。

#### 循环体：while / for

for和while循环体的写法是非常直观易于理解的，这里不再赘述。在使用上，for适用于有计数，需要初始化等细节控制的循环，而while则适合于对于循环次数没有具体控制的情况。这里K&R引用一个叫做Shell sort的排序算法来演示for循环：

```c
// Shell sort!
void shell_sort(int v[], int n)
{
  int gap, i, j, temp;
  
  for (gap = n/2; gap>0; gap /= 2) {
    for (i = gap; i < n; i++) {
      for (j = i-gap; j>=0 && v[j]>v[j+gap]; j-=gap) {
        temp = v[j];
        v[j] = v[j+gap];
        v[j+gap] = temp;
      }
    }
  }
}
```

最后，书中介绍了一个可以在for循环体中运行两个条件语句的逗号方法

```c
void reverse(char s[])
{
  int i, j;
  char temp;
  for (i=0, j=strlen(s)-1; i<j; i++, j--){
    s[i] = temp;
    s[i] = s[j];
    s[j] = temp;
  }
}
```

#### break和continue

break就是跳出循环体，提前结束循环。而continue是跳过循环的一个步，重新回到循环的头上来。下面这个例子演示了如何跳过一个数组中的负数，而仅对正数做处理。

```c
for (i=0; i<n; i++){
  if (s[i]<0)
    continue;
  // do sth. to positive elements.
}
```

### 函数

传递参数的三种方式，pass by value, pass by reference, pass pointer

```c
int func(int x){
... 
}

int func(int *x){
... 
}

int func(int &x){
... 
}
```

