
# MySQL权限

## p1
	All/All Privileges权限代表全局或者全数据库对象级别的所有权限
	Alter权限代表允许修改表结构的权限，但必须要求有create和insert权 限配合。如果是rename表名，则要求有alter和drop原表，create和 insert新表的权限
	Alter routine权限代表允许修改或者删除存储过程、函数的权限
	Create权限代表允许创建新的数据库和表的权限
	Createroutine权限代表允许创建存储过程、函数的权限
	Createtablespace权限代表允许创建、修改、删除表空间和日志组的权 限
	Create temporary tables权限代表允许创建临时表的权限
	Createuser权限代表允许创建、修改、删除、重命名user的权限
	Createview权限代表允许创建视图的权限

## p2
	• Delete权限代表允许删除行数据的权限
	• Drop权限代表允许删除数据库、表、视图的权限，包括truncatetable命令
	• Event权限代表允许查询，创建，修改，删除MySQL事件
	• Execute权限代表允许执行存储过程和函数的权限
	• File权限代表允许在MySQL可以访问的目录进行读写磁盘文件操作，可使用 的命令包括load data infile,select ... into outfile,load file()函数
	• Grant option权限代表是否允许此用户授权或者收回给其他用户你给予的权 限
	• Index权限代表是否允许创建和删除索引
	• Insert权限代表是否允许在表里插入数据，同时在执行analyze table,optimize table,repair table语句的时候也需要insert权限
	• Lock权限代表允许对拥有select权限的表进行锁定，以防止其他链接对此表 的读或写

## p3
	• Process权限代表允许查看MySQL中的进程信息，比如执行showprocesslist,
	• Reference权限是在5.7.6版本之后引入，代表是否允许创建外键
	• Reload权限代表允许执行flush命令，指明重新加载权限表到系统内存中， refresh命令代表关闭和重新开启日志文件并刷新所有的表
	• Replication client权限代表允许执行show master status,show slave status,show binary logs命令
	• Replication slave权限代表允许slave主机通过此用户连接master以便建立主从 复制关系
	• Select权限代表允许从表中查看数据，某些不查询表数据的select执行则不需 要此权限，如Select 1+1，Select PI()+2;而且select权限在执行update/delete 语句中含有where条件的情况下也是需要的
	• Showdatabases权限代表通过执行showdatabases命令查看所有的数据库名
	• Show view权限代表通过执行show create view命令查看视图创建的语句mysqladmin processlist, show engine等命令

## p4
	• Shutdown权限代表允许关闭数据库实例，执行语句包括mysqladmin shutdown
	• Super权限代表允许执行一系列数据库管理命令，包括kill强制关闭某个连接 命令，change master to创建复制关系命令，以及create/alter/drop server等命 令
	• Trigger权限代表允许创建，删除，执行，显示触发器的权限
	• Update权限代表允许修改表中的数据的权限
	• Usage权限是创建一个用户之后的默认权限，其本身代表连接登录权限
