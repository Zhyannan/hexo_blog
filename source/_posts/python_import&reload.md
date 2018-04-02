---
title: python基础之模块儿导入和重载
date: 2017-07-14 10:15:00
tags: [python,import,reload] 
categories: [python基础]
---
# python基础学习之模块儿导入和重载

## 1.import 的工作流程
1. 找到模块儿文件
2. 编译成位码（需要时）
3. 执行模块儿的代码来创建起所定义的对象


```python
#创建一个名为myfile.py的python模块儿文件，其内容为：
title = "Hello Word"
```


```python
#在新的python文件中首次加载我们刚才创建的myfile模块儿
import myfile
```

    Hello Word
    


```python
# 默认情况下，只是在每次会话的第一次运行，在第一次导入之后，其他的导入都不会再工作
import myfile #再次导入就没有执行
```


```python
# 使用reload函数可以再次执行
from imp import reload
reload(myfile)
```

    Hello Word
    




    <module 'myfile' from 'myfile.pyc'>



## 2.获取模块儿的属性


```python
#创建一个名为myfile.py的python模块儿文件，其内容为：
a = 'first'
b = 'second'
c = 'third'
print a,b,c
```


```python
#在新的python文件中获取myfile中的变量
from imp import reload
reload(myfile)
print myfile.a,myfile.b
```

    first second third
    first second
    


```python
#或者使用from,import导入变量
from myfile import a,b
a,b
```




    ('first', 'second')




```python
#内置的dir函数可以用来获取模块儿内部可用的变量名的列表
dir(myfile) #以双下划线开头并结尾的变量名;这些通常都是由Python预定义的内置变量名,那些通过代码赋值而定义的变量( a,b,c ) 在dir结果的最后显示。
```




    ['__builtins__',
     '__doc__',
     '__file__',
     '__name__',
     '__package__',
     'a',
     'b',
     'c',
     'title']


