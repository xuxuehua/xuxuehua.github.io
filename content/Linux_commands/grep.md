---
title: "grep"
date: 2018-08-28 09:46
---

[TOC]

# grep 

根据模式搜索问吧，并将符合模式的文本行显示到屏幕上



## 正则表达式

行首不为#的行作为输出

```
grep '^[^#]'  files
```





## -i 不敏感大小写

-i     ignore 大小写 The enforces case insensitive match in both pattern and input files

​    

## --colour 加上颜色

 \- - colour 加上颜色



## -v 显示没有被匹配

-v     显示没有被模式匹配到的行 



## -o 显示被匹配

-o     只显示被匹配到的字符串



抓取mac 网卡地址

```
ifconfig en0 | grep -o "inet .*" | cut -d ' ' -f 2
```



抓取Linux 网卡地址

```
ifconfig eth0 | grep -o "inet addr:[0-9.]{1.}"
```







## -E 扩展正则表达式

-E     extended regexp

等同于egrep 命令



## -A -B -C 匹配行的信息

-A +num     显示被匹配之后，和后面number 行的信息

-B +num     显示被匹配之后，和前面number 行的信息

-C +num     显示被匹配之后，和前后number行的信息



## -q 静默模式

-q     quiet, Do not write anything to standard output.



## -f 从文件匹配

-f FILE       This obtains a patterns from a file, one per line 



## -e 多字符匹配

-e PATTERN      This specifies multiple search pattern 



## -r 目录遍历，不含软连接

-r      Reads all the files in a directory recursively, excluding resolving of symbolic links unless explicitly specified as an input file 



## -R  目录遍历，含软连接

-R      This reads all the files in a directory recursively and resolving symbolic if any



## -a 处理二进制文件

-a      This processes binary file as a text file



## -n 行号

-n      This prefixes each matched line along with a line number



## -s 过滤错误信息

-s     Don’t print error messages



## -c 匹配行数

-c           This prints the count  of matching lines of each input file

