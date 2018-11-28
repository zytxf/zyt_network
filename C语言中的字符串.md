# C语言中的字符串 



## 简介

C风格的字符串其实就是特殊的 char 数组。特殊在于，数组中至少有一个 '\0' (其ASCII码值为0)空字符元素来作为字符串结束的标志。否则，这个数组只能看做是字符数组，而不能看做是字符串。C处理字符串的标准库string.h，以及其他的字符串处理函数，都建立在这种约定上，所以如果不满足这种约定，则它们不能正确工作。


例如 "C Language"是一个字符串常量，或者叫字符串字面值。它有9个英文字母和1个空格，但它占用11个字节，因为编译器自动在它末尾添加'\0'作为字符串结束标志。也就是说不管是程序员,还是编译器,都遵守这样一个规则:C语言字符串以'\0'结尾。

| C    |      | L    | a    | n    | g    | u    | a    | g    | e    | \0   |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
|      |      |      |      |      |      |      |      |      |      |      |

 

下面通过例子说明'\0'对字符串的重要意义以及字符串和字符数组的差别。



```
char str1[] = {'h' , 'e' , 'l' , 'l' , 'o' , '\0'} ;    //字符串"hello"
char str2[] = {'h' , 'e' , 'l' , 'l' , 'o'} ;       //不是字符串，而是字符数组


/*
字符串"he" ，因为 '\0' 是字符串结束的标志。第一个'\0'后的字符将被忽略(虽然它们的确存储在内存中,占用这个数组的空间)。
sizeof(str3)  返回整个数组的大小 6，而strlen(str3) 返回的是字符串的字符数，他遇见 '\0'就结束计数了，因此返回的是 2。
*/
char str3[] = {'h' , 'e' , '\0' , 'l' , 'o' , '\0'} ; 
   



/*上面的方法都没有指定字符数组的大小，而是让编译器去完成计算。也可以显示指定数组的大小，但是必须确保数组能保存所有字符（包括末尾的'\0'）
*/
char str5[2] = { 'h' , 'e' };  // 错误，没有给'\0'提供数组空间
char str6[3] = { 'h' , 'e' ,'\0'};//OK 
/*C允许使用另一种便捷的方式初始化一个字符串*/ 

char str2 [] = "hello" ; /*与下面一种等价，编译器自动将双引号后面追加一个'\0'，然后将双引号中的每个字符赋值给数组的元素。*/ 

char str1[] = {'h' , 'e' , 'l' , 'l' , 'o' , '\0'} ;
```



 

## 空字符串

空字符串的类型是char[1]，如 

```
char empty_str1[1] = "";     类型是:const char[1]
char empty_str2[1] = {'\0'}  类型是:char[1]
```

 

## 字符串字面值

直接书写的，用双引号表示的就是字符串字面值。形如 "hello" 这样的叫做字符串字面值，或者字符串文字常量。它是字符串，但与普通的数组存储的字符串相比有一些其他的特性。 

ANSI C声明：修改一个字符串字面值的后果是未定义的，因此现在的编译器都不允许程序员修改字符串字面值的内容。像下面的代码是不允许的，即便编译通过，也会发生运行时错误。



```
#include<stdio.h>
int main(int argc, char *argv[])
{
    char *msg = "hello";
    msg[0] = 'g';   // 不允许。不能通过msg指针去修改字符串，只能读它。
}
```



 

因此，程序员自己可以把字符串字面值当做是const数组看待，这样就避免让自己写出错误的代码。

```
"hello"  //类型是 const char[6]
""       //类型是 const char[1]
const char* p = "ddd";
```

 

ANSI C这样做的一个好处是：程序中使用相同内容的字符串字面值的可能会共享同一个字符串内存数据实体，以避免内存的浪费。 

下面两处使用了相同的字符串字面值，好的编译器会仅仅存储一份 "hello"实体在内存中，而指针s 和 msg指向相同的字符串去使用他们。 



```
#include<stdio.h>
char* foo()
{
    char *s = "hello";      //一
    printf("foo函数中字符串的地址是%p\n",s);  
}
int main(int argc, char *argv[])
{
    char *msg = "hello";    //二
    printf("main函数中字符串的地址是%p\n",msg);
    
    foo();
}
```



