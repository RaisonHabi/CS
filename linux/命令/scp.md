## scp
是secure copy的简写，**用于在Linux下进行远程拷贝文件的命令**  
和它类似的命令有cp，***不过cp只是在本机进行拷贝不能跨服务器，而且scp传输是加密的***。   

可能会稍微影响一下速度。  
当你服务器硬盘变为只读 read only system时，用scp可以帮你把文件移出来。  
另外，scp还非常不占资源，不会提高多少系统负荷，在这一点上，rsync就远远不及它了。  
虽然 rsync比scp会快一点，但当小文件众多的情况下，rsync会导致硬盘I/O非常高，而scp基本不影响系统正常使用。

## 命令格式：
scp [参数] [原路径] [目标路径]
## 命令功能：
scp是linux系统下基于ssh登陆进行安全的远程文件拷贝命令。  
linux的scp命令**可以在linux服务器之间复制文件和目录**。  
命令参数详见参考
## 指定端口
```
scp -P port file_name user@ip:/dir_name
```
-P: 大写的P, 指定端口号


## References
[每天一个linux命令（60）：scp命令](https://www.cnblogs.com/peida/archive/2013/03/15/2960802.HTML)  
[scp传文件指定端口](https://blog.csdn.net/qq_29307291/article/details/72819802)
