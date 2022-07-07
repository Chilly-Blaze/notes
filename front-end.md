

# HTML

- `<h>`  标题标签
- `<p>`  段落标签	
- `<img src="" alt="">`  链接 替换文字  
- `<em>`  斜体
- `<strong>`  加粗
- `<span>`  无任何样式
- `<ul>/<ol type="">`  无序/有序列表 样式		`<li>`
- `<div>`  模块标签
- class/id	如`<h class="">`	自定义标签应用
- `<!-------------------->`	注释
- `<br>`  换行
- `&nbsp`  空格

# CSS

- `/********************/`	注释
- `.classname/#idname`		编写样式
- `top/bottom/left/right`	上下右左[tbrl]
- `auto/inherit`			自动/与父级相同
- `display`					设置属于什么元素
- `cursor`					指针样式
- `float`					浮动[:tbrl]
- `color`					颜色
- `overfloat`:hidden		溢出隐藏
- `position`				层模型定位
- `opacity`					透明度 (:1为100%)
- `z-index`					层级关系（数字大的在上面）
- `width/height`			宽/高（块状元素）
- `list` 列表				-style 样式
- `font` 字体				-family 字体[simsun宋体/simhei黑体/Microsoft  yahei微软雅黑]	-weight 粗细		-size 大小
- `text` 文本				-decoration 装饰[下划线等]	-align 对齐
- `line` 文本行			-height 行高
- `letter` 字符			-spacing 间距		-radius 圆角
- `order` 边框			-style 风格[上下 左右 下 左]	-width 粗细		-color 颜色	-tbrl		-radius 圆角	
- `background` 背景		-color 颜色					-repeat 重复		-position 位置
- `margin` 边距			-tbrl
- `padding` 填充[会变大]		-tbrl
- `transform` 移动		:translate(px,px) 平移		:retate(deg) 旋转				:scale(,) 缩放(倍数)	:skew(deg,deg) 斜切
- `transition` 过度		:[哪一个样式] [多少时间] [是否缓入缓出] [延迟多少秒]

# JavaScript

## 简介&代码规则

它是世界上最流行的脚本语言，Java和JavaScript没有太多的关系，只是当时设计JavaScript的公司是Java的粉丝而已（蹭热度），而JavaScript仅仅用了10天就被开发出来了

ECMAScript（ES）可以理解为JavaScript的一个标准，目前最新版本是ES6，但大部分浏览器还停留在ES5上

```html
<head>
    <meta charset="UTF-8">
    <title>Title</title>

    <!--script标签内可以写JavaScript代码
    但是一般来说我们要模块化编程，不能这样东一个西一个标签-->
    <script>
        alert('hello,world');
    </script>

</head>
```

更加通用的方式就是外部引用方式：

