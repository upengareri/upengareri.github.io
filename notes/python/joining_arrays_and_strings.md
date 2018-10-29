---
layout: single
title: <span style="color:#ABB2B9">Joining arrays and strings</span>
date: 2018-10-29
---

## ARRAY

### 1. Append
- to add only one element or any object at the end of the list

> `Note: The length of the list increases by one.`

_Example 1.1:_

```python
a = [1, 'x', 2]
a.append('y')
print(a)

OUTPUT:
[1, 'x', 2, 'y']
```

_Example 1.2:_

```python
a = [1, 'x', 2]
b = ['y', 3, 'z']
a.append(b)
print(a)

OUTPUT:
[1, 'x', 2, ['y', 3, 'z']]
```
> `Notice that 'b' is added as a single object at the end of the list 'a'`

### 2. Extend
- to combine elements of another iterable to a list

> `Note: The length of the list increases by the number of elements in its arguments.`<br/>
***Caution:*** Unlike append, extend takes only __iterable__ as an arguments.

_Example 2.1:_

```python
a = [1, 'x', 2]
b = ['y', 3, 'z']
a.extend(b)
print(a)

OUTPUT:
[1, 'x', 2, 'y', 3, 'z']
```
> `Notice that each element of 'b' is added separately to the list 'a'`


_Example 2.2:_
```python
a = [1,'x', 2]

a.extend(3)

OUTPUT:
TypeError: 'int' object is not iterable
```
> `Notice that we can't add non iterable`

_Example 2.3:_
```python
a = [1,'x', 2]
b = 'hello'
a.extend(b)
print(a)

OUTPUT:
[1, 'x', 2, 'h', 'e', 'l', 'l', 'o']
```
> `Since string is an iterable, each character of the string gets added as a separate element to 'a'`

### Side Note: How is 'EXTEND' different from '+' operator

```python
a = [1, 'x', 2]
b = ['y', 3, 'z']
a + b

OUTPUT:
[1, 'x', 2, 'y', 3, 'z']
```
> `We can produce the same result as _Example 2.1_ using '+' operator as well but there are two major differences between 'EXTEND' and '+'`

<span style="color:#F5B7B1">`(i) We can't concatenate any other iterable (like string, tuple, dictionary) except list to a list using '+' operator`</span>

```python
a = [1, 'x', 2]
b = 'hello'
a + b

OUTPUT:
TypeError: can only concatenate list (not "str") to list
```
<span style="color:#F5B7B1">`(ii)  '+' operator creates a new list whereas 'EXTEND' does _in-place_ modification. This makes '+' computationally expensive operation compared to 'EXTEND'`</span>

```python
a = [1, 'x', 2]
b = ['y', 3, 'z']
c = a + b
print(a)
print(b)
print(c)

OUTPUT:
[1, 'x', 2]
['y', 3, 'z']
[1, 'x', 2, 'y', 3, 'z']
```

### 3. INSERT
- to add an element/object at some particular index

_Example 3.1_

```python
a = [1, 'x', 5]
a.insert(2,4)

OUTPUT:
[1, 'x', 4, 5]
```

> First argument is 'index' whereas second one is 'item'

## STRING

### 1. Use '+' operator to append two separate strings

_Example 1.1_

```python
a = 'hello'
b = ' world'
print(a + b)

OUTPUT:
hello world
```

### 2. Use 'join' to concatenate list of strings

_Example 2.1_

```python
‘ ‘ .join([‘hello’, ‘world’])

OUTPUT:
hello world
```


_Example 2.1_

```python
‘,‘ .join([‘hello’, ‘world’])

OUTPUT:
hello,world
```

> Notice that the object before the join acts as a separator. In _Example 2.1_, 'space' acts as a separator whereas in _Example 2.2_, 'comma' acts as separator


## SUMMARY

### FOR ARRAY:
___append:___ `to add only one element or an object at the end of the list`<br/>
___insert:___ `to add an element/object at some particular index`<br/>
___extend:___ `to combine elements of another iterable to a list.`

> '+' is relatively heavy operation when dealing with list concatenation  

### FOR STRING:
___'+':___ `for adding two/more simple objects`<br/>
___'join':___ `for list of string objects`

