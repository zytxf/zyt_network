# C语言快速入门（Wiki)



**C**是一种通用的编程语言，广泛用于系统软件与应用软件的开发。于1969年至1973年间，为了移植与开发[UNIX](https://zh.wikipedia.org/wiki/UNIX)[操作系统](https://zh.wikipedia.org/wiki/%E4%BD%9C%E6%A5%AD%E7%B3%BB%E7%B5%B1)，由[丹尼斯·里奇](https://zh.wikipedia.org/wiki/%E4%B8%B9%E5%B0%BC%E6%96%AF%C2%B7%E9%87%8C%E5%A5%87)与[肯·汤普逊](https://zh.wikipedia.org/wiki/%E8%82%AF%C2%B7%E6%B1%A4%E6%99%AE%E9%80%8A)，以[B语言](https://zh.wikipedia.org/wiki/B%E8%AF%AD%E8%A8%80)为基础，在[贝尔实验室](https://zh.wikipedia.org/wiki/%E8%B4%9D%E5%B0%94%E5%AE%9E%E9%AA%8C%E5%AE%A4)设计、开发出来。

C语言具有高效、灵活、功能丰富、表达力强和较高的[可移植性](https://zh.wikipedia.org/wiki/%E7%A7%BB%E6%A4%8D_(%E8%BB%9F%E9%AB%94))等特点，在[程序设计](https://zh.wikipedia.org/wiki/%E7%A8%8B%E5%BA%8F%E8%AE%BE%E8%AE%A1)中备受青睐，成为最近25年使用最为广泛的编程语言[[2\]](https://zh.wikipedia.org/wiki/C%E8%AF%AD%E8%A8%80#cite_note-AutoTX-3-2)。目前，C语言[编译器](https://zh.wikipedia.org/wiki/%E7%B7%A8%E8%AD%AF%E5%99%A8)普遍存在于各种不同的[操作系统](https://zh.wikipedia.org/wiki/%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F)中，例如[Microsoft Windows](https://zh.wikipedia.org/wiki/Microsoft_Windows)、[macOS](https://zh.wikipedia.org/wiki/Mac_OS_X)、[Linux](https://zh.wikipedia.org/wiki/Linux)、[Unix](https://zh.wikipedia.org/wiki/Unix)等。C语言的设计影响了众多后来的编程语言，例如[C++](https://zh.wikipedia.org/wiki/C%2B%2B)、[Objective-C](https://zh.wikipedia.org/wiki/Objective-C)、[Java](https://zh.wikipedia.org/wiki/Java)、[C#](https://zh.wikipedia.org/wiki/%EF%BC%A3%EF%BC%83)等。

二十世纪八十年代，为了避免各开发厂商用的C语言语法产生差异，由[美国国家标准局](https://zh.wikipedia.org/wiki/%E7%BE%8E%E5%9C%8B%E5%9C%8B%E5%AE%B6%E6%A8%99%E6%BA%96%E5%B1%80)为C语言订定了一套完整的国际标准语法，称为[ANSI C](https://zh.wikipedia.org/wiki/ANSI_C)，作为C语言的标准。二十世纪八十年代至今的有关程序开发工具，一般都支持匹配ANSI C的语法。

## 设计

C语言设计目标是提供一种能以简易的方式编译、处理低级存储器、产生少量的[机器代码](https://zh.wikipedia.org/wiki/%E6%A9%9F%E6%A2%B0%E7%A2%BC)以及不需要任何运行环境支持便能运行的编程语言。C语言也很适合搭配[汇编语言](https://zh.wikipedia.org/wiki/%E6%B1%87%E7%BC%96%E8%AF%AD%E8%A8%80)来使用。尽管C语言提供许多低级处理的功能，但仍保持良好[跨平台](https://zh.wikipedia.org/wiki/%E8%B7%A8%E5%B9%B3%E5%8F%B0)的特性，以一个标准规格写出的C语言程序可在许多计算机平台上进行编译，甚至包含一些嵌入式处理器（[微控制器](https://zh.wikipedia.org/wiki/%E5%BE%AE%E6%8E%A7%E5%88%B6%E5%99%A8)或称MCU）以及[超级计算机](https://zh.wikipedia.org/wiki/%E8%B6%85%E7%B4%9A%E9%9B%BB%E8%85%A6)等作业平台。

## 概述

### 特性

- C语言是一个有结构化程序设计、具有变量作用域（variable scope）以及递归功能的过程式语言。
- C语言传递参数均是以值传递（pass by value）[[3\]](https://zh.wikipedia.org/wiki/C%E8%AF%AD%E8%A8%80#cite_note-3)，另外也可以传递指针（a pointer passed by value）。
- 不同的变量类型可以用结构体（struct）组合在一起。
- 只有32个保留字（reserved keywords），使变量、函数命名有更多弹性。
- 部分的变量类型可以转换，例如整型和字符型变量。
- 透过[指针](https://zh.wikipedia.org/wiki/%E6%8C%87%E6%A8%99_(%E9%9B%BB%E8%85%A6%E7%A7%91%E5%AD%B8))（pointer），C语言可以容易的对存储器进行低级控制。
- 编译预处理（preprocessor）让C语言的编译更具有弹性。

## 历史

### 早期发展

![img](https://upload.wikimedia.org/wikipedia/commons/thumb/4/46/Ken_Thompson_and_Dennis_Ritchie.jpg/220px-Ken_Thompson_and_Dennis_Ritchie.jpg)



肯·汤普逊和丹尼斯·里奇，是C编程语言的开发者.

C语言最早由[丹尼斯·里奇](https://zh.wikipedia.org/wiki/%E4%B8%B9%E5%B0%BC%E6%96%AF%C2%B7%E9%87%8C%E5%A5%87)（Dennis Ritchie）为了在[PDP-11](https://zh.wikipedia.org/wiki/PDP-11)计算机上运行的[Unix](https://zh.wikipedia.org/wiki/Unix)系统所设计出来的编程语言，第一次发展在1969年到1973年之间。

C源于[BCPL语言](https://zh.wikipedia.org/wiki/BCPL)，后者由[马丁·理察德](https://zh.wikipedia.org/wiki/%E9%A6%AC%E4%B8%81%C2%B7%E7%90%86%E5%AF%9F%E5%BE%B7)（Martin Richards）于1967年左右设计实现。BCPL是一门"无类型"的编程语言：它仅能操作一种数据类型，即[机器字](https://zh.wikipedia.org/wiki/%E5%AD%97_(%E8%AE%A1%E7%AE%97%E6%9C%BA))（machine word）。1970年，肯·汤普逊为运行在[PDP-7](https://zh.wikipedia.org/wiki/PDP-7)上的首个Unix系统设计了一个精简版的BCPL，这个语言被称为[B语言](https://zh.wikipedia.org/wiki/B%E8%AF%AD%E8%A8%80)，它也是无类型的。

Unix最早运行在PDP-7上，是以[汇编语言](https://zh.wikipedia.org/wiki/%E7%B5%84%E5%90%88%E8%AA%9E%E8%A8%80)写成。在PDP-11出现后，丹尼斯·里奇与[肯·汤普逊](https://zh.wikipedia.org/wiki/%E8%82%AF%C2%B7%E6%B1%A4%E6%99%AE%E9%80%8A)着手将[Unix](https://zh.wikipedia.org/wiki/Unix)移植到PDP-11上，无类型的语言在PDP-11上愈发显得合适。PDP-11提供了多种不同规格大小的基本对象：一字节长的字符，两字节长的整型数以及四字节长的浮点数。B语言无法处理这些不同规格大小的对象，也没有提供单独的操作符去操作它们。

C语言最初尝试通过向B语言中增加数据类型的想法来处理那些不同类型的数据。和大多数语言一样，在C中，每个对象都有一个类型以及一个值；类型决定了可用于值的操作的含义，以及对象占用的存储空间大小。

1973年，Unix[操作系统](https://zh.wikipedia.org/wiki/%E4%BD%9C%E6%A5%AD%E7%B3%BB%E7%B5%B1)的核心正式用C语言改写，这是C语言第一次应用在操作系统的核心编写上。

1975年C语言开始移植到其他机器上使用。[史蒂芬·强生](https://zh.wikipedia.org/w/index.php?title=%E5%8F%B2%E8%92%82%E8%8A%AC%C2%B7%E5%BC%B7%E7%94%9F&action=edit&redlink=1)实现了一套“[可移植编译器](https://zh.wikipedia.org/wiki/%E5%8F%AF%E7%A7%BB%E6%A4%8DC%E7%B7%A8%E8%AD%AF%E5%99%A8)”，这套编译器修改起来相对容易，并且可以为不同的机器生成代码。从那时起，C在大多数计算机上被使用，从最小的微型计算机到与CRAY-2超级计算机。C语言很规范，即使没有一份正式的标准，你也可以写出C程序，这些程序无须修改就可以运行在任何支持C语言和最小运行时环境的计算机上。

C最初在小型机器上实现，并且继承了一系列小语种编程语言的特点；与功能相比，C的设计者更倾向于简单和优雅。此外，从一开始，C语言就是为系统级编程而设计，程序的运行效率至关重要，因此，C语言与真实机器能力的良好匹配也就不足为奇。例如，C语言为典型硬件所直接支持的对象：[字符](https://zh.wikipedia.org/wiki/%E5%AD%97%E7%AC%A6)，[整数](https://zh.wikipedia.org/wiki/%E6%95%B4%E6%95%B0)（也许有多种大小），以及[浮点数](https://zh.wikipedia.org/wiki/%E6%B5%AE%E7%82%B9%E6%95%B0)（同样可能有多种大小）提供了相应的基本数据类型。

### K&R C

![img](https://upload.wikimedia.org/wikipedia/commons/thumb/9/95/The_C_Programming_Language%2C_First_Edition_Cover_%282%29.svg/171px-The_C_Programming_Language%2C_First_Edition_Cover_%282%29.svg.png)



《C程序设计语言》第一版封面

1978年，[丹尼斯·里奇](https://zh.wikipedia.org/wiki/%E4%B8%B9%E5%B0%BC%E6%96%AF%C2%B7%E9%87%8C%E5%A5%87)和[布莱恩·柯林汉](https://zh.wikipedia.org/wiki/%E5%B8%83%E8%90%8A%E6%81%A9%C2%B7%E6%9F%AF%E6%9E%97%E6%BC%A2)合作出版了《[C程序设计语言](https://zh.wikipedia.org/wiki/C%E7%A8%8B%E5%BA%8F%E8%AE%BE%E8%AE%A1%E8%AF%AD%E8%A8%80_(%E4%B9%A6))》的第一版。书中介绍的C语言标准也被C语言程序员称作“K&R C”，第二版的书中也包含了一些[ANSI C](https://zh.wikipedia.org/wiki/ANSI_C)的标准。

K&R C主要引入了以下语言特性：

- 标准I/O库
- 结构（`struct`）类型
- 长整数（`long int`）类型
- 无符号整数（`unsigned int`）类型
- 把运算符`=+`和`=-`改为`+=`和`-=`。因为`=+`和`=-`会使得编译器不知道用户要处理`i = -10`还是`i =- 10`，使得处理上产生混淆。

即使在后来[ANSI C标准](https://zh.wikipedia.org/wiki/ANSI_C)被提出的许多年后，K&R C仍然是许多编译器的最低标准要求，许多老旧的编译仍然运行K&R C的标准。

### ANSI C 和 ISO C

主条目：[ANSI C](https://zh.wikipedia.org/wiki/ANSI_C)

1989年，C语言被[美国国家标准协会](https://zh.wikipedia.org/wiki/%E7%BE%8E%E5%9C%8B%E5%9C%8B%E5%AE%B6%E6%A8%99%E6%BA%96%E5%8D%94%E6%9C%83)（ANSI）标准化，编号为ANSI X3.159-1989。这个版本又称为C89。标准化的一个目的是扩展K&R C，增加了一些新特性。

- `void` 函数
- 函数返回 `struct` 或 `union` 类型
- `void *` 数据类型

1990年，[国际标准化组织](https://zh.wikipedia.org/wiki/%E5%9B%BD%E9%99%85%E6%A0%87%E5%87%86%E5%8C%96%E7%BB%84%E7%BB%87)（ISO）成立 ISO/IEC JTC1/SC22/WG14 工作组，来规定国际标准的C语言，通过对ANSI标准的少量修改，最终制定了 ISO 9899:1990，又称为C90。随后，ANSI亦接受国际标准C，并不再发展新的C标准。

K&R C语言到ANSI/ISO标准C语言的改进包括：

- 增加了真正的标准库
- 新的预处理命令与特性
- 函数原型允许在函数申明中指定参数类型
- 一些新的关键字，包括 `const`、`volatile` 与 `signed`
- 宽字符、宽字符串与多字节字符
- 对约定规则、声明和类型检查的许多小改动与澄清

WG14工作小组之后又于1994年，对1985年颁布的标准做了两处技术修订（缺陷修复）和一个补充（扩展）。下面是 1994 年做出的所有修改：

- 3 个新的标准库头文件 iso646.h、wctype.h 和 wchar.h
- 几个新的记号与预定义宏，用于对国际化提供更好的支持
- printf/sprintf 函数一系列新的格式代码
- 大量的[函数](https://zh.wikipedia.org/wiki/%E5%87%BD%E6%95%B0)和一些[类型](https://zh.wikipedia.org/wiki/%E8%B3%87%E6%96%99%E9%A1%9E%E5%9E%8B)与[常量](https://zh.wikipedia.org/wiki/%E5%B8%B8%E6%95%B8)，用于[多字节字符](https://zh.wikipedia.org/w/index.php?title=%E5%A4%9A%E5%AD%97%E8%8A%82%E5%AD%97%E7%AC%A6&action=edit&redlink=1)和[宽字节字符](https://zh.wikipedia.org/w/index.php?title=%E5%AE%BD%E5%AD%97%E8%8A%82%E5%AD%97%E7%AC%A6&action=edit&redlink=1)

### C99

在ANSI的标准确立后，C语言的规范在一段时间内没有大的变动，然而C++在自己的标准化创建过程中继续发展壮大。《标准修正案一》在1994年为C语言创建了一个新标准，但是只修正了一些C89标准中的细节和增加更多更广的国际字符集支持。不过，这个标准引出了1999年[ISO 9899:1999](https://zh.wikipedia.org/w/index.php?title=ISO_9899:1999&action=edit&redlink=1)的发表。它通常被称为C99。C99被ANSI于2000年3月采用。

在C99中包括的特性有：

- 增加了对编译器的限制，比如源始码每行要求至少支持到 4095 字节，变量名函数名的要求支持到 63 字节（extern 要求支持到 31）。

- 增强了预处理功能。例如：

  - [宏](https://zh.wikipedia.org/wiki/%E5%B7%A8%E9%9B%86)支持取可变参数 #define Macro(...)  \__VA_ARGS__
  - 使用[宏](https://zh.wikipedia.org/wiki/%E5%B7%A8%E9%9B%86)的时候，允许省略参数，被省略的参数会被扩展成空串。
  - 支持 // 开头的单行注释（这个特性实际上在C89的很多编译器上已经被支持了）

- 增加了新关键字

   

  restrict, inline, _Complex, _Imaginary, _Bool

  - 支持 `long long, long double _Complex, float _Complex` 等类型

- 支持不定长的数组，即数组长度可以在运行时决定，比如利用变量作为数组长度。声明时使用 `int a[var]` 的形式。不过考虑到效率和实现，不定长数组不能用在全局，或 `struct`与 `union` 。

- [变量](https://zh.wikipedia.org/wiki/%E5%8F%98%E9%87%8F_(%E7%A8%8B%E5%BA%8F%E8%AE%BE%E8%AE%A1))声明不必放在语句块的开头，for 语句提倡写成 `for(int i=0;i<100;++i)` 的形式，即`i` 只在 `for` 语句块内部有效。

- 允许采用`（type_name）{xx,xx,xx}` 类似于 C++ 的构造函数的形式构造匿名的结构体。

- 初始化结构的时候允许对特定的元素赋值，形式为：

- 格式化字符串中，利用 `\u` 支持 unicode 的字符。

- 支持 16 进制的浮点数的描述。

- printf scanf 的格式化串增加了对 `long long int` 类型的支持。

- 浮点数的内部数据描述支持了新标准，可以使用 #pragma 编译器指令指定。

- 除了已有的 `__line__ __file__` 以外，增加了 `__func__` 得到当前的函数名。

- 允许编译器化简非常数的表达式。

- 修改了 `/ %` 处理负数时的定义，这样可以给出明确的结果，例如在C89中`-22 / 7 = -3, -22 % 7 = -1`，也可以`-22 / 7= -4, -22 % 7 = 6`。 而C99中明确为` -22 / 7 = -3, -22 % 7 = -1`，只有一种结果。

- 取消了函数返回类型默认为 `int` 的规定。

- 允许在 `struct` 的最后定义的数组不指定其长度，写做 [](flexible array member)。

- `const const int i` 将被当作 `const int i` 处理。

- 增加和修改了一些标准头文件，比如定义 bool 的 <stdbool.h> ，定义一些标准长度的 int 的 <inttypes.h> ，定义复数的 <complex.h> ，定义宽字符的 <wctype.h> ，类似于泛型的数学函数 <tgmath.h>， 浮点数相关的 <fenv.h>。 在<stdarg.h> 增加了 va_copy 用于复制 ... 的参数。<time.h> 里增加了 struct tmx ，对 struct tm 做了扩展。

- 输入输出对宽字符以及长整数等做了相应的支持。

但是各个公司对C99的支持所表现出来的兴趣不同。当GCC和其它一些商业编译器支持C99的大部分特性的时候[[4\]](https://zh.wikipedia.org/wiki/C%E8%AF%AD%E8%A8%80#cite_note-4)，[微软](https://zh.wikipedia.org/wiki/%E5%BE%AE%E8%BD%AF)和[Borland](https://zh.wikipedia.org/wiki/Borland)却似乎对此不感兴趣。

### C11

主条目：[C11](https://zh.wikipedia.org/wiki/C11)

2011年12月8日，ISO正式发布了新的C语言的新标准C11，之前被称为C1X，官方名称为[ISO/IEC 9899:2011](https://zh.wikipedia.org/wiki/C11)。新的标准提高了对C++的兼容性，并增加了一些新的特性。这些新特性包括泛型宏、多线程、带边界检查的函数、匿名结构等。但直到现在仍未有编译器完整的支持。

## 语法

### Hello World 程序

下面是一个在标准输出设备（stdout）上打印出 "[Hello, world!](https://zh.wikipedia.org/wiki/Hello_World%E7%A8%8B%E5%BA%8F)" 字符串的简单程序。类似的程序，通常作为初学编程语言时的第一个程序：

```c
1 #include <stdio.h>
2 
3 int main(void)
4 {
5     printf("Hello, world!\n");
6     return 0;
7 }
```

### 进一步了解

C语言由函数和变量组成，C的函数就像是[Fortran](https://zh.wikipedia.org/wiki/Fortran)中的子程序和函数。

在C语言中，程序从 [`main`](https://zh.wikipedia.org/wiki/%E4%B8%BB%E5%87%BD%E5%BC%8F#C/C++) 开始执行。`main` 函数通过调用和控制其他函数进行工作。例如上面的`printf`。程序员可以自己写函数，或从库中调用函数。在上面的`return 0;` 使得 `main` 返回一个值给调用程序的[壳层](https://zh.wikipedia.org/wiki/%E6%AE%BC%E5%B1%A4)，表明程序是否成功运行。

一个C语言的函数由返回值、函数名、参数列表和函数体组成。函数体的语法和其它的复合的语句部分是一样的。

### 复合语句

C语言中的复合语句（或称**语句块**）的格式为：

```c
{
    语句;
    语句;
    /* ... */
}
```

复合语句可以使得几个语句从文法上变成一个语句。

有时必须使用复合语句，否则会产生错误。例如，在运用循环语句的时候，如果循环体（即循环中执行部分）包含多个语句（以分号隔开），则必须使用花括号将他们合并成一个复合语句。如果不这么做，系统仅把第一个分号前的内容看做循环体。

需要注意的是，部分C编译器并不支持在任意位置使用复合语句。

### 条件语句

C语言有两种条件语句形式，分别是`if`和`switch`。

If 的格式如下：

```c
if(運算式) // 如果
    語句; 
// 有时还会有 else：
else      // 否则
    語句;
```

表达式的值非零表示条件为真；如果条件为假，程序将跳过`if`处的语句，直接运行`if`后面的语句。但是如果`if`后面有`else`，则当条件为假时，程序跳到`else`处运行。`if`和`else`后面的语句可以是另个`if`语句，这种套叠式的结构，允许更复杂的逻辑控制流程得以实现。在一般情况下，`else`一定与最接近的`if`成对，因此常用括弧`**{}**`越过此限制。比较下面两种情况：

```c
if(逻辑表达式)
    if (逻辑表达式)
        語句; 
    else
        語句;
1 if(逻辑表达式甲)
2 {
3     if(逻辑表达式乙)
4         語句;
5 }
6 else 
7     語句;
```

要注意这里的缩进和换行只用于方便阅读。编译器并不会根据缩进层级猜测 if 和 else 的对应关系。

`switch`通常用于对几种有明确值的条件进行控制。它要求的条件值通常是整数或字符。与`switch`搭配的条件转移是`case`。使用`case`后面的标值，控制程序将跳到满足条件的`case`处一直往下运行，直到语句结束或遇到`break`。通常可以使用`default`把其他例外的情况包含进去。如果`switch`语句中的条件不成立，控制程序将跳到`default`处运行；如果省略`default`子句，则直接运行下一语句。`switch`是可以嵌套的。

```c
switch(值)
{
  case 甲:
  case 乙:
    語句段1; // 甲乙都会执行
    // 更多语句…
    break;  // 跳转到 switch 末尾处
  case 丙:
    語句段2;
    break; 
  default:  // 无论如何都会匹配
    語句段3;
}
```

简单的条件判断也可用?:

```c
運算式?值1:值2;
如:
   a=b>c?b:c // 如果變數"b"的值大於變數"c" 把變數"b"的值賦予變數"a"
```

### 循环语句

C语言有三种形式的循环语句：

```c
do 
    語句
while(判断式); 

和:

while(判断式) 
    語句;

和:

for(起始化; 判断式;運算式)
    語句;
```

在`while`和`for`中，语句将运行到表达式的值为零时结束。在`do...while`语句中，循环将至少被运行一次。这三种循环结构可以互相转化：

```c
for(起始化; 判断式;運算式)
    語句;
```

如果**语句**中不使用continue语句的话，相当于

```c
初始化;
while (判断式) {
    語句;
    運算式;
}
```

当循环条件一直为真时，将产生[死循环](https://zh.wikipedia.org/wiki/%E7%84%A1%E7%AA%AE%E8%BF%B4%E5%9C%88)。

### 跳转语句

跳转语句包括四种：`goto，continue，break和return`。

```
goto 標記;
```

`goto`语句是无条件转移语句，且标记必须在当前函数中定义，使用“标记:”的格式定义。程序将跳到标记处继续运行。由于`goto`（特别是向回 goto 和长距离的 goto）容易产生阅读上的困难，所以对新手应该尽量少用。[GCC](https://zh.wikipedia.org/wiki/GCC) 编译器拓展支持对指针 `goto`和宏内 goto，一定程度上增强了 goto 的可读性。


`continue`语句用在循环语句中，作用是结束当前一轮的循环，马上开始下一轮循环。

`break`语句用在循环语句或`switch`中，作用是结束当前循环，跳到循环体外继续运行。但是使用`break`只能跳出一层循环。在要跳出多重循环时，可以使用`goto`使得程序更为简洁。

当一个函数运行结束后要返回一个值时，使用`return`。`return`可以跟一个表达式或变量。如果`return`后面没有值，将运行不返回值。

### 在C语言中的运算符号

| ()、 []、 -> 、 .、 !、 ++、 --                          | 圆括号、方括号、指针、成员、逻辑非、自加、自减 |
| -------------------------------------------------------- | ---------------------------------------------- |
| ++ 、 -- 、 * 、 & 、 ~ 、 ! 、 + 、 - 、 sizeof、(cast) | 单目运算符                                     |
| * 、 / 、 %、==                                          | 算术运算符                                     |
| + 、 -                                                   | 算术运算符                                     |
| << 、 >>                                                 | 位运算符                                       |
| < 、 <= 、 > 、 >=                                       | 关系运算符                                     |
| == 、 !=                                                 | 关系运算符号                                   |
| &                                                        | 位与                                           |
| ^                                                        | 位异或                                         |
| \|                                                       | 位或                                           |
| &&                                                       | 逻辑与                                         |
| \|\|                                                     | 逻辑或                                         |
| ? :                                                      | 条件运算符                                     |
| = 、 += 、 -= 、 *= 、 /= 、 %= 、 &= 、 \|= 、 ^=       | 赋值运算符                                     |
| ,                                                        | 顺序运算符                                     |

比较特别的是，比特右移（>>）运算符可以是*算术*（左端补最高有效位）或是*逻辑*（左端补 0）位移。例如，将 11100011 右移 3 比特，算术右移后成为 11111100，逻辑右移则为 00011100。因算术比特右移较适于处理带负号整数，所以几乎所有的编译器都是算术比特右移。

运算符的优先级从高到低大致是：单目运算符、算术运算符、关系运算符、逻辑运算符、条件运算符、赋值运算符（=）和逗号运算符。

### 安全性

| 符号 | 安全性         | 符号 | 安全性              | 符号 | 安全性         | 符号 | 安全性 |
| ---- | -------------- | ---- | ------------------- | ---- | -------------- | ---- | ------ |
| +    | 溢出,包裹,循环 | -=   | 溢出,包裹,循环,截裁 | >>   | 无             | >=   | 无     |
| -    | 溢出,包裹,循环 | *=   | 溢出,包裹,循环,截裁 | &    | 无             | ==   | 无     |
| *    | 溢出,包裹,循环 | /=   | 溢出,截裁           | ~    | 无             | !=   | 无     |
| %    | 溢出           | <<=  | 溢出,包裹,循环,截裁 | !    | 无             | &&   | 无     |
| ++   |                | >>=  | 截裁                | un+  | 无             | \|\| | 无     |
| --   |                | &=   | 截裁                | un-  | 溢出,包裹,截裁 | ?:   | 无     |
| =    |                | \|=  | 截裁                | <    | 无             |      |        |
| +=   |                | <<   | 溢出,包裹,截裁      | >    | 无             |      |        |

### 数据类型

#### 基础数据类型

**注意：以下是典型的数据位长和范围。编译器可能使用不同的数据位长和范围。请参考具体的参考手册。**

在标准头文件`limits.h` 和 `float.h`中说明了基础数据的长度。`float，double和long double`的范围就是在[IEEE 754](https://zh.wikipedia.org/wiki/IEEE_754)标准中提及的典型数据。

| 关键字               | 位长(字节)                                                   | 范围                                                         | 格式化字符串   |
| -------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | -------------- |
| `char`               | 1 bytes                                                      | -128..127（或0..255，与体系结构相关）                        | %c             |
| `unsigned char`      | 1bytes                                                       | 0..255                                                       | %c, %hhu       |
| `signed char`        | 1bytes                                                       | -128..127                                                    | %c, %hhd, %hhi |
| `int`                | 2bytes(16位系统) 或 4bytes                                   | -32768..32767 或 -2147483648..2147483647                     | %i, %d         |
| `unsigned int`       | 2bytes 或  4 bytes                                           | 0..65535 或 0..4294967295                                    | %u             |
| `signed int`         | 2bytes 或 4bytes                                             | -32768..32767 或 -2147483648..2147483647                     | %i, %d         |
| `short int`          | 2bytes                                                       | -32768..32767                                                | %hi, %hd       |
| `unsigned short`     | 2 bytes                                                      | 0..65535                                                     | %hu            |
| `signed short`       | 2bytes                                                       | -32768..32767                                                | %hi, %hd       |
| `long int`           | 4bytes 或 8bytes[[6\]](https://zh.wikipedia.org/wiki/C%E8%AF%AD%E8%A8%80#cite_note-6) | -2147483648..2147483647 或 -9223372036854775808..9223372036854775807 | %li, %ld       |
| `unsigned long`      | 4bytes 或 8 bytes                                            | 0..4294967295 或 0..18446744073709551615                     | %lu            |
| `signed long`        | 4 bytes或 8bytes                                             | -2147483648..2147483647 或 -9223372036854775808..9223372036854775807 | %li, %ld       |
| `long long`          | 8bytes                                                       | -9223372036854775808..9223372036854775807                    | %lli, %lld     |
| `unsigned long long` | 8bytes                                                       | 0..18446744073709551615                                      | %llu           |
| `float`              | 4bytes                                                       | 2.939x10−38..3.403x10+38 (7 sf)                              | %f, %e, %g     |
| `double`             | 8bytes                                                       | 5.563x10−309..1.798x10+308 (15 sf)                           | %lf, %e, %g    |
| `long double`        | 10bytes或 16bytes                                            | 7.065x10-9865..1.415x109864 (18 sf或33 sf)                   | %Lf, %Le, %Lg  |

#### 结构数据类型

结构数据类型允许构造由多个基础数据类型组合而成的复杂结构，结构数据类型为面向对象的蓝本。以下的结构数据类型通过指针实现了二叉树结构：

```c
1 typedef struct Bintree {
2     int data;
3     struct bintree *lchild; // left child of the node
4     struct bintree *rchild; // right child of the node
5 } bintree; // 自定义 bintree 类型
```

为结构数据类型定义变量时通常会用到动态内存分配：

```c
1 #define mktree() (bintree *)malloc(sizeof(bintree)) // 分配该结构所需的内存单元数量
2 bintree *tree;
3 tree = mktree(); // 分配到 tree 指针
4 tree->data = 1;
5 tree->lchild = mktree();
6 ...
```

由于C语言不具备自动垃圾收集（Garbage Collection）功能，使用完毕后调用`free(treePtr)`来释放之前通过`malloc(size)`分配的内存。详见以下指针章节。

### 数组

如果一个变量名后面跟着一个有数字的中括弧，这个声明就是[数组](https://zh.wikipedia.org/wiki/%E9%99%A3%E5%88%97)声明。字符串也是一种数组，它们以ASCII的NUL作为数组的结束。要特别注意的是，方括内的索引值是从**0**算起的。

例如：

```c
int myvector [100]；/* 從myvector[0]至[99]共100個元素 */
char mystring [80]；
// 声明时初始化
float mymatrix [3] [2] = {2.0 , 10.0, 20.0, 123.0, 1.0, 1.0};
int notfull [3][3] = {{1},{1,2,3},{4,5}};
// 数组套数组
char lexicon [10000] [300]；/* 共一萬個最大長度為300的字元陣列。*/
int a[3][4]；
```

上面最后一个例子创建了一个数组，但也可以把它看成是一个多维数组。注意数组的下标从0开始。这个数组的结构如下：

| a\[0][0]     | **a\[0][1]** | **a\[0][2]** | **a\[0][3]** |
| ------------ | ------------ | ------------ | ------------ |
| **a\[1][0]** | **a\[1][1]** | **a\[1][2]** | **a\[1][3]** |
| **a\[2][0]** | **a\[2][1]** | **a\[2][2]** | **a\[2][3]** |

**例子中notfull创建了一个3*3的二维数组，初始化时有些元素并未赋值。如下：**

```c
1  ?  ?
1  2  3
4  5  ?
```

**根据C标准的规定，在存在初始化列表时，如果初始化列表中未提供对所有元素的初始化，则剩余元素会被默认初始化，并使用与静态变量相同的初始化规则。**

#### **指针**

****如果一个变量声明时在前面使用 * 号，表明这是个指针型变量。换句话说，该变量存储一个地址，而 *（此处特指单目运算符 \*，下同。C语言中另有双目运算符 * 表示乘） 则是取内容操作符，意思是取这个内存地址里存储的内容。把这两点结合在一起，可将 `int *a;`看作是 “*a 解得的内容类型为 int”，对更复杂的声明也如此。指针是 C 语言区别于其他同时代高级语言的主要特征之一。**

指针不仅可以是变量的地址，还可以是数组、数组元素、函数的地址。通过指针作为形式参数可以在函数的调用过程得到一个以上的返回值（不同于`return z`这样的仅能得到一个返回值。

指针是一把双刃剑，许多操作可以通过指针自然的表达，但是不正确的或者过分的使用指针又会给程序带来大量潜在的错误。

**例如：**

```c
int *pi;     // 指向整型数据的指针 pi
int * api[3];// 由指向整型数据的指针构成的数组，长度为 3
char ** argv;// 指向一个字符指针的指针
struct { int member; } stinst,
  * pst = & stinst;
// pst是一个指向一个匿名结构体的指针
```

**储存在指针中的地址所指向的数值在程序中可以由 * 读取。例如，在第一个例子中， `*pi` 是一个整型数据。这叫做引用一个指针。**

**另一个运算符 `&`，叫做取地址运算符，它将返回一个变量、数组或函数的存储地址。因此，下面的例子：**

```c
int i, *pi; /* int and pointer to int */
pi = &i;
```

**`i` 和 `*pi` 在程序中可以相互替换使用，直到 `pi` 被改变成指向另一个变量的地址。**

**当指针指向结构体时，可以使用运算符 -> 代替 *和. 的作用，如 `(*p).m` 与 `p->m` 等效。**

#### **字符串**

**C语言的字符串其实就是char型数组，所以使用字符串并不需要引用库。然而C标准库确实包含了用于对字符串进行操作的函数，使得它们看起来就像字符串而不是数组。使用这些函数需要引用[头文件](https://zh.wikipedia.org/wiki/%E6%A8%99%E9%A0%AD%E6%AA%94)`string.h`。**

### **文件输入／输出**

**在C语言中，输入和输出是经由标准库中的一组函数来实现的。在ANSI/ISO C中，这些函数被定义在头文件`stdio.h`中。**

#### **标准输入／输出**

**有三个标准输入／输出是标准I/O库预先定义的：``**



- **stdin *标准输入*stdout *标准输出***

- **`stderr *输入输出错误*`**

**下面的这个例子显示了一个过滤程序（filter program）是怎样构成的。**

```c
#include <stdio.h>

int main(int argc, const char * argv[])
{
    char c;
    while ((c=getchar())!=EOF)
        putchar(c);
    perror("getchar() got EOF");
    return -1;
}
```

### **函数**

C语言的基本结构单位是函数。系统首先调用 [main函数（主函数）](https://zh.wikipedia.org/wiki/%E4%B8%BB%E5%87%BD%E5%BC%8F#C/C++)，通过函数的嵌套调用，再调用其他函数。函数可以是系统自带的函数，也可以是用户定义的函数。C语言中，不允许函数嵌套定义。

## **内存管理**

C语言的特色之一是：程序员必须亲自处理内存的分配细节。

C语言使用栈（Stack）来保存函数返回地址／栈帧基址、完成函数的参数传递和函数局部变量的存储。 如果程序需要在运行的过程中动态分配内存，可以利用[堆](https://zh.wikipedia.org/wiki/%E5%A0%86)（Heap）来实现。

基本上C程序的元素存储在内存的时候有3种分配策略：

- **静态分配**

如果一个变量声明为[全局变量](https://zh.wikipedia.org/wiki/%E5%85%A8%E5%B1%80%E5%8F%98%E9%87%8F)或者是函数的[静态变量](https://zh.wikipedia.org/wiki/%E9%9D%99%E6%80%81%E5%8F%98%E9%87%8F)，这个变量的存储将使用静态分配方式。静态分配的内存一般会被编译器放在[数据段](https://zh.wikipedia.org/wiki/%E6%95%B0%E6%8D%AE%E6%AE%B5)或[代码段](https://zh.wikipedia.org/wiki/%E4%BB%A3%E7%A0%81%E6%AE%B5)来存储，具体取决于实现。这样做的前提是，在编译时就必须确定变量的大小。 以IA32的x86平台及gcc编译器为例，全局及静态变量放在数据段的低端；全局及静态常量放在代码段的高端。

- **自动分配**

函数的自动局部变量应该随着函数的返回会自动释放（失效），这个要求在一般的体系中都是利用栈（Stack）来满足的。相比于静态分配，这时候，就不必绝对要求这个变量在编译时就必须确定变量的大小，运行时才决定也不迟，但是C89仍然要求在编译时就要确定，而C99放松了这个限制。但无论是C89还是C99，都不允许一个已经分配的自动变量运行时改变大小。

所以说C函数永远不应该返回一个局部变量的地址。

要指出的是，自动分配也属于动态分配，甚至可以用alloca函数来像分配堆（Heap）一样进行分配，而且释放是自动的。

- **动态分配**

还有一种更加特殊的情况，变量的大小在运行时有可能改变，或者虽然单个变量大小不变，变量的数目却有很大弹性，不能静态分配或者自动分配，这时候可以使用[堆](https://zh.wikipedia.org/wiki/%E5%A0%86)（Heap）来满足要求。ANSI C定义的堆操作函数是malloc、calloc、realloc和free。

使用[堆](https://zh.wikipedia.org/wiki/%E5%A0%86)（Heap）内存将带来额外的开销和风险。

## **安全问题**

C语言的特色之一是：语言不负责内存边界检查。

## **库**

主条目：[C 标准库](https://zh.wikipedia.org/wiki/C_%E6%A8%99%E6%BA%96%E5%87%BD%E5%BC%8F%E5%BA%AB)

C语言的标准文档要求了一个平台移植C语言的时候至少要实现的一些功能和封装的集合，称为“标准库”，标准库的声明头部通过[预处理器](https://zh.wikipedia.org/wiki/%E9%A2%84%E5%A4%84%E7%90%86%E5%99%A8)命令#include进行引用。

在C89标准中：

| 文件       | 简介说明                                                     |
| ---------- | ------------------------------------------------------------ |
| <assert.h> | 断言相关                                                     |
| <ctype.h>  | 字符类型判断                                                 |
| <errno.h>  | 标准报错机制                                                 |
| <float.h>  | 浮点运算                                                     |
| <limits.h> | 各种体系结构限制                                             |
| <locale.h> | 本地化接口                                                   |
| <math.h>   | 数学函数                                                     |
| <setjmp.h> | 跨函数跳转                                                   |
| <signal.h> | 信号（类似[UNIX](https://zh.wikipedia.org/wiki/UNIX)的[信号](https://zh.wikipedia.org/wiki/%E4%BF%A1%E5%8F%B7_(Unix))定义，但是差很远） |
| <stdarg.h> | 可变参处理                                                   |
| <stddef.h> | 一些标准宏定义                                               |
| <stdio.h>  | 标准I/O库                                                    |
| <stdlib.h> | 标准工具库函数                                               |
| <string.h> | ASCIIZ字符串及任意内存处理函数                               |
| <time.h>   | 时间相关                                                     |

在94年的修正版中

- <iso646.h>
- <wchar.h>
- <wctype.h>

在C99中增加了六个库

- <complex.h>
- <fenv.h>
- <inttypes.h>
- <stdbool.h>
- <stdint.h>
- <tgmath.h>

以上是C语言的标准。各个系统各自又对C库函数进行的各种扩充，就浩如烟海了。如[POSIX C](https://zh.wikipedia.org/w/index.php?title=POSIX_C&action=edit&redlink=1)、[GNU C](https://zh.wikipedia.org/wiki/GNU_C)等。

## **工具软件**

工具软件可以帮助程序设计者避免一些程序中潜藏或容易出现的问题，例如常会造成程序未预期动作或是运行期错误的代码。

许多语言都有自动源代码检查及审计工具，C语言也有类似工具，像是[Lint](https://zh.wikipedia.org/wiki/Lint)。可以在程序刚写好时用Lint找出可能有问题的程序，通过Lint后再用C编译器进行编译，许多编译器也可以设置是否要针对一些可能有问题的代码提出警告。[MISRA C](https://zh.wikipedia.org/wiki/MISRA_C)是一套针对[嵌入式系统](https://zh.wikipedia.org/wiki/%E5%B5%8C%E5%85%A5%E5%BC%8F%E7%B3%BB%E7%BB%9F)的法则，可主要也是避免一些可能有问题的代码。

也有一些编译器、程序库或操作系统可以处理一些非标准C语言的功能，例如边界值检查、[缓存溢出](https://zh.wikipedia.org/wiki/%E7%BC%93%E5%AD%98%E6%BA%A2%E5%87%BA)侦测、[序列化](https://zh.wikipedia.org/wiki/%E5%BA%8F%E5%88%97%E5%8C%96)及[自动垃圾回收](https://zh.wikipedia.org/wiki/%E5%9E%83%E5%9C%BE%E5%9B%9E%E6%94%B6_(%E8%A8%88%E7%AE%97%E6%A9%9F%E7%A7%91%E5%AD%B8))功能。

使用像[Valgrind](https://zh.wikipedia.org/wiki/Valgrind)或[IBM Rational Purify](https://zh.wikipedia.org/w/index.php?title=IBM_Rational_Purify&action=edit&redlink=1)等软件工具，或者链接有特别[malloc](https://zh.wikipedia.org/w/index.php?title=Malloc&action=edit&redlink=1)函数的程序库，有助于找出一些运行期存储器使用的问题。

## **保留关键字**

**以下是C语言的保留关键字：**

| **`char`**     | **`short`**    | **`int`**     | **`unsigned`** |
| -------------- | -------------- | ------------- | -------------- |
| **`long`**     | **`float`**    | **`double`**  | **`struct`**   |
| **`union`**    | **`void`**     | **`enum`**    | **`signed`**   |
| **`const`**    | **`volatile`** | **`typedef`** | **`auto`**     |
| **`register`** | **`static`**   | **`extern`**  | **`break`**    |
| **`case`**     | **`continue`** | **`default`** | **`do`**       |
| **`else`**     | **`for`**      | **`goto`**    | **`if`**       |
| **`return`**   | **`switch`**   | **`while`**   | **`sizeof`**   |

### **C99新增关键字**

| **`_Bool`** | **`_Complex`** | **`_Imaginary`** | **`inline`** | **`restrict`** |
| ----------- | -------------- | ---------------- | ------------ | -------------- |
|             |                |                  |              |                |

### **C11新增关键字**

| **`_Alignas`**       | **`_Alignof`**      | **`_Atomic`** | **`_Generic`** | **`_Noreturn`** |
| -------------------- | ------------------- | ------------- | -------------- | --------------- |
| **`_Static_assert`** | **`_Thread_local`** |               |                |                 |

## **经典错误**

“void main()”的用法并不是任何标准制定的。 C语言标准语法是“int main()”，任何实现都必须支持`int main(void) { /* ... */ }`和`int main(int argc, char* argv[]) { /* ... */ }。`

 在 C++ 标准中，main的标准类型应是int，否则类型是由实现定义的。任何实现都必须支持`int main() { /* ... */ }`和`int main(int argc, char* argv[]) { /* ... */ }`。