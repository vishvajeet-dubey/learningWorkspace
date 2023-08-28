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
# Scala Kernel Instructions for MacOS

*Note: These instructions are over 3 years old. Please consult the Scala docs and
the [Almond docs](https://almond.sh/docs/quick-start-install) for up-to-date instructions.*

1. Download Scala https://www.scala-lang.org/download/

   - check Java version (`java -version`)
   - Install Scala sbt `brew install sbt@1`
     ```
     You can use $SBT_OPTS to pass additional JVM options to sbt.
     Project specific options should be placed in .sbtopts in the root of your project.
     Global settings should be placed in /usr/local/etc/sbtopts

2. Install coursier

   `brew install --HEAD coursier/formulas/coursier`

3. Install almond

   - `git clone https://github.com/willingc/almond.git`
   - edit `project/plugin.sbt`
      - add `addSbtPlugin("io.get-coursier" % "sbt-coursier" % "1.1.0-SNAPSHOT")`
   - bootstrap install

     ```
     coursier bootstrap \
     →     -i user -I user:sh.almond:scala-kernel-api_$SCALA_VERSION:$ALMOND_VERSION \
     →     sh.almond:scala-kernel_$SCALA_VERSION:$ALMOND_VERSION \
     →     -o almond
     ```

   - `./almond --install`

