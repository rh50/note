
## PHP获取当前文件路径信息的方法
https://www.cnblogs.com/timelesszhuang/p/4330063.html

文件名  test.php 

1、__FILE__ 获取 “路径 + 文件名” ： /var/www/test/test.php 
echo __FILE__;

//取得当前文件的路径：用魔术常量 __FILE__，这里的路径包含了文件名

2、basename获取 “文件名 ”： test.php 
echo basename(__FILE__);

3、basename获取“不含扩展名的文件名”：test 

echo basename(__FILE__, '.php'); 

 

4、dirname获取“到此目录前的完整 PATH, 不含文件名 ”：/var/www/test 
echo dirname(__FILE__);

//去掉上面路径的文件名，得到纯路径：dirname(__FILE__)

5、dirname获取“当前文件的上层目录 PATH”： /var/www 

echo dirname(dirname(__FILE__));

 

6、realpath 返回一层目录到本文件的根目录：

realpath(dirname(__FILE__).'/../')

 

7、当前请求的 Host: 头部的内容 即域名信信息

echo $_SERVER['HTTP_HOST'];

8、 $_SERVER['PHP_SELF'];
http://www.yoursite.com/example/ — – — /example/index.php
http://www.yoursite.com/example/index.php — – — /example/index.php
http://www.yoursite.com/example/index.php?a=test — – — /example/index.php
http://www.yoursite.com/example/index.php/dir/test — – — /dir/test

当我们使用$_SERVER['PHP_SELF']的时候，无论访问的URL地址是否有index.php，它都会自动的返回 index.php.但是如果在文件名后面再加斜线的话，就会把后面所有的内容都返回在$_SERVER['PHP_SELF']。

9、$_SERVER['REQUEST_URI']
http://www.yoursite.com/example/ — – — /
http://www.yoursite.com/example/index.php — – — /example/index.php
http://www.yoursite.com/example/index.php?a=test — – — /example/index.php?a=test
http://www.yoursite.com/example/index.php/dir/test — – — /example/index.php/dir/test

$_SERVER['REQUEST_URI']返回的是我们在URL里写的精确的地址，如果URL只写到”/”，就返回 “/”

10、$_SERVER['SCRIPT_NAME']
http://www.yoursite.com/example/ — – — /example/index.php
http://www.yoursite.com/example/index.php — – — /example/index.php
http://www.yoursite.com/example/index.php — – — /example/index.php
http://www.yoursite.com/example/index.php/dir/test — – — /example/index.php

在所有的返回中都是当前的文件名/example/index.php
echo $_SERVER['SCRIPT_NAME'];

当前正在执行脚本的文件相对网站根目录地址，但当该文件被其他文件引用时，只显示引用文件的相对地址，不显示该被引用脚本的相对地址。
11、 $_SERVER['DOCUMENT_ROOT'];

当前运行脚本所在的文档根目录。在服务器配置文件中定义
