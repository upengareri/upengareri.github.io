---
layout: single
title: <span style="color:#62c462">Downloading data with Python</span>
date: 2018-10-31

---

Here, we go through some of the ways in which we can download files in Python.

> Note: Although we can do a lot with the below mentioned modules, we'll focus only on downloading files.

Let's say we want to download an image from __http://google.com/favicon.ico__

<h2 style="color: #55acee; font-size:26px; font-family: 'Lucida Grande'">Option 1: (for Python 2)</h2>

### import urllib2

```python
import urllib2
url = "http://google.com/favicon.ico"
dest = "./tmp/icon.ico"
filedata = urllib2.urlopen(url)  # returns an object

data_to_write = filedata.read()

with open(dest) as f:
	f.write(data_to_write)

```

<h2 style="color: #55acee; font-size:26px; font-family: 'Lucida Grande'">Option 2: (for Python 3)</h2>

### import urllib.request

```python
import urllib.request
url = "http://google.com/favicon.ico"
dest = "./tmp/icon.ico"

urllib.request.urlretreive(url, dest)
```

<h2 style="color: #55acee; font-size:26px; font-family: 'Lucida Grande'">Option 3: (for both Python 2 and 3)</h2>

### from six.moves.urllib.request import urlretrieve

```python
from six.moves.urllib.request import urlretrieve
url = "http://google.com/favicon.ico"
dest = "./tmp/icon.ico"

urllib.request.urlretreive(url, dest)
```

> Note: ___six.moves___ module makes some modules available in Python 3 to be accessible in Python 2.<br/>
If you want to know more about making your script compatible with both Python 2 and 3, check [targeting_python_2_3](targeting_python_2_3.md)

<h2 style="color: #55acee; font-size:26px; font-family: 'Lucida Grande'">Option 4: (external library)</h2>

### import requests
Since it is a third-party library, you need to install the module.<br/>
To install it using pip, use:

`pip install requests`  (for Python 2)<br/>
`pip3 install requests` (for Python 3)s

```python
import requests
url = "http://google.com/favicon.ico"
dest = "./tmp/icon.ico"

resp = requests.get(url)  # returns the response

with open(dest) as f:
	f.write(resp.content)
```

<h2 style="color: #55acee; font-size:26px; font-family: 'Lucida Grande'">CONCLUSION:</h2>

Personally, I prefer to use requests module as it simple and gives us a lot of features. However, there are cases where you might not be allowed to use third-party library. In that case you can use any of the other three options depending on the environment you are targetting.

To know how to use _requests_ module to download archived files and extract them, check [Downloading and extracting archived files](downloading_and_extracting.md)








