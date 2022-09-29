---
title: python列表删除元素(全)
date: 2022-09-29 17:54:45
tags:
---
**python列表删除元素**
<!--more-->

### 列表直接删除元素

**remove: 删除单个元素，删除首个符合条件的元素，按值删除**

```python
str = [1,2,3,4,3,5,6,2]
str.remove(3)
print(str)  # [1, 2, 4, 3, 5, 6, 2]
```

**pop: 删除单个或多个元素，按位删除(根据索引删除), 删除时会返回被删除的元素**

```python
str_pop= [1,2,3,4,3,5,6,2]
str_pop.pop(3)
print(str_pop)  # [1, 2, 3, 3, 5, 6, 2]
```

**del: 根据索引删除**

```python
str_del= [1,2,3,4,3,5,6,2]
del str_del[1]
print(str_del)  # [1, 3, 4, 3, 5, 6, 2]
```

<br/>

## 列表遍历过程中删除元素, 会造成不可预知错误, 可使用下面几种方法删除

**方法一: 列表推导式**

```python
# 删除 <4
list1 = [1, 2, 3, 4, 5, 6]
new_list1 = [i for i in list1 if i > 4]
print(new_list1)
```

**方法二: filter + lambda**

```python
# 删除 <4
list2 = [1, 2, 3, 4, 5, 6]
new_list2 = filter(lambda i: i > 4, list2)
print(list(new_list2))
```

**方法三: 倒序遍历**

```python
# 删除 >4
list3 = [1, 2, 3, 4, 5, 6]
for i in range(len(list3)-1, -1, -1):
    if list3[i] > 4:
        list3.remove(list3[i])
print(list3)
```

**方法四:**

```python
# 删除 >4
list4 = [1, 2, 3, 4, 5, 6]
new_list4 = []
for i in list4:
    if i <= 4:
        new_list4.append(i)
print(new_list4)
```

