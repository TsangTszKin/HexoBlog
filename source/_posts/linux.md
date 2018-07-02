---
title: linux
date: 2016-01-27 23:18:40
description: 'linux常用命令行大全'
tags: 'linux'
categories: '后端'
---

##编辑文件###
编辑文件 a.txt: 
    vi a.txt
    i  (进入插入模式)
    ~
    ~
    编辑
    ~
    ~
    Esc (推出编辑模式 )
    shitf+q (回到正常模式)+wq(保存)/q!(不保存)    


###创建目录，连续创建在当前目录的几个子目录和下一个目录###
	mkdir -p CDY_1/{20160305,20160306,20160307} CDY_2


###删除空文件夹###
	rmdir a

###删除文件夹和文件实例###
	rm -rf /var/log/httpd/access

将会删除/var/log/httpd/access目录以及其下所有文件、文件夹
-r 就是向下递归，不管有多少级目录，一并删除
-f 就是直接强行删除，不作任何提示的意思


###打开文件，查看文件###
	cat a.txt


###从根目录重新访问###
	cd /apps/..../


###访问当前目录的子目录###
	cd apps/.../


###创建新文件###
	touch a.txt


###显示当前目录###
	pwd

###历史使用过的命令###
	history  显示历史试用过的全部命令
	history 5       显示最近试用过的5个命令
	!5        执行历史编号为5的命令
	！ls    执行最后一次以“ls”结尾的命令


###命令的使用说明###
	man history          “history”这个命令的使用说明
######

###列表###
	ls 列出当前目录的文件和文件夹
	ls -l 列出文件的详细信息。
 	ls -a ｛文件夹目录｝ 不改变当前路径查看当前目录之下的某个文件夹的里面一级目录的内容列表
######

###查看磁盘使用情况###
	df -lh
######

###快捷键###
Ctrl+C  终止一个程序的运行， 比较暴力，就是发送Terminal到当前的程序，比如你正在运行一个查找功能，文件正在查找中，Ctrl+C就会强制结束当前的这个进程
Ctrl+Z  挂起一个当前运行的程序， 是把当前的程序挂起，暂停执行这个程序，比如你正在mysql终端中，需要出来搞点其他的文件操作，又不想退出mysql终端（因为下次还得输入用户名密码进入，挺麻烦），于是可以ctrl+z将mysql挂起，然后进行其他操作，然后输入fg回车后就可以回来，当然可以挂起好多进程到后台，然后fg 加编号就能把挂起的进程返回到前台。当然，配合bg和fg命令进行前后台切换会非常方便
Ctrl+D     退出当前的SHELL，相当于exit命令
######

###修改文件权限###
	chmod 764 a.txt
######

###任务调度###
 	crontab -e
然后弹出编辑界面  编写任务命令 如 02*** date > /home/mydate 表示每个月每天凌晨两点钟 执行‘date’这条命令，然后保存在 /home/mydate下，如果目录不存在的话，目录就会被创建
*****（分别表示第*分钟，小时，日，月，星期）
或者写  02*** /apps/mytask.sh 每天凌晨两点钟会自动执行  /apps/mytask.sh 这个shell文件
######

###执行文件###
	./a.sh        ./ 是执行。
	sh a.sh      sh 是执行bash读该shell文件，用的读权限。
######

###在查看列表的时候， 加上 | more或者 | less###
列表超过屏幕的时候自动分页，按空格键翻页
######

###查看进程###
	ps -ef 或者ps -aux
######

###查看当前目录的文件详情###
ls -lh
######

###结束进程 ###
	kill 1777     kill 加上进程号
	kill -9 1777 强制关闭一个进程
	killall 1777 关闭一个进程和他的子进程
######

###查看cpu，内存，进程，用户具体的使用情况###
	top 
	top -d 10    每隔10秒钟更新，动态监控
######

###退出###
	q
######

###在线下载安装软件（root）###
 	yum install -y pcre pcre-devel  
 	yum install -y zlib zlib-devel  
 	yum install -y openssl openssl-devel  
######

###创建目录（nginx-src）并进去；然后，从官方地址（http://nginx.org/）下载，解压，配置，编译，安装：###
	mkdir nginx-src && cd nginx-src  
	wget http://nginx.org/download/nginx-1.7.3.tar.gz  
	tar xzf nginx-1.7.3.tar.gz   
	cd nginx-1.7.3  
	./configure  
	make  
	make install  
	whereis nginx  
	nginx: /usr/local/nginx  
