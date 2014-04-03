# install hadoop 2.2

# hadoop 2.2 64 bit vm warning:
```
    Java HotSpot(TM) 64-Bit Server VM warning: You have loaded library /opt/hadoop-2.2.0/lib/native/libhadoop.so.1.0.0 which might have disabled stack guard. The VM will try to fix the stack guard now.  
    It's highly recommended that you fix the library with 'execstack -c <libfile>', or link it with '-z noexecstack'.  
    13/11/01 10:58:59 WARN util.NativeCodeLoader: Unable to load native-hadoop library for your platform... using builtin-java classes where applicable  
```

solutions: http://blog.csdn.net/focusheart/article/details/14058153

Basically we need to recompile the hadoop by src
```
    $ sudo apt-get install build-essential  
    $ sudo apt-get install g++ autoconf automake libtool cmake zlib1g-dev pkg-config libssl-dev  
    $ sudo apt-get install maven  
```

We need protobuf ( https://protobuf.googlecode.com/files/protobuf-2.5.0.tar.gz)
```
$ wget https://protobuf.googlecode.com/files/protobuf-2.5.0.tar.gz
$ tar xzvf protobuf-2.5.0.tar.gz  
$ cd protobuf-2.5.0  
$ ./configure --prefix=/usr  
$ make  
$ sudo make install  
```

Compile hadoop
```
    $ tar xzvf hadoop-2.2.0-src.tar.gz  
    $ cd hadoop-2.2.0-src  
    $ mvn package -Pdist,native -DskipTests -Dtar  
```

Problems:
### mvn failed to compile the Hadoop Maven Plugins
change jdk from 1.8 to 1.7.

### mvn failed on hadoop-auth 
get this patch https://issues.apache.org/jira/browse/HADOOP-10110

Here should be the compiled hadoop lib
```
hadoop-2.2.0-src/hadoop-dist/target/hadoop-2.2.0/lib  
```

# Hadoop 1.x 
## installation
http://hadoop.apache.org/docs/r1.2.1/single_node_setup.html

## account without kerbos:
http://amalgjose.wordpress.com/2013/02/09/setting-up-multiple-users-in-hadoop-clusters/

set `HADOOP_USER_NAME=remote_user_name` should work on the remote client machine
