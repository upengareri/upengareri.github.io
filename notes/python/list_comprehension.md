---
layout: single
title: <span style="color:#62c462">Using list comprehension</span>
date: 2018-12-15

---

In this article, I will try to cover some of the use cases and style of coding when it comes to list comprehension (LC).
For beginners, I'll also compare the list comprehension with 'for loop' approach.

> List comprehension is an alternative to for-loop and is generally faster in time execution

### A simple list
`Using for-loop`
```python
	num_list = []
	for item in range(10):
		num_list.append(item)
```

`Using LC`
```python
	[item for item in range(10)]
```

`Output:`<br/>
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

### List with conditionals

<span style="color: #55acee;background-color: #1E242C;font-size:16px; font-family: 'Lucida Grande'">I. List with if condition</span><br/>

`Using for-loop`
```python
	even_list = []
	for item in range(10):
		if item % 2 == 0:
			even_list.append(item)
```

`Using LC`
```python
	[item for item in range(10) if item % 2 == 0]
```

`Output:`<br/>
[0, 2, 4, 6, 8]

<span style="color: #55acee;background-color: #1E242C;font-size:16px; font-family: 'Lucida Grande'">II. List with multiple if conditions</span><br/>

`Using for-loop`
```python
	num_list = []
	for item in range(10):
		if item % 2 == 0:
			if item % 3 == 0:
				num_list.append(item)
```

`Using LC`
```python
	[item for item in range(10) if item % 2 == 0 if item % 3 == 0]
```

`Output:`<br/>
[0, 6]

<span style="color: #55acee;background-color: #1E242C;font-size:16px; font-family: 'Lucida Grande'">III. List with if-else conditions</span><br/>

`Using for-loop`
```python
	num_list = []
	for item in range(10):
		if item % 2 == 0:
			num_list.append(item)
		else:
			num_list.append(str(item))


```

`Using LC`
```python
	[item if item % 2 == 0 else str(item) for item in range(10)]
```

`Output:`<br/>
`[0, '1', 2, '3', 4, '5', 6, '7', 8, '9']`

> In general, for only 'if' condition the syntax goes after the for loop but for 'if-else' it goes before the for loop.

### Two for-loops

<span style="color: #55acee;background-color: #1E242C;font-size:16px; font-family: 'Lucida Grande'">Example I</span><br/>

```python
	matrix = [[1,2,3], [4,5,6],[7,8,9]]
```

`Using for-loop`
```python
	flattened_ = []
	for row in matrix:
		for element in row:
			flattened_.append(element)
```

`Using LC`
```python
flattened_ = [element for row in matrix for element in row]
```
`Output:`<br/>
`[1, 2, 3, 4, 5, 6, 7, 8, 9]`

<span style="color: #55acee;background-color: #1E242C;font-size:16px; font-family: 'Lucida Grande'">Example II</span><br/>

```python
	non_flattened = [[1,2,3], [4,5,6],[7,8]]
```

`Using for-loop`
```python
	flattened_ = []
	for row in non_flattened:
		if len(row) > 2:
			for element in row:
				flattened_.append(element)
```

`Using LC`
```python
flattened_ = [element for row in non_flattened if len(row) > 2 for element in row]
```
`Output:`<br/>
`[1, 2, 3, 4, 5, 6]`

> The order of LC following the same convention as the traditional for-loop.

<span style="color: #55acee;background-color: #1E242C;font-size:16px; font-family: 'Lucida Grande'">Example III</span><br/>

```python
	matrix = [[1,2,3], [4,5,6],[7,8,9]]
```

`Using for-loop`
```python
	transposed_ = []
	for i in range(3):
		transposed_row = []
			for row in matrix:
				transposed_row.append(row[i])
			transposed_.append(transposed_row)
```

`Using LC`
```python
transposed_ = [[row[i] for row in matrix] for i in range(3)]
```
`Output:`<br/>
`[[1, 4, 7], [2, 5, 8], [3, 6, 9]]`

> Here, the flow of execution is backwards because of square bracket within the LC.

### Conclusion:

* List comprehension is fast and quite pythonic way of coding compared to traditional for-loop.
* Although I have not talked about map, reduce, filter and lamda in this article, but LC is more favoured and serves the purpose more clearly than the latter ones.
* We also have something called generator expressions which are quite useful when dealing with arrays with huge size.
* I'll try to cover generators in future article but for now just remember that for very large arrays generators are much faster than LC. This is because for big arrays LC takes a large chunk of space in RAM and processing becomes slow.




