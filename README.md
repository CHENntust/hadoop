# Hadoop - Establish NameNode and DataNode

## HDFS分散式檔案系統

*    硬體故障式常態而非異常。

*    Streaming存取資料，犧牲反應時間來提高存取資料的量。

*    cluster叢集架構擴充方便。

*    分散式計算。(移動運算筆移動資料成本更低)

<img src="https://github.com/CHENntust/hadoop/blob/main/img/HDFS.png"/>

★  NameNode：儲存檔案的block清單，稱之為metadata

★  DataNode：負責儲存實體檔案的block。

使用者以HDFS下儲存檔案的命令後，系統會將檔案切割為多個Block(A、B、C)，每個區塊是64MB，每個Block預設會複製三份(可再Hadoop組態中設定)，當區塊損毀時，NameNode會自動尋找其它DataNode上的副本來回復資料。

## MapReduce(MapReduce2.0 - YARN)

★  Map：將工作分割成小工作，由暪台伺服器分別執行。

★  Reduce：將所有伺服器的運算結果彙整，回傳最後的結果。

<img src="https://github.com/CHENntust/hadoop/blob/main/img/MapReduce.png"/>

1. Client會向Resource Manager要求執行運算

2. NameNode的Resource Manager會統籌管理運算需求

3. DataNode的Node Manager會負責執行分配下來的工作，並向Resource Manager回報結果

## Spark2.0

Spark在這個版本的主要功能包括**提升執行效率**、**整合SQL和Hive的Query功能**、**機器學習是以DataFrame為基礎**有效的整合python操作
```
import pandas as pd
data = [(100,'lily',18) (101,'lucy',19)]
schema = StructType([StructField('id' ,LongType() ,True ) ,
                      StructField('name' ,StringType() ,True ) ,
                      StructField('age' ,LongType() ,True )])
df = spark.createDataFrame(data,schema)
pandas_df = df.toPandas()
```
## 安裝步驟
*    由於hadoop是使用JAVA開發，因此需要先安裝JDK。
```
#安裝
sudo apt install openjdk-8-jdk

#確認JAVA版本。
java -version

#確認JAVA的安裝路徑。
update-alternatives --display java
```
    
*    設定SSH無密碼登入
```
#安裝相依套件
sudo apt install gedit
sudo apt install net-tools
sudo apt-get install rsync
sudo apt-get install ssh

#生成授權金鑰(設定直接空白Enter)
ssh-keygen -t rsa -P ""

#將授權金鑰放置至授權檔案中
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
```

*    下載hadoop

https://hadoop.apache.org/releases.html (3.1.4 version is selected and click binary yo download)

```
#解壓縮至hadoop資料夾
tar -zxvf hadoop-3.1.4.tar.gz
sudo mv hadoop-3.1.4 ~/hadoop
```

*    設定環境變數

```
sudo gedit ~/.bashrc
```
    export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
    export HADOOP_HOME=/home/使用者名稱/hadoop
    export PATH=$PATH:$HADOOP_HOME/bin
    export PATH=$PATH:$HADOOP_HOME/sbin
    export HADOOP_MAPRED_HOME=$HADOOP_HOME
    export HADOOP_COMMON_HOME=$HADOOP_HOME
    export HADOOP_HDFS_HOME=$HADOOP_HOME
    export YARN_HOME=$HADOOP_HOME
    export HADOOP_COMMON_LIB_NATIVE_DIR=$HADOOP_HOME/lib/native
    export HADOOP_OPTS="-Djava.library.path=$HADOOP_HOME/lib/native"
    export JAVA_LIBRARY_PATH=$HADOOP_HOME/lib/native:$JAVA_LIBRARY_PATH

```
sudo gedit ~/.bashrc
```
*    組態設定
*    建立HDFS目錄
*    啟動Hadoop
*    開啟Web管理介面
