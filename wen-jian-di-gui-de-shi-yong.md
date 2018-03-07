**I.统计一个目录文件下的文件大小**

1.定义一个函数，传入的参数为要计算的目录

2.定义一个统计大小的变量

3.打开这个目录，返回文件资源流 opendir

4.读取这个文件流里面的目录/文件,如果没有了则返回false，并关闭文件，返回计算值

5.定义目前的文件组合

6.判断是否为同级和上级

7.如果不是则，判断是否为目录，如果是则进行递归

8.如果不是，则统计大小

```
<?php
	header('content-type:text/html;charset=utf-8');
	//统计某个目录包括子目录的文件大小
	
	$dir_full_path = 'd:/tndb';
	$dir_size = getDirSize($dir_full_path);
	echo '<br> 大小是 ' . $dir_size;
	function getDirSize($dirname) {
		
		//变量，用于统计大小
		$dirsize=0;
		//打开目录
		$dir=opendir($dirname);
		//false !== 判断原因防止有文件夹或者文件名字就是0
		while(false !== ($filename=readdir($dir))){
			$file=$dirname . '/' .  $filename ;
			//如果不是 . 并且不是 .. 才去统计大小
			if($filename!="." && $filename!=".."){
				if(is_dir($file)){
					//如果是一个目录，就递归继续统计
					$dirsize += getDirSize($file); 
				}else{
					//如果是一个文件，就直接统计大小
					$dirsize += filesize($file);
				}
			}
		}
		closedir($dir);
		return $dirsize;
	}
```

  


**II.删除一个目录下所有文件**

1.定义一个函数，传入的参数为要删除的目录

2.打开这个目录，返回文件资源流 

3.读取这个文件流里面的目录/文件，如果没有则返回FALSE，并关闭文件，删除这个目录

4.定义目前的文件组合

5.判断是否为同级或上级，如果是，进行下一次循环

6.如果不是同级或上级；判断是否目录，如果是则删除这个目录

7.如果是文件，则删除文件

```
<?php
	header('content-type:text/html;charset=utf-8');
	//删除整个目录
	//定义一个目录
	$dir_full_path = 'd:/tndb';
	rrmdir($dir_full_path);
	function rrmdir($src) {
		$dir = opendir($src);
		while(false !== ( $file = readdir($dir)) ) {
				if (( $file != '.' ) && ( $file != '..' )) {
					$full = $src . '/' . $file;
					if ( is_dir($full) ) {
						rrmdir($full);
					}
					else {
						//删文件
						unlink($full);
					}
				}
		}
		closedir($dir);
		rmdir($src);
	}
```

  


**III.拷贝一个目录到另一个目录**

1.定义一个函数，传入的参数为要拷贝的文件目录，一个是要拷贝到的文件目录

2.判断拷贝的目录是文件还是目录，如果是文件则进行拷贝，或者返回FALSE退出

3.是目录，则先创建目标目录文件，

4.将被拷贝的文件目录扫描为包含着目录和文件的目录

5.如果不是空文件夹，则如果是目录，进行递归拷贝，如果为空，则返回TRUE

6.是文件，则直接进行拷贝

7.如果是同级和上级，则直接跳过

```
<?php
	header('content-type:text/html;charset=utf-8');
	//拷贝一个文件夹到另外一个目录下 
	//定义一个目录分隔符
	define('DS', DIRECTORY_SEPARATOR); 
	
	$path="d:/hspweb";
	//这个 $desc目录可以不存在,也可以存在, 会把 e:/hspweb/ 目录
	//下的所有文件及其子目录拷贝到 指定目录 $desc下 [注:只含e:/hspweb本身这个目录名]
	$dest="e:/mymvc300";
	copy_r($path,$dest);
	echo 'ok';
    function copy_r( $path, $dest )
    {
		//先判断你的被拷贝的$path 是不是一个目录
        if( is_dir($path) )
        {
			//创建目标目录
            @mkdir( $dest );
            //调用了一个 scandir函数(扫描)
			$objects = scandir($path);
			
			//如果不是空文件夹
			if( sizeof($objects) > 0 )
            {
                foreach( $objects as $file )
                {
                    if( $file == "." || $file == ".." )
                        //不要继续下走，执行下一次foreach
						continue;
                    
                    if( is_dir( $path.DS.$file ) )
                    {
						//如果是一个目录，就继续调用copy_r
                        copy_r( $path.DS.$file, $dest.DS.$file );
                    }
                    else
                    { 
						//如果是一个文件，就直接拷贝
                        copy( $path.DS.$file, $dest.DS.$file );
                    }
                }
            }
            return true;
        }
        elseif( is_file($path) )
        {
            return copy($path, $dest);
        }
        else
        {
            return false;
        }
    }
```

  


