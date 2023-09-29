# Hadoop-MapReduce
Hadoop MapReduce Java 

#### Hadoop Installation
### Install hadoop via Homebrew
```
$ brew install hadoop
```
### Install JavaSDK8
```
$ ls /Library/Java/JavaVirtualMachines/
$ sudo rm -rf /Library/Java/JavaVirtualMachines/jdk-13.0.1.jdk/

$ brew tap adoptopenjdk/openjdk
$ brew cask install adoptopenjdk8
```
### Check JAVA path
```
$ /usr/libexec/java_home
/Library/Java/JavaVirtualMachines/jdk1.8.0_251.jdk/Contents/Home
```

### Configure hadoop files
* **core-site.xml**
```
<!-- Put site-specific property overrides in this file. -->
<configuration>
  <property>
    <name>hadoop.tmp.dir</name>
    <value>/Users/rohinjoshi/hadoop/hdfs/tmp</value>
    <description>A base for other temporary directories</description>             
  </property>
  <property>
    <name>fs.default.name</name>
    <value>hdfs://localhost:8020</value>
  </property>
</configuration>
```

* **mapred-site.xml**
```
<configuration>
  <property>
    <name>mapred.job.tracker</name>
    <value>localhost:8021</value>
  </property>
</configuration>
```

* **hdfs-site.xml**
```
<configuration>
  <property>
    <name>dfs.replication</name>
    <value>1</value>
  </property>
</configuration>
```

### Authorize SSH Keys
```
$ ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa
$ cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
$ chmod 0600 ~/.ssh/authorized_keys
```

### Enable Remote Login Preferences > Sharing
```
$ ssh localhost
Last login: Thu Apr 16 12:19:27 2020
```
### Format
```
$ cd /usr/local/opt/hadoop
$ hdfs namenode -format
```

### Adding shortcuts and path - ```~/.bash_profile```
```
export JAVA_HOME=$(/usr/libexec/java_home)
alias hstart="/opt/homebrew/Cellar/hadoop/3.3.6/sbin/start-all.sh"
alias hstop="/opt/homebrew/Cellar/hadoop/3.3.6/sbin/stop-all.sh"
export HADOOP_HOME=/opt/homebrew/Cellar/hadoop/3.3.6/libexec
```
### Save and Run
```
$ source ~/.bash_profile
```

### To start hdfs service
```
$ hstart
```

### Check all services
```
Resource Manager: http://localhost:9870/
JobTracker: http://localhost:8088/
Node Specific Info: http://localhost:8042/
```

### To stop hdfs service
```
$ hstop
```


#### MapReduce commands
### Start hdfs service
```
$ hstart
```

### Check the availability of all the nodes
```
$ jps
```

### Create Input directory
```
$ hdfs dfs -mkdir [PATH_WITH_NAME]
```
Example
```
$ hdfs dfs -mkdir /input
```

### Move dataset to Input directory
```
$ hdfs dfs -put [DATSET_PATH] [INPUT_DIRECTORY_ON_HDFS]
```
Example
```
$ hdfs dfs -put /data.csv /input
```

### Run MapReduce with created JAR
```
$ hadoop jar [JAR_PATH] [CLASS_NAME] [INPUT_DIRECTORY_ON_HDFS]  [OUTPUT_DIRECTORY_ON_HDFS]
```
Example
```
$ hadoop jar /target/hadoop_mapRed_marks-1.0-SNAPSHOT.jar org.RohinJoshi.StudentScoreCount /input /output
```

### Output - IN BROWSER
```
http://localhost:9870
(GOTO - Utilities > Browse the file system)
```

### To remove HDFS directory
```
$ hdfs dfs -rm -r -f [DIRECTORY_PATH]
```
Example
```
$ hdfs dfs -rm -r -f /output
```

### Stop hdfs service
```
$ hstop
```

### Problem
Use the Hadoop MapReduce programming framework to come up with a Program which will take the data from this .csv file and computes the following
1. Total number of students who have scored more than 60 in Subject 1

