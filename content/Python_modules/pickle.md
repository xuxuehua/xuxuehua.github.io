---
title: "pickle"
date: 2018-08-24 12:39
---

[TOC]

# pickle

仅支持Python所有的数据类型



## dump 

`pickle.dump(info, f)`

等同于

`f.write(pickle.dumps(info))`







## dumps 序列化

变成二进制





## load

`pickle.load(f)`

等同于

`pickle.loads(f.read())`



## loads 反序列化





