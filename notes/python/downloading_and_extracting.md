---
layout: single
title: <span style="color:#62c462">Downloading and extracting archived files</span>
date: 2018-11-03

---
Datasets are important part of Machine Learning and quite often the datasets are provided in a zip file.
In this article we'll cover how to download an archived dataset from any URL and extract it using a python script.

```python
# IMPORTING MODULES
import os
import zipfile
import tarfile
import gzip
import shutil
import requests
```
```python
# ARCHIVE EXTENSIONS
ZIP_EXTENSION = ".zip"
TAR_EXTENSION = ".tar"
TAR_GZ_EXTENSION = ".tar.gz"
TGZ_EXTENSION = ".tgz"
GZ_EXTENSION = ".gz"
```

```python
EMPTY_URL_ERROR = "ERROR: URL should not be empty."
FILENAME_ERROR = "ERROR: Filename should not be empty."
UNKNOWN_FORMAT = "ERROR: Unknown file format. Can't extract."
```

```python
def download_dataset(url, target_path="data/", keep_download=True, overwrite_download=False):
	"""Downloads dataset from a url.
	url: string, a dataset path
	target_path: string, path where data will be downloaded
	keep_download: boolean, keeps the original file after extraction
	overwrite_download: boolean, stops download if dataset already exists
	"""
	if url == "" or url is None:
		raise Exception(EMPTY_URL_ERROR)

	filename = get_filename(url)
	file_location = get_file_location(target_path, filename)

	os.makedirs(data_dir, exist_ok=True)

	if os.path.exists(file_location) and not overwrite_download:
		print(f"File already exists at {file_location}. Use: 'overwrite_download=True' to \
overwrite download")
		extract_file(target_path, filename)
		return

	print(f"Downloading file from {url} to {file_location}.")
	# Download
	with open(file_location, 'wb') as f:
		with requests.get(url, allow_redirects=True, stream=True) as resp:
			for chunk in resp.iter_content(chunk_size = 512):  #chunk_size in bytes
				if chunk:
					f.write(chunk)

	print("Finished downloading.")
	print("Extracting the file now ...")
	extract_file(target_path, filename)

	if not keep_download:
		os.remove(file_location)

```

```python
def extract_file(target_path, filename):
	"""Extract file based on file extension
	target_path: string, location where data will be extracted
	filename: string, name of the file along with extension
	"""
	if filename == "" or filename is None:
		raise Exception(FILENAME_ERROR)

	file_location = get_file_location(target_path, filename)

	if filename.endswith(ZIP_EXTENSION):
		print("Extracting zip file...")
		zipf = zipfile.ZipFile(file_location, 'r')
		zipf.extractall(target_path)
		zipf.close()
	elif filename.endswith(TAR_EXTENSION) or \
		 filename.endswith(TAR_GZ_EXTENSION) or \
		 filename.endswith(TGZ_EXTENSION):
		print("Extracting tar file")
		tarf = tarfile.open(file_location, 'r')
		tarf.extractall(target_path)
		tarf.close()
	elif filename.endswith(GZ_EXTENSION):
		print("Extracting gz file")
		out_file = file_location[:-3]
		with open(file_location, "rb") as f_in:
			with open(out_file, "wb") as f_out:
				shutil.copyfileobj(f_in, f_out)
	else:
		print(UNKNOWN_FORMAT)

```

```python
def get_filename(url):
	"""Extract filename from file url"""
	filename = os.path.basename(url)
	return filename

def get_file_location(target_path, filename):
	""" Concatenate download directory and filename"""
	return target_path + filename
```

### About _requests_ module
Request module is useful when downloading large files. I prefere to use this module when the size of the file is more than 500MB. In the above code, the important thing to discuss is <span style="color: #55acee;background-color: #1E242C;font-size:14px; font-family: 'Lucida Grande'">`stream`</span> parameter of <span style="color: #55acee;background-color: #1E242C;font-size:14px; font-family: 'Lucida Grande'">requests.get</span> method. <br/>

If <span style="color: #55acee;background-color: #1E242C;font-size:14px; font-family: 'Lucida Grande'">`stream`</span> is set to <span style="color: #55acee;background-color: #1E242C;font-size:14px; font-family: 'Lucida Grande'">`False`</span> then the entire file gets downloaded into memory and if the file size is too large, then it can be an issue with the memory consumption.<br/>
If <span style="color: #55acee;background-color: #1E242C;font-size:14px; font-family: 'Lucida Grande'">`stream`</span> is set to <span style="color: #55acee;background-color: #1E242C;font-size:14px; font-family: 'Lucida Grande'">`True`</span>, then the download does not start immediately. Instead, only the header is downloaded and the connection remains open. This way we can either go with the download or we can cancel it (depending on header info). The file gets downloaded only when we use the <span style="color: #55acee;background-color: #1E242C;font-size:14px; font-family: 'Lucida Grande'">`content`</span> property or iterate over the content with <span style="color: #55acee;background-color: #1E242C;font-size:14px; font-family: 'Lucida Grande'">`iter_content`</span>.  <br/>
The <span style="color: #55acee;background-color: #1E242C;font-size:14px; font-family: 'Lucida Grande'">`content`</span> property puts the entire content into the memory which we should try to avoid for bigger files whereas the <span style="color: #55acee;background-color: #1E242C;font-size:14px; font-family: 'Lucida Grande'">`iter_content`</span> loads the file in chunks into the memory.
