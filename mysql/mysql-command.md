[toc]

# mysql运维命令笔记

## 1 常用命令

| desc       | cmd                                                          |
| ---------- | ------------------------------------------------------------ |
| 启动       | bin/mysqld_safe --defaults-file=etc/my.cnf &                 |
| 停止       | bin/mysqladmin --defaults-extra-file=etc/user.root.cnf shutdown |
| 登录       | bin/mysql --defaults-extra-file=etc/user.root.cnf            |
| 创建用户   | create user ''@'' identified by '';                          |
| 授权       | grant all privileges on *.* to ''@'';                        |
| 清理binlog | purge binary logs to 'mysql-bin.000298';                     |

## 2 组合命令

### 2.1 主从切换

### 2.2 批量drop

批量drop table

```shell
#! /bin/bash
# drop tables
word=`echo $1`
params=`echo $#`
echo "your input param is|"$word"|"
#param is ok?
if [ $params -lt 1 ]
then
 echo "usage:drop 'yourword'"
 exit
fi

cnt=1
while ((cnt < 101))
do
 #connect mysql and read tb names
 var=$(./bin/mysql --defaults-extra-file=etc/user.root.cnf -e"use test$cnt;show tables like '$word';")

 count=0
 #read table names
 for i in $var;
 do
  let count=$count+1
  if [ $count -ne 1 -a $count -ne 2 ]
  then
  #delete from db
  echo "deleting ...$i"
  ./bin/mysql --defaults-extra-file=etc/user.root.cnf -e"use test$cnt;drop table $i"
  fi
 done
 let cnt=$cnt+1
done
```

**批量drop database**

```shell
# drop databases
#! /bin/bash
word=`echo $1`
params=`echo $#`
echo "your input param is|"$word"|"
#param is ok?
if [ $params -lt 1 ]
then
 echo "usage:drop 'yourword'"
 exit
fi

cnt=1
while ((cnt < 101))
do
 #delete from db
 echo "deleting ...test$cnt"
 ./bin/mysql --defaults-extra-file=etc/user.root.cnf -e"drop database test$cnt"
 let cnt=$cnt+1
done
```
