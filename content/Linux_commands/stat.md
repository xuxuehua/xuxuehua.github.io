---
title: "stat"
date: 2018-10-10 11:14
---


[TOC]

# stat

stat查一个文件或目录的三个时间



## Synopsis 语法

```
stat [OPTION]... FILE...
```



## Options







## 查看文件

```
# stat 1.py
  File: ‘1.py’
  Size: 278       	Blocks: 8          IO Block: 4096   regular file
Device: fd01h/64769d	Inode: 646849      Links: 1
Access: (0644/-rw-r--r--)  Uid: (    0/    root)   Gid: (    0/    root)
Context: unconfined_u:object_r:admin_home_t:s0
Access: 2018-03-04 13:00:19.291533019 +0000
Modify: 2018-03-04 13:00:17.066513273 +0000
Change: 2018-03-04 13:00:17.066513273 +0000
 Birth: -
```

> Access访问时间 atime=access time
>
> Modify修改时间 mtime=modifiy time
>
> Change状态改动时间 ctime=change time





以简明格式显示`<file>`的状态信息。

```
stat -t <file>
```





## 查看目录

```
# stat test
  File: ‘test’
  Size: 4096      	Blocks: 8          IO Block: 4096   directory
Device: fd01h/64769d	Inode: 646725      Links: 8
Access: (0755/drwxr-xr-x)  Uid: (    0/    root)   Gid: (    0/    root)
Context: unconfined_u:object_r:admin_home_t:s0
Access: 2018-10-10 03:33:22.943072238 +0000
Modify: 2018-09-21 16:12:05.137138213 +0000
Change: 2018-09-21 16:12:05.137138213 +0000
 Birth: -
```

> Access访问时间 atime=access time
>
> Modify修改时间 mtime=modifiy time
>
> Change状态改动时间 ctime=change time



## 查看系统

显示`<file>`所在文件系统的状态信息。

```
stat -f <file>
```

