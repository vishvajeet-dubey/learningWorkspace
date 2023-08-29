# INSTALLATION

## Anaconda navigator Installation
* [Download](https://repo.anaconda.com/archive/Anaconda3-2023.07-2-Linux-x86_64.sh) the .sh file from official page
* Write the below command to extract the .sh file</br>
```
bash ~/Downloads/Anaconda3-2020.05-Linux-x86_64.sh 
```
* follow the office installation steps [link](https://docs.anaconda.com/free/anaconda/install/linux/)

## PySpark installation
* Follow the steps from [link](https://sparkbyexamples.com/pyspark/install-pyspark-in-anaconda-jupyter-notebook/)
* Prerequisite:
1. Python/Anaconda installed
2. openjdk installed
* Write below command inside conda bash
```
conda install pyspark
```
* **install findspark** In order to run PySpark in Jupyter notebook first, you need to find the PySpark Install, I will be using findspark package to do so. Since this is a third-party package we need to install it before using it.

```
conda install -c conda-forge findspark
```
* validate the pySpark by launching the notebook

## Spark installation
* follow the [link](https://sparkbyexamples.com/spark/spark-installation-on-linux-ubuntu/) to install spark on top of linux
* [Download](https://www.apache.org/dyn/closer.lua/spark/spark-3.4.1/spark-3.4.1-bin-hadoop3.tgz) Apache Spark .tar file from office site.
* unzip the file using below command
```
tar -xzf spark-3.0.1-bin-hadoop2.7.tgz
```
* By using below command set environment variable.
```
sparkuser@sparknode:~$ vi ~/.bashrc
# Add below lines at the end of the .bashrc file.
export SPARK_HOME=/home/sparkuser/spark
export PATH=$PATH:$SPARK_HOME/bin
```
* launch the `spark-shell` to test the spark.

## Almond kernel for scala jupyter notebook installation
* Follow the [link](https://almond.sh/docs/quick-start-install) to install almond kernel.
* Run the below command to make sure java jdk should installed
```
$ java -version
java version "1.8.0_121"
Java(TM) SE Runtime Environment (build 1.8.0_121-b13)
Java HotSpot(TM) 64-Bit Server VM (build 25.121-b13, mixed mode)
```
* 
# Scala almond kernel Instructions for Linux

*Note: These instructions are over 3 years old. Please consult the Scala docs and
the [Almond docs](https://almond.sh/docs/quick-start-install) for up-to-date instructions.*

1. Download Scala https://www.scala-lang.org/download/

   - check Java version (`java -version`)

2. Almond can then be fetched and installed with coursier, like
```
$ curl -Lo coursier https://git.io/coursier-cli
$ chmod +x coursier
$ ./coursier launch --fork almond -- --install
$ rm -f coursier
```

Note the -- before --install, separating the arguments passed to Almond from the ones handled by coursier.  
You can specify explicit Almond and / or Scala versions, like
```
$ ./coursier launch --fork almond:0.10.0 --scala 2.12.11 -- --install
```

Short Scala versions, like just 2.12 or 2.13, are accepted too. The available versions of Almond can be found here. Not all Almond and Scala versions combinations are available. See the possible combinations here).

* Equivalent Windows command
    Once the kernel is installed, you can use it within Jupyter or nteract.

* Getting help about the launcher
    pass --help instead of --install, like
```
$ ./coursier launch --fork almond -- --help
```

* Update the almond kernel
    To update the almond kernel, just re-install it, but passing the --force option to almond (like ./coursier launch --fork almond -- --install --force). That will override any previous almond (or kernel with name scala).

* Uninstall the almond kernel
    To uninstall the almond kernel, use jupyter kernelspec remove scala.
