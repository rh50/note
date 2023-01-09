
# php将数组或对象原样写入或保存到文件有三种方法可以实现
	https://www.cnblogs.com/ryanzheng/p/9086115.html

## 第一种方法是使用serialize，
```php
$file='./cache/phone.php'; 
$array=array('color'=> array('blue','red','green'),'size'=> array('small','medium','large')); 
//缓存 
if(false!==fopen($file,'w+')){ 
	file_put_contents($file,serialize($array));//写入缓存 
} 
//读出缓存 
$handle=fopen($file,'r'); 
$cacheArray=unserialize(fread($handle,filesize($file)));
```

## 第二种方法是使用print_r，
```php
$b = array (
	'm' => 'monkey', 
	'foo' => 'bar', 
	'x' => array ('x', 'y', 'z'),
);
$results = print_r($b, true); 
file_put_contents('filename.txt', print_r($b, true));
```

## 第三种方法是使用var_export，
```php
$file='./cache/phone.php'; 
$array=array('color'=> array('blue','red','green'),'size'=> array('small','medium','large')); 
//缓存 
$text='<?php $rows='.var_export($array,true).';'; 
if(false!==fopen($file,'w+')){ 
	file_put_contents($file,$text); 
}else{ 
	echo '创建失败'; 
}
```
