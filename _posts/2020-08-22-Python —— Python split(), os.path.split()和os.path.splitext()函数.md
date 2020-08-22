---
layout: post
title:  "Python —— python split(), os.path.split()和os.path.splitext()函数"
date:   2020-08-22 22:46:13
categories: Python
permalink: /archivers/how-to-using-split-path.split-path.splitext
---

### 1. split()

split() 函数通过指定分隔符对字符串进行切片，如果参数 num 有指定值，则仅分隔 num 个子字符串

语法：

str.split(str="", num=string.count(str))

参数：

str -- 分隔符 默认为所有的空字符，包括空格、换行(\n)、制表符(\t)等

num -- 分割次数

```python
>>> '/home/ubuntu/python/example.py'.split('/')  # 分裂
['', 'home', 'ubuntu', 'python', 'example.py']
 
>>> '/home/ubuntu/python/example.py'.split('/', 1)  # 只分裂一次
['', 'home/ubuntu/python/example.py']
```

### 2. os.path.split()

os.path.split() 函数将文件路径和文件名分开

```python
>>> os.path.split('/home/ubuntu/python/example.py')
('/home/ubuntu/python', 'example.py')
```

### 3. os.path.splitext()

os.path.splitext() 函数将文件名和扩展名分开

```python
>>> os.path.splitext('/home/ubuntu/python/example.py')
('/home/ubuntu/python/example', '.py')
```




*****

欢迎来跟博主讨论Python有关的问题。