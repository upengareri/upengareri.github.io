---
layout: single
title: <span style="color:#ABB2B9">Targeting Python 2 & 3</span>
date: 2018-10-19

---

Let's say we are creating a very important module which will be used by hundreds of users but not all of them have Python 2 or 3. The first option can be to distribute 2 modules, one for Python 2 and the other for 3. The second option is to create a single module compatible with both 2 and 3. Here, we will use two tricks to make our code compatible with Python 2 and 3.


### Future imports
I'll take an example of division operator to clarify this.
There are basically two types of division in Python - integer or floor division and floating point division

	x=5
	Python 3:
	x / 2 = 2.5 (floating point division)
	x // 2 = 2 (integer or floor division)
	Python 2:
	x / 2 = 2
	x // 2 = 2
	float(x) / 2 = 2.5
	float(x) // 2 = 2.0

Now, the problem here is if we want an accurate result in Python 2 then we need to convert 'x' to float to get floating point result or it'll always result in integer value. 
So, if we are creating a single module for both versions, we can use something like below -

	from __future__ import division
	x / 2

This brings the functionality of division from Python 3 to Python 2 and will always print floating point value.


### Module renaming
Some modules have been changed in Python 3. For example `urllib` is used for fetching URLs. In Python 2 it is called `urllib2` whereas in Python 3 the same functionality is provided under `urllib.request`. An example to use this module that will be compatible with both 2 and 3 is shown below -
	
	try:
		import urllib.request as urllib_request  # for Python 3
	except:
		import urllib2 as urllib_request  # for Python 2

As per the above code, in Python 3, the try block will execute whereas in Python 2, it will try to import try block but since Python 2 does not have `urllib.request` it will go to except block and import urllib2. The significance of `as` keyword is to rename any module and here whether try or except block gets executed the alias in both the case would be `urllib_request`. This way even if except block gets executed, all the classes and methods of urllib2 module will be accessed using `urllib_request`. 


### Summary
* `from __future__ import` : to bring the functionality of Python 3 to Python 2
* `import <module> as <alias> within try-except` : to handle renamed module 







