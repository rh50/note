
# vmstat

	vmstat命令，是 Virtual Meomory Statistics（虚拟内存统计）的缩写，可用来监控 CPU 使用、进程状态、内存使用、虚拟内存使用、硬盘输入/输出状态等信息。此命令的基本格式有如下 2 种：


 	-a 的含义是用 inact/active（活跃与否） 来取代 buff/cache 的内存输出信息。除此之外，表 1 罗列出了 vmstat 命令的第二种基本格式中常用的选项及各自的含义。


	表1 vmstat命令常用选项及含义
	选项 含义
	-fs
		-f：显示从启动到目前为止，系统复制（fork）的程序数，此信息是从 /proc/stat 中的 processes 字段中取得的。
		-s：将从启动到目前为止，由一些事件导致的内存变化情况列表说明。
	-S 单位
		令输出的数据显示单位，例如用 K/M 取代 bytes 的容量。
	-d
		列出硬盘有关读写总量的统计表。
	-p
		分区设备文件名 	查看硬盘分区的读写情况。



	表 2 vmstat 命令输出字段及含义 
	字段 含义
	procs
		进程信息字段：
			-r：等待运行的进程数，数量越大，系统越繁忙。 
			-b：不可被唤醒的进程数量，数量越大，系统越繁忙。
	memory
		内存信息字段：
			-swpd：虚拟内存的使用情况，单位为 KB。
			-free：空闲的内存容量，单位为 KB。
			-buff：缓冲的内存容量，单位为 KB。
			-cache：缓存的内存容量，单位为 KB。
	swap 
		交换分区信息字段：
			-si：从磁盘中交换到内存中数据的数量，单位为 KB。
			-so：从内存中交换到磁盘中数据的数量，单位为 KB。
			这两个数越大，表明数据需要经常在磁盘和内存之间进行交换，系统性能越差。
	io 
		磁盘读/写信息字段：
			-bi：从块设备中读入的数据的总量，单位是块。
			-bo：写到块设备的数据的总量，单位是块。
			这两个数越大，代表系统的 I/O 越繁忙。
	system
		系统信息字段：
			-in：每秒被中断的进程次数。
			-cs：每秒进行的事件切换次数。
			这两个数越大，代表系统与接口设备的通信越繁忙。
	cpu
		CPU信息字段：
			-us：非内核进程消耗 CPU 运算时间的百分比。
			-sy：内核进程消耗 CPU 运算时间的百分比。
			-id：空闲 CPU 的百分比。
			-wa：等待 I/O 所消耗的 CPU 百分比。
			-st：被虚拟机所盗用的 CPU 百分比。

