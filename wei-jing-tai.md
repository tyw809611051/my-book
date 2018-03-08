优势：
    地址更简洁，便于用户记忆
    对SEO友好

实现伪静态 
```![](/img/Language/PHP/Basic/190a915b-c469-4b09-bc44-f5b01ad25f5f.jpg)
 //初始化pathinfo
    private function initPathInfo()
    {
    	if(isset($_SERVER['PATH_INFO'])){
    		//获得url地址的信息
    		$path = $_SERVER['PATH_INFO'];	//"/home/index/indexAction.html"
    		 
    		//2. .html是障眼法，迷惑搜索引擎、用户，在这里没有实际作用，所以我们先替换掉
    		$postfix = strrchr($path, '.');
    		$path = str_replace($postfix, '', $path);	//	"/home/index/indexAction"
    		 
    		//3. 把第一个 / 替换掉,从索引为1的地方开始截取，如果不写第三个参数就表示截取到末尾
    		$path = substr($path, 1);				//	"home/index/indexAction"
    		 
    		//4. 将字符串根据  /  炸开
    		$arr = explode('/', $path);		//如果地址栏就是3个参数，可以获得mca
    		//思考：如果地址栏中不是3个参数的时候，怎么处理一下？
    		$length = count($arr);
    		if($length==1){
    			//确定模块
    			$_GET['m'] = $arr[0];
    		}elseif ($length==2){
    			//确定模块
    			$_GET['m'] = $arr[0];
    			//控制器
    			$_GET['c'] = $arr[1];
    		}elseif ($length==3){
    			//确定模块
    			$_GET['m'] = $arr[0];
    			//控制器
    			$_GET['c'] = $arr[1];
    			//方法
    			$_GET['a'] = $arr[2];
    		}else{
    			//如果参数大于3个，从第4个开始（下标为3的），每两个是一对  page=>6  id=>3
    			//确定模块
    			$_GET['m'] = $arr[0];
    			//控制器
    			$_GET['c'] = $arr[1];
    			//方法
    			$_GET['a'] = $arr[2];
    			
    			//生成这样的结果：$_GET['page'] = 6   $_GET['id']=3;
    			for ($i=3;$i<$length;$i+=2){
    				$_GET[$arr[$i]] = $arr[$i+1];
    			}
    			//echo '<pre>';
    			//var_dump($_GET);
    		}
    	}
    }
```
1.1隐藏入口文件
![](/img/Language/PHP/static/95eecb02-eb0d-4b32-b22d-fa40d079982a.jpg)
1.需要在当前项目的根目录下面创建一个.htaccess文件
2.apache开启了rewrite_module这个模块
![](/img/Language/PHP/static/0.927690380718559.png)

3.  ![](/img/Language/PHP/static/clip_image00209928989-9d55-4c30-951b-1f908b053c33.jpg)
 
4.最后完成.htaccess文件
    
    