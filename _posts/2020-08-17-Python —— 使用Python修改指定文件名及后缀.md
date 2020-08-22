---
layout: post
title:  "Python —— 使用Python修改指定文件名及后缀"
date:   2020-08-17 22:46:13
categories: Python
permalink: /archivers/how-to-change-filename
---

# 1、重命名文件名称

```python
import os

# 列出当前目录中文件
print("目录为: %s" % os.listdir(os.getcwd()))
# 重命名
os.rename("111.txt", "test.txt")
print("重命名成功")
# 列出重命名后的目录文件
print("目录为: %s" % os.listdir(os.getcwd()))
```

> os.getcwd() 获取当前工作目录
>
> os.rename(*args, **kwargs) 修改名称，第一个参数为当前文件名，第二个为修改后文件名



# 2、修改文件后缀

```python
# python批量更换后缀名
import os

# 列出当前目录下所有的文件
files = os.listdir('.')
print(files)
for filename in files:
    portion = os.path.splitext(filename)
    # 如果后缀是.dat
    if portion[1] == ".dat":
        # 重新组合文件名和后缀名
        newname = portion[0] + ".txt"
        os.rename(filename, newname)
```

> os.path.splitext(“文件路径”)  分离文件名与扩展名；默认返回(fname,fextension)元组，可做分片操作

example:

```python
import os
path_01='D:/User/wgy/workplace/data/notMNIST_large.tar.gar'
path_02='D:/User/wgy/workplace/data/notMNIST_large'
root_01=os.path.splitext(path_01)
root_02=os.path.splitext(path_02)
print(root_01)
print(root_02)
```

Result:

```python
结果：
('D:/User/wgy/workplace/data/notMNIST_large.tar', '.gar')
('D:/User/wgy/workplace/data/notMNIST_large', '')
```

# 3、修改文件名指定内容

```python
import os

files_name = os.listdir()
# print(files_name)
for file_name in files_name:
    if '123' in file_name:
        file_name_new = file_name.replace('123', '111')
        os.rename(file_name, file_name_new)

    # print(file_name)
```



*****

欢迎来跟博主讨论Python有关的问题。