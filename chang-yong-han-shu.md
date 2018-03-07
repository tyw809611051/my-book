**一、写入文件**

1.打开资源（文件）fopen\($filename,$mode\)

2.写文件fwrite\($handle,$str\)

3.关闭文件fclose\($handle\)

4.一步写入file\_put\_contents\($filename,$str,$mode\) FILE\_APPEND LOCK\_EX

}



**二、读文件**

1.读文件fread\($handle,字节数\)

2.读一行fgets\($handle\);

3.读一个字符fgetc\($handle\)

4.读成一个数组中file\($filename\)

5.一步读取file\_get\_contents\($filename\)



**三、 目录操作**

1，建目录mkdir\($dirname\)

2，删除目录rmdir\($dirname\)

3，打开目录句柄opendir\($dirname\)

4，读取目录条数readdir\($handle\)

5，关闭目录资源closedir\($handle\)

6，重置目录资源rewinddir\($dirname\);



**四、目录和文件操作**

1， 检查文件或目录是否存在file\_exists\($filename\)

2，文件或者目录重命名rename\($file\)



**五、 文件操作**

1拷贝文件copy\('原文件','目标文件'\)

2删除文件unlink\($filename\)

3获取文件大小filesize\($filename\)

4取得文件的创建时间filectime\($filename\)

5取得文件的访问时间fileatime\($filename\)

6取得文件的修改时间filemtime\($filename\)



**六、路径操作**

1获取路径dirname\($path\)

2获取文件名basename\($path\)

3获取路径信息pathinfo\($path\)  


**七、数组函数（极其重要）**

#### 本帖隐藏的内容

1.在数组的开头插入一个元素array\_unshift\($arr,$v\)

2.在数组的尾部添加数组元素array\_push\($arr,$v,$v1...\)

3.将数组的第一个元素移出，并返回此元素array\_shift\($arr\)

4.在数组的尾部删除元素array\_pop\($arr\)

5.将数组用$separator连接成一个字符串implode\($a,$arr\)

6.检测变量是否是数组is\_array\($arr\)

7.获得数组的键名array\_keys\($arr\)

8.获得数组的值array\_values\($arr\)

9.检索$value是否在$arr中，返回布尔值in\_array\($v,$arr\)

10.检索数组$arr中，是否有$key这个键名array\_key\_exists\($k,$arr\)

11.检索$value是否在$arr中，若存在返回键名Array\_search\($value, $arr\)

12.将一个数组逆向排序，如果第二个参数为true，则保持键名Array\_reverse\($arr, true\)

13.交换数组的键和值 Array\_flip\($arr\)

14.统计数组元素的个数 Count\($arr\)

15.统计数组中所有值的出现次数 Array\_count\_values\($arr\)

16.移除数组中的重复值 Array\_unique\($arr\)

17.值由小到大排序 Sort\($arr\)

18.值由大到小排序 Rsort\($arr\)

19.键由小到大排序 ksort\($arr\)

20.键由大到小排序 krsort\($arr\)

21.随机从数组中取得$num个元素 Array\_rand\($arr, $num\)

22.对数组的所有元素求和Array\_sum\($arr\)

23.合并数组 array\_merge\($arr,$arr\)  


**八、字符串函数（极其重要）**

1.输出字符串 echo\($str\) echo

2.原样输出（区分单引号和双引号） print\($str\)

3.输出字符串，结束脚本执行 Die\($str\):die\($str\) die;

4.输出字符串，结束脚本执行 exit\($str\) exit;

5.输出格式化字符串 printf\($str,$p1,...\)

6.不直接输出格式化的字符串，返回格式化的字符串，保存到变量中 sprintf\($str,$p1,...\)

7.打印变量的相关信息 var\_dump\($p\)

8.字符串转换为小写 strtolower\($str\)

9.字符串转换为大写 strtoupper\($str\)

10.将字符串的第一个字符转换为大写 ucfirst\($str\)

11.将字符串中每个单词转换为大写 ucwords\($str\)

12.去除字符串两端的空白字符。 Trim\($str,' ,'\)

13.去除字符串左边空白字符。 Ltrim\($str\)

14.去除字符串右边空白字符。Rtrim\($str\)

空白字符：""，"\t"，"\n"，"\r"，”\0”

15取得字符串长度 strlen\($str\)

16统计包含的字符串个数 substr\_count\($str,’子串’\)

17返回字符串$string中由$start开始，长度为$length的子字符串

Substr\($string ,$start\[,$length\]\)

18返回字符串$string中，$search第一次出现到字符串结束的子字符串。

Strstr\($string,$search\)

strrchr

—

查找指定字符在字符串中的最后一次出现

19查找$search在$str中第一次位的置，从$offset开始。

Strpos\($str,$search\[,int $offset\]\)

20.查找$search在$str中最后一次的位置，从$offset开始

Strrpos\($str,$search\[,int $offset\]\)

21.替换$str中的全部$search为 $replace。

Str\_replace\($search,$replace,$str\)

22.重复输出指定的字符串

Str\_repeat\(\)

23.加密字符串

Md5\(\)

24.字符串翻转

Strrev\(\)

25.使用一个字符串分割另一个字符串,形成一个数组//把字符串变成数组

Explode\(“分隔符”,$str\);

