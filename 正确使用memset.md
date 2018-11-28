正确使用memset

函数实现：

```c
void* memset(void* s, int c, size_t n)
{
    unsigned char* p = (unsigned char*) s;


    while (n > 0) {
    *p++ = (unsigned char) c;
    --n;
    }

    return s;
}
```




1. **memset是以字节为单位，初始化内存块。**
  当初始化一个字节单位的数组时，可以用memset把每个数组单元初始化成任何你想要的值，比如，

  ```c
  char data[10];  
  memset(data, 1, sizeof(data));    // right  
  memset(data, 0, sizeof(data));    // right  
  ```

  而在初始化其他基础类型时，则需要注意，比如,

  而在初始化其他基础类型时，则需要注意，比如,

  ```c
  int data[10];  
  memset(data, 0, sizeof(data));    // right  
  memset(data, -1, sizeof(data));    // right  
  memset(data, 1, sizeof(data));    // wrong, data[x] would be 0x0101 instead of 1  
  ```


此处memset(data, 1, sizeof(data));为什么data[x]中的每一个元素都是0x0101?   从函数实现中我们可以得到答案。

2. **当结构体类型中包含指针时，在使用memset初始化时需要小心。**
  比如如下代码中，

  ```c++
  struct Parameters {  
         int x;  
         int* p_x;  
  };  
  Parameters par;  
  par.p_x = new int[10];  
  memset(&par, 0, sizeof(par));  
  ```


当memset初始化时，并不会初始化p_x指向的int数组单元的值，而会把已经分配过内存的p_x指针本身设置为0，造成内存泄漏。同理，对std::vector等数据类型，显而易见也是不应该使用memset来初始化的。