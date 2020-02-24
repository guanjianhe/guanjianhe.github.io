---
layout: post
title: "C语言文件读写" 
description: "C语言文件读写函数总结"
tag: C 
---



# C语言文件读写

### 打开文件

`FILE *fopen(const char *filename, const char *mode)`

- **filename** -- 这是 C 字符串，包含了要打开的文件名称。

- **mode** -- 这是 C 字符串，包含了文件访问模式，模式如下:
  - "r"：打开一个文本文件，可以读取文件，该文件必须存在
  - "w"：打开一个文本文件，可以写入文件，如果文件不存在则创建，存在则覆盖
  - "a"：打开一个文本文件，可以写入文件，向已有文件的尾部追加内容，如果文件不存在则创建
  - "r+"：打开一个文本文件，可以读取和写入文件
  - "w+"：打开一个文本文件，可以读取和写入文件，如果文件不存在则创建，存在则覆盖
  - "a+"：打开一个文本文件，可以读取和写入，写入时向已有文件的尾部追加内容，如果文件不存在则创建
  - "rb"、"wb"、"ab"、"ab+"、"a+b"、"wb+"、"w+b"、"rb+"、"r+b"，与上面的模式相似，但使用二进制模式打开
  
- 返回值

  该函数返回一个 FILE 指针。否则返回 NULL

### 关闭文件

`int fclose(FILE *stream)`

- 参数

	**stream** -- 这是指向 FILE 对象的指针，该 FILE 对象指定了要被关闭的流。

- 返回值

  如果流成功关闭，则该方法返回零。如果失败，则返回 `EOF`。



### 读文件

`int fscanf(FILE *stream, const char *format, ...)`

- 返回值

  如果成功，该函数返回成功匹配和赋值的个数。如果到达文件末尾或发生读错误，则返回 `EOF`。



`int fgetc(FILE *stream)`

 - 返回值

   该函数以无符号 char 强制转换为 int 的形式返回读取的字符，如果到达文件末尾或发生读错误，则返回 `EOF`。



`char *fgets(char *str, int n, FILE *stream)`

- 返回值

  如果成功，该函数返回相同的 str 参数。如果到达文件末尾或者没有读取到任何字符，str 的内容保持不变，并返回一个空指针。如果发生错误，返回一个空指针。

  

`size_t fread(void *ptr, size_t size, size_t nmemb, FILE *stream)`

- 参数
  - **ptr** -- 这是指向带有最小尺寸 *size\*nmemb* 字节的内存块的指针。
  - **size** -- 这是要读取的每个元素的大小，以字节为单位。
  - **nmemb** -- 这是元素的个数，每个元素的大小为 size 字节。
  - **stream** -- 这是指向 FILE 对象的指针，该 FILE 对象指定了一个输入流。
- 返回值
  成功读取的元素总数会以 size_t 对象返回，size_t 对象是一个整型数据类型。如果总数与 nmemb 参数不同，则可能发生了一个错误或者到达了文件末尾。



### 写文件

`int fprintf(FILE *stream, const char *format, ...)`

- 返回值

  如果成功，则返回写入的字符总数，否则返回一个负数。

`int fputc(int char, FILE *stream)`

- 返回值

  如果没有发生错误，则返回被写入的字符。如果发生错误，则返回 `EOF`

`int fputs(const char *str, FILE *stream)`

- 返回值

  该函数返回一个非负值，如果发生错误则返回 `EOF`。



`size_t fwrite(const void *ptr, size_t size, size_t nmemb, FILE *stream)`

- 参数

  - **ptr** -- 这是指向要被写入的元素数组的指针。
  - **size** -- 这是要被写入的每个元素的大小，以字节为单位。
  - **nmemb** -- 这是元素的个数，每个元素的大小为 size 字节。
  - **stream** -- 这是指向 FILE 对象的指针，该 FILE 对象指定了一个输出流。

- 返回值

  如果成功，该函数返回一个 size_t 对象，表示元素的总数，该对象是一个整型数据类型。如果该数字与 nmemb 参数不同，则会显示一个错误。



### 读写位置相关

`int fseek(FILE *stream, long int offset, int whence)`

- 参数

  - **stream** -- 这是指向 FILE 对象的指针，该 FILE 对象标识了流。
  - **offset** -- 这是相对 whence 的偏移量，以字节为单位。
  - **whence** -- 这是表示开始添加偏移 offset 的位置。它一般指定为下列常量之一：

  | 常量     |        描述        |
  | :-------: | :----------------: |
  | SEEK_SET |     文件的开头     |
  | SEEK_CUR | 文件指针的当前位置 |
  | SEEK_END |     文件的末尾     |
  
- 返回值

  如果成功，则该函数返回零，否则返回非零值。



`void rewind(FILE *stream)`

- 功能描述：

  设置文件位置为给定流 **stream** 的文件的开头。



### 删除文件

`int remove(const char *filename)`

- 返回值

  如果成功，则返回零。如果错误，则返回 -1

### 修改文件名

`int rename(const char *old_filename, const char *new_filename)`

- 参数

  - **old_filename** -- 这是 C 字符串，包含了要被重命名/移动的文件名称。
  - **new_filename** -- 这是 C 字符串，包含了文件的新名称。

- 返回值

  如果成功，则返回零。如果错误，则返回 -1

### 判断文件是否结束

`int feof(FILE *stream)`

- 返回值

  当设置了与流关联的文件结束标识符时，该函数返回一个非零值，否则返回零。



### 重定向流

`FILE *freopen(const char *filename, const char *mode, FILE *stream)`

- 描述

  C 库函数 **FILE \*freopen(const char \*filename, const char \*mode, FILE \*stream)** 把一个新的文件名 **filename** 与给定的打开的流 **stream** 关联，同时关闭流中的旧文件。

- 参数

  - **filename** -- 这是 C 字符串，包含了要打开的文件名称。
  - **mode** -- 这是 C 字符串，包含了文件访问模式
  - **stream** -- 这是指向 FILE 对象的指针，该 FILE 对象标识了要被重新打开的流。

- 返回值

  如果文件成功打开，则函数返回一个指针，指向用于标识流的对象。否则，返回空指针。

- 示例：

  ```c
  #include <stdio.h>
  
  int main ()
  {
     FILE *fp;
  
     printf("该文本重定向到 stdout\n");
  
     fp = freopen("file.txt", "w+", stdout);
  
     printf("该文本重定向到 file.txt\n");
  
     fclose(fp);
     
     return(0);
  }
  ```
  
- 补充

  C 语言把所有的设备都当作文件。所以设备（比如显示器）被处理的方式与文件相同。以下三个文件会在程序执行时自动打开，以便访问键盘和屏幕。

  | 标准文件 | 文件指针 | 设备     |
  | :-------: | :-------: | :-------: |
  | 标准输入 | stdin    | 键盘     |
  | 标准输出 | stdout   | 屏幕     |
  | 标准错误 | stderr   | 您的屏幕 |

  文件指针是访问文件的方式，本节将讲解如何从屏幕读取值以及如何把结果输出到屏幕上。

  C 语言中的 I/O (输入/输出) 通常使用 `printf()` 和 `scanf()` 两个函数。

  `scanf()` 函数用于从标准输入（键盘）读取并格式化， `printf()` 函数发送格式化输出到标准输出（屏幕）。

  `stdout`和`stderr`的区别：`stdout`是行缓冲的，它的输出会放在一个buffer里面，只有到换行的时候，才会输出到屏幕。而`stderr`是无缓冲的，会直接输出
