## 显示当前GPU使用情况
Nvidia自带了一个nvidia-smi的命令行工具，会显示显存使用情况：
```
$ nvidia-smi
```
&nbsp;
## 周期性输出GPU使用情况
但是有时我们希望不仅知道那一固定时刻的GPU使用情况，我们希望一直掌握其动向，此时我们就希望周期性地输出，比如每 10s 就更新显示。 这时候就需要用到 watch命令，来周期性地执行nvidia-smi命令了。

了解一下watch的功能：
```
$ whatis watch
 watch(1)        - execute a program periodically, showing output fullscreen
```
作用：周期性执行某一命令，并将输出显示。

watch的基本用法是：
```
$ watch [options]  command
```
最常用的参数是 -n， 后面指定是每多少秒来执行一次命令。

监视显存：我们设置为每 10s 显示一次显存的情况：
```
$ watch -n 10 nvidia-smi
```
&nbsp;
## References
[Linux下监视NVIDIA的GPU使用情况](https://blog.csdn.net/jasonzzj/article/details/52649174)  
