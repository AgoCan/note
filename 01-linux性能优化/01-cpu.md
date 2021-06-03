- 平均负载

> 单位时间内，系统运行着可运行状态和不可中断状态的平均活跃进程数

`ps aux`查看的`running`或者`runable`,一个cpu平均负载1表示这个cpu跑了一个进程，如果1个负载2表示进程使用cpu不够用

查看cpu数量
```
grep 'model name' /proc/cpuinfo | wc -l
```

> 平均负载到达cpu的一个阈值的时候就需要查看原因，例如 70%。  48cpu * 70% =33.6的时候进行查看

- 平均负载和cpu使用率

不是等价关系，可运行状态和不可中断状态 包含： 正在使用cpu、等待cpu、等待I/O

工具： `iostat`、`mpstat`、`pidstat`、`stress`、`sysstat`

场景 ubuntu18.04

三个终端窗口
```
uptime # 查看负载
```

```
# 增加cpu使用率
apt-get update
apt-get install stress -y
stress --cpu 1 --timeout 600
```

```
# 查看cpu使用率情况
apt-het update
apt install sysstat -y
mpstat -P ALL 5
```

```
# 查看进程使用100%
pidstat -u 5 1 # centos 没有iowait的命令，需要升级，ubuntu则不需要
pidstat -d 5 1 # 查看io进程情况
```

```
# i/o 密集型
stress -i 1 --timeout 600
iostat -x -d 2 60 # 查看io使用情况
```

```
# 大量进程的场景, 8个进程
stress -c 8 --timeout 600
```

- cpu上下文切换

`vmstat`
