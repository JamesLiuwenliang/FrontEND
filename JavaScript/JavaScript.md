## JavaScript

`JavaScript`是世界上最流行的脚本语言

### 1. 基本语法

```javascript
// 弹窗
alert('hello World'); 
```

#### 1.1浏览器必备调试

- Elements：跑网站，复刻网站
- Console：调试JS
- Source：打断点
- Network：抓包
- Application：查看网站的Cookie

![1593330701258](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1593330701258.png)

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>


<!--    外部引入-->
    <script src = "JavaScript/qj.js"></script>

<!--    不用显示定义的type，也默认是JavaScript-->
    <script type ="text/javascript"></script>

    <script>
        // 定义变量 变量类型 变量名 = 变量值
        var num = 1;
        var zzz = "hello World";
        var score = 100
        // 条件控制
        if(2>1){
            alert('true');
        }else if(score = 1>60){
            alert('false');
        }

        // JavaScript严格区分大小写
        // console.log(score) 在浏览器的控制台打印变量
    </script>
</head>
<body>

</body>
</html>
```

#### 1.2 严格检查模式

````html
    <!--前提:IDEA需要支持ES6语法
        'use strict'; 严格检查模式，预防JavaScript的随意性导致产生的一些问题，必须写在第一行
        局部变量建议使用let去定义
    -->
    <script>
        'use strict';
        let i =1;
    </script>
````

#### 1.3 特殊点

```javascript
// 比较运算符
==  等于（类型不一样，值一样，也会判断为true），坚持不要使用
=== 绝对等于（类型一样，值一样，结果为true）
```

```javascript
null: 空
undefined :未定义
```

```javascript
var arr =  [1,2,3,4,6,10,'hello',null ,true] //不同于java必须相同类型

```

**对象**

```javascript
// 对象是大括号，数组是中括号
// 每个属性之间需要,隔开，最后不需要加;
        var  Person = {
            name : "liu",
            age: 3,
            tags : [1,2,3.4,5]
        }
delete Person.name ;// 是可以删除元素的   
Person.qq //是不会报错的，显示 undefined
Person.qq = "123456" // 是可以添加元素的

    
```

字符串拼接

```javascript
    <script>
        'use strict'
        let name = "lwl";
        let age = 18;
        let msg = `Hello,${name}`;
    </script>
```

数组：如果给数组大小赋值，数组大小会发生变化，后续没有内容的用`undefined`代替

使用`indexof()`方法，会发现字符串"1"和数字1是不同的

**`slice()`**：截取Array的一部分，返回一个新的数组，类似String中的`subString()`

`shift()`和`unshift()`：压入到头部和弹出头部的一个元素

#### 1.4 流程控制

`for-each()`:

```javascript
var age = [1,2,3,4,5,10];

age.forEach(function(value){
    console.age(value);
})
```

`for...in`

```javascript
for(var num in age){
    if(age.hasOwnProperty(num)){
        console.log("存在");
        console.log(age[num]);
    }
}
```

####  1.5 `Map`和`Set`

```javascript
        'use strict';
        var map = new Map([['tom',100],['jack',90],['haha',80]]);
        var name = map.get('tom');
        map.set(['ja',90]);
```

`Set`：无序不重复的集合，两者为ES6的新特性。

#### 1.6 `iterator`

可以用来遍历迭代`Map`和`Set`

### 2. 函数及面向对象

#### 2.1 定义函数

```javascript
function abs(x){
    if(typeof x !== 'number'){
        throw 'Not a number';
    }
    if(x>=0){
        return x;
    }else{
        return -x;
    }
}
```

一旦执行到return代表函数结束，返回结果

如果没有执行return，函数执行完后也会返回结果，结果就是`undefined`

- **`arguments`**是一个Js免费赠送的关键字，代表传递进来的所有参数是一个数组

- **`rest`**：ES6引入的新特性，获取除了已经定义的参数之外的所有参数，这个函数只能写在最后满，并用`...`标识。

```javascript
function aaa(a,b,...rest) {
    console.log(a);
    console.log(b);

    console.log("------------");
    console.log(rest);

}
>> aaa(1,2,4,5,5,6,6,)
>> rest会被当做数组，前面必须加 ...
```

#### 2.2 变量的作用域

假设在函数体内部声明，则在函数体外不可以使用，非想要用，可以研究**闭包**。

假设在JavaScript中函数直接查找从自身函数开始，由内向外查找。

```javascript
function aaa(a,b,...rest) {
    var y;
    var x = "x"+y;
    console.log(x);
    y = 'y';

}

> x undifined; // y在var 之后是 undefined状态
```

所有变量尽量放在定义的函数的头部，便于代码维护

**全局对象**：默认所有的全局变量，都会自动绑定在`windows`对象下

##### 规范：

由于所有的全局变量都会绑定到`window`上，如果不同的js文件，使用了相同的全局变量，会产生冲突。

```javascript
// 唯一全局变量
var App ={};

