# atol()函数

```c
头文件：#include <stdlib.h>

函数原型：
long atol(const char * str);

将字符串转换成长整型数(long)
```



ANSI C 规范定义了 [stof()](http://c.biancheng.net/cpp/html/124.html)、[atoi()](http://c.biancheng.net/cpp/html/125.html)、[atol()](http://c.biancheng.net/cpp/html/126.html)、[strtod()](http://c.biancheng.net/cpp/html/128.html)、[strtol()](http://c.biancheng.net/cpp/html/129.html)、[strtoul()](http://c.biancheng.net/cpp/html/130.html) 共6个可以将字符串转换为数字的函数

# read()函数

头文件：#include <unistd.h>

```c
read(0, buf, 0x20u);

read函数原型：ssize_t read(int fd, void * buf, size_t count);
```

功能：**read()会把参数fd 所指的文件传送count 个字节到buf  指针所指的内存中. 若参数count 为0, 则read()不会有作用并返回0. 返回值为实际读取到的字节数, 如果返回0,  表示已到达文件尾或是无可读取的数据,此外文件读写位置会随读取到的字节移动.**

fd为0时，就是从输入端读取内容。


---


# fopen()函数
**FILE *fopen(const char *filename, const char *mode)**

**使用指定的mode打开filename所指向的文件**



---


# fgets()函数
**char *fgets(char *str, int n, FILE *stream)**

从指定的流 stream 读取一行，并把它存储在 **str** 所指向的字符串内。当读取 **(n-1)** 个字符时，或者读取到换行符时，或者到达文件末尾时，它会停止，具体视情况而定。

* **str** -- 这是指向一个字符数组的指针，该数组存储了要读取的字符串。
* **n** -- 这是要读取的最大字符数（包括最后的空字符）。通常是使用以 str 传递的数组长度。
* **stream** -- 这是指向 FILE 对象的指针，该 FILE 对象标识了要从中读取字符的流。

---


# fread()函数
函数原型：size_t fread(void *ptr, size_t size, size_t nmemb, FILE *stream)

函数功能：从给定流 **stream** 读取数据到 **ptr** 所指向的数组中。

参数

* **ptr**  -- 这是指向带有最小尺寸 *size*nmemb* 字节的内存块的指针。
* **size** -- 这是要读取的每个元素的大小，以字节为单位。
* **nmemb**  -- 这是元素的个数，每个元素的大小为 size 字节。
* **stream** -- 这是指向 FILE 对象的指针，该 FILE 对象指定了一个输入流。

---


# **write()函数**
ssize_t write(int fd, const void *buf, size_t nbyte);

将buf所指内存区nbyte个字节的内容送到参数fd所指的文件内。


---


# memchr()函数
函数原型：void *memchr(void *s, char ch, unsigned n); 

函数功能：从s所指内存区域的前n个[字节](https://baike.baidu.com/item/%E5%AD%97%E8%8A%82/1096318)查找[字符](https://baike.baidu.com/item/%E5%AD%97%E7%AC%A6/4768913)ch。


---


# memcpy函数
函数原型：void *memcpy(void *dest, const void *src, size_t n);

函数功能：从src的开始位置拷贝n个字节的数据到dest。


---


# memset()函数
函数原型：void *memset(void *s, int ch, size_t n);

函数功能：将s中当前位置后面的n个字节 （typedef unsigned int size_t ）用 ch 替换并返回 s 。


---

# mmap()函数

Linux 内存映射函数

```c
头文件 <sys/mman.h> 
函数原型 
void* mmap(void* start,size_t length,int prot,int flags,int fd,off_t offset); 
int munmap(void* start,size_t length);

返回值：
    成功执行时，mmap()返回被映射区的指针，munmap()返回0。失败时，mmap()返回MAP_FAILED[其值为(void *)-1]，munmap返回-1。
```

**mmap用于把文件映射到内存空间中，简单说mmap就是把一个文件的内容在内存里面做一个映像。**

参数：

```cpp
start：要映射到的内存区域的起始地址，通常都是用NULL（NULL即为0）。NULL表示由内核来指定该内存地址
```



```cpp
length：要映射的内存区域的大小
```



```cpp
prot：期望的内存保护标志，不能与文件的打开模式冲突。是以下的某个值，可以通过or运算合理地组合在一起
PROT_EXEC //页内容可以被执行
PROT_READ  //页内容可以被读取
PROT_WRITE //页可以被写入
PROT_NONE  //页不可访问
```



```c
flags：指定映射对象的类型，映射选项和映射页是否可以共享。它的值可以是一个或者多个以下位的组合体
MAP_FIXED ：使用指定的映射起始地址，如果由start和len参数指定的内存区重叠于现存的映射空间，重叠部分将会被丢弃。如果指定的起始地址不可用，操作将会失败。并且起始地址必须落在页的边界上。
MAP_SHARED ：对映射区域的写入数据会复制回文件内, 而且允许其他映射该文件的进程共享。
MAP_PRIVATE ：建立一个写入时拷贝的私有映射。内存区域的写入不会影响到原文件。这个标志和以上标志是互斥的，只能使用其中一个。
MAP_DENYWRITE ：这个标志被忽略。
MAP_EXECUTABLE ：同上
MAP_NORESERVE ：不要为这个映射保留交换空间。当交换空间被保留，对映射区修改的可能会得到保证。当交换空间不被保留，同时内存不足，对映射区的修改会引起段违例信号。
MAP_LOCKED ：锁定映射区的页面，从而防止页面被交换出内存。
MAP_GROWSDOWN ：用于堆栈，告诉内核VM系统，映射区可以向下扩展。
MAP_ANONYMOUS ：匿名映射，映射区不与任何文件关联。
MAP_ANON ：MAP_ANONYMOUS的别称，不再被使用。
MAP_FILE ：兼容标志，被忽略。
MAP_32BIT ：将映射区放在进程地址空间的低2GB，MAP_FIXED指定时会被忽略。当前这个标志只在x86-64平台上得到支持。
MAP_POPULATE ：为文件映射通过预读的方式准备好页表。随后对映射区的访问不会被页违例阻塞。
MAP_NONBLOCK ：仅和MAP_POPULATE一起使用时才有意义。不执行预读，只为已存在于内存中的页面建立页表入口。
```



```cpp
fd：文件描述符（由open函数返回）
```



```cpp
offset：表示被映射对象（即文件）从那里开始对映，通常都是用0。 该值应该为大小为PAGE_SIZE的整数倍
```



# open()函数

```c
头文件：
#include <sys/types.h>
#include <sys/stat.h>    
#include <fcntl.h>
    
函数原型    
int open(const char * pathname, int flags);
int open(const char * pathname, int flags, mode_t mode);

```

参数 
pathname 指向欲打开的文件路径字符串;
flags 
所能使用的旗标:
O_RDONLY 以只读方式打开文件
O_WRONLY 以只写方式打开文件
O_RDWR 以可读写方式打开文件. 上述三种旗标是互斥的, 也就是不可同时使用, 但可与下列的旗标利用OR(|)运算符组合.
O_CREAT 若欲打开的文件不存在则自动建立该文件.
O_EXCL 如果O_CREAT 也被设置, 此指令会去检查文件是否存在. 文件若不存在则建立该文件, 否则将导致打开文件错误. 此外, 若O_CREAT 与O_EXCL 同时设置, 并且欲打开的文件为符号连接, 则会打开文件失败.
O_NOCTTY 如果欲打开的文件为终端机设备时, 则不会将该终端机当成进程控制终端机.
O_TRUNC 若文件存在并且以可写的方式打开时, 此旗标会令文件长度清为0, 而原来存于该文件的资料也会消失.
O_APPEND 当读写文件时会从文件尾开始移动, 也就是所写入的数据会以附加的方式加入到文件后面.
O_NONBLOCK 以不可阻断的方式打开文件, 也就是无论有无数据读取或等待, 都会立即返回进程之中.
O_NDELAY 同O_NONBLOCK.
O_SYNC 以同步的方式打开文件.
O_NOFOLLOW 如果参数pathname 所指的文件为一符号连接, 则会令打开文件失败.
O_DIRECTORY 如果参数pathname 所指的文件并非为一目录, 则会令打开文件失败。注：此为Linux2. 2 以后特有的旗标, 以避免一些系统安全问题. 
    
mode 则有下列数种组合, 只有在建立新文件时才会生效, 此外真正建文件时的权限会受到umask 值所影响, 因此该文件权限应该为 (mode-umaks).
S_IRWXU00700 权限, 代表该文件所有者具有可读、可写及可执行的权限.
S_IRUSR 或S_IREAD, 00400 权限, 代表该文件所有者具有可读取的权限.
S_IWUSR 或S_IWRITE, 00200 权限, 代表该文件所有者具有可写入的权限.
S_IXUSR 或S_IEXEC, 00100 权限, 代表该文件所有者具有可执行的权限.
S_IRWXG 00070 权限, 代表该文件用户组具有可读、可写及可执行的权限.
S_IRGRP 00040 权限, 代表该文件用户组具有可读的权限.
S_IWGRP 00020 权限, 代表该文件用户组具有可写入的权限.
S_IXGRP 00010 权限, 代表该文件用户组具有可执行的权限.
S_IRWXO 00007 权限, 代表其他用户具有可读、可写及可执行的权限.
S_IROTH 00004 权限, 代表其他用户具有可读的权限
S_IWOTH 00002 权限, 代表其他用户具有可写入的权限.
S_IXOTH 00001 权限, 代表其他用户具有可执行的权限.
    
返回值：

若所有欲核查的权限都通过了检查则返回0 值, 表示成功, 只要有一个权限被禁止则返回-1.



---



# strcat()函数

函数原型：**char *strcat(char *dest, const char *src)**

函数功能：把 **src** 所指向的字符串追加到 **dest** 所指向的字符串的结尾。

返回值：该函数返回一个指向最终的目标字符串 dest 的指针。

---



# strdup()函数

函数原型：char *strdup(const char *s);

头文件：#include <string.h>

功能：将串拷贝到新建的位置处

返回值：一个新的指针，指针指向的内容和s一样

# strtol()函数

函数原型：long int strtol(const char *str, char **endptr, int base)

函数功能：把参数 **str** 所指向的字符串根据给定的 **base** 转换为一个长整数（类型为 long int 型），base 必须介于 2 和 36（包含）之间，或者是特殊值 0。

参数

* **str** -- 要转换为长整数的字符串。
* **endptr** -- 对类型为 char* 的对象的引用，其值由函数设置为 **str** 中数值后的下一个字符。
* **base** -- 基数，必须介于 2 和 36（包含）之间，或者是特殊值 0。

---


#strstr()函数

函数原型

```c
char *strstr(const char *haystack, const char *needle)
```

函数功能

`C 库函数 **char \*strstr(const char \*haystack, const char \*needle)** 在字符串 **haystack** 中查找第一次出现字符串 **needle** 的位置，不包含终止符 '\0'。`

参数

```
haystack -- 要被检索的 C 字符串。
needle -- 在 haystack 字符串内要搜索的小字符串。
```

返回值

`该函数返回在 haystack 中第一次出现 needle 字符串的位置，如果未找到则返回 null。`

# strcpy()函数
**函数原型：char *strcpy(char *dest, const char *src)**

函数功能：把 **src** 所指向的字符串复制到 **dest**。

---



# strcmp()函数
函数原型：int strcmp(const char* stri1，const char* str2);

参数 str1 和 str2 是参与比较的两个字符串。

函数功能：码依次比较 str1 和 str2 的每一个字符，直到出现不到的字符，或者到达字符串末尾（遇见`\0`）。

返回值：

*  如果返回值 < 0，则表示 str1 小于 str2。
*  如果返回值 > 0，则表示 str2 小于 str1。
*  如果返回值 = 0，则表示 str1 等于 str2。

---


# strncmp()函数
函数原型：**int strncmp(const char *str1, const char *str2, size_t n)**

函数功能：把 **str1** 和 **str2** 进行比较，最多比较前 **n** 个字节。

返回值：

* 按照`ASCII`值进行比较，`str1-str2`的数值就是返回值。
* 如果返回值 `<` 0，则表示 `str1` 小于 `str2`。
* 如果返回值 `>` 0，则表示 `str2` 小于 `str1`。
* 如果返回值 `=` 0，则表示 `str1` 等于 `str2`。



---


# sprintf()函数
函数原型：**int sprintf(char *str, const char *format, ...)**

函数功能：发送格式化输出到 **str** 所指向的字符串。

这个函数不输出，只是把format所指的字符串送到str所指的地方。里面可以有格式符，可以被后面的参数解析。



---


# getline()函数
函数原型：ssize_t getline(char **linepter,size_t *n,FILE *stream)

参数：   

lineptr：指向存放该行字符的指针，如果是NULL，则有系统帮助malloc，请在使用完成后free释放。   

n：如果是由系统malloc的指针，请填0   

stream：文件描述符   

函数功能：将stream所指的内容取一行到linepter中

返回值：

成功：返回读取的字节数。

失败：返回-1。   

​       

​    


---


# bzero()函数
函数原型：extern void bzero(void *s, int n)

头文件：<string.h>

功能：置字节字符串s的前n个字节为零且包括‘\0’

说明：无返回值


---



