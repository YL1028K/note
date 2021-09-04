# sysbench 学习笔记

### 安装

centOS安装

```shell
yum -y install sysbench
```

### 测试OLTP

**wirte_only**

```shell
sysbench /usr/share/sysbench/oltp_write_only.lua/ --mysql-host=127.0.0.1 --mysql-port=8903 --mysql-user= --mysql-password= --mysql-db=test  --tables=100 --table-size=10000000 --report-interval=10 --threads=54 --skip-trx=on --mysql-ignore-errors=all --db-ps-mode=disable --db-driver=mysql prepare
```

##### Read_write

```shell
sysbench /usr/share/sysbench/oltp_read_write.lua/ --mysql-host=127.0.0.1 --mysql-port=8902 --mysql-user= --mysql-password= --mysql-db=test  --tables=100 --table-size=100000 --report-interval=10 --time=3600 --threads=128 --skip-trx=on --mysql-ignore-errors=all --db-ps-mode=disable --db-driver=mysql run
```

