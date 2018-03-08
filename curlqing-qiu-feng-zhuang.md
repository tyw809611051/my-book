```
<?php
namespace framework\tools;
/*
 * HttpRequest类是用来实现网络传输一些资源 get/post
 */
class HttpRequest
{
	//是否返回结果，默认是返回结果而不是直接显示
	private $is_return = 1;
	
	public function __set($p,$v){
		if(property_exists($this, $p)){
			$this -> $p = $v;
		}
	}	
	//发出http请求（get、post）
	//既能发出get请求，又能发出post请求,如果$data是空数组就发出get请求，如果$data有数据，就发出post请求
	public function send($url,$data=array())
	{
		//1. 初始化curl
		$curl = curl_init();
		
		//2. 设置请求的服务器地址url地址		
		curl_setopt($curl, CURLOPT_URL, $url);
		//跳过证书验证这个环节
		curl_setopt($curl, CURLOPT_SSL_VERIFYHOST, false);
		curl_setopt($curl, CURLOPT_SSL_VERIFYPEER, false);		
		if(!empty($data)){
			//说明提交数据了，就以post方式请求
			//post方式发出请求
			curl_setopt($curl, CURLOPT_POST, true);			
			curl_setopt($curl, CURLOPT_POSTFIELDS, $data);
		}
		//3. 发出请求		
		//如果只需要返回结果，而不是直接显示
		if($this->is_return){
			curl_setopt($curl, CURLOPT_RETURNTRANSFER, true);
			$result = curl_exec($curl);
			if($result===false){
				$msg['status'] = 0;
				$msg['msg'] = curl_error($curl);
				return $msg;
			}else{
				$msg['status'] = 1;
				$msg['msg'] = $result;
				return $msg;
			}			
		}else{
			curl_exec($curl);
		}
		//4. 关闭资源
		curl_close($curl);
	}
}
```
1.1curl 模拟get请求
    ![](/img/Language/PHP/curl/0.29156531509943306.png) 

通过配置项设置返回的结果怎么处理    
    ![](/img/Language/PHP/curl/0.016661139205098152.png) 


如果采集https协议的网络资源    
 ![](/img/Language/PHP/curl/0.23174252011813223.png) 


1.1curl 模拟post请求   
![](/img/Language/PHP/curl/0.19076906610280275.png) 


1.1curl模拟文件上传   
![](/img/Language/PHP/curl/0.5635815234854817.png) 

curl充当的就是将文件以表单的形式（input type=”file”）的形式传递到服务器，服务器接收到数据之后，就可以移动该文件了
 

1.1curl模拟cookie登录   

通过curl模拟cookie登录，需要两个步骤：
1.请求loginHandleAction，将登录状态保存到session
2.请求indexAction时，随身携带PHPSESSID
    ![](/img/Language/PHP/curl/clip_image0022990a2d6-a506-49ef-bd39-d7a0559b7e8d.jpg) 


