---
layout: single
title:  "AWS EC2 set-up and access through local Jupyter Notebook"
date:   2020-03-11
comments: true
---

## AWS EC2 PySpark Setup PLAN

    1. Create EC2 instance on AWS
    2. Use SSH to connect to EC2 over internet (for Mac)
    3. Set-up Spark and Jupyter on EC2 instance

So, let's get started.

### 1. Create EC2 instance on AWS

* Login to AWS Console --> go to ec2 --> create instance
    
    * __OS__: select machine image (Ubuntu)
    * __CPU__: select instance type (free version with 1 2.5 GHz Intel Xeon CPU and 1GB memory)
    * __NUMBER OF INSTANCES__: select default instance details (i.e number of instance = 1, for free version)
    * __HARD-DISK__: select default storage (8GB SSD)
    * __TAG INSTANCE__: basically name of the instance
    * __CREATE SECURITY__: from dropdown select ALL TRAFFIC
    * __LAUNCH INSTANCE__: create KEY-VALUE PAIR and download the PRIVATE RSA key

That's it for STEP 1. 

All we had to do was create an instance and download the `private RSA key`.

### 2. SSH to connect to connect to EC2

* Change mode of downloaded RSA key to read mode

    `chmod 400 download_rsa_filename`
* Use ssh command to connect to the EC2 instance using the public DNS of your instance given in AWS console

    `ssh -i downloaded_rsa_filename ubuntu@DNS_ADDRESS`

> _Change __downloaded_rsa_filename__ and __DNS_ADDRESS__ with the right values_.

That's it for STEP 2.

### 3. Set-up Spark and Jupyter on EC2 instance

    3.1 Download and install Spark
    3.2 Install Jupyter notebook
    3.3 Connect with PySpark
    3.4 Access EC2 Jupyter notebook in our local browser

Below is a bash script that I used to achieve the above goal -
```bash
#!/bin/bash

echo 'sudo apt-get update'
sudo apt-get update > /dev/null

echo 'sudo apt install python3-pip -y'
sudo apt install python3-pip -y > /dev/null

echo 'pip3 install jupyter'
pip3 install jupyter > /dev/null

echo 'sudo apt-get install default-jre -y'
sudo apt-get install default-jre -y > /dev/null

echo 'sudo apt-get install scala -y'
sudo apt-get install scala -y > /dev/null

echo 'pip3 install py4j'
pip3 install py4j > /dev/null

echo 'wget http://archive.apache.org/dist/spark/spark-2.4.5/spark-2.4.5-bin-hadoop2.7.tgz'
wget http://archive.apache.org/dist/spark/spark-2.4.5/spark-2.4.5-bin-hadoop2.7.tgz > /dev/null

echo 'sudo tar -zxvf spark-2.4.5-bin-hadoop2.7.tgz'
sudo tar -zxvf spark-2.4.5-bin-hadoop2.7.tgz > /dev/null

echo 'sudo rm -r spark-2.4.5-bin-hadoop2.7.tgz'
sudo rm -r spark-2.4.5-bin-hadoop2.7.tgz > /dev/null
 
cd ~

echo 'pip3 install findspark'
pip3 install findspark > /dev/null

cd ~

echo 'export PATH=$PATH:~/.local/bin'
export PATH=$PATH:~/.local/bin

echo 'jupyter notebook --generate-config'
jupyter notebook --generate-config > /dev/null

cd ~

echo "sudo openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem -subj '/C=DE/ST=Munich'"
mkdir certs
cd certs
# touch ~/.rnd
sudo openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem -subj '/C=DE/ST=Munich' > /dev/null
sudo chmod 777 mycert.pem

cd ~

echo 'jupyter echos'
echo "c = get_config()" >> ~/.jupyter/jupyter_notebook_config.py
echo "c.NotebookApp.certfile = u'/home/ubuntu/certs/mycert.pem'" >> ~/.jupyter/jupyter_notebook_config.py
echo "c.NotebookApp.ip = '0.0.0.0'" >> ~/.jupyter/jupyter_notebook_config.py
echo "c.NotebookApp.allow_origin = '*'" >> ~/.jupyter/jupyter_notebook_config.py
echo "c.NotebookApp.open_browser = False" >> ~/.jupyter/jupyter_notebook_config.py
echo "c.NotebookApp.port = 8888" >> ~/.jupyter/jupyter_notebook_config.py
cd ~
jupyter notebook
``` 
To use this shell script -

After connecting to EC2 instance using SSH i.e STEP 2, the terminal would be showing something like `ubuntu@SOME-IP-ADDRESS`. 

In terminal do the following -
```
nano ec2_spark_setup.sh
```
and copy paste the script data to this newly created file and save it. After that
```
chmod 700 ec2_spark_setup.sh
```
And now just run the shell script by
```
./ec2_spark_setup.sh
```

> This script should install everything needed to get you going.

You can adapt the above script for your settings such as the `spark version` as well as the `location (/C=DE/ST=Munich)`

Now, we just need to change the localhost of jupyter notebook opened in the local browser to public dns of the EC2 instance and we are done.

> NOTE: To use pyspark in your notebook, you need to use findspark module
```
import findspark
findspark.init("/home/ubuntu/spark-2.4.5-bin-hadoop2.7")  # location of your spark directory
```

#### Troubleshoot

As of Spark 2.4.x -

Spark runs on Java 8, Python 2.7+/3.4+ and R 3.1+. 
For the Scala API, Spark 2.4.4 uses Scala 2.12. You will need to use a compatible Scala version (2.12.x)

I found that the default java installed in my AWS instance was Java 11 and because of which some spark functions weren't running (crashing).
So, I had to change the java version in my instance to __Java 8__.

If you face the same issue, you can follow the following steps - 
```
sudo apt-get purge --auto-remove openjdk*
sudo apt install openjdk-8-jre
```

