---
layout: post
title: JDK安装注意事项
tag: 工具软件
---

- 不安装`Public JRE`
- 不推荐安装在有空格的路径下，例如装在`C:\Java\jdk\1.8.0`
- 添加环境变量，建议加在用户变量里面。路径值为（以上面路径为例）`C:\Java\jdk\1.8.0\bin`
- 如果JDK版本是在$1.5$以上，则`CLASSPATH`环境变量**没有必要加**
- 测试是否成功
  - 在命令行中运行 `java`或`javac`命令

---
转载请注明：[guanjianhe的博客](https://guanjianhe.github.io/) » [JDK安装注意事项](https://guanjianhe.github.io/2020/03/JDKInstall/)
