---
title: "file_operation 文件操作"
date: 2018-08-19 11:30
---

[TOC]



# 文件操作

## 标准模式

### r

只读模式（默认） 文件必须存在

```

```



### w

只写文件，若文件存在则文件长度清为0，即该文件内容会消失。若文件不存在则建立该文件。

```

```



### a

以附加的方式打开只写文件。若文件不存在，则会建立该文件，如果文件存在，写入的数据会被加到文件尾，即文件原先的内容会被保留。

```

```





## 模式

### r+

打开可读写的文件，该文件必须存在

```

```



### w+

可读写文件，若文件存在则文件长度清为零，即该文件内容会消失。若文件不存在则建立该文件。

```

```



### a+ 

以附加方式打开可读写的文件。若文件不存在，则会建立该文件，如果文件存在，写入的数据会被加到文件尾后，即文件原先的内容会被保留。

```

```





##  U模式

"U"表示在读取时，可以将 \r \n \r\n自动转换成 \n （与 r 或 r+ 模式同使用）

### rU

```

```



### r+U

```

```





## 二进制模式

表示处理二进制文件（如：FTP发送上传ISO镜像文件，linux可忽略，windows处理二进制文件时需标注）

### rb

读取二进制文件

```

```



### wb

```

```



### ab

```

```







### tell()

打印光标位置

```

```





## 文件对象的方法

### readline()

读取每行的内容

```

```



### readlines()

读取整个文件，生成列表

```

```



### f.read()

文件内容替换

```
for line in fileinput.input('filepath', inplace=1):
    line = line.replace('oldtext', 'newtext')
    print(line)
```

修改某行

```
with open('foo.txt', 'r++') as f:
    old = f.read() 
    f.seek(0)
    f.write('new line\n' + old)
line before
```



### write

写入
```
f.write('I like apple!\n')      # 将'I like apple'写入文件并换行
```



### close

关闭
```
f.close()  #关闭文件
```




## with语句

为了避免打开文件后忘记关闭，可以通过管理上下文，即：

```
with open('log','r') as f:
	pass
```

如此方式，当with代码块执行完毕时，内部会自动关闭并释放文件资源。

在Python 2.7 后，with又支持同时对多个文件的上下文进行管理，即：

```
with open('log1') as obj1, open('log2') as obj2:
	pass
```











## 查找



### seek()

```

```



### flush()

刷新缓冲

```
f = open('test.txt', 'w')
f.write('hello1\n')
f.flush()
f.write('hello2\n')
```



实时生成进度条 

```
import sys, time

for i in range(20):
    sys.stdout.write('#');
    sys.stdout.flush()
    time.sleep(0.2)
```






