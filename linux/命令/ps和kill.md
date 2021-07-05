## ps查看进程
### $ ps -ef 或者：$ ps -aux
Linux中的ps命令是Process Status的缩写。  
ps命令用来列出系统中当前运行的那些进程。**ps命令列出的是当前那些进程的快照，就是执行ps命令的那个时刻的那些进程，如果想要动态的显示进程信息，就可以使用top命令**。

### 命令参数
```
a  显示所有进程
-a 显示同一终端下的所有程序
-A 显示所有进程
c  显示进程的真实名称
-N 反向选择
-e 等于“-A”
e  显示环境变量
f  显示程序间的关系
-H 显示树状结构
r  显示当前终端的进程
T  显示当前终端的所有程序
u  指定用户的所有进程

-au 显示较详细的资讯
-aux 显示所有包含其他使用者的行程 

-C<命令> 列出指定命令的状况
--lines<行数> 每页显示的行数
--width<字符数> 每页显示的字符数
--help 显示帮助信息
--version 显示版本显示
```

### 常用ps命令参数
最常用的三个参数是u、a、x，下面将通过例子来说明其具体用法
#### ps
```
$ ps

PID TTY TIME COMMAND
5800 ttyp0 00:00:00 bash
5835 ttyp0 00:00:00 ps

PID（进程ID）、TTY（终端名称）、TIME（进程执行时间）、COMMAND（该进程的命令行输入）
```
#### ps u
可以使用u选项来查看进程所有者及其他一些详细信息
```
$ ps u

USER PID %CPU %MEM USZ RSS TTY STAT START TIME COMMAND
test 5800 0.0 0.4 1892 1040 ttyp0 S Nov27 0:00 -bash
test 5836 0.0 0.3 2528 856 ttyp0 R Nov27 0:00 ps u

在bash进程前面有条横线，意味着该进程便是用户的登录shell，所以对于一个登录用户来说带短横线的进程只有一个。
还可以看到%CPU、%MEM两个选项，前者指该进程占用的CPU时间和总时间的百分比；后者指该进程占用的内存和总内存的百分比。
```