//定义全局变量
App.name = "Outsider";
App.add =  function(a,b){
    return a+b;
}
```

把自己的代码全部放入自己定义的唯一空间名字中

##### 局部作用域 `let`：

尽量用，尽量不要用`var`

##### 常量`const`：

常量关键字，定义之后不能被改变，官方叫做只读变量。

#### 2.3 方法

```javascript
    <script>
        'use strict';
        let lwl = {
            name :"lwl",
            birth : 2000,
            age : function(){
                var now = new Date().getFullYear();
                return now - this.birth;
            }
        }
        console.log(lwl.name);
        console.log(lwl.age());
    </script>
```

`apply()`：在JavaScript中可以控制this指向

```javascript
    <script>
        'use strict';

        function getAge(){
            var now = new Date().getFullYear();
            return now - this.birth;
        }

        var lwl = {
            name :"lwl",
            birth : 2000,
            age1 : getAge
        }

        getAge.apply(lwl,[]);  //this指向了 lwl ，参数为空
        
    </script>

控制台： lwl.age1()
```

### 3. 内部对象

#### 3.1 `JSON`

`JSON`是一种轻量级的数据交换格式，在`JavaScipt`中一切皆为对象，任何js支持的类型都可以用`JSON`来表示。

格式：

- 对象都用{}
- 数组都用[]
- 所有的键值对都是用`key:value`

```javascript
var lwl = {
    name :"lwl",
    age : 3,
    sex : 'man'
}

// 对象转换为JSON字符串，{"name":"lwl","age":3,"sex":"man"}
var jsonUser = JSON.stringify(lwl);

// json字符串转换为JS对象
var obj = JSON.parse('{"name":"lwl","age":3,"sex":"man"}');
```

**尽量用双引号`""`**

`JSON`和`JS`的区别：

```javascript
var js_obj = {a:'hello' , b:'hellob'}; // JS的对象
var json = '{"a":"hello" , "b":"hellob"}'
```

#### 3.2 `Ajax`

- 原生的`js`写法，`xhr`异步请求
- `jQuey`封装好的方法 `$("#name").ajax("")`
- `axios`请求

### 4. 面向对象编程

#### 4.1 class继承

class关键字是在`ES6`引用的。

```javascript
// ES6之后
class Student{
    constructor(name) {
        this.name = name;
    }

    hello(){
        alert("Hello");
    }
}

var xiaoming = new Student("xiaoming");


```

Java称作继承，而JavaScript是原型链实现

### 5. 操作BOM对象（重点）

window：代表浏览器的窗口，`window.innerHeight`，

`Navigator`封装了浏览器的信息，但大多数时候不会使用，因为会被人为修改。

`screen`：代表屏幕

`location`：代表当前页面的URL信息

```javascript
location.assign('新的URL') // 设置新的地址
reload: f reload() // 刷新网页
```

`document`：代表当前的页面，HTML DOM文档树

```javascript
document.title = 'Outsider'
```

获取具体的文档树节点

获取cookie：`document.cookie`;

`history`：代表浏览器的历史记录，`history back()`后退 ； `history forward()`前进

### 6. 操作DOM对象（重点）

浏览器网页就是一个Dom树形结构

要操作一个Dom节点，就必须要先获得节点。

**获得节点**

```javascript
<div id = "father">
    <h1>标题一</h1>
    <p id ="p1">p1</p>
    <p class="p2">p2</p>
</div>


<script>
    // 对应的CSS选择器
    var h1 = document.getElementsByTagName('h1');
    var p1 = document.getElementById('p1');
    var p2 = document.getElementsByClassName('p3');
    var  father = document.getElementById('father');

</script>

father.firstchild
father.lastchild
```

这是原生代码，以后会使用`jQuery`

**更新节点**

```javascript
p1.innerText ="p2"
> "p2"
p1.innerHtml =...
pi.style.color = 'yellow'

```

**删除节点**

删除节点的步骤：先获取父节点，再通过父节点删除自己

```javascript
// 删除是一个动态的过程
father.removeChild(father.children[0]);

// 此时标题删除，且p1和p2向上移动
```

删除多个节点时，children是在时刻变化的，删除节点时一定要注意。

**插入节点**

我们获得某个Dom节点，假设这个Dom节点是空的，我们通过`innerHTML`就可以增加一个元素了，但是这个Dom节点

```javascript
<p id = "js">JavaScript</p>
<div id = "list">

    <p id = "p1">P1</p>
    <p id = "p2">P2</p>
    <p id = "p3">P3</p>

</div>

<script>
    var js = document.getElementById("js");
    var list = document.getElementById("list");
</script>

list.appendChild(js); // 追加到后面
结果：
    <p id = "p1">P1</p>
    <p id = "p2">P2</p>
    <p id = "p3">P3</p>
    <p id= "js">JavaScript</p>