![img](https://images2017.cnblogs.com/blog/858860/201712/858860-20171217165405014-1486269361.png)

 

其次，当字符串字面值作为右值使用时，那么表达式的值就是这个字符串字面值存储在内存中的起始地址，即第一个字符在内存中的地址。

```
char* p = "hello";
putchar(*p);   //打印出：h
```

 

再者，字符串字面值是存放在内存的静态存储区的，静态区的数据从程序载入内存运行，到程序结束都一直存在，因此，像下面的代码是合法有效的：即从函数返回一个字符串字面值(实质上是这个字符串在内存中的地址)，并不会因为函数执行完而将字符串字面值析构掉。 



```
#include<stdio.h>
char* foo()
{
    return "hello world";
}
int main(int argc, char *argv[])
{
    char *msg = foo();
    printf(msg);
}
```



## 标准库中的字符串函数

以下的字符串函数大多都定义在string.h中。给出的实现源代码从linux2.6内核中提取，仅供参考。

 

| size_t **strlen**( const char *str ); 一种可能的实现方式： size_t strlen(const char * s){    const char *sc;     for (sc = s; *sc != '\0'; ++sc)        /* nothing */;    return sc - s;} | 返回一个字符串的长度。字符串str必须以'\0'结尾。              |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| char* strcpy( char* dest, const char* src ); 一种可能的实现方式： char * strcpy(char * dest,const char *src){    char *tmp = dest;     while ((*dest++ = *src++) != '\0')        /* nothing */;    return tmp;} | 将src的字符（ 包括末尾的\0'）拷贝到des中去。 dest字符串必须保证至少有 strlen(src) +1 的空间。  如果des的容量不足以容纳src的全部字符和末尾的\0,则结果未定义。 如果des 和src内存发生重叠,则结果未定义 |
| char *strncpy( char *dest, const char *src, std::size_t count ); char * strncpy(char * dest,const char *src,size_t count){    char *tmp = dest;     while (count) {        if ((*tmp = *src) != 0) src++;        tmp++;        count--;    }    return dest;} | 将字符串src中最多count个字符拷贝到 dest中。返回字符串dest。  理想的情况是： count==strlen(src) +1 1、如果count 小于 src的长度 +1，则dest将不会以'\0'结尾。2、如果 count 大于 src 的长度 +1 ，则在完全拷贝src之后，继续在dest后面追加'\0'，直到总共拷贝 count 个 字符到 dest dest 和 src的内存块不能重叠，否则结果未定义。 |
| int **strcmp**( const char *lhs, const char *rhs ); int strcmp(const char * cs,const char * ct){    register signed char __res;     while (1) {        if ((__res = *cs - *ct++) != 0 \|\| !*cs++)            break;    }     return __res;} | 按照字典顺序（ASCII表）比较2个字符串。总之，如果第一个字符串“大于”第二个字符串，则返回一个正数，如果第一个字符串“小于”第二个字符串，则返回一个负数，如果2个字符串一样，则返回0。 2个字符串必须i是以'\0'结尾的。 如果2个字符串完全相同，则返回0。如果在循环比较的某个索引位置上，前者lhs的字符“小于”rhs的字符，则返回一个负数。如果在循环比较的某个索引位置上，前者lhs的字符“大于”rhs的字符，则返回一个正数。 |
| int **strncmp**( const char *lhs, const char *rhs, size_t count ); | 和strcmp一样，只不过它最多比较count个连续的字符。2个字符串必须i是以'\0'结尾的。count如果过大，使得strncmp在比较过程中访问了超出字符串所在的数组的空间则是未定义的。 |
| char *strcat( char *dest, const char *src ); 一种可能的实现方式：  char * strcat(char * dest, const char * src){    char *tmp = dest;     while (*dest)        dest++;      //退出循环后，dest指向目标字符串末尾的'\0'     while ((*dest++ = *src++) != '\0')  //拷贝，直到遇到src中的'\0'        ;     return tmp;} | 将字符串src追加到字符串dest的末尾，返回新的字符串dest的指针 。2个字符串必须i是以'\0'结尾的。 用src[0]替换dest中的原来的用于指示字符串末尾的'\0'，且最终dest依然是以'\0'结尾。 如果dest所在的数组无法容纳原来dest中的字符个数+src的字符个数+1，则结果未定义。 如果dest和是src内存重叠，则结果未定义。   ![img](https://images2017.cnblogs.com/blog/858860/201712/858860-20171217165842983-1522897770.png) |
| char ***strncat**( char *dest, const char *src, size_t count );  char * strncat(char *dest, const char *src, size_t count){    char *tmp = dest;     if (count) {        while (*dest)  //先找到dest的末尾            dest++;            while ((*dest++ = *src++) != 0) {            if (--count == 0) {                *dest = '\0';                break;            }        }    }     return tmp;} | 将src中至多count个字符串追加到dest的末尾。并保证函数调用结束后，dest总是以'\0'结尾的。 2个字符串必须i是以'\0'结尾的。如果dest和是src内存重叠，则结果未定义。 必须保证dest有足够的空间来容纳实际追加的字符个数和一个用于存储'\0'的空间。 如果strlen(src)>count，则实际只追加src中的前count个字符。如果strlen(src)<count，则实际将src全部追加到dest的末尾。 |
| schar ***strchr**( const char *str, int ch );                | 在字符串str中查找字符ch第一次出现的位置，并返回它在字符串中的指针。如果找不到则返回NULL。字符串str必须以'\0'结尾。 由于'\0'也是字符串的一部分，因此这个字符串也可以用于查找'\0'。 |
| char ***strrchr**( const char *str, int ch );                | 在字符串str中查找字符ch最后一次出现的位置（也可以理解为反向查找），并返回它在字符串中的指针。如果找不到则返回NULL。 字符串str必须以'\0'结尾。由于'\0'也是字符串的一部分，因此这个字符串也可以用于查找'\0'。 |
| char* **strpbrk**( const char* dest, const char* breakset ); | 在字符串dest中查找breakset字符集合中任何一个字符第一次出现的位置，返回它在dest中的指针，如果找不到则返回NULL。dest和breakset都必须以'\0'结尾。但是'\0'不算待查找的字符。breakset包含所有待查找的字符，但是其末尾的'\0'不计入其中。      char str[] = "a dog";    char*p = strpbrk(str,"dxv");  // p指向字符串"a dog"中的'd'。        char str1[] = "I have a pen";    char*p1 = strpbrk(str1,"bpn");  // p1指向字符串"I have a pen"中的'p'。 |
| char ***strstr**( const char* str, const char* substr );     | 在字符串str中查找子串substr。返回substr在str中第一次出现的位置（指针）。如果找不到，则返回NULL。str和substr都必须以'\0'结尾，但'\0'计入其中，不进行比较。 如果substr是一个空字符串，则直接返回str。 |
| size_t **strspn**( const char *dest, const char *src );      | 从dest字符串的起始处开始查找同时也出现在src中的字符 连续出现的次数。 dest和src都必须以'\0'结尾，但是'\0'不算待查找的字符。 从dest的开始依次扫描每个字符，如果当前这个字符ch同时也在src中，则计数器cnt加1，一旦发现当前字符ch不在src中，则统计结束，返回cnt的值。 #include <stdio.h>#include <stdlib.h>#include <string.h> size_t str_initnum_cnt(const char*str){    return strspn(str,"0123456789");} int main(void){    char str[] = "8923891a#$bjsd~!#";    printf("字符串str从最开始处连续的数字的个数是:%u\n",str_num_cnt(str));    //字符串str从最开始处连续的数字的个数是:7         char str1[] = "89d23891a#$bjsd~!#";    printf("字符串str1从最开始处连续的数字的个数是:%u\n",str_num_cnt(str1));    //字符串str1从最开始处连续的数字的个数是:2        return EXIT_SUCCESS;} |
| size_t **strcspn**( const char *dest, const char *src );     | 这个函数的和strspn的统计方法相反。他统计的是dest开始处连续的不出现在src中的字符个数。从dest的开始依次扫描每个字符，如果当前这个字符ch不出现在src中，则计数器cnt加1，一旦发现当前字符ch存在于在src中，则统计结束，返回cnt的值。 dest和src都必须以'\0'结尾，但是'\0'不算待查找的字符。 |
| void ***memset**( void *dest, int ch, size_t count );        | 用ch代表的字节数据（ch在函数内部会被看做是unsigned char）填充dest起始的前count个字节的字节数组内容。返回dest指针。 常用这个函数重置一个数组数据为指定的值。 dest不能是NULL，否则结果未定义。count不能过大，以让这个函数 访问了超过dest的数组空间，否则结果未定义。 |
| void* **memcpy**( void *dest, const void *src, size_t count ); | 将src代表的字节数组的前count个字节拷贝到dest代表的字节数组中。返回dest指针。 memcpy函数内部，src和dest都被看做是unsigned char数组。 memcpy是面向内存原始数据的拷贝，无论dest和src是什么类型的数组，他总是将他们解释为byte array。他通常比strcpy高效，因为memcpy可以利用机器提供的专门用于拷贝内存的指令来完成，而strcpy总是从字符串的开始挨个扫描字符来完成拷贝的。所以，拷贝字符串就使用strcpy，而想要拷贝一般的内存数据，则使用memcpy。  dest和src都不能是NULL。dest和src不能重叠。count不能太大而让函数访问超过这2个数组的空间。 |
| void* **memmove**( void* dest, const void* src, size_t count ); | 将src代表的字节数组的前count个字节拷贝到dest代表的字节数组中。返回dest指针。 memcpy函数内部，src和dest都被看做是unsigned char数组。 memmove和memcpy的效果类似，只不过memmove允许dest和src内存重叠。这种情况下，memmove的工作机制就好比先把src拷贝到一个临时数组tmp（tmp不和dest重叠）中，然后从tmp中拷贝数据到dest中。memmove通常比memcpy慢，但是当dest和src内存重叠就不得不用它。 dest和src都不能是NULL。count不能太大而让函数访问超过这2个数组的空间。 |
| int **memcmp**( const void* lhs, const void* rhs, size_t count ); | 比较字节数组lhs和字节数组rhs的前count个字节，在memcmp内部，2个数组都被解释为unsigned char数组，因此比较是按照字典顺序（ASCII表）比较的。 dest和src都不能是NULL。count不能太大而让函数访问超过这2个数组的空间。 |
| void* **memchr**( const void* ptr, int ch, size_t count );   | 在字节数组ptr的前count字节中查找字节数据ch第一次出现的位置，并返回他的指针。找不到则返回NULL。 函数内部，ptr被解释为unsigned char数组，而ch被解释为unsigned char类型。 ptr不能是NULL。count不能太大而让函数访问超过这个数组的空间。 |
| int **sprintf**( char *buffer, const char *format, ... );此函数定义在stdio.h中。 | 将格式化形成的字符串写入到字符串buffer中。因为写入的是字符串，因此'\0'也会被强制写入到buffer中。所以必须保证buffer的空间足够容纳所有的字符和最后的'\0'  返回实际总共写入的字符个数（但不包括末尾的'\0'） |
| int **sscanf**( const char  *buffer, const char  *format, ... );此函数定义在stdio.h中。 | 从字符串buffer中读取格式化的数据。buffer必须以'\0'结尾。此时buffer的末尾'\0'就好比是文件源的EOF。返回成功读取的数据的个数。 |
| int    atoi( const char *str ); 解析出一个int        long  atol( const char *str );解析出一个long        long long atoll( const char *str );    (C99) 解析出一个long long 这些函数定义在stdlib.h中 | 从一个字符串中解析出一个整数。解析时，字符串开头的空白符（如空格，tab，换行等）都会被忽略，直到扫描到第一个非空白符，则开始正真的解析工作。开始解析后，一旦遇到非法字符，则结束解析，返回数字。 如果目标字符串str根本无法解析出整数，则返回0。如果字符串str代表的整数超出了返回类型的范围，则返回的结果是未定义的。 #include <stdio.h> #include <stdlib.h>   int main(void) {     printf("%i\n", atoi(" -123junk"));    //-123     printf("%i\n", atoi("0"));              //0     printf("%i\n", atoi("junk"));         //根本无法解析，返回0     printf("%i\n", atoi("2147483648"));   //字符串代表的整数超出了int范围，返回一个期望之外的整数：-2147483648 } |