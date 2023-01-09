# centos 7 查看磁盘io ，找出占用io读写很高的进程

## 1，先用iostat查看磁盘io 是否读写负载很高

	用iostat -x 1 10

	如果 iostat 没有，要 yum install sysstat安装这个包，第一眼看下图红色圈圈的那个如果%util接近100%,表明I/O请求太多,I/O系统已经满负荷，磁盘可能存在瓶颈,一般%util大于70%,I/O压力就比较大，读取速度有较多的wait，然后再看其他的参数，

	rrqm/s:每秒进行merge的读操作数目。即delta(rmerge)/s 
	wrqm/s:每秒进行merge的写操作数目。即delta(wmerge)/s 
	r/s:每秒完成的读I/O设备次数。即delta(rio)/s 
	w/s:每秒完成的写I/0设备次数。即delta(wio)/s 
	rsec/s:每秒读扇区数。即delta(rsect)/s 
	wsec/s:每秒写扇区数。即delta(wsect)/s 
	rKB/s:每秒读K字节数。是rsec/s的一半，因为每扇区大小为512字节 

	wKB/s:每秒写K字节数。是wsec/s的一半 
	avgrq-sz:平均每次设备I/O操作的数据大小(扇区)。即delta(rsect+wsect)/delta(rio+wio) 
	avgqu-sz:平均I/O队列长度。即delta(aveq)/s/1000(因为aveq的单位为毫秒) 
	await:平均每次设备I/O操作的等待时间(毫秒)。即delta(ruse+wuse)/delta(rio+wio) 
	svctm:平均每次设备I/O操作的服务时间(毫秒)。即delta(use)/delta(rio+wio) 
	%util:一秒中有百分之多少的时间用于I/O操作,或者说一秒中有多少时间I/O队列是非空的

 

## 2，找出使用io高的进程的工具  iotop

	yum install iotop -y

	直接执行 iotop 命令，然后看下图的显示，查看那个进程的读写，找出进程
	————————————————
	版权声明：本文为CSDN博主「saga_gallon」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
	原文链接：https://blog.csdn.net/saga_gallon/article/details/82891709
