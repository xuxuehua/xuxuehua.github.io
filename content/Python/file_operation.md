---
title: "file_operation 文件操作"
date: 2018-08-19 11:30
---

[TOC]



# 文件操作

## 

## 文件处理

---

### readline()

* f.realine() 读取每行的内容

---

### f.write() f.read()

* 文件内容替换

```python
for line in fileinput.input('filepath', inplace=1):
    line = line.replace('oldtext', 'newtext')
    print(line)
```

---

* 修改某行

```python
with open('foo.txt', 'r++') as f:
    old = f.read() 
    f.seek(0)
    f.write('new line\n' + old)
line before
```

---