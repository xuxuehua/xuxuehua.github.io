---
title: "pymysql"
date: 2018-09-26 14:01
---


[TOC]


# pymysql



## 安装

```
pip install pymysql
```



## 初始化连接

```
conn = pymysql.connect(host='localhost', user='root', password='password', database='demo', port=3306)
cursor = conn.cursor()



conn.commit()
conn.close()
```





## 插入数据

### 单条数据

```
sql = '''
insert into user(id, username, age, password) values(1, 'aaa', 18, '123456')
'''

cursor.execute(sql)
conn.commit()
```



### 多条数据

```
sql = '''
insert into user(id, username, age, password) values(njull, %s, %s, %s)
'''
username = 'aaa'
age = 18
password = '123456'

cursor.execute(sql, (username, age, password))
conn.commit()
```







## 查询数据

### fetchone()

获取一条数据

```
cursor = conn.cursor()

sql = '''
select * from user
'''

cursor.execute(sql)
while True:
    result = cursor.fetchone()
    if not result:
        break
    print(result)
conn.close()
```



### fetchall()

获取所有数据

```
cursor = conn.cursor()

sql = '''
select * from user
'''

cursor.execute(sql)
results = cursor.fetchall()
for result in results:
    print(result)
conn.close()
```





### fetchmany(size)

获取指定条数的数据

```
cursor = conn.cursor()

sql = '''
select * from user
'''

cursor.execute(sql)
results = cursor.fetchmany(3)
for result in results:
    print(result)
conn.close()
```



## 删除数据

```
cursor = conn.cursor()

sql = '''
delete from user where id=1
'''

cursor.execute(sql)
conn.commit()
conn.close()
```



## 更新数据

```
cursor = conn.cursor()

sql = '''
update user set username='aaa' where id=1
'''

cursor.execute(sql)
conn.commit()
conn.close()
```

