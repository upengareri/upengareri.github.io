---
layout: single
title: <span style="color:#62c462">Extracting archived files</span>
date: 2018-11-01

---

Python has different in-built modules to deal with different types of archived files.
In this article we'll talk about extracting different archived extensions (specifically .tar, .tar.gz,
.tgz, .gz, .zip). <br/>
To know more about these extensions check [compression and archiving.](https://upengareri.github.io/compression_and_archiving)

```python
# Importing required modules
import zipfile  # for .zip
import tarfile  # for .tar, .tar.gz, .tgz
import gzip   # for .gz 
import shutil  # for copying .gz object
```

```python
# EXTENSIONS
ZIP_EXTENSION = ".zip"
TAR_EXTENSION = ".tar"
TAR_GZ_EXTENSION = ".tar.gz"
TGZ_EXTENSION = ".tgz"
GZ_EXTENSION = ".gz"
```

```python
FILENAME_ERROR = "ERROR: Filename should not be empty."
UNKNOWN_FORMAT = "ERROR: Unknown file format. Can't extract."

# EXTRACTION 
def extract_file(filename, out_dir="data/"):
	if filename == "" or filename is None:
		raise Exception(FILENAME_ERROR)
	if filename.endswith(ZIP_EXTENSION):
		print("Extracting zip file...")
		zipf = zipfile.ZipFile(filename, 'r')
		zipf.extractall(zipf, out_dir)
		zipf.close()
	elif filename.endswith(TAR_EXTENSION) or \
		 filename.endswith(TAR_GZ_EXTENSION) or \
		 filename.endswith(TGZ_EXTENSION):
		print("Extracting tar file")
		tarf = tarfile.open(filename, 'r')
		tarf.extractall(tarf, out_dir)
		tarf.close()
	elif filename.endswith(GZ_EXTENSION):
		print("Extracting gz file")
		out_file = filename[:-3]
		with open(filename, "rb") as f_in:
			with open(out_file, "wb") as f_out:
				shutil.copyfileobj(f_in, f_out)
	else:
		print(UNKNOWN_FORMAT)

```

> Checkout the below link on how to download and extract a dataset from any url.<br/>
 [Downloading and extracting archived files](downloading_and_extracting.md)
