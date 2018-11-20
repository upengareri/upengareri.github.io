---
layout: single
title: <span style="color:#62c462">Generating random numbers in Python and Numpy</span>
date: 2018-11-19

---

Most random number generators are not fully random. They are <span style="color: #FE9A70; font-family: 'Lucida Grande'">`pseudorandom numbers`</span>.<br/>
These numbers are generated using <span style="color: #55acee;background-color: #1E242C;font-size:14px; font-family: 'Lucida Grande'">`pseudorandom number generator (PRNG)`</span>. <br/>
PRNG is any algorithm for generating random numbers <span style="color: #FE9A70; font-family: 'Lucida Grande'">`which are reproducible`</span>.

___

The second type of number generator is <span style="color: #55acee;background-color: #1E242C;font-size:14px; font-family: 'Lucida Grande'">`truerandom number generator (TRNG)`</span>. They generate true random numbers.

---

PRNGs are done using software while TRNGs are done using hardware. In this article, we'll only talk about PRNGs.

____ 
### What do we mean by "not fully random" or "random numbers which are reproducible"?

Let's take a simple example to illustrate this.

```python
class NotSoRandom(object):
	def seed(self, val=2):
		"""handles the initial value for random number generation"""
		self.seedval = val

	def random(self):
		"""generates a random value based on seed value"""
		self.seedval = (self.seedval * 3) % 15
		return self.seedval

rand_obj = NotSoRandom()
seed = rand_obj.seed
random = rand_obj.random

seed(1234)
print([random() for _ in range(10)])
seed(1234)
print([random() for _ in range(10)])
```
```python
# OUTPUT:
[12, 6, 3, 9, 12, 6, 3, 9, 12, 6]
[12, 6, 3, 9, 12, 6, 3, 9, 12, 6]
```

- The random numbers generated depends on the seed value
- If the seed is set to the same value, the random numbers can be reproduced. 

Hence the random module documentation also mentions something that you don't want to miss:

> Warning: The pseudo-random generators of this module should not be used for security purposes.

> For security purpose one can use cryptographically secure pseudorandom number generator (CSPRNG).

Now that we have a rough idea of pseudorandom number generators, let's talk about the various use cases of random module. 

> Before diving into the code, one important thing to note is that Python's random module is mostly used for generating a single pseudorandom number or one-dimensional pseudorandom numbers containing few random items/numbers. Similarly, numpy's random module is used for creating multi-dimensional pseudorandom numbers. The above two sentences will become more clear with the code and example.


## The `random` module

<span style="color: #55acee;background-color: #1E242C;font-size:18px; font-family: 'Lucida Grande'">`1. Float number between [0,1) - `</span><span style="font-weight: bold;color: #FE9A70;">`random()`</span>

> - Includes 0 and excludes 1

```python
>>> import random
>>> random.random() 
```
```python
>>> random.seed(123)  # With seed
>>> random.random()
0.052363598850944326
>>> random.random()
0.08718667752263232
>>> 
>>> random.seed(123)  # Re-seed
>>> random.random()
0.052363598850944326
>>> random.random()
0.08718667752263232
```


<span style="color: #55acee;background-color: #1E242C;font-size:18px; font-family: 'Lucida Grande'">`2. Float number between range [x,y] - `</span><span style="font-weight: bold;color: #FE9A70;">`uniform()`</span>

> - Includes x and y

```python
>>> random.uniform(10,20)
14.072417636703983
```

<span style="color: #55acee;background-color: #1E242C;font-size:18px; font-family: 'Lucida Grande'">`3. Integer between range [x,y] - `</span><span style="font-weight: bold;color: #FE9A70;">`randint()`</span>

> - Includes x and y<br/>
- With <span style="font-weight: bold;color: #FE9A70;">`random.randrange(x,y)`</span> one can exlude the right hand side of the interval

```python
>>> random.randint(10,20)
11
```

<span style="color: #55acee;background-color: #1E242C;font-size:18px; font-family: 'Lucida Grande'">`4. To pick one random element from a sequence (like a list or a tuple) - `</span><span style="font-weight: bold;color: #FE9A70;">`choice()`</span>
```python
>>> items = ["one", "two", "three", "four", "five"]
>>> random.choice(items)
'one'
>>> random.choice(items)
'four'
```

<span style="color: #55acee;background-color: #1E242C;font-size:18px; font-family: 'Lucida Grande'">`5. To pick multiple random elements from a sequence with replacement (duplicate possible) - `</span><span style="font-weight: bold;color: #FE9A70;">`choices()`</span>
```python
>>> random.choices(items, k=3)
['five', 'one', 'two']
>>> random.choices(items, k=2)
['two', 'two']
```

<span style="color: #55acee;background-color: #1E242C;font-size:18px; font-family: 'Lucida Grande'">`6. To pick multiple random elements from a sequence without replacement (no duplicates) - `</span><span style="font-weight: bold;color: #FE9A70;">`sample()`</span>
```python
>>> random.sample(items, k=2)
['one', 'two']
>>> random.sample(items, k=4)
['two', 'one', 'five', 'three']
```

<span style="color: #55acee;background-color: #1E242C;font-size:18px; font-family: 'Lucida Grande'">`7. To shuffle/ randomize elements of a sequence in-place - `</span><span style="font-weight: bold;color: #FE9A70;">`shuffle()`</span>
```python
>>> items
['one', 'two', 'three', 'four', 'five']
>>> random.shuffle(items)
>>> items
['one', 'three', 'two', 'four', 'five']
>>> items
['one', 'three', 'two', 'four', 'five']
```

## Random sequence of arrays: `numpy.random`

As said earlier, most of python's random module returns a scalar random value. To generate sequence of random values we can either use python's list comprehension or `numpy.random`. 

```python
>>> [random.random() for _ in range(5)]  # using list comprehension
[0.8378376441951344, 0.7687947474799836, 0.3434621581559646, 0.801496591292033, 0.2068624706661114]
```
```python
>>> np.random.randn()
0.7170764416798703
>>> np.random.rand()  # using numpy
0.5460660016017443
```

> - `numpy.random` is most useful in generating multi-dimensional array of random numbers.

```python
>>> np.random.rand(2,2)  # 2 rows and 2 columns
array([[0.34054351, 0.50084858],
       [0.14742627, 0.61051125]])
```


All the methods of python's random module are also available in numpy's random module. The below table summarizes the different random functions of both the python and numpy modules.

|Python `random` |  | | Numpy `random` | Use case|
|-|-|-|-|-|
| random() |  | | rand() | random float in [0,1)|
| uniform(a,b) |  | | uniform() | random float in [a,b] |
| randint(a,b) |  | | random_integers() | random integer in [a,b] |
| randrange(a,b) |  | | randint() | random integer in [a,b) |
| choice(seq) |  | | choice()) | random element from seq |
| choices(seq,k=1) |  | | choice() | random k elements from seq with replacement |
| sample(seq,k=1) |  | | choice with replace=False | random k elements from seq without replacement |
| shuffle(seq) |  | | shuffle | shuffle seq in-place |


> Numpy is fast for high-dimensional array manipulation. For single or small sequence of random numbers, python's `random` module will suffice and may even be faster than numpy's random module.
