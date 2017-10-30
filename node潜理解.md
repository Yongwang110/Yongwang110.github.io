###  增
```javascript
const fs = require('fs') //创建一个本地文件的模块
fs.writeFile('1.txt','hh',function(err){ //往本地文件写入一个叫做“1.txt’的文件它的内容是‘hh’，搞完以后判断
	if(err){ //如果是err的话就是错的
		console.log('错的')
	}else{ //否则就是对的   创建搞定
		console.log('ok')
	}
})
```
### 查
```javascript
const http= require('http');//创建一个http的服务器
const fs = require('fs');//专门用来操作本地文件
			//（1）接收到前端的具体信息      （2）后台服务器做出的回应
http.createServer((req,res)=>{ //创建具体内容
	let urlName = req.url; //urlName是前端发送的信息（地址信息）
	console.log(urlName)
	let na ='www'; //文件名
	if(req.url !== '/favicon.ico'){
		//readFile 就是读取文件内容
		fs.readFile(na+urlName,function(err,data){
			if(err){
				res.write('404');
			}else{
				res.write(data.toString());
			}
			res.end(); //结束标语
		});
	}
}).listen(9090); //定义一个监听器（开通一个通道来监听这个端口）

```
### 接口
```javascript
const http = require('http');
const fs = require('fs');
/*
    localhost:88?user=xxx
    localhost:88/index.html
    1.静态文件的管理
    2.接口返回
*/
http.createServer((req,res)=>{
   let urlName = req.url; //   localhost:88?index.html
   let files = 'www';
   let obj = {
       code:0
   }
   let sql = [{"name":"leo","password":123},{"name":"马智","password":123},{"name":"徐婷","password":123}]
   let onOff = false;
   if(urlName !== '/favicon.ico'){
        console.log(urlName)
        if(urlName.indexOf('?')!=-1){ //有问号，走接口
            urlName = urlName.split('?')[1];
            let arr = urlName.split('&');
            for(var i=0;i<arr.length;i++){
                 //["name=xxx","pass=xx"]
                let a = arr[i].split('=');
                for(var j=0;j<sql.length;j++){
                    // console.log(decodeURI(a[1]))
                    if(sql[j].name == decodeURI(a[1])){
                        obj.code = 1;
                        obj.msg = '用户名已经注册';
                        onOff = true;
                        break;
                    }
                }
            }
            if(!onOff){ //可以注册
                obj.msg = '可以注册';
            }
            res.write(JSON.stringify(obj));
            res.end();
        }else{
            //没问号走静态文件

            fs.readFile(files+urlName,(error,data)=> {
                if(error){
                    res.write('404');
                }else{
                    res.write(data.toString());
                }
                res.end();
            });
        }
   }
   
}).listen(88);
```