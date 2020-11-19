---
title: Python_Module#1 os
categories: Python Module
tags: Python
---

```python
import os
```

<!-- more -->

# 1  os创建目录

###  `os.mkdir(path)`

这种情况下，上级目录必须存在，最后一个目录不存在则会自动创建。


```python
path = "mkdir"
if not os.path.exists(path):#判断目录路径是否存在
    os.mkdir(path)
```

###  `os.makedirs(path)`

这种情况下，只要目录路径下有不存在的目录，就会创建该目录，然后递归的创建文件目录。


```python
path = "blankfolder"
if not os.path.exists(path):
    os.makedirs(path)
```

###  os批量创建n个指定目录

文件名称中只带一个数字


```python
path = "blankfolder/folder_"
for i in range(100):
    isExists = os.path.exists(path+str(i+1))
    if not isExists:
        os.makedirs(path+str(i+1))
#        print("%s 目录创建成功"%(i+1))
    else:
#        print("%s 目录已经存在"%(i+1))
        continue
```

文件名称中带多个数字


```python
path = "PreData/Bearing"
for i in range(3):
    for j in range(5):
        end_path = path + str(i+1) + "_" + str(j+1)
        isExists = os.path.exists(end_path)
        if not isExists:
            os.makedirs(end_path)
        else:
            continue
```

文件有多个上级目录


```python
Path_List = ['35Hz12kN','37.5Hz11kN','40Hz10kN']
for i in range(3):
    path = 'PreData' + '/' + Path_List[i]
#    print(path)
    isExists = os.path.exists(path)
    if not isExists:
        os.makedirs(path)
    for j in range(5):
        end_path = path + '/' + 'Bearing' + str(i+1) + '_' + str(j+1)
#        print(end_path)
        isExists = os.path.exists(end_path)
        if not isExists:
            os.makedirs(end_path)
        else:
            continue
```

# 2  `os.listdir(path)`

返回一个列表，其中包含由`path`给出的目录中条目的名称。该列表按任意顺序排列，并且不包含特殊条目'.' 和'..'，即使它们存在于目录中。


```python
path = "blankfolder"
dirs = os.listdir(path)
#for folder in dirs:#输出所有文件文件和文件夹
#    print(folder)
```

# 3  目录下文件的排序—list排序

`sort(*,key=None,reverse=False)`  
*key* 指定一个带有参数的函数，用于从每个列表元素中提取比较键，默认值`None`表示直接对列表项排序不计算一个单独的键值； *reverse* 若为`True`，则反向排序  

*key* 函数可通过`lamdba`表达式来创建， **list** 会根据表达式的`expression`进行排序

### 按照文件中数字大小进行排序

`str.split(sep=None,maxsplit=-1)`  
返回字符串内单词组成的列表，使用 *sep* 作为分割字符串，若 *sep* 为`None`则按照空格进行拆分。若给出 *maxsplit* ,则最多进行 *maxsplit* 次拆分


```python
dirs.sort(key=lambda x:int(x.split('_')[1]))
#for folder in dirs:
#    print(type(int(folder.split('_')[1])))
#    print(folder.split('_')[1])
#    print(folder)
```

### 按文件名称字符串小写排序


```python
dirs.sort(key=lambda x:x.lower())
#for folder in dirs:
#    print(folder)
```

### 按创建时间精确到秒排序
+ `os.path.getatime(path)`:返回`path`的最后访问时间
+ `os.path.getmtime(path)`:返回`path`的最后修改时间
+ `os.path.getctime(path)`:返回`path`在系统中的ctime，Windows中，为`path`的创建时间


```python
dirs.sort(key=lambda x:os.path.getatime(os.path.join(path,x)))
#print(os.path.join(path,"folder_1"))
#for folder in dirs:
#    print(folder)
```


```python
dirs.sort(key=lambda x:os.path.getmtime(os.path.join(path,x)))
#for folder in dirs:
#    print(folder)
```


```python
dirs.sort(key=lambda x:os.path.getctime(os.path.join(path,x)))
#for folder in dirs:
#    print(folder)
```

### 按创建时间精确到纳秒排序

使用`os.stat(path)`的返回值`statinfo`的三个属性获取文件的创建时间等信息  
+ `st_atime_ns`:返回`statinfo`的最后访问时间(纳秒)
+ `st_mtime_ns`:返回`statinfo`的最后修改时间(纳秒)
+ `st_ctime_ns`:返回`statinfo`在系统中的ctime，Windows中，为`path`的创建时间(纳秒)


```python
dirs.sort(key=lambda x:os.stat(os.path.join(path,x)).st_ctime_ns)
#for folder in dirs:
#    print(folder)
```

**注:**在使用`os.path.getctime(path)`,`os.path.getmtime(path)`,`os.path.getatime(path)`或`os.stat(path)`时所用路径必须为相对路径全称，故需要用`os.path.join(path,*paths)`来拼接路径  

### 按文件名称中某几位特定的键值进行排序


```python
i = 4
dirs.sort(key=lambda x:x[:-i])
"""
for folder in dirs:
    print(folder[:-i])
    print(type(folder[:-i]))
    print(folder)
"""
```




    'for folder in dirs:\n    print(folder[:-i])\n    print(type(folder[:-i]))\n    print(folder)'



### 引入`re`按照文件名称排序

+ `re.compile(pattern,flags=0)`  

 将正则表达式的样式编译为一个正则表达式对象（正则对象），可以用于匹配  
 序列  
 ```
 prog = re.compile(pattern)
 result = prog.match(string)
 ```
 等价于
 ```
 result = re.match(pattern, string)
 ```
 如果需要多次使用这个正则表达式 *pattern* 话，使用`re.compile()`和保存这个这个正则对象以便复用，可以让程序更加高效

+ `re.split(pattern,string,maxsplit=0,flags=0)`  

用 *pattern* 分开 *string* 。 如果在 *pattern* 中捕获到括号，那么所有的组里的文字也会包含在列表里。如果 *maxsplit* 非零， 最多进行 *maxsplit* 次分隔， 剩下的字符全部返回到列表的最后一个元素。  

+ `pattern = r'(\d+)`  
  + `+`
    + 对它前面的正则式匹配1到任意次重复。 `ab+` 会匹配 `'a'` 后面跟随1个以上到任意个 `'b'`，它不会匹配 `'a'`。
  + `\d`
    + 对于 Unicode (str) 样式：匹配任何Unicode十进制数（就是在Unicode字符目录`[Nd]`里的字符）。这包括了`[0-9]`，和很多其他的数字字符。如果设置了ASCII标志，就只匹配`[0-9]`。
    + 对于8位(bytes)样式：
      匹配任何十进制数，就是`[0-9]`。

+ `s[i:j:k]`

s从i到j步长为k的切片

+ `map(function, iterable,...)`

对每个iterable进行function运算，可以使用lambda匿名函数


```python
import re
#自定义sort_key函数
def sort_key(s):
    #sort_strings_with_embedded_numbers
    re_digits = re.compile(r'(\d+)')
    pieces = re_digits.split(s)  # 切成数字与非数字
#    print(pieces)
#    print(pieces[1::2])
    pieces[1::2] = map(int, pieces[1::2])  # 将数字部分转成整数
    return pieces
```


```python
path = "PreData"
dirss = os.listdir(path)
dirss.sort(key=sort_key)
#for folder in dirss:
#    print(folder)
```