######

###vi撤销上一步操作###
按Esc后再按u
######

###SSH远程登录###
 	ssh apps@ip   ip为要连接的服务器的地址
######

###查看当前文件夹的大小###
 	du -sh 
######

###修改文件和文件夹的用户和用户组属性###
	chown -R user:group apps         将apps目录下的所有档案与子目录的拥有者皆设为 group 群体的使用者 user:                   
######

###服务器远程同步###
	rsync -avzptL ssh /apps/ apps@119.29.194.46:/apps/      把SSH远程的服务器的根目录apps（文件和安装的程序）同步到119.29.194.46的服务器apps根目录下
######

###创建软连接（相当于创建快捷方式）###
	ln -s /var/tomcat/tomcat-8/bin/startup.sh start.sh
######

###文件重命名###
	mv text1.sh text.2.sh
######

###sftp(linux服务器文件上传和下载)###
	sftp root(用户)@192.168.180.65(ip)
在sftp中get表示下载即得到；  put表示上传即放置
	sftp> get 远程主机下文件的路径   将文件保存到本地电脑的路径
	sftp> put 本地文件的路径 将文件版保存到远程主机的路径
######

###使用全局正则表达式搜索文本###
 	grep -r AAAA* 在当前目录下（-r递推到所有子目录）所有文本包含AAAA的文件，打印文本的路径和出现搜索关键词的地方
######

###压缩###
	zip test.zip test  把当前目录test文件压缩成test.zip
	zip -r test.zip test  把当前目录test文件夹压缩成test.zip
	tar czvf b2b2c.bak.201605091008.tar.gz b2b2c
######

###解压###
	tar zxvf b2b2c.2016.05.05.22.tar.gz
	tar xzf oneinstack-full.tar.gz
	unzip a.zip
######


###临时退出，进入一个对话框###
	system bash 进入
 	exit 退出临时框
######


系统
### 查看内核/操作系统/CPU信息
	uname -a
###查看操作系统版本 
	 head -n 1 /etc/issue 
### 查看CPU信息
	 cat /proc/cpuinfo 
### 查看计算机名
	 hostname 
### 列出所有PCI设备
	 lspci -tv 
### 列出所有USB设备
	 lsusb -tv 
### 列出加载的内核模块
	lsmod 
### 查看环境变量
	 env 
资源
### 查看内存使用量和交换区使用量
	 free -m 
### 查看各分区使用情况
	 df -h 
### 查看指定目录的大小
	 du -sh <目录名> 
### 查看内存总量
	 grep MemTotal /proc/meminfo 
### 查看空闲内存量
	 grep MemFree /proc/meminfo 
