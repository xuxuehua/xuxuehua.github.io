---
title: "json"
date: 2018-08-24 12:31
---



[TOC]

# json



## dump

```
import json

person = [
    {
        'name': 'Rick',
        'age': 30
    },
    {
        'country': 'China',
        'Language': 'Python'
    }
]
json_str = json.dumps(person)

with open('person.json', 'w') as f:
    json.dump(person, f)
```



### 中文编码处理

```
import json

person = [
    {
        'name': 'Rick Xu',
        'age': 30
    },
    {
        'country': '中国',
        'Language': 'Python'
    }
]
json_str = json.dumps(person)

with open('person.json', 'w', encoding='utf-8') as f:
    json.dump(person, f, ensure_ascii=False)
```



## dumps 序列化

```
import json

person = [
    {
        'name': 'Rick',
        'age': 30
    },
    {
        'country': 'China',
        'Language': 'Python'
    }
]

print(json.dumps(person))

>>>
[{"age": 30, "name": "Rick"}, {"Language": "Python", "country": "China"}]
```



## load

```
import json

with open('person.json', 'r', encoding='utf-8') as f:
    person = json.load(f)
    print(person)
    
>>>
[{'name': 'Rick Xu', 'age': 30}, {'country': '中国', 'Language': 'Python'}]
```

## loads 反序列化

```
import json

json_str = '[{"age": 30, "name": "Rick"}, {"Language": "Python", "country": "China"}]'

print(json.loads(json_str))

>>>
[{'name': 'Rick', 'age': 30}, {'Language': 'Python', 'country': 'China'}]
```