[每天一个linux命令（41）：ps命令](https://www.cnblogs.com/peida/archive/2012/12/19/2824418.html)  
[linux 命令——PS命令](https://www.cnblogs.com/timelesszhuang/p/4305139.html)

&nbsp;
## kill
### 示例
**$ kill -s 9 1827**  
其中-s 9 制定了传递给进程的信号是９，即强制、尽快终止进程。各个终止信号及其作用见附录。  
1827则是上面ps查到的火狐的PID。

简单吧，但有个问题，进程少了则无所谓，进程多了，就会觉得痛苦了，无论是ps -ef 还是ps -aux，每次都要在一大串进程信息里面查找到要杀的进程，看的眼都花了。
### 改进1
把ps的查询结果通过管道给grep查找包含特定字符串的进程。管道符“|”用来隔开两个命令，管道符左边命令的输出会作为管道符右边命令的输入。
```
$ ps -ef | grep firefox
smx       1827     1  4 11:38 ?        00:27:33 /usr/lib/firefox-3.6.18/firefox-bin
smx      12029  1824  0 21:54 pts/0    00:00:00 grep --color=auto firefox
```
这次就清爽了。然后就是 $kill -s 9 1827  
还是嫌打字多？
### 改进2 使用pgrep
一看到pgrep首先会想到什么？没错，grep！pgrep的p表明了这个命令是专门用于进程查询的grep。
```
$ pgrep firefox
1827
```
看到了什么？没错火狐的PID，接下来又要打字了：
$kill -s 9 1827
### 改进３ 使用pidof
看到pidof想到啥？没错pid of xx，字面翻译过来就是 xx的PID。
```
$ pidof firefox-bin
1827
```
和pgrep相比稍显不足的是，pidof必须给出进程的全名。然后就是老生常谈：$kill -s 9 1827

无论使用ps 然后慢慢查找进程PID 还是用grep查找包含相应字符串的进程，亦或者用pgrep直接查找包含相应字符串的进程pid，然后手动输入给kill杀掉，都稍显麻烦。有没有更方便的方法？有！
### 改进４
```
$ps -ef | grep firefox | grep -v grep | cut -c 9-15 | xargs kill -s 9
```
说明：
```
“grep firefox”的输出结果是，所有含有关键字“firefox”的进程。
“grep -v grep”是在列出的进程中去除含有关键字“grep”的进程。
“cut -c 9-15”是截取输入行的第9个字符到第15个字符，而这正好是进程号PID。
“xargs kill -s 9”中的xargs命令是用来把前面命令的输出结果（PID）作为“kill -s 9”命令的参数，并执行该命令。“kill -s 9”会强行杀掉指定进程。
```
难道你不想抱怨点什么？没错太长了
### 改进５
知道pgrep和pidof两个命令，干嘛还要打那么长一串！
```
$ pgrep firefox | xargs kill -s 9
```
### 改进６
```
$ ps -ef | grep firefox | awk '{print $2}' | xargs kill -9
kill: No such process
```
有一个比较郁闷的地方，进程已经正确找到并且终止了，但是执行完却提示找不到进程。

其中awk '{print $2}' 的作用就是打印（print）出第二列的内容。根据常规篇，可以知道ps输出的第二列正好是PID。就把进程相应的PID通过xargs传递给kill作参数，杀掉对应的进程。
### 改进７
难道每次都要调用xargs把PID传递给kill？答案是否定的：
```
$kill -s 9 `ps -aux | grep firefox | awk '{print $2}'`
```
### 改进８
没错，命令依然有点长，换成pgrep。
```
$kill -s 9 `pgrep firefox`
```
### 改进9 pkill
看到pkill想到了什么？没错pgrep和kill！pkill＝pgrep+kill。
```
$pkill -９ firefox
```
说明："-9" 即发送的信号是9，pkill与kill在这点的差别是：pkill无须 “ｓ”，终止信号等级直接跟在 “-“ 后面。之前我一直以为是 "-s 9"，结果每次运行都无法终止进程。

### 改进10 killall
killall和pkill是相似的,不过如果给出的进程名不完整，killall会报错。pkill或者pgrep只要给出进程名的一部分就可以终止进程。
```
$killall -9 firefox
```

### 附录：各种信号及其用途
<table id="sortable_table_id_0" class="wikitable sortable" style="table-layout:fixed;"><tbody><tr><th>Signal<span class="sortarrow"></span></th>
<th>Description<span class="sortarrow"></span></th>
<th>Signal number on Linux x86<sup id="cite_ref-0" class="reference"><span style="color:#336699;"><span>[</span>1<span>]</span></span></sup><span class="sortarrow"></span></th>
</tr><tr><td style="font-size:12px;"><span style="color:#336699;">SIGABRT</span></td>
<td style="font-size:12px;">Process aborted</td>
<td style="font-size:12px;">6</td>
</tr><tr><td style="font-size:12px;"><span style="color:#336699;">SIGALRM</span></td>
<td style="font-size:12px;">Signal raised by <tt><span style="font-family:'Courier New';color:#336699;">alarm</span></tt></td>
<td style="font-size:12px;">14</td>
</tr><tr><td style="font-size:12px;"><span style="color:#336699;">SIGBUS</span></td>
<td style="font-size:12px;">Bus error: "access to undefined portion of memory object"</td>
<td style="font-size:12px;">7</td>
</tr><tr><td style="font-size:12px;"><span style="color:#336699;">SIGCHLD</span></td>
<td style="font-size:12px;">Child process terminated, stopped (or continued*)</td>
<td style="font-size:12px;">17</td>
</tr><tr><td style="font-size:12px;"><span style="color:#336699;">SIGCONT</span></td>
<td style="font-size:12px;">Continue if stopped</td>
<td style="font-size:12px;">18</td>
</tr><tr><td style="font-size:12px;"><span style="color:#336699;">SIGFPE</span></td>
<td style="font-size:12px;">Floating point exception: "erroneous arithmetic operation"</td>
<td style="font-size:12px;">8</td>
</tr><tr><td style="font-size:12px;"><span style="color:#336699;">SIGHUP</span></td>
<td style="font-size:12px;">Hangup</td>
<td style="font-size:12px;">1</td>
</tr><tr><td style="font-size:12px;"><span style="color:#336699;">SIGILL</span></td>
<td style="font-size:12px;">Illegal instruction</td>
<td style="font-size:12px;">4</td>
</tr><tr><td style="font-size:12px;"><span style="color:#336699;">SIGINT</span></td>
<td style="font-size:12px;">Interrupt</td>
<td style="font-size:12px;">2</td>
</tr><tr><td style="font-size:12px;"><span style="color:#336699;">SIGKILL</span></td>
<td style="font-size:12px;">Kill (terminate immediately)</td>
<td style="font-size:12px;">9</td>
</tr><tr><td style="font-size:12px;"><span style="color:#336699;">SIGPIPE</span></td>
<td style="font-size:12px;">Write to pipe with no one reading</td>
<td style="font-size:12px;">13</td>
</tr><tr><td style="font-size:12px;"><span style="color:#336699;">SIGQUIT</span></td>
<td style="font-size:12px;">Quit and dump core</td>
<td style="font-size:12px;">3</td>
</tr><tr><td style="font-size:12px;"><span style="color:#336699;">SIGSEGV</span></td>
<td style="font-size:12px;"><span style="color:#336699;">Segmentation violation</span></td>
<td style="font-size:12px;">11</td>
</tr><tr><td style="font-size:12px;"><span style="color:#336699;">SIGSTOP</span></td>
<td style="font-size:12px;">Stop executing temporarily</td>
<td style="font-size:12px;">19</td>
</tr><tr><td style="font-size:12px;"><span style="color:#336699;">SIGTERM</span></td>
<td style="font-size:12px;">Termination (request to terminate)</td>
<td style="font-size:12px;">15</td>
</tr><tr><td style="font-size:12px;"><span style="color:#336699;">SIGTSTP</span></td>
<td style="font-size:12px;">Terminal stop signal</td>
<td style="font-size:12px;">20</td>
</tr><tr><td style="font-size:12px;"><span style="color:#336699;">SIGTTIN</span></td>
<td style="font-size:12px;">Background process attempting to read from tty ("in")</td>
<td style="font-size:12px;">21</td>
</tr><tr><td style="font-size:12px;"><span style="color:#336699;">SIGTTOU</span></td>
<td style="font-size:12px;">Background process attempting to write to tty ("out")</td>
<td style="font-size:12px;">22</td>
</tr><tr><td style="font-size:12px;"><span style="color:#336699;">SIGUSR1</span></td>
<td style="font-size:12px;">User-defined 1</td>
<td style="font-size:12px;">10</td>
</tr><tr><td style="font-size:12px;"><span style="color:#336699;">SIGUSR2</span></td>
<td style="font-size:12px;">User-defined 2</td>
<td style="font-size:12px;">12</td>
</tr><tr><td style="font-size:12px;"><span style="color:#336699;">SIGPOLL</span></td>
<td style="font-size:12px;">Pollable event</td>
<td style="font-size:12px;">29</td>
</tr><tr><td style="font-size:12px;"><span style="color:#336699;">SIGPROF</span></td>
<td style="font-size:12px;">Profiling timer expired</td>
<td style="font-size:12px;">27</td>
</tr><tr><td style="font-size:12px;"><span style="color:#336699;">SIGSYS</span></td>
<td style="font-size:12px;">Bad <span style="color:#336699;">syscall</span></td>
<td style="font-size:12px;">31</td>
</tr><tr><td style="font-size:12px;"><span style="color:#336699;">SIGTRAP</span></td>
<td style="font-size:12px;">Trace/breakpoint <span style="color:#336699;">trap</span></td>
<td style="font-size:12px;">5</td>
</tr><tr><td style="font-size:12px;"><span style="color:#336699;">SIGURG</span></td>
<td style="font-size:12px;">Urgent data available on socket</td>
<td style="font-size:12px;">23</td>
</tr><tr><td style="font-size:12px;"><span style="color:#336699;">SIGVTALRM</span></td>
<td style="font-size:12px;">Signal raised by timer counting virtual time: "virtual timer expired"</td>
<td style="font-size:12px;">26</td>
</tr><tr><td style="font-size:12px;"><span style="color:#336699;">SIGXCPU</span></td>
<td style="font-size:12px;">CPU time limit exceeded</td>
<td style="font-size:12px;">24</td>
</tr><tr><td style="font-size:12px;"><span style="color:#336699;">SIGXFSZ</span></td>
<td style="font-size:12px;">File size limit exceeded</td>
<td style="font-size:12px;">25</td>
</tr></tbody></table>                     

&nbsp;
## References
[linux下杀死进程（kill）的N种方法](https://blog.csdn.net/andy572633/article/details/7211546)  

