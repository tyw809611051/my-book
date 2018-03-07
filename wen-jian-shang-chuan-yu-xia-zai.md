//文件上传的验证步骤

// 1.验证是否有自身带有的错误

// 2.验证大小是否超出限制

// 3.分离文件后缀，定义文件存放目录名（随机生成文件名前缀）

// 4.验证后缀名是否符合

// 5.验证文件类型是否符合

// 6.用fileinfo验证文件类型

// 7.判断文件要存放的目录是否存在，

// 8.移动目录

```
class Upload
{
    //成员属性
    private $_upload_path;              //上传的路径
    private $_max_size = 2*1024*1024;   //上传的文件最大限制
    private $_prefix;                   //上传到服务器的文件的前缀
    private $_allow_type = array('.jpg','.png','.gif'); //允许的文件后缀
    //允许的文件的mime类型
    private $_allow_mime_type =
    array('image/png', 'image/gif', 'image/jpeg', 'image/pjpeg', 'image/x-png');
    
    //提供对应的set方法，允许用户在类的外面设置属性的值
    public function setUploadPath($upload_path)
    {
        $this -> _upload_path = $upload_path;
    }
    public function setMaxSize($max_size)
    {
        $this -> _max_size = $max_size;
    }
    public function setPrefix($prefix)
    {
        $this -> _prefix = $prefix;
    }
    public function setAllowType($types)
    {
        $this -> _allow_type = $types;
    }
    public function setAllowMimeType($mimes)
    {
        $this -> _allow_mime_type = $mimes;
    }
        
    //成员方法
    public function doUpload($fileinfo)
    {
        //echo 'ok';
        //判断用户是否上传了文件
        if($fileinfo['error']!=0){
            echo '请选择上传的文件';
            exit;
        }
        //参数1：临时的文件
        //参数2：目的地
        //接收文件（二进制流数据）使用$_FILES接收
        //1. 限制上传的文件的大小不能超过2MB
        if($fileinfo['size']>$this->_max_size){
            echo '文件太大了，我的服务器受不了<br>';
            exit; //因为不需要返回结果，而仅仅是让代码在这里停止
        }
        //2. 随机生成文件名，防止上传同一张图片时文件名冲突
        
        $file_name = uniqid($this->_prefix,true);
        //拼接后缀,认为一个文件最后一次出现的.后面的就是后缀
        $ext = strrchr($fileinfo['name'], '.');
    
        //3. 以日期格式创建子目录
        $sub_path = date('Ymd').'/';
        if(!is_dir($this->_upload_path.$sub_path)){
            mkdir($this->_upload_path.$sub_path,0777,true);
        }
        $file_name = $this->_upload_path.$sub_path.$file_name . $ext;
        //die($file_name);
    
        //4. 验证用户上传的文件类型
        
        //获得用户上传的文件类型
        if(!in_array($ext,$this->_allow_type)){
            echo '文件类型不支持';
            exit;
        }
        //验证mime类型（网络中传输文件时的文档类型）
        
        if(!in_array($fileinfo['type'], $this->_allow_mime_type)){
            echo '文件类型不支持';
            exit;
        }
        //通过Finfo获得文件的类型
        $finfo = new Finfo(FILEINFO_MIME_TYPE);
        $mime_type = $finfo -> file($fileinfo['tmp_name']);
        //die($mime_type);
        if(!in_array($mime_type, $this->_allow_mime_type)){
            echo '文件类型不支持';
            exit;
        }
        if(move_uploaded_file($fileinfo['tmp_name'], $file_name)){
            return true;
        }else{
            return false;
        }
    }
}
```

  


// 可更改的属性值：文件保存目录，文件大小设置，文件后缀类型数组，文件类型数组，文件名前缀

  


// 文件下载步骤

// 1.获取文件名变量完整路径

// 2.如果未达到的话，就要拼接文件名

// 3.设置文件名编码，

// 4.判断文件路径名是否存在

// 5.设置header头，以二进制流的形式

// 6.打开这个文件，

// 7.读取文件直到末尾，并输出流

// 8.关闭文件

```
//接收超链接身上的参数
   $filename = $_GET['filename'];
   if($filename == ''){
       echo '没有参数，不知道下载哪一个';
       exit;
   }
   
   //根据地址栏上 传递的参数获得对应的文件地址
   //echo __DIR__;    //directory，当前文件所在的目录
   define('DOWNLOAD_PATH',str_replace('\\', '/', __DIR__).'/');
   //echo DOWNLOAD_PATH;
   $file_full_path = DOWNLOAD_PATH.'img/'.$filename;
   
   //操作系统的文件是gbk编码，php使用的是utf-8编码
   $file_full_path = iconv('utf-8', 'gbk', $file_full_path);
   
   //echo $file_full_path;
   if(!file_exists($file_full_path)){
       echo '骗我，没有这个文件怎么下载';
       exit;
   }
   //获得文件大小
   $file_size = filesize($file_full_path);
   
   //通过php的头信息进行文件下载
   //告诉浏览器，我向你回应的是一个二进制流文件
   header("Content-type: application/octet-stream");
   //按照字节大小返回
   header("Accept-Ranges: bytes");
   //下载时显示文件大小
   header("Content-Length: $file_size");
   //这里客户端的弹出对话框，对应的文件名
   header("Content-Disposition: attachment; filename=".$filename);
    
   //通过文件函数，读取文件里面的资源，再将资源输出
   $fp = fopen($file_full_path, 'r');
   //读取里面的资源,只要还没有到达文件的结尾就一直读取
   while(!feof($fp)){
       $data = fread($fp, 1024);
       echo $data;
   }
   fclose($fp);
   

```

  


