###  es6的继承
/*
       使用ES6的class不能使用Drag.prototype = {}
        Drag.prototype = {
            constructor:Drag,
            move,
            up,
            down
        }
    */
****
```javascript
  class Drag {
        constructor(id){ //创建一个构造函数
            this.box = document.getElementById(id);
            this.disX = 0;
            this.disY = 0;
        }

        init(){ //这个和普通的一样
            this.box.addEventListener('mousedown',(ev)=>{
                this.down(ev);
            });
        }

        down(ev){
            this.disX = ev.clientX - this.box.offsetLeft;
            this.disY = ev.clientY - this.box.offsetTop;
            var move = ev => this.move(ev);
            var up = ev => this.up(ev,move,up);
            
            document.addEventListener('mousemove',move);
            document.addEventListener('mouseup',up);
            ev.preventDefault();
            
        }
        move(ev){
            this.box.style.left = ev.clientX - this.disX + 'px';
            this.box.style.top = ev.clientY - this.disY + 'px';
        }
        up(ev,move,up){
            document.removeEventListener('mousemove',move);
            document.removeEventListener('mouseup',up);
        }
    }

   
    class Drag2 extends Drag { //让Drag继承Drag
       constructor(id,txt){
           
            //继承写了constructor必须写super，不然会报错
            //在super()上面就不能设置属性(不能使用this)，不然会报错
            // this.txt = txt;   报错
            super(id);
            this.txt = txt;
            
       }
       say(){
           alert(this.txt);
       }
       move(ev){
            var l = ev.clientX - this.disX;
            if(l<0)l=0;
            this.box.style.left = l  + 'px';
            this.box.style.top = ev.clientY - this.disY + 'px';
        }

    }

    var d = new Drag('box');
    var d2 = new Drag2('box2','呵呵');
    d.init();
    d2.init();
    d2.say();
    d.say();
```