![image-20210821223437217](https://s2.loli.net/2021/12/05/ORcPNFlQ51gTUtY.png)

> 注意到src目录可以被删去，原因是IDEA只会去src目录找Java文件编译（虽然也可以自己改，但没必要）

代码就可以改成

```html
<head>
    <meta charset="UTF-8">
    <title>Title</title>

    <!--注意，script标签必须成对出现-->
    <script src="js/Demo.js"></script>
    <!--不用显示类型，默认也是JavaScript，十分方便-->
    <script type="text/javascript"></script>


</head>
```

```javascript
alert('hi');
```

## 基本语法

### 变量

注意JavaScript严格区分大小写

```JavaScript
let i = 1;
alert(i);  // 弹窗输出
console.log(i)  // 在控制台输出
```

#### 定义变量

```JavaScript
let x = 1+y;
let y = 1;

// 等价于
let y;
let x = 1+y;
y = 1;
```

即使在后面定义变量程序依旧不会报错，因此我们需要严格在最头部定义所有变量，方便后来的人阅读

#### 初识window对象

所有的`let`定义的变量，都绑定在`window`对象上，而像`alert`这种没头没脑的方法实际上也是绑定在window对象上（即`window.alert`）

因此为了防止全局变量命名冲突问题，建议在写代码的时候把自己的代码全部放入自己定义的唯一命名空间中

```JavaScript
let a = {}
a.n = 1
a.a = "123"
```

### 浏览器审查元素

上述代码被浏览器编译执行后

![](https://s2.loli.net/2021/12/05/VC2kGPMl5ETv1QX.png "控制台界面")

> 上图中可以看出可以直接在控制台执行js代码

![image-20210821232426120](https://s2.loli.net/2021/12/05/Uly3iCOfKkXn6YM.png)

这种特性实际上就是把浏览器当作了一个IDE来进行代码的调试

### 数据类型

大多数都和Java没什么区别，但还是要注意一些问题

- `===`表示无论是类型还是值都相同

- `NaN`表示不是一个数（not a number）

- 数组定义`var a = [1,'a',null,true]`

- 如果输入`a[4]`则会`undefined`未定义

- `\x41`打印ascii第41号字符

- \`\`是多行字符串（反引号）

  ![image-20210822103106839](https://s2.loli.net/2021/12/05/RsOnyivuNC2a6wP.png)

- 注意字符串不可变，虽然可以`s[0]`取到第一个字符，但是不能`s[0] = 1`

  ![image-20210822141245186](https://s2.loli.net/2021/12/05/qpdLa5v6gPHDcko.png)

  其他大多数方法和Java都没什么区别

- ```JavaScript
  let a = [0,1,2,3,4]
  let s = "01234"
  a.indexOf(1)  // 获取第一个元素的下标索引
  a.slice(1,2)  // 截取数组
  a.push(5,6)  // 往数组最后添加元素
  a.pop()  // 弹出最后一个元素（弹出意味着会返回最后一个元素）
  a.unshift(-2,-1)  // 在数组头部添加元素
  a.shift()  // 弹出第一个元素
  a.sort() // 排序，从小到大
  s.substring(2)  // 截取字符串
  // 还有很多，大多都和Java差不多
  ```

- `for (let n in a)`n是a的索引，和python要区别开来，而`for (let n of a)`才是数组值

### 严格检查模式

由于JavaScript太随意了，像python一样会有检查的机制，防止你乱写代码

比如也可以直接`i = 1`但这是全局变量，太危险了，要让他是局部变量，ES5之前用`var`，ES6用`let`

想要使用严格检查模式，就要在JavaScript代码之前（第一行）写上`‘use strict’`

![image-20210822100328636](https://s2.loli.net/2021/12/05/U9vqyxBHcTl15tW.png "报错了")

这样就可以预防JavaScript随意性导致的产生的一些问题

还有一种方案是我们手动抛出异常，直接`throw ‘[异常信息]'`即可

### 函数

基本形式`function f(x){return x}`这样

还可以`let f = function(x){}` 两者等价

#### 参数

注意当含参的时候也可以进行无参调用，但是返回undefined，同样也可以传入多个参数，可以省略很多重载

因此JavaScript给了一个`arguments`关键字，表示传入的所有参数，是一个数组

同样也可以通过`...[value]`表示接下来可能还有很多参数，并把接下来的参数都存在`value`数组里

### 对象

对象的定义和C的结构体差不多`var f{a:1,b:'2'}`等等，a和b就是这个对象的属性

- `‘a' in f`可以判断某个属性是否在对象内
- `delete`直接删除某个属性

#### 方法

方法实际上就是将一个属性赋值为另一个函数

```JavaScript
let f ={   // f不是一个函数，是一个对象！
    n:"1",
    b:2,
    f: function (){
        return 3;
    }
}
```

注意调用方法的时候必须加括号

#### 关于this

```JavaScript
function f(){
    return this.n;
}
let a ={
    n:"1",
    b:2,
    c:f  // 注意这里f不能加括号，加了就报错！！！
}

console.log(a.c());  // 这里要加！！
console.log(f.apply(a))  // 这两条语句等价
```

注意到如果直接写`f()`就会报错（或者输出NaN），而`apply`这个方法实际上就是把`this`定位为`a`对象

### 常用对象

#### Date日期对象

```JavaScript
let now = new Date();  // 这里记得要new出来
now.getTime()  // 获取时间戳
new Date(now.getTime());  // 通过时间戳还原时间
now.toLocaleTimeString()  // 获取当地时间
```

`Date`对象一般都用在计算或者显示中

#### JSON对象

早期所有的文件传输习惯用XML文件，JSON就是用于对标XML

**JSON**（JavaScript Object Notation）是一种轻量级的数据交换格式，人类很容易阅读和写作，机器很容易解析和生成，同时简洁和清晰的层次结构使得 JSON 成为理想的数据交换语言，他既易于人阅读和编写，同时也易于机器解析和生成，并有效地提升网络传输效率

所以现在所有的网络传输，后端请求接口都是json，而任何的JavaScript支持的类型都可以用JSON来表示

##### 格式

- 所有的对象都用`{}`
- 数组都用`[]`
- 键值对都用`key:value`

```javascript
let a ={
    n:1,
    s:"1",
    b:true
}

let json = JSON.stringify(a);  // 将a转换为json形式表达
let aa = JSON.parse(json);  // 将json表达转换为对象
```

![image-20210823112436419](https://s2.loli.net/2021/12/05/Nau4EfksognHWSG.png)

## 面向对象编程

类是一个模板，对象是一个具体的实例

### 面向原型继承

在JavaScript中将这种模式用到了极致，旧版当中提出了**原型(proto)**的概念

```javascript
let fa = {
    n : 1,
    s : "1",
}

let so = {
    n : 2
}

so.__proto__ = fa  // 指定so的原型为fa
console.log(so.s)  // 可以使用原型的属性
```

### 面向class继承

class关键字是在ES6引入的，实际操作和Java完全一样

```JavaScript
class Fa{
    constructor(name) {
        this.n = name  // 构造器
    }
}
let so1 = new Fa(1)
let so2 = new Fa(2)
class So extends Fa {  // 等价于so.__proto__ = fa，后台代码完全一样
    constructor(name) {
        super(name);
    }
}
```

> 实际上好像就是重新搞了一套东西出来，比如下面代码中的Fa实际上好像并不是严格意义上的类（在控制台中无法直接输出类信息
>
> ![image-20210823185507578](https://s2.loli.net/2021/12/05/IBDNaixoORGzl1v.png)

### 原型链

![img](https://s2.loli.net/2021/12/05/s7mYoUBV6KjOEd5.png)

所有对象都有一个原型，而所有原型最终都归结于`Object`，然而`Object`的原型存在的函数（方法）依旧指向`Object`原型，但是注意到`Object`没有原型

![image-20210823132954098](https://s2.loli.net/2021/12/05/ZyuMq6epOAHiTgY.png)

## 操作BOM对象

BOM即操作浏览器对象模型

### 浏览器介绍

JavaScript的出现就是为了让浏览器能够运行一段脚本，所以操作浏览器是JavaScript一个非常重要的特性

常见的浏览器有很多，但是内核的种类并不多，比如360浏览器其实是可以自由更换内核

常见的内核包括：

- IE (Microsoft)
- Chrome (Android)
- Safari (iOS)
- FireFox (linux)
- Opera

### window对象

window对象实际上就代表着浏览器的窗口，可以通过它获取到很多浏览器甚至显示屏等硬件的属性（高度，宽度等）

所有能够直接打出来的方法，属性都是属于window对象

#### .Navigator对象

内部有封装了浏览器相关的各种信息（Navigator是第一代浏览器）

```JavaScript
navigator.appVersion  // 获取浏览器版本
navigator.userAgent  // 浏览用户相关信息
navigator.platform  // 浏览器运行平台（64位）
```

但是大多数时候我们不会使用`navigator`对象，因为会被人为修改，所以不建议使用这些属性来判断和编写代码

#### .screen对象

封装有整个屏幕的某些属性（分辨率，色深等）

#### .location对象

location代表着当前页面的URL信息，可以用它来实现一些重定向

![image-20210823205950795](https://s2.loli.net/2021/12/05/Gx8wouSb3KJv6qF.png "百度的location信息")

如图后面带有一个*f*的都是方法，许多的方法用处都很大

- `reload`重新加载网页，相当于刷新
- `assign`重定向，可以跳转到指定网页（如：`location.assign(www.baidu.com)`）

#### .document对象

代表当前页面的文档信息

可以通过document获取网站上的文档树节点（爬虫），也可以获取网页的`cookie`

#### .history对象

可以进行后退/前进操作，相当于浏览器上边点一下，代表浏览器的历史记录

但是不建议使用，已经被阿贾克斯替代了

## DOM

DOM就是文档对象模型（和BOM分开）

### 获得DOM

浏览器网页就是一个DOM树形结构，我们可以对其每一个节点（div等）进行增删改查，重点就是利用`document`对象

```JavaScript
document.getElementsByTagName('a')  // 获得指定标签名下的内容
document.getElementById('a')  // 获得指定id标签下的内容
document.getElementsByClassName('a')  // 获得指定类名下的内容
// ...
```

但是这只是原生代码，之后尽量还是要用jQuery

### 操作DOM

```html
<div id="aa">
    <p id="bb">"hh"</p>
</div>
```

```JavaScript
    let id = document.getElementById("bb")
    // 修改HTML
    id.innerText = "123"  // 修改文本的值
    id.innerHTML = "<strong>123</strong>"  // 可以解析HTML文本标签
    // 修改CSS
    id.style.color = "red"
    id.style.fontSize = "20px"
    id.style.padding = "2em"
    // 移除标签（找父亲干掉儿子）
    let fa = id.parentElement
    fa.removeChild(id)  // 顺着id找到父亲然后把自己干掉
    fa.removeChild(fa.children[0])  // 注意删除具有动态性，删完第一个原来的第二个就变成第一个了
    // 新增一个标签（追加操作）
    let p = document.createElement('p')  // 创建一个p标签
    p.id = "cc"
    p.innerText = "1234"
    fa.appendChild(p)  // 将p标签追加到fa标签末尾
```

> 注意Node就是一个标签对象

## 操作表单

操作表单涉及到验证的问题，可以避免在服务器端进行验证

表单有很多，包括

- 文本框(text)
- 下拉框(\<select\>)
- 单选框(radio)
- 隐藏域(hidden)
- 密码框(password)

表单的目的就是提交信息给服务端

```html
<head>
    <meta charset="UTF-8">
    <title>Title</title>

    <!--必需的 action 属性规定当提交表单时，向何处发送表单数据
        form内的onsubmit和onclick差不多，规定了发送表单时执行的JavaScript操作
        （注意函数aa必须前面加上return才不会忽略返回值，不然只写aa()会默认返回值true）
        -->
    <form action="https://www.baidu.com/" onsubmit="return aa()">
        <p>
            <span>用户名</span> <label for="username"> </label><input type="text" id="username">
        </p>

        <p>
            <span>性别</span>
            <input type="radio" name="a" id="sex"><label for="sex"> 男</label>
            <label>
                <input type="radio" name="a"> 女
            </label>
            <!--必须要有name属性才可以在请求中看到信息-->
            <input type="hidden" id="hide-username" name="username">
        </p>

        <p>
            <input type="submit">
            <button type="button" onclick="aa()">onclick:当按钮被点击时执行Javascript代码</button>
        </p>
    </form>

    <script>
        function aa(){
            // 在这里可以获取表单的值
            let id = document.getElementById("username");  // 非常容易获得表单信息
            let sex = document.getElementById("sex");  // 获得选中情况
            console.log(id.value)
            console.log(sex.checked)  // 打印输入情况
            // 然后我们可以对表单信息进行加密，使得别人对他进行抓包的时候不会注意到账户信息
            // 先获取隐藏框信息
            let hidden = document.getElementById("hide-username")
            // 加密后存入隐藏框
            hidden.value = id.value  // 这里可以对value值应用加密算法
            // 如果比如说直接id.value = md5(id.value)就会在提交的一瞬间密码变长，一下子就看出来了，十分不好（就是暗示教务系统！）
            // 可以校验表单内容，true就是通过提交，false就是阻止提交
            return true;
        }
    </script>

</head>
```

> 注意到`<label>`标签通常和`<input>`标签一起使用，`<label>`标签为`input`元素定义标注（标记）。
>
> `<label>`标签的作用是为鼠标用户改进了可用性，当用户点击`<label>`标签中的文本时，浏览器就会自动将焦点转到和该标签相关联的控件上
>
> 简单来说，点到文字选框也会勾选，增加交互

## jQuery

jQuery就是一个封装了大量JavaScript的方法（函数）的库

### 获取jQuery

搜索`cdn jQuery`即可获得线上地址，粘贴过来就行了

```html
<script src="http://code.jquery.com/jquery-migrate-1.2.1.min.js"></script>
```

![image-20210825165914199](https://s2.loli.net/2021/12/05/B3i4N6qdRQuEe8n.png)

### 怎么用？

就一个公式，用`$([selector]).[action]()`括号内是**选择器**，就是css选择器，.后面是**事件**

```html
<head>
    <meta charset="UTF-8">
    <title>Title</title>

    <button id="a">click me</button>

    <script src="https://libs.baidu.com/jquery/2.0.0/jquery.min.js"></script>
    <script>
        // // 原来底层代码：
        // // 上面先改为<button id="a" onclick="aa()">click me</button>
        //    然后：
        //              let a = document.getElementById("a")
        //              function aa(){
        //              	alert("a")
        // 				}
        $('#a').click(function (){
            alert("a")
        })
        // $('#a')定位到id为a的标签，当这个标签被action(点击)的时候执行function操作
    </script>

</head>
```

回顾选择器（善用[jQuery帮助文档](https://jquery.cuishifeng.cn/)）

- `#[id]`id选择器
- `.[class]`类选择器
- 等等

通过选择器+事件的模式来操作各种`html`标签

### 事件

![image-20210825174239439](https://s2.loli.net/2021/12/05/ir8uP9qGLY7JXEx.png)

实现了一个在方框内移动鼠标并显示鼠标坐标的程序

```html
<head>
    <meta charset="UTF-8">
    <title>Title</title>

    <script src="https://libs.baidu.com/jquery/2.0.0/jquery.min.js"></script>

    <style>
        #divMove{
            width: 500px;
            height: 500px;
            border: 1px solid red;
        }
    </style>

    mouse:<span id="mouseMove"></span>
    <div id="divMove">
        move your mouse
    </div>

    <script>
        $(function (){
            $('#divMove').mousemove(function (e){  // e就代表着鼠标对象
                $('#mouseMove').text(e.pageX+','+e.pageY)
            })
        })
        // 这个就是$(document).ready(function()) 的简化版（这也太简略了），用它来表示网页加载完了要响应的事件
    </script>

</head>
```

而改css样式或添加标签之类的也非常方便

```html
<body>
    <ul id="a">
        <li>1</li>
    </ul>

    <script>
        $('#a').append('<li>2</li>');  // 内部追加li，after是在该元素之后加（和ul地位相等）
        $('ul li:first-child').text('3');  // 自定义li内容
        $('ul li:last').addClass(function() {
            return 'item-' + $(this).index();
        });  // 可用循环遍历自动生成每一个li
        $('.item-1').css({"color": "red"})  // 暴力设置CSS样式
    </script>
</body>
```

其他：

- `$().toggle`隐藏/显示状态切换
- `$(window).`操作浏览器窗口
- 等等