---
layout: post
title: 十六进制的字符转成对应的十六进制数
tag: C
---

有时候得到的文件数据是十六进制字符形式，这时候需要把字符形式的十六进制转成对应的十六进制数，代码如下：

```c
#include <stdio.h>
#include <string.h>

//十六进制字符转二进制

/* C 库函数 int feof(FILE *stream) 测试给定流 stream 的文件结束标识符。 */

int main(void)
{
    unsigned int tmp;
    FILE *infp;
    FILE *outfp;
    /* 打开文件in.txt，只读，该文件必须存在 */
    infp = fopen("in.txt", "r");
    /* 打开文件out.txt，写二进制 */
    outfp = fopen("out.txt", "wb");
    /* 这边要先读再判断，不然会多出一个字节 */
    /* 从文件指针info读取一个十六进制数给tmp变量 */
    fscanf(infp, "%X", &tmp);

    /* 判断是否到了文件末尾，是的话函数feof返回1 */
    while (!feof(infp))
    {
        /* 把变量tmp的数据写入到文件里去 */
        putc(tmp, outfp);
        fscanf(infp, "%X", &tmp);
    }

    /* 关闭两文件 */
    fclose(infp);
    fclose(outfp);
    return (0);
}
```

---

转载请注明：[guanjianhe的博客](https://guanjianhe.github.io/) » [十六进制的字符转成对应的十六进制数](https://guanjianhe.github.io/2020/03/char2binary/)
