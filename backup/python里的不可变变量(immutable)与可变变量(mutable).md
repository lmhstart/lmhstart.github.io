# python里的不可变变量(immutable)与可变变量(mutable)

 ---


>在正文开始前先看两道题做做比较
```python
def func(num):
    num += 1 
    return num

x = 5
print(func(x))  # 输出结果6
print(x)        # 输出结果5 
```


```python
def func(lst):
    lst.append(4)  
    return lst

my_list = [1, 2, 3]
print(func(my_list))  # 输出结果[1, 2, 3, 4]
print(my_list)        # 输出结果[1, 2, 3, 4] （变了！）
```

>由此可见，同样是修改变量的函数，第二段中变量`my_list`却在最后输出时发生变化


接下来引入正题：

程序的数据必须以特定类型存放在内存的某个区域，如果变量的值(value)发生了了变化，内存地址也发生了变化，那么这个变量就属于可变类型，否则为不可变类型。

>可以使用`id()`函数来进行变量内存地址的判断


 ---

## **不可变（Immutable）类型**
这些类型的值一旦创建就不能修改：
1. 整数(init)
2. 浮点数(float)
3. 布尔值(bool)
4. 字符串(string)
5. 元组(tuple)
6. 冻结集合(frozenset)

## **可变（mutable）类型**
这些类型的值可以在后续被函数或方法修改：
1. 列表(list)
2. 字典(dictionary)
3. 集合(set)

>[!tip]
>一般append(),pop()适用的都属于可变变量









