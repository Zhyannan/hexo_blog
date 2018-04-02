---
title: python基础之函数
date: 2017-07-15 11:22:00
tags: [python,函数,python多态] 
categories: [python基础]
---
# python基础学习之函数

## 1.函数基础

### 1.1什么是函数？为什么要用函数编程？
  - 什么是函数？ 一个函数就是将一些语句集合在一起的部件，它们能够不止一次地在程序中运行。函数还能够计算出一个返回值， 并能够改变作为函数输入的参数，而这些参数在代码运行时也许每次都不相同。
  - 为什么要用函数？1.最大程度的重用和最小化代码冗余 2.流程的分解
### 1.2函数相关的语句和表达式


```python
# Calls def是可执行的代码,一一函数并不存在，直到Python运行了def后才存在。
eg:myfunc("spam","eggs",meat=ham)
# def创建了一个对象并将其赋值给某一变量名.
def adder(a,b=1,*c):
    # return将一个结果对象发送给调用者
    return a+b+c[0]
#lambda创建一个对象但将其作为结果返回
 Funcs = [lambda x: x**2,lambda x: x*3]
#yield 向调用者发回一个结果对象.但是记住它离开的地方
def squares(x):
    for i in range(x):
        yield i ** 2
"""
global声明了一个模块级的变量并被赋值,在默认情况下.所有在一个函数中被眠
值的对象，是这个函数的本地变量，并且仅在这个函数运行的过程中存在。为了
分配一个可以在整个模块中都可以使用的变量;名，函数需要在global语句中将它列
举出来。通常情况下，变'量名往往需要关注它的作用域(也就是说变量存储的地
方) ，并且是通过实赋值语句将变景名绑定至作用域的。
"""
def changer():
    global x; x = 'new'
"""
nonlocal声明了将要赋值的一个封闭的函数变量。类似的， Python3.0中添加的
nonlocal语句允许一个函数来赋值一条语泌封闭的def语句的作用域中已有的名
称。这就允许封闭的函数作为保留状态的一个地方一一当一个函数调用的时候，信
息被记住了一一而不必使用共享的全局名称。
"""
def changer():
    nonlocal x; x = 'new'
```


```python
# def创建了一个对象并将其赋值给某一变量名.
eg:def adder(a,b=1,*c):
```


```python
# return将一个结果对象发送给调用者
eg:return a+b+c[0]
```

### 1.3函数的定义和调用


```python
# def语句是实时执行的:Python函数在程序运行之前并不需要全部定义。更确切地讲. def在运行时才进行评估，而在def之中的代码在函数惆用后才会评估。
def times(x,y):
    return x * y
times(3,5)
```




    15



### 1.4python中的多态
- 就像我们看到的那样， ti mes 函数中表达式沪y的意义完全取决干x和y的对象类型，同样的函数，在一个实例下执行的是乘泣， 在另一个实例下执行的却是赋值。Py thon将对某一对象在某种语法的合理性交囱对象自身来判断。实际上， "*"在针对正被处理的对象进行了随机应变。这种依赖类型的行为称为多态


```python
# eg1
def times(x,y):
    return x * y
times(3,5)
times("ab",3)
```




    'ababab'




```python
# eg2
def intersect(seq1,seq2):
    res = []
    for x in seq1:
        if x in  seq2:
            res.append(x)
    return res
s1 = "SDAF"
s2 = "SDBOF"
print intersect(s1,s2)
#intersect是多态的,它可以支持多种类型,只要其支持扩展对象接口
x = intersect([1,2,3],(1,4))
print x
#intersect函数相当慢(它执行嵌套循环) ，并不是真正的数学交集(结果中可能有重复的元素)，这个函数可以用一个单独的列表解析表达式来替代
s1 = "SDAF"
s2 = "SABOF"
print [x for x in s1 if x in s2]
s1 = [1,2,3]
s2 = (1,4)
print [x for x in s1 if x in s2]
```

    ['S', 'D', 'F']
    [1]
    ['S', 'A', 'F']
    [1]
    

#### 本地变量，以上例中的intersect函数为例：
- res,seq1,seq2,x都是intersect函数的本地变量
- 所有的本地变量都会在函数调用时出现，并在函数退出时悄失

### 1.5 q&a(个人理解)
- q:什么时候Python将会创建函数?在函数定义内部的语句什么时候运行? 
- a:python函数是实时执行的，只有当Python运行到并执行def语句的时候才会创建函数，并且函数内部的代码也只会在调用函数的时候进行评估。
- q:当一个函数没有return语句时，它将返还什么? 
- a:函数的几个要素包括：函数名，参数，处理过程，返回结果（return），其中处理过程不必要，但其他三个是一定有的（但是return不一定要写，在定义函数时可以不写return，函数会默认返回None。
- q:检查传入函数的对象类型有什么错误? 
- a:~~如果传入的参数数量不对或者传入的参数数量是对的，但参数类型不能被函数所接受，都会报TypeError的错误~~ 
- a：检查传入函数的对象类型，实质上就是破坏函数的灵活性，把函数限制在特定的类型上。没有这类检查时，函数可能处理所有的对象类型: 任何支持函数所预期的接口的对象都能用。
