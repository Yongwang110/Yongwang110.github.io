```javascript
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
	</head>
	<body>
		<input type="text" id="txt" />
		<ul id="ul"></ul>
		<script>
			//http://suggest.video.iqiyi.com/?key=${txt.value}&platform=11&rltnum=10&uid=b00b02370b6f4b46953fbc947084d9ea&ppuid=&callback=window.Q.__callbacks__.cbjo6vvk
			function fn(obj){
				console.log(obj)
				ul.innerHTML ='';
				obj.data.forEach((e,i)=>{
					var li = document.createElement('li');
					li.innerHTML = e.name;
					ul.appendChild(li);
				});
			}
			txt.onkeyup = function(){
				var os = document.createElement('script');
			os.src =`http://suggest.video.iqiyi.com/?key=${txt.value}&platform=11&rltnum=10&uid=b00b02370b6f4b46953fbc947084d9ea&ppuid=&callback=fn`;
document.getElementsByTagName('head')[0].appendChild(os);
				os.remove();
			}
			</script>
	</body>
</html>
```