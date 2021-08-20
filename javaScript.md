## javaScript

### 1.流程控制

**if判断**

```javascript
var age = 3;
if(age > 3){
  alert("hahaha");
}else{
  alert("123");
}
```

循环

```javascript
while(age<100){
  age = age+1;
  console.log(age);
}

for(var i = 0;i<100;i++){
	console.log(i);
}

for(var num in age){  //in是索引  of是值
  console.log(age[num]);
  
}

age.forEach（function(data){
  
});
```

### 2.Map和Set

```javascript
var map = new Map([["liuyi",100],["tom",444]]);
map.get()

var set = new Set([3,1,1,1,1,1]);//3,1  会去重
```



### 3.iterator

迭代器





### 4.函数

- 定义函数

```javascript
function abs(x){
  if(x>=0){
    return x;
  }else{
    return -x;
  }
}

第二种
var abs = function(x){
  if(x>=0){
    return x;
  }else{
    return -x;
  }
  
  if(typeof x !== 'number'){
    throw 'not a number';//手动抛出异常
  }
}
```



- arguments

  `arguments`是一个js免费赠送的关键词  代表传递进来的所有参数是一个数组



### 5.变量的作用域

- 所有的全局变量 都绑定再window下

  - 例如 var x ;

    x = window.x;

  - alert() 也是window中的一个方法

  **ES6 引入了const 关键字 定义只读变量**



### 6.Date





### 7.Ajacx

- 原生的jss写法  xhr异步请求
- Jquery  封装好的方法
- axios请求





### 8.面向对象

```javascript
    var user = {
        name : "liuyi",
        age : 24,
        run : function () {
            console.log(this.name + "在跑步");
        }
    };

    var xiaoming = {
        name : "xiaoming"
    };
    xiaoming.__proto__ = user;  //.__proto__ 继承
```

ES6 之后可以和java一样创建对象

var liuyi  = new Student();



### 9.操作BOM(浏览器 对象 模型)

> 浏览器介绍

javaScript 和 浏览器关系

javaScript 诞生就是为了让他能够在浏览器中运行

BOM: 浏览器对象模型

- IE 6~11
- Chrome
- Safari
- fireFox

>window 代表 浏览器窗口



> screen 代表屏幕

>location 

location代表当前页面的URL信息

```javascript
host:"www.baidu.com"
href:"https....."
protocal:"https:"
reload:f reload()//刷新页面
//设置新的地址
location.assign("https://blog....")


```



> document

document代表当前的页面，HTML DOM文档树



- 获取具体的文档树节点

  - document.getElementById('app')；

- 获取cookie

  - ducument.cookie 获取cookie

  js可以劫持你的cookie

- 服务器端可以设置cookie: httpOnly  设置为只读保证安全



> history 代表浏览器的历史记录

history.back(); 页面后退

history.forward(); 页面前进



### 10.操作DOM对象

DOM:文档对象模型

> 核心

浏览器网页就是一个Dom属性结构

- 更新：更新DOM节点
- 遍历dom节点:得到DOM节点
- 删除: 删除一个DOM节点
- 添加： 添加一个新的节点

要操作一个节点，就必须要先获得这个DOM节点



获得Dom节点

```javascript
document.getElementsByTagName('h1');
document.getElementByid("id1");
document.getElementByClassName("class1");

//获取子节点
var father = ducumen.getElementByid("father");
var children = father.chilren;
father.firstChild;
father.lastChild;
```



> 更新节点

- xx.innerText = '456' 修改文本的值
- xx.innerHtml   可以解析html样式
- xx.style.



> 删除节点

删除节点的步骤 ： 现货区父节点 再删除自己

```html
father = son.parentElement;
father.removeChild(son);
```

