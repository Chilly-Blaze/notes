# Linux

## 代码

-  `ctrl+c` 退出当前命令
-  `ctrl+l` 清屏
-  `ls` 显示此目录的文件
- `-al` 所有信息
  
  - \- 二进制文件 
     - d 目录 
     - l  软链接
     - rwx 读\改\执行
     - 三组rwx分别是所属用户、所属组、其他用户权限
-  `mkdir` 创建一个目录

   - `-p aa/bb/cc` 创建子目录里子目录
-  `cd` 与cmd相同
-  `pwd` 显示从home开始的完整目录
-  `rmdir` 删除空目录
-  `cp` 复制 

   - `-i` 覆盖时提示
   - `-r` 文件夹
-  `mv` 移动或改名
-  `rm -r [地址]` 删除该地址
-  `man [指令]` 帮助   --help也可
-  `touch [文件1] [文件2] [文件3]` 就可以在当前目录下创建多个文件
-  `cat [文件名]` 查看文件   (tac 倒着滚) 

   - `-n` 查看行号 

   - `-b` 空行不标号

   - `/etc/group` 确认组信息

     - 最后一个冒号后表示组成员（附加组）

   - `/etc/passwd | grep` 确认用户信息

     - 冒号分组信息
     - :x表示有密码且加密
     - 三组数字分别是用户代号，组代号和全名（空就是没有设置默认用户名）
-  `more` 分页显示  空格是翻页      回车是下一行
-  `grep [字段] [文件]`  可以显示文件中所有包含指定字段的行

   - `-n`显示行号  
   - `-v` 表示取反（不包含指定字段的行）
   - `-i` 忽略大小写  
   - `^[字段]` 只出现在行首   
   - `[字段]$` 只出现在行尾
-  `less` 上下翻
-  `head` [文件名] 显示前几行      (`tail` 相反)

   - `-n` [数字] 
-  `ln -s [源文件] [软链接名]` 创建一个软链接 (不加-s就是硬链接)
-  `vim` 进入某个文件 (nano也可以)
-  `:wq` 保存并退出
   -  `:q!` 强制退出
-  `tree` 树状结构显示

   - `-d` 只显示文件夹
-  `echo [参数]` 把参数显示在终端中
-  `> [文件]`      把原本输出在终端中的参数输出在文件中       
-  `>>[文件]` 追加到末尾  (不一定要和echo连用，所有终端上显示的东西都可以)
-  `[命令1] | [命令2]` 管道，将第一个命令的输出作为第二个命令的输入     （常用more和grep）
-  `shutdown` 一分钟后关机

   - `-c` 取消 
   - `-r` 重新启动 
   - `now` 现在 
   - `xx:xx` 指定时间关机  
   - `+[数字]` 几分钟后关闭
-  `ssh [用户名@地址(ip/域名)]`
-  `scp [本机文件] [用户名]:[文件位置]` （将本机拷贝到服务器）
-  `./xx.xx` 在当前目录下执行xx.xx文件
-  `groupadd/groupdel [组名]` 添加/删除组
-  `chown [用户名][文件名/目录名]` 修改文件/目录所有者
-  `chmod`

   - `+/- [文件名]` 增加/减少权限

   - `-R` 目录下所有文件的权限
   - `755` 将rwx数字编号
-  `chgrp -R [组名] [文件/目录名]` 递归修改文件/目录的所属组
-  `useradd [组] [新建用户名]` 添加新用户

   - `-m` 自动为用户添加家目录
   - `-g` 不加的话建立一个和用户同名的组
-  `passwd [用户名]` 为用户添加密码
-  `userdel [用户名]`

   - `-r` 自动删除家目录
-  `id [用户]` 显示用户信息（uid、gid（显示的代号是主组））
-  `who` 查看当前所有登录的用户列表
-  `usermod`
   -  `-G [组] [用户名]` 修改用户的附加组
   -  `-g ~` 修改主组
   -  `-s /bin/bash` 修改用户登录的shell（bash）
-  `which [指令]` 该指令所在的文件位置

   - `/bin` 表示普通的可执行文件
   - `/sbin` 和系统相关的管理员专用的可执行文件
   - `/usr/bin` 后期安装的一些软件
   - `/usr/sbin` 超级用户的一些管理程序
-  `su - [用户名]` 切换用户且切换目录
-  `date` 今天日期
-  `cal` 日历表
-  `df/du` 根目录总的的空间使用状况/目录下子目录

   - `-h` 人性化显示（空间大小自动转换）
-  `ps` 显示当前开启的应用程序
   - `a` 显示终端上的所有进程，包括其他用户的进程
   - `u` 显示进程的详细状态（cpu、内存占用，使用用户等）
   - `x` 显示没有控制终端的进程
-  `top / htop` 动态显示内存和cpu占用高的程序
   - `q` 退出
-  `kill [UID]` 杀死进程
   -  \-9 强行结束
-  `find [路径] -name "[要搜索文件的条件]"` 搜索某文件
-  `tar `
   -  `-cvf [打包文件名.tar] [被打包的文件]` 将多个文件打包成一个大的文件
   -  `-xvf [解包文件名.tar]`  解包
   -  `-z` 打包的同时顺便压缩/解压缩（tar.gz）
   -  `-C` 加在最后，指定打/解 包/压缩后的保存路径
   -  `-j` 用bzip2压缩文件
-  `gzip` 
-  `init 0` 关机

## 知识

- 文件名和文件数据分开保存，硬链接指向磁盘上的位置，软链接指向文件

- 建立链接源文件尽量用绝对地址

- ```shell
  sudo rm /var/lib/dpkg/lock-frontend
  sudo rm /var/cahe/apt/archives/lock
  sudo rm /var/lib/dpkg/lock  			#解除锁
  ```

- 对于目录，可读就是进去以后能不能看到里面内容，可写就是能不能创建文件，可执行就是可不可以执行文件

- 应用程序的桌面入口快捷方式通常保存在 `/usr/share/applications` 目录下，以 `.desktop` 结尾

  - 里面的内容Icon代表图标，Exec代表源文件位置

- 卸载一个程序只需要删除解压缩目录，保存配置信息的隐藏目录（home目录下）和桌面快捷方式删掉

  ```shell
  #以删除pycharm为例
  sudo rm	-r /opt/pycharm-xxxx.x.x/
  rm -r ~/.PyCharmxxxx.x/
  rm /usr/share/applications/pycharm-xxxx.x.x/
  ```

# Python

## 优点

- 代码量少
- 开源
- 易理解
- 短期开发
- 同一件事情只用一种方法
- 没有歧义语法
- 扩展性强（用 `C` 或者 `C++` 编写然后在 `python` 中使用）

## 面向过程语法

- `print("%[类型]" % (变量1, 变量2), end = [以什么结尾])` 格式化输出，默认回车结尾

  > 第二个括号代表的实际上就是一个元组，可以用元组名替代
  >
  > 同时内部`"%[类型]" % ([元组名])` 同样可以作为一个字符串进行引用

  - `%0?d` 让整数为?长度，不足的地方用0补全（000001），多了不管他
  - `%?d` 同上，不足的地方用空格补全
  - `%.?f` 保留?位小数，四舍五入

- `#` 单行注释

  > 快捷键`Ctrl + /` 

  - `~ TODO [将要做的内容]` 建立一个TODO注释提醒自己（在注释内）

- `"""` 多行注释（用两个它把注释内容框起来）

  - `:param [形参1]: [表示内容]` 给函数的形参打注释

- `**` 幂

- `//` 整除

- `%` 取余

- `+` 

  - 加法运算
  - 拼接两个非数字型类型变量，形成一个新的变量（与`.extend`、`.append` 区别）

- `*` 

  - 进行乘法运算
  - 将非数字型类型变量重复指定次数，形成一个新的变量

- `type([变量])` 查看某变量的数据类型

- `input("[提示信息]")` 输入一个数，

- `exit()` 退出交互式程序）

- `[类型名]()` 将括号内的数变为指定类型

