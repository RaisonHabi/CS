## 两者区别
**du：disk usage**    
是通过搜索文件来计算每个文件的大小然后累加，du能看到的文件只是一些当前存在的，没有被删除的。他计算的大小就是当前他认为存在的所有文件大小的累加和。

**df：disk free**  
通过文件系统来快速获取空间大小的信息，当我们删除一个文件的时候，这个文件不是马上就在文件系统当中消失了，而是暂时消失了，当所有程序都不用时，才会根据OS的规则释放掉已经删除的文件， df记录的是通过文件系统获取到的文件的大小，他比du强的地方就是能够看到已经删除的文件，而且计算大小的时候，把这一部分的空间也加上了，更精确了。

当文件系统也确定删除了该文件后，这时候du与df就一致了。

&nbsp;
## df
linux中df命令的功能是用来检查linux服务器的文件系统的磁盘空间占用情况。可以利用该命令来获取硬盘被占用了多少空间，目前还剩下多少空间等信息。

显示指定磁盘文件的可用空间。如果没有文件名被指定，则所有当前被挂载的文件系统的可用空间将被显示。默认情况下，磁盘空间将以 1KB 为单位进行显示，除非环境变量 POSIXLY_CORRECT 被指定，那样将以512字节为单位进行显示。

Linux du命令也是查看使用空间的，但是与df命令不同的是Linux du命令是查看当前指定文件或目录(会递归显示子目录)占用磁盘空间大小。

&nbsp;

Linux df命令用于显示目前在Linux系统上的文件系统的磁盘使用情况统计。
```
文件-a, --all 包含所有的具有 0 Blocks 的文件系统
文件--block-size={SIZE} 使用 {SIZE} 大小的 Blocks
文件-h, --human-readable 使用人类可读的格式(预设值是不加这个选项的...)
文件-H, --si 很像 -h, 但是用 1000 为单位而不是用 1024
文件-i, --inodes 列出 inode 资讯，不列出已使用 block
文件-k, --kilobytes 就像是 --block-size=1024
文件-l, --local 限制列出的文件结构
文件-m, --megabytes 就像 --block-size=1048576
文件--no-sync 取得资讯前不 sync (预设值)
文件-P, --portability 使用 POSIX 输出格式
文件--sync 在取得资讯前 sync
文件-t, --type=TYPE 限制列出文件系统的 TYPE
文件-T, --print-type 显示文件系统的形式
文件-x, --exclude-type=TYPE 限制列出文件系统不要显示 TYPE
文件-v (忽略)
文件--help 显示这个帮手并且离开
文件--version 输出版本资讯并且离开
```

&nbsp;
## References
[Linux的du、df命令](https://www.jianshu.com/p/5d13c7dfd0c1)  
[Linux df命令](https://www.runoob.com/linux/linux-comm-df.html)
