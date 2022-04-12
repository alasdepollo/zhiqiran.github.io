一、依据HDFS平台现有的数据构建商品表

【1】存在商品表文件product，内容如下：

1|1|ball|70.0
2|1|book|98.5

```
[root@node1 ~]# vi /export/data/hivedata/product

[root@node1 ~]# hadoop fs -mkdir -p /gmall/p

[root@node1 ~]# hadoop fs -put /export/data/hivedata/product  /gmall/p
```

【1】按product表数据建立表（产品ID，用户ID，购买商品名，商品价格）
     指定表读取数据路径 为“/gmall/p”

```
create external table  product (
u_id int,p_id int,p_name string,p_price float
)
ROW FORMAT DELIMITED FIELDS TERMINATED BY '|' --数据以‘|’分割
location '/gmall/p';
```

【2】按product表数据建立表（产品ID，用户ID，购买商品名，商品价格）
     使用默认表读取路径

create external table  product (
u_id int,p_id int,p_name string,p_price float
)
ROW FORMAT DELIMITED FIELDS TERMINATED BY '|' --数据以‘|’分割

【3】说明表指定LOCATION与不指定时的区别

LOCATION指定时会从指定的目录建立表结构，读取该表下面的数据

不指定时默认数据库路径是/user/hive/warehouse/，数据库名为default。

【4】说明表与LOCATION的关系

表结构是建立在location所指定的目录上，表数据是该目录里的文件数据。