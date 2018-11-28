在一个多任务OS中，每个进程都运行在它自己的内存沙箱中。这个沙箱就是虚拟地址空间，在32位下就是一块容量为4GB的内存地址。内核将这些虚拟地址按页表（page table）映射为物理内存，并交由CPU访问。每个进程有自己的页表集，但有一点要注意。虚拟地址一旦被启用，就会应用到机器上所有运行的程序上，也包括内核自己。因此虚拟地址空间必须为内核预留一部分（否则就没办法和内核交互了）：

[![img](http://static.duartes.org/img/blogPosts/kernelUserMemorySplit.png)](http://static.duartes.org/img/blogPosts/kernelUserMemorySplit.png%5C%22+target=%5C%22_blank%5C%22+target=%5C%22_blank%5C%22+target=%5C%22_blank%5C%22+target=%5C%22_blank)

给内核预留那么多空间，并不是说内核真的使用了那么多物理内存，只是内核可以这部分虚拟地址自由的映射到某片物理内存上（而不用和其它虚拟地址遵循相同的规则）。内核空间在页表中被标记为专属的特权代码（ring 2或更低），用户态的程序访问它时就会产生页错误（page fault）。Linux的内核空间在所有进程中都映射到相同的物理内存上。内核代码和数据总是可寻址的（总是可以找到的），任意时刻都可处理中断和系统调用。作为对比，当进程切换时，用户态地址空间的映射就会发生改变：

[![img](http://static.duartes.org/img/blogPosts/virtualMemoryInProcessSwitch.png)](http://static.duartes.org/img/blogPosts/virtualMemoryInProcessSwitch.png%5C%22+target=%5C%22_blank%5C%22+target=%5C%22_blank%5C%22+target=%5C%22_blank%5C%22+target=%5C%22_blank)

蓝色区域表示映射到物理内存的虚拟地址空间，而白色区域则表示未映射的空间。在这个例子中，Firefox惊人的内存需求让它使用的虚拟地址远远超过了其自身的地址空间。内存地址空间是按堆、栈这样的内存段进行管理的。要记住内存段就是简单的一个内存地址范围，而且与Intel风格的段没有任何关系。下面是一个Linux进程的标准内存段布局：

[![img](http://static.duartes.org/img/blogPosts/linuxFlexibleAddressSpaceLayout.png)](http://static.duartes.org/img/blogPosts/linuxFlexibleAddressSpaceLayout.png%5C%22+target=%5C%22_blank%5C%22+target=%5C%22_blank%5C%22+target=%5C%22_blank%5C%22+target=%5C%22_blank)

如果计算过程轻松愉快、准确无误，那么上图显示的内存段起始虚拟地址在几乎每个进程中都是一样的。这导致了远程利用安全漏洞变得非常容易。一次漏洞探测通常需要引用内存的绝对地址：一个栈上地址，一个库函数的地址，等等。远程攻击者只能盲目的选择这样的地址，指望地址空间都是一样的。如果这种情况真发生了，用户就悲剧了。因此地址空间随机化变的很流行。Linux会给栈、mmap段、和堆的起始地址一个随机偏离。不幸的是，32位地址空间实在是太紧凑了，只给随机化很小的空间，妨碍了它的效果。

进程地址空间的最上面是栈，栈里保存了局部变量，以及大多数编程语言中的函数参数。一次方法或函数调用就会向栈增加一个栈帧（stack frame）。当函数返回时栈帧就会被销毁。因为数据遵循严格的“后入先出”顺序，这种简单的设计意味着不需要复杂的数据结构就能追踪到栈的上下文——栈顶的一个指针就搞定。栈的Push和pop操作因此变得快速且确定。同时，栈区域的稳定重用也有助于栈内存在CPU缓存中保持活跃，加快了访问速度。进程中的每个线程都有自己的栈。

如果推入栈的数据过多，可能会耗尽栈映射的地址区域。这会导致一次页错误，Linux将其处理为一次expand_stack()调用，实际上是调用acct_stack_growth()检查当前是否可以增加栈大小。如果栈大小小于RLIMIT_STACK（通常8MB）就可以继续增长，程序会正常继续，不会察觉到什么。这是栈大小调整的默认处理。但是，如果栈大小达到了上限，就会发生栈溢出，程序会接到一次段错误（Segmentation Fault）。相对的，当栈变小时，不会缩减栈大小。这就像联邦预算，只增不减（笑）。

在访问到未映射内存区（上图中的白色部分）时，只有动态栈增长可能是合法的。其它方式访问到未映射区域时都会引发一次页错误，进而导致段错误。一些映射区是只读的，对它们的写操作也会导致段错误。

在栈的下面就是mmap段，内核在这里将文件内容映射为内存。任何应用都可以通过Linux下的mmap()或Windows下的CreateFileMapping()/MapViewOfFile()申请一片mmap区域。mmap是一种高效便捷的文件I/O方式，被用于加载动态链接库。我们同样可以创建一块与文件没有关系的mmap区，用来存放程序的数据。在Linux中，如果你通过malloc()申请一大块内存，glibc会返回一块匿名的mmap内存块，而不是用堆内存。“大”意思是比MMAP_THRESHOLD大，通常是128KB，可以调用mallopt()修改。

接下来我们开始说堆。堆提供了运行时的内存分配，这点和栈类似；数据的生命期与执行分配的函数生命期不一致，这点与栈不同。大多数语言都提供了堆的管理。因此满足内存请求需要语言的运行环境和内核协作完成。C语言中分配堆的接口是malloc()族函数，而在有gc的语言（例如C#）其接口则是关键字new。

如果堆内存足够，语言运行时环境就可以处理内存请求，不需要内核介入，或者可以通过brk()系统调用去增大堆内存。堆的管理很复杂，在面对程序杂乱的分配方式时，需要使用在速度和内存使用率上努力做平衡的微妙算法。满足一次堆请求的时间差异可以非常大。实时系统需要特殊用途的分配器来处理这个问题。使用时堆也会变的很碎片化，见下图：

[![img](http://static.duartes.org/img/blogPosts/fragmentedHeap.png)](http://static.duartes.org/img/blogPosts/fragmentedHeap.png%5C%22+target=%5C%22_blank%5C%22+target=%5C%22_blank%5C%22+target=%5C%22_blank%5C%22+target=%5C%22_blank)



最后，我们看一下最下面的内存段：BSS、data、代码段。在C里面BSS和data段都是存储静态变量（全局）的数据。区别是BSS段存储没有初始化的静态变量，即在代码中没有初始值的静态变量。BSS区是匿名的：不映射自任何文件。如果代码中有static int cntActiveUsers;，那么cntActiveUsers就在BSS段。

而data段则存放代码中显示初始化了的静态变量。这块内存区不是匿名的，它映射自程序镜像中包含对应静态变量的文件。这种映射是私有映射，即内存中的变化不会反映到文件中。如果不这样，改变一个全局变量的值就会修改你磁盘中的镜像文件，这就太荒谬了！

下图中的data示例有些取巧，使用了一个指针。指针gonzo的内容——4字节的地址——就存在data段。而它指向的字符串则不是，字符串存放在text段。text段是只读的，存放字符串字面值等不会执行的代码。text段也会映射程序文件，但对它的写操作会引发段错误。这会避免一些指针bug，但不像第一时间在C代码中避免指针bug那么有效。下图显示了这些段和示例变量：

[![img](http://static.duartes.org/img/blogPosts/mappingBinaryImage.png)](http://static.duartes.org/img/blogPosts/mappingBinaryImage.png%5C%22+target=%5C%22_blank%5C%22+target=%5C%22_blank%5C%22+target=%5C%22_blank%5C%22+target=%5C%22_blank)



你可以读/proc/pid_of_process/maps来检查一个Linux进程的内存区。一个内存段可能包含多个内存区。例如，每个mmap映射的文件都会在mmap段有一个单独的内存区，而动态库还会有在BSS和data段的内存区。下篇文章会剖析“内存区”意味着什么。有时人们也会用“data段”代指整个data + BSS + 堆。

你可以用[nm](http://manpages.ubuntu.com/manpages/intrepid/en/man1/nm.1.html%5C%22+.=%5C%22outline:+none;+text-decoration:+none;+color:+rgb%2861,+129,+238%29;+border-bottom-width:+1px;+border-bottom-.:+dashed;%5C%22+target=%5C%22_blank%5C%22+target=%5C%22_blank%5C%22+target=%5C%22_blank%5C%22+target=%5C%22_blank%5C%22+target=%5C%22_blank%5C%22+target=%5C%22_blank)和[objdump](http://manpages.ubuntu.com/manpages/intrepid/en/man1/objdump.1.html%5C%22+.=%5C%22outline:+none;+text-decoration:+none;+color:+rgb%2861,+129,+238%29;+border-bottom-width:+1px;+border-bottom-.:+dashed;%5C%22+target=%5C%22_blank%5C%22+target=%5C%22_blank%5C%22+target=%5C%22_blank%5C%22+target=%5C%22_blank%5C%22+target=%5C%22_blank%5C%22+target=%5C%22_blank)命令检查镜像文件中的符号、它们的地址、所属的段，等等。最后，上面说的虚拟地址布局是Linux的“灵活”布局，也是近年来Linux的默认布局。它假设RLIMIT_STACK有值。否则Linux会回到下图的“经典”布局：

[![img](https://edu.unigress.com/data/attachment/album/201704/10/090207kdjr6rzr3rclgddr.png)](http://bbs.unigress.com/data/attachment/album/201704/10/090207kdjr6rzr3rclgddr.png%5C%22+target=%5C%22_blank%5C%22+target=%5C%22_blank)

the end！