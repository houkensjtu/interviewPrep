# bitOperations
Bit hacks in C.

### 1. 返回整数的符号

```c
int v;      // 对象整数
int sign;   // 输出符号

sign = -(v < 0);  // 普通方法，如果小于0则返回-1，否则返回0
// CHAR_BIT是1 byte所含比特数，一般等于8
sign = -(int)((unsigned int)((int)v) >> (sizeof(int) * CHAR_BIT - 1));
// or, for one less instruction (but not portable):
sign = v >> (sizeof(int) * CHAR_BIT - 1); 
```
