# Python上机代码

## 读取键盘输入

input读取一行，回车结束。

```python
str = int(input()) #读取为str转为int
```

```python
str = input("请输入：")
print ("你输入的内容是: ", str)
# 请输入：菜鸟教程
# 你输入的内容是:  菜鸟教程
```

很多题目要求，输入一个n，然后接着输入n个整数，如：

5

1 2 3 4 5

用input()输入如何将这5个数隔开呢？（input是整行输入，且输入为字符串）

用split：

```python
n = int(input())#输入整数n
ans = input()
if len(ans.split())==n:
	a = [int(i) for i in ans.split()]
```

> ```python
> str.split(str="", num=string.count(str))
> ```
>
> - str -- 分隔符，默认为所有的空字符，包括空格、换行(\n)、制表符(\t)等。
> - num -- 分割次数。默认为 -1, 即分隔所有。
>
> 参考资料：https://www.runoob.com/python/att-string-split.html



## 数据类型转换

| 函数                                                         | 描述                                                |
| :----------------------------------------------------------- | :-------------------------------------------------- |
| [int(x ,base\)](https://www.runoob.com/python3/python-func-int.html) | 将x转换为一个整数                                   |
| [float(x)](https://www.runoob.com/python3/python-func-float.html) | 将x转换到一个浮点数                                 |
| [complex(real ,imag)](https://www.runoob.com/python3/python-func-complex.html) | 创建一个复数                                        |
| [str(x)](https://www.runoob.com/python3/python-func-str.html) | 将对象 x 转换为字符串                               |
| [repr(x)](https://www.runoob.com/python3/python-func-repr.html) | 将对象 x 转换为表达式字符串                         |
| [eval(str)](https://www.runoob.com/python3/python-func-eval.html) | 用来计算在字符串中的有效Python表达式,并返回一个对象 |
| [tuple(s)](https://www.runoob.com/python3/python3-func-tuple.html) | 将序列 s 转换为一个元组                             |
| [list(s)](https://www.runoob.com/python3/python3-att-list-list.html) | 将序列 s 转换为一个列表                             |
| [set(s)](https://www.runoob.com/python3/python-func-set.html) | 转换为可变集合                                      |
| [dict(d)](https://www.runoob.com/python3/python-func-dict.html) | 创建一个字典。d 必须是一个 (key, value)元组序列。   |
| [frozenset(s)](https://www.runoob.com/python3/python-func-frozenset.html) | 转换为不可变集合                                    |
| [chr(x)](https://www.runoob.com/python3/python-func-chr.html) | 将一个整数转换为一个字符                            |
| [ord(x)](https://www.runoob.com/python3/python-func-ord.html) | 将一个字符转换为它的整数值                          |
| [hex(x)](https://www.runoob.com/python3/python-func-hex.html) | 将一个整数转换为一个十六进制字符串                  |
| [oct(x)](https://www.runoob.com/python3/python-func-oct.html) | 将一个整数转换为一个八进制字符串                    |

## 保留小数位

`round()`函数可以接受两个参数：要四舍五入的数字和要保留的小数位数。如果不指定小数位数，`round()`函数默认将四舍五入到最接近的整数。

```python
num = 3.14159
rounded_num = round(num, 2)  # 保留两位小数
print(rounded_num)  # 输出：3.14
```



## 列表

列表末尾追加元素：

```python
# append追加单个元素
list1 = ['Google', 'Runoob', 'Taobao']
list1.append('Baidu')
print ("更新后的列表 : ", list1)
# 更新后的列表 :  ['Google', 'Runoob', 'Taobao', 'Baidu']

# extend追加一个列表
list1 = ['Google', 'Runoob', 'Taobao']
list2=list(range(5)) # 创建 0-4 的列表
list1.extend(list2)  # 扩展列表
print ("扩展后的列表：", list1)
# 扩展后的列表： ['Google', 'Runoob', 'Taobao', 0, 1, 2, 3, 4]
```

删除列表元素：

```python
list = ['Google', 'Runoob', 1997, 2000]
 
print ("原始列表 : ", list)
del list[2]
print ("删除第三个元素 : ", list)
# 原始列表 :  ['Google', 'Runoob', 1997, 2000]
# 删除第三个元素 :  ['Google', 'Runoob', 2000]
```

使用列表来实现队列的基本功能：

- `append()` 方法向队列的末尾添加一个元素。
- `pop()` 方法从队列的开头删除一个元素并返回它。

例子：

```python
queue = []

# 添加元素到队列的末尾
queue.append('A')
queue.append('B')
queue.append('C')

# 从队列的开头删除元素并返回
print(queue.pop(0))  # A
print(queue.pop(0))  # B
print(queue.pop(0))  # C
```

使用列表来实现栈的基本功能：

```python
# 压入
stack.append(1)
stack.append(2)
stack.append(3)
print(stack)  # 输出: [1, 2, 3]

# 弹出
top_element = stack.pop()
print(top_element)  # 输出: 3
print(stack)        # 输出: [1, 2]
```

列表的逆序遍历：

```python
a = [1,3,6,8,9]
print("通过下标逆序遍历1：")
for i in a[::-1]:
    print(i, end=" ")
print("\n通过下标逆序遍历2：")
for i in range(len(a)-1,-1,-1):
    print(a[i], end=" ")
print("\n通过reversed逆序遍历：")
for i in reversed(a):
    print(i, end=" ")
```

列表脚本操作符：

| Python 表达式                         | 结果                         | 描述                 |
| :------------------------------------ | :--------------------------- | :------------------- |
| len([1, 2, 3])                        | 3                            | 长度                 |
| [1, 2, 3] + [4, 5, 6]                 | [1, 2, 3, 4, 5, 6]           | 组合                 |
| ['Hi!'] * 4                           | ['Hi!', 'Hi!', 'Hi!', 'Hi!'] | 重复                 |
| 3 in [1, 2, 3]                        | True                         | 元素是否存在于列表中 |
| for x in [1, 2, 3]: print(x, end=" ") | 1 2 3                        | 迭代                 |

列表函数&方法

| 序号 | 函数                                                         |
| :--- | :----------------------------------------------------------- |
| 1    | [len(list)](https://www.runoob.com/python3/python3-att-list-len.html) 列表元素个数 |
| 2    | [max(list)](https://www.runoob.com/python3/python3-att-list-max.html) 返回列表元素最大值 |
| 3    | [min(list)](https://www.runoob.com/python3/python3-att-list-min.html) 返回列表元素最小值 |
| 4    | [list(seq)](https://www.runoob.com/python3/python3-att-list-list.html) 将元组转换为列表 |

| 序号 | 方法                                                         |
| :--- | :----------------------------------------------------------- |
| 1    | [list.append(obj)](https://www.runoob.com/python3/python3-att-list-append.html) 在列表末尾添加新的对象 |
| 2    | [list.count(obj)](https://www.runoob.com/python3/python3-att-list-count.html) 统计某个元素在列表中出现的次数 |
| 3    | [list.extend(seq)](https://www.runoob.com/python3/python3-att-list-extend.html) 在列表末尾一次性追加另一个序列中的多个值（用新列表扩展原来的列表） |
| 4    | [list.index(obj)](https://www.runoob.com/python3/python3-att-list-index.html) 从列表中找出某个值第一个匹配项的索引位置 |
| 5    | [list.insert(index, obj)](https://www.runoob.com/python3/python3-att-list-insert.html) 将对象插入列表 |
| 6    | [list.pop(index=-1\)] 移除列表中的一个元素（默认最后一个元素），并且返回该元素的值 |
| 7    | [list.remove(obj)](https://www.runoob.com/python3/python3-att-list-remove.html) 移除列表中某个值的第一个匹配项 |
| 8    | [list.reverse()](https://www.runoob.com/python3/python3-att-list-reverse.html) 反向列表中元素 |
| 9    | [list.sort( key=None, reverse=False)](https://www.runoob.com/python3/python3-att-list-sort.html) 对原列表进行排序 |
| 10   | [list.clear()](https://www.runoob.com/python3/python3-att-list-clear.html) 清空列表 |
| 11   | [list.copy()](https://www.runoob.com/python3/python3-att-list-copy.html) 复制列表 |



## 字典

删除字典元素：

```python
tinydict = {'Name': 'Runoob', 'Age': 7, 'Class': 'First'}
 
del tinydict['Name'] # 删除键 'Name'
tinydict.clear()     # 清空字典
```

遍历字典：

字典 items() 方法以列表返回视图对象，是一个可遍历的key/value 对。

```python
d={1:"a",2:"b",3:"c"}
result=[]
for k,v in d.items():
    result.append(k)
    result.append(v)

print(result)
```

| 序号 | 函数及描述                                                   |
| :--- | :----------------------------------------------------------- |
| 1    | [dict.clear()](https://www.runoob.com/python3/python3-att-dictionary-clear.html) 删除字典内所有元素 |
| 2    | [dict.copy()](https://www.runoob.com/python3/python3-att-dictionary-copy.html) 返回一个字典的浅复制 |
| 3    | [dict.fromkeys()](https://www.runoob.com/python3/python3-att-dictionary-fromkeys.html) 创建一个新字典，以序列seq中元素做字典的键，val为字典所有键对应的初始值 |
| 4    | [dict.get(key, default=None)](https://www.runoob.com/python3/python3-att-dictionary-get.html) 返回指定键的值，如果键不在字典中返回 default 设置的默认值 |
| 5    | [key in dict](https://www.runoob.com/python3/python3-att-dictionary-in.html) 如果键在字典dict里返回true，否则返回false |
| 6    | [dict.items()](https://www.runoob.com/python3/python3-att-dictionary-items.html) 以列表返回一个视图对象 |
| 7    | [dict.keys()](https://www.runoob.com/python3/python3-att-dictionary-keys.html) 返回一个视图对象 |



## 排序sorted(key=lambda)

> sorted(list, key=lambda)与list.sort(key=lambda)用法几乎一样，推荐后者。

当待排序列表的元素由多字段构成时，我们可以通过sorted(iterable，key，reverse)的参数key来制定我们根据哪个字段对列表元素进行排序。

**key=lambda 元素: 元素[字段索引]**
例如：想对元素第二个字段排序，则**key=lambda y: y[1]** 备注：这里y可以是**任意**字母，等同key=lambda x: x[1]。

例子：

```python
listA = [3, 6, 1, 0, 10, 8, 9]
print(sorted(listA))

listB = ['g', 'e', 't', 'b', 'a']
print(sorted(listB))
print(sorted(listB, key=lambda y: y[0]))

listC = [('e', 4), ('o', 2), ('!', 5), ('v', 3), ('l', 1)]
print(sorted(listC, key=lambda x: x[1]))
```

```python
#结果一
[0, 1, 3, 6, 8, 9, 10]
#结果二
['a', 'b', 'e', 'g', 't']
['a', 'b', 'e', 'g', 't']
#结果三
[('l', 1), ('o', 2), ('v', 3), ('e', 4), ('!', 5)]
```

如果是多字段按优先级排序：

```python
lis = [{ "name" : "Taobao", "age" : 100},  
{ "name" : "Runoob", "age" : 7 }, 
{ "name" : "Google", "age" : 100 }, 
{ "name" : "Wiki" , "age" : 200 }] 
  
# 通过 age 升序排序
print ("列表通过 age 升序排序: ")
print (sorted(lis, key = lambda i: i['age']) )
  
print ("\r") 
  
# 先按 age 排序，再按 name 排序
print ("列表通过 age 和 name 排序: ")
print (sorted(lis, key = lambda i: (i['age'], i['name'])) )
  
print ("\r") 
  
# 按 age 降序排序
print ("列表通过 age 降序排序: ")
print (sorted(lis, key = lambda i: i['age'],reverse=True) )
```

## 单链表

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-
# @Time: 2020-Jul-06
# @Author: xiaofu

class Node(object):
    def __init__(self, value):
        self.value = value
        self.next = None


class SingleLinkedList(object):
    def __init__(self, node=None):
        self.__head = node

    def isEmpty(self):
        """check if the list is empty"""
        return self.__head == None

    def length(self):
        """length of the list"""
        # cur is current position
        cur = self.__head
        count = 0
        while cur != None:
            cur = cur.next
            count += 1
        return count

    def travel(self):
        """traverse through the list"""
        # cur is current position
        cur = self.__head
        while cur != None:
            print(cur.value, end=" ")
            cur = cur.next
        print('')

    def shift(self, value):
        """add a node to the start"""
        node = Node(value)
        # link before break
        node.next = self.__head
        self.__head = node

    def append(self, value):
        """add a node to the end"""
        node = Node(value)
        if self.isEmpty():
            self.__head = node
        else:
            cur = self.__head
            while cur.next != None:
                cur = cur.next
            cur.next = node

    def insert(self, pos, value):
        """insert a node at specific position"""
        if pos <= 0:
            self.shift(value)
        elif pos > (self.length() - 1):
            self.append(value)
        else:
            node = Node(value)
            cur = self.__head
            count = 0
            while count < pos - 1:
                cur = cur.next
                count += 1
            node.next = cur.next
            cur.next = node

    def remove(self, value):
        """remove a node from list when a value first appears"""
        cur = self.__head
        if cur.value == value:
            self.__head = cur.next
            return value
        elif self.__head is None:
            return
        else:
            while cur.next != None:
                if cur.next.value == value:
                    cur.next = cur.next.next
                    return value
                else:
                    cur = cur.next
            return

    def exist(self, value):
        """whether a node exists in list"""
        cur = self.__head
        while cur != None:
            if cur.value == value:
                return True
            else:
                cur = cur.next
        return False
```

> https://blog.csdn.net/Victor2code/article/details/107170807

## 二叉树

```python
#! /usr/bin/env python
# -*- coding: utf-8 -*- 
# @author: xiaofu
# @date: 2020-Jul-24

class Node:
    """binary tree node"""

    def __init__(self, value, lchild=None, rchild=None):
        self.value = value
        self.lchild = lchild
        self.rchild = rchild


class Binary_Tree:
    """binary tree"""

    def __init__(self, root=None):
        self.root = root

    def add(self, node):
        if self.root is None:
            self.root = node
            return
        temp = [self.root]
        while temp:
            nextNode = temp.pop(0)
            if nextNode.lchild is None:
                nextNode.lchild = node
                return
            elif nextNode.rchild is None:
                nextNode.rchild = node
                return
            else:
                temp.append(nextNode.lchild)
                temp.append(nextNode.rchild)

    def breadth_travel(self):
        if self.root is None:
            return
        temp = [self.root]
        while temp:
            nextNode = temp.pop(0)
            print(nextNode.value, end=' ')
            if nextNode.lchild is None:
                continue
            elif nextNode.rchild is None:
                temp.append(nextNode.lchild)
                continue
            else:
                temp.append(nextNode.lchild)
                temp.append(nextNode.rchild)


    def preorder(self):
        self.__preorder(self.root)


    def inorder(self):
        self.__inorder(self.root)


    def postorder(self):
        self.__postorder(self.root)


    def __preorder(self, node):
        if node is None:
            return
        print(node.value, end=' ')
        self.__preorder(node.lchild)
        self.__preorder(node.rchild)

    def __inorder(self, node):
        if node is None:
            return
        self.__inorder(node.lchild)
        print(node.value, end=' ')
        self.__inorder(node.rchild)

    def __postorder(self, node):
        if node is None:
            return
        self.__postorder(node.lchild)
        self.__postorder(node.rchild)
        print(node.value, end=' ')


if __name__ == '__main__':
    tree = Binary_Tree()
    tree.add(Node(1))
    tree.add(Node(2))
    tree.add(Node(3))
    tree.add(Node(4))
    tree.add(Node(5))
    tree.add(Node(6))
    tree.add(Node(7))
    tree.add(Node(8))
    tree.add(Node(9))
    tree.breadth_travel()
    print('')
    tree.preorder()
    print('')
    tree.inorder()
    print('')
    tree.postorder()
```

> https://blog.csdn.net/Victor2code/article/details/107619099



> 参考资料：
>
> 1. https://blog.csdn.net/u010758410/article/details/79737498
> 2. 菜鸟教程
> 3. 