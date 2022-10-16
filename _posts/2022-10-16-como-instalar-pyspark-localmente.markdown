---
title: "How to install Pyspark locally"
layout: post
date: 2022-10-16 22:48
image: /assets/images/blog/2021-12-11-como-acessar-jupyter-remoto/banner.png
headerImage: false
tag:
- pyspark
- elements
star: true
category: blog
author: emdemor
description: CHow to install pyspark in a local machine
---

# Pyspark Installation

1. Check whether pip is intalled
	```
    $ sudo apt install python3-pip
    ```

2. Check whether jupyter is intalled
	```
    $ pip3 install jupyter
    ```

3. Install Java
	```
    $ sudo apt-get install default-jre
    ```

4. Install Scala
	```
    $ sudo apt-get install scala
    ```

5. Install py4j
	```
    $ pip3 install py4j 
    ```

6. Install Spark
	- Access [https://spark.apache.org/downloads.html](https://spark.apache.org/downloads.html), download the file `spark-X.X.X-bin-hadoopX.tgz` and move it to your home directory.
	- In home directory:
		```
        $ sudo tar -zxvf spark-X.X.X-bin-hadoopX.tgz
        ```

7. Set environment variables

	export SPARK_HOME=/home/risknow/spark

	export PATH=$PATH:$SPARK_HOME/bin:$SPARK_HOME/sbin

	export PATH=$PATH:$SPARK_HOME/bin:$SPARK_HOME/bin

	export PYTHONPATH="${PYTHONPATH}:$SPARK_HOME/python"

	export PYSPARK_PYTHON=python3

	export PYSPARK_DRIVER_PYTHON="jupyter"

	export PYSPARK_DRIVER_PYTHON_OPTS="notebook"