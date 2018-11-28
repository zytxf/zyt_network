## c标准库中string.h里的常用函数用法	

 		

　　在我们平常写的c/c++程序，一些算法题中，我们常常会用到c标准库中string.h文件中的函数，这些函数主要用于处理内存，字符串相关操作，是很有用的工具函数。而且有些时候，在笔试或面试中也会出现让你来实现某个函数的情况（比如strcpy）。而且里面有些函数时间长不用就生疏了，本文就是要全面回顾这些函数。

#### **1. NULL**

NULL是一个宏，可以扩展为空指针常量。空指针常量是一个等于零的整数常量表达式，后者是如(void *)0一样的从0转换为空指针void *.*

*(A null-pointer constant is an integral constant expression that evaluates to zero (like `0` or `0L`), or the cast of such value to type `void*` (like `(void*)0`).)

一个空指针常量能够转换为任何指针类型，空指针变量的值表明该指针不指向任何对象。



#### 2. size_t

typedef unsigned int size_t;

size_t 是sizeof操作符的返回类型。



#### 3. 复制操作类函数

**void * memcpy ( void * destination, const void * source, size_t num );**

memcpy函数从source指向的地址处开始直接复制num字节的数据到由destination指向的内存块。该函数在source处不会检查其复制的数据是以空字符结束（null-terminated），memcpy仅仅正好复制num字节。为避免溢出，由source和destination指向的内存块大小都应该不小于num字节，且source与destinatin也不应该由重叠区，即这是需要由程序员来保证的（对于内存块有重叠的情况，memmove是一个更好的选择）。



**void * memmove ( void * destination, const void * source, size_t num );**

 memmove函数与memcpy的功能基本一致，只是memmove函数允许destination与source指向的内存块有重叠区，复制的过程可能是使用了一块中间缓存区，该缓存区没有覆盖source与destination的有效区，先把source中的num字节数据复制到该中间缓存区，然后再由该缓存区复制到destination处。



**char * strcpy ( char * destination, const char * source );**

strcpy函数复制由source指向的c字符串到destination指向的数组，该复制也会复制空字符结束符。为避免发生溢出，destinaton指向的数组大小应该能够放下由source指向的c字符串（包含空字符结束符），并且source与destination指向的内存区也不应该重叠。



**char * strncpy ( char * destination, const char * source, size_t num );**

strncpy与strcpy功能类似。strncpy函数复制由source指向的前num个字符至destination，如果source指向的c字符串（包含空字符结束符）的字符数小于num，那么除了把source指向的字符串复制到destination外，还会继续填充零直到destination处的字符书到达num个。

如果source指向的字符串字符数大于num，那么在destination出的字符串是不会在位段添加空字符结束符（'\0'）的。在这种情况下，不应该将destination视为一个c风格字符串（如果将其作为c字符串可能会导致溢出）。destination与source应当无重叠。

 

#### 4. 字符串连接函数

char * strcat ( char * destination, const char * source );

将source指向的字符串添加到destination字符串，destination字符串的空字符结束符被source字符串的第一个字符覆盖，两字符串连接得到的新的字符串的结尾会添加一个就空字符结束符。source和destination无重叠。



char * strncat ( char * destination, const char * source, size_t num );

将source字符串的前num个字符连接到destination然后再加一个空字符结束符。如果source指向的c字符串长度小于num,那么只复制source字符串从起始到空字符结束符。

 

#### 5. 比较函数

int memcmp ( const void * ptr1, const void * ptr2, size_t num );

memcmp函数比较由ptr1与ptr2指向的前num字节的内存块，如果这两块内存匹配返回零，否则返回非零值表示哪块内存大。注意，该函数不同于strcmp，在发现空字符结束符时比较不会停止。



int strcmp ( const char * str1, const char * str2 );

strcmp函数从第一个字符开始比较两个字符串，如果两字符相同，那么继续比较下一对字符，如果不同或遇到了空字符结束符，比较就会停止。

