## Linux 技巧

+ `crtl+r` 快速寻找之前的一些命令
+ 后台运行程序 & 
+ 打包压缩: tar
	- -c 归档文件
	- -x 压缩文件
	- -z gzip压缩文件
	- -v 显示压缩或者解压缩的过程
	- -f 使用文档名
	- expamle: tar -cvf /home/abc.tar /home/abc              只打包，不压缩
	- tar -zcvf /home/abc.tar.gz /home/abc        打包，并用gzip压缩
	- 当然，如果想解压缩，就直接替换上面的命令  tar -cvf  / tar -zcvf  / tar -jcvf 中的“c” 换成“x” 就可以了
+ 查看所有进程端口使用情况 netstat -apn
+ 查看端口情况 lsof -i[:port] 
+ 查看某一个命令的详情 man
+ 查看进程信息 ps -aux
	- a all显示其他用户信息
	- u 启动这个进程的用户和它启动的时间
	- x 查看系统中属于自己的进程
+ 查看某个进程的信息(linux环境下) `ps -aux|grep [info]`    info是关键字
+ git grep 在当前工作目录(Tree)中, 查找相关的东西
+ 杀死某个进程 kill
	- kill -9(SIGKILL) [pid] 
+ pkill -f <name> 根据进程的名字杀死进程
+ secure Copy [scp命令](http://www.hypexr.org/linux_scp_help.php):
	- 从本地到远程: scp foobar.txt your_username@remotehost.edu:/some/remote/directory 
	- 从本地到远程: scp -r foo your_username@remotehost.edu:/some/remote/directory/bar -r 表示文件夹
	- 从远程到本地: scp your_username@remotehost.edu:foobar.txt /some/local/directory

+ 给可执行文件(sh)添加权限: chmod 777 *.sh
+ chmod adc file a,b,c表示三者用户的权限
	- a :User
	- b :Group
	- c :Other
	
>
-rw------- (600) -- 只有属主有读写权限。  
-rw-r--r-- (644) -- 只有属主有读写权限；而属组用户和其他用户只有读权限。  
-rwx------ (700) -- 只有属主有读、写、执行权限。  
-rwxr-xr-x (755) -- 属主有读、写、执行权限；而属组用户和其他用户只有读、执行权限。  
-rwx--x--x (711) -- 属主有读、写、执行权限；而属组用户和其他用户只有执行权限。  
-rw-rw-rw- (666) -- 所有用户都有文件读、写权限。这种做法不可取。  
-rwxrwxrwx (777) -- 所有用户都有读、写、执行权限。更不可取的做法。  
以下是对目录的两个普通设定:  
drwx------ (700) - 只有属主可在目录中读、写。  
drwxr-xr-x (755) - 所有用户可读该目录，但只有属主才能改变目录中的内容。

如下是权限图

![](./chomd.png)

+ 制作可执行文件bin的软连接 ln -s [可执行文件路径]
+ 查看某一个端口的情况 netstat -an|grep 8091 
+ 显示内存使用情况: free -h
+ uptime为显示当前系统的平均负载, `17:29  up 18 days, 27 mins, 5 users, load averages: 2.37 2.26 2.15` 最近
+ 统计文件中的字数,字节数,行数: wc (-c -l -w)
+ ps -aux监控linux上面的相关进程
+ dstat:多功能网络系统资源统计工具
+ netstat: 查看linux上网络相关的信息
+ systemctl: 系统服务管理器指令
	- systemctl start [server-name]:启动某服务
	- systemctl stop  [server-name]:停止某服务
+ netstat 显示网络状况
+ find :查找某个文件的命令
	- `find .` 查看当前目录下的所有文件
	- `find /home -name "*.txt"` 查看/home目录下所有.txt的文件
	- `find . \( -name "*.txt" -o -name "*.pdf" \)` 查找当前路径下面所有以 `.txt` `.pdf` 结尾的文件
	- `find . -name "*.py"|wc -l` 查看当前目录下所有的`py`文件
	- `find . -not \( -path './$(VENV)' -prune \) -name '*.pyc' -exec rm -f {} \;` 清除python项目中pyc文件, find命令中括号使用了转义, 用来组织多个条件
	- `find . \( -name "*.py" \)| xargs wc -l` 统计当前文件中所有的代码行数
+ `vmstat` 显示虚拟内存状态, 可以报告关于进程, 内存, I/O等整体的情况
+ `cat /proc/meninfo` 查看物理内存和文件缓存情况
+ `iostat`用来监视输入输出设备和cpu的情况
	- `iostat -x /dev/sda1` 用来查看磁盘io详情
+ `top -p PID`查看某一个进程的占用内存的大小
+ `tail -f`: 常用来跟踪某个文件的输出
+ `netstat`: linux中查看网络状态信息
+ `netstat -an | grep ':80'` 查看在具体某一个端口的进程
+ `sort`: linux下对文件进行排序输出, 并将结果输出至标准输出端口中
+ `sort -nk 2 -t: sort.txt` 对`sort.txt`文件以`:`为分隔符, 安装第2列的数值进行升序排序
+ `mysqldump -h hostname-of-the-server -u mysql_user -p database_name > file.sql` 将远程的数据库dump到本地
+ `bash -c <stirng>` -c 为`command`
+ `bash -c "echo hello"` 执行字符串的命令
## tmux

+ tmux ls 列出tmux服务
+ tmux attach -t index 挂载某个tmux服务
+ prefix key :ctrl+B (简称pk)
+ 创建一个窗口 pk+C
+ 关闭一个窗口 pk+&
+ 窗口直接的切换: pk+index (index为窗口的序号)
+ 关闭删除某个session: tmux kill-session -t 会话名
+ 关闭当前session,但是在后台运行 :pk+D
+ 重命名一个session: tmux rename-session -t [index] [name]
+ 重命名一个window: tmux rename-window -t [old-window] [name]
+ 创建一个tmux session: tmux new -s <name-of-my-session>

## vim

+ 翻到下一页: ctrl+f
+ 翻到上一页: ctrl+b
+ Esc: vsp [filepath]垂直分屏打开一个文件
+ yy 复制一行 nyy复制当前光标之后的n行 p粘贴
+ 显示行号: set number
+ 不显示行号: set nonu
+ 切换到右边的屏: ctrl+w l
+ 切换到左边的屏: ctrl+w h
+ vim +PluginInstall +qall 安装插件
+ ESC: U 撤销
+ CTRL+R 反撤销
+ ESC: b上一个单词,e下一个单词
## docker

+ docker ps:查看docker中的进程

## git

+ `git checkout` 切换分支
+ `git add <file>` 添加某个文件到本次提交
+ `git commit` 提交本次commit
+ `git commit -a` 提交更新
+ `git push origin [branch-name]` 提交更新到远程分支
+ `git fetch orgin` 获取所有远程分支的更新
+ `git branch --track <new><remote>` 用来第一次创建本地分支提交代码
+ `git rebase -i` 在本地进行commit的合并 i 之后加相应的参数可以进行到某个时间点合并
+ `git rebase -i~<num>`使用d来删除某个commit
+ 可以通过`git reset 和 git checkout` 来修改代码文件的工作区域
+ `git remote add` 用来添加不同的remote, 通常来说是
+ `git fetch origin, git merge origin/another-branch` 用来在更新本地分支(合并远程分支)
+ `git fetch origin, git rebase origin/another-branch` 功能同上 
+ 当更新本地分支出现:`First, rewinding head to replay your work on top of it...`,并且要强制更新本地分支则 `git fetch origin, git reset --hard origin/<branch>`
+ 当本地分支更新完成之后, 需要手动`git push origin/<branch>` 更新跟踪的远程分支
+ `git branch branch_name --set-upstream-to origin/branch_name` git 切换跟踪的远程分支
+ 当提交`merge request`时,出现了冲突则`git fetch` `git rebase origin/<branch>`来解决冲突
+ `git diff` 用来查看当前改变和HEAD的区别, `git diff HEAD^ HEAD`查看上一次提交和当前HEAD的区别, `git diff a b`, a 早期提交, b后来提交
+ 添加`.gitignore`文件`echo '.idea' >> .gitignore, git rm -r --cached .idea, git add .gitignore`
+ `git config --local` 配置当前项目的配置, `git config --global`配置全局配置
+ `git reset HEAD@{3}` 使用通常为`git reset HEAD^`之后查看`git reflog`来返回上一次提交 
+ `git reset --soft HEAD~1`不提交上一次的`commit`
+ `git revert <commit>` undo the specific commit
+ `git commit -a -amend` 提交修改至最后一次commit中
+ `git rm --cached <filename>` 从git中删除, 并不从文件系统中删除
+ `git branch -m <new-branch-name>`: 重新命名一个新的分支的名字
+ `git push origin :old-branch`: 删除一个远程分支
+ `git push origin :old-name new-name`: 删除远程分支, 并push新分支名字
+ `git branch -d <branch name>`: 删除本地分支
+ `git branch -r`: 列出所有远程分支

## g++
> reference: 

+ `.a` 文件编译期静态链接, 在编译器静态链接到项目中, 是项目工程的一部分
+ `.so` 文件运行期动态连接到项目中去,如果对`.so`文件有一定的改动不需要重新编译项目工程文件
+ C标准库,C++STL都是`.so` 
+ ` gcc -Wall -fPIC -c *.c`
+ `gcc -shared -o libfoo.so foo.o`
+ `gcc -shared -Wl,-soname,libctest.so.1 -o libctest.so.1.0   *.o` 

## TCPdump
> tcpdump 运行启动linux下的抓包工具

#### 网络相关概念
+ `MTU`: `maximum transmission unit`, 为10进制的字节, 可以为报文或者帧. TCP报文超过了`MTU`则会导致重传

#### 命令操作
+ `tcpdump -i eth0`: 从特定的网卡接口抓包
+ `tcpdump -c 5`: 抓取数量为5的报文
+ `tcpdump -A`: 将报文以ASCII的形式输出
+ `tcpdump -D`: 列出所有可用的网卡接口
+ `tcpdump -XX`: 将报文以16进制
+ `tcpdump -w xxx.pcap`: 抓包写入文件
+ `tcpdump -r xxx.pcap`: 抓包读入文件 
+ `tcpdump port 80`: 从特定的端口进行抓包, `tcpdump -i lo0 port 7080`对本地7080端口进行抓包
+ `tcpdump -i eth0 src ip`从源端口进行抓包
+ `tcpdump -i eth0 dst ip`抓取目的端口的包
+ [tcp 的一个基本介绍](http://cizixs.com/2015/03/12/tcpdump-introduction)

#### Httpry httpflow

该工具用来抓HTTP包

## shell 

+ `export`: 该命令通常是用来创建一个环境变量, 即当执行一个子程序时, 将会继承来自于父进程的环境变量. 
+ `ssh-add` 命令添加`private key`到`ssh`中, 具体为`ssh-add -K <private key(wangruoxuan_internalJump)> `, 记得输密码.
+ `ctrl + a`: 移动bash命令的行首, `ctrl + e`: 移动bash命令的行尾
+ `ctrl + b`: 光标前移一个字符, `ctrl + f`: 光标后移一个字符
+ `ctrl + u`: 删除光标左边所有, 即删除全部
+ `ctrl + r`: 关键字查找之前的命令
+ `alias` 可以用来设置运行指定的脚本, 或者命令

## curl

+ ` curl -s --user 'api:key-e252c1676701badf282a8f28030b3217' -G https://api.mailgun.net/v3/mail.faceplusplus.com/bounces`
	- `-s` 静默输出
	- `--user` 用户认证
	- `-G` GET方法
+ `curl  -d '{"image_id": "gQ5wlrWxnFkIxfJ5srBNyA=="}' -X POST http://10.104.4.50:8000/faceid/v1/detect`


## pycharm 快捷键

+ `shift+command+r/f`: 全局替换或者查找, 可以指定范围
+ `comand +r/f`: 当前文件查找或者替换
+ `command + o`: 查找类
+ `alt + command + o`: 查找某个函数
+ `shift + command + o`: 查找某个路径