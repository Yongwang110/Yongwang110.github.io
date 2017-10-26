```javascript
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
	</head>
	<style>
		#txt{
			border-style:1px;
			outline: none;
		}
	</style>
	<body>
		<input type="text" name="" id="txt" value="" />
		<script>
			txt.oninput = function(){ 
				var	xhr = new XMLHttpRequest;  //首先造一个手机
		xhr.open("get","php/get.php?user="+txt.value,true)  //然后要输入号码
		xhr.send(); //再拨号中···
		xhr.onload = function(){  //最后确定拨号是否成功
			console.log(xhr.responseText);
          	if(/\(\D{9}\)$/.test(xhr.responseText)){
          		txt.style.borderColor = 'red';
          	}else{
          		txt.style.borderColor = 'green';
          	}
			
		}
			}
		
		</script>
	</body>
</html>
```