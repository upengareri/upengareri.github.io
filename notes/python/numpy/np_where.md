---
layout: single
title: <span style="color:#62c462">Finding elements in an array using numpy.where()</span>
date: 2018-11-22

---

In order to find some specific elements or indexes of those elements from an array we can use `np.where`.
It returns all those indexes that are true or associated with true condition.

#### Get 12 random numbers between [10,50)
```python
import numpy as np
>>> x = np.random.randint(10,50,12)
>>> x
array([14, 38, 16, 24, 21, 14, 19, 41, 10, 40, 49, 11])

``` 

#### Get index where element is more than 20
```python
>>> idx_21 = np.where(x>20)
>>> idx_21
(array([ 1,  3,  4,  7,  9, 10]),) 
```
#### Get elements which are more than 20
```python
>>> x[idx_21]
array([38, 24, 21, 41, 40, 49])
```

Another famous use case of `np.where` is to find images from a batch for which the predictions are either right or wrong.
Example:


```python
pred = [0,0,1,0,1,1]
actual = [0,0,0,0,1,0]

def rand_mask(mask): return np.random.choice(np.where(mask)[0], min(len(pred), 2), replace=False)
def rand_correct(is_correct): return rand_mask((pred == actual) == is_correct)

```
#### Get random indexes where prediction is correct
```python
idxs_correct = rand_correct(True)
```

#### Get random indexes where prediction is incorrect
```python
idxs_incorrect = rand_correct(False)
```

#### Get random images based on the correct or incorrect predicted indexes
```python
imgs_correct = [images[id] for id in idxs_correct]
imgs_incorrect = [images[id] for id in idxs_incorrect]
```

