# 进程“已杀死”问题：内存不够

可能是内存溢出，Out of memory内存不够，需要清理一下内存（缓存）。

## linux查看内存

指令：

```bash
$ free [-bkmotV][-s <间隔秒数>]
```

参数：

- -b 　以Byte为单位显示内存使用情况。

- -k 　以KB为单位显示内存使用情况。

- -m 　以MB为单位显示内存使用情况。

- ==-h 　以合适的单位显示内存使用情况，最大为三位数，自动计算对应的单位值。==单位有：

  ```
  B = bytes
  K = kilos
  M = megas
  G = gigas
  T = teras
  ```

- -o 　不显示缓冲区调节列。

- -s<间隔秒数> 　持续观察内存使用状况。

- -t 　显示内存总和列。

- -V 　显示版本信息。

## 清理缓存

清理缓存前先用sync命令：

```bash
$ sync
```

释放缓存指令：

```bash
$ echo 3 > /proc/sys/vm/drop_caches
```

0 – 不释放
1 – 释放页缓存 （数字1是用来清空最近访问过的文件页面缓存）
2 – 释放dentries和inodes （数字2是用来清空文件节点缓存和目录项缓存）
3 – 释放所有缓存 （数字3是用来清空1和2所有内容的缓存。）

**如果权限不够：**

```bash
$ sudo sh -c "echo 3 > /proc/sys/vm/drop_caches"
```





# GPU空间不够

需要清理一下显存。

## 查看显存占用情况

```bash
$ fuser -v /dev/nvidia* 
```

可发现进程占用情况类似如下：

```
                     USER        PID ACCESS COMMAND
/dev/nvidia0:        hnj        1660 F...m compiz
                     hnj        4388 F...m chrome
                     hnj        4418 F...m chrome
                     hnj        8542 F...m python
                     hnj       23641 F...m TeamViewer
/dev/nvidiactl:      hnj        1660 F...m compiz
                     hnj        4388 F...m chrome
                     hnj        4418 F...m chrome
                     hnj        8542 F...m python
                     hnj       23641 F...m TeamViewer
/dev/nvidia-modeset: hnj        1660 F.... compiz
                     hnj        4388 F.... chrome
                     hnj        4418 F.... chrome
                     hnj       23641 F.... TeamViewer
/dev/nvidia-uvm:     hnj        8542 F.... python
```

根据对应的进程号杀死：

```bash
$ kill -9 8542
```

