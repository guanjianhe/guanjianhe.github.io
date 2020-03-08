---
layout: post
title: 文件数据转对应的数组
tag: C
---

有时候需要把文件二进制数据转成对应的数组，以下程序能实现功能：

```c
#include <stdio.h>
#include <string.h>

/*
 * feof():当设置了与流关联的文件结束标识符时，该函数返回一个非零值，否则返回零。
 * C 库函数 int getc(FILE *stream) 从指定的流 stream 获取下一个字符（一个无符号字符），并把位置标识符往前移动。
 * C 库函数 int fprintf(FILE *stream, const char *format, ...) 发送格式化输出到流 stream 中。
 */

int main(void)
{
    unsigned char tmp;
    unsigned long count = 0;
    FILE *infp;
    FILE *outfp;
    infp = fopen("in.txt", "rb");
    outfp = fopen("out.txt", "wb");
    fprintf(outfp, "%s", "const char arr[]={");
    /* 要先读取再判断，不然会多出一个字节 */
    tmp = getc(infp);

    while (!feof(infp))
    {
        fprintf(outfp, "0x%02X,", tmp);
        count++;
        tmp = getc(infp);
    }

    fprintf(outfp, "%s", "};");
    fprintf(outfp, "\n\n//一共有%u个字节\n", count);
    printf("一共有%u个字节\n", count);
    fclose(infp);
    fclose(outfp);
    return (0);
}
```

---

转载请注明：[guanjianhe的博客](https://guanjianhe.github.io/) » [文件数据转对应的数组](https://guanjianhe.github.io/2020/03/filedata2arr/)
