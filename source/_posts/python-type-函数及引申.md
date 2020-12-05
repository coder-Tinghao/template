---
layout: article
title: python--type()函数及引申
date: 2020-11-26 11:22:44
tags: python
---

## python文档学习



### python类型---type()函数

##### type()函数基础用法为：

class type(object)：

传入一个参数时，返回 *object* 的类型。 返回值是一个 type 对象，通常与 [`object.__class__`](https://docs.python.org/zh-cn/3/library/stdtypes.html#instance.__class__) 所返回的对象相同。

推荐使用 [`isinstance()`](https://docs.python.org/zh-cn/3/library/functions.html#isinstance) 内置函数来检测对象的类型，在下面给出解释：

###### isinstance(object, classinfo):

如果参数 *object* 是参数 *classinfo* 的实例或者是其 (直接、间接或 [虚拟](https://docs.python.org/zh-cn/3/glossary.html#term-abstract-base-class)) 子类则返回 True。 如果 *object* 不是给定类型的对象，函数将总是返回 False。

##### type()函数还有另一个用法：

*class* `type`(*name*, *bases*, *dict*)：

传入三个参数时，返回一个新的 type 对象。 这在本质上是 [`class`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#class) 语句的一种动态形式。 *name* 字符串即类名并且会成为 [`__name__`](https://docs.python.org/zh-cn/3/library/stdtypes.html#definition.__name__) 属性；*bases* 元组列出基类并且会成为 [`__bases__`](https://docs.python.org/zh-cn/3/library/stdtypes.html#class.__bases__) 属性；而 *dict* 字典为包含类主体定义的命名空间并且会被复制到一个标准字典成为 [`__dict__`](https://docs.python.org/zh-cn/3/library/stdtypes.html#object.__dict__) 属性。 例如，下面两条语句会创建相同的 [`type`](https://docs.python.org/zh-cn/3/library/functions.html#type) 对象:

```python
class X:
    a = 1

X = type('X', (object,), dict(a=1))
```

当我们使用class定义类的时候，Python解释器仅仅是扫描一下定义的语法，然后调用type()函数创建class类，下面是一个例子：

```python
class A(object):
    # 类属性
    role = 'student'

    # 实例方法
    def __init__(self, name):
        # 实例属性
        self.name = name

    # 类方法
    @classmethod
    def study(cls):
        pass

    # 静态方法
    @staticmethod
    def cal_student_num():
        pass
    
# 对应type()函数的写法    
A = type(
    'A',
    (object,),
    {
        'role': 'student',
        '__init__': __init__,
        'study': study,
        'cal_student_num': cal_student_num
    })
```

显然，因为class的可读性和结构性，在定义类时会使用第一种方式，使用class定义对象的时候，Python解释器调用type()函数来动态创建对象。