### 查看系统运行时间、用户数、负载
	 uptime 
	
	# cat /proc/loadavg # 查看系统负载
	磁盘和分区
	# mount | column -t # 查看挂接的分区状态
	# fdisk -l # 查看所有分区
	# swapon -s # 查看所有交换分区
	# hdparm -i /dev/hda # 查看磁盘参数(仅适用于IDE设备)
	# dmesg | grep IDE # 查看启动时IDE设备检测状况
	网络
	# ifconfig # 查看所有网络接口的属性
	# iptables -L # 查看防火墙设置
	# route -n # 查看路由表
	# netstat -lntp # 查看所有监听端口
	# netstat -antp # 查看所有已经建立的连接
	# netstat -s # 查看网络统计信息
	进程
	# ps -ef # 查看所有进程
	# top # 实时显示进程状态
	用户
	# w # 查看活动用户
	# id <用户名> # 查看指定用户信息
	# last # 查看用户登录日志
	# cut -d: -f1 /etc/passwd # 查看系统所有用户
	# cut -d: -f1 /etc/group # 查看系统所有组
	# crontab -l # 查看当前用户的计划任务
	服务
	# chkconfig --list # 列出所有系统服务
	# chkconfig --list | grep on # 列出所有启动的系统服务
	程序
	# rpm -qa # 查看所有安装的软件包
	linux常见命令的列表
	系统命令
	apropos whatis 显示和word相关的命令。 参见线程安全
	man -t man | ps2pdf - > man.pdf 生成一个PDF格式的帮助文件
	which command 显示命令的完整路径名
	time command 计算命令运行的时间
	time cat 开始计时. Ctrl-d停止。参见sw
	nice info 运行一个低优先级命令（这里是info）
	renice 19 -p $$ 使脚本运行于低优先级。用于非交互任务。
	目录操作
	cd - 回到前一目录
	cd 回到用户目录
	(cd dir && command) 进入目录dir，执行命令command然后回到当前目录
	pushd . 将当前目录压入栈，以后你可以使用popd回到此目录
	文件搜索
	alias l='ls -l --color=auto' 单字符文件列表命令
	ls -lrt 按日期显示文件. 参见newest
	ls /usr/bin | pr -T9 -W$COLUMNS 在当前终端宽度上打印9列输出
	find -name '*.[ch]' | xargs grep -E 'expr' 在当前目录及其子目录下所有.c和.h文件中寻找'expr'. 参见findrepo
	find -type f -print0 | xargs -r0 grep -F 'example' 在当前目录及其子目录中的常规文件中查找字符串'example'
	find -maxdepth 1 -type f | xargs grep -F 'example' 在当前目录下查找字符串'example'
	find -maxdepth 1 -type d | while read dir; do echo $dir; echo cmd2; done 对每一个找到的文件执行多个命令(使用while循环)
	find -type f ! -perm -444 寻找所有不可读的文件(对网站有用)
	find -type d ! -perm -111 寻找不可访问的目录(对网站有用)
	locate -r 'file[^/]*\.txt' 使用locate 查找所有符合*file*.txt的文件
	look reference 在（有序）字典中快速查找
	grep --color reference /usr/share/dict/words 使字典中匹配的正则表达式高亮
	归档 and compression
	gpg -c file 文件加密
	gpg file.gpg 文件解密
	tar -c dir/ | bzip2 > dir.tar.bz2 将目录dir/压缩打包
	bzip2 -dc dir.tar.bz2 | tar -x 展开压缩包 (对tar.gz文件使用gzip而不是bzip2)
	tar -c dir/ | gzip | gpg -c | ssh user@remote 'dd of=dir.tar.gz.gpg' 目录dir/压缩打包并放到远程机器上
	find dir/ -name '*.txt' | tar -c --files-from=- | bzip2 > dir_txt.tar.bz2 将目录dir/及其子目录下所有.txt文件打包
	find dir/ -name '*.txt' | xargs cp -a --target-directory=dir_txt/ --parents 将目录dir/及其子目录下所有.txt按照目录结构拷贝到dir_txt/
	( tar -c /dir/to/copy ) | ( cd /where/to/ && tar -x -p ) 拷贝目录copy/到目录/where/to/并保持文件属性
	( cd /dir/to/copy && tar -c . ) | ( cd /where/to/ && tar -x -p ) 拷贝目录copy/下的所有文件到目录/where/to/并保持文件属性
	( tar -c /dir/to/copy ) | ssh -C user@remote 'cd /where/to/ && tar -x -p'  拷贝目录copy/到远程目录/where/to/并保持文件属性
	dd bs=1M if=/dev/sda | gzip | ssh user@remote 'dd of=sda.gz' 将整个硬盘备份到远程机器上
	rsync (使用 –dry-run选项进行测试)
	rsync -P rsync://rsync.server.com/path/to/file file 只获取diffs.当下载有问题时可以作多次
	rsync --bwlimit=1000 fromfile tofile 有速度限制的本地拷贝，对I/O有利
	rsync -az -e ssh --delete ~/public_html/ remote.com:'~/public_html' 镜像网站(使用压缩和加密)
	rsync -auz -e ssh remote:/dir/ . && rsync -auz -e ssh . remote:/dir/ 同步当前目录和远程目录
	ssh (安全 Shell)
	ssh $USER@$HOST command 在$Host主机上以$User用户运行命令(默认命令为Shell)
	ssh -f -Y $USER@$HOSTNAME xeyes 在名为$HOSTNAME的主机上以$USER用户运行GUI命令
	scp -p -r $USER@$HOST: file dir/ 拷贝到$HOST主机$USER'用户的目录下
	ssh -g -L 8080:localhost:80 root@$HOST 由本地主机的8080端口转发到$HOST主机的80端口
	ssh -R 1434:imap:143 root@$HOST 由主机的1434端口转发到imap的143端口
	wget (多用途下载工具)
	(cd cmdline && wget -nd -pHEKk http://www.pixelbeat.org/cmdline.html) 在当前目录中下载指定网页及其相关的文件使其可完全浏览
	wget -c http://www.example.com/large.file 继续上次未完的下载
	wget -r -nd -np -l1 -A '*.jpg' http://www.example.com/ 批量下载文件到当前目录中
	wget ftp://remote/file[1-9].iso/ 下载FTP站上的整个目录
	wget -q -O- http://www.pixelbeat.org/timeline.html | grep 'a href' | head 直接处理输出
	echo 'wget url' | at 01:00 在下午一点钟下载指定文件到当前目录
	wget --limit-rate=20k url 限制下载速度(这里限制到20KB/s)
	wget -nv --spider --force-html -i bookmarks.html 检查文件中的链接是否存在
	wget --mirror http://www.example.com/ 更新网站的本地拷贝(可以方便地用于cron)
	网络(ifconfig, route, mii-tool, nslookup 命令皆已过时)
	ethtool eth0 显示网卡eth0的状态
	ethtool --change eth0 autoneg off speed 100 duplex full 手动设制网卡速度
	iwconfig eth1 显示无线网卡eth1的状态
	iwconfig eth1 rate 1Mb/s fixed 手动设制无线网卡速度
	iwlist scan 显示无线网络列表
	ip link show 显示interface列表
	ip link set dev eth0 name wan 重命名eth0为wan
	ip link set dev eth0 up 启动interface eth0(或关闭)
	ip addr show 显示网卡的IP地址
	ip addr add 1.2.3.4/24 brd + dev eth0 添加ip和掩码(255.255.255.0)
	ip route show 显示路由列表
	ip route add default via 1.2.3.254 设置默认网关1.2.3.254
	tc qdisc add dev lo root handle 1:0 netem delay 20msec 增加20ms传输时间到loopback设备(调试用)
	tc qdisc del dev lo root 移除上面添加的传输时间
	host pixelbeat.org 查寻主机的DNS IP地址
	hostname -i 查寻本地主机的IP地址(同等于host `hostname`)
	whois pixelbeat.org 查寻某主机或莫IP地址的whois信息
	netstat -tupl 列出系统中的internet服务
	netstat -tup 列出活跃的连接
	windows networking (samba提供所有windows相关的网络支持)
	smbtree 寻找一个windows主机. 参见findsmb
	nmblookup -A 1.2.3.4 寻找一个指定ip的windows (netbios)名
	smbclient -L windows_box 显示在windows主机或samba服务器上的所有共享
	mount -t smbfs -o fmask=666,guest //windows_box/share /mnt/share 挂载一个windows共享
	echo 'message' | smbclient -M windows_box 发送一个弹出信息到windows主机(XP sp2默认关闭此功能)
	文本操作 (sed使用标准输入和标准输出，如果想要编辑文件，则需添加<oldfile >newfile)
	sed 's/string1/string2/g' 使用string2替换string1
	sed 's/\(.*\)1/\12/g' 将任何以1结尾的字符串替换为以2结尾的字符串
	sed '/ *#/d; /^ *$/d' 删除注释和空白行
	sed ':a; /\\$/N; s/\\\n//; ta' 连接结尾有\的行和其下一行
	sed 's/[ \t]*$//' 删除每行后的空白
	sed 's/\([\\`\\"$\\\\]\)/\\\1/g' 将所有转义字符之前加上\
	seq 10 | sed "s/^/      /; s/ *\(.\{7,\}\)/\1/" 向右排N(任意数)列
	sed -n '1000p;1000q' 输出第一千行
	sed -n '10,20p;20q' 输出第10-20行
	sed -n 's/.*<title>\(.*\)<\/title>.*/\1/ip;T;q' 输出HTML文件的<title></title>字段中的 内容
	sort -t. -k1,1n -k2,2n -k3,3n -k4,4n 排序IPV4地址
	echo 'Test' | tr '[:lower:]' '[:upper:]' 转换成大写
	tr -dc '[:print:]' < /dev/urandom 过滤掉不能打印的字符
	history | wc -l 计算指定单词出现的次数
	集合操作 (如果是英文文本的话export LANG=C可以提高速度)
	sort file1 file2 | uniq 两个未排序文件的并集
	sort file1 file2 | uniq -d 两个未排序文件的交集
	sort file1 file1 file2 | uniq -u 两个未排序文件的差 集
	sort file1 file2 | uniq -u 两个未排序文件的对称差集
	join -a1 -a2 file1 file2 两个有序文件的并集
	join file1 file2 两个有序文件的交集
	join -v2 file1 file2 两个有序文件的差集
	join -v1 -v2 file1 file2 两个有序文件的对称差集
	数学
	echo '(1 + sqrt(5))/2' | bc -l 方便的计算器(计算 φ)
	echo 'pad=20; min=64; (100*10^6)/(pad+min)*8)' | bc 更复杂地计算，这里计算了最大的FastE包率
	echo 'pad=20; min=64; print (100E6)/(pad+min)*8)' | python Python处理数值的科学表示法
	echo 'pad=20; plot [64:1518] (100*10**6)/(pad+x)*8)' | gnuplot -persist 显示FastE包率相对于包大小的图形
	echo 'obase=16; ibase=10; 64206' | bc 进制转换(十进制到十六进制)
	echo $((0x2dec)) 进制转换(十六进制到十进制)(shell数学扩展)
	units -t '100m/9.69s' 'miles/hour' 单位转换(公尺到英尺)
	units -t '500GB' 'GiB' 单位转换(SI 到IEC 前缀)
	units -t '1 googol' 定义查找
	seq 100 | (tr '\n' +; echo 0) | bc 加N(任意数)列. 参见 add and funcpy
	日历
	cal -3 显示一日历
	cal 9 1752 显示指定月，年的日历
	date -d fri 这个星期五是几号. 参见day
	date --date='25 Dec' +%A 今年的圣诞节是星期几
	date --date '1970-01-01 UTC 2147483647 seconds' 将一相对于1970-01-01 00：00的秒数转换成时间
	TZ=':America/Los_Angeles' date 显示当前的美国西岸时间(使用tzselect寻找时区)
	echo "mail -s 'get the train' P@draigBrady.com < /dev/null" | at 17:45 在指定的时间发送邮件
	echo "DISPLAY=$DISPLAY xmessage cooker" | at "NOW + 30 minutes" 在给定的时间弹出对话框
	locales
	printf "%'d\n" 1234 根据locale输出正确的数字分隔
	BLOCK_SIZE=\'1 ls -l 用ls命令作类适于locale()文件分组
	echo "I live in `locale territory`" 从locale数据库中展开信息
	LANG=en_IE.utf8 locale int_prefix 查找指定地区的locale信息。参见ccodes
	locale | cut -d= -f1 | xargs locale -kc | less 显示在locale数据库中的所有字段
	recode (iconv, dos2unix, unix2dos 已经过时了)
	recode -l | less 显示所有有效的字符集及其别名
	recode windows-1252.. file_to_change.txt 转换Windows下的ansi文件到当前的字符集(自动进行回车换行符的转换)
	recode utf-8/CRLF.. file_to_change.txt 转换Windows下的ansi文件到当前的字符集
	recode iso-8859-15..utf8 file_to_change.txt 转换Latin9（西欧）字符集文件到utf8
	recode ../b64 < file.txt > file.b64 Base64编码
	recode /qp.. < file.txt > file.qp Quoted-printable格式解码
	recode ..HTML < file.txt > file.html 将文本文件转换成HTML
	recode -lf windows-1252 | grep euro 在字符表中查找欧元符号
	echo -n 0x80 | recode latin-9/x1..dump 显示字符在latin-9中的字符映射
	echo -n 0x20AC | recode ucs-2/x2..latin-9/x 显示latin-9编码
	echo -n 0x20AC | recode ucs-2/x2..utf-8/x 显示utf-8编码
	光盘
	gzip < /dev/cdrom > cdrom.iso.gz 保存光盘拷贝
	mkisofs -V LABEL -r dir | gzip > cdrom.iso.gz 建立目录dir的光盘镜像
	mount -o loop cdrom.iso /mnt/dir 将光盘镜像挂载到 /mnt/dir (只读)
	cdrecord -v dev=/dev/cdrom blank=fast 清空一张CDRW
	gzip -dc cdrom.iso.gz | cdrecord -v dev=/dev/cdrom - 烧录光盘镜像 (使用 dev=ATAPI -scanbus 来确认该使用的 dev)
	cdparanoia -B 在当前目录下将光盘音轨转录成wav文件
	cdrecord -v dev=/dev/cdrom -audio *.wav 将当前目录下的wav文件烧成音乐光盘 (参见cdrdao)
	oggenc --tracknum='track' track.cdda.wav -o 'track.ogg' 将wav文件转换成ogg格式
	磁盘空间 (参见FSlint)
	ls -lSr 按文件大小降序显示文件
	du -s * | sort -k1,1rn | head 显示当前目录下占用空间最大的一批文件. 参见dutop
	df -h 显示空余的磁盘空间
	df -i 显示空余的inode
	fdisk -l 显示磁盘分区大小和类型（在root下执行）
	rpm -q -a --qf '%10{SIZE}\t%{NAME}\n' | sort -k1,1n 显示所有在rpm发布版上安装的包，并以包字节大小为序
	dpkg-query -W -f='${Installed-Size;10}\t${Package}\n' | sort -k1,1n 显示所有在deb发布版上安装的包，并以KB包大小为序
	dd bs=1 seek=2TB if=/dev/null of=ext3.test 建立一个大的测试文件（不占用空间）. 参见truncate
	监视/调试
	tail -f /var/log/messages 监视Messages日志文件
	strace -c ls >/dev/null 总结/剖析命令进行的系统调用
	strace -f -e open ls >/dev/null 显示命令进行的系统调用
	ltrace -f -e getenv ls >/dev/null 显示命令调用的库函数
	lsof -p $$ 显示当前进程打开的文件
	lsof ~ 显示打开用户目录的进程
	tcpdump not port 22 显示除了ssh外的网络交通. 参见tcpdump_not_me
	ps -e -o pid,args --forest 以树状结构显示进程
	ps -e -o pcpu,cpu,nice,state,cputime,args --sort pcpu | sed '/^ 0.0 /d' 以CPU占用率为序显示进程
	ps -e -orss=,args= | sort -b -k1,1n | pr -TW$COLUMNS 以内存使用量为序显示进程. 参见ps_mem.py
	ps -C firefox-bin -L -o pid,tid,pcpu,state 显示指定进程的所有线程信息
	ps -p 1,2 显示指定进程ID的进程信息
	last reboot 显示系统重启记录
	free -m 显示(剩余的)内存总量(-m以MB为单位显示)
	watch -n.1 'cat /proc/interrupts' 监测文件/proc/interrupts的变化
	系统信息 (参见sysinfo)
	uname -a 查看内核/操作系统/CPU信息
	head -n1 /etc/issue 查看操作系统版本
	cat /proc/partitions 显示所有在系统中注册的分区
	grep MemTotal /proc/meminfo 显示系统可见的内存总量
	grep "model name" /proc/cpuinfo 显示CPU信息
	lspci -tv 显示PCI信息
	lsusb -tv 显示USB信息
	mount | column -t 显示所有挂载的文件系统并对齐输出
	dmidecode -q | less 显示SMBIOS/DMI 信息
	smartctl -A /dev/sda | grep Power_On_Hours 系统开机的总体时间
	hdparm -i /dev/sda 显示关于磁盘sda的信息
	hdparm -tT /dev/sda 检测磁盘sda的读取速度
	badblocks -s /dev/sda 检测磁盘sda上所有的坏扇区
	
	===== 交互 (参见linux keyboard shortcut database) =====
	
	readline Line editor used by bash, python, bc, gnuplot, ...
	screen 多窗口的虚拟终端, ...
	mc 强大的文件管理器，可以浏览rpm, tar, ftp, ssh, ...
	gnuplot 交互式并可进行脚本编程的画图工具
	links 网页浏览器
	miscellaneous
	alias hd='od -Ax -tx1z -v' 方便的十六进制输出。 (用法举例: ? hd /proc/self/cmdline | less)
	alias realpath='readlink -f' 显示符号链接指向的真实路径(用法举例: ? realpath ~/../$USER)
	set | grep $USER 在当前环境中查找
	touch -c -t 0304050607 file 改变文件的时间标签 (YYMMDDhhmm)
	python -m SimpleHTTPServer Serve current directory tree at http://$HOSTNAME:8000/
	
	linux下实时查看tomcat运行日志
	1、先切换到：cd usr/local/tomcat5/logs
	2、tail -f catalina.out
	3、这样运行时就可以实时查看运行日志了
	
	添加防火墙的端口
	1，修改添加
	vi /etc/sysconfig/iptables
	2， 添加
	3，service iptables stop
	4， service iptables start
	
	linux源码安装
	1， ./configure
	2. make
	3, make install