该函数的返回值是一个小于，或等于，或大于零的值，分别对应str1小于，或等于，或大于str2字符串。



int strncmp ( const char * str1, const char * str2, size_t num );

strncmp与strcmp类似，只不过strncmp函数是比较str1与str2的前num个字符的大小。

 

#### 6. 查询函数

const void * memchr ( const void * ptr, int value, size_t num );
​          void * memchr (  void * ptr, int value, size_t num );

在ptr指向前num个字节的内存块中查找value的第一次出现，并且返回该找到的值的指针。value和该内存块中的每个字节都被解释为unsigned char来比较。



const char * strchr ( const char * str, int character );
​      char * strchr (       char * str, int character );

strchr返回一个指针，指向character在str指向的字符串中第一次出现的位置，由于空字符结束符也是c风格字符串的一部分，因此为了取回str的结尾，'\0'也会被定位。



size_t strcspn ( const char * str1, const char * str2 );

扫描str1字符串来查找str2字符串中任一部分字符在str1中第一次出现的位置，函数返回在找到该位置之前扫描过的str1的字符数。该查找包含了空字符结束符，因此如果str2中没有字符出现在str1中，那么会返回str1的长度。



const char * strpbrk ( const char * str1, const char * str2 );
​      char * strpbrk (       char * str1, const char * str2 );

扫描str1字符串来查找str2字符串中任一部分字符在str1中第一次出现的位置并返回指针，如果没有匹配返回空指针。该函数的查找不包含空字符结束符，而是会遇到该字符时停止。



const char * strrchr ( const char * str, int character );
​      char * strrchr (       char * str, int character );

strrchr与strchr函数相反，返回指针指向character在str字符串中最后一次出现的位置。由于空字符结束符也是c风格字符串的一部分，因此为了取回str的结尾，'\0'也会被定位。



size_t strspn ( const char * str1, const char * str2 );

返回str1字符串中str2中字符出现的个数。该函数的查找不包含空字符结束符，而是会遇到该字符时停止。



const char * strstr ( const char * str1, const char * str2 );
​      char * strstr (       char * str1, const char * str2 );

strstr返回字符串str2在str1字符串中第一次出现的位置处的指针，或者返回空指针如果str2不是str1字符串的一部分。该函数的匹配过程不包含空字符结束符，而是会遇到该字符时停止。



char * strtok ( char * str, const char * delimiters );

对str字符串调用该函数会将str分割为tokens.各个token就是str被delimiters中的字符分割后得到的一个个连续字符序列。

第一次调用该函数时，str应该是一个c风格字符串。str的第一个字符被作为token扫描的起始位置。在随后的调用中，该函数期待一个空指针并且利用上一个token的结尾的下一个位置作为新的起始扫描位置。

为了判定一个token的起始与结束，该函数首先从第一个不包含在delimiters中的字符处（这也是一个token的开始初）开始扫描，然后接着从第一个包含在delimiters中的字符处（这也是一个token的结尾处）开始扫描。如果遇到空字符结束符就停止。

一个token的结尾会自动用一个空字符结束符替换，函数返回该token的起始字符指针。

一旦在该函数的调用中遇到了空字符结束符，那么所有的后续调用都会返回空指针。

 

#### 7.其他

void * memset ( void * ptr, int value, size_t num );

memset函数将ptr指向的前num字节的内存块设置为value（以unsigned char解释）值。

char * strerror ( int errnum );

strerror函数解释errnum的值，并产生一个字符串信息描述errno的值。该函数的返回值是一个指向静态分配的字符串的指针，程序不应该修改该字符串。后续的调用会覆盖掉字符串内容。strerror产生的error字符串可能在不同的系统和库实现中不同。

size_t strlen ( const char * str );

该函数返回c字符串的长度。c字符串的长度是由空字符结束符决定的，一个c字符串的长度是不包含空字符结束符的字符的个数。