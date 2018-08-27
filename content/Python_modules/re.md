---
title: "re"
date: 2018-08-26 19:30
---

[TOC]

# Regular Expression

用于匹配字符串



## 常用符号

```
'.'     默认匹配除\n之外的任意一个字符，若指定flag DOTALL,则匹配任意字符，包括换行
'^'     匹配字符开头，若指定flags MULTILINE,这种也可以匹配上(r"^a","\nabc\neee",flags=re.MULTILINE)
'$'     匹配字符结尾，或e.search("foo$","bfoo\nsdfsf",flags=re.MULTILINE).group()也可以
'*'     匹配*号前的字符0次或多次，re.findall("ab*","cabb3abcbbac")  结果为['abb', 'ab', 'a']
'+'     匹配前一个字符1次或多次，re.findall("ab+","ab+cd+abb+bba") 结果['ab', 'abb']
'?'     匹配前一个字符1次或0次
'{m}'   匹配前一个字符m次
'{n,m}' 匹配前一个字符n到m次，re.findall("ab{1,3}","abb abc abbcbbb") 结果'abb', 'ab', 'abb']
'|'     匹配|左或|右的字符，re.search("abc|ABC","ABCBabcCD").group() 结果'ABC'
'(...)' 分组匹配，re.search("(abc){2}a(123|456)c", "abcabca456c").group() 结果 abcabca456c
 
 
'\A'    只从字符开头匹配，re.search("\Aabc","alexabc") 是匹配不到的
'\Z'    匹配字符结尾，同$
'\d'    匹配数字0-9
'\D'    匹配非数字
'\w'    匹配[A-Za-z0-9]
'\W'    匹配非[A-Za-z0-9]
's'     匹配空白字符、\t、\n、\r , re.search("\s+","ab\tc1\n3").group() 结果 '\t'
 
'(?P<name>...)' 分组匹配 re.search("(?P<province>[0-9]{4})(?P<city>[0-9]{2})(?P<birthday>[0-9]{4})","371481199306143242").groupdict("city") 结果{'province': '3714', 'city': '81', 'birthday': '1993'}
```



## 常用方法

### re.match 

从头开始匹配

```
In [45]: ret = re.match('^Rick', "Rickwithyou")

In [46]: ret.group()
Out[46]: 'Rick'
```



### re.search 

匹配包含

```
In [47]: re.search("\D+", '1234$@a')
Out[47]: <_sre.SRE_Match object; span=(4, 7), match='$@a'>

In [48]: re.search('(?P<id>[0-9]+)(?P<name>[a-zA-Z]+)', 'abcd1234EFGh!@#$').group('id')
Out[48]: '1234'
```



### re.findall 

把所有匹配到的字符放到以列表中的元素返回



### re.split

以匹配到的字符当做列表分隔符

```
In [49]: re.split('[0-9]', 'abcd1234EFGH!@#$')
Out[49]: ['abcd', '', '', '', 'EFGH!@#$']
```





### re.sub      

匹配字符并替换

```
In [52]: re.sub('[0-9]+', '|', 'abcd1234EFGH!@#$')
Out[52]: 'abcd|EFGH!@#$'

In [55]: re.sub('[0-9]+', '|', 'abcd1234EFGH!@#$1111', count=1)
Out[55]: 'abcd|EFGH!@#$1111'
```





## 匹配模式

### re.I(re.IGNORECASE)

忽略大小写（括号内是完整写法，下同）



### M(MULTILINE)

多行模式，改变'^'和'$'的行为（参见上图）



### S(DOTALL)

点任意匹配模式，改变'.'的行为





## 反斜杠

反斜杠的困扰 与大多数编程语言相同，正则表达式里使用"\"作为转义字符，这就可能造成反斜杠困扰。假如你需要匹配文本中的字符"\"，那么使用编程语言表示的正则表达式里将需要4个反斜杠"\\\\"：前两个和后两个分别用于在编程语言里转义成反斜杠，转换成两个反斜杠后再在正则表达式里转义成一个反斜杠。Python里的原生字符串很好地解决了这个问题，这个例子中的正则表达式可以使用r"\\"表示。同样，匹配一个数字的"\\d"可以写成r"\d"。有了原生字符串，你再也不用担心是不是漏写了反斜杠，写出来的表达式也更直观。 

