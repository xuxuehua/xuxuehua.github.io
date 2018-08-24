---
title: "sys"
date: 2018-07-02 18:05
---

[TOC]



# sys 模块



## argv

```
import sys
 
print(sys.argv)
 
 
#输出
$ python test.py helo world
>>>
['test.py', 'helo', 'world']  #把执行脚本时传递的参数获取到了
```



## path

打印python全局环境变量

第三方库在site-packages目录里

```
import sys

print(sys.path)
>>>
['/Users/xhxu/python/python3/test', '/Users/xhxu/python/python3', '/Users/xhxu/.pyenv/versions/3.5.3/lib/python35.zip', '/Users/xhxu/.pyenv/versions/3.5.3/lib/python3.5', '/Users/xhxu/.pyenv/versions/3.5.3/lib/python3.5/plat-darwin', '/Users/xhxu/.pyenv/versions/3.5.3/lib/python3.5/lib-dynload', '/Users/xhxu/.pyenv/versions/env3.5.3/lib/python3.5/site-packages', '/Users/xhxu/.pyenv/versions/env3.5.3/lib/python3.5/site-packages/setuptools-28.8.0-py3.5.egg', '/Users/xhxu/.pyenv/versions/env3.5.3/lib/python3.5/site-packages/pip-9.0.1-py3.5.egg']
```



### append

添加环境变量

```
sys.path.append(BASE_DIR)
```

