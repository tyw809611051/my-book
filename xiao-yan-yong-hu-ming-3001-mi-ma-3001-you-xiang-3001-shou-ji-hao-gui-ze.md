```
<?php 
namespace framework\tools;
class Verify {
	//该属性保存错误信息
	private $error = array();
	
	//给用户显示错误信息
	public function showError()
	{
		$message = '';
		foreach ($this->error as $row)
		{
			$message .= $row.'<br>';
		}
		return $message;
	}
	/**
	 * 〈验证用户名是否符合规则〉
	 * 〈用户名规则：6-30位，字母开头，〉
	 * @param [$username]     [验证的用户名]
	 * @param [$min]     [最少多少位]
	 * @param [$max]     [最多多少位]
	 * @return[返回类型说明]
	 */
	public function verifyUsername($username,$min=6,$max=30) {
		// 建立规则
		$reg = '/^[a-zA-Z]\w{'.$min.','.$max.'}$/';
		preg_match($reg,$username,$match);
		// 判断结果
		if(!$match) {
			// 不符合规则
			$this->error[] = '<font color="red">用户名必须在'.$min.'-'.$max.'位字母、数字、或下划线，字母开头</font>';
			return false;
		} else {
			return true;
		}
	}
	/**
	 * 〈验证密码是否符合规则〉
	 * 〈密码规则：6-20位，字母，数字，下划线，任意字符都可〉
	 * @param [参数1]     [参数1说明]
	 * @param [参数2]     [参数2说明]
	 * @return[返回类型说明]
	 */
	public function verifyPass($pass,$min=6,$max=20) {
		// 建立规则
		$reg = '/^[a-zA-Z]{'.$min.','.$max.'}$/';	#纯字母组合
		$reg1 = '/^[\d]{'.$min.','.$max.'}$/';	#纯数字组合
		$reg2 = '/^[\w]{'.$min.','.$max.'}$/';	#字母和数字组合
		$reg3 = '/^[a-zA-Z0-9~!@#$%\^&\*\(\)-_\+=\[\]\{\}\|\;:\'"<>,\.\?\/]{6,20}$/';	#字母数字任意字符组合
		preg_match($reg, $pass,$res1);
		preg_match($reg1, $pass,$res2);
		preg_match($reg2, $pass,$res3);
		preg_match($reg3, $pass,$res4);
		if($res1 || $res2) {
			//通过了说明是字母或纯数字的
			echo '纯字母、数字的密码，强度一般<br>';
			return true;
		} else if($res3) {
			//说明是字母、数字组合的时候
			echo '字母数字的组合，强度中等<br>';
			return true;
		} else if($res4) {
			//说明字母、数字、特殊符合组合
			echo '字母数字特殊符合的组合，强度杠杠的<br>';
			return true;
		} else {
			$this->error[] = '<font color="red">密码不符合规则</font>';
			return false;
		}
	}
	/**
	 * 〈验证邮箱是否符合规则〉
	 * 〈邮箱规则：任意字母，数字，下划线.-809611051@qq.com 数字、字母.只有一个.后面的.com〉
	 * @param [参数1]     [参数1说明]
	 * @param [参数2]     [参数2说明]
	 * @return[返回类型说明]
	 */
	public function verifyEmail($email) {
		// 建立规则
		$reg = '/^[\w\.\-]+@[\w]+(\.[\w]+)?\.[a-zA-Z]{2,4}$/';
		
		preg_match($reg, $email,$match);
		if(!$match) {
			$this->error[]= '<font color="red">邮箱地址不符合规则</font>';
			return false;
		} else {
			return true;
		}
	}
	/**
	 * 〈验证手机号码〉
	 * 〈规则:11位〉
	 * @param [参数1]     [参数1说明]
	 * @param [参数2]     [参数2说明]
	 * @return[返回类型说明]
	 */
	public function verifyTel($tel) {
		// 建立规则
		$reg = '/^1[34578]\d{9}/';
		preg_match($reg, $tel,$match);
		if(!$match) {
			$this->error[] = '<font color="red">手机格式有误</font>';
			return false;
		} else {
			return true;
		}
	}
}
 ?>

```
