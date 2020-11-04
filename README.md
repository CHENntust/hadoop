# Hadoop - Establish NameNode and DataNode.md

## HDFS

*    硬體故障式常態而非異常。

*    Streaming存取資料，犧牲反應時間來提高存取資料的量。

*    cluster叢集架構擴充方便。

*    分散式計算。(移動運算筆移動資料成本更低)

<img src="https://github.com/CHENntust/hadoop/blob/main/img/HDFS.png"/>

★  NameNode：儲存檔案的block清單，稱之為metadata

★  DataNode：負責儲存實體檔案的block。

使用者以HDFS下儲存檔案的命令後，系統會將檔案切割為多個Block(A、B、C)，每個區塊是64MB，每個Block預設會複製三份(可再Hadoop組態中設定)，當區塊損毀時，NameNode會自動尋找其它DataNode上的副本來回復資料。