- `import [模块]` 通过`import`关键字导入一个模块（关键字）

  ```python
  import keyword
  print(keyword.kwlist)		#查看python中原本的内置关键字 
  ```

  - 调用格式：`[模块].[函数名]` 

    > 一个独立的`python` 文件就是一个模块

  - 通过`import [模块] as [别名]`给一个模块起一个别名，之后可以直接通过别名调用

  - `from [模块] import [方法]`可以从模块中导入个别函数/<a name="类返回">[类](#类)，之后可以直接调用函数名而不需要跟上模块</a>

    >  注意导入类时不需要跟`()`，直接输入类名即可
    >
    >  同时如果`import`后跟`*`，表示导入模块内所有的方法

  - 如果两个模块中存在同名的函数，则调用后一个

  - 导入模块时先查找当前目录再查找系统目录，在系统目录下创建和已存在的系统模块同名文件则无法调用系统模块（如`random`）

  - 导入某个模块时会直接先执行该模块中所有未缩进的内容

  - 需要导入模块时，最好按以下顺序导入

    1. 官方标准模块导入
    2. 第三方模块导入
    3. 应用程序模块导入

- `if (判断条件):` 判断语句（注意缩进）

  - `elif (判断条件2) :` 等价于`else if` （如果是`else` 则没有别的判断）

- `and` 、 `or` 、 `not` 逻辑运算符

- ``` python
  import random
  random.randint(a, b)			#生成[a, b]之间的整数（闭区间）
  ```

- `while [条件] :`  循环

  - `break` 、`continue` 和 `C` 相同

- `+=` 之类的的和 `C` 相同，转义符也相同（`\t` etc.）

- `def [函数名](形参1, 形参2) :` 定义一个函数（注意缩进）

  - `return` 也和 `C` 一样

    > `return` 可以不传递任何参数，同时后面的代码都不执行，有时可以借助这一功能为`if` 语句省略一个`else` ，同时如果想返回多个值可以使用元组
    >
    > > 同时如果函数返回的类型是元组，小括号可以省略
    >
    > ```python
    > def measure():
    >     ...					#函数体
    >     return t, w			#一次用元组返回多个值
    > gl_t, gl_w = measure()	#用多个变量一次接受函数的返回结果
    > ```

  - 函数中只有方法能够改变实参地址的数值，赋值语句对传入地址没有影响

    >  :arrow_down_small:当然也有例外情况:arrow_down_small:
    >
    >  ```python
    >  def function(num_1, _list):
    >    global num				#调用全局变量num
    >    num = 1					#改变全局变量
    >    num_1 += 1				#不改变全局变量
    >    _list += _list			#在全局变量列表末尾追加一个自己
    >    _list = _list + _list		#重新定义一个局部_list变量，不改变全局变量
    >  num = 0
    >  gl_list = [0]				#定义两个全局变量整数和列表
    >  function(num, gl_list)		#将全局变量作为实参传入函数
    >  ```

  - 先对函数的形参进行定义，在调用的时候可以**缺省参数**

    ```python
    def function(test_1, test_2 = "", test_3 = Ture):
        pass
    function(1, test_3 = false)					#不需要传入参数
    ```

    > 1. 缺省参数必须在函数的末尾
    > 2. 多个缺省参数必须在调用函数的时候打入参数名字

  - 当函数现需要处理的参数个数是不确定的，可以使用**多值参数**

    ```python
    def function(num, *args, **kwargs):
        print(num)
        print(*args)
        print(**kwargs)
    demo(1, 2, 3, num=1)
    #1传给num，(2, 3)作为元组传递给args，{'num': 1}作为字典传递给kwargs
    ```

    > 存放元组多值参数一般取名`*args` ，而存放字典的则取名`**kwargs` 
    >
    > > 其中`*/**` 表示拆包，可以把一个元组/字典变量拆分成若干个元素
    >
    > 因此，如果想传入元组`y`到一个多值参数内 ，则需要`function(1, *y)`，字典变量同

  - 当函数没有返回值时，默认返回一个空对象`None`

- `[列表名] = [[元素1], [元素2], ...]` 定义一个列表（数组）

  >  列表可以拥有不同类型的元素

  - `.index(元素)` 输出列表中项的索引位置

    >  列表中的索引从0开始，`[列表名][0]` 为第一个元素

  - `.append(元素)` 将一个**元素**追加到指定列表末尾

  - `.extend([列表名])` 将一个**列表**追加到指定列表末尾

  - `.insert([索引],[插入数据])` 在指定索引位置插入元素

    > `list.remove` 同

  - `.clear` 清除所有元素

  - `.pop/list.remove` 删除数据，前者指向索引，后者指向元素

    > `pop` 在默认情况下删除最后一个元素
    >
    > `del list[[索引]]` 同 `pop` ，而`del` 本质是将一个变量删除（不能使用该变量了）
    >
    > 列表存在相同数据时，`remove` 删除的是第一个元素

  - `.count(数据)` 统计该元素在列表中出现了几次

  - `.sort()` 升序排序

    > 括号内输入`reverse=true` 则降序，而`.reverse()` 为列表翻转

- `for [变量名] in [非数字型类型变量]:` 一次从变量（列表，元组，字典，字符串）中顺序取出一个元素保存在变量当中，循环次数为变量元素个数

  `else:` 当for循环不以break退出时，在循环结束之后执行的代码、

  > 可以显示列表里元素信息并添加不存在的元素

- `[元组名] = ([元素1], [元素2], ...)` 定义一个元组

  > 元组和列表很像，但是元组不可修改，一般用来保存类型不同的元素

  ```python
  _tuple = (0, )		#定义只有一个元素的元组
  a, b = b, a			#交换a,b元素（等号左边是两个变量，等号右边是一个元组（省略括号））
  ```

- `list([元组名])/tuple([列表名])` 元组与列表相互转换

- `[字典名] = {[键1]: [值1], [键2]: [值2], ...}` 定义一个字典

  > 常常用字典来定义某一个物体的各个特征，它可以与列表一起使用（通讯录）
  >
  > 使用 `print` 函数输出的时候往往与定义时的顺序不一样
  >
  > 字典的`key` 只能使用**不可变类型**，因为在`python` 中，字典`key` 的保存需要借助**哈希函数**来分配内存

  - `~[[键]] = [值]` 取值/增加/修改
  - `.pop(键)` 删除
  - `.update(字典名)`  合并字典，如果有相同的键则取后一个字典的

- `[字符串名] = "[内容]"` 定义一个字符串

  - `.is*` 用于判断字符串元素组成，返回布尔值，建议查表

  - `.startswith([字符串])` 判断是否以指定字符串开始（`endswith()` 同）

  - `.find/.index([字符串])` 查找是否存在指定字符串，存在则输出第一个字符索引

    > 如果不存在指定字符串，则`find` 输出-1，`index` 会报错

  - `.replace([替换字符串], [目标字符串])` 本行操作替换但不改变原有字符串

  - `.l/rjust/center([填充数量], [填充字符])`  左/右/居中对齐,默认填充字符为英文空格

  - `.l/rstrip()` 去除左/右两端空白字符

    ```python
    test = ["1","\t\n123","12345\t\n"]
    for test_str in test:
        print(test_str.strip.center(10))	#先执行去除空白字符，再居中
    ```

  - `.split([指定分隔符],[分割数量])` 将字符串以分隔符拆分为固定数量的字符串列表

    > 默认以`\r` `\t` `\n` 分割，不指定数量则分到完，返回值为一个列表
    >
    > 其中分割数量表示检测到几个分隔符为止，最终字符串数量为分割数量 + 1

  - `.join([字符串列表])` 以指定字符串为分隔符，将一个字符串列表合并成一个字符串

- `~[[开始索引]:[结束索引]:[步长]]` 非数字型类型变量（除字典）切片

  > 左闭右开，开始索引在内，结束索引不在内，结束索引不指定则切到最后一位
  >
  > 如果想切到倒数第几位，可以使用倒序索引，最后一位的索引为-1，以此类推
  >
  > 步长表示开始索引到结束索引内每隔一个步长截取一个字符（默认为1），步长为负数则倒序输出

- `len([非数字型类型变量])` 获得列表中的元素个数

- `del([变量])` 删除一个变量

  > `del` 也有关键字形式，效果相同，建议使用函数`del` 

- `max/min([非数字型类型变量])` 取变量集内最大/小的元素

  > 对于字典，只比较两者的`key` 

- `[值] in/not in [非数字型类型变量]` 判断元素是否存在于目标变量（成员运算符）

  > 对于`or` 判断十分有用
  >
  > ```python
  > if i in [1,2,3]:		#以此类推
  > ```

- `pass` 是一个关键字，表示一个占位符，能够保证程序的代码结构正确

- `id(变量)` 查看变量的地址

  > 数据的地址不变，变量的地址变化，把变量看作一张便签纸

- `hash([可变类型])` 通过内置的哈希函数计算**不可变类型**的哈希值

- `eval([字符串])` 将目标字符串当成表达式来计算（等于把双引号去掉）

  > 注意使用该函数不要把`input()` 当作参数直接计算，因为可能不怀好意的用户直接输入系统命令
  
- `format()`

## 注意点

- 区分大小写
- 驼峰命名法
- `=` 前后要加一个空格，`,` 后面要加一个空格
- 函数定义前后要求两个空行（ `PEP 8` 提示 ）
- 字典和字典不能比较大小，列表之间比较大小从第一个值开始比较
- 取列表里的列表内容最好就用`for` 循环实现
- 条件太多了就为条件增加一个`()` 后换行（Pycharm会自动缩进）
- `import` 导入时，每一个导入应该占一行

## PyCharm

- 删除家目录中的 `.PyCharmxxxx.x` 来恢复PyCharm的初始设置

  ```shell
  ls -la
  rm -r ~/.PyCharmxxxx.x
  ```

- 打开一个项目要先为他建立一个目录

- 打开目录之后会在该目录下创建一个 `.idea` 的目录用来存放当前python版本信息

- 将解压后的pycharm移动到 `/opt` 目录下

  ```shell
  tar -zxvf pycharmxxxxxxx.tar.gz	#解压
  sudo mv pycharmxxxx/ /opt/ 		#移动到opt目录
  cd /opt/pycharmxxxxx/bin		#移动到bin目录
  ./pycharm.sh					#启动
  ```

- F7（步入）可以将单步到函数内，但是F8（步过）会把调用函数一步完成

- 可以通过点击黄色的小灯泡来添加函数的形参注释

- `Ctrl + Q` 可以查看某方法的说明<img src="https://s2.loli.net/2021/12/05/5vU6xrGY9fqWQ2h.png" alt="image-20210125175554683" style="zoom: 50%;" title="[字符串].split 说明示例"/>

  1. 如图可通过括号内的提示进行了解该方法
  2. `self` 项可以忽略
  3. `optional` 表示该参数可选，同时下方英文会解释不填时的默认值
  4. `sep: /maxsplit: ` 表示参数名字，按照`: ` 给出的参数类型添加参数
  5. `->` 后表示该方法返回值的类型

- 可以在左下角的TODO窗口快速定位TODO

- `右击` → `重构` → `重命名` 可以对程序内的同一变量进行批量重命名（快捷键`Shift + F6`）

- 文件开头添加`#! [python3的绝对地址]` 可以在终端中不通过`python3` 命令执行`.py` 文件

  > `#!`叫 Shebang（也称为Hashbang），出现在文本文件的第一行的前两个字符

- 单步执行中深蓝色框住的地方就是当前执行的位置，可以通过左下角的`MainThread` 切换查看，当进入一个函数中时，会生成一个新的`MainThread` ，原有的仍旧存在，点击后用一个淡蓝色的框表示该函数还未执行完成

  > `MainThread` 中，`<module>` 表示主程序，进入一个函数后生成一个新的以函数名为开头的`MainThread` ，最后`:*` 表示该`MainThread` 最后执行的行数`*` 
  >
  > <center> <img src="https://s2.loli.net/2021/12/05/PsgRyacvq9jYodN.png" alt="image-20210129200124232" style="zoom:50%; align=center;" title="MainThread对话框示例" /> </center> 
  >
  > <img src="https://s2.loli.net/2021/12/05/GU4YdVSJOpsywob.png" alt="image-20210129201445899" title="深蓝色框" style="zoom:80%;" />
  >
  > ![image-20210129211615667](https://s2.loli.net/2021/12/05/RKqZrc5xX8Vf6ua.png "浅色框")
  
- 敲下`main`后按空格可以直接打印[`if __name__ == '__main__':`](#name属性解释)

- `Ctrl + Alt + L` 自动排版

## 知识性内容

### 解释器简介

`C`语言之类的叫做编译型语言，人们开发完以后统一交给编译器处理，然后再交给CPU

`Python`则是解释型语言，逐一读取代码，翻译一行执行一行

相比之下编译型语言执行的快，而解释型语言跨平台能力强

代码执行时，CPU先将解释器的程序复制到内存中，解释器让CPU翻译程序代码，再执行

### `.pyc` 后缀文件

`import` 导入一个模块的时候解释器会先将模块内容解释一遍生成后缀为`.pyc` 的文件

该文件保存在`python` 底下的`__pycache__`目录下

目录下`.pyc` 前面的表示用何版本`python`解释器解释过的程序

该文件为字节码（二进制文件），作为下次启动该模块的优化

### 关键字、函数和方法

关键字的后面的参数不需要小括号（如`if` 、`del` 等在`keyword.kwlist` 显示的）

函数可以在`import [关键字]` 后代码直接引用（`print` 、`input` 等）

方法必须是`[关键字].[方法]` （列表操作，可以通过`[关键字].` 来显示该关键字的方法）

函数需要死记硬背，方法可以不用背

### 集成开发环境（IDE）

- 代码补全，自动缩进
- 编译器/解释器
- 调试器（断点/单步执行）

### 一个项目的组成

1. 创建一个`_main.py` 文件
2. 为了程序的完整性往往需要一个无限循环`while True`，通过`break` 退出程序
3. 先写大的框架，在细节部分用`pass` 占位符
4. 对于每一个`TODO` 都可以用一个函数来执行

### 变量与内存

程序中的变量实际上只是指向所对应值的地址

重新定义变量意味着变量重新指向一个新开辟的内存空间

函数中，传递的是参数的地址而不是参数本身

内存中的数据不允许被修改的类型叫做不可变类型（数字类型，字符串，元组）

修改其中的值不改变原有内存地址的类型叫做可变类型（列表，字典）

类型的方法不改变内存地址，但是赋值语句会改变任何变量的地址

### 异常

当程序遇到问题时，`python` 的解释器会==**抛出异常**== ，程序员应该根据解释器抛出的异常进行处理

就算是正确的代码，用户不正确的执行仍旧会抛出异常

如果遇到某些代码符合语法规则，但是不知道执行情况，我们可以**捕获异常**

```python
try:										#尝试执行
    num = 1 / int(input())
except ValueError:							#错误名1
    print("Please input true integer")
except ZeroDivisionError:					#错误名2
    print("Don't input the zero")
except Exception as result:					#碰到未知错误，用result来作为异常状态的别名
    print("An unknown error: %s" % result)	#将未知的错误输出
    #注意到result捕获到的未知错误并不是错误名而是错误名后的内容（如下图的division by zero）
else:										#没有异常
    print(num)
finally:									#无条件执行
    print("PROGRAM END")
```

![image-20210208224905673](https://s2.loli.net/2021/12/05/rzYQ4W5RuLVoC9I.png "上述程序可能会出现的异常信息")

实际上，当一个函数/方法执行出现异常时，程序会将异常的信息传递到调用函数/方法的一方

直到传递到主程序时仍然没有进行异常处理，程序才会被终止

正因为如此，当函数内出现错误时，会出现多个报错，直到传递到主程序时终止

因此我们可以在主程序中利用异常的传递性，只在主程序中捕获异常

利用**抛出异常**的特性，可以在程序的执行过程中**主动的抛出异常**

```python
error = Exception("错误信息")	#先用Exception异常类定义一个异常对象
raise error						#使用raise关键字抛出异常对象
#注意到Exception后括号内填写的就是之前代码用到的Exception as result捕获到的内容
```

![image-20210209161936041](https://s2.loli.net/2021/12/05/UQ8Wjv6XhnkN4pH.png "主动抛出异常")

### 包

包是一个包含多个模块的特殊**目录**（window中的文件夹）

在该目录下必须包含文件`__init__.py`

想要通过外部导入的方式使用包内的模块，需要在`__init__.py` 文件中指定对外界提供的模块列表

```python
from . import [模块名]
```

#### 如何制作一个压缩包并分享给其他人

1. 在想要分享的**包**外创建`setup.py` 文件

2. 该文件内容为

   ```python
   from distutils.core import setup
   
   setup(name=[包名], 
         version=[版本信息], 
         description=[描述信息], 
         long_description=[完整的描述信息],
         author=[作者],
         author_email=[作者邮箱],
         url=[主页],
         py_modules=[[模块1], [模块2], ...])	#从distuils.core模块中调用setup函数
   ```

3. 在终端中构建模块

   ```shell
   $ python3 setup.py build
   ```

   该代码运行完成后，会生成一个`build`目录，包含`lib`目录，而`lib`中是我们想要分享的包

4. 继续在终端中生成发布压缩包

   ```shell
   $ python3 setup.py sdist
   ```

   执行后会生成一大堆提示，并生成一个`dist` 目录，在目录内就是目标包的压缩文件

5. 接收者先对该压缩文件解压缩，生成目标包的目录，内有一个目录和两个文件：

   `[包名]`内为发送者想要

   `PKG-INFO`该文件为该包的版本信息文件，内容便是之前在`setup.py` 内输入的内容

   `setup.py` 可执行文件，执行后在`python`系统目录中生成目标包

6. 之后接收者可以直接通过`import`导入接受的包

7. 想要删除某个包，先通过包的`__file__`属性确定包的绝对地址，找到它删除即可

### 文件

可以使用文本编辑软件查看的文件是文本文件，得用特定软件打开的文件是二进制文件

无论是否编辑，对文件的操作都要分成三步

1. 打开文件

2. 将磁盘的内容读入内存/将内存的内容写回磁盘

   > 一般软件打开文件时默认将其读入内存，当按下`Ctrl + S`时将内存中文件内容写回磁盘

3. 关闭文件

#### 调用文件

- `open("[文件名]", "[打开方式]")` 调用文件函数
  - `r` 只读方式，默认打开方式，文件不存在就报错，文件指针在开头
  - `w` 只写方式，创建一个新的文件，文件存在就覆盖原有文件
  - `a` 追加方式，文件指针被移动到文件末尾
  - `r/w/a+` 读写方式打开，功能和指针位置与前三种无异
  - 如果打开文件含有中文，则需在打卡方式后再加`encoding='utf-8'`

- `read()` 将文件内容读取到内存方法

  - 当无参数时，默认读取文件的全部内容

  - 读取完毕后，文件指针移动到读取内容的末尾

    > 文件指针标记`python` 从那个位置开始读取数据
    >
    > 因此当没有参数时，`read` 函数只能执行一次，执行完毕后文件指针指到文件末尾

- `readline()` 读取文件的一行内容，方法执行后，文件指针移到下一行

- `write("[内容]")` 将指定内容写入文件方法

- `close()` 关闭文件方法

  ```python
  #复制文件案例
  file_read = open("TEST")
  file_write = open("TEST1", "w")
  while True:
      text = file_read.readline()
      if not text:
          break
      file_write.write(text)
  file_write.close()
  file_read.close()
  ```

#### `with..as` 语句

紧跟with后面的语句被求值后，返回对象的`enter()`**方法**被调用，这个方法的返回值将被赋值给as后面的变量。当with后面的代码块全部被执行完之后，将调用前面返回对象的`exit()`**方法**

```python
class Sample:
    def __enter__(self):
        print "In __enter__()"
        return "Foo"
 
    def __exit__(self, type, value, trace):
        print "In __exit__()"
 
def get_sample():
    return Sample()
 
with get_sample() as sample:
    print "sample:", sample

代码输出结果如下：
In __enter__()
sample: Foo
In __exit__()
```

用`with` 调用文件不仅可以使代码层次清晰，更可以避免出现忘记关闭文件的问题

```python
with open('./sougou.html', 'w', encoding="utf-8") as fp:
    fp.write(page_text)
```

#### 文件管理操作

`import os` 这个模块可以执行常规的文件/目录管理操作，下述为这个模块的方法

同时所有的文件/目录名/命令名都应该加上`“”` 下面统一省略

- `rename([原文件名], [目标文件名])` 修改文件名
- `remove([文件名])` 删除文件
- `listdir([目录名])` 用列表输出目录内容
- `path.isdir([文件/目录名])` 判断一个对象是否为目录
- `mk/rmdir[目录名]` 创建/删除一个目录
- `getcwd()` 获取当前目录
- `system([命令名])` 使用系统中的命令

#### 文件编码格式

`ASCII` 编码每一个字符在内存中占用一个字节，`UTF-8` 是一种`UNICODE`编码格式，编码不同的字符表示字节数不同，汉字由三个字节表示

`python2` 默认`ASCII` 编码格式所以不支持中文输入，可以通过特定单行注释`# *-* coding:utf8 *-*` 来支持中文

> 但是即使如此`python2`在遍历时仍旧一个字节一个字节遍历，所以还是使用`python3` 吧！

## 面向对象（OOP）

### 基本概念

面向对象和面向过程一样都是一种编程方式

面向过程把完成某一个需求的所有步骤从头到尾逐步实现，然后根据代码的需求将某些功能独立的代码封装成一个又一个函数，而最后的代码只是顺序调用不同的函数，它不注重职责分工，对于需求复杂的项目代码也会变得十分复杂

面向对象是一个更大的封装，根据职责在一个对象中封装多个方法，然后让不同的对象调用不同的方法，每一个对象都有对应的职责，更加适合应对复杂的需求变化

### 类和对象

类是对一群具有相同**特征**或者**行为**事物的一个统称，不能够直接使用，是一个模板，负责创建对象

- **特征**被称为**属性**
- **行为**被称为**方法**

对象就是由类创建出来的一个具体存在，可以直接使用，由哪一个类中创建的对象，就拥有在哪一个类中定义的**属性**和**方法**

> 把一个类看成一张飞机图纸，上面画的是飞机各个零件，尽管它拥有飞机的所有组件，但一张图纸并不能飞起来，不具有对象的功能，必须把它组装成飞机，而这个由图纸创建出来的飞机就是对象

如上述，先有类再有对象，类只有一个，而对象可以有很多个，不同对象之间的属性可能不同，类中定义了什么属性和方法，对象中就有什么属性和方法

> 定义一个类的时候要使用大驼峰命名法（`CapWords`）

创建一个类的时候要先进行需求分析，一般来说，外观定义为属性，动作定义为方法

### 定义

- 定义一个只包含方法的<a name="类">[类](#类返回)</a>

  ```python
  class [类名]:		#大驼峰命名法
      def [方法1](self, [参数列表]):		#方法的第一个参数必须是self
          pass
      def [方法2](self, [参数列表]):
          pass
  ```

- 当类定义完成之后，用这个类来创建对象

  ```python
  [对象变量] = [类名]()
  ```

> 1. 不同的对象变量调用同一个类，对象之间互相独立
> 2. 未改变`__str__` 方法时，使用`print([对象变量])` 可以输出指定对象的十六进制内存地址
>
> ![image-20210131232034941](https://s2.loli.net/2021/12/05/AHTsUrVlGm3uxq9.png "定义一个空Cat类后用两个对象调用并输出")
>
> 3. **哪一个对象调用的方法，`self` 就是哪一个对象的引用！** 
> 4. 在方法内，使用`self.[属性名]` 访问传入对象的属性
> 5. 创建出来的对象叫做类的实例，创建这个动作叫做实例化
> 6. 广义的对象包含所有种类的元素（包括类，实例等等）
> 7. 调用方法后必须加`()`

- 创建一个类属性和类方法

  ```python
  class Tool(object):
      count = 0				#定义类属性(注意到类属性前不需要加Tool.)
      def __init__(self):		#有几个实例用的是该类
          count += 1			#改变类属性
          
  	@classmethod			#该标识符下方的方法为类方法
      def display_count(cls)	#该cls和self十分类似，哪一个类调用该方法，cls就是哪一个类
          print(cls.count)	#输出类属性
  
          
  tool = Tool()				#定义tool类
  Tool.display_count()		#调用类方法
  ```

  > 类属性可以计算有关该类的总体信息
  >
  > 使用`[实例名].[类属性]` 也可以访问类属性，但是并不推荐，因为该方法只能获取值并不能定义值（会变成一个实例属性）
  >
  > 类方法只能传递类属性，同时类方法必须在该类的内部定义并执行，虽然有所谓的`cls`，但是只有该类能够调用该类方法

- 定义一个静态方法

  ```python
  class Tool(object):	#定义一个类
      @staticmethod	#标识符，表示下述代码为静态方法
      def st():		#定义一个静态方法，不传递任何参数
          pass
  Tool.st()			#直接通过[类名].来访问某个类的静态方法,可以没有任何实例
  ```

### 语法

- `dir([对象])` 查看一个对象的所有属性和方法

  > 无论是函数，数据，变量都是一个对象

- `__[方法/属性名]__` 系统内置的方法/属性，存放在[`object`](#基类) 类内

- `__[方法/属性名]` 私有方法或者私有属性

  > 私有方法/属性只能在一个对象内部通过方法使用，而不能在主程序中被访问到
  >
  > 但事实上，通过`[对象]._[类名]__[方法/属性名]` 依旧可以访问到~~虚假的私有….~~
  >
  > [子类](#子类)不能在自己的方法内部访问到父类的私有属性/方法

- `[变量] = None` 如果不知道给一个变量设定什么值，就指定一个空对象，用`is` 来判断

- `[变量1] is [变量2]` 用于判断两个变量是否为同一个内存地址（是否为同一对象）

  > 类似`id([变量1]) == id([变量2])`

- `__init__` 使用`[类名]()` 创建一个对象之后，会自动调用的初始化方法

  > 通过在该方法内`[对象].[属性名] = [属性值]`给一个对象增加属性

  ```python
  class demo:
      def __init__(self, arg):		#定义方法__init__
          self.attribute = arg		#为调用该类的对象定义属性
  test = demo("test")					#调用类demo，省略self，并传入参数test
  ```

- `__doc__` 查看一个函数的文档说明

- `__del__` 对象从内存中销毁前会被自动调用的方法

  > 1. 当程序结束之后，会对所有的变量进行回收
  > 2. 使用`del` 关键字删除某个变量

- `__str__` 希望使用`print` 输出变量时能够打印自定义内容

  > 如果需要用该方法，必须用`return` 返回一个字符串

- `class [子类]([父类1], [父类2])` 将<a name="子类">子类</a>继承父类的除私有属性和方法外所有属性和方法

  > 子类从父类继承/派生，子类是父类的基类/派生类
  >
  > 如果父类的方法不能满足子类的需求，继承之后可以对父类的方法进行重写

  - 使用`super().[重写方法名]`可以在重写某一方法后再次调用父类的方法 
  - 假设不同的父类有同一个方法，则执行`[父类1]` 的方法

- `__mro__` 查看类中方法的搜索顺序

  > 一般顺序为`[本类]`→`[父类1,2...]`→`object`
  >
  > > `object` 是所有类的父类，叫<a name="基类">基类</a>，所有的类在创建时会以它为父类
  > >
  > > 碰到一个方法时，由此顺序寻找各个类中是否拥有该方法，如果有则执行，并结束寻找

- `__new__` 当创建实例**之前**作为静态方法被调用，返回值为为实例分配的内存空间

  ```python
  def __new__(cls, *args, **kwargs):	#重写__new__静态方法
  return super().__new__(cls)		#object内的__new__方法不起作用了，要调用父级
  #注意到该静态方法有一个cls的参数，很奇怪
  #该程序中调用父级时仍旧传递cls参数
  ```

- `__file__` **模块的属性**，用于查看模块的完整路径

  > 模块的属性可以在程序中直接通过`print(__[属性名]__)`来查看

- <a name="name属性解释">`__name__`</a> **模块的属性**，当直接执行本文件时，该属性为`__main__`，作为模块导入另一个文件时该属性为该文件名称

  > 利用这个特性可以在原有文件中通过判断该属性是否为`__main__`来使导入文件时不再执行原有文件代码
  >
  > 同时正规的模块导入文件也有相应的默认格式要求
  >
  > ```python
  > # 导入模块
  > # 定义全局变量
  > # 定义类
  > # 定义函数
  > # 在代码最下方
  > def main():
  >  pass
  > if __name__ == "__main__":
  >  main()
  > ```

- `__import__("[模块名]")` 等价于`import [模块]` 但该属性可以直接引用模块方法

  ```python
  __import__('os').system('rm xxx')	#调用系统Linux删除命令
  ```

### 单例设计模式

设计模式是前人工作的总结和提炼，是针对某一特定问题的成熟的解决方案

目的是让一个类创建的对象，在系统中只有唯一的一个实例

每一次执行`[类名]()` 返回的对象内存地址是相同的

使用`__new__` 方法的重写和类属性实现内存地址不变

```python
class Demo(object):
    instance = None								#定义一个类属性指向空的内存地址
    def __new__(cls, *args, **kwargs):			#重写__new__方法
        if cls.instance is None:				#判断传入__new__的类的类属性地址是否为空（is）
            cls.instance = super().__new__(cls)	#调用父级__new__方法分配内存空间
        return cls.instance						#返回内存空间值
```

在没有别的更改的情况下，每一次创建实例`__init__` 初始化方法仍旧会被执行多次

不想多次执行初始化操作同样可以定义一个新的类属性来实现，下略

## Pygame

### 游戏相关知识

#### 游戏的初始化和退出

使用`Pygame` 提供的所有功能之前，需要调用`init`方法，游戏结束前需要调用`quit` 方法

> `init` 方法主要是针对图像的绘制，窗口的处理进行初始化

```python
import pygame
pygame.init()
# 代码
pygame.quit()j
```

#### 游戏窗口及元素

游戏窗口的左上角是坐标系的原点，水平方向是x轴，竖直方向是y轴

所有可见的元素都是以矩形区域来描述位置的，元素的锚点在左上角

##### 创建一个元素

要描述一个矩形元素需要四个要素

- x，y轴坐标
- 矩形区域的长（height）和宽（width）

利用`rect(x, y, width, height)` 方法可以创建一个矩形区域

> 另外`Rect` 是一个特殊的类，只包含数字的运算，可以不执行`init` 方法直接使用
>
> 同时`Rect` 封装了一个`size` 属性，封装一个元组用于查看宽和高，还封装了一个`bottom = = y + height` 属性，`centerx/y = x/y + 0.5 * width/height`属性，

```python
hero_rect = pygame.Rect(100, 500, 120, 125)
print(hero_rect.x, hero_rect.y)
print("%d %d" % hero_rect.size)
# 输出为100 500 120 125
```

##### 创建一个主窗口

`Pygame` 专门做了一个模块`Pygame.display` 用于创建和管理游戏窗口

- `set_mode(resolution=(0,0), flags=0, depth=0)` 初始化游戏显示窗口
  - 该函数四个参数都是缺省参数
  - `resolution` 是窗口的宽度和高度
  - `flags` 是指定屏幕的附加选项（是否全屏等）
  - `depth` 表示颜色的位数（24位真彩色等），默认自动匹配
  - 该函数返回结果为一个游戏窗口，必须使用一个变量来记录返回结果
- `update()`更新整个屏幕的显示

##### 如何显示一个图像到创建的窗口

和窗口模块类似，`pygame.image`模块用于图像操作，其中`load([文件名])` 可以加载一个图片对象

与此类似的还有`pygame.Surface.blit([图像], [位置])` 可以将指定图像绘制到指定位置 

而且想在屏幕上看到最终的结果，一定要调用`pygame.display.update()` 方法

> 事实上，通过`set_mode` 创建的对象只是一个在内存中的数据对象，`bilt` 方法只是在这个数据对象上绘制一个图像，`update` 方法的作用就是把这个数据对象的最终结果展现在我们实际的屏幕上

```python
# 省略初始化代码
screen = pygame.display.set_mode((480, 700))
bg = pygame.image.load("../images/background.png")
screen.blit(bg, (0, 0))
pygame.display.update()
```

#### 游戏循环和游戏时钟

每一次调用`update` 方法产生的结果就是一帧，多次执行形成动画效果

游戏的无限循环就是游戏循环，意味着游戏的正式开始，其上方部分是初始化部分

常规上各部分<a name="游戏初始化和游戏循环">内容大致为</a>

- 游戏初始化部分
  - 设置游戏窗口
  - 绘制图像的初始位置
  - 设置游戏时钟
- 游戏循环
  - 设置刷新帧率
  - 检测用户交互
  - 检测游戏内判断
  - 更新所有图像位置
  - 更新屏幕显示

利用`pygame.time.Clock` 创建时钟对象，在游戏循环中调用`tick([帧率])` 方法指定执行频率

##### 结合`Rect`方法达到动画效果

```python
# 接上代码
clock = pygame.time.Clock()
me1_rect = pygame.Rect(200, 500, 102, 126)
while True:
    clock.tick(1)				# 每秒钟刷新一次
    me1_rect.y -= 50
    screen.blit(me1, me1_rect)	# 对于位置参数，只接收me1_rect元组内x, y两个位置参数
    pygame.display.update()
```

会发现这样的程序实现结果会令飞机留下残影，解决方法是每一帧重新绘制一遍背景图像

```python
screen.blit(bg, (0, 0))	# 加在上述代码第六行后
```

#### 游戏中的监听和事件

事件就是用户对于游戏的操作

监听就是在游戏循环中判断用户的具体操作

`pygame` 中通过`pygame.event.get()` 模块可以获得用户当前所做动作的**所有**事件**列表**

对于获得列表的每一个元素，有`type` 属性来记录用户该时刻的操作类型

##### 事件含义

- `Keydown`表示按下某按键
- `Keyup ` 表示松开某按键
- `MouseMotion` 表示鼠标移动
- `Quit` 表示点击右上退出按钮

##### 相关代码

对于监听，代码相对来说十分固定

```python
for event in pygame.event.get()
	if event.type == pygame.QUIT:	# 判断是否是退出事件
  	  	print("退出游戏")
 	  	pygame.quit()
  	  	exit()
```

#### 精灵和精灵组

`pygame.sprite` 提供了精灵`Sprite`和精灵组`Group`两个类，可以方便的操作某个图像在窗口上的移动

> 其中，`pygame` 是一个包，`sprite` 是这个包里的一个模块名称，`Sprite` 才是类名称（开头大写）

一个储存了图像数据属性`image` 和位置属性`rect` 的对象就叫做精灵

每个精灵可以通过`update` 方法更新精灵的位置

实际开发中，我们可以根据不同的游戏角色派生出不同的子类精灵，在不同的精灵中通过重写`update` 方法进行不同的运动

包含了多个精灵的对象叫做精灵组

创建精灵组的时候可以使用多值参数的方法传入多个精灵（`__init__(self, *精灵)`）

之后在游戏循环中直接通过`[精灵组].update` 和`[精灵组].draw(screen)` 来批量调用各个精灵的`update` 方法，并显示在屏幕中

> 精灵组调用`update` 方法，精灵组中的精灵各自调用各自的`update` 方法
>
> 精灵组的`draw(screen)`方法会将精灵组中所有的精灵的`image` 属性绘制到`Surface`的`rect` 位置，之后与`screen.bilt` 方法雷同，还需要再执行`pygame.display.update()` 方法
>
> >  `screen`就是一个`Surface`类，而`blit`方法事实上也所属`Surface` 类

### 正式的PlaneBattle游戏开发

#### 派生精灵子类

一个游戏的开发往往需要派生多个精灵子类，这时候需要用到**继承父类**来简便的建立一个子类

> 记住当一个类的父类不只是`object` 时，一定要先`super()`一下父类的`__init__`方法，来保证父类中实现的`__init__` 代码能够被正常执行

1. 新建一个`plane_sprite` 文件

2. 定义`GameSprite` 子类继承自`pygame.sprite.Sprite` 

3. 对子类`GameSprite` 进行属性和方法分析

   | GameSprite                                                  |
   | :---------------------------------------------------------- |
   | `image`<br />`rect`<br />`speed`                            |
   | `__init__(self, image_name, speed=1):`<br />`update(self):` |

   > `python.image` 还提供有`rect` 方法，可以返回一个`pygame.Rect(0, 0, [该图像宽], [高])`的对象，可以方便的获得某个图像的长宽
   >
   > 通过初始化方法中的`image_name` 来加载图片，并指定图片的位置
   >
   > 而在这个类中，`update` 方法可以让`self.rect.y`值和速度`self.speed` 相加，从而移动对象

   ```python
   import pygame
   class GameSprite(pygame.sprite.Sprite):
       """飞机大战游戏精灵"""
       def __init__(self, image_name, speed=1):
           super().__init__()
           self.image = pygame.image.load(image_name)
           self.rect = self.image.get_rect()
           self.speed = speed
       def update(self)
           self.rect.y += self.speed
   ```

#### 游戏框架搭建

一个游戏的主程序需要进行游戏的初始化和游戏循环

因此设计的主游戏类也应该包含这两个功能方法

1. 创建一个`PlaneGame`类

2. 根据职责封装私有方法，可以避免某一个方法的代码太过冗长

3. 进行游戏初始化和游戏循环的方法[分析](#游戏初始化和游戏循环)

4. `PlaneGame`类的属性和方法分析

   | PlaneGame                                                    |
   | ------------------------------------------------------------ |
   | `screen`<br />`block`<br />`精灵组或精灵`                    |
   | `__init__(self):`<br />`__create_sprites(self):`<br /><br />`start_game(self):`<br />`__event_handler(self):`<br />`__check_collide(self):`<br />`__update_sprites(self):`<br />`__game_over()` |

#### 明确文件职责

在该游戏中，只需要两个`python`文件即可

- `plane_main`
  1. 封装主游戏类
  2. 创建游戏对象
  3. 启动游戏
- `plane_sprites`
  1. 封装游戏中所有需要使用的精灵子类
  2. 提供游戏的相关工具

一般来说，开发游戏的一个步骤就是创建所需文件并在文件中定义空类，这样才不至于在开发游戏时有所缺漏

#### 常量与变量

游戏中，禁止直接使用数字，所有的参数都应该是某个变量/常量

定义常量的方法和变量完全一样，但是常量的命名所有的字母必须是大写，单词和单词用下划线连接

`python` 中没有真正意义上的常量，因为他是纯动态语言

对于本游戏，可以创建一个常量来保存屏幕大小和帧率

```python
SCREEN_RECT = pygame.Rect(0, 0, 480, 700)
FRAME_PER_SEC = 60
```

#### 如何实现背景滚动

思路：游戏启动后，背景图像连续不断地向下方移动

让两张图像连续竖向排列，一阵图片完全移出窗口后再将其移动至窗口上方

新建一个`Background`类，继承于`GameSprites` 类

```python	
# 工具文件
class Background(GameSprite):
    def update(self, *args, **kwargs) -> None:
        super().update()
        if self.rect.y >= SCREEN_RECT.height:
            self.rect.y = -self.rect.height
            
# 主文件
    bg1 = Background("../images/background.png")
    bg2 = Background("../images/background.png")
    bg2.rect.y = -bg2.rect.height
    self.back_group = pygame.sprite.Group(bg1, bg2)
```

> 该程序依旧存在不少缺陷
>
> 1. 可以把背景图像信息封装到背景类中，简化代码
>
> 2. 主程序不应该用来指定某个精灵的初始化位置
>
>    ```python
>    # 为背景类添加初始化属性
>        def __init__(self, is_alt=False):
>            super().__init__("../images/background.png")
>            if is_alt:
>                self.rect.y = -self.rect.height
>    ```

#### 如何添加敌人飞机

##### 定时器

使用`pygame` 内的`time.set_time(eventid, milliseconds)`定时器类来实现每一秒飞入一架敌机

- `eventid `是事件代号，每一个数值对应具体的事件，需要基于`pygame.USEREVENT` 来指定

  > `USEREVENT`是一个专门给用户用的事件代号，对其+1/-1可以实现多个自定义事件的添加

- `milliseconds` 以**毫秒**（1s = 1000ms）作为单位，指定事件触发的间隔时间
- 通过`pygame.event.get()` 配合`event.type` 与`eventid` 进行比较，判断事件代号从而执行事件

使用定时器的套路十分固定

1. 定义定时器常量——`eventid` 
2. 在初始化方法中，调用`set_timer` 方法设置定时器事件
3. 在游戏循环中监听定时器事件

##### 具体思路

新建一个`Enemy`类，依旧继承于`Gamesprites` 类，设计每架敌机的事件

1. 敌机向屏幕下方飞行，飞行速度各不相同
2. 每架敌机出现的水平位置也不尽相同
3. 敌机从屏幕下方飞出，不会再回到屏幕中
4. 一秒出现一架敌机

根据需求，判断`__init__`和`update` 方法需要执行的内容

```python
class Enemy(GameSprite):
    def __init__(self):
        super().__init__("../images/enemy1.png")
        self.speed = random.randint(1, 3)
        self.rect.bottom = 0
        self.rect.x = random.randint(0, SCREEN_RECT.width - self.rect.width)
    def update(self, *args, **kwargs) -> None:
        super().update()
        if self.rect.y >= SCREEN_RECT.height:
            self.kill()
```

同时，面对这种多次出现的相同精灵，可以每创建一个精灵直接通过`add` 方法丢进精灵组，并且在单个精灵的`update` 方法中通过`self.kill()` 在不需要该精灵的帧时对其删除（如上）

```python
# 定时添加敌机模块
if event.type == CREAT_ENEMY_EVENT:
    enemy = Enemy()
    self.enemy_group.add(enemy)
```

> 创造组再往里面丢精灵是最为常用的制造批量对象的方法

#### 设计玩家飞机及子弹

##### 捕获键盘按键

1. ```python
   if event.type == pygame.KEYDOWN and event.key == pygame.K_RIGHT:
       print("向右移动")
   ```

   事件监听只能判断一次，当按下某个键不放手时不进行第二次执行

2. ```python
   # 使用get_pressed()键盘模块方法
   keys_pressed = pygame.key.get_pressed()
   if keys_pressed[pygame.K_d]:
       print("向右移动")
   ```

   每一帧都执行一次，可以保证持续连贯的移动

##### 设计思路

定义`Plane` 类，玩家飞机需要有移动和开火两个，因此除`update` 外还需要创建`fire` 方法

```python
class Plane(GameSprite):
    def __init__(self):
        super().__init__("../images/me1.png", 0)
        self.rect.centerx = SCREEN_RECT.centerx
        self.rect.bottom = SCREEN_RECT.bottom - 120
        self.bullets = pygame.sprite.Group()
    def update(self, *args, **kwargs) -> None:
        self.rect.x += self.speed
        if self.rect.x < 0:
            self.rect.x = 0
        if self.rect.right > SCREEN_RECT.right:
            self.rect.right = SCREEN_RECT.right
    def fire(self):
        bullet = Bullet()
        bullet.rect.bottom = self.rect.y
        bullet.rect.centerx = self.rect.centerx
        self.bullets.add(bullet)
```

注意到，玩家飞机在执行`update` 方法时没有调用父级方法，因为玩家飞机的运动与父级设计的完全不一样

> 但是我们可以改善父级的`update` 方法，满足个性化需求，如：
>
> ```python
>     def __init__(self, image_name, speedy=1.0, speedx=0):	#增加方向轴属性
>         super().__init__()
>         self.speedy = speedy
>         self.speedx = speedx
>     def update(self, *args, **kwargs) -> None:
>         self.rect.y += self.speedy
>         self.rect.x += self.speedx
> ```

为了使飞机不飞出边界，应当使用如上方第九、十行代码操作

因为子弹飞出位置和飞机当前位置相关，通过`fire` 方法可以非常方便的达成要求

子弹精灵的方法设计和敌机的基本相同，注意速度为负数

```python
class Bullet(GameSprite):
    def __init__(self):
        super().__init__("../images/bullet1.png", -2)
    def update(self, *args, **kwargs) -> None:
        super().update()
        if self.rect.bottom < 0:
            self.kill()
```

#### 碰撞检测

`pygame.sprite` 提供了两个方法`spritecollide` 和`groupcollide`，用于检测精灵和**精灵组**/精灵组和精灵组的碰撞

- `groupcollide(group1, group2, dokill1, dokill2, collided = None)`
  - `group1/2` 代表需要判断的两个精灵组
  - `dokill` 参数设置为`True`时，发生碰撞的精灵被移除
  - `collided`参数没什么卵用
- `spritecollide(sprite, group, dokill, collided = None)` 
  - `dokill` 专门控制精灵组中的精灵是否删除
  - 返回值为一个列表，返回和精灵发生碰撞的精灵列表

```python
def __check_collide(self):
    pygame.sprite.groupcollide(self.plane.bullets, self.enemy_group, True, True)
    enemies = pygame.sprite.spritecollide(self.plane, self.enemy_group, True)
    if enemies:
        self.plane.kill()
        PlaneGame.__game_over()
```

## 爬虫

### 爬虫的分类

- 通用爬虫：抓取一整张页面数据，抓取系统的重要组成部分
- 聚焦爬虫：建立在通用爬虫的基础上，抓取页面中特定的局部数据
- 增量型爬虫：检测网站中数据更新的情况，只会抓取更新出来的数据

### 常用头信息

`User-Agent` 请求载体的身份标识（UA）

`Connection` 请求完毕后是否断开连接

`Content-Type` 服务器响应回客户端的数据类型

### 加密方式

`https` 是安全的`http` 协议，因为对其进行了加密

- 对称密钥加密：密钥和密文放在一起传过去

- 非对称密钥加密：

  1. 服务器创建密钥对
  2. 将公钥发送给客户端
  3. 客户端使用公钥对信息进行加密并将密文发送给服务器
  4. 服务器通过私钥解密

  > 弊端是可能公钥被拦截后篡改，同时操作复杂影响通信速度

- 证书密钥加密（`https` ）

  1. 服务器开发者向数字证书认证机构提出公钥的申请
  2. 机构对公钥进行审核并数字签名
  3. 客户端收到已签名的公钥再对其解密

### `requests`模块

基于网络请求的模块还有`urllib`模块，但是比较古老，不怎么用了

一般来说都用`requests` 模块，功能十分强大，可以模拟浏览器发送请求

#### 使用方法

1. 指定`url` 
   - UA伪装
   - 请求参数的处理
2. 发起请求（模拟`http/https` 协议发请求）
3. 获取相应数据（浏览器页面）
4. 持久化存储（数据库）

```python
import requests
if __name__ == '__main__':
    url = "http://www.sogou.com/"  # 指定url
    response = requests.get(url=url)  # 发起请求，并返回一个响应对象
    page_text = response.text  # 返回字符串类型的响应数据
    print(page_text)
    with open('./sougou.html', 'w', encoding="utf-8") as fp:
        fp.write(page_text)
```

#### 自制搜索引擎

![image-20210221162749966](https://s2.loli.net/2021/12/05/jHYxgSh3V65Ffp4.png "百度搜索后地址栏显示内容")

如图，对于百度搜索引擎，在域名后加`s?wd=搜索内容` 即可实现搜索

利用百度的搜索引擎在`python` 中搜索自己想要的内容

```python
if __name__ == '__main__':
    url = "http://www.baidu.com/s?"  # 指定url
    kw = input("enter a word")
    param = {
        "wd": kw
    }
    response = requests.get(url=url, params=param)  # 发起请求，并返回一个响应对象，并在域名后动态拼接一个字典
    page_text = response.text  # 返回字符串类型的响应数据
    filename = 'Search ' + kw + ' by Baidu.html'
    print(page_text)
    with open(filename, 'w', encoding="utf-8") as fp:
        fp.write(page_text)
```

#### UA伪装

注意到利用爬虫访问的UA标识里可以看出不是浏览器请求，因此网站可以通过UA检测制定反爬虫规则

差不多百分之八十的网站都有UA检测

但是我们可以通过**UA伪装**，即将爬虫对应的请求载体身份标识伪装成某一浏览器来进行反反爬虫策略

![image-20210221165653048](https://s2.loli.net/2021/12/05/OIvzeljpMYUqRBu.png "用百度打败百度")

如图可以定位本机电脑的UA字符串，用于伪装

```python
headers = {
    'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/88.0.4324.182 Safari/537.36'
}
response = requests.get(url=url, params=param, headers=headers)  # 发起请求，并返回一个响应对象，并在域名后动态拼接一个字典，且身份标识为本机电脑
```

#### 百度翻译提取翻译结果

当在百度上输入一个单词时会生成一个携带了参数（输入的单词）的`POST`类型的`AJAX`请求发送给服务器，服务器的响应数据时一组`json` 数据

![image-20210221202706125](https://s2.loli.net/2021/12/05/e9Pzdqhp1wBMU5D.png "搜索cat时返回的文件内容")

将该页面拉到底会发现本地发送请求的数据内容

![image-20210221202818711](https://s2.loli.net/2021/12/05/Pc58WQqAsrHnKuO.png "客户端发送了一个cat喵")

同理，通过`requests` 库请求时也应该发送一个`POST` 请求

```python
import requests
import json
if __name__ == '__main__':
    # UA伪装
    headers = {
        'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/88.0.4324.182 Safari/537.36'
    }
    post_url = 'https://fanyi.baidu.com/sug'  # 注意url不是地址栏显示的域名哦
    # 发送POST请求参数的处理（与get方法请求基本一致）
    word = input('enter a word: ')
    data = {
        'kw': word
    }
    response = requests.post(post_url, data, headers=headers)
    dic_obj = response.json()  # json方法返回的是一个字典对象，必须是服务器响应的是一组json数据
    filename = word + ' by Baidu Translation.json'
    fp = open(filename, 'w', encoding='utf-8')  # 创建一个json文件
    json.dump(dic_obj, fp=fp, ensure_ascii=False)  # 使用json模块存入爬取到的内容，有中文所以不用ascii编码
```

#### 豆瓣排行榜

会发现滚轮滚到底部的时候发起了一个`AJAX`请求（因为地址栏内容没有变化）

![image-20210221205118544](https://s2.loli.net/2021/12/05/wvEK35iVmB7CpWO.png)

看似这个`URL` 很长，但实际上`top_list?`后的内容都是参数，而在该页面底部我们能找到一模一样的参数

![image-20210221205327527](https://s2.loli.net/2021/12/05/gpH62Xo8uVSMA1O.png)

所以可以把`URL` 内的参数删除，用字典形式封装参数

```python
import requests
import json
if __name__ == '__main__':
    headers = {
        'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/88.0.4324.182 Safari/537.36'
    }
    url = 'https://movie.douban.com/j/chart/top_list?'
    param = {
        'type': '24',
        'interval_id': '100:90',
        'action':'',
        'start': '0',  # 从库中的第几部电影中取
        'limit': '1',  # 一次取出的个数
    }  # 注意复制参数时要加引号，成为键值形式
    response = requests.get(url, param, headers=headers)
    list_data = response.json()
    fp = open('./douban.json', 'w', encoding='utf-8')
    json.dump(list_data, fp=fp, ensure_ascii=False)
```

#### 化妆品生产许可详情

![image-20210221215223444](https://s2.loli.net/2021/12/05/OXZCqHPVoYzyurA.png "目标网站首页")

![image-20210221215312151](https://s2.loli.net/2021/12/05/VgqlMnfyx4rpWbh.png "目标网站详情页")

会发现直接爬取`URL` 得到的界面并没有任何信息，且有很多乱码

原来是因为那些信息是通过另一个请求得到的（AJAX）

![image-20210221212544420](https://s2.loli.net/2021/12/05/qhimL6fBgQJTESx.png "和之前一样抓包到的XHR请求")

哇好神奇，真的可以通过`XHD`捕捉到一个数据包欸

会发现他也是返回`json` 文件，依葫芦画瓢，可以爬取到他的公司数据

通过观察可以发现返回的`json` 文件中有一个神秘的`ID`

![image-20210221214220886](https://s2.loli.net/2021/12/05/lfR2SMoHOmYQvjI.png "返回的直观信息")

而当我们点入公司证书页面时地址栏也有一个神秘的`ID`

![image-20210221214324932](https://s2.loli.net/2021/12/05/LhzIEnwZPaxNpkD.png "某公司地址栏")

哇塞，两个`ID` 居然是一样的欸，于是我们直接缝合怪就可以找到某家企业详情页的`URL` 

但是这还不够，通过同样的方法，我们会发现详情页里面的内容居然也是`AJAX` ，简直离谱

幸好发送的内容同样也是`ID` ，所以只要掌握了`ID` 就拥有了一切

![image-20210222114953224](https://s2.loli.net/2021/12/05/A2jzhxeZrgbCRWD.png)

通过观察发现首页中返回的`ID` 值在`json`字典中`list` 子字典位置，通过遍历可以遍历每个`ID` 

```python
import requests
import json

if __name__ == '__main__':
    headers = {
        'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/88.0.4324.182 Safari/537.36'
    }
    url = "http://scxk.nmpa.gov.cn:81/xk/itownet/portalAction.do?method=getXkzsList"
    id_list = []  # 存储企业的id
    for page in range(1, 6): # 遍历一到五页
        page = str(page)
        data = {
            'on': 'true',
            'page': page,
            'pageSize': '15',
            'productName': '',
            'conditionType': '1',
            'applyname': '',
        } # 来源于网络抓包
        json_ids = requests.post(url, data, headers=headers).json()
        for dic in json_ids['list']:  # 拿到列表中每一个公司的id值
            id_list.append(dic['ID'])  # 注意到要调用append方法必须已经有一个空字典
    # 获取企业详情数据
    # 会发现发送的AJAX请求url大体上并不变，变的只是最后method内容
    all_data_list = [] 
    url = 'http://scxk.nmpa.gov.cn:81/xk/itownet/portalAction.do?method=getXkzsById'
    for id in id_list:
        data = {
            'id': id
        }
        detail_json = requests.post(url, data, headers=headers).json()
        all_data_list.append(detail_json)
    fp = open('../result/alldata.json', 'w', encoding='utf-8')
    json.dump(all_data_list, fp=fp, ensure_ascii=False)
```

### 数据解析

对爬取到的整张页面进行解析操作，也就是聚焦爬虫

#### 正则

##### 语法

- `.` 除换行外所有字符

- `[]` 匹配集合中的任意一个字符`[aoe] [a-w]`

- `\d` 数字

- `\D` 非数字

- `\w` 数字、字母、下划线、中文

- `\W` 非`\w` 的其他字符

- `\s` 所有的空白字符包

- `\S` 非空白

- `*` 任意多次

- `+` 至少一次

- `?` 可有可无

- `{m}` 固定m次

- `{m,}` 至少m次

- `{m, n}` m-n次

- `$` 以某某结尾

- `^` 以某某开头

- `(ab)` 分组

- `.*` 贪婪模式

- `.*?` 懒惰模式

- `re.I` 忽略大小写

- `re.M` 多行匹配

- `re,S` 单行匹配

- `re.sub(正则表达式, 替换内容, 字符串)` 基本格式

##### 使用正则表达式爬取网站上的所有图片

通过对网站源码分析，可以找到图片所在的`div` 对其标签进行提取

![image-20210222135713091](https://s2.loli.net/2021/12/05/XgbYynJSmjAVuwK.png)

 下方所有的其他图片也都是这个路径，可以通过正则表达式查找所有图片标签

表达式`<div class="thumb">.*?<img src="(.*?)" alt.*?</div>`

同时会发现页面跳转时地址栏的信息变了

![image-20210222145639874](https://s2.loli.net/2021/12/05/eqQkfcMSFTyBKLX.png)

根据这个变化可以依次爬取所有页面的图片信息

```python
import requests
import re
import os
if __name__ == '__main__':
    # 创建一个文件夹保存所有图片
    if not os.path.exists('../result/SpiderPicture'):
        os.mkdir('../result/SpiderPicture')
    headers = {
        'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/88.0.4324.182 Safari/537.36'
    }
    # 设置一个通用的url模板
    url_model = 'https://www.qiushibaike.com/imgrank/page/%d'
    for pageNum in range(1,3):
        url = format(url_model%pageNum)  # 对应页码的url
        page_text = requests.get(url, headers=headers).text  # 主页面源码
        # 使用正则表达式提取图片
        ex = '<div class="thumb">.*?<img src="(.*?)" alt.*?</div>'  # .*?就代表任意字符
        img_src_list = re.findall(ex, page_text, re.S)  # 数据解析一定是re.S
        # 会发现提取到的图片地址没有协议头
        for src in img_src_list:
            src = 'https:' + src
            # content返回的是一个二进制形式的图片数据，可以用大多数软件直接打开
            # text （字符串） content （二进制） json() （对象）
            img_data = requests.get(src, headers=headers).content
            # 生成图片名称
            img_name = src.split('/')[-1]  # 以/为分隔符，取分割后生成的列表的最后一个元素
            imgPath = '../result/SpiderPicture/' + img_name  # 图片存储路径
            with open(imgPath, 'wb') as fp:
                fp.write(img_data)
                print(img_name, '下载成功')
```

注意到某些视频网站的视频内容有可能是一段`js`代码，这导致`xpath`和`bs4`都没有用，然而正则yyds

#### bs4（仅使用于`python`）

原理类似于正则

1. 实例化一个`BeautifulSoup`对象，并且将页面源码数据加载到该对象中
2. 通过调用`BeautifulSoup`对象中相关的属性或者方法进行标签定位和数据提取

想用bs4还得进行环境安装，需要安装bs4和lxml解析器

```python
# 实例化BeautifulSoup对象
from bs4 import BeautifulSoup
page_text = response.text
soup = BeautifulSoup(page_text, 'lxml')
```

之后`soup` 对象中就有页面的完整信息，可以通过以下方法提取标签

- `[标签名称]` 可以提取第一次出现指定标签及其内的内容

- `find('[标签名称]', class_='[类名]')` 定位到有该属性名的标签

- `find_all('[标签名字]')` 找到符合要求的所有标签（列表）

- `select('[类/id/标签的选择器][名称]')` 找到符合要求的所有内容（列表）

  - `.` class选择器

  - `#` id选择器、

  - `>` 表示一个层级

  - 可以有层级关系，如`soup.select('.tang > ul > li > a')[0]` 取到该层级内的第一个标签，可以用一个空格表示多个层级关系

  - `string/text/get_text()` 方法都可以将标签的内容提取出来

    >  后两个可以获取该标签下所有的文本内容，可以不是直系的

  - `['[属性值]']` 获取标签内的属性值（如`href`等）

```python
import requests
from bs4 import BeautifulSoup

if __name__ == '__main__':
    headers = {
        'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/88.0.4324.182 Safari/537.36'
    }
    url = 'https://www.shicimingju.com/book/sanguoyanyi.html'
    page_text = requests.get(url, headers=headers).text.encode('ISO-8859-1')  # 防止乱码
    soup = BeautifulSoup(page_text, 'lxml')
    li_list = soup.select('.book-mulu > ul > li')
    fp = open('../result/sanguo.txt', 'w', encoding='utf-8')
    for li in li_list:
        title = li.a.string
        detail_url = 'https://www.shicimingju.com' + li.a['href']
        detail_page_text = requests.get(url=detail_url, headers=headers).text.encode('ISO-8859-1')
        detail_soup = BeautifulSoup(detail_page_text, 'lxml')
        div_tag = detail_soup.find('div', class_='chapter_content')
        content = div_tag.text
        fp.write(title+':'+content+'\n')
        print(title,'爬取成功')
```

#### xpath

是最常用且最便捷高效的解析方式，具有通用性

解析原理：

1. 实例化一个`etree`的对象，且需要将被解析的页面源码数据加载到该对象中
2. 调用`etree`对象中的`xpath`方法结合着`xpath`表达式实现标签的定位和内容的捕获

```python
from lxml import etree
tree = etree.HTML('page_text')
tree.xpath('[xpass表达式]')
```

##### xpath表达式

- 直接用`/` 分割不同层级标签，`/html/head/title`，返回的是一个列表包含所有的目标标签
- `//` 表示多个层级
- `//div[@class="song"]` 进行属性定位
- `//div[3]/a` 拿到第三个`div`标签，注意这个和列表不同，是从1开始
- `div/text()`拿到`div` 标签内的文本，但是返回的时一个列表
- `//text()` 获取目标标签下所有的文本内容
- `img/@src` 取某一个图片的地址

```python
# 58同城二手房标题爬取
from lxml import etree
import requests

if __name__ == '__main__':
    headers = {
        'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/88.0.4324.182 Safari/537.36'
    }
    url = 'https://bj.58.com/ershoufang/'
    page_text = requests.get(url, headers=headers).text
    tree = etree.HTML(page_text)
    div_list = tree.xpath('//div[@class="property"]')
    fp = open('../result/58bjtext.txt', 'w', encoding='utf-8')
    for h3 in div_list:
        h3_text = h3.xpath('.//div[@class="property-content-title"]/h3/text()')[0]
        fp.write(h3_text + '\n')
```

```python
# 爬取网站上的图片内容
from lxml import etree
import requests
import os

if __name__ == '__main__':
    headers = {
        'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/88.0.4324.182 Safari/537.36'
    }
    url = 'http://pic.netbian.com/4kdongman/'
    response = requests.get(url, headers=headers)
    # response.encoding = 'gbk'  # 防止输出乱码
    page_text = response.content  # 将原本text改成content也可防止乱码
    tree = etree.HTML(page_text)
    # 数据解析：src的属性值 alt的属性值
    li_list = tree.xpath('//div[@class="slist"]/ul/li')
    if not os.path.exists('../result/Comicpic'):
        os.mkdir('../result/Comicpic')

    for li in li_list:
        pic_src = 'http://pic.netbian.com' + li.xpath('./a/img/@src')[0]
        pic_name = li.xpath('./a/img/@alt')[0] + '.jpg'
        # pic_name = pic_name.encode('iso-8859-1').decode('gbk')  # 另一种解决乱码的通用方式
        # 请求图片进行持久化存储
        pic_data = requests.get(pic_src,headers=headers).content
        pic_path = '../result/Comicpic/' + pic_name  # 图片保存路径一定是带有图片名字的
        with open(pic_path, 'wb') as fp:
            fp.write(pic_data)  # 注意到存储图片时用的是二进制编码
            print(pic_name, '保存成功！')
```

对于目标数据存在于不同的层级中，可以使用`|` 符号表示两个路径同时作用于`xpath` ，任意一个成功的结果都会被添加到最终的列表中

```python
# 爬取站长素材里面第一页的模板素材
from lxml import etree
import requests
import os

if __name__ == '__main__':
    headers = {
        'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/88.0.4324.182 Safari/537.36'
    }
    url = 'https://sc.chinaz.com/moban/'
    main_page_text = requests.get(url, headers=headers).text
    tree = etree.HTML(main_page_text)
    model_access_href_list = tree.xpath('//*[@id="container"]/div/div/a/@href')
    download_url = []

    if not os.path.exists('../result/hw_model'):
        os.mkdir('../result/hw_model')

    for detail_url in model_access_href_list:
        detail_url = 'https:' + detail_url
        detail_page_text = requests.get(detail_url, headers=headers).content
        tree = etree.HTML(detail_page_text)
        model_name = tree.xpath('//d    iv[@class="text_wrap"]/h2/a/text()')[0] + '.rar'
        model_path = '../result/hw_model/' + model_name
        model_url = tree.xpath('//div[@class="downbody"]/div[3]/a[4]/@href')[0]
        model_data = requests.get(model_url, headers=headers).content
        with open(model_name, 'wb') as fp:
            fp.write(model_data)
            print(model_name, '保存成功')
```

注意`xpath`无法匹配到`tbody`标签

### 模拟登录

验证码是门户网站的一种反爬机制，一般存在于查看用户信息内容

- 解决方法：第三方自动识别验证码（超级鹰）

成功识别验证码之后就进行模拟登录

1. 通过抓包工具抓取单击登录按钮后发起的请求，记得勾选`Preserve log` 
2. 定位到一个`login` 的数据包
3. 可以在最后的`Form Data`看到登录的时候发送的数据
4. 快乐编程

```python
response = requests.post(url, headers=headers, data=data).text  # 向客户端发送登录请求
print(response.status_code)
# 通用的检查登录是否成功，如果成功则输出200
```

想要获取登陆后展示的个人信息，直接对`URL` 发起请求并不奏效

#### cookie

`http/https` 是一种无状态的协议，所以就算是之前通过`requests` 请求登录过了，下一次请求也不会保留上一次的登录信息

`cookie` 是用来让服务器端记录客户端的登陆状态

![image-20210224223540891](https://s2.loli.net/2021/12/05/QU4M7TvSpcJyq3s.png)

将请求头内带上这串`cookie` 就可以在请求时访问到个人主页信息

```python
headers = {
    'cookie':'xxxx'
}
detail_page_text = requests.get(url, headers=headers).text
# 可以简单的实现键入cookie值
```

考虑到`cookie`值很可能随着时间改变发生变化，所以不建议直接手动输入

事实上，`cookie` 值来源于登录的时候服务器最早发的请求中

![image-20210224225022068](https://s2.loli.net/2021/12/05/LIHjoXSiJ87qDtw.png)

#### session会话对象

- 可以进行请求的发送
- 如果请求过程中产生了cookie，则该cookie会被自动的储存/携带在该session对象中

```python
session = requests.Session()
response = session.post(url, headers=headers)
print(response.status_code)
detail_page_text = session.get(detail_url, headers=headers).text
```

可以发现，`session` 对象和`requests` 使用方法基本相同

#### 代理

防止过度访问某网站导致`ip` 信息被服务器端封掉

代理就是代理服务器，使网络信息中的中转站，可以突破自身`ip` 访问的限制，且隐藏自身真实的`ip` 

通过一些网站可以获取到代理的`ip` 

![image-20210225111258955](https://s2.loli.net/2021/12/05/fX5vzWylLp8EPme.png)

- 类型当中`http/https`分别对应其能够访问的协议类型网站
- 匿名度表示服务器是否知道本机使用了代理，高匿的话什么都不知道

```python
page_text = requests.get(url, headers=headers, proxies={'[类型]':'[ip+端口]'}).text
```

### 异步爬虫

异步是一种高性能的数据爬取，当有多个`URL` 的响应数据等待被爬取，采用单线程串行的方式显然效率十分低下

因为`get` 方法是一个阻塞的方法，只有执行完毕之后才执行别的语句

#### 多线程多进程

多线程多进程可以为相关阻塞操作单独开启线程或者进程，阻塞操作异步执行

但是无法无限制开启多线程，因为会过度消耗`cpu`资源，到头来还是影响效率（不推荐）

#### 线程池

这时候就可以用到线程/进程池，可以降低系统对进程或者线程创建和销毁的频率，从而降低系统开销

但是池中的线程和进程的数量是有上限的（适当使用）

```python
import time
from multiprocessing.dummy import Pool  # 导入线程池
def get_page(integer):
    print("Download..", integer)
    time.sleep(2)
    print("over")
start_time = time.time()
pool = Pool(4)
pool.map(get_page, range(1, 4))  # 将列表中每一个列表元素传递给get_page进行处理
# map返回值为一个列表，存储的是get_page的返回值
end_time = time.time()
print(end_time-start_time)
```

注意，线程池只处理的是阻塞且耗时的操作

#### 单线程+异步协程

##### 协程的基本概念

协程不是计算机提供的，而是程序员人为创造的，通过一个线程实现代码块相互切换执行

让协程运行两个函数，会先在第一个函数内运行一会，再在第二个函数内运行一会，切换运行

##### 实现协程的方法

- `greenlet`是早期模块
- `yield`关键字
- `asyncio`装饰器（py3.4）
- `async/await`关键字（py3.5）【主流】

##### 语法

- `event_loop`事件循环，相当于一个无限循环，可以把一些函数注册到这个事件的循环上，只有满足某些条件时，函数被循环执行
- `coroutine`协程对象，将其注册到事件循环中被调用，当我们用`async`关键字对其定义一个方法，使这个方法在调用的时候不会立刻执行，而是返回一个协程对象
- `task`对协程对象的进一步封装，包含了任务的各个状态
- `future`和`task`没有本质区别
- `async`定义一个协程
- `await`用于挂起阻塞方法的执行

```python
import asyncio


async def func():
    print(1)
    await asyncio.sleep(2)
    print(2)
    return "返回值"


async def main():
    print('开始')

    task_list = [
        asyncio.create_task(func(), name='n1'),
        asyncio.create_task(func(), name='n2')
    ]

    print('结束')

    done = await asyncio.wait(task_list, timeout=None)
    print(done)


asyncio.run(main())
#运行结果：开始 结束 1 1 2 2
```

注意，用`async`定义的协程函数实际上是一个对象，并不能直接运行

```python
import asyncio

async def request(url):
    print('正在请求的url是', url)
    print('请求成功',url)
    #async修饰的函数，调用之后返回一个协程对象
    return url

if __name__ == '__main__':

    c = request('www.baidu.com')
    # 创建一个事件循环对象
    loop = asyncio.get_event_loop()
    # 将协程对象注册到loop中，然后启动loop
    # 之后loop当中的注册的协程对象对应的函数内部的程序语句会被执行
    loop.run_until_complete(c)  # run_until_complete这个函数既能够实现注册又可以实现启动事件循环

    # task的使用，对协程对象进一步封装
    d =request('www.google.com')
    # 基于loop创建一个task对象
    task = loop.create_task(d)
    print(task)
    loop.run_until_complete(task)
    print(task)

    # future的使用，不用基于循环对象
    e = request('www.bilibili.com')
    task = asyncio.ensure_future(e)  # 和loop.creat_task本质没有区别，但不基于循环对象
    print(task)
    loop.run_until_complete(task)
    print(task)

    # 绑定回调
    def callback_func(task):  #回调函数
        # result返回的就是任务对象中封装的协程对象对应的函数的返回值
        print(task.result())
    c = request('www.baidu.com')
    task = loop.create_task(c)
    # 将回调函数绑定到任务对象中
    task.add_done_callback(callback_func)  # 将任务对象作为参数传递给回调函数（绑定）
    # 上述两行代码约等于asyncio.run()
    loop.run_until_complete(task)
```

![image-20210226161037365](https://s2.loli.net/2021/12/05/l9VRiwWxUBXHIa6.png)

以上协程的操作都是基于单任务的，只给他制定了一个协程对象，将这一个协程对象封装到了一个任务对象当中，将这一个任务对象注册到了事件循环当中，最终事件循环当中只被注册了一个事件对象

大多数情况下要注册多任务的协程对象

##### 多任务协程

```python
# 简单的多任务编程
import asyncio
import time


async def request(url):
    print('Download...', url)
    # 在异步协程中，如果出现了同步模块相关的代码，那么就无法实现异步
    # # time.sleep(2) 这不行
    await asyncio.sleep(2)
    print('over', url)

start = time.time()
urls = {
    'www.baidu.com',
    'www.sougou.com',
    'www.google.com'
}
tasks = []
for url in urls:
    c = request(url)
    tasks.append(c)

# 需要将任务列表封装到wait中
asyncio.run(asyncio.wait(tasks))
print(time.time()-start)
```

```python
# 想要进行异步多任务执行？
import asyncio
import time
import requests

start = time.time()
urls = [
    'http://127.0.0.1:5000/first',
    'http://127.0.0.1:5000/second',
    'http://127.0.0.1:5000/third'
]


async def get_page(url):
    print('正在下载')
    response = requests.get(url)
    print(response.text)

tasks = []

for url in urls:
    c = get_page(url)
    tasks.append(c)

asyncio.run(asyncio.wait(tasks))

print(time.time()-start)
```

上述代码并不能实现异步执行，原因是`requests`模块是基于同步的，如果想实现异步，必须使用基于异步的网络请求模块(aiohttp)

```python
# 附 搭建简易服务器的代码
from flask import Flask
import time

app = Flask(__name__)


@app.route('/first')
def index_first():
    time.sleep(2)
    return 'hello 1'


@app.route('/second')
def index_second():
    time.sleep(2)
    return 'hello 2'


@app.route('/third')
def index_third():
    time.sleep(2)
    return 'hello 3'


if __name__ == '__main__':
    app.run(threaded=True)

```

##### aiohttp

可以对上述代码进行修改

```python
import asyncio
import time
import aiohttp

start = time.time()
urls = [
    'http://127.0.0.1:5000/first',
    'http://127.0.0.1:5000/second',
    'http://127.0.0.1:5000/third'
]


async def get_page(url):
    async with aiohttp.ClientSession() as session:
        # get(),post():
        # headers,params/data,proxy='http://ip:port'
        async with await session.get(url) as response:
            # text()返回的是字符串形式的响应数据
            # read()返回的是二进制类型的响应数据
            # json()返回的就是json对象
            # 注意在获取响应数据操作之前一定要使用await进行手动挂起
            page_text = await response.text()
            print(page_text)

tasks = []

for url in urls:
    c = get_page(url)
    tasks.append(c)
    
asyncio.run(asyncio.wait(tasks))

print(time.time()-start)
```

可以发现，对于每个`get/post`请求前必须手动`await`挂起请求，且`aiohttp`模块和文件操作相同，使用`with..as`来接收返回参数

### selenium模块

之前当一个网页出现动态加载出来的`AJAX`请求时，我们需要通过抓包工具对其进行抓包，在搜索相关内容来确定某些信息是否为动态加载

但是有些网站比较坑，加载出来的数据超级难查，这时候就可以使用`selenium`模块来便捷地获取网站中动态加载出来的数据

同时`selenium`模块也可以便捷地实现模拟登录

#### 概念

`selenium`模块是基于浏览器自动化的一个模块

让`python`触发的动作模拟到浏览器当中

#### 使用方法

1. `pip3 install selenium`
2. 下载浏览器驱动`https://chromedriver.storage.googleapis.com/index.html`
3. 将下载的驱动拷贝到`Scripte`目录下

```python
from selenium import webdriver
from lxml import etree
from time import sleep

# 实例化一个浏览器对象
bro = webdriver.Chrome(executable_path='./Scripts/chromedriver.exe')
# 编写基于浏览器自动化的操作代码
bro.get('https://www.baidu.com')  # 让浏览器发起一个指定url对应请求
page_text = bro.page_source  # 获取浏览器当前页面的页面源码数据，包括了AJAX请求到的数据
tree = etree.HTML(page_text)  # 这次再用xpath就可以捕获到页面的动态加载的数据
search_input = bro.find_element_by_id('kw')  # 找到搜索框的标签
search_input.send_keys('python')  # 搜索内容python
bottom = bro.find_element_by_id('su')  # 找到搜索按钮
bottom.click()  # 点击搜索按钮
sleep(1)  # 程序执行太快会导致有些操作可能执行不了，要先sleep一下
bro.back()  # 后退
bro.forward()  # 前进
sleep(1)
# 我们知道，通过浏览器检查项目的Console选项通过键入js代码来实现页面滚动
# window.scrollTo(0,-document.body.scrollHeight)
bro.execute_script('window.scrollTo(0,document.body.scrollHeight)')
sleep(1)
bro.quit()  # 退出
```

有些页面会存在`iframe`标签，放置一些能拖动的`div`等，而这里面的`div`并不能够直接通过`find`方法查找到，则运用`switch_to`方法

```python
from selenium import webdriver
# 导入动作链对应的类
from selenium.webdriver import ActionChains

# 实例化一个浏览器对象
bro = webdriver.Chrome(executable_path='./Scripts/chromedriver.exe')
# 当某个标签存在于iframe标签中时
bro.switch_to.frame('[iframe的id]')  # 切换浏览器标签定位的作用域
div = bro.find_element_by_id('[iframe内的div的id]')
# 动作链
action = ActionChains(bro)  # 实例化一个动作链对象
action.click_and_hold(div)  # 点击并长按指定的标签
for i in range(5):
    # 以一次17个像素立即执行动作链操作
    action.move_by_offset(17, 0).perform()  # move_by_offset第一个为x第二个为y，perform为立即执行
    sleep(0.3)
action.release()  # 释放动作链
```

有时候浏览器的弹出十分sb，所以我们需要一个无可视化浏览器

```python
# 无头浏览器
from selenium import webdriver
from selenium.webdriver.chrome.options import Options

chrome_options = Options()
chrome_options.add_argument('headless')
chrome_options.add_argument('disable_gpu')
bro = webdriver.Chrome(executable_path='./Scripts/chromedriver.exe', chrome_options=chrome_options)
bro.get('http://www.baidu.com/')
print(bro.page_source)
```

有些网站会检测`selenium`的请求，于是我们又需要伪装

```python
# 实现检测规避
from selenium.webdriver import ChromeOptions

option = ChromeOptions()
option.add_experimental_option('excludeSwitches', ['enable-automation'])
```

#### 使用超级鹰&selenium实现模拟登录

`https://www.chaojiying.com/` 超级鹰官方网站

##### 超级鹰使用流程

1. 创建软件id
2. 开发文档页面下载示例代码
3. 价格体系页面查看验证码编号
4. 修改示例代码

##### 12306验证码

考虑到页面每刷新一次就会产生一个新的验证码，因此我们可以通过selenium对当前页面进行截图

截取到验证码所在区域再发送给超级鹰，超级鹰会返回识别的验证码坐标

```python
import requests
from hashlib import md5
from selenium import webdriver
from time import sleep
from PIL import Image  # 导入Pillow模块
from selenium.webdriver import ActionChains  # 实现点击动作

# 超级鹰官方模块
class Chaojiying_Client(object):

    def __init__(self, username, password, soft_id):
        self.username = username
        password =  password.encode('utf8')
        self.password = md5(password).hexdigest()
        self.soft_id = soft_id
        self.base_params = {
            'user': self.username,
            'pass2': self.password,
            'softid': self.soft_id,
        }
        self.headers = {
            'Connection': 'Keep-Alive',
            'User-Agent': 'Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 5.1; Trident/4.0)',
        }

    def PostPic(self, im, codetype):
        """
        im: 图片字节
        codetype: 题目类型 参考 http://www.chaojiying.com/price.html
        """
        params = {
            'codetype': codetype,
        }
        params.update(self.base_params)
        files = {'userfile': ('ccc.jpg', im)}
        r = requests.post('http://upload.chaojiying.net/Upload/Processing.php', data=params, files=files, headers=self.headers)
        return r.json()

    def ReportError(self, im_id):
        """
        im_id:报错题目的图片ID
        """
        params = {
            'id': im_id,
        }
        params.update(self.base_params)
        r = requests.post('http://upload.chaojiying.net/Upload/ReportError.php', data=params, headers=self.headers)
        return r.json()


# 主程序
bro = webdriver.Chrome(executable_path='./Scripts/chromedriver.exe')
bro.get('https://kyfw.12306.cn/otn/login/init')
# 可以设置浏览器缩放数值 bro.execute_script("document.body.style.zoom='2'")
sleep(1)  # 等待验证码图片加载
bro.save_screenshot('../result/aa.png')  # 保存全屏截图
# 确定验证码图片对应的左上角和右下角的坐标
code_img_ele = bro.find_element_by_xpath('//*[@id="loginForm"]/div/ul[2]/li[4]/div/div/div[3]/img')  # 定位验证码div位置
location = code_img_ele.location  # 验证码左上角的坐标
size = code_img_ele.size  # 验证码的长和宽
scope = (
    int(location['x'])*2, int(location['y'])*2,
    int(location['x'])*2 + int(size['width'])*2, int(location['y'])*2 + int(size['height'])*2)
# 最终验证码图片详细位置，注意根据电脑缩放率的不同需要乘以不同倍数
i = Image.open('../result/aa.png')  # 调用Pillow模块对图片进行局部截图
code_img_name = '../result/aa.png'
frame = i.crop(scope)  # 引用crop方法定位局部截图位置
frame.save(code_img_name)  # 保存局部截图

chaojiying = Chaojiying_Client('l135163642', 'yW.yyCAitQWP3mP', '913387')  # 账号密码和软件id
im = open('../result/aa.png', 'rb').read()	  # 本地图片文件路径来替换
pic_str = chaojiying.PostPic(im, 9004)  # 验证码类型9004
pic_str = pic_str['pic_str']  # 提取返回字典中的 'pic_str' 元素
# pic_str样式大概为'100,100|200,200|...'分别存储多个坐标，用|分割
# 下述代码对其进行切割变成列表[[100,100], [200,200], ...]
all_list = []
list_1 = pic_str.split('|')
for i in list_1:
    x = int(i.split(',')[0])/2
    y = int(i.split(',')[1])/2  # 注意到这里要/2保证位置精确
    all_list.append([x, y])
print(all_list)
for _ in all_list:
    x = _[0]
    y = _[1]
    ActionChains(bro).move_to_element_with_offset(code_img_ele, x, y).click().perform()  # 将光标定位到验证码div的指定坐标位置！
# 真的执行成功了啊啊啊啊啊啊啊太感动了吧
```

### scrapy框架

框架就是一个集成了很多功能并且具有很强通用性的项目模板

我们只需要了解框架封装的各种功能的详细用法

scrapy是一个爬虫中封装好的一个明星框架

1. 高性能的持久化存储
2. 异步的数据下载
3. 高性能的数据解析
4. 分布式

#### 环境配置

1. `pip3 install wheel` ，因为`scrapy`框架中异步相关的操作是基于`twisted`模块，而`twisted`模块又需要`wheel`模块支持
2. `https://www.lfd.uci.edu/~gohlke/pythonlibs/#twisted`下载`twisted`
3. 安装`twisted`模块
4. `pip3 install scrapy`安装`scrapy`框架

#### 新建一个scrapy工程

![image-20210228173511457](https://s2.loli.net/2021/12/05/mluo3KRpSz7sxHP.png)

执行成功后项目中会多出一个目录，如下图

![image-20210228173933406](https://s2.loli.net/2021/12/05/O36tZfL2AwgNyUT.png)

因此我们先要在终端中新建一个爬虫源文件

![image-20210228174330776](https://s2.loli.net/2021/12/05/D2RnxJ9NgU6Vi3F.png)

如图，通过`scrapy genspider [源文件名称] [目标网站]`来创建一个源文件（图中忘了url了）

编写好程序之后，通过`scrapy crawl [源文件名称]`来运行某个项目（进行数据爬取）

#### 进入爬虫文件

默认状态下，系统会给我们自动编写好初始代码

![image-20210228174849782](https://s2.loli.net/2021/12/05/j8rB3YEgcZyU1hD.png)

```python
# 源文件解释
import scrapy
class FirstSpider(scrapy.Spider):
    # 爬虫文件的名称，是爬虫源文件的一个唯一标识
    name = 'first'
    # 允许的域名，用来限定start_url列表中哪些url可以进行请求发送，一般不常用（已注解）
    # allowed_domains = ['www.baidu.com']
    # 起始的url列表，该列表中存放的url会被scrapy自动进行请求的发送
    start_urls = ['https://www.baidu.com/', 'https://www.sougou.com']
    # 列表里有两个url，就会发送两个请求，获得两个响应对象

    # parse方法用于数据解析，response参数表示的就是请求成功后对应的响应对象
    # 上述的两个响应对象会依次赋值给response参数
    def parse(self, response):
        print(response)  # 校验
```

对上述文件在终端中进行`scrapy crawl first`会产生一大串日志内容，但是好像并没有网站的相关信息

#### 获得第一条回应

![image-20210228190919740](https://s2.loli.net/2021/12/05/cYj2U8yhNeLxgbi.png)

定位到如图框选中的`INFO`日志，会发现配置文件中有一个`ROBOTSTXT_OBEY`值为`True`，正是因为这个原因我们没有拿到正确的响应

其实这个就是`ROBOTS`协定，也就是君子协定，爱遵守不遵守，不过你遵守了就爬不到网站内容了

所以我们果断进入`settings.py`（以下统称为配置文件）里面将它改成`False`~~（我就是小人~~

再次运行，我们得到了它

![image-20210228192052230](https://s2.loli.net/2021/12/05/mLyY8IUXMNPrKqR.png)

如果嫌乱七八糟的日志烦，可以在`scrapy crawl first`后加上`--nolog`，使得只显示打印的内容

然而这样的话程序就没有报错了，难以检查

这时候就需要在配置文件中添加`LOG_LEVEL = 'ERROR'`，则这时就算不加`--nolog`依旧不会显示除错误日志之外的别的信息

#### 数据解析

```python
import scrapy
class QiubaiSpider(scrapy.Spider):
    name = 'qiubai'
    # allowed_domains = ['www.xxx.com']
    start_urls = ['https://www.qiushibaike.com/text/']

    def parse(self, response):  # 数据解析的操作写在这
        div_list = response.xpath('//div[@class="col1 old-style-col1"]/div')
        # 在scrapy中直接通过调用提供的xpath方法实现数据解析，省去etree对象的调用
        for div in div_list:
            # author = div.xpath('./div[1]/a[2]/h2/text()')  # 这样会拿到一个Selector对象
            # extract可以将Selector对象中data参数储存的字符串提取出来
            author = div.xpath('./div[1]/a[2]/h2/text()').extract_first()
            content = div.xpath('.//a[1]/div/span//text()').extract()
            content = ''.join(content)  # join方法将列表转换成字符串
            print(author, content)
```

可以发现，大体上来说`scrapy`和之前学过的`requests + lxml `相差不多，但总体来说更加简便

#### 持久化存储

`scrapy`提供了两种持久化存储的方式，分别是基于终端指令存储和基于管道存储

##### 基于终端指令

只可以将`parse`方法的返回值存储到本地的文本文件中（数据库×）

将上述代码添加返回值，可以通过建立字典来实施

```python
all_data = []  # 存储所有解析到的数据
# for循环内
    dic = {
        'author': author,
        'content': content
    }
    all_data.append(dic)

return all_data
```

之后我们就可以在在终端中通过`scrapy crawl [项目名] -o ./[数据名称].csv`来存储返回数据

注意到基于终端指令的持久化存储类型只能为`'json', 'jsonlines', 'jl', 'csv', 'xml', 'marshal', 'pickle'`这些

这种方式比较简洁，但是局限性比较强

#####  基于管道（重要）

流程相对于基于终端比较多

1. 数据解析

2. 在`item`类中定义相关的属性

   ![image-20210228210707823](https://s2.loli.net/2021/12/05/7U4hjtSDPAomr3g.png)

   ```python
   # 要预先在items.py中封装两个对象
   author = scrapy.Field()
   content = scrapy.Field()
   ```

3. 将解析到的数据封装存储到`item`类型的对象

   ```python
   # 源文件
   item = QiushibaikeItem()
   item['author'] = author
   item['content'] = content
   
   yield item  # 将item提交给了管道
   # 每一个循环都要提交一遍管道
   ```

4. 将`item`类型的对象提交给管道`pipelines.py`进行持久化存储的操作

5. 在管道类的`process_item`中要将接收到的`item`对象中存储的数据进行持久化的存储操作

   ```python
   # pipellines.py文件
   class QiushibaikePipeline(object):
       fp = None
       def open_spider(self, spider):  # 相当于__init__
           print('开始爬虫')
           self.fp = open('./qiubai.txt', 'w', encoding='utf-8')
   
       # 专门用来处理item类型对象的方法
       # 该方法只能接受爬虫文件提交过来的item对象
       def process_item(self, item, spider):
           author = item['author']
           content = item['content']
           self.fp.write(author+':'+content+'\n')
           return item
   
       def close_spider(self, spider):  # 管道结束时执行的方法
           print('结束爬虫')
           self.fp.close()
   ```

6. 在配置文件中开启管道（默认不开启）

   ```python
   # settings.py文件
   ITEM_PIPELINES = {
      'qiushibaike.pipelines.QiushibaikePipeline': 300,  # 300表示优先级，数值越小优先级越高
   }
   ```

有时候会遇到匿名用户无法显示名称，则用`|`表达式再连接一个`xpath`表达式，因为匿名用户在不一样的标签中

同时我们可以发现，配置文件中的优先级指的好像就是管道文件中的类，所以我们可以在管道文件中再创建一个类用于别的存储，参考上述的类定义方法，每一个类对应的就是将数据存储到的一种平台

定义好一个类之后我们可以在配置文件中添加管道并定义优先级，之后执行爬虫文件时管道文件就会根据优先级的顺序执行各类

同时，爬虫文件提交的`item`只会给管道文件中的第一个被执行的管道类接受

事实上，管道类中的`return item`会将本类中的`item`信息作为参数传递到下一个次于它优先级的类，如果想要将某一组数据存在的`item`同时存放不同文件中，必须在类结尾加上`return item`

#### 手动请求发送

对于多页爬取内容，可以先建立一个`URL`模板，添加页码内容后手动请求

```python
url_model = 'xxx'  
page_num = 1   # 在parse方法外

new_url = format(self.url_model % self.page_num)
self.page_num += 1
yield scrapy.Request(url=new_url, callback=self.parse())  # 请求完之后回调parse方法
```

#### 五大核心组件

五大核心组件就是调度器，引擎，管道，Spider，下载器

- Spider
  - 产生`URL`，封装成请求对象发送给引擎，引擎再发送给调度器
  - 接受引擎发送的`response`数据，传递给`parse`方法进行解析数据
- 将解析好的数据封装成`item`对象，交付给管道
- 调度器由两个部分组成
  - 过滤器，将引擎提交的请求对象进行去重
  - 队列，过滤器处理好的请求对象全部放到队列
  - 调度器从队列当中调度请求对象给引擎，引擎再交给下载器
- 下载器
  - 将收到的请求对象发送给互联网来下载数据
  - 接受互联网返回的`response`发送给引擎
  - `twisted`异步模块就在下载器内使用
- 引擎
  - 进行数据流处理
  - 根据判断接收到的数据流来触发相应的事物（对象实例化，执行方法）
- 管道就是应用于持久化存储

#### 请求传参

如果爬取的要解析的数据不在同一张页面中，就需要使用到请求传参（详情页中的数据）

请求传参和管道持久化存储相关

```python
def parse(self, response):
    # 对主页列表信息进行爬取
    li_list = response.xpath('...')
    for li in li_list:
        item = QiushibaikeItem()
        name = li.xpath('...')
        item['name'] = name
        # 获取到子页面的url
        detail_url = '...' + li.xpath('...')
        # 对详情页请求获取详情页的页面源码数据（手动请求发送）
        # 这时需要用到请求传参，因为回调函数是另一个方法，item对象作为局部变量无法实时更新
        # 请求传参：meta={}，可以将meta字典传递给请求对应的回调函数
        yield scrapy.Request(detail_url, callback=self.parse_detail, meta={'item': item})
     # 分页操作
        
def parse_detail(self, response):
    item = response.meta['item']
    # 获取详情页的数据
    desc = response.xpath('...')
    desc = ''.join(desc)
    item['desc'] = desc
    # 传递给管道
    yield item
```

#### 图片爬取

对于字符串数据，只需要基于`xpath`进行解析然后提交到管道进行持久化存储

而对于图片数据，`xpath`只能解析出图片的`src`的属性值，然后单独对图片地址发起请求来获取图片二进制类型的数据

`scrapy`提供了一个管道类`ImagePipeLine`来方便的爬取图片

我们只需要获得`src`然后提交到这个管道，它就会自动对图片的`src`进行请求发送获得二进制数据并且进行持久化存储

##### 图片软属性

当我们对站长素材中的图片进行爬取的时候，会发现除了当前页面中显示的图片`img`以外，其他的图片`img`标签都没有`src`属性，而变成了`src2`

其实这是一种图片的反爬机制，可以动态的使在浏览器中可视化界面的图片动态修改其`src`名称

对于我们发送的`request`请求，并没有可视化的界面，通过直接定位`src`标签自然无法取得图片内容

##### 代码部分

下面以爬取站长素材的图片为例

```python
# spider文件代码
import scrapy
from imgsPro.items import ImgsproItem

class ImgSpider(scrapy.Spider):
    name = 'img'
    # allowed_domains = ['www.xxx.com']
    start_urls = ['https://sc.chinaz.com/tupian/']

    def parse(self, response):
        div_list = response.xpath('//div[@id="container"]/div')
        for div in div_list:
            # src = div.xpath('./div/a/img/@src').extract_first()  # 会发现这样并不能爬到数据
            src = 'https:' + div.xpath('./div/a/img/@src2').extract_first()
            src = src.split('_')[0] + '.jpg'  # 会发现原始图片为缩略图，进行处理后才是高清图
            item = ImgsproItem()
            item['src'] = src
            yield item
```

```python
# 管道文件代码

# class ImgsproPipeline:
#     def process_item(self, item, spider):
#         return item  # 只爬取图片的话并不需要这个类，直接注释掉

from scrapy.pipelines.images import ImagesPipeline  # 导入模块自带的图片处理管道
import scrapy
class ImgsPileLine(ImagesPipeline):  # 创建一个子类
    # 重写父类的的三个方法

    # 这个方法可以根据图片地址进行图片数据的请求
    def get_media_requests(self, item, info):
        yield scrapy.Request(item['src'])  # 不需要进行图片解析，所以不用callback

    # 指定图片存储的路径
    def file_path(self, request, response=None, info=None, *, item=None):
        imgName = request.url.split('/')[-1]
        return imgName

    # 将item返回给下一个即将被执行的管道类
    def item_completed(self, results, item, info):
        return item
```

```python
# 配置文件代码
IMAGES_STORE = './imgs'  # 指定图片存储路径
# 记得还要开启并修改管道类的名称和UA伪装
```

#### 中间件

在引擎和下载器/spider之间都有中间件，分别叫做下载中间件和爬虫中间件

`scrapy`内的中间件类都在`middlewares.py`的文件中，下称为中间件文件

其中封装了两个方法，分别对应着下载中间件和爬虫中间件

下载中间件可以拦截到整个工程中所有的请求对象和响应对象

在中间件文件中，对于下载中间件，我们需要重点看到`process`开头的三个方法，对应上述两个拦截功能

- 拦截请求作用

  - UA伪装，和在设置中进行的（全局）是不同的，这次UA伪装只针对某一次请求
  - 代理IP，可以给每一个请求设定不同的IP

  ```python
  # 拦截请求的两个方法
  # 拦截正常的请求
  def process_request(self, request, spider):
      # UA伪装，其实也可以放在异常处理中，但是不推荐
      request.headers['User-Agent'] = random.choice(self.user_agent_list)
      return None
  
  # 拦截发生异常的请求
      def process_exception(self, request, exception, spider):
          # 代理，也可以放在正常请求里面，但是会影响效率
          if request.url.split(':')[0] == 'http':
              request.meta['proxy'] = 'http://ip:port'
          else:
              request.meta['proxy'] = 'https://ip:port'
          # 将修订之后的请求对象重新发送
          return request
  ```

- 拦截响应作用

  - 篡改响应数据和响应对象（动态加载元素）

  拦截响应数据可以作用于当我们想爬取某个详情页中动态加载的数据

  ```python
  # spider文件代码
  class MiddleSpider(scrapy.Spider):
      name = 'middle'
      allowed_domains = ['www.xxx.com']
      start_urls = ['http://www.xxx.com/']
      def __init__(self):
          self.bro = webdriver.Chrome(executable_path='')  # 实例化一个浏览器对象
      def parse_model(self, response):  # 处理详情页内的响应数据（包含动态加载的数据）
          div_list = response.xpath('...')
          for div in div_list:
              title = div.xpath('...')
              ...
      def close(self, spider, reason):  # 爬虫结束之后执行的方法
          self.bro.quit()
  ```

  ```python
  # 中间件文件代码
  import random
  from scrapy.http import HtmlResponse  # scrapy给我们封装好的响应对象类型
  from time import sleep
  # 该方法拦截所有响应
  # response就是拦截到的响应对象，request就是拦截到该响应对象所对应的请求，spider表示爬虫文件中的内容！
  def process_response(self, request, response, spider):
      bro = spider.bro  # 获取了在爬虫类中定义的爬虫对象
      # 挑选出指定的响应对象进行篡改
      # 通过url定位到request
      # 通过request对应到相应的response
      if request.url in spider.models_urls:   # models_urls是爬虫文件中前往详情页的url列表，是Spider类中的一个属性！
          # 获得的response就是我们需要的响应对象，我们对其篡改
          # 实例化一个新的响应对象，替代原来旧的响应对象
          # 可以通过selenium便捷获取动态加载数据，但是不能写在该方法内，因为只需要实例化一个对象
          # HtmlResponse(url, body, encoding, request)
          bro.get(request.url)  # 重新发送详情页对应的请求
          sleep(2)
          page_text = bro.page_source  # 包含了动态加载的响应数据
          new_response = HtmlResponse(url=request.url, body=page_text, encoding='utf-8',request=request)
          return new_response
      else:
          return response
  ```

  注意`scrapy`内部请求是基于异步的，所以不用考虑异步代码

#### CrawlSpider

`CrawlSpider`是`Spider`的一个子类，专门应用于全站数据爬取

![image-20210304190732683](https://s2.loli.net/2021/12/05/nWqmN4jAMhZU3Kk.png)

会发现之前创建的`spider`文件的父类都是`Spider`，现在我们可以考虑用`CrawlSpider`

##### 初始化操作

想要创建源文件时自动定义父类为`CrawlSpider`，需要使用代码

```
scrapy genspider -t crawl [爬虫名称] www.xxx.com
```

![image-20210304193858296](https://s2.loli.net/2021/12/05/8cSGU6ODnmYd2bC.png)

链接提取器可以根据制定规则进行指定链接的提取

其中链接提取器`allow`后面单引号内的是一个正则表达式，用来捕捉相关的标签内容

注意到正则表达式甚至可以只写相关链接的一部分，整条链接也会被直接提取出来

规则解析器就将链接提取器提取到的链接进行指定规则（callback）的解析操作

会发现比如单纯的提取第一页的页码信息是有限的，理想状态应该是跳转不同界面进行页码提取

这时候就需要用到`Rule`内的`follow`参数，把他改成`True`即可（可能会被封ip）

> `follow=True`可以将链接提取器继续作用到链接提取器提取到的链接所对应的页面中
>
> 其中重复的内容会被调度器过滤掉

##### 案例操作

```python
# 源文件中
rom scrapy.linkextractors import LinkExtractor
from scrapy.spiders import CrawlSpider, Rule
from crawlspidertest.items import CrawlspidertestItem, DetailItem


class SunSpider(CrawlSpider):
    name = 'sun'
    allowed_domains = ['www.xxx.com']
    start_urls = ['http://www.xxx.com/']
    link = LinkExtractor(allow=r'...')  # 页码信息
    link_detail = LinkExtractor(allow=r'...')  #详情页信息
    rules = (
        Rule(link, callback='parse_item', follow=True),
        Rule(link_detail, callback='parse_detail')  # 默认follow为False
    )

    # 因为没有手动请求操作，自然不能请求传参，所以我们在items文件中额外封装一个item方法用于不同页面二点数据解析的数据封装
    def parse_item(self, response):
        ...
        item = CrawlspidertestItem()
        item['...'] = ...
        yield item

    def parse_detail(self, response):
        ...
        item = DetailItem()
        item['...'] = ...
        yield item
```

因为异步爬虫请求的返回是随机的，我们应该对最终存储数据进行分类

```python
# 管道文件中
class CrawlspidertestPipeline:

    def process_item(self, item, spider):
        if item.__class__.__name__ == 'DetailItem':  # 检测item的类型便于持久化存储
            ...
        else:
            ...
        return item
```

#### 分布式爬虫

分布式爬虫就是搭建一个机群，让其对同一组资源进行分布联合爬取

需要下载`scrapy-redis`组件，因为原生的`scrapy`无法实现分布式

事实上，分布式实现的可能就是调度器的实时共享，并汇总到同一个共享管道中

实现流程：

1. 创建一个工程

2. 创建一个基于CrawlSpider的爬虫文件

3. 修改当前的爬虫文件

   1. 在源文件中`from scrapy_redis.spiders import RedisCrawlSpider`
   2. 将`start_urls`改成`redis_key = ‘[可以被共享的调度器队列的名称]’`
   3. 编写数据解析相关的操作
   4. 将当前爬虫类的父类修改成`RedisCrawlSpider`

4. 修改配置未见

   1. 指定使用可以被共享的管道

      ```python
      ITEM_PIPELINES = {
          'scrapy_redis.pipelines.RedisPipeline': 400
      }
      ```

   2. 指定调度器

      ```python
      # 封装好的过滤器
      DUPEFILTER_CLASS = ‘scrapy_redis.dupefilter.RFPDupeFilter'
      # 封装好的调度器
      SCHEDULER = 'scrapy_redis.scheduler.Scheduler'
      # 某一台机器出现问题了可以从没有爬过的数据开始爬
      SCHEDULER_PERSIST = True
      ```

   3. 指定`redis`服务器

      ```python
      REDIS_HOST = ‘127.0.0.1’  # 最好是redis远程服务器的ip
      REDIS_PORT = [端口]
      ```

5. `redis`相关操作配置

   1. 配置`redis`的配置文件（`.conf`后缀文件）
      1. 删除`bind 127.0.0.1`
      2. 关闭保护模式：`protected-mode: no`
   2. 结合着配置文件开启`redis`服务
   3. 启动客户端`./redis-cli`

6. 执行工程

   1. `scrapy runspider [源文件]`

   2. 任何一个服务器向调度器的队列中放入一个起始`url`

      1. `lpush xxx www.*.com`在之前启动客户端的终端中

         > 其中xxx就是之前`redis_key`的内容

#### 增量式爬虫

只会爬取新增加的数据信息，之前爬过的数据不会再爬取

可以使用`redis`的`sadd`方法来判断某一`url`是否被爬取过

```python
from redis import Redis
conn = Redis(host='127.0.0.1', port=...)
def parse_item(self, response)
	ex = self.conn.sadd('urls', detail_url)
    if ex ==1:  # 说明该数据没有被爬取过
       	pass
    else:
        pass
```

会发现其实这样的增量式爬虫第二次还是会重新爬取所有网站进行检测，实际上效率不是很高