// 创建一个标签节点（通过这个属性，可以设置任意的值）
var myScript = document.createElement('myScript');
myScript.setAttribute('type','text/javascript');

// 要包含的节点.insertBefore(newNode,targetNode);
list.insertBefore(js,ee);

```

### 7. 操作表单（验证）

- 文本框 text
- 下拉框 <select>
- 单选框 radio
- 多选框 checkbox
- 隐藏域 hidden
- 密码框 password

- .....

```javascript
<!--    多选框的值，就是定义好的value-->
    <p>
        <span>sex:</span>
        <input type="radio" name = "sex" value="man" id="boy"> man
        <input type="radio" name = "sex" value="woman" id="girl"> woman

    </p>
</form>



<script>
    var input_text = document.getElementById('username');
    var boy_radio = document.getElementById('boy');
    var girl_radio = document.getElementById('girl');

    // 对于单选框，多选框等等固定的值，girl_radio.value只能获得当前的value
    // 应该用 girl_radio.checked 查看返回结果是true还是false

</script>
```

尽量在本地检查，可以降低服务器的负载

#### 7.1 表单提交

```javascript
// 可以首先添加MD5工具类
<!--MD5工具类-->
<script src="https://cdn.bootcss.com/blueimp-md5/2.10.0/js/md5.min.js"></script>
```

然后提交表单

```javascript
<form action="post">
    <p>
        <span>用户名：</span> <input type="text" id="username">
    </p>

<!--    多选框的值，就是定义好的value-->
    <p>
        <span>密码：</span> <input type="password" id="password">
    </p>
    <p>
        <span>sex:</span>
        <input type="radio" name = "sex" value="man" id="boy"> man
        <input type="radio" name = "sex" value="woman" id="girl"> woman
    </p>

    <!--绑定事件 onclick 被点击
        onclick = "aaa()"：被点击后执行相关函数
    -->
    <button type="submit" onclick="aaa()">submit</button>

</form>

<script>
    var input_text = document.getElementById('username');
    var boy_radio = document.getElementById('boy');
    var girl_radio = document.getElementById('girl');

    // 对于单选框，多选框等等固定的值，girl_radio.value只能获得当前的value
    // 应该用 girl_radio.checked 查看返回结果是true还是false

    function aaa() {
        var username = document.getElementById('username');
        var pwd = document.getElementById('password');
        console.log(username.value);

        // MD5算法
        pwd.value = md5(pwd.value);
        console.log(pwd.value);
    }
</script>
```

抓包的Form Data中密码会被加密

**表单绑定提交事件**，提交表单最佳优化方案

```javascript
<form action="https://www.baidu.com/" method ="post" onsubmit="return aaa()">
    <p>
        <span>用户名：</span> <input type="text" id="username">
    </p>
    <p>
        <span>密码：</span> <input type="password" id="input_password">
    </p>

    <input type="hidden" id="md5_password" name = "password">

    <button type="submit" >submit</button>

</form>



<script>

    function aaa() {
        var username = document.getElementById('username');
        var pwd = document.getElementById('input_password');
        var md5pwd = document.getElementById('md5_password');

        md5pwd.value = md5(pwd.value);
        return true;
    }
</script>
```

### 8. `jQuery`

#### 8.1 选择器

是一个库，存在JavaScript大量的方法。

```javascript
<!--
公式 ： $(selector)action()
-->

<a href="" id ="test-jquery">click me</a>

<script>
    $('#test-jquery').click(function () {
        alert('Hello ');
    })

</script>
```

#### 8.2 事件

鼠标事件、键盘事件、其他事件

```javascript
   // 需要注意要调用合适的库，不然容易出问题 
<script src="https://cdn.bootcdn.net/ajax/libs/jquery/3.4.1/jquery.slim.min.js"></script>

    <style>
        #divMove{
            width:500px;
            height: 500px;
            border:1px solid red;
        }
    </style>
```

```javascript
  <!--要求：获取鼠标当前的一个坐标-->
    mouse: <span id="mouseMove"></span>

    <div id = "divMove">
        在这里移动鼠标
    </div>

    <script>
        // 当网页元素加载完毕之后，响应事件
        $(function () {
            $('#divMove').mousemove(function (e) {
                // 显示当前坐标位置
                $('#mouseMove').text('x:'+e.pageX + ' y:'+e.pageY)
            })
        });
    </script>
```

操作DOM

```javascript
    <ul id = "test_ul">
        <li class = "js">JavaScript</li>
        <li name ="python">Python</li>
    </ul>

    <script>
        // 当网页元素加载完毕之后，响应事件
        $(`#test_ul li[name=python]`).text(); // 获得值
        $(`#test_ul`).html();  // 获得值

    </script>

$(`#test_ul li[name=python]`).text("123456"); //设置值
> E.fn.init [li, prevObject: E.fn.init(1)]
```

测试

```javas
$(window).width();

```



> 学习前端技巧

- 看`jQuery`源码，看游戏源码
- 扒网站，修改看效果





