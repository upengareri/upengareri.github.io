---
layout: single
title: <span style="color:#ABB2B9">Efficient way of string formatting - Python 3's f-string</span>
date: 2018-10-30
---

Before diving into f-string introduced in Python 3.6, let's talk about the other two string formatting options available in Python.

### Option 1: % formatting

> Note: % formatting is not recommended by Python docs now.

<span style="color:#F5B7B1">`How to use it?`</span>

_Example 1.1:_
```python
>>> name =  "Naveen"
>>> lastname = "Kumar"
>>> "Hello, %s %s" %(name, lastname)
'Hello, Naveen Kumar'

```
<span style="color:#F5B7B1">`Why not great?`</span>

- not readable
- with more arguments, things get messy

### Option 2: str.format

<span style="color:#F5B7B1">`How to use it?`</span>

_Example 2.1:_
```python
>>> name =  "Naveen"
>>> lastname = "Kumar"
>>> "Hello, {} {}".format(name, lastname)
'Hello, Naveen Kumar'
```

We can also use indexing to reference variables in any order.

_Example 2.2:_
```python
>>> name =  "Naveen"
>>> lastname = "Kumar"
>>> "My lastname is: {1} and my first name is: {0}".format(name, lastname)
'My lastname is: Kumar and my first name is: Naveen'

```


<span style="color:#F5B7B1">`Why not great?`</span>

- better than % formatting but still very verbose when dealing with multiple parameters


### Option 3: f-string

This is the most efficient option if you are using Python 3.6 or greater.

<span style="color:#F5B7B1">`How to use it?`</span>

_Example 3.1:_ ___Simple syntax___

```python
>>> name =  "Naveen"
>>> lastname = "Kumar"
>>> f"My name is {name}{lastname}"
'My name is Naveen Kumar'
```

_Example 3.2:_ ___Any expression___

```python
>>> f"{5*2}"
'10'
```
_Example 3.3:_ ___Any function___

```python
def lowercase(x):
	return x.lower()

greetings = 'HELLO'

>>> f"{lowercase(greetings)}"
'hello'

>>> f"{greetings.lower()}"
'hello'
```

_Example 3.4:_ ___Dictionary___
```python
>>> info = {'name': 'Naveen', 'lastname': 'Kumar', 'age': 20}
>>> f"My firstname is {info['name']}. My lastname is {info['lastname']}. My age is {info['age']}."
'My firstname is Naveen. My lastname is Kumar. My age is 20.'
```

_Example 3.5:_ ___Multiline___

```python
>>> name = "Naveen"
>>> lastname = "Kumar"
>>> age = 20
>>> 
>>> info = (
... f"My first name is {name}. "
... f"My last name is {lastname}. "
... f"My age is {age}."
... )
>>> info
'My first name is Naveen. My last name is Kumar. My age is 20.'
```
> You have to put 'f' in front of every line.



