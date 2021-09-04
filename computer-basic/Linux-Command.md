[toc]

# Linux 常用命令

## 1、查看系统信息

### 1.1 cpu、线程

```shell
cat /prco/cpuinfo
```



### 1.2 磁盘空间

```shell
df #disk free 查看磁盘所有可用空间
df -h # 以便于理解的方式展示磁盘空间大小

du # disk used 查看磁盘使用情况
du -sh # -sh [dir] 查看目录磁盘大小
du -h # 查看所有子目录

```

### 1.3 进程、内存

```shell
top # 显示process信息
# 面板指令
# e 切换下方内存显示单位
# E 切换上方内存显示单位
# 
#
#
top -p # 指定pid查看
top -u # 指定用户查看

```



### 1.4 IO

### 1.5 网络IO

#### 1.5.1 iftop

**简介**：iftop是类似于top命令的效果，对机器的每个IP+PORT的网络IO进行监控的工具

**安装**

```shell
yum -y install iftop
```

**使用方式**

```shell
sudo iftop
	 -h                  display this message
   -n                  don't do hostname lookups
   -N                  don't convert port numbers to services
   -p                  run in promiscuous mode (show traffic between other
                       hosts on the same network segment)
   -b                  don't display a bar graph of traffic
   -B                  display bandwidth in bytes
   -a                  display bandwidth in packets
   -i interface        listen on named interface
   -f filter code      use filter code to select packets to count
                       (default: none, but only IP packets are counted)
   -F net/mask         show traffic flows in/out of IPv4 network
   -G net6/mask6       show traffic flows in/out of IPv6 network
   -l                  display and count link-local IPv6 traffic (default: off)
   -P                  show ports as well as hosts
   -m limit            sets the upper limit for the bandwidth scale
   -c config file      specifies an alternative configuration file
   -t                  use text interface without ncurses

   Sorting orders:
   -o 2s                Sort by first column (2s traffic average)
   -o 10s               Sort by second column (10s traffic average) [default]
   -o 40s               Sort by third column (40s traffic average)
   -o source            Sort by source address
   -o destination       Sort by destination address

The following options are only available in combination with -t
-s num              print one single text output afer num seconds, then quit
-L num              number of lines to print
```

#### 1.5.2 nethogs

**简介**：nethogs是类似于top命令的效果，对每个进程的网络IO进行监控的工具

**安装**

```shell
yum -y install nethogs
```

**使用方式**

```shell
sudo nethogs

		-V : 打印版本.
		-h : help信息.
		-b : bughunt mode - implies tracemode. 会打印大量堆栈信息，不会显示流量
		-d : delay for update refresh rate in seconds. default is 1. 刷新间隔
		-v : view mode (0 = KB/s, 1 = total KB, 2 = total B, 3 = total MB). default is 0. 显示总量或者实时流量
		-c : number of updates. default is 0 (unlimited). 刷新次数
		-t : tracemode. 可读的ip、端口单条流量信息（非进程）
		-p : sniff in promiscious mode (not recommended).
		-s : sort output by sent column. 按发送流量排序
   -a : monitor all devices, even loopback/stopped ones.
		device : device(s) to monitor. default is all interfaces up and running excluding loopback
		
When nethogs is running, press:
 q: quit
 s: sort by SENT traffic 
 r: sort by RECEIVE traffic
 m: switch between total (KB, B, MB) and KB/s mode
```

**BUG** 

```
version-0.8.5 
部分机器无法显示，卡在waiting for receive first package
大流量无法实时刷新，有个延迟
```



### 1.6 文件、内容查找

文件信息查看

```shell
ls # list files 
ls -a # all 列出所有文件（包括.开头文件）
ls -l # 文件大小、权限等信息
ls -t # 按时间排序列出文件
```

查找文件

```shell
find #
-perm	#<权限数值>	查找符合指定的权限数值的文件或目录
-type #<文件类型>	只寻找符合指定的文件类型的文件
-name #<范本样式>	指定字符串作为寻找文件或目录的范本样式
-expty	#寻找文件大小为 0 Byte 的文件，或目录下没有任何子目录或文件的空目录
-ls	#假设find指令的回传值为ture，就将文件或目录名称列出到标准输出
-maxdepth #<目录层级>	设置最大目录层级
-mindepth #<目录层级>	设置最小目录层级
-exec #<执行指令>	假设find指令的回传值为true，就执行该指令
-ok #<执行指令>	此参数的效果和指定-exec类似，但在执行指令之前会先询问用户，若回答y或Y，则放弃执行命令

# 使用
find . -name "mysql" #查找当前目录下所有名字为mysql的文件或目录
```

​	列出当前系统打开文件

```shell
lsof -i:8000 #列出占用8000端口的文件和进程信息,也可借此查看端口连接数?


```



### 1.7 操作系统信息



### 1.8 文本内容

#### 1.8.1 awk

#### 1.8.2 sed

```shell
sed -i "s/original/replace/g" file #替换字符串
```



### 1.9 多线程

### 1.10 自动交互命令

### 1.11 文件压缩

```shell
tar -cvf  #压缩文件
tar -xvf  #解压缩文件
```













