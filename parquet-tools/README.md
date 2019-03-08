
http://logservice-resource.oss-cn-shanghai.aliyuncs.com/tools/parquet-tools-1.6.0rc3-SNAPSHOT.jar?spm=a2c63.p38356.a3.6.74ea44dfoTlulH&file=parquet-tools-1.6.0rc3-SNAPSHOT.jar
[下载](http://logservice-resource.oss-cn-shanghai.aliyuncs.com/tools/parquet-tools-1.6.0rc3-SNAPSHOT.jar?spm=a2c63.p38356.a3.6.74ea44dfoTlulH&file=parquet-tools-1.6.0rc3-SNAPSHOT.jar)
## 查看Parquet文件schema
```
$ java -jar parquet-tools-1.6.0rc3-SNAPSHOT.jar schema -d 00_1490803532136470439_124353.snappy.parquet | head -n 30
message schema {
  optional int32 __time__;
  optional binary ip;
  optional binary __source__;
  optional binary method;
  optional binary __topic__;
  optional double seq;
  optional int64 status;
  optional binary time;
  optional binary url;
  optional boolean ua;
}
creator: parquet-cpp version 1.0.0
file schema: schema
--------------------------------------------------------------------------------
__time__: OPTIONAL INT32 R:0 D:1
ip: OPTIONAL BINARY R:0 D:1
.......
```

## 查看Parquet文件全部内容
```
$ java -jar parquet-tools-1.6.0rc3-SNAPSHOT.jar head -n 2 00_1490803532136470439_124353.snappy.parquet
__time__ = 1490803230
ip = 10.200.98.220
__source__ = *.*.*.*
method = POST
__topic__ =
seq = 1667821.0
status = 200
time = 30/Mar/2017:00:00:30 +0800
url = /PutData?Category=YunOsAccountOpLog&AccessKeyId=*************&Date=Fri%2C%2028%20Jun%202013%2006%3A53%3A30%20GMT&Topic=raw&Signature=********************************* HTTP/1.1
__time__ = 1490803230
ip = 10.200.98.220
__source__ = *.*.*.*
method = POST
__topic__ =
seq = 1667822.0
status = 200
time = 30/Mar/2017:00:00:30 +0800
url = /PutData?Category=YunOsAccountOpLog&AccessKeyId=*************&Date=Fri%2C%2028%20Jun%202013%2006%3A53%3A30%20GMT&Topic=raw&Signature=********************************* HTTP/1.1
```


更多用法请执行：java -jar parquet-tools-1.6.0rc3-SNAPSHOT.jar -h，参考帮助。

<!--
  ~ Licensed to the Apache Software Foundation (ASF) under one
  ~ or more contributor license agreements.  See the NOTICE file
  ~ distributed with this work for additional information
  ~ regarding copyright ownership.  The ASF licenses this file
  ~ to you under the Apache License, Version 2.0 (the
  ~ "License"); you may not use this file except in compliance
  ~ with the License.  You may obtain a copy of the License at
  ~
  ~   http://www.apache.org/licenses/LICENSE-2.0
  ~
  ~ Unless required by applicable law or agreed to in writing,
  ~ software distributed under the License is distributed on an
  ~ "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
  ~ KIND, either express or implied.  See the License for the
  ~ specific language governing permissions and limitations
  ~ under the License.
  -->

Parquet Tools
======

Parquet-Tools contains java based command line tools that aid
in the inspection of [Parquet files](https://parquet.apache.org).

Currently these tools are available for UN*X systems.

## Build

If you want to use parquet-tools in local mode, you should use the local profile so the 
hadoop client dependency is included.

```sh
cd parquet-tools && mvn clean package -Plocal 
```

To use it in hadoop mode, the default profile will exclude the hadoop client dependency

```sh
cd parquet-tools && mvn clean package 
```

The resulting jar is target/parquet-tools-<Version>.jar, you can copy it to the place where you
want to use it

#Run from hadoop

See Commands Usage for command to use

```sh
hadoop jar ./parquet-tools-<VERSION>.jar <command> my_parquet_file.lzo.parquet
```

#Run locally

See Commands Usage for command to use

```
java -jar ./parquet-tools-<VERSION>.jar <command> my_parquet_file.lzo.parquet
```

## Commands Usage

To see usage instructions for all commands: 

```
java -jar ./parquet-tools-<VERSION>.jar --help
```

**Note:** To run it on hadoop, you should use `hadoop jar` instead of `java -jar`

## Meta Legend

### Row Group Totals

Acronym | Definition
--------|-----------
RC | Row Count
TS | Total Byte Size

### Row Group Column Details

Acronym | Definition
--------|-----------
DO | Dictionary Page Offset
FPO | First Data Page Offset
SZ:{x}/{y}/{z} | Size in bytes. x = Compressed total, y = uncompressed total, z = y:x ratio
VC | Value Count
RLE | Run-Length Encoding
