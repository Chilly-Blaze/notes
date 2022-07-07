# Linux

## 代码

-  `ctrl+c` 退出当前命令
-  `ctrl+l` 清屏
-  `ls` 显示此目录的文件
-  `-al` 所有信息

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
    >  global num				#调用全局变量num
    >  num = 1					#改变全局变量
    >  num_1 += 1				#不改变全局变量
    >  _list += _list			#在全局变量列表末尾追加一个自己
    >  _list = _list + _list		#重新定义一个局部_list变量，不改变全局变量
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
  > pass
  > if __name__ == "__main__":
  > main()
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
>  def __init__(self, image_name, speedy=1.0, speedx=0):	#增加方向轴属性
>      super().__init__()
>      self.speedy = speedy
>      self.speedx = speedx
>  def update(self, *args, **kwargs) -> None:
>      self.rect.y += self.speedy
>      self.rect.x += self.speedx
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

# JavaSE

## 简介

### 三个名词

JDK：Java开发者工具，在JRE基础上添加了很多工具，包含JRE

JRE：Java运行时环境，有它就可以运行程序，但是要开发程序必须要有JDK

JVM：Java虚拟机，属于JRE，在电脑上模拟了一个小cpu，等于一个小的虚拟机，用它才能实现Java的跨平台

> Write once,run anywhere

### 安装

1. `https://www.oracle.com/java/technologies/javase-downloads.html`下载JDK
2. 直接安装
3. （*可能不用）添加环境变量
   1. 进入`Java`目录
   2. `bin\jlink.exe --module-path jmods --add-modules java.desktop --output jre`生成jre文件夹
   3. 新建系统变量![image-20210307115419394](https://s2.loli.net/2021/12/05/KIgS9Dm8haRxcFi.png)
   4. 新建PATH变量![image-20210307115459215](https://s2.loli.net/2021/12/05/NVHFIj6wyUhR7td.png)
4. 安装目录内`bin`目录存放各种 `.exe`文件，用于运行Java文件
5. `include`目录引用了一些`c`的头文件
6. `lib`目录放了一些Java的库文件
7. `lib`里面还有个`src.zip`存放Java的所有类源代码

### 卸载

1. 删除Java安装目录
2. 删除JAVA_HOME环境变量
3. 删除PATH内有关JAVA的目录
4. `java -version`查看Java版本信息，检查是否删除成功

### 编译型&解释型

**Java语言是结合了编译语言和解释语言**

`.java`文件通过编译器（Javac）预编译变成了`.class`文件，这种`.class`文件介于机器码和Java源代码之间（字节码）

当`.class`文件运行的时候会走到JVM虚拟机的类装载器中，对其中的字节码进行校验，看看写的对不对

如果都是对的，就把这个代码交给解释器，解释完后给操作系统平台

## 简单的开始

### 默认类创建时所需

```java
public class Hello{
    public static void main(String[] args){
        System.out.println("Hello,World!");
    }
}
```

> 在IDEA中，只需要输入`psvm`就可以快速创建`main`方法
>
> 而输入`i.sout`就可以直接`System.out.println(i)`

### 执行第一个Java程序

```cmd
javac Hello.java # 编译Java文件
java Hello # 执行Java的class文件，但注意不要加后缀class
```

![image-20210307115814933](https://s2.loli.net/2021/12/05/2GNvK4YMJatLAdy.png)

### Warning

1. Java大小写敏感
2. 尽量使用英文
3. 文件名和类名必须保证一致，并且首字母大写
4. 符号不能使用中文

### 在IDEA中新建一个空项目

1. 文件→新建→项目，并在弹出页面中选择**空项目**
2. 文件→新建→新模块，选择Java模块并设置名字
3. 文件→项目结构，在项目一栏中的SDK中选择自己的Java版本，并在项目语言级别中同样选择自己的Java版本
4. 在创建好的新模块下的`src`目录中创建一个Java类文件
5. 愉快的编写代码

> IDEA优化&有趣的代码注释

### 类型和运算

- `//`单行注释

- `/*   */`多行注释

- `/**   */`文档注释，内部可以通过`@`加内容

- 数据类型（Java是一种强类型语言，所有变量都应该先定义后才能使用）

  - 在定义的时候必须直接定义内容

  - `byte/short/int/long`都是整数类型，`long`类型后面要加一个`L`

    - 整数类型前`0b`表示二进制，`0`是八进制，`0x`是十六进制

    - 数字之间可以加下划线，不影响输出

    - ```java
      int i = 10_0000_0000
      int j = 20
      long total = i * j
      ```

      如果输出会发现输出了一个负数，实际上`i*j`作为`int`计算完之后再进行转换

      ```java
      long total = i * (long)j
      ```

      这样就可以正确输出

    - 除了`long`类型，其他整数类型相互运算结果都是`int`类型

  - `float/double`则是浮点类型，`float`类型后面要加`F`

    - **不要使用浮点数进行比较**
    - 银行业务可以用别的类，反正不要用浮点

  - `char`是字符型，可以包含一个字符

    - `’\u0x‘`表示unicode的一个编码

  - `boolean`是布尔类型
  - `String`**不是关键字**，因为它以大写开头，其实是一个类，不属于基本数据类型
    
    - 拼接字符串直接`+`
  - 所有的关键字的如果大写首字母就变成一个类，可以看到这个关键字的基本信息
  - 在前面使用`([基本类型])`可以强制类型转换，但是当类型从低容量转换到高容量时，自动就可以转换了，布尔类型不能转换

- 变量类型

  - 实例变量，在某个方法外，等于是一个类的属性，不初始化内容就是默认值（`0/0.0/\u0000/false/null`）

  - 局部变量，一定要有初始值，在某个方法内

  - 类变量，在变量前加`static`修饰符，不是类的属性了，而是这个类当中的全局变量

    > 加了修饰符之后会对后面的变量产生一定的效果，修饰符不分前后

  - `final` 加在原本变量之前来定义一个常量，常量建议全部大写字母+下划线

- 运算符和`C`语言都一样

- `Math.pow([数字],[几次])`幂运算

### 包机制

包实际上就是一个文件夹

一般使用公司的域名倒置作为包的名称（com.baidu.www）

如上所示创建一个包之后，会发现递归创建了三个文件夹，我们把所需的各个网站内容分别装在不同的文件夹中

在类的最上边要明示包名

```java
package com.baidu.www;
```

正因如此，`src`目录下第一个文件夹往往是`com`

`Ctrl + [点击包名]`可以跳转到某个包的路径

在某个Java文件中要使用别的包的内容，且用的内容存在歧义（如好多个包中都有`Date`这个方法），就需要使用`import`进行导包

且`import`导入的包不能和本文件的类名称相同

> - 阿里巴巴开发手册

### JavaDoc

#### 概要

JavaDoc是用来生成自己的API文档的，需要使用文档注释

注释中的参数信息

- `@author [作者名]`
- `@version [版本号]`
- `@since [需要最早使用的jdk版本]`
- `@param [参数名]`
- `@return [返回值情况]`
- `@throws [异常抛出情况]`

要给某个类做注释就要加在那个类**上面**

#### 生成自己的JavaDoc文档

之后在命令行内可以查看某个Java文件的JavaDoc

```bash
javadoc -encoding UTF-8 -charset UTF-8 [.java文件名]
```

之后会出现一个`index.html`，进入后会出现该类的详细文档说明

### 流程控制

#### 利用Scanner对象实现人机交互

```java 
Scanner scanner = new Scanner(System.in);
// 创建一个scanner对象，使用System.in接收用户的输入，并封装成scanner对象
// 可以通过new Scanner(System.in)然后按Alt + Enter快速生成对象
if (scanner.hasNext()){
    // 如果用户还有输入，就使用next方法接收
    String str = scanner.next();  // 使用scanner接收用户的输入
    // nextLine()也可以接收，可以忽略输入时候的空格
}
// 所有IO流的类如果不关闭就会一直占用资源，用完scanner就要关掉
scanner.close();
```

事实上上述代码的判断语句可以删除，依旧可以输入一个内容，但是一般来说要经过一个判断来判定用户是否输入了正确的类型

```java
Scanner scanner = new Scanner(System.in);
if (scanner.hasNextInt()){
    int i = scanner.nextInt();
    System.out.println(i);
}
else {
    System.out.println("请输入整数");
}
scanner.close();
```

#### 各种基本结构

**顺序结构**就是Java代码正常情况下从上往下依次执行

**判断结构**就是`if/else`或`switch/case`语句，和`C`语言没啥区别

> 注意`case`穿透现象，当某一个`case`判断成功后，没有`break`的情况时，会把后面每一个`case`内容都执行一遍
>
> > `JDK7`之后，`case`语句支持字符串的判定了，我们可以通过项目管理里查找到编译后的`.class`文件
> >
> > ![image-20210309180041704](https://s2.loli.net/2021/12/05/9pEiHo4ehSVmcnG.png)
> >
> > 将`.class`文件直接拷到`.java`文件的目录内，通过`IDEA`打开，可以获得`.class`文件的反编译代码
> >
> > 会发现`case`语句处理字符串时，使用了其中的`.hashCode`方法生成哈希值来判定
> >
> > ![image-20210309181447344](https://s2.loli.net/2021/12/05/fvFsT9jKaAoI7qN.png)

**循环结构**也和`C`语言没什么不同，就是`while/do..while/for`语句

> 通过`fori`快速生成一个递增循环
>
> 通过`100.for`来快速生成一个循环100次的`for`语句，而`100.forr`可以快速生成一个递减循环
>
> `break`和`contiune`也和`C`语言一样

- 增强型`For`循环，实际上和`python`中的`for`循环差不多

  ```java
  int[] numbers = {1,2,3,4};
  for (int x:numbers){
      // == for x in numbers
      // 循环语句
  }
  // 可以直接通过numbers.for来快速生成一个进阶for循环
  ```

- 循环体中标签的使用

  ```java
  outer:for (int i = 0; i<10; i++){
      for (int j = 0; j<10; j++){
          continue outer;
          // 跳转到第一个for循环
      }
  }
  ```

### 方法

方法的基本格式

```java
public static void main(String[] args){
    return [返回值]
}
// [修饰符] [返回类型] [方法名([参数类型] [参数名])]{}
```

方法约等于函数，因为Java面向对象所以函数的模式被淡化了

#### 方法重载

只需要方法的参数不同，方法可以用同一个名字，编译器会自动识别用哪一个方法，这就是方法重载

```java
public class Demo3 {
    public static void main(String[] args) {
        int i = max(10,20);
        double j = max(10,20);
        System.out.print(i+" "+j);
    }

    public static int max(int a, int b){
        return a>b?a:b;
    }
    public static double max(double a, double b){
        return a>b?a:b;
    }
}

```

#### 命令行传参

当我们在命令行使用`java [文件名]` 执行某一个`class`文件时，可以在后面加若干个参数，会根据空格作为分割通过字符串的方式传递给`main`方法的`args`字符串数组

```java
// 输出args数组内的内容
public class Demo4 {
    public static void main(String[] args) {
        int j = 0;
        for (String i:args){
            j++;
            System.out.println(j+""+i);
        }
    }
}
```

#### 可变传参

在某个形参定义时类型的后面加`...`可以传递任意参数，等于`python`中的`*args`

事实上就是把某个类型变成了一个数组，传递的参数变成了数组中的值

```java
public class Demo5 {
    public static void main(String[] args) {
        test(1,2,3,4,5);
    }
    public static void test(int... i){
        for (int j:i){
            System.out.println(j);
        }
    }
}
```

注意可变传参的参数必须在形参的最后一个

### 数组

数组可以用两种方式定义

```java
int[] nums1;
int num2[];  // 不推荐
num1 = new int[10]  // 定义数组长度，每个元素赋默认值0
```

可以通过`.length`方法获取数据长度

事实上，Java通过堆和栈的共同作用来定义一个数组

![image-20210310180005509](https://s2.loli.net/2021/12/05/5B6RQdj14ClmMEP.png "关于堆和栈的理解")

会发现命名在栈中完成，开辟空间在堆中完成，赋值就在堆中的空间中执行

同时，通过`new`创建的变量属于动态初始化，直接在变量后`= [值]`叫做静态初始化，动态初始化包含默认初始化

```java
Man[] mans = {new Man(1,1), new Man(2,2)};  // 静态初始化,Man时另一个文件中的一个类，本质就是创建+初始化
int[] int1 = new int[10];  // 动态初始化，每个元素赋默认值
```

#### Arrays类

`Arrays`类是系统封装的一个用于操作数组的类

- `sort`对数组进行排序
- `toString`变成带中括号的字符串
- `fill(*,[起始],[结束],[填充内容])`将指定内容填充数组的每一个元素
- 其他的方法建议通过帮助文档查看

#### 稀疏数组

有些时候某个数组的大多数元素的值都是默认值0，反而占用大量空间，这时候就可以用我们的稀疏数组

比如棋盘的内容，我们就可以用另一个简单的$3*n$二维数组来保存

- `a[0]`保存这个棋盘的大小`a[1/2/3]`分别是行、列、元素个数
- 从`a[1]`开始，每一行保存元素所在位置和所在位置的值

### 面向对象编程(OOP)

#### 方法的调用

当在某一个方法前面加`static`就将一个方法变成静态方法，在别的程序中可以直接通过`[类名].[方法名]`来调用

不加`static`的方法就是非静态方法，必须先通过`new`实例化一个对象，再通过这个对象调用其中的方法

`static`方法是和类一起加载的，而非静态方法是类的实例化，在类创建完之后加载，因此不能在`static`方法中调用另一个不是`static`修饰的方法

#### 构造器

类中的构造器也称为构造方法，是在进行创建对象的时候必须要调用的，他有两个特点

- 必须和类的名字相同
- 必须没有返回类型，也不能写viod

就算我们只单纯定义一个类，编译的时候也会自动创建一个构造器

相当于`python`中的`__init__`方法

如果要给构造器传递参数，就要用有参构造，不过注意如果定义了有参构造，无参构造必须显示

```java
public class Test {
    String name;
    public Test() {
        // 有参构造必须创建一个空的无参构造
    }
    public Test(String name){   // 有参构造
        this.name = name;  // this等于python中的self
    }
}
```

有参构造的方法也可以同名但是参数不同，系统会自动识别

`Alt+insert`可以自动生成无参/有参构造器

#### 封装

程序设计要追求**“高内聚，低耦合”**，类的内部数据操作细节自己完成，不允许外部干涉，仅暴露少量方法提供给外部使用

通常，应禁止直接访问一个对象中数据的实际表示，而应通过操作接口来访问，这称为**信息隐藏**

要实现属性私有，就要使用`private`修饰符，外部想要访问到某个私有属性，我们可以提供一个`get`方法

![image-20210310205049211](https://s2.loli.net/2021/12/05/3vqnjNwSJ6bAYMG.png)

如图，系统会自动生成一个`get`方法，里面自动`return`了私有属性`name`

外部想要设置某一个属性，同样如图设定一个`set`方法

```java
public class Test {
    private String name;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```

`Alt+insert`可以自动生成`get/set`方法

通过`get/set`方法可以有效规避不法分子乱定义属性，我们只需要在`get/set`方法内判断并抛出异常

#### 继承

在某一个类名后`extends [父类]`就可以继承一个父类，注意Java没有多继承

使用`super`代替`this`可以访问父类的方法/属性

子类不能继承父类的私有属性/方法，甚至使用`super`也不行

在子类的界面中按下`Ctrl+H`可以看到继承完整树

事实上，和`python`相同，在Java中，所有的类都默认继承`object`类

同时注意子类的无参构造中会自动执行父类的无参构造，隐藏了`super()`这一行代码

使用`super/this()`可以直接执行构造器方法，不过必须放在方法的第一行（所以两个方法不能同时调用）

![image-20210311182200630](https://s2.loli.net/2021/12/05/JEvoQmO8rKBGnNh.png)

上图可以发现，存在继承关系时，子类可以重写父类的方法，不过注意

- 重写的方法名必须相同
- 重写的餐宿列表必须相同（不然就是重载）
- 重写时修饰符可以扩大但不能缩小（`public>protected>default（默认）>privite`）
- 抛出的异常可以被缩小但不能被扩大
- `static`方法属于类不属于生成的对象，不能被重写
- `final`方法无法改变也不能重写，甚至不能有子类
- `private`方法也不能重写

#### 多态

看上图，`new`后面是指向，前面的是引用类型

```java
B b = new A();
// [引用] [对象名] = new [类型名]
```

一个对象的指向是确定的，但是引用类型不确定，父类的引用可以指向子类

子类重写的父类的方法，上述代码执行子类的方法

父类的引用不能调用非重写子类的方法，也就是能执行的方法看左边的引用，但执行效果需要看右边

如果强行要让父类类型执行子类方法，需要强制类型转换`((A)b).test`

要看某个类是否是另一个类的子类，需要用`instanceof`关键字

```java
// Object > String
// Object > Test
Test test = new Test();
Object object = test;  // 可以直接转换为父类
System.out.println(object instanceof Test);  // True
System.out.println(object instanceof Object);  // True
System.out.println(object instanceof String);  // False
System.out.println(test instanceof String);  // 会报错，他们俩没有半毛钱关系
```

子类虽然能直接转换为父类，但是可能丢失一些方法，父类转子类用强制转换，才能调用子类未重写的方法

#### Static关键字详解

![image-20210311193138594](https://s2.loli.net/2021/12/05/C8Z37Jy2HTz6hnF.png "创建一个类时各方法的执行顺序")

可以发现`static`方法永远位于第一个执行，和类一起加载，然后通过`main`方法新建一个类后，先执行匿名代码块（成员变量）内容，再执行构造方法

通过静态导入包，可以快捷直接访问某个包内的方法

```java
package com.mine.oopdemo;
import static java.lang.Math.random;

public class Demo2 {
    public static void main(String[] args) {
        System.out.println(random());
    }
}
```

#### 抽象类

![image-20210311205410993](https://s2.loli.net/2021/12/05/HS6e98cBGbm4lFu.png)

抽象类由于单继承的局限性，用到的情况不是很多，不过还是要注意

- 抽象类不能被`new`出来，只能靠子类去实现它

- 抽象类里可以写普通方法，但是抽象方法不能写在普通类中

#### 接口

接口什么都没有，自己甚至无法写方法，比抽象类还要抽象，是专业的约束

面对大的项目的时候，我们要学会面向接口编程，由架构师整理出大的框架再由码农进行方法设计

接口就是规范，像法律一样，定义好了之后大家都要遵守

![image-20210311213956059](https://s2.loli.net/2021/12/05/zg4JVtkG7OwrlKj.png "不同的图标样式")

```java
// 接口定义

// interface定义的关键字就是接口，接口都需要有实现类
public interface Demo5 {
    // 接口定义的属性都是常量，默认public static final
    int AGE = 100;
    // 接口中的所有定义其实都是抽象的，默认public abstract
    void add(String name);
    void delete(String name);
    void update(String name);
    void query(String name);
}
```

```java
// 实现类

// 接口的实现类一般名字以Impl结尾
// 类可以实现接口，通过implements关键字，可以通过逗号分隔用来继承多个接口
// 实现了接口中的类，就需要重写接口中的方法
public class Demo5Impl implements Demo5{

    @Override
    public void add(String name) {

    }

    @Override
    public void delete(String name) {

    }

    @Override
    public void update(String name) {

    }

    @Override
    public void query(String name) {

    }

}
```

#### 内部类

```java
public class Demo6 {
    private int id;
    public void out(){
        System.out.println("外部类的方法");
    }
    
    public class Inner{
        public void in(){
            // 内部类可以获得外部类的私有属性/方法
            System.out.println(id);
        }
    }
    
    // 另外方法中也可以定义一个类，叫做局部内部类

    public static void main(String[] args) {
        Demo6 demo6 = new Demo6();
        Inner inner = demo6.new Inner();  // 如何定义一个内部类
    }
}
```

### 异常机制

当程序运行中出现了编译之外的错误，程序就会自动抛出异常

异常可以分为三类

- 检查性异常，用户错误或问题引起的异常，程序员无法预见，在编译时无法被简单的忽略，比如打开不存在的文件
- 运行时异常，可能被程序员避免，可以在编译时被忽略，比如递归调用
- 错误（ERROR），不是异常，时脱离程序员控制的问题，在代码中通常被忽略，比如栈溢出

Java中可以把异常当作一个对象来处理，制定了一个异常体系结构，并定义了一个基类`java.lang.Throwable`作为所有异常的超类

其中又分为两个大类，错误（Error）和异常（Exception）

![img](https://ss1.bdstatic.com/70cFuXSh_Q1YnxGkpoWK1HF6hhy/it/u=3365527833,3762210150&fm=26&gp=0.jpg)

另外，`Error`类对象是由Java虚拟机生成并抛出，大多数错误与代码编写者所执行的操作无关，这些异常发生的时候，Java虚拟机（JVM）就直接终止了

`RuntimeException`属于运行时异常，程序应该从逻辑角度尽可能避免这些异常的发生

```java
public class Demo1 {
    public static void main(String[] args) {
        int a = 1;
        int b = 0;
        if (b == 0){
            throw new ArithmeticException();  // 主动抛出异常，一般存在某个方法中无法处理某个异常
        }
        try {  // try监控区域
            System.out.println(a/b);
        }catch (ArithmeticException e){  // 捕获异常，括号里是想要捕获的异常类型（最高时Throwable）
            // 增加
            System.out.println("div 0");
        }catch (Exception e){  // 大类的异常必须在小类异常的后边
            System.out.println("Exception");
        }finally {  // 处理善后工作
            System.out.println("finally");
        }
        // finally 可以不要，之后学习中可以用来释放占用的资源
    }
}
```

选中一行代码`Ctrl+Alt+T`可以快速生成包裹代码

另外，用户可以自定义异常类，只需要继承`Exception`类即可

```java
// 异常类

public class Demo2 extends Exception{
    // 传递数字>10就抛出异常
    private int detail;
    public Demo2(int a){
        this.detail = a;
    }

    @Override
    public String toString() {  // 直接通过alt+insert快速创建，打印异常信息
        return "Demo2{" +
                "detail=" + detail +
                '}';
    }

}
```

```java
// 抛出自定义异常

public class Demo3 {
    public static void main(String[] args) throws Demo2{
        int a = 11;
        if (a>10){
            throw new Demo2(a);  // 抛出
        }
       
    }
}
```

## I/O流

### 流

流就是内存和存储设备传输数据的通道

#### 分类

输入流就是将存储设备中的内容读入到内存中，输出流相反

字节流以字节为单位，可以读写所有的数据，字符流只能读写文本数据

节点流是具有实际传输数据的读写功能，过滤流就是在节点流的基础上增强功能

#### 字节流

`InputStream`和`OutputStream`是所有`I/O`流的超类，提供了一般子类的方法

下面以文件字节输入/输出流示例

##### FileInputStream

```java
public class Demo1 {
    public static void main(String[] args) throws IOException {
        // 创建文件输入流，并指定路径
        FileInputStream input = new FileInputStream("D://test.txt");// 可能没有这个文件，抛出异常
        // 1. 单个字节读入
        int len;
        while ((len=input.read())!=-1){
            System.out.print((char)len);
        }
        // 2. 多个字节读入
        byte[] buf = new byte[4];
        int count = input.read(buf);  // 将文件中读到的buf长度内容放在buf数组中
        System.out.println(new String(buf));
        System.out.println(count);
        // 3. 最优结合（因为不能够创建一个过大的数组）
        byte[] buf = new byte[1024];  // 缓冲区，每次接收1kb内容
        int count=0;
        while ((count=input.read(buf))!=-1) System.out.print(new String(buf,0,count));
        // 关闭
        input.close();
    }
}
```

##### FileOutputStream

```java
public class Demo2 {
    public static void main(String[] args) throws IOException {
        FileOutputStream os = new FileOutputStream("test.txt",true);  // 布尔为真代表追加内容
        // 追加内容同样会创建文件
        os.write(97);  // a的ASCII码，输出仍为a
        os.write('b');
        os.write('\n');
        String s="hello";
        os.write(s.getBytes());  // 传入字节数组
    }
}
```

##### 字节缓冲流

缓冲流即`BufferInputStream/BufferOutputStream`

本身文件输入输出流是不带缓冲的，单独使用文件字节流效率不高（容量太小）

缓冲流通过单独创建一个缓冲区，当主数据缓冲区内有可以直接获得

可以用于提高I/O的效率，减少访问磁盘的次数

数据存储在缓冲区内，通过`flush`将缓冲区内的内容写入文件中

```java
public class Demo3 {
    public static void main(String[] args) throws IOException {
        // 创建BufferInputStream
        FileInputStream is = new FileInputStream("test.txt");
        BufferedInputStream bufIs = new BufferedInputStream(is);  // 说明这个缓冲流是为了增强is的
        // 从缓冲区读取
        // int data=0;
        // while ((data=bufIs.read())!=-1) System.out.println();  // 利用BufferedInputStream自带的缓冲区
        // 也可以自己创建一个缓冲区并传入
        int count;
        byte[] buffer = new byte[1024];
        while ((count=bufIs.read(buffer))!=-1) System.out.print(new String(buffer,0,count));

        // 关闭只需要关闭缓冲流
        bufIs.close();
    }
}
```

```java
public class Demo4 {
    public static void main(String[] args) throws IOException {
        FileOutputStream os = new FileOutputStream("test.txt");
        BufferedOutputStream bufOs = new BufferedOutputStream(os);
        for (int i = 0; i < 10; i++) {
            bufOs.write("hello\n".getBytes());  // 写入8K缓冲区，先不写入文件
            // 直到缓冲区满了自动写入文件
            // bufOs.flush();  // 也可手动每次刷新到硬盘
        }
        bufOs.close();  // 关闭的时候会自动执行flush()操作
    }
}
```

#### 对象流

对象流增强了缓冲区功能和8种基本数据类型和字符串功能

同时通过流传输**对象**的过程称为<a name="序列化">序列化</a>和反序列化

```java
// 想要序列化一个对象，必须实现Serializable接口，但这个接口没有任何的方法（标记接口）
class Test1 implements Serializable {
    // 序列化版本号ID，可以保证序列化的类和反序列化的类是同一个类
    // 反序列化的时候UID会与文件中的UID比对，不一样就抛出异常
    @Serial
    private static final long serialVersionUID = 100L;

    private String name;
    private int age;
    private transient int test1;  // 用transient（瞬间的）修饰不会被序列化
    private static int test2;  // 静态属性也不会被序列化

    public Test1(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // 一个类正确的定义方式
    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    @Override
    public String toString() {
        return "Test1{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}

public class Demo5 {
    public static void main(String[] args) throws IOException, ClassNotFoundException {
        // 实现把一个对象写在硬盘上，序列化操作
        FileOutputStream fos = new FileOutputStream("test.bin");
        ObjectOutputStream oos = new ObjectOutputStream(fos);
        Test1 test = new Test1("test", 1);
        oos.writeObject(test);
        oos.close();
        // 读取文件重构对象，反序列化操作
        FileInputStream fis = new FileInputStream("test.bin");
        ObjectInputStream ois = new ObjectInputStream(fis);
        Test1 t = (Test1) ois.readObject();  // 强转为Test1类型
        // 如果文件内有多个对象继续读就能获得第二个对象
        ois.close();  // 关闭的时候也会关闭文件流
        System.out.println("Done");
        System.out.println(t.toString());
    }
}
```

注意要求序列化类中的对象属性（假设某个属性的类型是一个类的话）也要实现`Serializable`接口

#### 字符编码

- ISO-8859-1 收录除ASCII外，还包括西欧、希腊语、泰语、阿拉伯语、希伯来语对应的文字符号（一字符）
- UTF-8 针对Unicode码表的可变长度字符编码
- GB2312 简体中文
- GBK 简体中文、GB2312扩充（ANSI在中国即是GBK）
- BIG5 台湾、繁体中文

注意当编码方式和解码方式不一致的时候会出现乱码

#### 字符流

我们可以通过记事本的另存为查看当前记事本记录的代码格式

```java
public class Demo6 {
    public static void main(String[] args) throws IOException {
        // 当文件中存在中文时，要用字符流读取和写入
        FileWriter fileWriter = new FileWriter("test.txt");
        for (int i = 0; i < 10; i++) {
            fileWriter.write("你好\n");
        }
        fileWriter.close();

        FileReader fr = new FileReader("test.txt");  // FileReader继承FileInputStream
        int data=0;
        while ((data=fr.read())!=-1){  // 读取一个字符不再是一个字节
            System.out.print((char) data);
        }
    }
}
```

#### 字符缓冲流

```java
public class Demo7 {
    public static void main(String[] args) throws IOException {
        // BufferedReader
        FileReader fileReader = new FileReader("test.txt");
        BufferedReader br = new BufferedReader(fileReader);
        // 第一种方法
//        char[] buf = new char[1024];
//        int count = 0;
//        while ((count=br.read(buf))!=-1)
//            System.out.println(new String(buf,0,count));
//        br.close();
        // 第二种方法（readLine()）
        String line = null;
        while ((line=br.readLine())!=null)
            System.out.println(line);
        br.close();

        FileWriter fileWriter = new FileWriter("test.txt");
        BufferedWriter bw = new BufferedWriter(fileWriter);
        for (int i = 0; i < 10; i++) {
            bw.write("你好！");
            bw.newLine();  // 写入一个换行符（如果是windows就是\r\n，linux是\n）
        }
        bw.close();
    }
}
```

#### 打印流

打印流可以在写入文件时原样写入

```java
public class Demo8 {
    public static void main(String[] args) throws FileNotFoundException {
        PrintWriter pw = new PrintWriter("test.txt");
        pw.println(1);
        pw.println(true);
        pw.print(1.1);
        pw.print('a');
        pw.close();
    }
}
```

#### 转换流

转换流可以将字节流转换为字符流，并且可以设置字符的编码方式

```java
public class Demo9 {
    public static void main(String[] args) throws IOException {
        FileInputStream fis = new FileInputStream("test.txt");
        InputStreamReader inputStreamReader = new InputStreamReader(fis, StandardCharsets.UTF_8);
        int data=0;
        while ((data= inputStreamReader.read())!=-1){
            System.out.print((char) data);
        }
    }
}
```

### 文件类（File）

File代表物理盘符中的一个文件或者一个文件夹

我们可以通过内部的方法访问文件的各个属性或创建文件

```java
public class Demo1 {
    static File file = new File("test.txt");  // 现在只是创建了一个文件对象，可以并没有文件

    public static void main(String[] args) throws IOException {
        separator();
        information();
        check();
        directoryOpen();
    }

    // 1. 文件分隔符
    public static void separator(){
        System.out.println("路径分隔符"+ File.pathSeparator);  // ';'
        System.out.println("名称分隔符"+ File.separator);  // '\'
    }

    // 2. 文件创建/删除
    public static void fileOpen() throws IOException {
        if (!file.exists()) {  // 也是用来判断文件是否存在
            boolean b = file.createNewFile();
            System.out.println("创建结果：" + b);  // 文件已经存在就返回false，否则创建一个新文件并返回true
        }
        boolean b = file.delete();  // 直接删除，返回方式和上面创建文件同理
        System.out.println("删除结果："+ b);
        file.deleteOnExit();  // 利用jvm在程序结束后删除文件
    }

    // 3. 获取文件信息
    public static void information(){
        System.out.println("文件的绝对路径：" + file.getAbsolutePath());
        System.out.println("定义时的路径：" + file.getPath());
        System.out.println("获取文件名称："+ file.getName());
        System.out.println("获取父目录："+ file.getParent());
        System.out.println("获取文件长度："+ file.length());
        System.out.println("文件的创建时间："+ new Date(file.lastModified()).toString());
    }

    // 4. 判断文件属性
    public static void check(){
        System.out.println("是否可写："+ file.canWrite());
        System.out.println("是否是文件："+ file.isFile());
        System.out.println("是否隐藏："+ file.isHidden());
    }

    // 5. 目录操作
    public static void directoryOpen(){
        // 创建文件夹
        File dir = new File("a\\b");  // dir指向最后一个目录
        if (!dir.exists())
            System.out.println("创建结果：" + dir.mkdirs());
        System.out.println("删除结果："+dir.delete());  // 删除的必须是空目录，同时只能删除最底层目录b
        dir.deleteOnExit();  // 同
        // 获取目录信息和判断和文件相同
        String[] files = dir.list();  // 返回目录下所有文件名称，是字符串数组
        if (files != null) {
            for (String s : files) {
                System.out.println(s);
            }
        }
    }
}
```

### 文件过滤器接口（FileFilter）

当调用`File`类中的`listFiles()`方法时，支持传入`FileFileter`接口的接口实现类，对获取的文件进行过滤，只有满足条件的文件才可以出现在`listFiles()`的返回值中

```java
public class Demo2 {
    public static void main(String[] args) {
        File file = new File("a\\b");
        File[] files = file.listFiles(pathname -> pathname.getName().endsWith(".jpg"));  // Lambda表达式
        assert files != null;
        for (File file1 : files) {
            System.out.println(file1.getName());
        }
    }
}
```

### 递归遍历文件夹

```java
public class Demo3 {
    public static void main(String[] args) {
        listDir(new File("a"));
    }

    public static void listDir(File dir){
        File[] files = dir.listFiles();
        System.out.println(dir.getAbsolutePath());
        if (files!=null && files.length>0){
            for (File file : files) {
                if (file.isDirectory()) listDir(file);
                else System.out.println(file.getAbsolutePath());
            }
        }
        // 同理也可以递归删除文件夹
    }
}
```

### Properties集合

相当于字典类型，存储的属性名和属性值都是字符串类型，存储内容和流有关，没有泛型

```java
public class Demo1 {
    public static void main(String[] args) throws IOException {
        Properties properties = new Properties();
        properties.setProperty("name","test");
        System.out.println(properties.toString());
        Set<String> proNames = properties.stringPropertyNames();
        for (String pro : proNames) {
            System.out.println(pro+"->"+properties.getProperty(pro));
        }
        // 通过打印流打印集合内容
        PrintWriter pw = new PrintWriter("test.txt");
        properties.list(pw);  // 传入一个打印流对象
        pw.close();
        // 通过文件输出流保存集合信息
        FileOutputStream fos = new FileOutputStream("test.txt");
        properties.store(fos,"comments");
        fos.close();
        // 通过输入流加载之前保存的集合信息
        Properties pro1 = new Properties();
        FileInputStream fis = new FileInputStream("test.txt");
        pro1.load(fis);
        fis.close();
        System.out.println(pro1.toString());
    }
}
```

## GUI编程

### AWT

包含了很多的类和接口

![image-20210314171920071](https://s2.loli.net/2021/12/05/MK7gHT1heNjuvwS.png)

#### 窗口（Frame）

```java
package com.GUI.test1;

import java.awt.*;

public class Demo2 {
    public static void main(String[] args) {
        MyFrame myFrame1 = new MyFrame(100, 100, 200, 200);
        MyFrame myFrame2 = new MyFrame(100, 300, 200, 200);
        MyFrame myFrame3 = new MyFrame(300, 100, 200, 200);
    }
}

class MyFrame extends Frame{
    static int id=0;  // 可能存在多个窗口，我们需要一个计数器
    public MyFrame(int x,int y, int w, int h){
        super("MyFrame "+ ++id);
        setVisible(true);  // 可见性
        setBounds(x,y,w,h);  // 快捷窗口大小
        setBackground(Color.pink);
    }
}
```

#### 面板（Panel）

面板是在容器里面的，可以看成一个空间，但是不能单独存在

面板的方法大多和窗口`Frame`一模一样（布局，大小等）

内容应该全部放在面板中执行，因为窗口是唯一的

```java
public class Demo3 {
    public static void main(String[] args) {
        Frame frame = new MyFrame(100,100,1000,500);
        Panel panel = new Panel();
        frame.setLayout(null);  // 设置布局
        panel.setBounds(100,100,100,100);
        panel.setBackground(new Color(127, 255, 152));
        frame.add(panel);
    }
}
```

#### 监听

Java内置了`WindowListener`监听器，但是直接使用的话会需要重写很多方法

```java
new WindowListener() {
    @Override
    public void windowOpened(WindowEvent e) {
        
    }

    @Override
    public void windowClosing(WindowEvent e) {

    }

    @Override
    public void windowClosed(WindowEvent e) {

    }

    @Override
    public void windowIconified(WindowEvent e) {

    }

    @Override
    public void windowDeiconified(WindowEvent e) {

    }

    @Override
    public void windowActivated(WindowEvent e) {

    }

    @Override
    public void windowDeactivated(WindowEvent e) {

    }
}
```

因此我们可以使用适配器模式快速添加想要的监听效果

```java
frame.addWindowListener(new WindowAdapter() {  // 适配器模式，是WindowListener的一个子类
    @Override
    public void windowClosing(WindowEvent e) {
        System.exit(0);
        super.windowClosing(e);
    }
});  // 监听事件（窗口关闭：System.exit(0)）
```

然而，`WindowListener`只能监听窗口动作，要监听别的事件需要`ActionListener`

同时我们可以通过判断一个元素的`ActionCommand`来通过同一个监听类执行不同按钮的不同命令

```java
public class Demo7 {
    public static void main(String[] args) {
        Frame frame = new Frame();
        Button button = new Button("test");
        button.setActionCommand("start");  // 设定命令，如果没写的话就默认Label值
        frame.setBounds(100,100,500,500);
        // 因为addActionListener()需要一个ActionListener，所以我们需要构造一个ActionListener
        MyActionListener myActionListener = new MyActionListener();
        button.addActionListener(myActionListener);
        frame.add(button,BorderLayout.CENTER);
        frame.setVisible(true);
        closeWindow(frame);  // 关闭窗口
    }

    private static void closeWindow(Frame frame){
        WindowAdapterIMPL windowAdapterIMPL = new WindowAdapterIMPL();
        frame.addWindowListener(windowAdapterIMPL);
    }
}

// 事件监听
class MyActionListener implements ActionListener{
    @Override
    public void actionPerformed(ActionEvent e) {
        System.out.println(e.getActionCommand());  // 获得之前设置的命令动作名
    }
}

class WindowAdapterIMPL extends WindowAdapter{
    @Override
    public void windowClosing(WindowEvent e) {
        System.exit(0);
        // 也可以通过setVisible(false);隐藏窗口，但是不关闭进程
        super.windowClosing(e);
    }
}
```

#### 布局管理器

会发现上述代码中我们使用了一个布局管理器

```java
frame.setLayout(null);  // 设置布局
```

事实上，该方法还提供了很多种布局

- 流式布局

  ```java
  public class Demo4 {
      public static void main(String[] args) {
          MyFrame myFrame = new MyFrame(100,100,500,500);
          Button button = new Button("hi");
          button.setSize(200,200);
          myFrame.setLayout(new FlowLayout(FlowLayout.LEFT/*默认是CENTER*/));  // 流式布局
          myFrame.add(button);  // 尽管设定了200的大小，实际显示的大小还是按字数多少来
      }
  }
  ```

  从左到右排，排满了之后换下一行

  ![image-20210314185605795](https://s2.loli.net/2021/12/05/UKl1gdANDGqrT9O.png)

- 东西南北中

  ```java
  public class Demo5 {
      public static void main(String[] args) {
          MyFrame myFrame = new MyFrame(100,100,500,500);
          Button test1 = new Button("test");
          Button test2 = new Button("test");
          test1.setSize(200,100);
          myFrame.setLayout(new BorderLayout());
          myFrame.add(test1,BorderLayout.CENTER);
          myFrame.add(test2,BorderLayout.SOUTH);
      }
  }
  ```

  按钮会铺满整个屏幕

  ![image-20210314190317907](https://s2.loli.net/2021/12/05/pEw6tkg5r7nFqxK.png)

- 表格布局（Grid）

  ```java
  public class Demo6 {
      public static void main(String[] args) {
          MyFrame myFrame = new MyFrame(100, 100, 500, 500);
          Button test1 = new Button("test1");
          Button test2 = new Button("test2");
          Button test3 = new Button("test3");
          Button test4 = new Button("test4");
          Button test5 = new Button("test5");
          myFrame.setLayout(new GridLayout(3,2));  // 建立一个三行两列的表格
          myFrame.add(test1);
          myFrame.add(test2);
          myFrame.add(test3);
          myFrame.add(test4);
          myFrame.add(test5);
  
          myFrame.pack();  // 可以自动的选择最优秀的布局，是一个Java函数，使用后窗口变小了
      }
  }
  ```

  ![image-20210314191046586](https://s2.loli.net/2021/12/05/FlIijACQOMYB68V.png)

事实上，单个布局无论是哪一个都十分难看，所以实际开发中大多使用嵌套的方式进行布局

可以面板套面板，并在最后一层中添加按钮

#### 输入框（TextFIeld）

```java
public class Demo1 {
    public static void main(String[] args) {
        new MyFrame();
    }
}

class MyFrame extends Frame{
    public MyFrame() throws HeadlessException {
        TextField textField = new TextField();
        add(textField);
        setBounds(200,200,500,500);
        ActionListenerIMPL actionListenerIMPL = new ActionListenerIMPL();
        // 按下 enter 就会触发这个输入框的事件
        textField.addActionListener(actionListenerIMPL);
        textField.setEchoChar('*');  // 将输入的字母变成*
        setVisible(true);
        closeWindow(this);
    }

    private static void closeWindow(Frame frame){
        frame.addWindowListener(new WindowAdapterEXT());
    }
}

class ActionListenerIMPL implements ActionListener{
    @Override
    public void actionPerformed(ActionEvent e) {
        TextField content = (TextField) e.getSource();  // 会发现这是一个object类，可以强制类型转化
        System.out.println(content.getText());
        content.setText("");  // 按下回车后清空内容
    }
}

class WindowAdapterEXT extends WindowAdapter {
    @Override
    public void windowClosing(WindowEvent e) {
        System.exit(0);
        super.windowClosing(e);
    }
}
```

#### 组合和内部类

`oop`原则，组合大于继承

```java
class A extends B{}  // 继承
class A{
    public B b;  // 组合，在A类中私有B（用B类型定义b）
}
```

让我们开发一个计算器

```java
public class Demo2 {
    public static void main(String[] args) {
        new Calculator().loadFrame();
    }
}

class Calculator extends Frame {
    TextField num1, num2, num3;
    public void loadFrame(){
        num1 = new TextField(10);
        num2 = new TextField(10);
        num3 = new TextField(20);
        Button button = new Button("=");
        button.addActionListener(new MyCalculatorListener(this));
        Label label = new Label("+");  // 是一个标签，可以显示文字
        setLayout(new FlowLayout());
        setBounds(100,100,500,500);
        add(num1);
        add(label);
        add(num2);
        add(button);
        add(num3);
        setVisible(true);
        closeWindow(this);
    }

    private static void closeWindow(Frame frame){
        frame.addWindowListener(new WindowAdapterEXT());
    }

}

class MyCalculatorListener implements ActionListener{
    // 在一个类中组合另外一个类！可以使用这个类的所有属性和方法！
    Calculator calculator;

    public MyCalculatorListener(Calculator calculator) {
        this.calculator = calculator;
    }

    @Override
    public void actionPerformed(ActionEvent e) {
        int n1 = Integer.parseInt(calculator.num1.getText());
        int n2 = Integer.parseInt(calculator.num2.getText());
        calculator.num3.setText(""+(n1+n2));
        calculator.num1.setText("");
        calculator.num2.setText("");
    }
}
```

```java
// 或者直接使用内部类，一步搞定，甚至不需要组合
// 直接复制到类Calculator内
private class MyCalculatorListener implements ActionListener{

    @Override
    public void actionPerformed(ActionEvent e) {
        int n1 = Integer.parseInt(num1.getText());
        int n2 = Integer.parseInt(num2.getText());
        num3.setText(""+(n1+n2));
        num1.setText("");
        num2.setText("");
    }
}
```

#### 画笔（Paint）

```java
public class Demo3 {
    public static void main(String[] args) {
        new MyPaint().loadFrame();
    }
}

class MyPaint extends Frame{

    public void loadFrame(){
        setBounds(200,200,500,500);
        setVisible(true);
        closeWindow();
    }

    private void closeWindow(){
        this.addWindowListener(new WindowAdapterEXT());
    }

    // 画笔
    @Override
    public void paint(Graphics g) {
        // 画笔，需要有颜色，画笔可以画画
        g.setColor(Color.red);
        g.fillOval(100,100,100,100);  // 实心的圆
        // g.drawOval(); 是空心的
    }
}
```

#### 监听鼠标事件

让我们实现用鼠标在窗口中画点

```java
public class Demo4 {
    public static void main(String[] args) {
        new MouseTest("Test");
    }
}

class MouseTest extends Frame{

    static ArrayList<Point> points;

    public MouseTest(String title) throws HeadlessException {
        super(title);
        setBounds(200,200,300,400);
        points = new ArrayList<>();
        setVisible(true);
        this.addMouseListener(new MyMouseListener());  // 会发现这个和窗口监听一样是一个接口，要重写很多类
        this.addWindowListener(new WindowAdapterEXT());
    }

    @Override
    public void paint(Graphics g) {
        Iterator<?> iterator;  // 迭代器
        iterator = points.iterator();
        while (iterator.hasNext()){
            Point next = (Point) iterator.next();
            g.setColor(Color.blue);
            g.fillOval(next.x,next.y,20,20);
        }
    }

    // 适配器模式
    private class MyMouseListener extends MouseAdapter {
        @Override
        public void mousePressed(MouseEvent e) {
            // 让我们点击的时候能够在界面上产生一个点
            // 这个点就是鼠标的点，e就是鼠标
            points.add(e.getPoint());
            // 每次点击鼠标都要重画一遍
            repaint();  // 调用父类方法
        }
    }
}
```

#### 监听键盘监听

```java
public class Demo5 {
    public static void main(String[] args) {
        new KeyTest();
    }
}

class KeyTest extends Frame{
    public KeyTest() throws HeadlessException {
        setBounds(100,100,500,500);
        setVisible(true);

        this.addKeyListener(new KeyAdapter() {
            @Override
            public void keyPressed(KeyEvent e) {
                int keycode = e.getKeyCode();
                System.out.println(keycode);
                if (keycode==KeyEvent.VK_W){
                    System.out.println("W键");
                }
            }
        });
        
        addWindowListener(new WindowAdapterEXT());
    }
}
```

### Swing

`AWT`比`Swing`更底层，类似于一个框架，`Swing`在`AWT`的基础上可以实现更多的功能

#### 建立一个窗口和标签

```java
public class Demo1 {
    // init() 初始化
    public void init(){
        JFrame frame = new JFrame("这是一个JFrame窗口");
        frame.setVisible(true);
        frame.setBounds(100,100,300,300);
        // 设置文字 JLabel
        JLabel jLabel = new JLabel("Hello");
        frame.add(jLabel);
        // 文本居中
        jLabel.setHorizontalAlignment(SwingConstants.CENTER);  // 水平对齐+常量居中
        // 设置背景色
        // 获得一个容器，容器里面的颜色才是他自己的颜色
        // 所有元素放在容器中，同时容器不需要被add进JFrame窗口中
        Container contentPane = frame.getContentPane();
        contentPane.setBackground(Color.yellow);
        // 关闭事件
        frame.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);  // 高级的关闭方法
    }

    public static void main(String[] args) {
        // 建立一个窗口
        new Demo1().init();
    }
}
```

#### 弹窗

```java
// 主窗口
public class Demo2 extends JFrame {

    public Demo2() throws HeadlessException {
        this.setVisible(true);  // 涉及两个窗口，必须要用this
        this.setBounds(100,100,700,500);
        // 容器
        Container contentPane = this.getContentPane();
        contentPane.setLayout(null);  // 绝对定位

        JButton jButton = new JButton("点击弹出一个对话框");
        jButton.setBounds(30,30,200,50);
        contentPane.add(jButton);
        // 点击按钮的时候弹出一个弹窗
        jButton.addActionListener(e -> new DialogEXT());
        this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
    }

    public static void main(String[] args) {
        new Demo2();
    }
}

// 弹窗
class DialogEXT extends JDialog{
    public DialogEXT() {
        this.setVisible(true);
        this.setBounds(100,100,500,500);
        // 注意默认状态下弹窗就有关闭事件，可以不设定

        Container contentPane = this.getContentPane();
        contentPane.setLayout(null);
        JLabel label = new JLabel("Hello");
        label.setBounds(100,100,200,200);
        label.setHorizontalAlignment(SwingConstants.CENTER);
        label.setOpaque(true);  // 想给标签设定颜色就得先把透明度调了
        label.setBackground(Color.black);
        contentPane.add(label);
    }
}
```

#### 图标

```java
// 同时继承类和图标接口
public class Demo3 extends JFrame implements Icon {

    private int width;
    private int height;

    public Demo3() throws HeadlessException {
    }

    public void init(){
        Demo3 demo3 = new Demo3(15,15);  // 定义一个图标
        // 图标放在标签上，也可以放在按钮上
        JLabel icon = new JLabel("icon", demo3, SwingConstants.CENTER);
        Container contentPane = getContentPane();
        contentPane.add(icon);
        contentPane.setVisible(true);
        this.setVisible(true);
        this.setBounds(100,100,500,500);
        this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
    }

    public Demo3(int width, int height) throws HeadlessException {
        this.width = width;
        this.height = height;
    }

    public static void main(String[] args) {
        new Demo3().init();
    }

    // 重写三个接口方法
    @Override
    public void paintIcon(Component c, Graphics g, int x, int y) {
        g.fillOval(x,y,width,height);
    }

    @Override
    public int getIconWidth() {
        return this.width;
    }

    @Override
    public int getIconHeight() {
        return this.height;
    }
}
```

#### 图片

```java
public class Demo4 extends JFrame {

    public Demo4() throws HeadlessException {
        JLabel label = new JLabel("ImageIcon");
        URL url = Demo4.class.getResource("test.jpg");  // 获取当前这个类的下面图片资源，返回的url是一个绝对路径
        ImageIcon imageIcon = new ImageIcon(url);  // 利用图片对象保存url
        label.setIcon(imageIcon);
        label.setHorizontalAlignment(SwingConstants.CENTER);
        Container contentPane = this.getContentPane();
        contentPane.add(label);
        setVisible(true);
        setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
        setBounds(100,100,400,400);
    }

    public static void main(String[] args) {
        new Demo4();
    }
}
```

#### 面板

```java
public class Demo5 extends JFrame {

    public Demo5() throws HeadlessException {
        Container contentPane = this.getContentPane();
        contentPane.setLayout(new GridLayout(2,1,10,10));  // 表格布局，后面参数代表元素之间间距
        JPanel jPanel = new JPanel(new GridLayout(1,3,10,10));
        jPanel.add(new JButton("1"));
        jPanel.add(new JButton("1"));
        jPanel.add(new JButton("1"));
        contentPane.add(jPanel);
        this.setVisible(true);
        this.setBounds(100,100,500,500);
        this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
    }

    public static void main(String[] args) {
        new Demo5();
    }
    
}
```

#### 滚动条

```java
public class Demo6 extends JFrame{

    public Demo6() throws HeadlessException {
        Container contentPane = getContentPane();
        
        // 文本域，支持换行
        JTextArea jTextArea = new JTextArea(20,50);
        jTextArea.setText("Hello");

        // Scroll面板
        JScrollPane jScrollPane = new JScrollPane(jTextArea);
        contentPane.add(jScrollPane);
        setVisible(true);
        setBounds(100,100,200,200);
        setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
    }

    public static void main(String[] args) {
        new Demo6();
    }
}
```

![image-20210319001948117](https://s2.loli.net/2021/12/05/2FqeYHLOVcp41ER.png "滚动条")

#### 按钮

- 图片按钮

  ```java
  public class Demo7 extends JFrame {
      public Demo7() throws HeadlessException {
          Container contentPane = this.getContentPane();
          URL resource = Demo7.class.getResource("test.jpg");
          ImageIcon imageIcon = new ImageIcon(resource);
          contentPane.setLayout(null);  // 利用绝对定位防止按钮占满整个屏幕
  
          JButton jButton = new JButton();
          jButton.setIcon(imageIcon);
          jButton.setToolTipText("鼠标放上时弹出的提示文本");
          jButton.setText("按钮文本");
          jButton.setBounds(100,100,600,300);
          jButton.setHorizontalAlignment(SwingConstants.CENTER);
          contentPane.add(jButton);
          this.setVisible(true);
          this.setBounds(100,100,1000,500);
          this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
      }
  
      public static void main(String[] args) {
          new Demo7();
      }
  }
  ```

  ![image-20210319091410202](https://s2.loli.net/2021/12/05/HeRCTDQWBUlMGny.png "图片按钮")

- 单选按钮

  ```java
  public class Demo8 extends JFrame {
      public Demo8() throws HeadlessException {
          Container contentPane = getContentPane();
          contentPane.setLayout(new FlowLayout());
  
          JRadioButton jB1 = new JRadioButton("1");
          JRadioButton jB2 = new JRadioButton("2");
          JRadioButton jB3 = new JRadioButton("3");
  
          // 由于单选框只能选一个，要对以上单选框打组
          ButtonGroup buttonGroup = new ButtonGroup();
          buttonGroup.add(jB1);
          buttonGroup.add(jB2);
          buttonGroup.add(jB3);
  
          contentPane.add(jB1);  // 注意不能直接添加一个组
          contentPane.add(jB2);
          contentPane.add(jB3);
  
          this.setVisible(true);
          this.setBounds(100,100,300,300);
          this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
      }
  
      public static void main(String[] args) {
          new Demo8();
      }
  }
  ```

- 多选框

  将单选框改成`JCheckBox`即可，同时注意不需要打组了

#### 列表

- 下拉框

  ```java
  public class Demo9 extends JFrame {
  
      public Demo9() throws HeadlessException {
          Container contentPane = getContentPane();
          JPanel jPanel = new JPanel();  // 一般都会放在一个面板中
          jPanel.setBounds(50,50,100,10);
  
          JComboBox<Object> objectJComboBox = new JComboBox<>();
          objectJComboBox.addItem("hello");
          objectJComboBox.addItem("hi");
          objectJComboBox.addItem("good");
  
          jPanel.add(objectJComboBox);
          contentPane.add(jPanel);
  
          setVisible(true);
          setBounds(100,100,200,200);
          setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
      }
  
      public static void main(String[] args) {
          new Demo9();
      }
  }
  ```

- 列表框

  ```java
  public class Demo10 extends JFrame {
  
      public Demo10() throws HeadlessException {
          Container contentPane = getContentPane();
  
          String[] contents = {"1","2","3"};
          JList<Object> objectJList = new JList<>(contents);
  
          contentPane.add(objectJList);
  
          setVisible(true);
          setBounds(100,100,200,200);
          setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
      }
  
      public static void main(String[] args) {
          new Demo10();
      }
  }
  ```

#### 文本框

```java
public class Demo11 extends JFrame {

    public Demo11() throws HeadlessException {
        Container contentPane = getContentPane();
        contentPane.setLayout(new GridLayout(3,1));

        // 文本框
        JTextField textField = new JTextField("文本框");

        // 密码框
        JPasswordField passwordField = new JPasswordField("密码框");

        // 文本域
        JTextArea textArea = new JTextArea("文本域");

        contentPane.add(textField);
        contentPane.add(passwordField);
        contentPane.add(textArea);

        setVisible(true);
        setBounds(100,100,1000,500);
        setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);

    }

    public static void main(String[] args) {
        new Demo11();
    }
}
```

![image-20210319095630633](https://s2.loli.net/2021/12/05/AiND51PuT6H4yVv.png)

注意到文本框和密码框默认都是居中，且无法换行，文本域顶格

### 贪吃蛇

制作一个贪吃蛇，我们首先需要对其中的界面进行分析

- 一个窗口
- 一个面板用来承载所有元素
- 一个画笔画出元素
- 图片素材

然后我们要制订完成的步骤

1. 画上总体的界面
2. 绘制小蛇
3. 使小蛇随时间运动
4. 使小蛇随键盘转弯
5. 放置食物
6. 失败判定

对于每一个步骤，我们都可以对其进行机械化操作

1. 定义数据
2. 画上去
3. 监听事件（键盘，事件）

## 多线程初步

### 简介

在操作系统中运行的程序就是进程，一个进程可以有多个线程，比如一个视频可以同时听声音，看图像，看弹幕等等，多线程就是一台机器同时完成多个任务

进程等于是一个保护伞，各种各样的线程在进程内跑，线程是`CPU`调度和执行的单位

我们知道程序执行的时候会先执行`main()`函数，这就说明`main()`函数是程序的主线程

除了主线程之外，还有一个`gc()`线程主要负责垃圾回收

事实上，一个`CPU`还是只能执行一个代码，所以我们模拟多线程就是使`CPU`迅速切换执行代码

在一个进程中，如果开辟了多个线程，线程的运行由调度器安排调度，调度器是与操作系统紧密相关的，先后顺序不能人为干预

对同一份资源进行操作时，会存在资源抢夺的问题，需要加入并发控制

> 不能让资源被同时抢夺，让抢夺资源的线程排好队一个一个来

### 线程创建

创建线程有两种方法

- 继承`Thread`类方法

  ```java
  // 创建线程方式1，继承
  public class Demo1 extends Thread{
      @Override
      public void run() {
          // run方法线程体
          for (int i = 0; i < 5; i++) {
              System.out.println("Looking..."+i);
          }
      }
  
      public static void main(String[] args) {
          // main线程，主线程
          // 创建一个线程对象
          Demo1 demo1 = new Demo1();
          // 调用start()方法开启线程
          demo1.start();
          for (int i = 0; i < 5; i++) {
              System.out.println("Studying..."+i);
          }
      }
  }
  ```

  ![image-20210321165300770](https://s2.loli.net/2021/12/05/zcljsOe2gaWSKCH.png "多线程执行模式")

  如果不使用`start`方法而是直接使用`run()`调用就不会进行多线程操作了

### 尝试用多线程下载网图

网络上下载`commons-io.jar`复制后粘贴到项目中新建的`lib`目录下，并且右击添加到库

![image-20210403192636438](https://s2.loli.net/2021/12/05/P8eOvSAI1wl9Guf.png "添加库")

```java
public class Demo2 extends Thread{
    private String url;
    private String name;

    public Demo2(String url, String name){
        this.url = url;
        this.name = name;
    }

    @Override
    public void run() {
        WebDownloader webDownloader = new WebDownloader();
        webDownloader.downloader(url, name);
        System.out.println("下载的文件名为:"+name);
    }

    public static void main(String[] args) {
        Demo2 j1 = new Demo2("https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/u=2458053954,3888878830&fm=26&gp=0.jpg", "1.jpg");
        Demo2 j2 = new Demo2("https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/u=2458053954,3888878830&fm=26&gp=0.jpg", "2.jpg");
        Demo2 j3 = new Demo2("https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/u=2458053954,3888878830&fm=26&gp=0.jpg", "3.jpg");

        j1.start();
        j2.start();
        j3.start();
    }
}

class WebDownloader{
    public void downloader(String url, String name){
        try {
            FileUtils.copyURLToFile(new URL(url),new File(name));  // 把一个url变成一个文件
        } catch (IOException e) {
            e.printStackTrace();
            System.out.println("IO异常,downloader方法出现问题");
        }
    }
}
```

### 实现Runnable接口

和`Thread`类整体差不多，但是是一个接口

```java
public class Demo3 implements Runnable{

    @Override
    public void run() {
        for (int i = 0; i < 5; i++) {
            System.out.println("Looking..."+i);
        }
    }

    public static void main(String[] args) {
        // 创建runnable接口的实现类对象
        Demo3 demo3 = new Demo3();
        // 创建线程对象，通过线程对象来开启我们的线程（代理）
        Thread thread = new Thread(demo3);
        thread.start();
        for (int i = 0; i < 5; i++) {
            System.out.println("Studying..."+i);
        }
    }
}
```

事实上`Thread`类也实现了`Runnable`接口，推荐使用`Runnable`，因为Java要避免单继承的局限性

### 多个线程运行同一操作

```java
public class Demo4 implements Runnable{

    private int ticketNum = 10;

    @Override
    public void run() {
        while (ticketNum > 0) {
            System.out.println(Thread.currentThread().getName() + "-->拿到了第" + ticketNum-- + "张票");
        }
    }

    public static void main(String[] args) {
        Demo4 tickets = new Demo4();
        new Thread(tickets,"1").start();
        new Thread(tickets,"2").start();
        new Thread(tickets,"3").start();
    }
}
```

![image-20210403201546436](https://s2.loli.net/2021/12/05/hGpM2DkZH5En3ru.png "拿票模拟")

事实上，当多个线程操作同一个资源的情况下，线程不安全了，数据紊乱

比如可能遇到某两个人拿到了同一张票的情况（上图无体现，但可以看出数据顺序出现问题）

这就涉及到并发的问题

### 代理

静态代理模式，就是代理对象和真实对象都实现同一个接口

代理对象要代理真实角色，同时代理对象可以实现很多真实角色实现不了的事情，而真实对象只需要专注于做自己的事情

以上一部分代码为例，`Thread`就是代理对象，我们实现的接口类就是真实对象

我们先通过接口实现一个对象，再用代理对象`Thread`传入真实对象，通过`Thread`类的方法来实现真实对象本身实现不了的操作

真实对象就是我们个人，代理对象就是专门做某件事的公司，我们个人也可以做这件事，但是好麻烦，于是我们把这件事交给公司来专业方便的实现

### Lambda表达式

`Lambda`表达式实际上简化了我们的表达式

#### 使用原因

- 避免匿名内部类定义过多
- 可以让一些代码看上去更加简洁
- 去掉了一堆没有意义的代码，只留下核心的逻辑

#### 函数式接口

任何接口，如果只包含唯一一个抽象方法，那么他就是一个函数式接口

```java
// 官方定义的Runnable接口
@FunctionalInterface
public interface Runnable {
    /**
     * When an object implementing interface {@code Runnable} is used
     * to create a thread, starting the thread causes the object's
     * {@code run} method to be called in that separately executing
     * thread.
     * <p>
     * The general contract of the method {@code run} is that it may
     * take any action whatsoever.
     *
     * @see     java.lang.Thread#run()
     */
    public abstract void run();
}
```

对于函数式接口，我们可以 通过`Lambda`表达式来创建该接口的对象

#### 怎么演化的

```java
// 1.这是一个函数式接口
interface TestInterface{
    void test();
}

// 2.这是一个平常的实现类
class TestInterface1 implements TestInterface{
    @Override
    public void test() {
        System.out.println("实现类");
    }
}

public class Demo5 {
    
    // 3.这是一个静态内部类
    static class TestInterface2 implements TestInterface{
        @Override
        public void test() {
            System.out.println("静态内部类");
        }
    }

    public static void main(String[] args) {
        TestInterface test;
        test = new TestInterface1();
        test.test();
        test = new TestInterface2();
        test.test();
        
        // 4.这是一个局部内部类

        class TestInterface3 implements TestInterface{
            @Override
            public void test() {
                System.out.println("局部内部类");
            }
        }
        test = new TestInterface3();
        test.test();
        
        // 5.是一个匿名内部类，没有类的名称，必须借助接口或者父类
        test = new TestInterface(){
            @Override
            public void test() {
                System.out.println("匿名内部类");
            }
        };
        test.test();
        
        // 6.这是利用lambda表达式
        test = ()-> System.out.println("lambda表达式");
        test.test();
    }
}
```

由上述可以看出`lambda`表达式对于代码的简化，不过注意到首先要保证`test`是一个函数式接口类型

如果接口类存在参数，就把`()`改成一个参数名称即可

> 如：`test = a->sout("hi "+ a);`
>
> 注意到甚至不需要定义a的类型，前提是接口当中已经定义了a

### 线程状态

![image-20210407163233804](https://s2.loli.net/2021/12/05/LznEwQY8F4ItXTS.png)

#### 线程停止

- 不推荐使用JDK使用的`stop()`、`destory()`方法
- 推荐让线程自己停下来，例如利用次数
- 建议使用一个标志位进行终止变量，当`flag=false`时，终止线程运行

```java
public class Demo6 implements Runnable{

    private boolean flag = true;

    @Override
    public void run() {
        int i = 0;
        while (flag){
            System.out.println("run...Thread"+i++);
        }
    }

    public void stop(){
        this.flag = false;
    }

    public static void main(String[] args) {
        Demo6 demo6 = new Demo6();
        new Thread(demo6).start();
        for (int i = 0; i < 1000; i++) {
            System.out.println("main"+i);
            if (i==900){
                // 调用stop方法切换标志位，让线程停止
                demo6.stop();
                System.out.println("线程停止");
            }
        }
    }
}
```

#### 线程休眠

利用`sleep()`方法令线程进行休眠，模拟网络延时，放大问题的发生性

同时记住每一个对象都有一把锁，`sleep()`不会释放锁

```java
// 获取系统当前时间
public class Demo7 {
    public static void main(String[] args) {
        while (true) {
            try {
                Date date = new Date(System.currentTimeMillis());
                Thread.sleep(1000);
                System.out.println(new SimpleDateFormat("HH:mm:ss").format(date));
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}
```

#### 线程礼让

- 礼让线程，让当前正在执行的线程暂停，但不阻塞
- 让线程从运行状态转为就绪状态
- 继而让`cpu`重新调度，但是注意礼让不一定成功，看`cpu`心情

```java
public class Demo8 {
    static class MyYield implements Runnable{

        @Override
        public void run() {
            System.out.println(Thread.currentThread().getName()+" 线程开始执行");
            // if (Thread.currentThread().getName().equals("a")) Thread.yield();  // 礼让
            System.out.println(Thread.currentThread().getName()+" 线程停止执行");
        }
    }

    public static void main(String[] args) {
        MyYield myYield = new MyYield();
        new Thread(myYield,"a").start();
        new Thread(myYield,"b").start();
    }
}
```

#### 线程合并

通过`join`合并进程，待此线程执行完之后再执行其他线程，执行`join`线程时其他线程阻塞（插队）

```java
public class Demo9 implements Runnable{
    @Override
    public void run() {
        for (int i = 0; i < 100; i++) {
            System.out.println("插入线程 " + i);
        }
    }

    public static void main(String[] args) {
        for (int i = 0; i < 100; i++) {
            System.out.println("主线程 " + i);
            if (i == 50){
                Thread thread = new Thread(new Demo9());
                thread.start();
                try {
                    thread.join();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}
```

#### 查看线程状态

通过`Thread.State`查看线程状态

- `NEW` 线程尚未启动
- `RUNNABLE`线程处于就绪状态
- `BLOCKED`线程被阻塞并正在等待监视器锁定
- `WAITING`该线程正在等待另一个线程执行
- `TIMED_WAITING`等待另一个线程执行动作达到指定等待时间（`sleep`）
- `TERMINATED`已退出的线程

#### 线程优先级

Java提供一个线程调度器来监控程序中启动后进入就绪状态的所有线程，线程调度器按照优先级决定应该先调度那个线程来执行

线程的优先级用数字表示，范围从1~10，其中

- `Thread.MIN_PRIORITY = 1`
- `Thread.MAX_PRIORITY = 10`
- `Thread.NORM_PRIORITY = 5`

同时我们可以通过`getPriority()`和`setPriority(int x)`来改变或获取优先级

优先级高的只是大概率先执行，权重比较大，事实上小概率也会让优先级低的先执行

#### 守护线程

线程分为用户线程和守护线程

虚拟机必须确保用户线程执行完毕（`main()`）

但是虚拟机不用等待守护线程执行完毕（`gc()`）

守护线程可以在后台记录操作日志，监控内存，垃圾回收等等

```java
public class Demo10 {
    public static void main(String[] args) {
        Daemons daemons = new Daemons();
        Users users = new Users();

        Thread thread1 = new Thread(new Daemons());
        Thread thread2 = new Thread(new Users());

        thread1.setDaemon(true);  // 默认false表示用户线程

        thread1.start();
        thread2.start();
    }
}

class Daemons implements Runnable{
    @Override
    public void run() {
        while (true) System.out.println("守护线程");
    }
}

class Users implements Runnable{
    @Override
    public void run() {
        for (int i = 0; i < 10; i++) {
            System.out.println("用户线程");
        }
    }
}
```

### 线程同步

线程同步就是同一个对象被多个线程操作

但是如同之前编的代码一样，当同一个资源多个人都想使用的时候，这个资源可能会被重复使用

因此，处理多线程问题时，多个线程访问同一对象，并且某些线程还想修改这个对象，这时我们需要线程同步，线程同步就是一种等待机制，多个需要同时访问此对象的线程进入这个**对象的等待池**形成队列，等待前面的线程使用完毕，下一个线程再使用

#### 锁

面对线程同步时，必须使用**队列+锁**的机制

为了保证数据在方法中被访问时的正确性，在访问中加入了锁机制（synchronized）

当一个线程获得对象的排他锁，独占资源，其他线程必须等待，使用后释放锁即可，同时注意

- 当一个线程持有锁会导致其他所有需要锁的线程挂起
- 在多线程的竞争下，加锁，释放锁会导致比较多的上下文切换和调度延时，引起性能问题
- 如果一个优先级高的线程等待一个优先级低的线程释放锁，会导致优先级倒置，引起性能问题

线程同步一定会损失性能，但是保证了安全性

通过对方法加入`synchronized`关键字控制对对象的访问，每个对象对应一把锁，每个`synchronized`方法都必须获得调用该方法的对象的锁才能执行，否则线程阻塞

注意，若将一个大的方法申明为`synchronized`将会影响效率

所以一般来说，我们会使用`synchronized(Obj){}`块

- 其中`Obj`是一个监视器，可以是任何对象，但是推荐使用共享资源作为同步监视器
- 同步方法中无需指定同步监视器，因为同步方法的同步监视器就是`this`这个对象本身

```java
public class Demo1 {
    public static void main(String[] args) {
        List<String> list = new ArrayList<String>();
        for (int i = 0; i < 10000; i++) {
            new Thread(()->{
                synchronized (list){
                    list.add(Thread.currentThread().getName());  // 对list加锁
                }
            }).start();
        }
        System.out.println(list.size());
    }
}
// 该程序可能还出现并不会显示完所有内容，其实是因为list线程和主线程一起在跑，可能主线程跑完了list线程还没跑完但程序直接结束了，因为start()之后并不会马上执行某线程
// 只需要在结尾休眠一会即可
```

多个线程进行同一操作，就在同一操作中添加锁

#### JUC并发包

JUC是别人写好的专门用来做并发编程的包，可以省去加锁过程

可以把上述代码的`List<>`改成`CopyOnWriteArrayList<>`安全列表

#### 死锁

多个线程各自占有一些共享资源，并且互相等待其他线程占有的资源才能运行

但是如果遇到两个线程互相在等待对方释放资源，都停止执行就会发生死锁现象

重点是一个锁还没执行完就想要获得另一个锁

```java
public class Demo2 {
    public static void main(String[] args) {
        DeadLock test1 = new DeadLock(0, "test1");
        DeadLock test2 = new DeadLock(1, "test2");
        new Thread(test1).start();
        new Thread(test2).start();
    }
}

class Lock1 {}
class Lock2 {}

class DeadLock implements Runnable{

    // 保证需要的资源只有一份
    static Lock1 lock1 = new Lock1();
    static Lock2 lock2 = new Lock2();

    int o;
    String name;

    public DeadLock(int o, String name) {
        this.o = o;
        this.name = name;
    }

    @Override
    public void run() {
        try {
            deadLock();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }

    private void deadLock() throws InterruptedException{
        if (this.o == 0){
            synchronized (lock1){
                System.out.println(this.name + " acquire lock1");
                Thread.sleep(1000);
                synchronized (lock2){
                    System.out.println(this.name + " acquire lock2");
                }
            }
        }
        else {
            synchronized (lock2){
                System.out.println(this.name + " acquire lock2");
                Thread.sleep(1000);
                synchronized (lock1){
                    System.out.println(this.name + " acquire lock1");
                }
            }
        }
    }

}
```

#### Lock锁

`Lock`接口存在于`java.util.concurrent.locks`中，提供了对共享资源的独占访问

- `ReentrantLock`类实现了`Lock`接口，拥有与`synchronized`相同的并发性和内存语义
- 同时可以显式加锁，释放锁

```java
public class Demo3 implements Runnable{

    int tickets = 10;
    // 定义Lock锁，推荐的定义方法
    private final ReentrantLock lock = new ReentrantLock();

    @Override
    public void run(){
        while (true){
            try {
                lock.lock();  // 加锁
                if (tickets > 0) {
                    System.out.println(tickets--);
                } else {
                    break;
                }
            }finally {
                lock.unlock();  // 解锁
            }
        }
    }

    public static void main(String[] args) {
        Demo3 demo3 = new Demo3();

        new Thread(demo3).start();
        new Thread(demo3).start();
        new Thread(demo3).start();
    }
}
```

`synchronized`和`Lock`对比

- `Lock`是显性锁（手动开启和关闭锁），`synchronized`是隐性锁，出了自动域自动释放

- `Lock`只有代码块锁，`synchronized`有代码块锁和方法锁
- `Lock`锁性能更好，并且具有更好的扩展性（提供有更多的子类）
- 优先使用顺序
  - `Lock`>同步代码块（已经进入方法体，分配了相应资源）>同步方法（在方法体外）

### 线程协作

可以看作生产者和消费者模型，首先由生产者生产东西，生产中消费者处于等待状态

生产完成后通知消费者，消费者消费东西，让生产者等待，往复循环

```java
// 管程法

public class Demo4 {
    public static void main(String[] args) {
        SynContainer container = new SynContainer();

        new Producer(container).start();
        new Consumer(container).start();
    }
}

// 生产者
class Producer extends Thread {
    SynContainer container;

    public Producer(SynContainer container) {
        this.container = container;
    }
    @Override
    public void run() {
        for (int i = 0; i < 100; i++) {
            container.push(new Product(i));
            System.out.println("生产了 " + i);
        }
    }
}

// 消费者
class Consumer extends Thread{
    SynContainer container;

    public Consumer(SynContainer container) {
        this.container = container;
    }

    @Override
    public void run() {
        for (int i = 0; i < 100; i++) {
            System.out.println("消费了 "+container.pop().id);
        }
    }
}

// 产品
class Product{
    int id;

    public Product(int id) {
        this.id = id;
    }
}

// 缓冲区
class SynContainer{
    // 需要一个容器大小
    Product[] products = new Product[10];
    int count = 0;

    // 生产者放入产品
    public synchronized void push(Product product){
        while (count == products.length){
            // 生产等待
            try {
                this.wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        // 没有满，丢入商品
        products[count] = product;
        count++;
        // notifyAll就是通知wait的方法不用等待了
        this.notifyAll();
    }

    public synchronized Product pop(){
        while (count==0){
            try {
                this.wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        count--;
        this.notifyAll();
        return products[count];
    }
}
```

```java
// 信号灯法，等于为1的管程法
public class Demo5 {
    public static void main(String[] args) {
        TV tv = new TV();
        new Player(tv).start();
        new Watcher(tv).start();
    }
}

class Player extends Thread{
    TV tv;

    public Player(TV tv) {
        this.tv = tv;
    }

    @Override
    public void run() {
        for (int i = 0; i < 20; i++) {
            this.tv.play("节目 "+i);
        }
    }
}

class Watcher extends Thread{
    TV tv;

    public Watcher(TV tv) {
        this.tv = tv;
    }

    @Override
    public void run() {
        for (int i = 0; i < 20; i++) {
            this.tv.watch();
        }
    }
}

class TV{
    String voice;
    boolean flag = true;

    public synchronized void play(String voice){
        if (!flag){
            try {
                this.wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }

        System.out.println("表演 "+voice);
        this.notifyAll();
        this.voice = voice;
        this.flag = !this.flag;
    }

    public synchronized void watch(){
        if (flag){
            try {
                this.wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        System.out.println("观看 "+voice);
        this.notifyAll();
        this.flag = !this.flag;
    }
}
```

### 线程池

经常创建和销毁、使用量特别大的资源，比如并发情况下的线程，对性能影响很大

我们可以提前创建好多个线程，放入线程池中，使用时直接获取，使用完放回池中，可以避免频繁创建和销毁线程，实现重复使用

- 可以提高响应速度
- 降低资源消耗
- 便于线程管理
  - `corePoolSize` 核心池的大小
  - `maximumPoolSize` 最大线程数
  - `keepAliveTime` 线程没有任务时最多保持多长时间后终止

```java
public class Demo6 {

    static class MyThread implements Runnable{

        @Override
        public void run() {
            for (int i = 0; i < 100; i++) {
                System.out.println(Thread.currentThread().getName()+i);
            }
        }
    }

    public static void main(String[] args) {
        // 创建服务，创建线程池，参数为线程池大小
        ExecutorService service = Executors.newFixedThreadPool(10);
        service.execute(new MyThread());
        service.execute(new MyThread());
    }
}
```

## 网络编程

网络编程主要针对的是传输层内容（TCP，UDP）

Java中网络编程相关类都封装在`java.net`包中

### IP

`cmd`中`ipconfig`获得的都是我们的局域网ip，公网ip是看不到的

公网（互联网）-私网（局域网）

- 192.168.xx.xx 一般都是局域网，专门给组织内部使用的

```java
public class Demo1 {
    public static void main(String[] args) {
        try {
            // 发现这个类没有构造方法，不能new出来
            InetAddress inetAddress;
            inetAddress = InetAddress.getByName("127.0.0.1");
            System.out.println(inetAddress);
            inetAddress = InetAddress.getByName("localhost");
            System.out.println(inetAddress);
            inetAddress = InetAddress.getLocalHost();
            System.out.println(inetAddress);
            // 三种方法获得本机ip
        } catch (UnknownHostException e) {
            e.printStackTrace();
        }
    }
}
```

### 端口

端口表示的是计算机中一个程序的进程，不同的进程有不同的端口号

端口分为TCP端口和UDP端口，每一协议都有65535个端口

端口分类：

- 公有端口 0~1023（尽量不要占用）
  - HTTP : 80
  - HTTPS : 443
  - FTP : 21
  - Telent : 23
- 程序注册端口 1024~49151，主要给用户或者程序使用
  - Tomcat : 8080
  - MySQL : 3306
  - Oracle : 1521
- 动态，私有端口 49152~65535（也尽量不要用）

CMD中通过`netstat -ano`查看所有端口，通过`tasklist`查看所有进程（任务管理器也可）

```java
// 存放一个ip+端口
public class Demo2 {
    public static void main(String[] args) {
        InetSocketAddress inetSocketAddress = new InetSocketAddress("127.0.0.1", 8080);
        System.out.println(inetSocketAddress);
    }
}
```

### 通信协议

网络通信协议非常的复杂，我们需要对他进行分层

TCP/IP协议簇，实际上是一组协议

- TCP: 用户传输协议
- UCP: 用户数据报协议
- IP: 网络互联协议

TCP协议可以看作打电话，运用了**三次握手 四次分手**两者进行连接比较稳定，分为客户端为服务端，传输完成自动释放连接，效率比较低

UDP协议相当于发短信，不连接不稳定，客户端和服务端没有明确的界限，不管有没有准备好，都可以发给你，效率高（DDOS: 洪水攻击）

### TCP实现传输数据

```java
// 服务端
public class ServerTest {
    public static void main(String[] args) throws IOException {
        // 服务器应该有一个地址
        ServerSocket serverSocket = new ServerSocket(9999); // 网络编程也叫做套接字编程
        // 监听 等待客户端连接
        Socket socket = serverSocket.accept();
        // 读取客户端消息
        InputStream is = socket.getInputStream();
        // 管道流 让输入流通过管道接一下再输出
        ByteArrayOutputStream pipeOs = new ByteArrayOutputStream();
        byte[] bytes = new byte[1024];
        int len;
        while ((len=is.read(bytes))!=-1){
            pipeOs.write(bytes,0,len);
        }
        System.out.println(pipeOs.toString());
        // 通知客户端已经接收完毕
        OutputStream os = socket.getOutputStream();
        os.write("done".getBytes(StandardCharsets.UTF_8));
        // 关闭资源
        pipeOs.close();
        is.close();
        socket.close();
        serverSocket.close();
    }
}

// 客户端
public class ClientTest {
    public static void main(String[] args) throws IOException {
        // 要知道服务器的地址
        InetAddress byName = InetAddress.getByName("127.0.0.1");
        int port = 9999;
        Socket socket = new Socket(byName, port);
        // 发送消息 IO流
        OutputStream os = socket.getOutputStream();
        os.write("hi".getBytes(StandardCharsets.UTF_8));
        // 通知服务器已经结束
        socket.shutdownOutput();
        // 确认服务器接收完毕，断开连接
        InputStream inputStream = socket.getInputStream();
        // 接收服务器发来的确认数据
        ByteArrayOutputStream byteArrayOutputStream = new ByteArrayOutputStream();
        byte[] bytes = new byte[1024];
        int len;
        while ((len=inputStream.read(bytes))!=-1)
            byteArrayOutputStream.write(bytes,0,len);
        System.out.println(byteArrayOutputStream.toString());
        // 关闭服务
        byteArrayOutputStream.close();
        inputStream.close();
        os.close();
        socket.close();
    }
}
```

### 文件上传

将上述代码的`Byte`改成`File`即可

同时注意在客户端上传文件时要先使用`FileInputStream`导入文件内容

```java
FileInputStream fileInputStream = new FileInputStream(new File("test.jpg"));
byte[] buffer = new byte[1024];
int len1;
while ((len1=fileInputStream.read(buffer))!=-1){
    os.write(buffer,0,len1);  // 输出文件
}
```

### Tomcat

 `Tomcat`即是一种`B/S`架构，是我们本地通过浏览器与`Tomcat`服务器进行通信

### UDP

`UDP`发送数据不需要连接服务器，只需要知道对方的地址

```java
// 发送端
public class UDPClientTest {
    public static void main(String[] args) throws Exception {
        // 建立一个Socket，随机指定一个端口
        DatagramSocket socket = new DatagramSocket();
        // 建立一个包
        String msg = "Hello";
        // 发送给谁
        InetAddress localhost = InetAddress.getByName("127.0.0.1");
        int port = 9999;
        // 数据，数据的长度，发送给谁
        DatagramPacket packet = new DatagramPacket(msg.getBytes(), 0, msg.getBytes().length, localhost, port);
        // 发送包
        socket.send(packet);
        socket.close();
    }
  
// 接收端    
public class UDPServerTest {
    // 其实这并不是服务端，哪一边都可以直接发送数据
    public static void main(String[] args) throws Exception {
        // 开放端口
        DatagramSocket socket = new DatagramSocket(9999);
        // 接收数据包
        byte[] bytes = new byte[1024];
        DatagramPacket datagramPacket = new DatagramPacket(bytes, 0, bytes.length);
        socket.receive(datagramPacket);  // 阻塞接收
        System.out.println(datagramPacket.getPort());
        System.out.println(new String(datagramPacket.getData(),0,datagramPacket.getLength()));
    }
}
```

#### 基于多线程UDP在线会话

```java
// 发送端
public class UDPSendTest implements Runnable {
    DatagramSocket socket;
    BufferedReader reader;

    int myPort;
    String toIP;
    int toPort;

    public UDPSendTest(int myPort, String toIP, int toPort) throws SocketException {
        this.myPort = myPort;
        this.toIP = toIP;
        this.toPort = toPort;

        this.socket = new DatagramSocket(myPort);
        this.reader = new BufferedReader(new InputStreamReader(System.in));
    }

    @Override
    public void run(){
        while (true){
            String s = null;
            try {
                s = this.reader.readLine();
            } catch (IOException e) {
                e.printStackTrace();
            }
            assert s != null;
            byte[] bytes = s.getBytes();
            DatagramPacket packet = new DatagramPacket(bytes, 0, bytes.length, new InetSocketAddress(this.toIP, this.toPort));
            try {
                this.socket.send(packet);
            } catch (IOException e) {
                e.printStackTrace();
            }
            if (s.equals("Done")) break;
        }
        this.socket.close();
    }
}
```

```java
// 接收端
public class UDPReceiveTest implements Runnable{
    DatagramSocket socket;
    int port;

    public UDPReceiveTest(int port) throws SocketException {
        this.port = port;
        this.socket = new DatagramSocket(this.port);
    }

    @Override
    public void run() {
        while (true){
            byte[] bytes = new byte[1024];
            DatagramPacket datagramPacket = new DatagramPacket(bytes,0,bytes.length);
            try {
                this.socket.receive(datagramPacket);
            } catch (IOException e) {
                e.printStackTrace();
            }
            String s = new String(datagramPacket.getData(), 0, datagramPacket.getData().length).trim();
            System.out.println("From "+datagramPacket.getPort()+": "+s);
            if (s.equals("Done")){
                break;
            }
        }
        socket.close();

    }
}
```

```java
// 用户端
public class UDPUser1 {
    public static void main(String[] args) throws SocketException {
        // 开启两个线程
        new Thread(new UDPSendTest(7777,"localhost",9999)).start();
        new Thread(new UDPReceiveTest(8888)).start();
    }
}

public class UDPUser2 {
    public static void main(String[] args) throws SocketException {
        // 开启两个线程
        new Thread(new UDPSendTest(6666,"localhost",8888)).start();
        new Thread(new UDPReceiveTest(9999)).start();
    }
}
```

## 注解和反射

注解和反射是所有框架的底层，是其底层实现的机制

### 注解

#### 什么是注解

- 注解和注释都可以给人看，但是注解还可以给程序解释，给程序读取

  > 注解是`Annotation` 而注释是`comment`


- 注解是以`@注解名`在代码中存在的，还可以添加一些参数值
- 注解可以附加在包，类，方法，属性等内容上，相当于给他们添加了额外的辅助信息，我们可以通过反射机制编程实现对这些元数据的访问
- 注解还可以起到检查注解内容的作用

#### 内置注解

- `@Override`只适用于修饰方法，表示重写注解

- `@Deprecated`可以用于修饰方法，属性，类，表示不鼓励使用这样的元素，通常是有更好的选择

- `@SuppressWarning`用来抑制编译时的警告信息，需要添加一个参数才可以使用

  > 一个变量未使用就会有警告，标黄也是警告，可以在前添加`@SuppressWarning`来镇压全部警告

#### 元注解(meta-annotation)

元注解的作用就是负责注解其他注解，Java定义了4个标准的元注解类型，他们被用来提供对其他注解类型做说明

- `@Target`用于描述注解的使用范围（被描述的注解可以用在什么地方）

- `@Retention`表示需要在什么级别保存该注释信息，用于描述注解的生命周期

  > `SOURCE` < `CLASS` < `RUNTIME`，一般都是用`RUNTIME`（运行时有效）

- `@Document`说明该注解将被包含在javadoc中

- `@Inherited`说明子类可以继承父类中的该注解

#### 自定义注解

`@interface`用来声明一个注解，格式：`public @interface [注解名]{[定义内容]}`，其中的每一个看似的方法实际上时声明了一个配置参数，方法的名称就是参数的名称，返回值类型就是参数的类型

> 注意返回值只能是基本类型，Class，String，enum

可以通过`default`来声明参数的默认值

如果只有一个参数成员，一般参数名为`value`

注解的元素必须要有值，我们定义注解元素时，经常使用空字符串或0作为默认值

```java
public class Demo1{
    @MyAnnotation(test = {"test"})
    public void test(){
        
    }
}

// 定义一个注解
@Target({ElementType.METHOD,ElementType.TYPE})  // 定义只能在方法和类上使用，当只有一个方法时可以省略value = 
// 同时注意，当且仅当只有一个方法且方法名为value时可以省略value = 
@Retention(value = RetentionPolicy.RUNTIME)  // 表示在所有地方都有效(RUNTIME)
@interface MyAnnotation{
    // 注解的参数：参数类型+参数名();
    // 可以默认为空
    String name() default "";
    int age() default -1;  // 如果默认值为-1表示不存在
    String[] test();
}
```

### 反射

Java作为一个静态语言，反射为其提供了动态性

反射是一个大概念，通过反射获取注解信息只是它的其中一个用处

#### 静态/动态语言

动态语言就是一类在运行的时候可以改变其结构的语言，例如添加新的函数，对象，甚至可以引进代码，已有的函数可以被删除或进行其他结构变化，即运行时代码可以改变自身结构

静态语言与之相反，Java不是动态语言，但是具有一定的动态性，即反射，我们可以利用反射机制获得蕾丝动态语言的特性，可以在编程的时候更加灵活

#### Reflection

`Reflection（反射）`是Java被视为动态语言的关键，其允许程序在执行期间借助`Reflection API`取得任何类内部信息，并能直接操作任意对象的内部属性及方法

```java
Class c = Class.forName("java.lang.String");  // 加载一个类的方式
```

![image-20210513195524986](https://s2.loli.net/2021/12/05/dFIhVg4LevTo98b.png "正常创建对象和通过反射加载类区别")

加载完类之后，在对内存的方法区中就产生一个Class类型的对象（一个类只有一个Class对象），这个对象包含了完整的类的结构信息，我们可以通过这个对象看到**类的结构**

![image-20210513201611638](https://s2.loli.net/2021/12/05/IV5n8blUAuotMyj.png "反射就是逆着来")

#### 应用

反射机制都是在程序运行中

- 判断对象所属的类
- 构造一个类的对象
- 判断一个类所具有的成员变量和方法
- 获取泛型信息
- 运行时处理注解
- 生成动态代理

#### 缺点

对性能有影响，使用反射是一种解释操作，通过JVM满足我们的要求，这类操作总是慢于直接执行相同的操作

#### Class类

Class类是我们创建的所有类的源头，对于每一个类而言，JRE都为其保留了一个不变的Class类型对象，一个Class对象包含了特定某个结构的有关信息

- Class本身也是一个类
- Class对象只能由系统建立对象
- 一个加载的类在JVM中只会有一个Class实例
- 一个Class对象对应的是一个加载到JVM中的一个`.class`文件
- 每个类的实例都会记得自己是由哪个Class实例所生成的
- 通过Class可以完整地得到一个类中的所有被加载的结构
- Class类是Reflection的根源，针对任何想要动态加载、运行的类，唯有先获得相应的Class对象

```java
public class Demo2 {
    public static void main(String[] args) throws ClassNotFoundException {
        // 通过反射获取类的class对象

        // 方式1：通过forName获得
        Class<?> c1 = Class.forName("com.mine.test1.User1");
        // 方式2：通过对象获得
        User user = new User1();
        Class<? extends User> c2 = user.getClass();
        // 方式3：通过类名.class获得
        Class<User1> c3 = User1.class;
        
        System.out.println(c1.hashCode());
        System.out.println(c2.hashCode());
        System.out.println(c3.hashCode());  // 返回值都相同！因为一个类型只有一个Class对象！
    }
}

class User {
    String name;

    public User() {
    }

    public User(String name) {
        this.name = name;
    }

    @Override
    public String toString() {
        return "User{" +
                "name='" + name + '\'' +
                '}';
    }
}

class User1 extends User {
    public User1() {
        this.name = "1";
    }
}

class User2 extends User {
    public User2() {
        this.name = "2";
    }
}
```

> 注意几乎所有的类型都有Class对象（万物皆对象）
>
> ```java
> public class Demo3 {
>     public static void main(String[] args) {
>         Class c1 = Object.class;
>         Class c2 = Comparable.class;
>         Class c3 = String[].class;
>         Class c4 = Override.class;
>         Class c5 = void.class;
>         Class c6 = Class.class;
>     }
> }
> ```
>
> ![image-20210513204619661](https://s2.loli.net/2021/12/05/UNrLIX2GZ9TeBgR.png "各种类型的class对象")

#### 内存分析一个类的加载过程

![image-20210513205046416](https://s2.loli.net/2021/12/05/aBZg3KVnEFo5kX6.png)

![image-20210513212628543](https://s2.loli.net/2021/12/05/82bT5gjlRusvke6.png)

![image-20210513212651085](https://s2.loli.net/2021/12/05/34pn6vdJj9Fx1Xy.png "jvm文字描述")

![image-20210729225308727](https://s2.loli.net/2021/12/05/5QJUDA1NjCh9nuz.png "jvm运行思路整理图")

##### 类的主动引用

类的主动引用一定会发生类的初始化

- 当虚拟机启动，先初始化main方法所在的类
- new一个类的对象
- 调用类的静态非常量成员和静态方法
- 对类进行反射调用
- 初始化某个类该类的父类未被初始化

##### 类的被动引用

不会发生类的初始化

- 当访问一个静态域时，只有真正声明这个域的类才会被初始化。如：通过子类引用父类的静态变量
- 通过数组定义类的引用
- 引用静态常量（常量在链接阶段就存入调用类的常量池中了）

```java
public class Demo4 {
    public static void main(String[] args) {
        System.out.println("Main Loading...");
        // 1. 主动引用
        Son son = new Son();
        Class<Son> sonClass = Son.class;
        // 2. 被动引用
        System.out.print(String.valueOf(Son.b));  // 只有父类被加载
        Son[] array = new Son[5];
        System.out.print(String.valueOf(Son.M));

    }
}

class Father {
    static int b = 2;
    static {
        System.out.println("Father Loading...");
    }
}

class Son extends Father{
    static {
        System.out.println("Son Loading...");
    }
    static final int M = 1;
}
```

#### 类加载器

##### 作用

- 将`.class`文件字节码内容加载到内存中

- 在堆中形成一个Class对象，作为方法区中类数据访问入口

详情可以见“jvm运行思路整理图”

##### 分类

| 名称                                      | 加载的类              | 说明                            |
| ----------------------------------------- | --------------------- | ------------------------------- |
| Bootstrap ClassLoader（启动类加载器）     | JAVA_HOME/jre/lib     | 无法直接访问                    |
| Extension ClassLoader(拓展类加载器)       | JAVA_HOME/jre/lib/ext | 上级为Bootstrap，**显示为null** |
| Application ClassLoader(应用程序类加载器) | classpath             | 上级为Extension                 |
| 自定义类加载器                            | 自定义                | 上级为Application               |

有关部分可以访问[Nyima]([https://nyimac.gitee.io/2020/07/03/JVM%E5%AD%A6%E4%B9%A0/])的jvm笔记总结博客

##### 使用

```java
public class Demo5 {
    public static void main(String[] args) {
        // 获取应用程序类加载器(ApplicationClassLoader)也叫系统类加载器(SystemClassLoader)
        ClassLoader appClassLoader = ClassLoader.getSystemClassLoader();
        // 获取扩展类加载器(Extension ClassLoader)
        ClassLoader extClassLoader = appClassLoader.getParent();
        // 获取启动类加载器(Bootstrap ClassLoader)
        ClassLoader bootClassLoader = extClassLoader.getParent();

        System.out.println(appClassLoader);  // jdk.internal.loader.ClassLoaders$AppClassLoader@2f0e140b
        System.out.println(extClassLoader);  // jdk.internal.loader.ClassLoaders$PlatformClassLoader@16b98e56
        System.out.println(bootClassLoader);  // null
    }
}
```

#### 创建运行时类的对象

##### 获得了Class后的相关方法获取

```java
public class Demo6 {
    public static void main(String[] args) throws ClassNotFoundException, NoSuchFieldException {
        // 获取类
        Class<?> aClass = Class.forName("com.mine.test1.TestClassLoader");

        // 获得类的信息
        System.out.println(aClass.getName());  // 包名+类名
        System.out.println(aClass.getSimpleName());  // 类名

        Field[] fields1 = aClass.getFields();  // 只能找到public属性，但是也可以找到父类的公共方法
        Field[] fields2 = aClass.getDeclaredFields();  // 所有声明了的属性，但是无法获得父类的方法
        aClass.getField("attr2");  // 已知某个属性
        for (Field field : fields2) {
            System.out.println(field);
        }  // 要这样输出
        // 获得方法的方式也于此雷同，只是变成了getMethod()和getDeclareMethod()，注意传参的时候第二项是返回值
        // 类似的还有getConstructor()可以获得类的构造器，指定构造器参数就是传入参数
    }
}

class TestFather {
    public int attr;
}

class TestClassLoader extends TestFather{
    private int attr1;
    public int attr2;
    protected int attr3;

    private void mat1(){}
    public void mat2(){}
    protected void mat3(){}
}
```

##### 利用反射获得对象/方法属性使用

```java
public class Demo7 {
    public static void main(String[] args) throws Exception {
        Class<?> aClass = Class.forName("com.mine.test1.TestClassLoader");
        // 利用反射构造一个对象
        // aClass.newInstance();  // 只能调用类的无参构造器来创建一个对象，不建议使用（因为如果没有无参构造就会报错
        // 指定构造方法（推荐）
        Constructor<?> constructor = aClass.getDeclaredConstructor(int.class);

        TestClassLoader instance = (TestClassLoader) constructor.newInstance(1);
        // 给这个构造器传入一个参数（可以看作new TestClassLoader(1))
        // 同时由于我们知道这个类的名称，所以可以将其返回值强转为我们指定的类

        System.out.println(instance);  // 注意应在类中加上toString方法，不然打印出来地址

        // 通过反射调用方法

        // 方法一
        Method setAttr1 = aClass.getDeclaredMethod("setAttr1", int.class);// 想要调用先要获取
        setAttr1.invoke(instance,1);  // 调用获取到的方法的invoke方法，传入谁想调用它（对象）和调用的参数
        // 方法二
        int attr1 = instance.getAttr1();  // 获取刚刚配置的值，直接通过对象调用


        System.out.println(attr1);

        // 通过反射修改属性
        Field attr11 = aClass.getDeclaredField("attr1");
        attr11.setAccessible(true);  // 如果修改的是私有属性可能会报错，关闭安全检测
        attr11.set(instance,1);  // 通常不能直接访问私有属性
        System.out.println(instance.getAttr1());
    }
}

class TestClassLoader extends TestFather{

    public TestClassLoader(int attr1) {
        this.attr1 = attr1;
    }

    private int attr1;

    public int getAttr1() {
        return attr1;
    }
    public void setAttr1(int attr1) {
        this.attr1 = attr1;
    }

    @Override
    public String toString() {
        return "TestClassLoader{" + "attr1=" + attr1 + '}';
    }
}
```

##### 获取泛型信息

- `ParameterizedType` 表示一种参数化类型，比如`Collection<String>`（也就是泛型）
- `GenericArrayType` 表示一种元素类型是参数化类型或者类型变量的数组类型
- `TypeVariable` 是各种类型变量的公共父接口
- `WildcardType` 代表一种通配符类型的表达式

以上各种类型都代表不饿能被归一到Class类中的类型但是又和原始类型齐名的类型

```java
public class Demo8 {
    public List<String> test01(Map<String,String> map, List<String> list) {
        return null;
    }

    public static void main(String[] args) throws NoSuchMethodException {
        Class<Demo8> c1 = Demo8.class;  // 反射获得Class
        Method met = c1.getDeclaredMethod("test01", Map.class, List.class);  // 获得其中的方法

        Type[] parameterTypes = met.getGenericParameterTypes();  // 获得该方法的参数类型信息，返回值为数组
        Type returnType = met.getGenericReturnType();  // 获得方法的返回类型信息

        // 获得泛型参数当中的每个参数类型
        for (Type parameterType : parameterTypes) {
            System.out.println("#" + parameterType);
            if (parameterType instanceof ParameterizedType) {  // 如果获得的类型是一个参数化类型（泛型）
                Type[] actualTypeArguments = ((ParameterizedType) parameterType).getActualTypeArguments();
                // 这样才能获得泛型里面包含的每个真实类型，存在数组里
                for (Type actualTypeArgument : actualTypeArguments) {
                    System.out.println(actualTypeArgument);  // 再将每个类型输出
                }
            }
        }

        //获得泛型返回值当中的每个参数类型，返回值只有一个
        if (returnType instanceof ParameterizedType) {
            Type[] actualTypeArguments = ((ParameterizedType) returnType).getActualTypeArguments();
            for (Type actualTypeArgument : actualTypeArguments) {
                System.out.println(actualTypeArgument);
            }
        }
    }
}
```

##### 获取注解信息

以下是通过<a name="ORM">某个类映射到数据库中一个表的示例</a>

![image-20210805103122811](https://s2.loli.net/2021/12/05/x1GfyLZ6cODizh5.png)

```java
public class Demo9 {
    public static void main(String[] args) throws NoSuchFieldException {
        Class<Demo9_1> c = Demo9_1.class;  // 还是先获得一个类（不是对象哦）

        // 通过反射获得所有类注解
        for (Annotation annotation : c.getAnnotations()) {
            System.out.println(annotation);
        }

        // 获得所有属性的所有注解
        for (Field declaredField : c.getDeclaredFields()) {
            for (Annotation declaredAnnotation : declaredField.getDeclaredAnnotations()) {
                System.out.println(declaredAnnotation);
            }
        }

        // 获得某个属性的某个注解的值
        Field id = c.getDeclaredField("id");  // 获得c这个对象的id属性
        TestInter2 a = id.getAnnotation(TestInter2.class);  // 寻找id中的某个注解
        System.out.println(a.s1() + " " + a.s2() + " " + a.i());  // 指定输出该注解的某个值
    }
}

@TestInter1("db_Demo")  // 注解了一下，并设定了名称
class Demo9_1{
    @TestInter2(s1="id",s2="int",i=8)
    private int id;
    @TestInter2(s1="age",s2="int",i=3)
    private int age;
    @Override
    public String toString() {
        return "Demo9_1{" +
                "id=" + id +
                ", age=" + age +
                '}';
    }
}

// 创建一个自定义类名注解
@Target(ElementType.TYPE)  // 作用域：类
@Retention(RetentionPolicy.RUNTIME)  // 作用时间：运行时
@interface TestInter1{
    String value();
}

@Target(ElementType.FIELD)  // 作用域：类
@Retention(RetentionPolicy.RUNTIME)  // 作用时间：运行时
@interface TestInter2{
    String s1();  // 在表中的列名
    String s2();  // 在这一列中存储什么类型的数据
    int i();  // 长度是多少
}
```

## JUC并发

JUC即指`java.util.concurrent`这个包，里面包括并发的功能，之前学过的`Callable`和`Lock`锁都在这个包里面

### 相关背景

#### 多线程初步遇到的问题

- `Thread`只是一个普通的线程类，`Runnable`接口没有返回值，相较于`Callable`效率较低
- 在业务当中之前学过的普通线程使用较少

#### 线程和进程

进程是一个程序的集合，一个进程往往包含多个线程，Java默认只包含`main`和`GC`两个线程

**例：**写文档的时候，就有键盘输入线程和自动保存线程等等

Java本身并没有权利开启线程，想要开启线程，即操作硬件，只能通过本地方法(`native`)

#### 并发和并行

- 并发：多线程操作同一个资源，一核CPU模拟出来多条线程，快速交替进行

- 并行：多个人一起行走，CPU多核，多个线程可以同时执行

>如何查看CPU的核数
>```java
>public class Demo1 {
>    public static void main(String[] args) {
>        // 获取CPU的核数（CPU密集型，IO密集型）
>        System.out.println(Runtime.getRuntime().availableProcessors());
>    }
>}
>```

并发编程的本质就是充分利用CPU的资源

#### 线程的状态

通过`Thread.state`查看线程的状态目录

```java
public enum State {
    // 新生
    NEW,
    // 运行
    RUNNABLE,
    // 阻塞
    BLOCKED,
    // 等待，死等
    WAITING,
    // 超时等待，一段时间就不等了
    TIMED_WAITING,
    // 终止
    TERMINATED;
}
```

#### wait/sleep区别

- `wait`来自`Object`，会释放锁，必须在同步代码块中使用，必须得有一个人让你等
- `sleep`在`Thread`里，抱着锁睡觉，不会释放锁，可以在任何地方睡觉

### Lock锁

#### Synchronized锁方法

传统`Synchronized`就是一个排队的过程，见下代码

```java
public class Demo2 {
    public static void main(String[] args) {
        // 并发：多个线程操作同一个资源类，把资源类丢入线程
        Demo2_1 t = new Demo2_1();
        // Runnable是@FunctionalInterface函数式接口，应该用lambda表达式
        // 即new Thread(()->{ }).start();
        new Thread(() -> {
            for (int i = 0; i < 30; i++) {
                t.test();
            }
        },"A").start();
        new Thread(() -> {
            for (int i = 0; i < 30; i++) {
                t.test();
            }
        },"B").start();
        // 以上的代码就是对一个资源类解耦的过程
    }
}

// 资源类 OOP，如果在这里实现了接口，这个类就成了单独的线程类，这个类就不干净了，耦合性太大
// 耦合性即资源类只干自己的事，不和外边主方法里的线程掺杂在一起
class Demo2_1{
    // 属性、方法
    private int i = 20;
    public void test(){
        if (i>0){
            System.out.println(Thread.currentThread().getName()+" consume "+(i--));
        }
    }
}
```

#### 实现类

![image-20210805115619090](https://s2.loli.net/2021/12/05/9IofsOxyjul35VT.png)

- 公平锁：十分公平，先来后到，一定要排队
- 非公平锁：可以插队，后面的线程可以先执行，`Synchronized`也是非公平锁

要用Lock锁，就得在方法内部先加锁，再在catch块中执行语句，再解锁

![image-20210805124126737](https://s2.loli.net/2021/12/05/HvW7J4XY2szZqmi.png)

```java
public class Demo3 {
    public static void main(String[] args) {
        Demo3_1 t = new Demo3_1();
        new Thread(() -> {
            for (int i = 0; i < 30; i++) {
                t.test();
            }
        },"A").start();
        new Thread(() -> {
            for (int i = 0; i < 30; i++) {
                t.test();
            }
        },"B").start();
    }
}

// lock使用  1、new一个可重入锁 2、l.lock()加锁 3、finally+unlock()解锁
class Demo3_1{
    private int i = 20;

    // 创建一个可重入锁对象
    Lock l = new ReentrantLock();  // 传入参数true的话就是公平锁，不然默认非公平锁

    public void test(){
        l.lock();  // 加锁
        try {
            if (i>0){
                System.out.println(Thread.currentThread().getName()+" consume "+(i--));
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            l.unlock();  // 解锁
        }
    }
}
```

#### 两个锁的区别

- `Synchronized`是Java内置的一个关键字，`Lock`是一个类
- `Synchronized`无法判断锁的状态，而`Lock`可以判断是否获取到了锁
- `Synchronized`会自动释放锁，A线程执行完了就自动释放
- `Synchronized`一个线程获得了锁，尽管堵塞了，另一个线程也会一直等，`Lock`锁就不一定会等（通过`lock.trylock`可以尝试获取锁，让堵塞的线程可以有机会释放锁）
- 他们都是可重入锁，不可以中断，非公平锁（`Lock`可以自己设置）
- `Synchronized`适合锁少量的代码同步问题，`Lock`适合锁大量的同步代码

#### 锁的含义

重要的就是解决生产者消费者问题，让程序知道当前需要操作的内容

实操时常考题：单例模式，排序算法，**生产者消费者问题**。死锁

##### Synchronized版（多线程中提到过）

`Synchronized`版围绕着`wait`和`notify`进行

```java
public class Demo4 {
    public static void main(String[] args) {
        Demo4_1 demo4_1 = new Demo4_1();
        new Thread(()->{
            for (int i = 0; i < 10; i++) {
                try {
                    demo4_1.inc();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        },"A").start();

        new Thread(()->{
            for (int i = 0; i < 10; i++) {
                try {
                    demo4_1.dec();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        },"B").start();
    }
}

class Demo4_1{
    private int num = 0;
    public synchronized void inc() throws InterruptedException {
        // 加锁三步q
        if (num!=0) this.wait();  // 1.判断等待
        num++;  // 2.功能
        System.out.println(Thread.currentThread().getName());
        this.notifyAll();  // 3.通知 其他所有线程加完了，解除其他线程的wait操作
    }
    public synchronized void dec() throws InterruptedException {
        if (num==0) this.wait();
        num--;
        System.out.println(Thread.currentThread().getName());
        this.notifyAll();
    }
}
```

**注意**：这样的程序并不安全，当创建大于两个线程的时候还是会不安全，因为运用了`if`判断，当等待被唤醒时无论当前状态如何都会跳出`if`进入接下来的语句，解决方法就是把`if`改成`while`即可

![image-20210809120241653](https://s2.loli.net/2021/12/05/QBSynxM6Yt1p7rF.png)

##### JUC版

JUC将传统的`wait`和`notify`替换为了`Condition`中的`await`和`signal`

通过`Condition`可以实现线程的任意的顺序进行

```java
public class Demo5 {
    public static void main(String[] args) {
        Demo5_1 demo5_1 = new Demo5_1();
        new Thread(()->{
            for (int i = 0; i < 10; i++) {
                try {
                    demo5_1.inc();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        },"A").start();

        new Thread(()->{
            for (int i = 0; i < 10; i++) {
                try {
                    demo5_1.dec();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        },"B").start();
    }
}

class Demo5_1{
    private int num = 0;
    private final Lock lock = new ReentrantLock();
    private final Condition condition1 = lock.newCondition();
    private final Condition condition2 = lock.newCondition();  // 两个方法两个监视器，通过监视器来判断当前执行的是哪个方法

    public void inc() throws InterruptedException {
        lock.lock();
        try {
            // 判断+功能+通知
            while (num==1){
                condition1.await();
            }
            System.out.println(Thread.currentThread().getName());
            num++;
            condition2.signal();  // 唤醒指定的人
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            lock.unlock();
        }
    }
    public void dec() throws InterruptedException {
        lock.lock();
        try {
            // 判断+功能+通知
           while (num==0){
                condition2.await();
            }
            System.out.println(Thread.currentThread().getName());
            num--;
            condition1.signal();  // 唤醒指定的人
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            lock.unlock();
        }
    }
}
```

##### 八个锁的现象

可以深刻理解锁到底是什么！

>  注意，下面的延迟用的都是`TimeUnit.SECONDS.sleep`这个方法，因为这是JUC包里面的方法

1. 对于外部两个线程争同一个锁，谁先拿到锁谁先执行
2. 拿到锁的线程无论方法内部是否延迟，都必须执行完
3. 普通方法的线程不受加锁方法内部延迟的影响
4. 创建两个实现类是两把不同的锁，执行顺序没有要求
5. 静态方法上锁实际上锁的是类Class模板（唯一），就算是两个对象也无所谓，类锁只有一把
6. 然而如果是静态方法和普通方法被对象调用（不管是不是同一个对象），由于一个是类锁一个是方法锁，所以有两把锁，操作结果同4

~~八个现象只有六点不是常识吗？~~

### 集合类不安全

```java
// list is unsafe
public class Demo6 {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();  // ArrayList不安全
        for (int i = 0; i < 100; i++) {
            new Thread(()->{
                list.add(UUID.randomUUID().toString().substring(0,5));
                System.out.println(list);
            }, String.valueOf(i)).start();
        }
    }
}
// Exception in thread "92" Exception in thread "89" java.util.ConcurrentModificationException 报错
```

**解决方法**

1. 把`ArrayList`改成`Vector`就不会报错，因为`Vector`默认线程安全（源码中有`Synchronized`加锁）

2. 利用`Collections`工具类内置方法实现

   ```java
   List<String> list = Collections.synchronizedList(new ArrayList<>());
   ```
   
3. 然而上面这个工具类并不在JUC里面，还可以用JUC内的`CopyOnWriteArrayList<>()`类

   ```java
   List<String> list1 = new CopyOnWriteArrayList<>();
   ```

   > CopyOnWrite 写入时复制，简称COW，是计算机设计领域的一种优化策略
   >
   > 当有多个线程调用的时候，对于相同的资源，在读取的时候是固定的但是写入的时候避免覆盖（会造成数据问题）
   >
   > 这也就是读写分离

第三种方法比起前两种，优势在于使用的是`Lock`锁完成（因为位于JUC下），同时运用读写分离，效率更高

### 未完待续……

# JavaEE

## JavaWeb

### 基本概念

web开发就是网页开发，表示我们可以从网上拿到一些东西

web分为静态web和动态web

- 静态web就是像html，css等，提供给所有人看的数据不会发生变化
- 动态web就是每个人在不同的时间不同的地点看到的信息各不相同（比如淘宝每日推荐等）

在Java中，动态web资源开发的技术统称为JavaWeb

像`xxx.html`这样的web资源，经过打包，统一地放在某一个文件夹下，这个文件夹可以供浏览器访问，那么这个程序就是web应用程序，通常一个web应用程序由多部分组成，包括：

- html，css，js
- jsp，servlet
- Java程序
- jar包
- 配置文件（Properties）

web应用程序编写完毕后，若想提供给外界访问，需要一个服务器来支持

#### 静态web

静态web的服务器需要有一个`web Service`将用户给的`Request`请求进行分析，将需要的内容`Response`返回

这些静态web都存在很多缺点，比如无法和数据库交互，大多都只通过JavaScript架构，缺少个性化

![image-20210825221446078](https://s2.loli.net/2021/12/05/qmhZPDSrxA6HQOL.png "静态web架构")

#### 动态web

页面会动态展示，因此服务器端的架构和静态web有所不同

![image-20210825222223734](https://s2.loli.net/2021/12/05/jEphuG7y1l9fgZO.png "动态web架构")

`WebServer Plugin`内置一些插件，会过滤一些有害请求，同时除了处理静态资源的一路，新增了动态资源的处理，处理之后同样交给`WebServer`

动态web也有缺点，假如服务器的动态web资源出现了错误，我们需要重新编写我们的后台程序，并重新发布（停机维护）

### web服务器相关技术

如上，所有的服务器都需要`WebServer`，同时`WebServer`有很多种类可以选择：

- ASP（Active Server Pages）
  - 微软公司开发，是国内最早流行的服务器页面
  - 在一个HTML中嵌入VB的脚本，ASP+DOM
  - ASP开发，因为在HTML里嵌入，十分繁杂混乱，基本上每一个页面都有几千行代码
  - ASP也可以用C#作为开发语言，用于进行微软的IIS开发
- PHP
  - PHP开发速度很快，功能很强大，跨平台，代码很简单
  - 但是无法承载大访问量的情况，具有局限性
  - 由于中国大部分网站都是小网站，使PHP很火爆
- JSP（本质就是Servlet）
  - 它是sun公司主推的B/S架构，基于Java语言（大部分大公司组件都是用Java写的）
  - 可以承载三高（高并发 高性能 高可用）问题带来的影响
  - 语法很像ASP，可以让原本学ASP的人快速上手JSP

而web服务器就是用于接收用户的请求并返回响应，包括IIS，**Tomcat**等

### Tomcat

#### 简介

[Tomcat](https://baike.baidu.com/item/tomcat/255751) 服务器是一个免费的开放源代码的Web 应用服务器，属于轻量级应用服务器，在中小型系统和并发访问用户不是很多的场合下被普遍使用，是开发和调试JSP 程序的首选。因为Tomcat 技术先进、性能稳定，而且免费，因而深受Java 爱好者的喜爱并得到了部分软件开发商的认可，成为目前比较流行的Web 应用服务器。

#### 安装

![image-20210825225616843](https://s2.loli.net/2021/12/05/1tvCMRFoc9IfrVS.png "官网")

![image-20210825230237703](https://s2.loli.net/2021/12/05/a6uGpU2K9xg3H8z.png "内部文件结构")

![image-20210825230412871](https://s2.loli.net/2021/12/05/UDyulFCrnqz7Sik.png "启动")

> 提示出现**org.apache.catalina.LifecycleException: 协议处理程序初始化失败**错误！
>
> ```shell
> 26-Aug-2021 00:37:54.080 严重 [main] org.apache.catalina.util.LifecycleBase.handleSubClassException 初始化组件[Connector
> [HTTP/1.1-8080]]失败。
>   org.apache.catalina.LifecycleException: 协议处理程序初始化失败
>           at org.apache.catalina.connector.Connector.initInternal(Connector.java:1054)
>           at org.apache.catalina.util.LifecycleBase.init(LifecycleBase.java:136)
>           at org.apache.catalina.core.StandardService.initInternal(StandardService.java:556)
>           at org.apache.catalina.util.LifecycleBase.init(LifecycleBase.java:136)
>           at org.apache.catalina.core.StandardServer.initInternal(StandardServer.java:1042)
>           at org.apache.catalina.util.LifecycleBase.init(LifecycleBase.java:136)
>           at org.apache.catalina.startup.Catalina.load(Catalina.java:747)
>           at org.apache.catalina.startup.Catalina.load(Catalina.java:769)
>           at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
>           at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:64)
>           at java.base/jdk.internal.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:
> 43)
>           at java.base/java.lang.reflect.Method.invoke(Method.java:564)
>           at org.apache.catalina.startup.Bootstrap.load(Bootstrap.java:305)
>           at org.apache.catalina.startup.Bootstrap.main(Bootstrap.java:475)
>   Caused by: java.net.BindException: Address already in use: bind
>           at java.base/sun.nio.ch.Net.bind0(Native Method)
>           at java.base/sun.nio.ch.Net.bind(Net.java:550)
>           at java.base/sun.nio.ch.ServerSocketChannelImpl.bind(ServerSocketChannelImpl.java:249)
>           at org.apache.tomcat.util.net.NioEndpoint.initServerSocket(NioEndpoint.java:242)
>           at org.apache.tomcat.util.net.NioEndpoint.bind(NioEndpoint.java:197)
>           at org.apache.tomcat.util.net.AbstractEndpoint.bindWithCleanup(AbstractEndpoint.java:1179)
>           at org.apache.tomcat.util.net.AbstractEndpoint.init(AbstractEndpoint.java:1192)
>           at org.apache.coyote.AbstractProtocol.init(AbstractProtocol.java:580)
>           at org.apache.coyote.http11.AbstractHttp11Protocol.init(AbstractHttp11Protocol.java:82)
>           at org.apache.catalina.connector.Connector.initInternal(Connector.java:1051)
> ```
>
> 通过`netstat -aon|findstr "8080"`找到占用我们8080端口的进程
>
> 然后记住占用的进程PID，在任务管理器-详细信息里面删掉他即可

> 如果出现闪退问题，可以在`startup.bat`文件末尾加上`pause`命令让程序执行完毕后暂停

![image-20210826010251191](https://s2.loli.net/2021/12/05/1ngUreRmispNtSz.png)

成功！

#### 配置

服务器核心配置文件就是`conf/server.xml`，其中可以配置系统的端口号，主机的名称，默认网站应用存放的位置等

> 改主机名称的时候不能只改配置文件里的内容，还需要改系统配置文件
>
> 1. ![image-20210826122520245](https://s2.loli.net/2021/12/05/Bb3V7O5SXK812Zn.png)
>    将此处的localhost改成自定义名称
> 2. `C:\Windows\System32\drivers\etc\hosts`在后面加上`127.0.0.1 [自定义的名称]`	![image-20210826122819666](https://s2.loli.net/2021/12/05/YUXrp29CamqtusE.png)

网站是如何访问的？

1. 输入一个域名+回车，意味着客户端发起了一个请求
2. 首先这个请求交给Windows的配置文件（hosts），检查是否有这个域名的映射
   - 有的话直接返回ip地址
   - 没有的话去DNS服务器寻找该域名对应的ip地址

3. 访问查询到的ip(OSI)

#### 发布一个自己的网站

将自己写的网站，放到服务器（Tomcat）中指定的web应用文件夹（webapps）下，即可通过浏览器（localhost:8080/[自定义文件夹]）访问

> 注意Tomcat默认情况会自动先进入ROOT文件夹内的（根目录）

注意，`webapps`里面一个目录就代表一个网站！网页默认会自动选择目录中的`index.html`内容进行优先展示

#### 部署网站的方式

部署项目的方式（目前有一个D盘下的hello.html需要部署到Tomcat）

1. 直接部署：

   将项目放到 webapps目录下即可。`/hello`:项目的访问路径即<a name="虚拟目录">虚拟目录</a>

   > 当项目十分多的时候，复制起来十分麻烦

2. 优化部署：

   将项目打成一个war包，再将war包放置到 webapps目录下，war包会自动解压缩成网站目录

   > 依旧涉及到复制操作，并不方便

3. 配置文件部署：

   在`conf/ server.xml`文件的`<Host>`标签体中配置`<Context docbase=D: \hello path=/hehe"/>`其中`docbase`为项目存放的路径，`path`为虚拟目录

   > 然而在配置文件中直接修改是十分危险的，这种方式也不建议

4. **热部署方式部署**：

   在 `conf\Catalina \localhost`创建任意名称的`.xml`文件。在文件中编写
   `<Context docbase="D: \hello/>`其中虚拟目录就是`.xml`文件的名称

   > 好处不仅是安全可靠，同时可以在Tomcat运行时修改文件内容而不用重启Tomcat服务

#### Http

Http全称超文本传输协议，是一个简单的请求-响应协议，他通常运行在TCP之上

超文本就是包括图片，音乐，视频，地图等在内的文件形式

Http分为`HTTP/1.0`和`HTTP/1.1(目前)`，前者客户端与web服务器链接后，只能获得一个web资源，然后立即断开连接，后者就是在先前的基础上可以获得多个资源（节省流量）

##### 请求/响应

- 请求：

  ![image-20210827113955393](https://s2.loli.net/2021/12/05/SkwNBq8ufmjOZRc.png)

  其中常用的有两种请求方式，分别是GET和POST

  - GET：请求能够携带的参数比较少，大小有限制，会在浏览器的URL中显示数据内容，不安全，但是比较搞高效

  - POST：请求携带的参数没有限制，大小没有限制，安全，但不高效

  - 但是鉴于目前的网络速度，高效的要求实际上差别不大，大多使用POST更加好

    > <img src="https://s2.loli.net/2021/12/05/T7XVtvOpS2bBRPA.png" alt="image-20210827120643139" style="zoom: 50%;" />

  而后的请求头内还有此次请求更加详细的请求信息

  ![image-20210827121430856](https://s2.loli.net/2021/12/05/a4Bcjk3WKdgJEXq.png)

  其中重要的参数有：

  - `Accept`告诉服务器自己这边支持的数据类型
  - `Accept-Encoding`声明自己支持的编码类型（gzip：接收用gzip压缩的输出）
  - `Accept-Language`声明自己浏览器的语言环境
  - `Connection`请求完成后事断开还是链继续连接
  - 等等

- 响应头：

  ![image-20210827114434878](https://s2.loli.net/2021/12/05/GNQ1PWxe4s9dMOZ.png)

  除了展示出来的响应头信息，还有些其他的内容

  - `Refresh`告诉客户端多久刷新一次
  - `Location`让网页重新定位

##### 状态码

整体印象可以看这个[http.cat](https://http.cat/)

常见的状态码比如：

- 200 OK，请求响应成功
- 3**，请求重定向
- 404，找不到资源
- 502，网关错误

### Maven

在Javaweb的开发中，需要使用大量的jar包，需要手动导入

如何能够让一个东西能够自动帮我们导入这些jar包，这就需要使用Maven（项目架构构建管理工具）

核心思想：约定大于配置。因为Maven会规定好你应该如何编写我们的Java代码，我们必须按照这个来

#### 安装

[官网](https://maven.apache.org/)直接下载解压即可

![image-20210827131108640](https://s2.loli.net/2021/12/05/ShNmzke1L4PDdJp.png)

其中Maven的配置文件为`apache-maven-3.8.2\conf\settings.xml`

#### 配置环境变量

在系统变量中，配置`M2_HOME`和`MAVEN_HOME`两个变量

![image-20210827133348943](https://s2.loli.net/2021/12/05/ch6s2rEiQp4uLNI.png)

并在环境变量Path中加上bin目录的地址

![image-20210827134055700](https://s2.loli.net/2021/12/05/CE5JaefwQdqpFAs.png)

启动cmd查看是否安装成功

![image-20210827133939909](https://s2.loli.net/2021/12/05/kY78uzRIMOm5rvn.png  "完成截图")

#### 添加镜像

由于国内访问国外的网站比较慢，我们可以给Maven添加阿里云镜像

访问[阿里云Maven镜像官网](https://developer.aliyun.com/mvn/guide)复制镜像配置信息

![image-20210827135112700](https://s2.loli.net/2021/12/05/ELJW572oVz8M4aG.png)

复制内容粘贴至[配置文件](apache-maven-3.8.2\conf\settings.xml)内的Mirrors内

```xml
  <mirrors>
      
    <mirror>
      <id>maven-default-http-blocker</id>
      <mirrorOf>external:http:*</mirrorOf>
      <name>Pseudo repository to mirror external repositories initially using HTTP.</name>
      <url>http://0.0.0.0/</url>
      <blocked>true</blocked>
    </mirror>

    <mirror>
      <id>aliyunmaven</id>
      <mirrorOf>*</mirrorOf>
      <name>aliyun public</name>
      <url>https://maven.aliyun.com/repository/public</url>
    </mirror>
    
  </mirrors>
```

#### 建立本地仓库

本地仓库使得我们可以不用每一次都从网上下载内容

在Maven环境中新建一个repo文件夹作为本地仓库，并在配置文件中添加地址

![image-20210827140414087](https://s2.loli.net/2021/12/05/cmike1xKMgr9NWt.png)

```xml
<!-- localRepository
   | The path to the local repository maven will use to store artifacts.
   |
   | Default: ${user.home}/.m2/repository
  <localRepository>/path/to/local/repo</localRepository>
  -->
  <localRepository>D:\PROGRAM\EXE\Environment\apache-maven-3.8.2\maven-repo</localRepository>
```

至此，Maven相关的文件配置工作完成

#### 在IDEA中创建原生Maven项目

创建项目之前，先在设置里修改我们的Maven路径

![image-20210827142702312](https://s2.loli.net/2021/12/05/GRvBO18EafdspZJ.png)

![image-20210827144028279](https://s2.loli.net/2021/12/05/ScjoWN5vqh4xEzk.png)

然后创建一个Maven项目

![image-20210827141203898](https://s2.loli.net/2021/12/05/x37uCXHgPjAoDRe.png)

> 会发现原型下面的内容非常的干净，有两个kotlin相关模板的也和我们javaweb的开发无关
>
> 当我们本地项目创建完之后会自动构建出很多模板，到时候再创建一遍即可

勾选从原型创建可以使用Maven的模板

![image-20210827141847849](https://s2.loli.net/2021/12/05/hgUXrkcOE5IGHxK.png)

> 图片错了，jav改成gav（坐标）

创建好Maven项目后会看到系统正在下一堆文件，慢慢等他下完就行

![image-20210827142506751](https://s2.loli.net/2021/12/05/TV1mnjaJgAKSFQ8.png)

然后可以在之前我们建的仓库中看看是不是有东西了

![image-20210827142933972](https://s2.loli.net/2021/12/05/uah6vyEgLfoG5nz.png)

#### 创建Maven时勾选模板

上述原生项目创建完毕后，我们再次新建一个Maven项目，会发现多了很多原型（模板）

![image-20210827145701602](https://s2.loli.net/2021/12/05/3TCgos9JtWacMFx.png)

选择模板后一路确定

![image-20210827150131448](https://s2.loli.net/2021/12/05/yw2Xo7eJYHc5mZi.png)

又会开始下一堆东西，慢慢等即可

#### 项目结构

原生的Maven项目十分干净，结构十分明了

![image-20210827144828402](https://s2.loli.net/2021/12/05/1Yl38fsTwdAyVvD.png)

通过web模板创建的Maven目录有些不一样

![image-20210827150413631](https://s2.loli.net/2021/12/05/6FJ3x9GgmoZtCIf.png)

为了让两者看上去差不多，可以手动<a name='创建源目录'>创建一下这里没有的目录</a>

> 会发现原生的Maven项目红红绿绿的文件夹比较多，事实上我们也可以创建这些文件夹
>
> 右击目录更改标记
>
> ![image-20210827150726407](https://s2.loli.net/2021/12/05/W4UXq2bm6yPTCeO.png)

当然现在的版本比较智能，当我们在main目录下创建目录时，会提示是否使用Maven原生目录

![image-20210827150912571](https://s2.loli.net/2021/12/05/x2AIEPVhcgfFXCq.png)

勾上就行了

#### 创建原生Maven文件添加web框架

在创建好的原生Maven模块处右键-添加框架支持并选择第一个选项即可，这样创建出来的web框架更加完整

![image-20210901191400088](https://s2.loli.net/2021/12/05/nTAZRLyHg8ujxKq.png)

![image-20210901191442251](https://s2.loli.net/2021/12/05/2dV6ULNRtD3GBZl.png)

#### 在Maven项目中添加Tomcat配置

![image-20210827152907144](https://s2.loli.net/2021/12/05/AgSYrKlcNUWs3i7.png)

然后就会出现Tomcat的配置页面

![image-20210827153419526](https://s2.loli.net/2021/12/05/wKysmBhFGUDxClT.png)

![image-20210827153552231](https://s2.loli.net/2021/12/05/tmQ6uZSKvAHqOFL.png)

 配置完成后还是会出现警告，我们点击部署-添加来添加一个工件

![image-20210827153745487](https://s2.loli.net/2021/12/05/72s6nmXF3pAyw4f.png)

点第一个即可

![image-20210827153814270](https://s2.loli.net/2021/12/05/yfmQdAs9OtMiLoK.png)

因为我们访问一个网站需要指定一个文件夹的名字（如Tomcat下的webapps文件夹），所以必须要创建一个工件

![image-20210827154654956](https://s2.loli.net/2021/12/05/xR9wnTs4D1K2YQh.png)

这个过程就叫做虚拟路径映射

之后只需要点击Tomcat旁边的绿色小三角即可启动Tomcat

![image-20210827154906676](https://s2.loli.net/2021/12/05/zC6HhdXRgLfAv9y.png)

之后会弹出`Helloworld`的网页，实际上就是项目文件中`index.jsp`内的内容（因为浏览器会自动去寻找网站下的`index`打头的文件)

启动过后，我们会发现项目结构中出现了一个`target`目录，里面就是我们构建出来的内容，然而我们可能发现Hello world的网页地址栏内容并不是`target`目录内的网站名，事实上是经过了虚拟路径映射（存疑）

> 虚拟目录映射，就是将web应用交给web服务器管理，然后就可以通过web服务器访问到这个资源。假设现在有一个专门用于发布新闻的web应用news，其位于c盘下，那么，如果配置tomcat，使得当我们访问tomcat服务器时会访问到news里的资源。
>
>    方式一、tomcat的自动映射，将news应用直接放在 tomcat主目录/webapps/，便可直接访问:`http://localhost:8080/news/index.html`
>
>    方式二、很多情况下，在实际的部署中，有可能web应用与tomcat服务器不在同一盘符下，即web应用没办法直接放在webapps目录下，这时就需要建立虚拟目录映射

![image-20210827234856030](https://s2.loli.net/2021/12/05/mwH3ufkgoziVE6P.png)

> 以下为个人猜想：
>
> 如图，此处`target`目录即为目标需要运行网站，程序启动之后在Tomcat下目录中建立相应文件夹，同时使`target`目录和图中`MVNTest_war`目录形成连接，即`MVNTest_war`目录为`target`目录的映射，使得浏览器能够正常读取`index.jsp`主页文件

此双击Maven侧边栏的clear命令，程序会自动清理target目录，这也说明target是一个临时性的目录，用于存放运行时的缓存临时复制文件，在程序结束以后可以被随意清理

#### Maven侧边栏内容

![image-20210827163543169](https://s2.loli.net/2021/12/05/OpVMA8Yyi7IvGEQ.png)

#### pom文件

`pom.xml`是Maven的核心配置文件，存放了Maven的相关信息

```xml
<?xml version="1.0" encoding="UTF-8"?>

<!--Maven版本和头文件-->
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <!--创建Maven时配置的GAV-->
  <groupId>com.test</groupId>
  <artifactId>MVNTest</artifactId>
  <version>1.0-SNAPSHOT</version>
  
  <!--项目的打包方式，
      Java应用通常用jar包
      JavaWeb应用通常用war包-->
  <packaging>war</packaging>

  <!--名称及范例，无关紧要-->
  <name>MVNTest Maven Webapp</name>
  <!-- FIXME change it to the project's website -->
  <url>http://www.example.com</url>

  <!--配置-->
  <properties>
    <!--项目的默认构建编码-->
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <!--编码版本-->
    <maven.compiler.source>1.7</maven.compiler.source>
    <maven.compiler.target>1.7</maven.compiler.target>
  </properties>

  <!--项目依赖-->
  <dependencies>
    <!--具体依赖的jar包配置文件，删除之后Maven会自动更新lib目录（存放程序需要的jar包）下的内容-->
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.11</version>
      <scope>test</scope>
    </dependency>
  </dependencies>

  <!--项目构建用的东西-->
  <build>
    <finalName>MVNTest</finalName>
    <pluginManagement><!-- lock down plugins versions to avoid using Maven defaults (may be moved to parent pom) -->
      <plugins>
        <plugin>
          <artifactId>maven-clean-plugin</artifactId>
          <version>3.1.0</version>
        </plugin>
        <!-- see http://maven.apache.org/ref/current/maven-core/default-bindings.html#Plugin_bindings_for_war_packaging -->
        <plugin>
          <artifactId>maven-resources-plugin</artifactId>
          <version>3.0.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.8.0</version>
        </plugin>
        <plugin>
          <artifactId>maven-surefire-plugin</artifactId>
          <version>2.22.1</version>
        </plugin>
        <plugin>
          <artifactId>maven-war-plugin</artifactId>
          <version>3.2.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-install-plugin</artifactId>
          <version>2.5.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-deploy-plugin</artifactId>
          <version>2.8.2</version>
        </plugin>
      </plugins>
    </pluginManagement>
  </build>
</project>
```

其中的项目依赖十分强大，我们可以随便在[Maven仓库](https://mvnrepository.com/)中搜一个依赖（这个web模板中是`junit`），直接粘贴进这里面的`dependencies`标签里

![image-20210828001735499](https://s2.loli.net/2021/12/05/VQTWI6F8fd9ryEs.png)

Maven不仅会自动导入所需jar包，甚至会智能导入这个jar包需要依赖的所有jar包（侧边栏可看）

![image-20210828001855185](https://s2.loli.net/2021/12/05/RYwZHy3V7ubzdTQ.png)

也可以在左边项目结构的外部库里看

![image-20210828002041517](https://s2.loli.net/2021/12/05/E2L7cQpvUHtA1wb.png)

同时由于Maven对约定的要求非常严格，之后我们可以会遇到我们自己写的配置文件无法被导出或者生效的问题，此时我们可以在pom的`build`标签中配置一下`resource`节点，使我们的配置文件可以被<a name="build导出问题">导出</a>

```xml
  <build>
        <resources>
            <resource>
                <directory>src/main/resources</directory>
                <includes>
                    <include>**/*.properties</include>
                    <include>**/*.xml</include>
                </includes>
                <filtering>true</filtering>
            </resource>
            <resource>
                <!--使Java目录下不只能够存放.java文件
					如果没有这一条可能会出现某些后缀的无法被导出-->
                <directory>src/main/java</directory>
                <includes>
                    <include>**/*.properties</include>
                    <include>**/*.xml</include>
                </includes>
                <filtering>true</filtering>
            </resource>
        </resources>
    </build>
```

#### Junit

会发现自动创建web模板的时候系统会默认给你导一个Junit的包，事实上Junit就是单元化测试包，导入这个包之后不用写main方法，直接在需要执行的**方法**前面加上`@Test`就可以直接执行某个方法

### Servlet

Servlet是sun公司开发动态web的一门技术，实际上就是一接口，当我们需要使用Servlet的时候，只需要编写一个类实现Servlet接口并把开发好的Java类部署到web服务器中即可

所以我们把实现了Servlet接口的**Java程序**叫做Servlet

#### 准备工作

首先我们需要创建一个普通的Maven项目，并删除其中的src目录，这样的工程就是我们的主工程

之后我们只需要在该项目中新建Module即可

之后我们可以预先将Servlet学习中需要的所有依赖导入（仓库直接搜索即可）

![image-20210828135143340](https://s2.loli.net/2021/12/05/WFcZ3ndvm5arlHC.png)

```xml
<dependencies>
    
    <!-- https://mvnrepository.com/artifact/javax.servlet/javax.servlet-api -->
    <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>javax.servlet-api</artifactId>
        <version>4.0.1</version>
        <scope>provided</scope>
    </dependency>

    <!-- https://mvnrepository.com/artifact/javax.servlet.jsp/javax.servlet.jsp-api -->
    <dependency>
        <groupId>javax.servlet.jsp</groupId>
        <artifactId>javax.servlet.jsp-api</artifactId>
        <version>2.3.3</version>
        <scope>provided</scope>
    </dependency>


</dependencies>
```

> 导入包的时候可能会遇到的问题：
>
> 1. 程序包的位置报红，就在侧边栏手动刷新一下，Maven会自动导入包
>
> 2. 还是报红，就去本地仓库中找一找相对应文件位置的jar包是否存在，比如上面的包
>
>    ![image-20210828140506569](https://s2.loli.net/2021/12/05/L2PFgu8jS59kHnZ.png)
>
>    如果不存在就在Maven仓库中手动下包，手动导入，导入路径和图示一致即可（注意改文件夹名）
>
> 3. 如果还有问题，可以在项目结构中有问题描述，根据要求解决问题
>
>    ![image-20210828140832878](https://s2.loli.net/2021/12/05/xpTyeBuY6RHj8zf.png)

接下来我们要建一个Servlet项目，由于Servlet是外部项目，现在我们需要从原型创建

![image-20210828144953216](https://s2.loli.net/2021/12/05/MxgQ6S8e9nip3qT.png)

下一步的时候发现有一个父项项目

![image-20210828145117148](https://s2.loli.net/2021/12/05/5P3ydmEOjZxqRQ1.png)

之后我们会发现项目结构中原本的项目下出现了新的子项目

![image-20210828151151759](https://s2.loli.net/2021/12/05/6H3jABuCM2Jft8y.png)

如果没出现parent标签就按照如图自己加一个即可

然后我们更改一下`src/main/webapp/WEB-INF/web.xml`的版本信息，默认的xml版本（2.3）过老，我们可以去Tomcat里把所有的东西直接复制过来，去掉那些没什么用的东西来直接更换

```xml
<?xml version="1.0" encoding="UTF-8"?>

<web-app xmlns="https://jakarta.ee/xml/ns/jakartaee"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="https://jakarta.ee/xml/ns/jakartaee
                      https://jakarta.ee/xml/ns/jakartaee/web-app_5_0.xsd"
  version="5.0"
  metadata-complete="true">

</web-app>
```

> 可以看到Tomcat 10里面用了5.0版本的xml

紧接着和之前一样[创建Maven源目录](#创建源目录)

然后在Java的目录下创建一个正常的Java普通类文件，现在只需要实现Servlet接口即可

#### 继承实现类HttpServlet

Sun公司对Servlet接口提供了两个实现类，分别是`HttpServlet`和`GenericServlet`，而前者又是继承后者的，所以我们这里直接**继承**`HttpServlet`即可

查看源码，会发现`HttpServlet`实现了`Servlet`接口中的`service`方法，而这个方法存在`req`和`resp`两个参数，这两个参数也就是我们能够操作请求从而实现动态web的核心

```java
protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    String method = req.getMethod();
    long lastModified;
    if (method.equals("GET")) {
        lastModified = this.getLastModified(req);
        if (lastModified == -1L) {
            this.doGet(req, resp);
        } else {
            long ifModifiedSince = req.getDateHeader("If-Modified-Since");
            if (ifModifiedSince < lastModified) {
                this.maybeSetLastModified(resp, lastModified);
                this.doGet(req, resp);
            } else {
                resp.setStatus(304);
            }
        }
    } else if (method.equals("HEAD")) {
        lastModified = this.getLastModified(req);
        this.maybeSetLastModified(resp, lastModified);
        this.doHead(req, resp);
    } else if (method.equals("POST")) {
        this.doPost(req, resp);
    } else if (method.equals("PUT")) {
        this.doPut(req, resp);
    } else if (method.equals("DELETE")) {
        this.doDelete(req, resp);
    } else if (method.equals("OPTIONS")) {
        this.doOptions(req, resp);
    } else if (method.equals("TRACE")) {
        this.doTrace(req, resp);
    } else {
        String errMsg = lStrings.getString("http.method_not_implemented");
        Object[] errArgs = new Object[]{method};
        errMsg = MessageFormat.format(errMsg, errArgs);
        resp.sendError(501, errMsg);
    }

}
```

看出来这个实现在请求方式不同时执行不同的方法，这意味着我们可以重写这些方法达到个性化操作的目的

```java
public class Demo1 extends HttpServlet {
    
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        PrintWriter writer = resp.getWriter();  // 响应流
        writer.print("Hello World!");
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);    // 由于get和post只是请求实现的不同方式，可以相互调用，业务逻辑都一样
    }
}
```

#### 编写Servlet映射

因为我们写的是Java程序，但是要通过浏览器访问，而浏览器需要连接web服务器，所以我们需要在web服务中注册我们写的Servlet，还需要给他一个浏览器能够访问的路径

这同样是在`web.xml`里面配置

```xml
<web-app xmlns="https://jakarta.ee/xml/ns/jakartaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="https://jakarta.ee/xml/ns/jakartaee
                      https://jakarta.ee/xml/ns/jakartaee/web-app_5_0.xsd"
         version="5.0"
         metadata-complete="true">

    <!--注册Servlet-->
    <servlet>
        <servlet-name>Demo1</servlet-name>
        <servlet-class>com.test.servlet.Demo1</servlet-class>  <!--Servlet文件地址-->
    </servlet>
    <!--Servlet的请求路径-->
    <servlet-mapping>
        <servlet-name>Demo1</servlet-name>   <!--name标签要相对应（但是可以和Servlet文件不一样）-->
        <url-pattern>/hello</url-pattern>  <!--现在我们只需要在前端请求一个/hello，就会走Servlet-->
    </servlet-mapping>
</web-app>
```

然后我们需要和之前一样[配置Tomcat](#在Maven项目中添加Tomcat配置)，此处我们设置应用程序上下文为D1

#### 启动测试

点击运行，会先出现默认的`index.jsp`里面的内容，然后我们在地址栏后加上`/hello`，页面成功的运行了我们提供的Servlet文件

![image-20210828170358921](https://s2.loli.net/2021/12/05/bSjepcyhirUBmlu.png)

然而也有可能会出现500错误的问题

![image-20210828233406219](https://s2.loli.net/2021/12/05/zK38lxB2iCdWypP.png)

原因是Tomcat10内置的Servlet用的是`jakarta`这个名称底下的jar包，而我们pom中的Servlet用的是`javax`底下的jar包，因此当你写的Servlet传入Tomcat的时候，它判定不出来这是个Servlet（包名不一致）

![image-20210828235030485](https://s2.loli.net/2021/12/05/c1y9fh6WIBTl4Xa.png)

遇到这种情况，解决方法也很简单，打开pom，再导入一个`jakarta`依赖即可

```xml
<!--Tomcat10 Servlet依赖-->
<!--jsp的依赖-->
<dependency>
  <groupId>jakarta.servlet.jsp</groupId>
  <artifactId>jakarta.servlet.jsp-api</artifactId>
  <version>3.0.0</version>
  <scope>provided</scope>
</dependency>
<!--jar包的依赖-->
<dependency>
  <groupId>jakarta.servlet</groupId>
  <artifactId>jakarta.servlet-api</artifactId>
  <version>5.0.0</version>
  <scope>provided</scope>
</dependency>
```

注意改完之后我们的Servlet里面的头部包名也要改

![image-20210829110039528](https://s2.loli.net/2021/12/06/j9oUFMOqZLJWaRr.png)

最终成功结果

#### 工作原理

第一次按下启动按钮的时候，先后发生了这些事（仅个人见解）

1. IDEA将我们写的Servlet编译成`.class`文件，同时与进行打包封装成target目录，之后部署到Tomcat目录下，使得Tomcat目录下拥有我们的网站目录

2. IDEA启动Tomcat，同时调用浏览器给`localhost:8080/D1`发送了一个请求

3. Tomcat启动之后就一直在监听8080端口，接收到请求后，其中的web服务器会产生请求头/体和响应头/体，web服务器根据这个响应收集资源`index.jsp`到浏览器

4. 当我们在浏览器后加上`/hello`时，web服务器在`web.xml`里找到了`\hello`内容，但是发现它用了`<servlet>`标签修饰了，意味着他是一个Servlet资源，因此带着请求和响应去目标的Servlet程序

5. Servlet会将请求封装成req参数，我们对req信息进行判断，然后将结果交给resp参数返回，之后resp会解耦重新变成响应交给web服务器，web服务器根据这个响应去寻找相应其他资源丢还浏览器

   > 正常的Java程序Tomcat并不能执行，必须要满足它提供的规范的Java程序才能被执行，而在Java中，一个规范实际上就是一个接口，而Tomcat能执行的就只有实现了Servlet接口的Java程序

   - 其中Servlet根据提供的接口出发，先执行构造方法，然后执行`init()`方法，接着执行`service()`方法

     > ```Java
     > public interface Servlet {
     >  void init(ServletConfig var1) throws ServletException;
     > 
     >  ServletConfig getServletConfig();
     > 
     >  void service(ServletRequest var1, ServletResponse var2) throws ServletException, IOException;
     > 
     >  String getServletInfo();
     > 
     >  void destroy();
     > }
     > ```
   

附上正规说明的Tomcat执行图

![preview](https://pic2.zhimg.com/v2-ce6e39bb02e3c6a2f4eb1e5afaa6e4e6_r.jpg?source=1940ef5c "附图")

#### Mapping

注意到我们在`web.xml`里面曾经加过`<servlet-mapping>`标签

```xml
<servlet-mapping>
    <servlet-name>Demo1</servlet-name>
    <url-pattern>/hello</url-pattern>
</servlet-mapping>
```

其中`url-pattern`即为Servlet匹配虚拟路径（**不是虚拟目录**），其中的路径可以使用通配符`*`，但注意不能用`?`，而且只存在三种情况：

1. `/*`表示默认路径，无论敲什么都匹配（优先级比较低，会先匹配之前有的明确虚拟路径，而且会顶替掉任何直接输入的文件）

   因此最好使用`/`而不是`/*`

2. `/xxx/*`指定通用映射路径（匹配前缀），只要指定路径xxx就一定会进行映射到指定Servlet

3. `*.xxx`表示匹配后缀，只要最后包含`.xxx`就一定会映射到指定Servlet

> `/*`和`/`的区别：
>
> - `< url-pattern>/</url-pattern>  `会匹配到`/login`这样的路径型url，不会匹配到模式为`*.jsp`这样的后缀型url。
>
> - `< url-pattern>/*</url-pattern> `会匹配所有url：路径型的和后缀型的url(包括`/login`,`*.jsp`,`*.js`和*.html等)。

#### 第二个项目

在项目中再新建一个项目，注意，建立新项目的时候要更改Tomcat配置元件

![image-20210829154134738](https://s2.loli.net/2021/12/06/MrQbzodeBpfYxED.png)

如果不新建元件Tomcat还会将这次的项目和之前的项目一起打包在一个文件里，那就糟糕了

顺便把上一个工程元件给删掉，否则每次启动时都要部署两个项目，也不方便

#### ServletContext对象

ServletContext就是上下文环境，web服务器在启动的时候会为每一个web程序都创建一个ServletContext对象，由于它是由web服务器创建的，因此凌驾于所有Servlet之上，它代表了当前的web应用，它也有很多作用

- 共享数据：比如我在一个Servlet中保存的数据，想要在另一个Servlet中拿到，就需要用到ServletContext

  ```java
  public class Demo1 extends HttpServlet {
      @Override
      protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
          ServletContext sc = this.getServletContext();
          String s = "你好";  // 某个数据
          sc.setAttribute("s",s);  // 将一个数据保存在Servlet中，名字为s
      }
  }
  
  public class Demo2 extends HttpServlet {
      @Override
      protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
          ServletContext sc = this.getServletContext();
          String s = (String) sc.getAttribute("s");// 两个Servlet共用一个ServletContext，那边设定完这边就可以取
  
          resp.setContentType("text/html");
          resp.setCharacterEncoding("utf-8");  // 让响应回去不要乱码
          resp.getWriter().print(s);
      }
  }
  ```

  设置`web.xml`之后只需要在浏览器中先访问Demo1后访问Demo2即可

- 请求转发：请求转发并不是重定向，状态码并不会报3xx，因为地址栏路径不变

  ```Java
  public class Demo3 extends HttpServlet {
      @Override
      protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
          ServletContext sc = req.getServletContext();
          sc.getRequestDispatcher("/2").forward(req,resp);
      }
  }
  ```

  <img src="https://s2.loli.net/2021/12/06/91pQbNevAcUMko6.png" alt="image-20210829232016726" style="zoom: 60%;" />

  <img src="https://s2.loli.net/2021/12/06/MkpC2yh4Ls5NGH6.png" alt="image-20210829234335333" style="zoom: 67%;" />

- 读取资源文件（需要用到Properties类）：

  - 创建一个`.properties`文件，将其放置在`resource`资源文件夹中，重启Tomcat

    会发现资源类文件存放在`target/classes/db.properties`中，说明它默认路径是`classpath`(即在classes目录下)

  - ```java
    public class Demo4 extends HttpServlet {
        @Override
        protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
            InputStream is = this.getServletContext().getResourceAsStream("/WEB-INF/classes/db.properties");
            Properties prop = new Properties();
            prop.load(is);
            String usn = prop.getProperty("usn");
            String pwd = prop.getProperty("pwd");
            resp.getWriter().print(usn+":"+pwd);
        }
    }
    ```

#### HttpServletResponse

当web服务器接收到客户端的http请求，针对这个请求，服务端会创建一个代表请求的HttpServletRequest对象和一个代表响应的HttpServletResponse对象，分别代表客户端请求内容和响应信息

应用：

1. 向浏览器输出信息

2. 下载文件：

   - 关于Content-Disposition：

     在常规的 HTTP 应答中，`Content-Disposition` 响应头指示回复的内容该以何种形式展示，是以**内联**的形式（即网页或者页面的一部分），还是以**附件**的形式下载并保存到本地。

     而在 HTTP 场景中，第一个参数或者是 `inline`（默认值，表示回复中的消息体会以页面的一部分或者整个页面的形式展示），或者是 `attachment`（意味着消息体应该被下载到本地；大多数浏览器会呈现一个“保存为”的对话框，将 `filename` 的值预填为下载后的文件名，假如它存在的话）。
   
     ```java
     Content-Disposition: inline
     Content-Disposition: attachment
     Content-Disposition: attachment; filename="filename.jpg"
     ```
   
   -    ```java
        public class Demo5 extends HttpServlet {
            @Override
            protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws IOException {
                // 1.获取下载文件的路径
                String rp = this.getServletContext().getRealPath("/WEB-INF/classes/1.png");  // 注意路径，跟上面的代码一样，最终文件存放位置就是这个
                // 2.获取下载文件的文件名
                String ss = rp.substring(rp.lastIndexOf("\\") + 1);  // 高级用法，检测最后一个\
                // 3.设置文件头，使浏览器能够支持下载我们需要的内容
                resp.setHeader("Content-Disposition","attachment;filename="+ URLEncoder.encode(ss, StandardCharsets.UTF_8));
                // 第一个参数为属性名，后一个参数为下载方式（attachment是以附件形式下载）最后一项是文件名
                // 4.获取下载文件的输入流
                FileInputStream is = new FileInputStream(rp);
                // 5.创建缓冲区
                int len;
                byte[] buf = new byte[1024];
                // 6.获取OutputStream对象
                ServletOutputStream os = resp.getOutputStream();
                // 7.将FileOutputStream写入到buf缓冲区
                while ((len=is.read(buf))>0)
                    os.write(buf,0,len);
                // 8.关闭内容
                is.close();
                os.close();
            }
        }
        ```
   
     > 注意到，`getRealPath()`并没有检错功能，要是你的相对路径写错了那就是写错了，他还是会傻瓜一样把一个没有的文件的绝对路径返回给你
     >
     > 在程序中，相对路径的根目录就是你的网站目录，即放在webapps底下的目录
   
   - 也可以把上一个获取资源类的Servlet改一下实现
   
     ```java
     public class Demo4 extends HttpServlet {
         @Override
         protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
             InputStream is = this.getServletContext().getResourceAsStream("/WEB-INF/classes/1.png");  //这个也是文件的一个路径
             resp.setHeader("Content-Disposition","attachment;filename=1.png");
             int len;
             byte[] buf = new byte[1024];
             ServletOutputStream os = resp.getOutputStream();
             while ((len=is.read(buf))>0)
                 os.write(buf,0,len);
         }
     }
     ```
   
   - 如果文件名为中文，下载的时候无法被显示，此时需要修改响应头的文件名称格式
   
     ```java
     resp.setHeader("Content-Disposition","attachment;filename="+ URLEncoder.encode(ss, StandardCharsets.UTF_8));
     ```

3. 验证码功能：

   ```java
   public class Demo6 extends HttpServlet {
       @Override
       protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws IOException {
           // 浏览器5秒刷新
           resp.setHeader("refresh","5");
           // 在内存中创建一个图片
           BufferedImage bi = new BufferedImage(80,20,BufferedImage.TYPE_INT_RGB);
           // 得到图片
           Graphics2D g = (Graphics2D) bi.getGraphics();
           // 设置图片的背景颜色
           g.setBackground(Color.WHITE);
           g.setColor(Color.BLUE);
           g.setFont(new Font("Consolas",Font.BOLD,20));
           g.drawString(radNum(),0,20);
   
           // 告诉浏览器这个请求用图片方式打开
           resp.setContentType("image/jpg");
           // 网站存在缓存，我们要不让他缓存
           resp.setDateHeader("expires",-1);
           resp.setHeader("Cache-Control","no-cache");
           resp.setHeader("Pragma","no-cache");  // 不缓存
   
           // 将图片写给浏览器
           ImageIO.write(bi,"jpg",resp.getOutputStream());
       }
   
       // 生成四位随机数
       private String radNum(){
           Random random = new Random();
           String s = random.nextInt(9999) + "";
           s = "0".repeat(Math.max(0, 4 - s.length())) + s;  // 这种更巧妙
           // 下面这种方式也可
           // StringBuffer sb = new StringBuffer();
           // for (int i = 4 - s.length(); i > 0; i--) {
           //    sb.append("0");
           //}
           //s = sb.toString() + s;
           return s;
       }
   }
   ```

   > ![20180411092400746](https://s2.loli.net/2021/12/04/4NDcrRGI2mq3S6i.png)

4. **重定向**

   一个web资源收到客户端请求，会通知客户端访问另外一个web资源的过程叫做重定向（用户登录）

   ```java
   public class Demo7 extends HttpServlet {
       @Override
       protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
           resp.sendRedirect("/2/6");  // 会跳到localhost:8080/2/6的地方，注意不能直接输/6
       }
   }
   ```

#### HttpServletRequest

`Request`和`Responce`是对应关系，那边`set`到的意味着这边都可以`get`到，请求中的所有信息都被封装到`HttpServletRequest`中

下面是一个应用了获得请求信息和请求转发的示例

```java
public class Demo7 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        // 获得请求信息
        String usn = req.getParameter("username");
        String pwd = req.getParameter("password");
        String[] ckb = req.getParameterValues("checkbox");
        resp.setContentType("text/html");
        resp.getWriter().print(usn+"\n"+pwd+"\n");
        System.out.println(Arrays.toString(ckb));
        // 请求转发
        req.getRequestDispatcher("/jumpWeb.jsp").forward(req,resp);
    }
}
```

```jsp
<%--jumpWeb.jsp--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>success</title>
</head>
<body>
<p>username : ${pageContext.request.getParameter("username")}</p>
<p>password : ${pageContext.request.getParameter("password")}</p>
<p>checkbox : ${pageContext.request.getParameterValues("checkbox")}</p>
</body>
</html>
```

```jsp
<%--index.jsp--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Test</title>
</head>
<body>

<div style="width: auto;height: auto;text-align: center">
    <h1>Login</h1>
    <%--${pageContext.request.contextPath}代表当前的项目--%>
    <form action="${pageContext.request.contextPath}/7" method="get">
        <label>
            username:
            <input type="text" name="username">
        </label><br>
        <label>
            password:
            <input type="password" name="password">
        </label><br>
        checkbox:
        <input type="checkbox" name="checkbox" value="1">
        <input type="checkbox" name="checkbox" value="2">
        <input type="checkbox" name="checkbox" value="3">
        <input type="checkbox" name="checkbox" value="4">
        <input type="checkbox" name="checkbox" value="5"><br>
        <input type="submit">
    </form>
</div>

</body>
</html>
```

### Cookie

会话：就是用户打开一个浏览器，访问web资源，关闭浏览器的过程

有状态会话：客户端访问某一个曾经访问过的服务端且服务端知道的过程

而如何记录一个客户端访问过服务端，就需要服务端对第一次会话进行保存

保存会话的两种方式，分别就是cookie和session（分别代表客户端技术和服务端技术）

#### 为客户端设置一个cookie

```java
public class Demo1 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        resp.setContentType("text/html");
        req.setCharacterEncoding("utf-8");
        resp.setCharacterEncoding("utf-8");

        PrintWriter out = resp.getWriter();

        // 服务端从客户端获取Cookie
        Cookie[] cookies = req.getCookies();
        // 判断Cookie是否为空，如果为空意味着第一次访问
        if (cookies!=null){
            // 如果存在就遍历cookie取出自己想要的数据
            out.write("你上一次访问的时间：");
            for (Cookie cookie : cookies) {
                if (cookie.getName().equals("time")) {  // 有key就有value
                    long l = Long.parseLong(cookie.getValue());  // 时间戳
                    SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
                    out.write(sdf.format(new Date(l)));
                }
            }
        }else{
            out.write("第一次访问");
        }
        // 服务端给客户端响应一个Cookie
        Cookie cookie = new Cookie("time",System.currentTimeMillis()+"");  // 存一个信息在cookie里
        resp.addCookie(cookie);

    }
}
```

其中在审查元素的Application里可以看到每一个cookie的信息，并可以对cookie进行删除

![image-20210831143502193](https://s2.loli.net/2021/12/06/xnuDrqm5jdpi84Z.png)

然而这样的代码当我们关闭浏览器再启动的时候先前的cookie不会被保存（默认），只需在27行后加上`cookie.setMaxAge(24*60*60);`即可

正由于由于cookie可以设置有效期的原因，导致cookie并不安全，我本地某一个文件夹中，然而现在随着技术的发展，cookie的形式已经渐渐被淘汰了，取而代之的是session

同时Cookie还存在一些别的问题：

- 一个Cookie只能保存一个信息
- 一个web站点可以个浏览器发送多个cookie，最多存放20个cookie
- Cookie大小有限制，一般在4kb左右
- 浏览器有300个cookie上限

### Session

当你通过浏览器访问一个网站时，服务器会给每一个用户都创建一个session对象，一个Session对象独占一个浏览器，只要浏览器没有关闭就一直存在，所以在用户登录之后可以带着自己的用户信息访问整个网站

#### 保存用户的信息/注销用户

```java
public class Demo2 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        resp.setContentType("text/html;charset=utf-8");
        // 得到Session
        HttpSession session = req.getSession();
        session.setAttribute("name","123");
        // 获取session的id
        String id = session.getId();
        // 判断session是不是新创建
        if (session.isNew()){
            resp.getWriter().write("Login done!id="+id);
        }else{
            resp.getWriter().write("your id="+id);
        }
    }
}
```

```java
public class Demo3 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        resp.setContentType("text/html;charset=utf-8");
        // 得到别的Servlet中配置的session属性
        HttpSession session = req.getSession();
        String name = (String) session.getAttribute("name");
        resp.getWriter().write(name);
        session.removeAttribute("name");  // 删除Session属性
        session.invalidate();  // 会删除当前SessionID
    }
}
```

根据代码可以发现，Session同样实现了之前需要ServletContext才能实现的内容，即实现两个Servlet之间实现数据传输，同时通过抓包可以发现，Session的实现在Cookie中保存了ID值

![image-20210831215016885](https://s2.loli.net/2021/12/06/WltjNxSwRF5boZa.png)

#### 原理

一个**浏览器**对应一个Session，同时虽然我们是在`req`参数中拿到的Session，但是这并不意味着Session是客户端创建的，相反，客户端只保留了Session的ID

sessionid是一个会话的key，浏览器第一次访问服务器会在服务器端生成一个session，有一个sessionid和它对应。tomcat生成的sessionid叫做jsessionid。

session在访问tomcat**服务器**HttpServletRequest的getSession(true)的时候**创建**，tomcat的ManagerBase类提供创建sessionid的方法：**随机数+时间+jvmid**；

存储在服务器的内存中，tomcat的StandardManager类将session**存储在内存中**，也可以持久化到file，数据库，memcache，redis等。**客户端只保存sessionid到cookie**中，而不会保存session，session销毁只能通过invalidate或超时，关掉浏览器并不会关闭session。

那么Session在何时创建呢？当然还是在服务器端程序运行的过程中创建的，不同语言实现的应用程序有不同创建Session的方法，而在Java中是通过调用HttpServletRequest的getSession方法（使用true作为参数）创建的。在创建了Session的同时，服务器会为该Session生成唯一的Session id，而这个Session id在随后的请求中会被用来重新获得已经创建的Session；在Session被创建之后，就可以调用Session相关的方法往Session中增加内容了，**而这些内容只会保存在服务器中，发到客户端的只有Session id；当客户端再次发送请求的时候，会将这个Session id带上，服务器接受到请求之后就会依据Session id找到相应的Session**，从而再次使用之。

#### 失效

1. 服务器会把长时间没有活动的Session从服务器内存中清除，此时Session便失效。Tomcat中Session的默认失效时间为20分钟，并不是随着浏览器的关闭消失！

2. 调用Session的invalidate方法。

```java
HttpSession session = request.getSession();
session.invalidate();  // 注销该request的所有session
```

3. session的过期时间是从：从session不活动的时候开始计算，如果session一直活动，session就总不会过期。从该Session未被访问,开始计时; 一旦Session被访问,计时清0;

4. 设置session的失效时间
   - web.xml中
   
     ```xml
     <session-config>
         <!--分钟为单位-->
         <session-timeout>30</session-timeout>
     </session-config>
     ```
   
   - 在程序中手动设置
   
     ```java	
     request.getSession().setMaxInactiveInterval(-1);  // 永不过期，秒为单位
     ```
     
   - tomcat也可以修改session过期时间，在server.xml中定义context时采用如下定义：
   
     ```xml
     <Context path="/livsorder" 
     docBase="/home/httpd/html/livsorder" 　　defaultSessionTimeOut="3600" 
     isWARExpanded="true" 　　
     isWARValidated="false" isInvokerEnabled="true" 　　isWorkDirPersistent="false"/>
     ```

Session和ServletContext的主要区别就是是否能够获取共有资源，Sessio对于资源的处理是个性化的，随着浏览器的不同（用户的不同）而存储不同内容，ServletContext则所有资源共用，每个人访问到的都是相同的内容

### JSP

JSP目前来说已经用的越来越少了，但是仍旧需要进行了解和掌握

最大的特点就是和HTML非常像，同时不同于HTML只能提供静态数据，JSP页面中可以嵌入JAVA代码，提供动态数据

启动Tomcat后，在Appdata目录下的IDEA的路径下，会发现一个`index_jsp.java`的文件，打开来再细研究还能发现他最终继承于Servlet，因此可以说，jsp最终会转变成一个Servlet文件

在JSP中，Java代码要用`<% %>`包裹起来即可直接使用

学习JSP的过程当中，需要导入三个包

```xml
<!-- https://mvnrepository.com/artifact/javax.servlet.jsp/javax.servlet.jsp-api -->
<dependency>
    <groupId>javax.servlet.jsp</groupId>
    <artifactId>javax.servlet.jsp-api</artifactId>
    <version>2.3.3</version>
</dependency>

<!-- https://mvnrepository.com/artifact/javax.servlet/jstl -->
<dependency>
    <groupId>javax.servlet</groupId>
    <artifactId>jstl</artifactId>
    <version>1.2</version>
</dependency>

<!-- https://mvnrepository.com/artifact/taglibs/standard -->
<dependency>
    <groupId>taglibs</groupId>
    <artifactId>standard</artifactId>
    <version>1.1.2</version>
</dependency>
```

#### 语法

- `<%=[Java代码]%>`正常的Java代码嵌入，同时省略了`out.println()`，
- `<%[Java代码]%>`可以写多行代码，不过要自己手动输出

- `out.print`手动在浏览器输出html代码（等于`resp.getWriter().print()`）

- `<%![声明]>`声明某个方法，变量（本质上和前面一个没什么区别）

- `<%----%>`注释

- `<%@[属性]%>`浏览器属性相关

  - `page`页面信息，包括自动刷新，导包，页面编码，及设置错误页面等 

  - `include`提取公共页面，就是网站中所有的网页都有的头部和尾部

    > 但一般会这样用`<jsp:include page='...'/>`，两种方式区别不大
    >
    > 前者将两个页面合二为一，后者是在Servlet中通过静态代码块拼接页面（还是两个页面）

  - `taglib`自定义标签形式

#### 九大内置对象

九大内置对象分别对应着Servlet中的九个对象

- out（JspWriter）：等同与response.getWriter()，用来向客户端发送文本数据；
- config（ServletConfig）：对应“真身”中的ServletConfig；

- page（当前JSP的真身类型）：当前JSP页面的“this”，即当前对象；
- pageContext（PageContext）：页面上下文对象，它是最后一个没讲的域对象；
- exception（Throwable）：只有在错误页面中可以使用这个对象；
- request（HttpServletRequest）：即HttpServletRequest类的对象；
- response（HttpServletResponse）：即HttpServletResponse类的对象；
- application（ServletContext）：即ServletContext类的对象；
- session（HttpSession）：即HttpSession类的对象，不是每个JSP页面中都可以使用，如果在某个JSP页面中设置<%@page session=”false”%>，说明这个页面不能使用session。

#### 四大作用域

会发现pageContext、request、session、application四个对象好多方法都基本一样，说明他们的结构是差不多的，这时候就需要理解他们的作用域问题

```jsp
  <%
    pageContext.setAttribute("1","1");  // 默认只在当前页面有效
    request.setAttribute("2","2");  // 在同一请求中有效
    session.setAttribute("3","3");  // 在一次会话中有效
    application.setAttribute("4","4");  // 在服务器关闭后才失效
    // 这四个作用域层层递进，逐级变高
  %>
```

什么状态需要用什么作用域十分重要，同时注意pageContext和request可以通过请求转发和页面转发在另外一个页面中取到

#### JSP标签/JSTL标签/EL表达式

jsp标签一般用于页面（pageContext）的处理，标准格式为`<jsp:[内容]></jsp:[内容]>`

EL表达式可以获取数据、执行运算、获取Web开发的常用对象，格式为`${[内容]}`

jstl标签库则集合了jsp应用的很多功能，用以弥补HTML标签的不足，格式为`<c:[内容]></c:[内容]>`

> 注意在jsp文件头部加上`<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>`才可以使用jstl标签库（你妈的Tomcat10根本不行，`jakarta.servlet`就没有jstl包，估计给淘汰了）
>
> 如果是Tomcat9报错可以直接将jstl包和standard包导到`Tomcat/lib`目录下，重启项目即可

```jsp
<html>
  <head>
    <title>$Title$</title>
  </head>
  <body>
  <form action="index.jsp" method="get">
    <input type="text" name="username" value="${param.username}">
    <input type="submit">
  </form>
  <c:if test="${param.username=='admin'}">
    <c:out value="ur admin,welcome"/>
  </c:if>
  <c:out value="hello+${param.username}"/>
  </body>
</html>
```

然后发现确实还不如Java代码好用，干，什么神秘jstl，狗都不用

#### JavaBean

JavaBean就是实体类，有特定的写法：

- 必须要有一个无参构造
- 属性必须私有化
- 必须有对应的get/set

一般用来和数据库的字段做映射（[ORM](#ORM)）

一般来说实体类的文件夹可以叫`pojo/entity`等，比较正规

```jsp
3<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
<%--
等价于 Bean bean = new Bean();
bean.getName("123");
...
--%>
<jsp:useBean id="bean" class="com.pojo.Bean" scope="request"/>
<jsp:setProperty name="bean" property="name" value="123"/>
<jsp:setProperty name="bean" property="age" value="1"/>
<jsp:setProperty name="bean" property="gender" value="true"/>

<jsp:getProperty name="bean" property="name"/>
<jsp:getProperty name="bean" property="age"/>
<jsp:getProperty name="bean" property="gender"/>
</body>
</html>
```

```java
public class Bean {
    private String name;
    private int age;
    private boolean gender;

    public Bean() {
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public boolean isGender() {
        return gender;
    }

    public void setGender(boolean gender) {
        this.gender = gender;
    }

    @Override
    public String toString() {
        return "Bean{" +
                "name='" + name + '\'' +
                ", age=" + age +
                ", gender=" + gender +
                '}';
    }
}
```

### MVC三层架构

直到微服务之前都是用这一个架构开发

MVC就是模型（Model/实体类），视图（View/jsp页面），控制器（Controller/Servlet跳转页面）

早期没有MVC架构的时候，用户直接访问控制层，控制层就可以直接操作数据库

![image-20210902005453923](https://s2.loli.net/2021/12/06/sZvCBIHrKg2i75Q.png)

> 然而这样的结构，Servlet直接通过CRUD来操作数据库，使得程序十分臃肿，因为在小小的Servlet中需要处理请求，响应，视图跳转，处理JDBC，处理业务代码，处理逻辑代码等等等等

于是逐渐演变为如今的MVC三层架构，其中的各个部分负责的内容及相互关联情况见下图

![image-20210902003641029](https://s2.loli.net/2021/12/06/zBgiNHW9moLU2rF.png)

Model：

- 业务处理：业务处理（Service）
- 数据持久层：CRUD（Dao）

View：

- 展示数据
- 提供链接发起Servlet请求（a，form，img…）

Controller（Servlet）

- 接受用户的请求：（req：请求参数、Session信息）
- 交给业务层处理对应的代码
- 控制视图跳转

### Filter

过滤器就是用来过滤网站的数据，可以减少很多代码的重复写入

过滤器存在于web服务器和后台资源之间，可以负责过滤掉浏览器的一些垃圾请求，以及进行共用参数初始化

首先也需要先创建一个Java文件，实现Filter接口即可创建一个过滤器

```java
public class Encoding implements Filter {

    // 初始化
    @Override
    public void init(FilterConfig filterConfig) throws ServletException {
        System.out.println("starting...");
    }

    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
        servletRequest.setCharacterEncoding("utf-8");
        servletResponse.setCharacterEncoding("utf-8");
        servletResponse.setContentType("text/html;charset=utf-8");
        filterChain.doFilter(servletRequest,servletResponse);
        // 必须通过Chain调用自己，用以让我们的请求继续走，不然程序运行到这就停住了
    }

    // 销毁
    @Override
    public void destroy() {
        System.out.println("end...");
    }
}
```

然后同样要和Servlet一样配置文件

```xml
<filter>
    <filter-name>filter1</filter-name>
    <filter-class>com.filter.Encoding</filter-class>
</filter>
<filter-mapping>
    <filter-name>filter1</filter-name>
    <url-pattern>/*</url-pattern>
    <!--作用域为所有网页-->
</filter-mapping>
```

#### Listener

监听器在java中和Filter十分相似，同时在运用中其实并不是很常见，同时java中存在着非常多的监听器，其功能都大差不差

比如我们可以运用SessionLisener来监听Session的创建事件，来判断当前网站的在线人数

#### 拦截请求

利用过滤器实现拦截请求功能，涉及到各个界面的转换

前端展示：

- 主页面/登录页面（`index.jsp`）

  ```jsp
  <html>
    <head>
      <title>$Title$</title>
    </head>
    <body>
    <form action="${pageContext.request.contextPath}/1" method="get">
      <input type="text" name="username" value="${param.username}">
      <input type="submit">
    </form>
    </body>
  </html>
  ```

- 被拦截页面（`sys/main.jsp`）

  ```jsp
  <%@ page contentType="text/html;charset=UTF-8" language="java" %>
  <html>
  <head>
      <title>主页</title>
  </head>
  <body>
  <h1>成功进入主页</h1>
  <a href="${pageContext.request.contextPath}/2">注销</a>
  </body>
  </html>
  ```

后端服务：

- 登录判断Servlet（`4/1`）

  ```java
  public class Demo01 extends HttpServlet {
      @Override
      protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
          String username = req.getParameter("username");
          if (username.equals("admin")){  // 登录成功
              req.getSession().setAttribute("USER",req.getSession().getId());
              resp.sendRedirect("/4/sys/main.jsp");
          }else{
              resp.sendRedirect("/4");
          }
      }
  }
  ```

- 注销判断Servlet（`4/2`）

  ```java
  public class Demo02 extends HttpServlet {
      @Override
      protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
          req.getSession().removeAttribute("USER");
          resp.sendRedirect("/4");
      }
  }
  ```

- 拦截页面访问过滤器

  ```java
  public class SysFilter implements Filter {
      @Override
      public void init(FilterConfig filterConfig) throws ServletException {
          Filter.super.init(filterConfig);
      }
  
      @Override
      public void doFilter(ServletRequest request, ServletResponse response, FilterChain filterChain) throws IOException, ServletException {
          HttpServletRequest req = (HttpServletRequest) request;
          HttpServletResponse resp = (HttpServletResponse) response;  // 强转为Http型的才能操作Session
  
          Object user = req.getSession().getAttribute("USER");
          if (user==null) resp.sendRedirect("/4");
          filterChain.doFilter(request, response);
      }
  
      @Override
      public void destroy() {
          Filter.super.destroy();
      }
  }
  ```

这样便可以完成一个简单的跳转登录专属界面的操作

### JDBC

JDBC就是Java到数据库的连接件，负责将各种类型的数据库的数据和web项目进行连接

#### MySQL连接

安装过程[详见](https://www.jb51.net/article/218236.htm)，同时下载[Navicat](https://www.navicat.com.cn/download/navicat-premium)并进行[破解](https://www.jb51.net/database/712269.html)（略），并进行连接

![image-20210903143811296](https://s2.loli.net/2021/12/06/Hg1KwEGLjIlmFvX.png "完成截图")

接着在IDEA中连接数据库，点击侧边栏后点击加号，配置连接参数

![image-20210903153725135](https://s2.loli.net/2021/12/06/gtnb4uRlEfOQTMP.png)

数据库没加载出来就上面的小圆圈刷新多点几遍

添加依赖

```xml
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>8.0.26</version>
</dependency>
```

设置中设置中MySQL的方言

![image-20210905155440023](https://s2.loli.net/2021/12/06/jTCupSHw8mdMN7P.png)

#### 获取数据

```java
public class TestJDBC {
    public static void main(String[] args) throws ClassNotFoundException, SQLException {
        String url = "jdbc:mysql://localhost:3306/demo?useUnicode=true&characterEncoding=utf-8";
        String username = "root";
        String password = "123456";
        // 1.加载驱动
        Class.forName("com.mysql.jdbc.Driver");
        // 2.获取数据库的连接
        Connection connection = DriverManager.getConnection(url, username, password);
        // 3.向数据库发送SQL的对象Statement
        Statement statement = connection.createStatement();
        // 4.编写SQL
        String sql = "select * from users";
        // 5.执行SQL，返回结果集（每一条记录）
        ResultSet resultSet = statement.executeQuery(sql);
        // 遍历记录
        while (resultSet.next()){
            System.out.println("id="+resultSet.getObject("id"));
            System.out.println("name="+resultSet.getObject("name"));
            System.out.println("password="+resultSet.getObject("password"));
        }
        // 6.关闭连接，释放资源（先开的后关）
        resultSet.close();
        statement.close();
        connection.close();
    }
}
```

其中的六个步骤就是JDBC的固定步骤，其中仅有第四步需要脑子体现个性化

其中的3-5步也可以写成

```java
PreparedStatement preparedStatement = connection.prepareStatement(sql);
preparedStatement.executeQuery();
```

使用预编译直接获得想要的内容

注意增删改都是`statement.executeUpdate`，查是`statement.executeQuery`

#### 事务

事务遵循[ACID](https://baike.baidu.com/item/acid/10738)原则，用来保证数据传输或者其他的安全，同时事务有四个状态：

- 开启事务
- 事务提交（`commit()`）
- 事务回滚（`rollback()`）
- 关闭事务

下面程序模拟了事务在实际中的重要性

```java
public class TestJDBC02 {
    public static void main(String[] args) throws Exception{
        Connection connection = null;
        try {
            String url = "jdbc:mysql://localhost:3306/demo?useUnicode=true&characterEncoding=utf-8";
            String username = "root";
            String password = "123456";
            // 加载驱动
            Class.forName("com.mysql.cj.jdbc.Driver");
            // 获取数据库的连接
            connection = DriverManager.getConnection(url, username, password);
            // 通知数据库开启事务，false开启
            connection.setAutoCommit(false);
            String sql = "update users set money = money-100 where id = 1;";
            connection.prepareStatement(sql).executeUpdate();
            // int i = 1/0;
            sql = "update users set money = money+100 where id = 2;";
            connection.prepareStatement(sql).executeUpdate();
            connection.commit();  // 两条语句都成功了才提交语句
        } catch (Exception e) {
            assert connection != null;
            connection.rollback();
            e.printStackTrace();
        }finally {
            assert connection != null;
            connection.close();
        }
    }
}
```

## SSM框架

### Mybatis

Mybatis简单来说就是简化了JDBC的操作，是一款优秀的持久层框架（DAO），目前可以在Github中寻找

> 持久化就是将我们的数据在持久状态和瞬时状态转换的过程，比如我们吃的东西吃不完了就要放冰箱，数据不用了放内存也会丢，要做持久化存储
>
> 而持久层就是完成持久化工作的代码块，与之并列的是服务层（Service）和控制层（Controller），其中各个层与层之间的界限非常明显，体现了分工模块化的思想

学习Mybatis，[官方文档](https://mybatis.org/mybatis-3/zh/)非常重要

#### 简单流程

1. 创建mysql数据表

   ```sql
   CREATE DATABASE `mybatis`;
   USE `mybatis`;
   CREATE TABLE `user`(
   	`id` INT(20) NOT NULL,
   	`name` VARCHAR(30) DEFAULT NULL,
   	`pwd` VARCHAR(30) DEFAULT NULL,
   	PRIMARY KEY(id)
   )ENGINE=INNODB DEFAULT CHARSET=utf8;
   
   INSERT INTO `user`(`id`,`name`,`pwd`) VALUES
   (1,'用户1','1234'),
   (2,'用户2','1234'),
   (3,'用户3','1234');
   ```

2. 新建一个Maven普通的父项目，添加依赖

   ```xml
   <!--导入依赖-->
   <dependencies>
       <dependency>
           <groupId>mysql</groupId>
           <artifactId>mysql-connector-java</artifactId>
           <version>8.0.26</version>
       </dependency>
   
       <dependency>
           <groupId>org.mybatis</groupId>
           <artifactId>mybatis</artifactId>
           <version>3.5.7</version>
       </dependency>
       
       <dependency>
           <groupId>junit</groupId>
           <artifactId>junit</artifactId>
           <version>4.13.2</version>
           <scope>test</scope>
       </dependency>
   </dependencies>
   ```

3. 在父项目中创建子模块

5. 编写mybatis工具类

   > 每个基于 MyBatis 的应用都是以一个 SqlSessionFactory 的实例为核心的。SqlSessionFactory 的实例可以通过 SqlSessionFactoryBuilder 获得。而 SqlSessionFactoryBuilder 则可以从 XML 配置文件或一个预先配置的 Configuration 实例来构建出 SqlSessionFactory 实例。

   ```java
   // 工具类
   // sqlSessionFactory --> sqlSession 工厂模式
   public class MybatisUtils {
       // 获取sqlSessionFactory对象
       private static SqlSessionFactory sqlSessionFactory;
       static {
           try {
               String resource = "mybatis-config.xml";
               InputStream inputStream = null;
               inputStream = Resources.getResourceAsStream(resource);
               sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
           } catch (IOException e) {
               e.printStackTrace();
           }
       }
   
       // 获取sqlSession实例，sqlSession无论是方法还是用法都非常像之前JDBC里面的Connection
       public static SqlSession getSqlSession () {
           return sqlSessionFactory.openSession();
       }
   }
   ```

   ![image-20210905104949398](https://s2.loli.net/2021/12/06/fAGJ76q1l98atpm.png)

6. 在`pojo`目录下编写<a name="User">实体类</a>

   ```java
   public class User {
       private int id;
       private String name;
       private String pwd;
   
       public User() {
       }
   
       public User(int id, String name, String pwd) {
           this.id = id;
           this.name = name;
           this.pwd = pwd;
       }
   
       public int getId() {
           return id;
       }
   
       public void setId(int id) {
           this.id = id;
       }
   
       public String getName() {
           return name;
       }
   
       public void setName(String name) {
           this.name = name;
       }
   
       public String getPwd() {
           return pwd;
       }
   
       public void setPwd(String pwd) {
           this.pwd = pwd;
       }
   
       @Override
       public String toString() {
           return "User{" +
                   "id=" + id +
                   ", name='" + name + '\'' +
                   ", pwd='" + pwd + '\'' +
                   '}';
       }
   }
   ```
   
6. 在`dao`目录下创建Dao接口，并且设置xml配置文件实现接口

   ```java
   public interface UserMapper {  // 注意实体类以Mapper结尾
       List<User> getUserList();
   }
   ```

   ```xml
   <?xml version="1.0" encoding="GBK" ?> <!--注意此处用GBK编码！-->
   <!DOCTYPE mapper
           PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
           "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
   <!--名称空间绑定唯一一个接口，这里等于是实现了这个接口-->
   <mapper namespace="com.test.dao.UserMapper">
       <!--select标签代表的就是查询语句，id对应方法名，resultType就是返回结果的类型，内容就是sql语句-->
       <select id="getUserList" resultType="com.test.pojo.User">
           select *from mybatis.user;
       </select>
   </mapper>
   ```

7. 在resources文件夹下创建`mybatis-config.xml`配置文件，接着编写Mybatis核心配置文件

   ```xml
   <?xml version="1.0" encoding="GBK" ?>
   <!DOCTYPE configuration
           PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
           "http://mybatis.org/dtd/mybatis-3-config.dtd">
   <!--核心配置文件-->
   <configuration>
   
       <environments default="development">
           <environment id="development">
               <transactionManager type="JDBC"/>
               <dataSource type="POOLED">
                   <property name="driver" value="com.mysql.cj.jdbc.Driver"/>
                   <property name="url" value="jdbc:mysql://localhost:3306/mybatis?useSSL=false&amp;useUnicode=true&amp;characterEncoding=UTF-8"/>
                   <property name="username" value="root"/>
                   <property name="password" value="123456"/>
               </dataSource>
           </environment>
       </environments>
       <!--每一个Mapper.xml都要在Mybatis配置文件中注册-->
       <mappers>
           <mapper resource="com/test/dao/UserMapper.xml"/>
       </mappers>
   </configuration>
   ```

8. Junit测试内容

   ```java
   public class UserDaoTest {
       @Test
       public void test(){
           // 获得SqlSession对象
           SqlSession sqlSession = MybatisUtils.getSqlSession();
           // 执行SQL
           UserMapper mapper = sqlSession.getMapper(UserMapper.class);
           for (User user : mapper.getUserList()) {
               System.out.println(user);
           }
           // 关闭SqlSession
           sqlSession.close();
       }
   }
   ```

   > 注意到我们自己编写的`.xml`文件（除了`pom.xml`）如果头部 为`UTF-8`且内部含有中文注释一律会报错，这就非常弱智，解决办法就是改为`UTF8`或者删除所有注释
   >
   > 同时记得要在`pom.xml`中[允许](#build导出问题)构建项目的时候把`*.xml`一起打包，不然这些配置文件会被忽略，不过也可以选择把`*Mapper.xml`放到resource文件夹下，就不需要更改pom文件了
   >
   > ![image-20210919135647274](https://s2.loli.net/2021/12/06/VnWqBgN529xCFPZ.png)
   >
   > > 可以看出这样的文件结构也更加美观，注意在resources目录中创建目录是，目录之间要用`/`分割，同时创建的目录结构必须和java目录下Mapper目录结构相同（如图中`com.test.mapper`）
   
   所有事情完成之后的项目结构（`Dao`和`Mapper`可以互换）
   
   ![image-20210905143842411](https://s2.loli.net/2021/12/06/yq86nXLBYMWTeao.png)

> 有时候我们可能忘记Mybatis这些工作流程，导致自己在配置环境的时候丢三落四，这时候就可以安装一个Mybatis Plugin的插件，他会提示我们Mapper里面的接口方法是否有配置文件匹配（匹配不到就会报错），以及通过可视化箭头快速跳转配置文件实现方法等，方便我们的Mybatis操作
>
> ![image-20210919145340629](https://s2.loli.net/2021/12/06/KZRUk5NLhsWCJ3m.png)

#### CRUD

现在我们只需要对两个Mapper文件和测试文件进行操作，其他的内容一律可以放着不用管了

- 接口

  ```java
  public interface UserMapper {
      // 查询所有用户
      List<User> getUserList();
      // 根据ID查询用户（带参数范例）
      User getUserById(int id);
      // 插入一个新用户（多个参数+insert标签）
      int addUser(User user);
      // 修改用户
      int updateUser(User user);
      // 删除用户
      int delUser(int id);
  }
  ```

- `.xml`配置文件

  ```xml
  <!--名称空间绑定唯一一个接口，这里等于是实现了这个接口-->
  <mapper namespace="com.test.mapper.UserMapper">
      <!--select标签代表的就是查询语句，id对应方法名，resultType就是返回结果的类型，内容就是sql语句-->
      <select id="getUserList" resultType="com.test.pojo.User">
          select *from mybatis.user;
      </select>
      <!--注意传参方式及使用参数内容形式-->
      <select id="getUserById" resultType="com.test.pojo.User" parameterType="int">
          select *from mybatis.user where id = #{id};
      </select>
      <!--insert标签没有resultType选项-->
      <insert id="addUser" parameterType="com.test.pojo.User" >
          insert into mybatis.user (id, name, pwd) values (#{id},#{name},#{pwd})
      </insert>
      <!--下面语句执行成功返回1，未执行或执行失败返回0（不会报错）-->
      <update id="updateUser" parameterType="com.test.pojo.User" >
          update mybatis.user
          set pwd = #{pwd}
          where id = #{id};
      </update>
      <delete id="delUser" parameterType="int">
          delete
          from mybatis.user
          where id=#{id};
      </delete>
  </mapper>
  ```

- 测试文件

  ```java
  public class UserDaoTest {
      // 获得SqlSession对象
      SqlSession sqlSession = MybatisUtils.getSqlSession();
      // 执行SQL
      UserMapper mapper = sqlSession.getMapper(UserMapper.class);
      @Test
      public void testM1(){
          for (User user : mapper.getUserList()) {
              System.out.println(user);
          }
          // 关闭SqlSession
          sqlSession.close();
      }
  
      @Test
      public void testM2(){
          User userById = mapper.getUserById(5);
          System.out.println(userById);
  
          sqlSession.close();
      }
  
      // 注意！增删改需要提交事务！不然根本插不进去！
      @Test
      public void testM3(){
          int i = mapper.addUser(new User(5, "用户5", "12345"));
          System.out.println(i);
          // 提交事务！
          sqlSession.commit();
          this.testM2();
          sqlSession.close();
      }
  
      @Test
      public void testM4(){
          int i = mapper.updateUser(new User(4, "用户4", "1234567"));
          System.out.println(i);
          sqlSession.commit();
          this.testM2();
          sqlSession.close();
      }
  
      @Test
      public void testM5(){
          int i = mapper.delUser(5);
          System.out.println(i);
          sqlSession.commit();
          this.testM2();
          sqlSession.close();
      }
  }
  ```

#### Map查询

当我们创建User对象的时候可能User有几百个属性，这样在我们创建用户的时候就要传一堆参数，这时候就需要用到Map

比如现在添加了一个`updateMUser`方法

```xml
<update id="updateMUser" parameterType="Map">
    update mybatis.user
    set pwd = #{setPwd}
    where id = #{setId};
</update>
```

```java
@Test
public void testM6(){
    Map<String, Object> map = new HashMap<String,Object>();
    map.put("setPwd","123456");
    map.put("setId",4);
    int i = mapper.updateMUser(map);
    System.out.println(i);
    sqlSession.commit();
    this.testM2();
    sqlSession.close();
}
```

这样即可完成相同的操作，甚至不用用到实体类，这样也很好的解决了多个传参的问题

同时利用`%`通配符作为参数传入还可以进行模糊搜索

#### 配置解析

MyBatis 的配置文件包含了会深深影响 MyBatis 行为的设置和属性信息。 配置文档的顶层结构如下：

- properties（属性）
- settings（设置）
- typeAliases（类型别名）
- typeHandlers（类型处理器）
- objectFactory（对象工厂）
- plugins（插件）
- environments（环境配置）
- environment（环境变量）
- transactionManager（事务管理器）
- dataSource（数据源）
- databaseIdProvider（数据库厂商标识）
- mappers（映射器）

##### 环境配置（environments）

MyBatis 可以配置成适应多种环境，这种机制有助于将 SQL 映射应用于多种数据库之中， 现实情况下有多种理由需要这么做。不过**尽管可以配置多个环境，但每个 SqlSessionFactory 实例只能选择一种环境。**

看上面的`environments`内容，我们可以发现主要由两部分组成

- 第一个是**事务管理器（transactionManager）** ，其中规定了使用JDBC的内容

- 第二个是**数据源（dataSource）**，其中**POOLED**属性代表这种数据源的实现利用“池”的概念将 JDBC 连接对象组织起来，避免了创建新的连接实例时所必需的初始化和认证时间。同时支持自定义更多属性

  > - `poolMaximumActiveConnections` – 在任意时间可存在的活动（正在使用）连接数量，默认值：10
  > - `poolMaximumIdleConnections` – 任意时间可能存在的空闲连接数。
  > - `poolMaximumCheckoutTime` – 在被强制返回之前，池中连接被检出（checked out）时间，默认值：20000 毫秒（即 20 秒）
  > - `poolTimeToWait` – 这是一个底层设置，如果获取连接花费了相当长的时间，连接池会打印状态日志并重新尝试获取一个连接（避免在误配置的情况下一直失败且不打印日志），默认值：20000 毫秒（即 20 秒）。
  > - `poolMaximumLocalBadConnectionTolerance` – 这是一个关于坏连接容忍度的底层设置， 作用于每一个尝试从缓存池获取连接的线程。 如果这个线程获取到的是一个坏的连接，那么这个数据源允许这个线程尝试重新获取一个新的连接，但是这个重新尝试的次数不应该超过 `poolMaximumIdleConnections` 与 `poolMaximumLocalBadConnectionTolerance` 之和。 默认值：3（新增于 3.4.5）
  > - `poolPingQuery` – 发送到数据库的侦测查询，用来检验连接是否正常工作并准备接受请求。默认是“NO PING QUERY SET”，这会导致多数数据库驱动出错时返回恰当的错误消息。
  > - `poolPingEnabled` – 是否启用侦测查询。若开启，需要设置 `poolPingQuery` 属性为一个可执行的 SQL 语句（最好是一个速度非常快的 SQL 语句），默认值：false。
  > - `poolPingConnectionsNotUsedFor` – 配置 poolPingQuery 的频率。可以被设置为和数据库连接超时时间一样，来避免不必要的侦测，默认值：0（即所有连接每一时刻都被侦测 — 当然仅当 poolPingEnabled 为 true 时适用）。

##### 属性（properties）

我们可以通过该属性来实现引用配置文件，注意在xml中所有的标签都有其固定的位置

![image-20210905201011162](https://s2.loli.net/2021/12/06/PJDixkTElV5vIyc.png)

其顺序就和上边例举时一样，其中属性必须放在第一个标签位置上

引入了外部配置文件之后，环境内的参数可以直接引用配置文件内的变量

```properties
driver=com.mysql.cj.jdbc.Driver
url=jdbc:mysql://localhost:3306/mybatis?useSSL=false&useUnicode=true&characterEncoding=UTF-8
username=root
password=123456
```

```xml
<!--引入外部配置文件同时优先使用外部文件的内容-->
<properties resource="db.properties"/>

<environments default="development">
    <environment id="development">
        <transactionManager type="JDBC"/>
        <dataSource type="POOLED">
            <property name="driver" value="${driver}"/>
            <property name="url" value="${url}"/>
            <property name="username" value="${username}"/>
            <property name="password" value="${password}"/>
        </dataSource>
    </environment>
</environments>
```

##### 类型别名（typeAliases）

当我们对某一个实体类定义一个别名，使得在项目中的任何位置都可以使用别名来代替完整包名

```xml
<typeAliases>
  	<typeAlias alias="Author" type="domain.blog.Author"/>
    <package name="domain.blog"/>
</typeAliases>
```

如图为该标签的两种用法，其中第二种用法可以通过在实体类前加注解实现自定义别名

```java
@Alias("author")
public class Author {
    ...
}
```

注意第二种方法建议别名使用小写

##### 设置（settings）

这是 MyBatis 中极为重要的调整设置，它们会改变 MyBatis 的运行时行为，但不需要全部掌握

唯一需要知道的就是<a name="日志设置">打印日志</a>

| logImpl | 指定 MyBatis 所用日志的具体实现，未指定时将自动查找。 | SLF4J \| LOG4J \| LOG4J2 \| JDK_LOGGING \| COMMONS_LOGGING \| STDOUT_LOGGING \| NO_LOGGING | 未设置 |
| :------ | ----------------------------------------------------- | :----------------------------------------------------------: | ------ |

##### 映射器（mappers）

之前已经使用过，Mybatis提供了四种方式来实现Mapper的映射

```xml
<!-- 1.使用相对于类路径的资源引用 -->
<mappers>
  <mapper resource="org/mybatis/builder/AuthorMapper.xml"/>
  <mapper resource="org/mybatis/builder/BlogMapper.xml"/>
  <mapper resource="org/mybatis/builder/PostMapper.xml"/>
</mappers>
<!-- 2.使用完全限定资源定位符（URL） -->
<mappers>
  <mapper url="file:///var/mappers/AuthorMapper.xml"/>
  <mapper url="file:///var/mappers/BlogMapper.xml"/>
  <mapper url="file:///var/mappers/PostMapper.xml"/>
</mappers>
<!-- 3.使用映射器接口实现类的完全限定类名 -->
<mappers>
  <mapper class="org.mybatis.builder.AuthorMapper"/>
  <mapper class="org.mybatis.builder.BlogMapper"/>
  <mapper class="org.mybatis.builder.PostMapper"/>
</mappers>
<!-- 4.将包内的映射器接口实现全部注册为映射器 -->
<mappers>
  <package name="org.mybatis.builder"/>
</mappers>
```

第三种方式是通过接口来寻找xml配置文件，但是当我们配置文件的文件名和接口类名不一样，或者两者不在同一个包下的时候，程序无法寻找到需要的配置文件

同时第四种方法同样要求配置文件名和接口类名相同，不然也找不到

同时还要注意通过第一和第二种方式的时候使用`/`来分隔目录和类

#### 生命周期和作用域

当程序开始执行时，建造器（SqlSessionFactoryBuilder）读取`mybatis-config.xml`文件，根据配置建造工厂（SqlSessionFactory），之后工厂通过执行器制造一个个SqlSession，每一个SqlSession可以得到一个SqlMapper，通过Mapper来调用我们创建的一个个方法

- 由于建造器只负责根据配置创建工厂，因此在整个程序中完全可以只作为局部变量出现（工具类）
- 工厂可以看作和数据库的连接池，因为程序需要他不断地提供资源给SqlSession，因此他必须在整个程序中一直存在，跟随程序的结束而结束，且全局仅有一个变量
- SqlSession就是连接到连接池的一个请求，工厂接收到请求给予相应的响应，同时他不是线程安全导致不能被共享，最好将其放入每个需要使用的方法中，随着某个要求的实现而结束，即每次收到一个HTTP请求，就打开一个SqlSession，响应之后及时关闭

#### ResultMap结果集映射

当我们的实体类属性和数据库中的字段名不一致的时候，就需要使用到ResultMap

比如我们将上面的[User](#User)实体类的pwd改为password，之后我们的Mapper会去寻找数据库中和实体类中字段相同的属性（password），然而并没有找到（数据库中只有pwd），就会返回空

```xml
<resultMap id="UserMap" type="user">
    <!--column就是数据库中的字段，property就是实体类中的属性，其中两者相同的属性可以不写-->
    <result column="pwd" property="password"/>
</resultMap>
```

其实就是告诉程序实体类中的什么属性等于数据库中的哪个字段名，同时数据库中总是用`_`来分割单词（由于数据库不区分大小写），而实体类中往往使用驼峰命名法，两者的不一致可以用结果集映射来统一

然而这只是非常简单的情况现实中往往不是这么简单

```xml
<!-- 非常复杂的语句 -->
<select id="selectBlogDetails" resultMap="detailedBlogResultMap">
  select
       B.id as blog_id,
       B.title as blog_title,
       B.author_id as blog_author_id,
       A.id as author_id,
       A.username as author_username,
       A.password as author_password,
       A.email as author_email,
       A.bio as author_bio,
       A.favourite_section as author_favourite_section,
       P.id as post_id,
       P.blog_id as post_blog_id,
       P.author_id as post_author_id,
       P.created_on as post_created_on,
       P.section as post_section,
       P.subject as post_subject,
       P.draft as draft,
       P.body as post_body,
       C.id as comment_id,
       C.post_id as comment_post_id,
       C.name as comment_name,
       C.comment as comment_text,
       T.id as tag_id,
       T.name as tag_name
  from Blog B
       left outer join Author A on B.author_id = A.id
       left outer join Post P on B.id = P.blog_id
       left outer join Comment C on P.id = C.post_id
       left outer join Post_Tag PT on PT.post_id = P.id
       left outer join Tag T on PT.tag_id = T.id
  where B.id = #{id}
</select>
```

这样的查询显得非常头痛，因此我们要使用结果集映射中的其他标签

```xml
<!-- 非常复杂的结果映射 -->
<resultMap id="detailedBlogResultMap" type="Blog">
  <constructor>
    <idArg column="blog_id" javaType="int"/>
  </constructor>
  <result property="title" column="blog_title"/>
  <association property="author" javaType="Author">
    <id property="id" column="author_id"/>
    <result property="username" column="author_username"/>
    <result property="password" column="author_password"/>
    <result property="email" column="author_email"/>
    <result property="bio" column="author_bio"/>
    <result property="favouriteSection" column="author_favourite_section"/>
  </association>
  <collection property="posts" ofType="Post">
    <id property="id" column="post_id"/>
    <result property="subject" column="post_subject"/>
    <association property="author" javaType="Author"/>
    <collection property="comments" ofType="Comment">
      <id property="id" column="comment_id"/>
    </collection>
    <collection property="tags" ofType="Tag" >
      <id property="id" column="tag_id"/>
    </collection>
    <discriminator javaType="int" column="draft">
      <case value="1" resultType="DraftPost"/>
    </discriminator>
  </collection>
</resultMap>
```

看上去非常的复杂，实际上是我们没有意识到为什么会那么复杂，这就需要先理解数据表与表之间的多对一/一对多的关系，并且从简单的问题出发，引申到复杂问题的解决

多对一就是很多学生**关联**着一个老师，一对多就是一个老师**集合**很多学生

看起来没什么区别，实际上对应着数据表于表之间的关系，不妨让我们先创建一个关系表

```sql
CREATE TABLE `teacher` (
  `id` INT(10) NOT NULL,
  `name` VARCHAR(30) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=INNODB DEFAULT CHARSET=utf8;

INSERT INTO teacher(`id`, `name`) VALUES (1, 'teacher');

CREATE TABLE `student` (
  `id` INT(10) NOT NULL,
  `name` VARCHAR(30) DEFAULT NULL,
  `tid` INT(10) DEFAULT NULL,
  PRIMARY KEY (`id`),
  KEY `fktid` (`tid`),
  CONSTRAINT `fktid` FOREIGN KEY (`tid`) REFERENCES `teacher` (`id`)
) ENGINE=INNODB DEFAULT CHARSET=utf8;
INSERT INTO `student` (`id`, `name`, `tid`) VALUES (1, 's1', 1); 
INSERT INTO `student` (`id`, `name`, `tid`) VALUES (2, 's2', 1); 
INSERT INTO `student` (`id`, `name`, `tid`) VALUES (3, 's3', 1); 
INSERT INTO `student` (`id`, `name`, `tid`) VALUES (4, 's4', 1); 
INSERT INTO `student` (`id`, `name`, `tid`) VALUES (5, 's5', 1);
```

其中每一个学生必须对应着唯一一个老师，而每一个老师可以拥有很多学生，也可以没有学生，其中查询某一个学生及他的老师就是多对一查询，查询某一个老师和他所有的学生就是一对多查询

> 这两张表出现了外键，但是在目前，外键的使用是越来越少了

##### 多对一（association标签）

接下来我们要创建两个实体类，为了多对一查询，我们在Student实体类中添加Teacher属性

```java
@Data
@AllArgsConstructor
@NoArgsConstructor
public class Student {
    private int id;
    private String name;
    private Teacher teacher;
}
```

```java
@Data
@AllArgsConstructor
@NoArgsConstructor
public class Teacher {
    private int id;
    private String name;
}
```

```java
SqlSession sqlSession = MybatisUtils.getSqlSession();
StudentMapper mapper = sqlSession.getMapper(StudentMapper.class);
for (Student student : mapper.listStu()) {
    System.out.println(student);
}
```

以上为测试类和实体类

- 通过配置文件执行和以前一样的操作，在前面的步骤和之前一样的情况下，确实能够输出每一个学生的信息，但是会发现其中的teacher字段为空，原因就是当Student实体类的一个属性为另一个Teacher类的时候，程序不知道应该在这个teacher属性里放什么内容

  ```xml
  <mapper namespace="com.test.mapper.StudentMapper">
      <select id="listStu" resultType="student">
          select * from mybatis.student;
      </select>
  </mapper>
  ```

- 换一种方式，可以用sql代码实现，但是他的问题是无法放进xml配置文件中，因为在我们对两张表取了别名之后，每个字段的名称都改了（t.id，s.id），何况id值查出来就有两个，程序不知道到底把student表里的id值放到Student实体类的id属性还是其中的teacher属性里的teacher.id属性中~（尽管我们能立马理解，但是程序比较笨）~

  ```sql
  select *
  from student s,teacher t
  where s.tid=t.id;
  ```

面对上面两种方式都会出现的问题，就需要万能的结果集映射

- 按照查询嵌套处理（从第一种方式出发）

  ```xml
  <!--查询嵌套-->
  <select id="listStuQ" resultMap="StuATea1">
      select * from mybatis.student;
  </select>
  <resultMap id="StuATea1" type="student">
      <!--复杂的属性单独处理
              其中对象:association
              集合:collection-->
      <association property="teacher" column="tid" select="getTeacher"/>
  </resultMap>
  <select id="getTeacher" resultType="teacher">
      select * from mybatis.teacher where id=#{id}
  </select>
  ```

  > 注意此处`getTeacher`选择中似乎并没有传入参数，实际上系统会默认将`association`下的`column`标签传入，且后面sql语句中的`#{id}`中的id可以被换成任何变量值，无论写什么都是对应着该项tid的值，说到底是系统对参数值的智能匹配

  查询嵌套的本质就是在模糊查询（`select * from mybatis.student`）的基础上对无法识别的内含实体类进行额外处理，优点在于不需要为每个数据表的每一项定制别名，但是缺点在于结构层次不明显，由于需要额外再写一条查询，当数据表结构复杂时难以进行阅读维护

- 按照结果嵌套处理（从第二种方式出发）

  ```xml
  <!--结果嵌套-->
  <select id="listStuR" resultMap="StuATea2">
      select s.id as sid,s.name as sn,t.name as tn,t.id as rid
      from mybatis.student s,mybatis.teacher t
      where s.tid=t.id;
  </select>
  <resultMap id="StuATea2" type="Student">
      <result property="id" column="sid"/>
      <result property="name" column="sn"/>
      <association property="teacher" javaType="teacher">
          <result property="name" column="tn"/>
          <result property="id" column="rid"/>
      </association>
  </resultMap>
  ```

  > 注意到其中给student表中的id字段取了sid的别名，那么等于最后查出来呈现的表中同样是以sid为列，因此在做结果集匹配的时候也需要用别名映射

  结果嵌套本质是从最终的sql语句出发，通过结果集解释每一个名称在数据表中的位置，相对来说更符合惯性思维容易理解，且呈现的内容上更加有层次感，但是注意这种方法必须给每一张表的每一个字段添加别名（其中`s.id as sid`中的as可以省略），否则之后的结果集映射无法找到内容

两种解决方式的思路不同但是最终是殊途同归，代表着`association`标签的两种用法，不过最重要先决条件是两张表存在互相联系的外键，且需要查询的内容（`Student`）和内含的实体类（`Teacher teacher`）是多对一的关系

##### 一对多（collection标签）

将上面的实体类稍加修改，创建Teacher类的students属性，从Teacher查询Student，就实现了一对多的查询

```java
@Data
@AllArgsConstructor
@NoArgsConstructor
public class Teacher {
    private int id;
    private String name;
    private List<Student> students;
}
```

- 根据查询嵌套处理

  ```xml
  <mapper namespace="com.test.mapper.TeacherMapper">
      <select id="listTeaQ" resultMap="TeaAStu1">
          select * from mybatis.teacher;
      </select>
      <resultMap id="TeaAStu1" type="teacher">
          <result property="id" column="id"/>
          <!--上一行不能省略，不然后面一行代码会自动仅将数据表id列作为与student表关联的工具而不会作用于teacher实体类的属性
              造成的结果就是id输出为0-->
          <collection property="students" column="id" ofType="student" select="getStu"/>
          <!--虽然数据表中不存在students列，但是与student的关联关系与id有关，column属性就填有关联的字段-->
      </resultMap>
      <select id="getStu" resultType="student">
          select * from mybatis.student where tid=#{id}; # 同样这个id想填啥就填啥
      </select>
  </mapper>
  ```

  其中的`ofType`代表泛型`List`内的内容类型，如果用`javaType`就是`ArrayList`

- 根据结果嵌套处理

  ```xml
  <select id="listTeaR" resultMap="TeaAStu2">
      select t.id rid,t.name tn,s.id sid,s.name sn
      from mybatis.student s,mybatis.teacher t
      where s.tid=t.id;
  </select>
  <resultMap id="TeaAStu2" type="teacher">
      <result property="id" column="rid"/>
      <result property="name" column="tn"/>
      <collection property="students" ofType="student">
          <result property="id" column="sid"/>
          <result property="name" column="sn"/>
      </collection>
  </resultMap>
  ```

可以看出无论是多对一还是一对多只要理解了内容就都不难，举一反三即可，重要的还是理解每一种方法的核心思想

#### 日志

日志就是当我们的程序出现错误的时候，我们想知道究竟哪里错了，这时候就需要日志

之前在配置解析中也有[提到过](#日志设置)，默认是不输出日志的（NO_LOGGING），而我们实际上只用在配置文件中设置中设定日志类型，之后就可以在程序中输出日志

-  STDOUT_LOGGING 标准的日志输出，我们可以直接用，配置进去就行了

  ```xml
  <settings>
      <setting name="logImpl" value="STDOUT_LOGGING"/>
  </settings>
  ```

- LOG4J 是一个强大的日志组件，需要额外导包

  1. ```xml
     <dependency>
         <groupId>org.apache.logging.log4j</groupId>
         <artifactId>log4j-core</artifactId>
         <version>2.14.1</version>
     </dependency>
     ```

  2. 在`resource`目录下创建`log4j.properties`配置文件

     ```properties
     #将等级为DEBUG的日志信息输出到console和file这两个目的地，console和file的定义在下面的代码
     log4j.rootLogger=DEBUG,console,file
     
     #控制台输出的相关设置
     log4j.appender.console = org.apache.log4j.ConsoleAppender
     log4j.appender.console.Target = System.out
     log4j.appender.console.Threshold=DEBUG
     log4j.appender.console.layout = org.apache.log4j.PatternLayout
     log4j.appender.console.layout.ConversionPattern=[%c]-%m%n
     
     #文件输出的相关设置
     log4j.appender.file = org.apache.log4j.RollingFileAppender
     log4j.appender.file.File=./log/log.log
     log4j.appender.file.MaxFileSize=10mb
     log4j.appender.file.Threshold=DEBUG
     log4j.appender.file.layout=org.apache.log4j.PatternLayout
     log4j.appender.file.layout.ConversionPattern=[%p][%d{yy-MM-dd}][%c]%m%n
     
     #日志输出级别
     log4j.logger.org.mybatis=DEBUG
     log4j.logger.java.sql=DEBUG
     log4j.logger.java.sql.Statement=DEBUG
     log4j.logger.java.sql.ResultSet=DEBUG
     log4j.logger.java.sql.PreparedStatement=DEBUG
     ```
     
  3. 之后启动某个测试项目就会生成log文件
  
     ```log
     [DEBUG][21-09-06][org.apache.ibatis.logging.LogFactory]Logging initialized using 'class org.apache.ibatis.logging.log4j.Log4jImpl' adapter.
     [DEBUG][21-09-06][org.apache.ibatis.io.VFS]Class not found: org.jboss.vfs.VFS
     [DEBUG][21-09-06][org.apache.ibatis.io.JBoss6VFS]JBoss 6 VFS API is not available in this environment.
     [DEBUG][21-09-06][org.apache.ibatis.io.VFS]Class not found: org.jboss.vfs.VirtualFile
     [DEBUG][21-09-06][org.apache.ibatis.io.VFS]VFS implementation org.apache.ibatis.io.JBoss6VFS is not valid in this environment.
     [DEBUG][21-09-06][org.apache.ibatis.io.VFS]Using VFS adapter org.apache.ibatis.io.DefaultVFS
     [DEBUG][21-09-06][org.apache.ibatis.io.DefaultVFS]Find JAR URL: file:/D:/STUDY/College/Programme/JAVA/MybatisTest/Demo02/target/classes/com/test/pojo
     [DEBUG][21-09-06][org.apache.ibatis.io.DefaultVFS]Not a JAR: file:/D:/STUDY/College/Programme/JAVA/MybatisTest/Demo02/target/classes/com/test/pojo
     [DEBUG][21-09-06][org.apache.ibatis.io.DefaultVFS]Reader entry: User.class
     [DEBUG][21-09-06][org.apache.ibatis.io.DefaultVFS]Listing file:/D:/STUDY/College/Programme/JAVA/MybatisTest/Demo02/target/classes/com/test/pojo
     [DEBUG][21-09-06][org.apache.ibatis.io.DefaultVFS]Find JAR URL: file:/D:/STUDY/College/Programme/JAVA/MybatisTest/Demo02/target/classes/com/test/pojo/User.class
     [DEBUG][21-09-06][org.apache.ibatis.io.DefaultVFS]Not a JAR: file:/D:/STUDY/College/Programme/JAVA/MybatisTest/Demo02/target/classes/com/test/pojo/User.class
     [DEBUG][21-09-06][org.apache.ibatis.io.DefaultVFS]Reader entry: ����
     ```
  
     前面的[DEBUG]表示调试级别，代表每个步骤的正常调试运行，目前输出的DEBUG级别都是Mybatis内部设置好的，如果我们需要自定义级别，可以在Java文件中编写代码
  
  4. 设置日志信息
  
     ```java
     @Test
     public void testLog(){
         logger.info("info level");
         logger.debug("debug level");
         logger.error("error level");
     }
     ```
  
     ```log
     [INFO][21-09-06][mapper.UserDaoTest]info level
     [DEBUG][21-09-06][mapper.UserDaoTest]debug level
     [ERROR][21-09-06][mapper.UserDaoTest]error level
     ```
  
  5. 之后我们要习惯使用log而不是sout打印输出！

#### 分页

分页的目的就是减少数据的处理量，正常通过sql的limit就可以实现，代码为`SELECT * from user limit 0,2`即可，查询从第一个人开始的往后两个人（不是0-2三个人）

知道分页原理之后，我们就可以通过编写mapper的方式来执行分页sql语句

```xml
<select id="getUserByLimit" parameterType="map" resultMap="UserMap">
    select * from mybatis.user limit #{startIndex},#{pageSize}
</select>
```

```java
@Test
public void testLimit(){
    HashMap<String, Integer> map = new HashMap<>();
    map.put("startIndex",1);
    map.put("pageSize",2);
    System.out.println(mapper.getUserByLimit(map));
    sqlSession.close();
}
```

#### 使用注解开发

对于映射器类来说，还有另一种方法来完成语句映射。 它们映射的语句可以不用 XML 来配置，而可以使用 Java 注解来配置。比如， XML 配置文件可以被替换成如下的配置：

```java
package org.mybatis.example;
public interface BlogMapper {
  @Select("SELECT * FROM blog WHERE id = #{id}")
  Blog selectBlog(int id);
}
```

注意之后需要在配置文件中修改mapper成类名注册的方式

```xml
<mappers>
    <mapper class="com.test.mapper.UserMapper"/>
</mappers>
```

然而这样的注解开发十分局限，比如无法实现之前描述过的实体类和数据项名称不一致的问题，因此注解只用于非常简单的情况

同时因为利用注解进行CRUD，必然无法进行提交操作，这时候回去看看当时创建SqlSession的时候，可以发现`sqlSessionFactory.openSession()`是可以传参的，传入true的时候创建出来的SqlSession可以自动提交

而且注解可以实现多参数的查询，之前引入map操作实际上并不正规，正规的多参写法应该在参数前加上`@param`标签

```java
// 注解多参数查询
@Update("update mybatis.user set pwd = #{psw} where id = #{id};")
int anUpdateUser(@Param("id")int id,@Param("psw") String pwd);
```

看上去确实比之前的方法清爽很多

这样参数的注解之后也可以在xml文件中进行相同配置而不需要`parameterType`参数

```java
int anUpdateUser(@Param("id")int id,@Param("pwd") String pwd);
```

```xml
<update id="anUpdateUser" >
    update mybatis.user set pwd = #{pwd} where id = #{id};
</update>
```

#### Lombok

总之就是简化getter和setter的操作，让代码更加简单，~~但相应的争议也很大（但他妈的用就完了）~~

先在setting内把Lombok的插件装上，然后要去maven导包

```xml
<!-- https://mvnrepository.com/artifact/org.projectlombok/lombok -->
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.18.20</version>
    <scope>provided</scope>
</dependency>
```

之后我们的实体类就可以使用Lombok来简单实现

```java
@Data
@AllArgsConstructor
@NoArgsConstructor
public class User {
    private int id;
    private String name;
    private String password;
}
```

~~操，这寄吧太简单了吧，他妈我爱爆~~

![image-20210906180613693](https://s2.loli.net/2021/12/06/XfjBT28UbDiIgqO.png "项目结构")

#### 动态SQL

动态SQL就是根据不同的条件生成不同的SQL语句，他是Mybatis的一个强大特性

```sql
CREATE TABLE `blog`(
`id` VARCHAR(50) NOT NULL COMMENT '博客id',
`title` VARCHAR(100) NOT NULL COMMENT '博客标题',
`author` VARCHAR(30) NOT NULL COMMENT '博客作者',
`create_time` DATETIME NOT NULL COMMENT '创建时间',
`views` INT(30) NOT NULL COMMENT '浏览量'
)ENGINE=INNODB DEFAULT CHARSET=utf8
```

先创建一个空表

注意到其中`create_time`中存在下划线，而在实体类中我们需要的是驼峰命名法，这时候就需要设置配置文件中的配置信息

![image-20210919123301490](https://s2.loli.net/2021/12/06/zDOnVZmoMwg7S2t.png)

```java
// 实体类
@Data
public class Blog {
    private String id;
    private String title;
    private String author;
    private Date createTime;
    private int views;
}
```

```xml
<mapper namespace="com.test.mapper.BlogMapper">
    <insert id="addBlog" parameterType="blog">
        insert into mybatis.blog (id, title, author, create_time, views)
        values (#{id}, #{title}, #{author}, #{createTime}, #{views});
    </insert>
</mapper>
```

```java
// 工具类
public class IDUtils {
    public static String getID(){
        return UUID.randomUUID().toString().replaceAll("-","");
    }
}
```

```java
// 测试类
public class DSTest {
    @Test
    public void test(){
        SqlSession session = MybatisUtils.getSqlSession();
        BlogMapper mapper = session.getMapper(BlogMapper.class);
        Blog blog = new Blog();
        blog.setId(IDUtils.getID());
        blog.setTitle("1");
        blog.setAuthor("a");
        blog.setViews(9999);
        blog.setCreateTime(new Date());
        mapper.addBlog(blog);
        session.commit();
    }
}
```

以上仅是常规的配置工作

##### if/where标签

```xml
<select id="queryBlogIF" parameterType="map" resultType="blog">
    select *
    from mybatis.blog
    <where>
        <if test="title != null">
            and title = #{title}
        </if>
        <if test="author != null">
            and author = #{author}
        </if>
    </where>
</select>
```

这样就可以在不传入任何参数的时候返回所有值，而在传入拥有`title`或`author`的键值时返回查找到的相应值，注意到*其中的where元素只会在子元素返回任何内容的情况下才插入 “WHERE” 子句。而且，若子句的开头为 “AND” 或 “OR”，where元素也会将它们去除（摘自[帮助文档](https://mybatis.org/mybatis-3/zh/dynamic-sql.html)）*，十分方便

##### choose/when/otherwise语句

当我们只需要多个条件中的选择一个使用时，使用`choose`语句，它有点像 Java 中的 switch 语句

```xml
<select id="queryBlogChoose" resultType="blog">
    select *
    from mybatis.blog
    <where>
        <choose>
            <when test="title != null">
                title = #{title};
            </when>
            <when test="author != null">
                author = #{author}
            </when>
            <otherwise>
                views = #{views}
            </otherwise>
        </choose>
    </where>
</select>
```

会发现比如说传入了title和author，那么程序在判断第一个when的时候就成立，直接跳出choose标签，返回title匹配的字段而不会再判断下面的操作，而if标签每一条都会被判断，取判断结果的交集

##### set标签

set应用在update语句中，代替其中的set语句，同样也会帮我们去除语句**结尾**无用的`,`符号

```xml
<update id="setBlog">
    update mybatis.blog
    <set>
        <if test="title != null">
            title = #{title},
        </if>
        <if test="author != null">
            author = #{author},
        </if>
    </set>
    where id = #{id};
</update>
```

替代后sql语句

```sql
update mybatis.blog SET title = ?, author = ? where id = ?;
Parameters: 4(String), c(String), 99515fc9708d49b9919f484cf53e7a41(String)
```

##### SQL片段

当我们实际应用中可能会出现多个重复使用的SQL语句，使用SQL片段可以将他们提取出来方便复用

```
<sql id="pdTAA">
    <if test="title != null">
        title = #{title},
    </if>
    <if test="author != null">
        author = #{author}
    </if>
</sql>

<update id="setBlog">
    update mybatis.blog
    <set>
        <include refid="pdTAA"/>
    </set>
    where id = #{id};
</update>
```

比如把上面的代码改成这样，也可以正常执行，最好只内含if语句，不然可能无法实现最高程度复用

##### foreach标签

直接用帮助手册上的例子：

```xml
<select id="selectPostIn" resultType="domain.blog.Post">
  SELECT *
  FROM POST P
  WHERE ID in
  <foreach item="item" index="index" collection="list"
      open="(" separator="," close=")">
        #{item}
  </foreach>
</select>
```

这语句就是foreach最基础的做法，其中collection代表一个集合，即外部的传入参数名（比如我们向上面一样用map传入，就需要一个list的键值，类型就为`Arraylist`），这个集合内的每一个元素值就是item（整型，字符串都可），其中元素下标即为index，同时拼接的字符串规则在第二行，表示以`(`起始，以`)`结尾，每一个item之间用`,`相连

比如我们传入参数为`{1,2,3}`这个集合，则最后拼接出来的SQL语句为

```sql
SELECT *
  FROM POST P
  WHERE ID in (1,2,3)
```

#### 缓存

缓存就是让一次查询的结果，暂存在一个可以直接取到的地方，当我们需要再次查询相同数据的时候，直接走缓存即可，免去了走数据库的麻烦，同时也可以解决高并发系统的性能问题

同时在实际应用中，查操作往往远远多于写操作，而对于经常查询并且基本不会改变的数据我们就需要使用缓存使得读写速度加快

Mybatis有非常强大的查询缓存特性，可以非常方便地定制和配置缓存，缓存可以极大的提升查询效率

其中默认定义了两级缓存

- 在默认情况下仅有一级缓存开启，它是SqlSession（即我们工具类里创建的）级别的缓存，也称为本地缓存

- 二级缓存需要手动开启和配置，它是基于namespace级别的缓存
- 同时我们还可以通过实现Cache接口来自定义二级缓存

##### 一级缓存

使用这样的测试代码

```java
@Test
public void test4(){
    Blog blog1 = mapper.queryBlog("1");
    System.out.println(blog1);
    System.out.println("---------------------------");
    Blog blog2 = mapper.queryBlog("1");
    System.out.println(blog2);
    System.out.println(blog1==blog2);
    session.close();
}
```

```log
Checking to see if class com.test.mapper.BlogMapper matches criteria [is assignable to Object]
Opening JDBC Connection
Created connection 443713699.
==>  Preparing: select * from mybatis.blog where title=?;
==> Parameters: 1(String)
<==    Columns: id, title, author, create_time, views
<==        Row: 99515fc9708d49b9919f484cf53e7a41, 1, a, 2021-09-19 13:47:35, 9999
<==      Total: 1
Blog(id=99515fc9708d49b9919f484cf53e7a41, title=1, author=a, createTime=Sun Sep 19 13:47:35 CST 2021, views=9999)
---------------------------
Blog(id=99515fc9708d49b9919f484cf53e7a41, title=1, author=a, createTime=Sun Sep 19 13:47:35 CST 2021, views=9999)
true
Closing JDBC Connection [com.mysql.cj.jdbc.ConnectionImpl@1a7288a3]
Returned connection 443713699 to pool.
```

通过输出日志可以很明显发现，其中的SQL语句只运行了一次，这就代表着第二次对于相同数据的查询并没有重新连接数据库，同时我们还可以发现对于同样的查询数据，他们不仅内容相同，地址也一样，意味着两个数据是从同一个缓存中取出的

> 注意到当取出不同数据或执行增删改的操作的时候，都会刷新缓存，为了使查询到的内容能够时刻保持最新（虽然有时候可能是更新二号用户但是一号用户的缓存也会更新）

除此之外，我们还可以手动清除缓存

```java
@Test
public void test4(){
    Blog blog1 = mapper.queryBlog("1");
    System.out.println(blog1);
    session.clearCache();  // 手动清理缓存
    System.out.println("---------------------------");
    Blog blog2 = mapper.queryBlog("1");
    System.out.println(blog2);
    System.out.println(blog1==blog2);
    session.close();
}
```

```log
Opening JDBC Connection
Created connection 1614133563.
==>  Preparing: select * from mybatis.blog where title=?;
==> Parameters: 1(String)
<==    Columns: id, title, author, create_time, views
<==        Row: 99515fc9708d49b9919f484cf53e7a41, 1, a, 2021-09-19 13:47:35, 9999
<==      Total: 1
Blog(id=99515fc9708d49b9919f484cf53e7a41, title=1, author=a, createTime=Sun Sep 19 13:47:35 CST 2021, views=9999)
---------------------------
==>  Preparing: select * from mybatis.blog where title=?;
==> Parameters: 1(String)
<==    Columns: id, title, author, create_time, views
<==        Row: 99515fc9708d49b9919f484cf53e7a41, 1, a, 2021-09-19 13:47:35, 9999
<==      Total: 1
Blog(id=99515fc9708d49b9919f484cf53e7a41, title=1, author=a, createTime=Sun Sep 19 13:47:35 CST 2021, views=9999)
false
Closing JDBC Connection [com.mysql.cj.jdbc.ConnectionImpl@6035b93b]
Returned connection 1614133563 to pool.
```

可以发现使用了不同的缓存区，最后判断结果为false

所以，一级缓存是默认开启的，而且也关闭不掉，只在一次Session中有效（即在开启->关闭过程中开启），意味着不同的用户会开启不同的缓存（作用域太低），从而导致一级缓存在实际中并不能起到很好的优化效果

##### 二级缓存

当我们需要使用全局缓存时，只需要在设置中开启全局缓存（虽然默认就是true），`mapper.xml`中加一个`<cache/>`即可，当然我们也可以通过参数来制定策略

> 注意不加参数的时候因为不存在策略，因此会报错（NotSerializableException），原因是实体类没有[序列化](#序列化)，只需要实体类实现Serializable接口即可，序列化的目的就是有一个规定的的格式使得对象在被序列化（变成字节码）之后能够正常从一级缓存写入到二级缓存中

二级缓存的存在可以让**被关闭**的一级缓存内容被转移到二级缓存，相对应一个`mapper`（mapper作用域比session高，session是去加载一个mapper，并不是创建了一个mapper）对应一个缓存

同时我们也可以在每一条查询内部设置缓存属性，支持个性化的定制缓存策略

```xml
<cache
  eviction="FIFO"
  flushInterval="60000"
  size="512"
  readOnly="true"/>
```

这个更高级的配置创建了一个 FIFO（[first in first out]先进先出策略） 缓存，每隔 60 秒刷新，最多可以存储结果对象或列表的 512 个引用，而且返回的对象被认为是只读的，因此对它们进行修改可能会在不同线程中的调用者产生冲突。

```log
Opening JDBC Connection
Created connection 1618984457.
==>  Preparing: select * from mybatis.blog where title=?;
==> Parameters: 1(String)
<==    Columns: id, title, author, create_time, views
<==        Row: 99515fc9708d49b9919f484cf53e7a41, 1, a, 2021-09-19 13:47:35, 9999
<==      Total: 1
Blog(id=99515fc9708d49b9919f484cf53e7a41, title=1, author=a, createTime=Sun Sep 19 13:47:35 CST 2021, views=9999)
---------------------------
Cache Hit Ratio [com.test.mapper.BlogMapper]: 0.0
Blog(id=99515fc9708d49b9919f484cf53e7a41, title=1, author=a, createTime=Sun Sep 19 13:47:35 CST 2021, views=9999)
true
```

下面是原理图

![image-20210919201333857](https://s2.loli.net/2021/12/06/szu5HwcKFBmbJpk.png)

##### 自定义缓存（Ehcache）

EhCache 是一个纯Java的进程内缓存框架，具有快速、精干等特点，是Hibernate中默认的CacheProvider

因为在mybatis中用的比较少，这里稍微就提一下

先导包，注意要导mybatis的包，然后在mapper配置文件中添加缓存

```xml
<cache type="com.domain.something.MyCustomCache"/>  <!--这里使用官方文档给出的-->
```

然后配置`ehcache.xml`文件，同样和log4j差不多，网上下一个配置文件，放到resorce文件夹中即可

```xml
<?xml version=1.0 encoding=UTF-8 ?>
<ehcache xmlns:xsi=http://www.w3.org/2001/XMLSchema-instance
         xsi:noNamespaceSchemaLocation=http://ehcache.org/ehcache.xsd
         updateCheck=false>

    <diskStore path=./tmpdir/Tmp_EhCache/>

    <defaultCache
            eternal=false
            maxElementsInMemory=10000
            overflowToDisk=false
            diskPersistent=false
            timeToIdleSeconds=1800
            timeToLiveSeconds=259200
            memoryStoreEvictionPolicy=LRU/>

    <cache
            name=cloud_user
            eternal=false
            maxElementsInMemory=5000
            overflowToDisk=false
            diskPersistent=false
            timeToIdleSeconds=1800
            timeToLiveSeconds=1800
            memoryStoreEvictionPolicy=LRU/>
</ehcache>
```

当然这个不是很重要，今后要学的redis更加牛逼，和spring的配合也更加好！

### Spring

#### 简介

广义上的Spring是一个无比巨大的项目，是一个大杂烩，整合了现有的框架，可能我们一辈子都学不完，我们需要学的只是其中的一个小部分，狭义中的Spring即指Spring Framework，我们所说的SSM框架即指Spring(Framework)、SpringMVC和Mybatis

在2002年的时候推出了Spring框架原型（Interface21），在2004年的时候正式发布了1.0版本，开发者Rod Johnson是一个搞音乐的，Spring框架是针对简化服务器的开发而制作的

它具有一些特点：

- Spring虽然叫做框架，但是实际上也可以看作一个容器
- Spring是一个轻量级的，非入侵式的框架
- 其中有两个核心理念，分别是控制反转（IoC）和面向切面编程（AOP）
- 具有特别优秀的事务处理能力，同时基本上可以整合目前市面上所有的框架

Spring七大模块组成

![20170713150400373](https://s2.loli.net/2021/12/07/iupzQWB7hoy3kFn.png)

#### 第一个程序

1. 第一步还是创建Maven项目并导包，注意要导的是[Spring Web MVC](https://mvnrepository.com/artifact/org.springframework/spring-webmvc)这个包

   ```xml
   <dependency>
       <groupId>org.springframework</groupId>
       <artifactId>spring-webmvc</artifactId>
       <version>5.3.10</version>
   </dependency>
   ```

2. 在java目录下创建`com.test.pojo`目录，并创建实体类`hello.java`，其中比如有一个str的属性

   ```java
   @Data
   public class Hello {
       private String str;
   }
   ```

   > 这里使用了[Lombok](#Lombok)的注解简化操作，手动的话一定要注意添加set方法

3. 在resource文件夹下创建`bean.xml`文件，加上相关头部信息，并在内部对我们刚刚创建的实体类进行属性编辑操作

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
   
       <!--使用Spring创建对象（Bean）-->
       <bean id="hello" class="com.test.pojo.Hello">
           <property name="str" value="Spring"/>
       </bean>
   
   </beans>
   ```

   如果把这行配置文件翻译成我们之前的语言，`id`即为创建的对象名（变量名），`class`就是`new`的对象，每一条`property`就是一个属性信息，包括了`name`属性名和`value`属性值

   > idea甚至贴心的可以自动创建Spring配置的头部文件
   >
   > <img src="https://s2.loli.net/2021/12/06/JfkpSZ1jDGCwoyb.png" alt="image-20210921163032772" style="zoom: 47%;" />

4. 在测试类中创建<a name="应用程序上下文">Spring上下文对象</a>（容器），这也是我们程序中唯一一个new对象

   ```java
   public class MTest {
       @Test
       public void test(){
           // 获取Spring的上下文对象
           ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
           // 我们的对象都在context容器中管理，我们要使用的时候直接从里面取即可
           Hello hello = (Hello) context.getBean("hello");
           System.out.println(hello.toString());
       }
   }
   ```

5. 程序结果为`Hello(str=Spring)`

如果把上面的例子带入的话，程序员不用修改程序，由于配置文件中附带了无论是Dao层还是Service层的所有的注册信息，如今只需要将配置文件交给用户，用户直接通过修改配置文件来达到获取自己需要的东西的效果

> 可能会说这他妈和修改代码有什么区别啊，实际上配置文件是灵活的，代码是需要编译+运行的，修改配置文件能够快速的达到不同的效果，无论是调试还是最终的个性化内容都十分方便
>
> 这即是控制反转（IoC）的理念，接下来我们会逐步理解IoC

#### 配置文件

Spring配置文件中，标签实际上并没有多少，常用的而且有用的就更加少了~（当然是在我们目前阶段）~

- `Alias`给我们的某个bean的id取一个别名

  ```xml
  <alias name="hello" alias="hello2"/>
  ```

- `bean`内大多数属性前面都了解过了，还有一些属性实际上也并不重要

  - `name`也是别名，还可以取多个别名，别名之间在`“”`内用`,`或者空格或者分号分隔都可（听说还有更多分隔符），这直接把`Alias`给干掉了
  - `scope`作用域，常用的有单例模式（singleton）和原型模式（prototype）
    - 单例模式，程序启动时创建，并在之后通过容器get时会永远只用同一个对象
    - 原型模式，与单例模式相反，每次get时都会重新创建一个新的对象（比较占内存)

- `import`一般用于团队开发使用，可以将多个配置文件导入合并为一个，比如有两个`bean.xml`，这时候就可以在其中一个配置文件中通过`import`导入另一个配置文件，这样在引用的时候就可以只引用整合起来的一个即可

#### 控制反转（IoC）

##### 理念推导

在没有出现IoC的时候，我们会先写一个Dao层接口（比如UserDao，里面有一个抽象方法get()），然后在Dao层中创建了几个实现类（比如MySQLUserImpl和OracleUserImpl，其中实现了get()接口，分别用来从不同的数据库中查询用户信息），同时由于Dao层不像用户开放，用户想要查询到自己的信息，我们就要创建一个业务层接口（比如UserService，同样提供了get接口），然后再创几个实现类（UserServiceImpl，里面创建了一个私有的UserDao类型对象属性userDao，并保存着一个new出来的MySQLUserImpl对象，同时实现get()方法，直接调用刚刚new出来的对象的方法即可），于是用户想要使用的时候就可以自己new一个业务层实现类，然后调用实现类的方法

![image-20210921150934356](https://s2.loli.net/2021/12/06/6KErLd5ZzfqCh94.png)

看似好像没有问题，但是当某一天我们需要从另一个数据库中搜索用户的信息时，我们必须对业务层中new代码进行修改（比如变成new OracleUserImpl），虽然后面的代码不用改变，但是当我们拥有很多个Dao层的实现类，并且业务层又存在多个new的时候，对于每一条代码的修改就显得非常麻烦

这时候就需要我们对业务层的内容进行修改，比如说加一个带参数的set()方法，当用户创建出业务层实现类对象后，通过调用set方法并传入自己外部new出来的持久层对象，指定自己想要去哪个数据库查询信息，而业务层中的set()方法直接将传入的对象赋值给自己的私有的属性，从而实现对用户要求的满足

这样的将主动权从业务层到用户的更改模式就是早期的**控制反转**思想

看似好像非常简单，但是一旦放到实际的应用中，我们或许并不能清楚的说出相关原理

##### 创建对象方式

通过测试的方式，我们可以粗略的探究Spring的运行原理

- 首先默认使用无参构造创建的对象，如果实体类中用有参构造覆盖了无参构造，那么运行时就会报错

- 当然Spring也是提供了三种方式来便于我们进行有参构造的初始化

  1. 利用下标进行有参构造，有参构造内第一个参数就是下标0，以此类推

     ``` xml
     <bean id="exampleBean" class="examples.ExampleBean">
         <constructor-arg index="0" value="7500000"/>
         <constructor-arg index="1" value="42"/>
     </bean>
     ```

  2. ~~利用类型进行有参构造（不建议）~~

     ```xml
     <bean id="exampleBean" class="examples.ExampleBean">
         <constructor-arg type="int" value="7500000"/>
         <constructor-arg type="java.lang.String" value="42"/>
     </bean>
     ```

  3. 利用参数名进行有参构造

     ```xml
     <bean id="exampleBean" class="examples.ExampleBean">
         <constructor-arg name="years" value="7500000"/>
         <constructor-arg name="ultimateAnswer" value="42"/>
     </bean>
     ```

- 无论我们想不想要某个bean，在程序启动的时候都已经被实例化了，等着我们去取

##### 依赖注入（DI）

依赖注入是Spring进行控制反转的主要手段，分别有构造器注入，**Set注入**和拓展方式注入

其中的依赖就是bean对象的创建依赖于容器，注入则是bean对象中的所有属性，由容器来注入

- 构造器注入就是之前我们尝试过的有参构造的初始化操作

- Set方式注入是一个非常重要的注入方式，也是DI的本质注入方式

  1. 创建拥有不同类型属性的实体类

     ```java
     @Data
     public class BeanF {
         private String s;
         private BeanS beanS;  // 另外一个自定义类，有一个字符串属性s
         private String[] ss;
         private List<String> l;
         private Map<String,String> m;
         private Properties p;
     }
     ```

  2. 对不同的属性进行注入

     ```xml
     <bean id="beanS" class="com.test.pojo.BeanS"/>
     
     <bean id="beanF" class="com.test.pojo.BeanF">
         <!--1.普通注入-->
         <property name="s" value="1"/>
         <!--2.bean注入-->
         <property name="beanS" ref="beanS"/>
         <!--3.数组注入-->
         <property name="ss">
             <array>
                 <value>a</value>
                 <value>b</value>
                 <value>c</value>
             </array>
         </property>
         <!--4.list集合-->
         <property name="l">
             <list>
                 <value>a</value>
                 <value>b</value>
             </list>
         </property>
         <!--5.map索引-->
         <property name="m">
             <map>
                 <entry key="a" value="1"/>
                 <entry key="b" value="2"/>
             </map>
         </property>
         <!--6.资源类-->
         <property name="p">
             <props>
                 <prop key="a">1</prop>
                 <prop key="b">2</prop>
             </props>
         </property>
     </bean>
     ```

- 拓展注入方式

  当内置的标签内容不能满足我们的要求时，我们可以导入外部的命名空间包，从而获得我们想要的内容

  首先先在配置文件 头部添加p标签网络地址，p标签实际上就是让属性值的快速注入

  ```xml
  xmlns:p="http://www.springframework.org/schema/p"
  ```

  ```xml
  <bean id="beanF" class="com.test.pojo.BeanF" p:s="1" p:beanS-ref="beanS">
  ```

  这样就相当于set注入时例子的第一、二种方式

  与此类似的是c命名空间，代表着的是构造器注入，同样要导入头部文件地址（上面p改成c即可）

  ```xml
  <bean id="beanF" class="com.test.pojo.BeanF" c:s="1" c:_1-ref="beanS">
  ```

  可以看出两者十分类似，代表着通常的两种注入

#### 自动装配

上面我们都是通过手动设置每一个Bean的属性，事实上Spring还支持属性的隐性的自动装配

原理就是Spring会在上下文中自动寻找，并自动给Bean装配属性

比如我们先搭一个父亲拥有两个孩子的环境

```java
@Data
public class Fat {
    private String n;
    private Son son;
    private Dau daughter;
}
```

配置文件也要搞好

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="son" class="com.test.pojo.Son"/>
    <bean id="daughter" class="com.test.pojo.Dau"/>

    <bean id="father" class="com.test.pojo.Fat">
        <property name="n" value="lyb"/>
        <property name="son" ref="son"/>
        <property name="daughter" ref="daughter"/>
    </bean>

</beans>
```

然后我们其实会发现，设置父亲的两个孩子的配置代码似乎是多余的，因为不用说我们也知道两个属性肯定是儿子和女儿

##### 利用配置文件自动装配

于是我们就可以使用bean的自动装配属性

```xml
<bean id="father" class="com.test.pojo.Fat" autowire="byName">
    <property name="n" value="lyb"/>
</bean>
```

会发现也达成了效果，不过有个非常重要的点，这个`byName`属性只会查找和自己对象的属性变量名一样的`beanid`

比如说我的父亲有`Dau daughter`的属性，这时候程序就会在配置文件中寻找是否有id（即变量名）为daughter的bean，有的话就给父亲对象默认加一个`<property name="daughter" ref="daughter"/>`的标签

与此类似的还有`byType`，引用上一个例子，他则会去寻找配置文件中是否有class为Dau的bean，操作相同

`byName`不能解决名字不相同和名字相同但类型不相同的情况，而`byType`则不能解决存在多个相同类型属性和配置文件对同一个实体类创建多个实例化类的情况

##### 注解实现自动装配

事实上，对于到底使用注解还是xml配置，官方文档里有这么一句话

==**The long answer is that each approach has its pros and cons, and, usually, it is up to the developer to decide which strategy suits them better. **==

意思就是各有利弊，但是显然通过注解配置相对来说更为方便

想要使用注解开发，我们要先导入约束，并且配置注解的支持

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:context="http://www.springframework.org/schema/context"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd">

    <context:annotation-config/>

</beans>
```

通过之前的学习，可以看出导入了一个`context`的命名空间，里面的`annotation-config`为我们提供了注解的支持

现在我们使用自动装配也变得十分简单，只需要在`Fat`类的需要自动装配属性前加上`@Autowired`即可

而我们的配置文件就可以变得十分简单

```xml
<bean id="son" class="com.test.pojo.Son"/>
<bean id="daughter1" class="com.test.pojo.Dau"/>

<bean id="father" class="com.test.pojo.Fat"/>
```

```java
@Data
public class Fat {
    private String n;
    @Autowired
    private Son son;
    @Autowired
    private Dau daughter;
}
```

其中注解会默认先匹配`byTye`如果存在类型相同的就使用`byName`，非常智能

实在还是无法自动匹配，就在`@Autowired`注解下加一个`@Qualifier(value = "son")`可以手动指定`beanid`

#### 利用注解配置

上面我们稍微讲了一下自动装配的注解方式，实际上Spring的注解是非常强大的

同时由于配置文件一般需要配置一些核心内容，对于像是bean中注入属性之类往往跟倾向于用注解

同时在Spring4之后，使用注解开发必须导入AOP的包，并导入context的约束

同时我们可能会发现，使用注解之后甚至不需要set方法了，因为注解是通过反射获得类的所有信息，不需要set就能访问到私有属性

```java
@Data
@Component  // 相当于之前的在配置文件中<bean id="user" class.../>这样
// 注意@Component往往专属于实体类层，在dao层往往使用@Repository，controller层和service层往往会使用@Controller和@Service
// 这四个注解名称不一样但是功能完全相同，都是将一个类交由Spring托管
@Scope("singleton")  // 相当于之前设置scope属性
public class User {

    @Value("a")  // 相当于之前的<property name="s" value="a"/>
    private String s;
}
```

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd">

    <!--指定要扫描的包，这个包底下的所有Spring注解都会生效-->
    <context:component-scan base-package="com.test"/>
    <context:annotation-config/>

</beans>
```

#### 使用JavaConfig配置

如果使用基于Java容器配置的方法来配置，就可以完全摆脱xml配置文件，全权交给Java来做配置

在Spring4之后，JavaConfig变成了推荐的配置方式，因为他对比于xml更加灵活

一共有两种方式为一个实体类创建配置：

- 通过`@Bean`实现

  - 在实体类中通过注解添加该类的属性值

    ```java
    @Data
    public class User02 {
        @Value("a")
        private String s;
    }
    ```
    
  - 创建一个Java的配置文件类（官网推荐`AppConfig.java`）

    ```java
    @Configuration
    public class AppConfig {
        @Bean
        public User02 user(){
            return new User02();
        }
    }
    ```

  - 这时候就可以将`AppConfig`看作之前的xml配置文件，`@Bean`注解就是`bean`标签，`user()`方法即为配置文件中的`id`，而`return`返回的内容即为配置文件中的`class`属性

    因此上述类可以化为xml配置文件`<bean id="user" class="com.test.pojo.User02"/>`

  - 于是乎我们可以在测试类中导入这个Java类配置文件

    ```java
    public class MTest {
        @Test
        public void test(){
            AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);
            Object user = context.getBean("user");
            System.out.println("user = " + user);
        }
    }
    ```

    与之前通过`ClassPathXmlApplicationContext`创建容器不同，现在由于没有xml配置文件，我们要使用JavaConfig注解方式`AnnotationConfigApplicationContext`获得应用程序上下文，可以看出`getBean`里面根据对应关系写的便是方法名，用法与先前类似

- 通过`@Conponent`&`@ComponentScan`实现

  - 在利用注解配置时，我们注意到当一个实体类拥有`@Component`注解且被Spring扫描到后，该类就可以自主的成为一个Bean，现在我们想要的就是把原本在xml中做的扫描操作搬到现在的JavaConfig中来

  - 同样先创建实体类，注意要给他标上`Component`注解

    ```java
    @Data
    @Component
    public class User01 {
        @Value("a")
        private String s;
    }
    ```

  - 创建JavaConfig配置文件

    ```java
    @Configuration
    @ComponentScan("com.test.pojo")
    public class AppConfig {
    }
    ```

    可以发配置文件中可以什么都没有，只需要加上`@ComponentScan`注解并指定正确的包名即可

  - 添加测试类

    ```java
    public class MTest {
        @Test
        public void test(){
            AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);
            User01 bean = context.getBean(User01.class);
            System.out.println("bean = " + bean);
        }
    }
    ```

- 注意到上述的代码有一个神秘的`@Configuration`注解，这个注解实际上是`@Component`注解的子注解，意味着它和`@Component`注解拥有一样的功能，也就是可以被Spring扫描功能扫到

- 而在上述代码中我们事实上并没有使用`@Configuration`的功能，因为我们通过传参的形式使得`AnnotationConfigApplicationContext`精准识别到了我们的JavaConfig文件，然而当我们拥有多个JavaConfig时，我们可以通过添加`@Configuration`注解在测试类中扫包获得JavaConfig

  ```java
  AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext();
  context.scan("com.test.config");  // 获取该目录下的所有带@Component及子注解的文件
  context.refresh();  // 注意refresh不能省略，为了将扫到的包能够更新到上下文
  ```

#### 面向切面编程（AOP）

代理模式就是SpringAOP的底层，想要了解AOP就必须了解代理模式

##### 静态代理

静态代理的角色分配及实现

- 抽象角色：一般会用接口或者抽象类解决（租房子）

  ```java
  public interface Rent {
      public void rent();
  }
  ```

- 真实角色：被代理的角色（房东）

  ```java
  public class Host implements Rent{
      @Override
      public void rent() {
          System.out.println("rent");
      }
  }
  ```

- 代理角色：代理真实角色，并且在代理之后做一些附属操作（中介）

  ```java
  public class Proxy implements Rent{
      private Host host;
  
      public Proxy() {
      }
  
      public Proxy(Host host) {
          this.host = host;
      }
  
      @Override
      public void rent() {
          // 在这里添加附属操作
          host.rent();
      }
  }
  ```

- 客户：访问代理对象的人（我）

  ```java
  public class Client {
      public static void main(String[] args) {
          Host host = new Host();
          Proxy proxy = new Proxy(host);
          proxy.rent();
      }
  }
  ```

其中的注意点是无论是中介还是房东实现的都是租房子的接口，同时我们需要将指定的房东信息交给中介，其中中介还可以在`rent()`方法中内联一些其他操作（比如给**我们**看价格，跟**我们**交涉等）

这样就可以保证房东的纯粹性，同时又满足了客户的要求，如果没有中介存在，当我们需要特定需求时就需要频繁修改房东的代码，而这种修改代码的行为破坏了原有稳定的房东类结构，是开发中的大忌

这种一个中介绑定一个房东的模式就叫做静态代理，当然正由于他的一对一特性，当存在多个房东时就需要多个中介，久而久之还是会使得类太多而显得臃肿，这时候就出现了动态代理

同时代理模式还可以从另一个角度理解，当我们已经形成了标准的纵向基础开发层次（dao、service、controller、前端等），却缺乏完整的应用体系时，通过代理模式，我们可以面向基础层次中的某一层，在不改动其基础代码的前提下横向拓展其功能，这就是最重要的AOP思想，也就是面向切面编程

![image-20210923124348208](https://s2.loli.net/2021/12/06/w3OFREuXLagMVkZ.png)

##### 动态代理

上面我们已经引出了动态代理的概念，事实上，动态代理和静态代理在角色分工上相同，但是代理类时动态生成的，不是我们直接写好的

动态代理可以分为两大类，分别是基于接口的动态代理和基于类的动态代理

- 基于接口–JDK动态代理
- 基于类–cglib
- 还可以通过Java字节码实现（但是不适配于Tomcat）

了解动态代理需要知道反射和两个类，分别是`Proxy`和`InvocationHandler`，这些都是JavaSE反射包的类

当我们的Host和Rent文件都不变时，通过实现`InvocationHandler`接口建造一个动态代理工厂，它可以根据我们的需求生成不同的代理对象，对不同的真实对象进行代理

```java
@Data
public class DynamicProxy implements InvocationHandler {
    private Object target;

    public Object getProxy(){
        // 三个参数分别是获取代理类所使用的构造器，代理类需要实现的接口，代理类调用方法时调用谁的invoke方法
        return Proxy.newProxyInstance(this.getClass().getClassLoader(), target.getClass().getInterfaces(),this);
    }
    // 每当我们通过代理类调用一个方法时，就会走这个invoke方法（反射调用），如proxy.rent()时
    @Override
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        // 动态代理的本质就是使用反射机制实现
        return method.invoke(target, args);
    }
}
```

对于invoke方法的使用及反射处理可以参考[前面章节](#反射)，下面通过客户调用动态代理工厂生成指定代理对象

```java
public class Client {
    public static void main(String[] args) {
        // 真实角色
        Host host = new Host();
        // 代理角色：利用代理类的处理程序生成一个代理角色，实现Rent接口
        DynamicProxy dynamicProxy = new DynamicProxy();
        dynamicProxy.setTarget(host);  // 生成的代理类要代理真实角色
        // 生成代理类相当于之前写好的静态代理类
        Rent proxy = (Rent) dynamicProxy.getProxy();
        proxy.rent();
    }
}
```

##### 走进AOP

在软件业，AOP为Aspect Oriented Programming的缩写，意为：面向切面编程，通过预编译方式和运行期间动态代理实现程序功能的统一维护的一种技术。AOP是OOP的延续，是软件开发中的一个热点，也是Spring框架中的一个重要内容，是函数式编程的一种衍生范型。利用AOP可以对业务逻辑的各个部分进行隔离，从而使得业务逻辑各部分之间的耦合度降低，提高程序的可重用性，同时提高了开发的效率。

![20181225093750237](https://s2.loli.net/2021/12/06/Ceg8wjPd6YHoMTc.png)

其中需要了解一些专有名词

- 切面(Aspect): 横切关注点(跨越应用程序多个模块的功能)被模块化的特殊对象；
- 通知(Advice): 切面必须要完成的工作；
- 目标(Target): 被通知的对象；
- 代理(Proxy): 向目标对象应用通知之后创建的对象；
- 连接点（Joinpoint）：程序执行的某个特定位置：如类某个方法调用前、调用后、方法抛出异常后等。连接点由两个信息确定：方法表示的程序执行点；相对点表示的方位。例如 ArithmethicCalculator#add() 方法执行前的连接点，执行点为 ArithmethicCalculator#add()； 方位为该方法执行前的位置；
- 切点（pointcut）：每个类都拥有多个连接点：例如 ArithmethicCalculator 的所有方法实际上都是连接点，即连接点是程序类中客观存在的事务。AOP 通过切点定位到特定的连接点。类比：连接点相当于数据库中的记录，切点相当于查询条件。切点和连接点不是一对一的关系，一个切点匹配多个连接点，切点通过 org.springframework.aop.Pointcut 接口进行描述，它使用类和方法作为连接点的查询条件。

当然这些概念实际上听也听不懂，我们在接下来的项目中在实践中理解

##### 简单实现

首先我们要导一个依赖包

```xml
    <dependencies>
        <!-- https://mvnrepository.com/artifact/org.aspectj/aspectjweaver -->
        <dependency>
            <groupId>org.aspectj</groupId>
            <artifactId>aspectjweaver</artifactId>
            <version>1.9.7</version>
            <scope>runtime</scope>
        </dependency>
    </dependencies>
```

创建服务层接口和实现类

```java
public interface UserService {
    public void add();
    public void delete();
    public void update();
    public void select();
}
```

```java
@Service("service")  // 取个别名，初始名为userServiceImpl太长了
public class UserServiceImpl implements UserService{
    @Override
    public void add() {
        System.out.println("add");
    }

    @Override
    public void delete() {
        System.out.println("delete");
    }

    @Override
    public void update() {
        System.out.println("update");
    }

    @Override
    public void select() {
        System.out.println("select");
    }
}
```

接下来我们在不更改上面两个文件的前提下插入一些我们自己的方法（比如添加日志）

以下提供三种方式实现

1. 使用SpringAPI接口

    ```java
    @Component
    public class BeforeLog implements MethodBeforeAdvice {  // 这个接口专门在方法前使用
        @Override
        public void before(Method method, Object[] args, Object target) throws Throwable {
            System.out.println("BeforeLog.before");
        }
    }
    ```

    ```java
    @Component
    public class AfterLog implements AfterReturningAdvice {  // 这个接口在方法运行完之后使用
        // 可以拿到返回值
        @Override
        public void afterReturning(Object returnValue, Method method, Object[] args, Object target) throws Throwable {
            System.out.println("AfterLog.afterReturning & return result:" + returnValue);
        }
    }
    ```

    接着我们怎么将这两个日志方法切进服务类中的某一个方法中执行呢？

    这时候就需要配置文件发力
    
    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:context="http://www.springframework.org/schema/context"
    xmlns:aop="http://www.springframework.org/schema/aop"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
    https://www.springframework.org/schema/beans/spring-beans.xsd
    http://www.springframework.org/schema/context
    https://www.springframework.org/schema/context/spring-context.xsd
    http://www.springframework.org/schema/aop
    https://www.springframework.org/schema/aop/spring-aop.xsd">
    
    <context:component-scan base-package="com.test"/>
    <context:annotation-config/>
    
    <!--配置AOP-->
    <aop:config>
        <!--切入点: expression 表达式:execution(要执行的位置 格式：修饰词 返回值 列名 方法名 参数)-->
        <aop:pointcut id="pointCut" expression="execution(* com.test.service.UserServiceImpl.*(..))"/>
        <!--这就代表着将某一个类插入到UserServiceImpl的所有方法中，同时不管方法有什么参数（(..)）-->
        <aop:advisor advice-ref="beforeLog" pointcut-ref="pointCut"/>
        <aop:advisor advice-ref="afterLog" pointcut-ref="pointCut"/>
        <!--将我们写好的两个类插入方法-->
    </aop:config>
    
    </beans>
    ```
    
    记得加上头部信息，不然无法识别aop标标签
    
    测试类
    
    ```java
    @Test
    public void test1(){
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("ApplicationContext.xml");
        // 动态代理的是一个接口
        UserService service = context.getBean("service", UserService.class);
        service.add();
    }
    ```
    
2. 自定义类实现

    先随便写一个类，里面定义一些要切入的方法

    ```java
    @Component
    public class Customize {
        public void before(){
            System.out.println("Customize.before");
        }
    
        public void after(){
            System.out.println("Customize.after");
        }
    }
    ```

    然后同样通过配置文件自定义切入位置和切入方法

    ```xml
    <aop:config>
        <aop:aspect ref="customize">
            <!--定义切入点-->
            <aop:pointcut id="point" expression="execution(* com.test.service.UserServiceImpl.*(..))"/>
            <!--定义自定义类中的方法操作位置-->
            <aop:before method="before" pointcut-ref="point"/>
            <aop:after method="after" pointcut-ref="point"/>
        </aop:aspect>
    </aop:config>
    ```

    这种方法相对来说简单，但是功能不如前一种强大（前一种利用反射可以拿到方法的信息）

3. 纯注解实现AOP

    创建配置类

    ```java
    @Aspect  // 标注这个类是一个切面
    @EnableAspectJAutoProxy  // 想要让Aspect注解生效就要加这个注解
    @Component
    public class AnnotationMethod {
        @Pointcut("execution(* com.test.service.UserServiceImpl.*(..))")
        public void pc(){}
    
        @Before("pc()")
        public void before(){
            System.out.println("AnnotationMethod.before");
        }
    
        @After("pc()")
        public void after(){
            System.out.println("AnnotationMethod.after");
        }
    
        @Around("pc()")  // 了解一下Around注解
        public Object around(ProceedingJoinPoint pjp) throws Throwable {
            // 自动在执行方法之前卡住，先执行前部分代码
            Signature signature = pjp.getSignature();
            System.out.println("signature = " + signature);
            System.out.println("AnnotationMethod.around before");
            // 执行完之后会等待一个继续执行方法的指令
            Object proceed = pjp.proceed();// 执行之前的before方法及add方法内容，返回一个Object内容（但我不知道这个Object有什么用）
    // 执行完后目标方法后并发的执行后面的代码和after代码
            System.out.println("AnnotationMethod.around after");
            return proceed;
        }
    }
    ```
    
    直接写测试类
    
    ```java
    @Test
    public void test2(){
        AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext();
        context.scan("com.test");
        context.refresh();
        UserService service = context.getBean("service", UserService.class);
        service.add();
    }
    ```

#### 整合Mybatis

整合需要好多包，除了之前导入的webmvc包以外，还需要

```xml
<dependencies>
    <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis</artifactId>
        <version>3.5.7</version>
    </dependency>
    <dependency>
        <groupId>org.aspectj</groupId>
        <artifactId>aspectjweaver</artifactId>
        <version>1.9.7</version>
    </dependency>
    <!-- https://mvnrepository.com/artifact/org.mybatis/mybatis-spring -->
    <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis-spring</artifactId>
        <version>2.0.6</version>
    </dependency>
    <!-- https://mvnrepository.com/artifact/org.springframework/spring-jdbc -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-jdbc</artifactId>
        <version>5.3.10</version>
    </dependency>
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>8.0.26</version>
    </dependency>
</dependencies>
```

接下来那一个流程走一遍

- 配置文件

  ```xml
  <?xml version="1.0" encoding="GBK" ?>
  <!DOCTYPE configuration
          PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
          "http://mybatis.org/dtd/mybatis-3-config.dtd">
  
  <configuration>
  
      <properties resource="db.properties"/>
  
      <settings>
          <setting name="logImpl" value="STDOUT_LOGGING"/>
          <setting name="mapUnderscoreToCamelCase" value="true"/>
      </settings>
  
      <typeAliases>
          <package name="com.test.pojo"/>
      </typeAliases>
  
      <environments default="development">
          <environment id="development">
              <transactionManager type="JDBC"/>
              <dataSource type="POOLED">
                  <property name="driver" value="${driver}"/>
                  <property name="url" value="${url}"/>
                  <property name="username" value="${username}"/>
                  <property name="password" value="${password}"/>
              </dataSource>
          </environment>
      </environments>
  
      <mappers>
          <package name="com.test.mapper"/>
      </mappers>
  </configuration>
  ```

- 资源文件

  ```properties
  driver=com.mysql.cj.jdbc.Driver
  url=jdbc:mysql://localhost:3306/mybatis?useSSL=false&useUnicode=true&characterEncoding=UTF-8
  username=root
  password=123456
  ```

- 实体类

  ```java
  @Data
  public class User {
      private int id;
      private String name;
      private String pwd;
  }
  ```

- Mapper

  ```java
  public interface UserMapper {
      @Select("select * from mybatis.user")
      public List<User> selectUser();
  }
  ```

- 测试类

  ```java
  public class MTest {
  
      @Test
      public void test() throws IOException {
          InputStream in = Resources.getResourceAsStream("mybatis-config.xml");
          SqlSessionFactory build = new SqlSessionFactoryBuilder().build(in);
          SqlSession session = build.openSession(true);
          UserMapper mapper = session.getMapper(UserMapper.class);
          for (User user : mapper.selectUser()) {
              System.out.println(user);
          }
      }
  
  }
  ```

这样看起来其实也还是挺简单的，看看这文件结构也挺清晰

![image-20210925175326270](https://s2.loli.net/2021/12/06/BNyr5p8nPWCe3wG.png)

然后就让我们正式进入`Mybatis-Spring`中

##### 原始方法

为了实现Spring代理数据源，我们需要通过bean的方式替代mybatis中的环境配置信息

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd
        http://www.springframework.org/schema/aop 
        https://www.springframework.org/schema/aop/spring-aop.xsd">

    <context:property-placeholder location="db.properties"/>
    <!--DataSource：使用Spring的数据源替换Mybatis配置-->
    <bean id="datasource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
        <property name="driverClassName" value="${driver}"/>
        <property name="url" value="${url}"/>
        <property name="username" value="${username}"/>
        <property name="password" value="${password}"/>
    </bean>

</beans>
```

既然这边已经设定了数据源，另一边的环境信息就可以删掉了

```xml
<!--这些都可以删了-->
<environments default="development">
    <environment id="development">
        <transactionManager type="JDBC"/>
        <dataSource type="POOLED">
            <property name="driver" value="${driver}"/>
            <property name="url" value="${url}"/>
            <property name="username" value="${username}"/>
            <property name="password" value="${password}"/>
        </dataSource>
    </environment>
</environments>
```

接着在Spring中创建一个SQLSession工厂，来制造sqlsession

然后我们甚至可以顺便把mybatis-config配置文件中的所有标签都移过来

```xml
    <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
        <property name="dataSource" ref="datasource"/>
        <!--绑定Mybatis配置文件-->
        <property name="mapperLocations" value="com/test/mapper/*"/>
        <property name="typeAliases" value="com.test.pojo.User"/>
    </bean>
```

当然这样并不能解耦配置文件，看着也挺烦的，最好还是在其中引用一下mybatis的配置文件，mybatis相关配置文件还是在相应xml中配置

```xml
<bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
    <property name="dataSource" ref="datasource"/>
    <property name="configLocation" value="mybatis-config.xml"/>
</bean>
```

现在我们有了工厂，下一步就是制造SqlSession

这时候就需要介绍Spring的一个Template（模板）习惯，很多的类在Spring内部都成了一个个`xxxTemplate`，实际上他和原本的类别无二致，我们不需要额外学习别的内容，`SqlSessionTemplate`就是一个例子

```xml
<bean id="sqlSession" class="org.mybatis.spring.SqlSessionTemplate">
    <!--使用构造器注入参数，创建一个SqlSession需要一个工厂，把工厂传进去即可-->
    <constructor-arg ref="sqlSessionFactory"/>
</bean>
```

到此为止，我们其实已经获得了一个SqlSession了（Spring中叫SqlSessionTemplate），接着我们要怎么用这个SqlSession呢，还是通过测试类中的context上下文调用吗？

事实上我们可以再创建一个Mapper类，通过定义方法的方式之后从外部调用方法

```java
@Data
public class UserMapperImpl implements UserMapper{

    // 现在使用SqlSessionTemplate来执行
    private SqlSessionTemplate sqlSession;

    @Override
    public List<User> selectUser() {
        // 从之前的通过测试类配置，到现在整合到一个类中实现
        return sqlSession.getMapper(UserMapper.class).selectUser();
    }
}
```

记得要在Spring中注册Bean

```xml
<bean id="userMaaper" class="com.test.mapper.UserMapperImpl">
    <property name="sqlSession" ref="sqlSession"/>
</bean>
```

终于大功告成，让我们在测试类中测试一下效果

```java
public class MTest {

    @Test
    public void test(){
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("ApplicationContext.xml");
        UserMapper userMapper = context.getBean("userMapper", UserMapper.class);
        for (User user : userMapper.selectUser()) {
            System.out.println("user = " + user);
        }
    }

}
```

> 发现报了一个错，`com.mysql.jdbc.exceptions.jdbc4.MySQLNonTransientConnectionException: Public Key Retrieval is not allowed`
>
> 上网查了一下有些说`db.properties`的url没写对，加个`allowPublicKeyRetrieval=true`之后变成了`Access denied for user 'lenovo'@'localhost' (using password: YES)`这个错误，看来是数据库什么用户信息搞错了，后来发现`username`和`password`是jdbc还不xml里面的两个关键字，编译的时候不会被识别为调用资源类的信息，所以我们只需要把名字改一改即可
>
> ```properties
> driver=com.mysql.cj.jdbc.Driver
> url=jdbc:mysql://localhost:3306/mybatis?useSSL=false&useUnicode=true&characterEncoding=UTF-8
> a.username=root
> a.password=123456
> ```
>
> 记得Spring配置文件里也要改哦

##### 终极简化使用SqlSession

```java
public class UserMapperImpl2 extends SqlSessionDaoSupport implements UserMapper {
    @Override
    public List<User> selectUser() {
        return getSqlSession().getMapper(UserMapper.class).selectUser();
    }
}
```

这时候在配置文件中直接给他注入一个SqlSessionFactory即可

```xml
<bean id="impl2" class="com.test.mapper.UserMapperImpl2">
    <property name="sqlSessionFactory" ref="sqlSessionFactory"/>
</bean>
```

这样直接省略了配置文件中的两步获得SqlSession和类中的一个私有SqlSession方法，获得工厂后直接可以使用，还是比较方便的

#### 声明式事务

[事务](#事务)内容之前提到过，这里就不再提了

*MyBatis-Spring 允许 MyBatis 参与到 Spring 的事务管理中。而不是给 MyBatis 创建一个新的专用事务管理器，MyBatis-Spring 借助了 Spring 中的 `DataSourceTransactionManager` 来实现事务管理*

在Spring中，事务可以通过AOP的方式织入某个程序中，使得在执行指定方法的时候开启/关闭事务

首先要更改Spring配置文件的头部信息，引入事务标签包

```xml
xmlns:tx="http://www.springframework.org/schema/tx"
```

然后在配置文件中配置声明式事务及配置事务通知

配置声明式事务之后，就会在该数据源中建立事务管理系统，当我们需要给数据源传输数据时会经过这个系统判别是否需要创建及提交事务

```xml
<!--配置声明式事务-->
<bean class="org.springframework.jdbc.datasource.DataSourceTransactionManager" id="transactionManager">
    <property name="dataSource" ref="datasource"/>
</bean>
<!--配置事务通知-->
<tx:advice id="txAdvice" transaction-manager="transactionManager">
    <!--想给哪些方法配置事务-->
    <!--配置事务的传播特性-->
    <tx:attributes>
        <tx:method name="delete" propagation="REQUIRED"/>
        <tx:method name="insert" propagation="REQUIRED"/>
        <!--所有方法则用"*"代替方法名-->
    </tx:attributes>
</tx:advice>
```

> 事务通知类型有七种，默认就是REQUIRED
>
> *REQUIRED：支持当前事务，如果当前没有事务，就新建一个事务。这是最常见的选择。* 
>
> *SUPPORTS：支持当前事务，如果当前没有事务，就以非事务方式执行。* 
>
> *MANDATORY：支持当前事务，如果当前没有事务，就抛出异常。* 
>
> *REQUIRES_NEW：新建事务，如果当前存在事务，把当前事务挂起。* 
>
> *NOT_SUPPORTED：以非事务方式执行操作，如果当前存在事务，就把当前事务挂起。* 
>
> *NEVER：以非事务方式执行，如果当前存在事务，则抛出异常。* 
>
> *NESTED：支持当前事务，如果当前事务存在，则执行一个嵌套事务，如果当前没有事务，就新建一个事务。*

同时在Mapper增加增删事务操作

```java
@Component
public interface UserMapper {
    @Select("select * from mybatis.user")
    public List<User> selectUser();
    @Delete("delete from mybatis.user where id=#{id}")
    public int delete(int id);
    @Insert("insert into mybatis.user (id, name, pwd) values (#{id}, #{name}, #{pwd})")
    public int insert(User user);
}
```

从上可以看出，`tx:method`标签应与mapper中需要创建事务的方法一一对应

之后结合AOP方式切入事务内容

```xml
    <!--结合AOP-->
    <!--配置事务切入-->
<!--    <bean class="com.test.mapper.UserMapper"/>-->
    <!--注意这里必须要导入接口类，因为我们的sql代码注解是编写在接口上的，不然Spring无法识别方法-->
    <aop:config>
        <aop:pointcut id="pc" expression="execution(* com.test.mapper.*.*(..))"/>
        <aop:advisor advice-ref="txAdvice" pointcut-ref="pc"/>
    </aop:config>
```

这样就可以实现事务的自动提交及回滚

### SpringMVC

MVC架构之前有所提及，就是模型（Model），视图（View），控制器（Controller）的简写，是一种设计规范

注意到最典型的MVC就是JavaBean+JSP+servlet的模式，分别对应着上面的三层结构

#### 回顾Servlet+Tomcat

创建普通Maven父项目，删除src目录，导入公共依赖

```xml
<dependencies>
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.13.2</version>
        <scope>test</scope>
    </dependency>
    <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>javax.servlet-api</artifactId>
        <version>4.0.1</version>
    </dependency>
    <dependency>
        <groupId>javax.servlet.jsp</groupId>
        <artifactId>javax.servlet.jsp-api</artifactId>
        <version>2.3.3</version>
    </dependency>
    <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>jstl</artifactId>
        <version>1.2</version>
    </dependency>

    <!--Tomcat10 Servlet依赖-->
    <!--jsp的依赖-->
    <dependency>
        <groupId>jakarta.servlet.jsp</groupId>
        <artifactId>jakarta.servlet.jsp-api</artifactId>
        <version>3.0.0</version>
        <scope>provided</scope>
    </dependency>
    <!--jar包的依赖-->
    <dependency>
        <groupId>jakarta.servlet</groupId>
        <artifactId>jakarta.servlet-api</artifactId>
        <version>5.0.0</version>
        <scope>provided</scope>
    </dependency>
</dependencies>
```

创建web子项目，注意先创建一个普通项目再通过添加框架支持添加web框架

![image-20210928121437118](https://s2.loli.net/2021/12/06/6QxlvpZEAGktK8R.png "项目结构")

如图最终效果应该是在web目录上有一个蓝色小点点，Tomcat就是通过它来确认是否为web项目

之后让我们创建一个简单的由主页传参给Sevlet并返回到指定页面的小项目

- 让我们从Servlet开始（Controller）

  ```java
  public class Demo1 extends HttpServlet {
      @Override
      protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
          // 获取前端参数
          String method = req.getParameter("method");
          if (method.equals("add")){
              req.getSession().setAttribute("msg","add");
          }
  
          // 调用业务层
          req.getRequestDispatcher("/WEB-INF/jsp/test.jsp").forward(req,resp);
      }
  }
  ```

  之后记得再web.xml中注册内容

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <web-app xmlns="https://jakarta.ee/xml/ns/jakartaee"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="https://jakarta.ee/xml/ns/jakartaee https://jakarta.ee/xml/ns/jakartaee/web-app_5_0.xsd"
           version="5.0">
  
      <servlet>
          <servlet-name>demo01</servlet-name>
          <servlet-class>com.test.Demo1</servlet-class>
      </servlet>
      <servlet-mapping>
          <servlet-name>demo01</servlet-name>
          <url-pattern>/1</url-pattern>
      </servlet-mapping>
  
      <session-config>
          <session-timeout>15</session-timeout>
      </session-config>
  
      <welcome-file-list>
          <welcome-file>index.jsp</welcome-file>
      </welcome-file-list>
  
  </web-app>
  ```

- 然后我们在`/WEB-INF/jsp/test.jsp`下开始设计返回目标的jsp（View）

  ```jsp
  <%@ page contentType="text/html;charset=UTF-8" language="java" %>
  <html>
  <head>
      <title>Title</title>
  </head>
  <body>
      ${msg}
  </body>
  </html>
  ```

- 之后是请求页面（index.jsp）

  ```jsp
  <%@ page contentType="text/html;charset=UTF-8" language="java" %>
  <html>
    <head>
      <title>$Title$</title>
    </head>
    <body>
      <form action="1" method="get">
        <label>
          <input type="text" name="method">
        </label>
        <input type="submit">
      </form>
    </body>
  </html>
  ```

- 然后配置Tomcat环境和建立应用程序上下文，启动项目，在地址栏输入`http://localhost:8080/1?method=add`或者在表单填入add再提交即可看到我们的test.jsp页面

搞清楚这些底层的内容之后，我们就开始正式的进入SpringMVC的学习中

#### 简单入门

SpringMVC有这些特点

- 轻量级，简单易学
- 高效，基于请求和响应的MVC框架
- 和Spring兼容性好，无缝结合
- 约定大于配置
- 功能强大（RESTful，数据验证，格式化，本地化，主题）
- 简介灵活

Spring的web框架围绕着DispatcherServlet设计，它可以理解为一个管理各种Servlet的调度器，它将请求分发到不同的处理器，同时它的本质也是一个Servlet

进入SpringMVC之后，注解就大于配置了，任何情况下都最好使用注解进行各种控制

口说无凭，不如先通过自己的操作动手搭建一个SpringMVC环境

1. 配置`web.xml`内容

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <web-app xmlns="https://jakarta.ee/xml/ns/jakartaee"
            xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xsi:schemaLocation="https://jakarta.ee/xml/ns/jakartaee https://jakarta.ee/xml/ns/jakartaee/web-app_5_0.xsd"
            version="5.0">
   
       <servlet>
           <servlet-name>springmvc</servlet-name>
           <!--导入DispatcherServlet，用它来管理我们的Servlet-->
           <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
           <!--为DispatcherServlet关联一个配置文件-->
           <init-param>
               <param-name>contextConfigLocation</param-name>
               <!--于是下一步我们需要创建一个配置文件
                   注意：classpath指的就是resource目录-->
               <param-value>classpath:springmvc-servlet.xml</param-value>
           </init-param>
           <load-on-startup>1</load-on-startup>
       </servlet>
       <!--使得DispatcherServlet对所有页面生效（类似过滤器？）-->
       <servlet-mapping>
           <servlet-name>springmvc</servlet-name>
           <url-pattern>/</url-pattern>
       </servlet-mapping>
   
   </web-app>
   ```

2. 由于上面导入了某xml，所以下一步是在resource目录下配置Spring的配置文件`springmvc-servlet.xml`

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
   
       <bean class="org.springframework.web.servlet.handler.BeanNameUrlHandlerMapping"/>
       <bean class="org.springframework.web.servlet.mvc.SimpleControllerHandlerAdapter"/>
   
       <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver" id="resolver">
           <!--前缀，因为我们请求的路径将不会是一个完整的路径-->
           <property name="prefix" value="/WEB-INF/jsp/"/>
           <!--后缀，程序会自动给我们的名字拼接上这个前后缀-->
           <property name="suffix" value=".jsp"/>
       </bean>
   
       <!--Handler-->
       <bean id="/t" class="com.test.controller.CDemo1"/>
   
   </beans>
   ```

3. 然后我们的配置工作暂告一段落，接下来我们需要创建控制类，实现Controller接口

   ```java
   public class CDemo1 implements Controller {
       @Override
       public ModelAndView handleRequest(HttpServletRequest request, HttpServletResponse response) {
           // ModelAndView模型和视图
           ModelAndView mv = new ModelAndView();
           // 封装对象啊那个，放在ModelAndView中
           mv.addObject("msg","Demo1");
           // 封装要跳转的视图，同样放在ModelAndView中
           mv.setViewName("test");  // /WEB-INF/jsp/test.jsp
           return mv;
       }
   }
   ```

4. 最后在把上一个项目的jsp文件拿过来即可，最终呈现的文件效果如图

   ![image-20210928162159966](https://s2.loli.net/2021/12/06/vZCytWxRUgF59q8.png)

> 由于我们是在Maven空项目中添加的框架支持，实际上并不算是完全的web项目，因此项目结构中并没有lib目录，Tomcat也无法从我们的lib目录中寻找到我们依赖的包（包括Springwebmvc等），无法正确识别我们的请求，因此在我们启动项目发送请求后会报404错误，这时候就需要我们手动创建lib目录并导包
>
> 先打开项目结构，选择工件
>
> ![image-20210928163823440](https://s2.loli.net/2021/12/06/qPi1Aw5IgLb6aGc.png)

接着启动项目，请求`http://localhost:8080/t`查看是否正常跳转到damo1

![image-20210928164129520](https://s2.loli.net/2021/12/06/gpX4wmORW8GLNJM.png)



#### 原理分析

在完成了这个项目之后，我们来通过一张图清晰的了解SpringMVC的工作原理

![image-20210928133253545](https://s2.loli.net/2021/12/06/AeOHjF6wGUtzR9X.png)

如图当一个用户发送请求时（比如说`/t`），请求会交给前端控制器（DispatcherServlet，即`web.xml`中编写的内容），之后前端控制器会向他自己绑定的配置文件中（springmvc-servlet.xml）通过HandlerMapping（Spring配置文件中设定的bean）查询需要的处理器（Handler）信息并返回结果，然后查到了我们创建的控制类处理器（CDemo1），于是通过HandlerAdapter（也是Spring配置文件中创建的bean）去执行控制类，在控制类中我们对请求进行了简单的处理（比如携带msg键值，设置视图名字为demo1），之后返回给前端控制器一个ModelAndView（mv），前端控制器再根据ViewResolver（Spring配置文件中的bean）对返回来的ModelAndView进行装饰（比如加上前缀后缀），并渲染成响应数据返回给用户

但是这样开发还是比较麻烦，每编写一个控制类都需要去Spring当中注册一个bean，一点都不智能，这时候就需要强大的注解功能出马

#### 注解实现

在原有的配置文件中，我们只需要修改Spring配置文件中的内容，为该SpringMVC项目添加注解支持

```xml
<context:component-scan base-package="com.test.controller"/>
<mvc:default-servlet-handler/>
<mvc:annotation-driven/>
```

第一个标签前面使用过，是扫包标签

第二个标签代表着启用mvc默认的Servlet构建Handler程序，意味着像是css、js等静态资源请求不会将其交给前端控制器，避免了直接请求静态资源导致的找不到内容

> 如果交给前端控制器，他又会去匹配配置文件中的处理器（Handler），然而我们并没有配置直接请求静态资源的处理器，但是这个静态资源又是确实存在的，于是当然会找不到内容

第三个标签表示启动支持mvc注解驱动，其中自动配置了之前的HandlerMapping和HandlerAdapter

因此之前配置的两个bean都可以删去了！

之后我们修改对应的控制类内容，实现利用注解开发

```java
@Controller
public class Demo1 {
    @RequestMapping("/t")  // 请求/t的时候走这个控制器
    public String test(Model model){
        // 封装数据
        model.addAttribute("msg","Demo1!");
        return "test";  // 返回的字符串就是转发到的jsp文件名字
    }
}
```

你可能不相信，但是确实这样就已经可以运行了

会发现现在的控制类中被传入了Model来植入携带信息，而用返回值携带View视图名字，等于说在之前的图中的前端控制器和处理器之间被中间又被`annotation-driven`又加了一层，用以使ModelAndView拆分成Model和View模块再只将Model传到我们的控制类中，实现了进一步的解耦

#### 数据处理

前端传参的时候我们后端需要对请求的参数进行接收和处理，这时候就需要在控制类中添加参数接收内容

```java
@Controller
public class Demo2 {
    @RequestMapping("/add")
    public String test1(int a, int b, Model model){  // 前端给我们传的参数必须跟这里参数保持一致
        int res = a + b;
        model.addAttribute("msg","结果："+res);
        return "test";
    }
}
```

之后通过`/add?a=1&b=2`来传参，a和b的值就会被传到我们的控制类

![image-20210929192220523](https://s2.loli.net/2021/12/06/LsuGD2fX4UjMyaV.png)

如果不想让前端和我们的参数名保持一致，就需要`@RequestParam`注解

```java
 @Controller
 public class Demo2 {
     @GetMapping("/t2")
     public String test1(@RequestParam("a1") int a,@RequestParam("b1") int b, Model model){ 
         int res = a + b;
         model.addAttribute("msg","结果："+res);
         return "test";
     }
 }
```

这时候就需要`/add?a1=1&b1=2`传参，但是并没有什么意义

实际开发中，前端传过来的往往不是某一个参数而是一个对象，这时候我们就需要创建实体类接收

比如我们有一个User对象

```java
@Data
@AllArgsConstructor
@NoArgsConstructor
public class User {
    private int id;
    private String name;
}
```

如果把实体类作为参数，当前端传参的时候就需要对每一个参数都分别传送，Spring会将其打包成对象

```java
@Controller
public class Demo4 {
    @GetMapping("/t4")
    public String test(User user, Model model){
        model.addAttribute("msg",user.getId()+" "+user.getName());
        return "test";
    }
}
```

这时候就需要这样传入参数`http://localhost:8080/t4?id=1&name=1`

不过注意到，并不建议这样进行传参，因为这样就无法运用Restful风格和别名简化传参

会发现当传入数据不太多时，直接

#### RestFul风格

Restful风格就是一个URL显示的风格形式，将地址栏中的比如`?`、`=`等乱七八糟的符号删去，全部变成`/`分隔，现在几乎所有的网站上都在使用

![image-20210929185910968](https://s2.loli.net/2021/12/06/x43d2Bo9vPybWSg.png)

传统的方式操作资源只能通过`GET`或`POST`方式通过请求不同的资源来获得不同的内容

而RestFul风格的重心是以对统一资源不同的请求方式来获得不同的内容效果

想使用RestFul风格，就只需要在上面的基础上修改`RestMapping`并增添`@PathVariable`注解即可

```java
@RequestMapping(value = "/add/{a}/{b}",method = RequestMethod.DELETE)
public String test1(@PathVariable int a,@PathVariable int b, Model model){}
```

> ```java
> @RequestMapping("/add/${a}/${b}")
> ```
>
> 直接这样修改RestMapping好像也可以，不知道是不是IDEA优化了还是这就是jQuery的某一种方式

之后就可以直接在地址栏输入`/add/1/2`即可对a，b参数赋值

这只是最基础的内容，要实现不同方式请求获得不同内容，就需要给ResultMapping加上请求类型

```java
@RequestMapping(value = "/add/${a}/${b}",method = RequestMethod.DELETE)
```

这样之后我们如果还跟之前一样输入地址，就会报405错误，因为默认的请求方法是GET，而本程序不支持

```java
@DeleteMapping("/add/{a}/{b}")
```

当然这样也可以，算是另一种方式

RestFul风格可以让URL变得更加简洁、高效和安全，别人不再知道传入的参数在服务器里到底是什么东西

#### 结果跳转方式

正常的Servlet转发和重定向必须得通过req和resp的方法实现，在Spring中可以被简化，在return中可以通过前缀实现转发和重定向

其中在拥有视图解析器的情况下，转发并不需要加前缀，而如果想要重定向就在前面加上`redirect:`即可

```java
@Controller
public class Demo3 {
    @RequestMapping("/t3")
    public String test(){
        return "redirect:/index.jsp";
    }
}
```

> 事实上如果我们把Spring配置文件中的所有东西都删掉，只留一个扫包标签，即没有视图解析器和HandlerMapping等等，这时候我们依然可以在控制类中通过前缀+全路径`return "forward:/WEB-INF/jsp/test.jsp";`的返回值实现转发

==注意重定向不能重定向到WEB-INF目录，因为他是隐藏的==

#### 乱码问题

当我们在前端提交一个中文参数的请求时，在转发的时候在Java层面上就会出现乱码，也就是根本无法把中文参数传到后端

![image-20211003163821782](https://s2.loli.net/2021/12/06/pJi9ErgqQeNB1Hk.png)

![image-20211003163840065](https://s2.loli.net/2021/12/06/PU8xOCtMRy4fsI2.png)

这时候就需要通过过滤器劫持前端发到后端的请求，进行utf-8编码后再传到后端

```java
public class EncodingF implements Filter {

    @Override
    public void init(FilterConfig filterConfig) throws ServletException {
        Filter.super.init(filterConfig);
    }

    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
        servletRequest.setCharacterEncoding("utf-8");
        servletResponse.setCharacterEncoding("utf-8");
        filterChain.doFilter(servletRequest,servletResponse);
    }

    @Override
    public void destroy() {
        Filter.super.destroy();
    }
}
```

做完之后记得在`web.xml`中添加过滤器依赖

```xml
<filter-mapping>
    <filter-name>encoding</filter-name>
    <url-pattern>/t5</url-pattern>
</filter-mapping>
<filter>
    <filter-name>encoding</filter-name>
    <filter-class>com.test.filter.EncodingF</filter-class>
</filter>
```

同时注意到get方法在Tomcat中会自动解决乱码，所以此处模拟时的post提交非常重要，这样才能看出是否解决乱码问题

当然这是我们自己写的乱码，事实上SpringMVC也给我们提供了一个写好了的乱码过滤器，此时我们只需要在`web.xml`中，直接配置即可

> 同时还需要注意一下，乱码过滤器在`web.xml`中作用域如果要是所有网页就应该写`/*`而不是`/`，因为`/`不过滤`.jsp`一类的文件请求，当展示页面的时候过滤器不生效（详见[过滤器](#Filter)）

#### 后端解析JSON

在讲JavaScript的时候我们[提到了](#JSON对象)JSON是一个什么东西，我们学习了怎么在前端把数据存储为JSON格式，现在我们则需要学习怎么在后端解析前端发来的JSON内容

当然因为JSON只是一个字符串，常理来说我们也可自己写一个对象转换JSON的方法，但是没必要，很多人已经帮我们写好了，常见的有 Jackson，Fastjson，gson等等

这里使用gson演示，这些工具实际上都大同小异

首先导入Gson依赖

```xml
<dependency>
    <groupId>com.google.code.gson</groupId>
    <artifactId>gson</artifactId>
    <version>2.8.8</version>
</dependency>
```

> 注意之后加载项目之前务必要在项目结构中那个将gson的包丢进去，不然会报`NoClassDefFoundError`的错

之后编写控制类，并创建Gson对象调用方法即可

```java
@Controller  // 这里改成RestController也可以实现下面ResponseBody一样的效果，只是作用域是一个类
public class Demo6 {
    @GetMapping(value = "/t6",produces = "text/html;charset=utf-8") // 设置传输给生成的文件的编码格式
    @ResponseBody  // 加上这个注解下面的方法就不会走视图解析器，也就不会请求转发给test.jsp
    // 而是会直接返回一个字符串到网页上（生成一个html文件然后在body里面直接插入返回内容，就是这么暴力）
    public String json(){
        User user = new User(1, "测试");
        Gson gson = new Gson();
        return gson.toJson(user);
    }
}
```

Gson相关方法还有比如说将JSON转换为对象等等， 功能还是挺强大的

#### Ajax

*AJAX = Asynchronous JavaScript and XML（异步的 JavaScript 和 XML）。*

*AJAX 不是新的编程语言，而是一种使用现有标准的新方法。*

*AJAX 最大的优点是在不重新加载整个页面的情况下，可以与服务器交换数据并更新部分网页内容。*

*AJAX 不需要任何浏览器插件，但需要用户允许JavaScript在浏览器上执行。*

Ajax实际上就是一个弹窗，不熟悉的话我们的HTML也有一个iframe标签，利用它可以简单的了解弹窗效果

下面是用纯HTML做的页内弹窗，实现弹窗内显示我们需要访问的网站

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
    <script>
        function g(){
            let value = document.getElementById("url").value;
            document.getElementById("iframe1").src=value;
        }
    </script>
</head>
<body>
<div>
    <p>请输入地址：</p>
    <p>
        <input type="text" id="url">
        <input type="button" value="提交" onclick="g()">
    </p>
</div>

<div>
    <iframe id="iframe1" style="width: 50%;height: auto"></iframe>
</div>
</body>
</html>
```

当然这并不是真正的Ajax，Ajax的核心是XHR（XMLHttpRequest），在原生Javascript中，我们要通过创建一个XHR对象来实现Ajax，然而现在有很多种简便的方法，其中jQuery提供了多个与Ajax有关的方法

下面是前端利用了jQuery的post方法（内含一个Ajax请求）来实现请求后台数据并展示

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
    <script
            src="https://code.jquery.com/jquery-3.6.0.js"
            integrity="sha256-H+K7U5CnXl1h5ywQfKtSj8PCmoN9aaq30gDh27Xc0jk="
            crossorigin="anonymous"></script>
    <script>
        function a(){
            $.post("${pageContext.request.contextPath}/ajax",function (data){
                let html="";
                for (let i = 0; i < data.length; i++) {
                    html += "<tr>"
                        +"<td>"+data[i].id+ "</td>"
                        +"<td>"+data[i].name+ "</td>"
                        +"<td>"+data[i].age+ "</td>"
                        +"</tr>"
                }  // 这里使用了非常复杂的字符串拼接操作，等到学到vue了以后就会被简化
                $("#context").html(html);
            })
        }
    </script>
</head>
<body>
    <label>
        <input type="button" id="btn" onclick="a()" value="显示内容">
    </label>
<table>
    <tr>
        <td>id</td>
        <td>name</td>
        <td>age</td>
    </tr>
    <tbody id="context">
    </tbody>
</table>
</body>
</html>
```

前端的繁琐使得我们后端变得十分简便，只需要无脑给前端传参数即可

```java
@RequestMapping("/ajax")
@ResponseBody  // 注意不要不小心带视图解析器了，只是单纯的返回数据即可
public List<User> test1(){
    User test1 = new User(1, "test1", 1);
    User test2 = new User(2, "test2", 2);
    User test3 = new User(3, "test3", 3);
    List<User> users = new ArrayList<>();
    users.add(test1);
    users.add(test2);
    users.add(test3);
    return users;
}
```

其中User类也十分简单

```java
@Data
@AllArgsConstructor
public class User {
    private int id;
    private String name;
    private int age;
}
```

如此就可以不刷新页面实现展示不同内容的功能

可以看出，Ajax把大部分内容都交给了前端，前后端仅通过XHR沟通，同时也避免了频繁刷新页面和设计过多不同页面的困扰

#### 拦截器

拦截器是AOP思想的具体应用，横切进某个具体方法中进行拦截，同时它只会拦街访问的控制器方法，如果访问的是jsp/html/css/image/js等静态资源则不会进行拦截（就算你在配置文件中写`/**`，这也体现了它运行在SpringMVC层上的特点）

SpringMVC提供了独有拦截器的功能，想要实现拦截器，只需要实现其中的`HandlerInterceptor`接口即可

> 在前面学习过滤器的时候我们使用过滤器实现了[拦截功能](#拦截请求)，虽然这个拦截器不是由web端执行，但是思路上面都是大差不差

该接口有三个需要实现方法（当然也可以不实现），分别对应着在方法前拦截，方法后拦截及清理的功能

```java
public class MInterceptor implements HandlerInterceptor {
    @Override
    // 这里return true就代表放行，执行下一个拦截器，相当于过滤器中clain.forward();
    // 请求前拦截
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        System.out.println("MInterceptor.preHandle");
        return true;
    }

    // 请求后拦截
    @Override
    public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {
        System.out.println("MInterceptor.postHandle");
    }

    // 清理内容
    @Override
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {
        System.out.println("MInterceptor.afterCompletion");
    }
}
```

由于拦截器是SpringMVC提供的，所以接下来要在`ApplicationContext.xml`而不是`web.xml`里面配置，意味着不是让Tomcat拦截而是SpringMVC，这也正体现了Spring独有的AOP思想

```xml
<mvc:interceptors>
    <mvc:interceptor>
        <mvc:mapping path="/**"/> <!--**代表这个请求下面的所有请求，*只代表当前文件夹下的某个请求-->
        <bean class="com.test.config.MInterceptor"/>
    </mvc:interceptor>
</mvc:interceptors>
```

一般来说，最重要的是第一个请求前拦截（毕竟你方法都执行完了也没必要拦截了），在方法执行之前判断是否能让这个方法执行（返回值），后两个一半是作为日志或者其他无关紧要的内容

同时接口内还有req和resp参数，可以在拦截之后让用户跳转到其他页面（登陆页面等）

由于之前写过，此处就不再赘述了，详细可以看前面的[Filter](#Filter)内容

#### 文件传输

需要进行文件传输，首先要导入文件上传和下载的包

```xml
<dependency>
    <groupId>commons-fileupload</groupId>
    <artifactId>commons-fileupload</artifactId>
    <version>1.3.2</version>
</dependency>
```

> 我们使用的文件上传的手段是通过Apache的一个文件上传组件来实现，上面的导入包及下面的前端表单配置内容都是这个文件上传包的要求所致

需要在前端传输文件，需要在表单中的`enctype`属性指定为`multipart/form-data`属性

```xml
<form action="${pageContext.request.contextPath}/file" enctype="multipart/form-data" method="post">
  <input type="file" name="file">
  <input type="submit" value="submit">
</form>
```

接下来我们要利用SpringMVC给我们的文件上传的支持，因此需要在配置文件中创建bean

```xml
<bean class="org.springframework.web.multipart.commons.CommonsMultipartResolver" id="multipartResolver">
    <property name="defaultEncoding" value="utf-8"/>
    <property name="maxUploadSize" value="10485760"/>
    <property name="maxInMemorySize" value="40960"/>
</bean>
```

下一步就是编写Controller内容

```java
@PostMapping("/file")
@ResponseBody
public String upload(@RequestParam("file") CommonsMultipartFile file, HttpServletRequest req)
        throws IllegalStateException, IOException {
    String path=req.getServletContext().getRealPath("/upload");  // 创建文件放置目录
    File realPath = new File(path);  // 将字符串存储为一种地址格式
    if (!realPath.exists()){  // 判断目录是否存在，不存在就创建一个
        realPath.mkdir();
    }
    file.transferTo(new File(realPath+"/"+file.getOriginalFilename()));
    // 调用Spring提供的文件类方法，快速将目标文件存储于指定目录
    return "success";
}
```

同时这些文件上传的操作只需要理解但不需要记忆，哪天需要用到了直接上网搜索复制即可

相比较与上传文件的繁琐，下载文件只需要在a标签中添加文件的所在位置即可，浏览器会自动下载内容

### SSM整合

三个模块基本都讲解完毕，接下来就可以运用SSM框架开发了

#### 准备工作

网站实际上就是一系列围绕数据库做的工作，所以一切要从创建数据库开始

```sql
CREATE DATABASE `ssmbuild`;
USE `ssmbuild`;
CREATE TABLE `books`(
                        `bookID` INT NOT NULL AUTO_INCREMENT COMMENT '书id',
                        `bookName` VARCHAR(100) NOT NULL COMMENT '书名',
                        `bookCounts` INT NOT NULL COMMENT '数量',
                        `detail` VARCHAR(200) NOT NULL COMMENT '描述',
                        KEY `bookID`(`bookID`)
)ENGINE=INNODB DEFAULT CHARSET=utf8;

INSERT INTO `books`(`bookID`,`bookName`,`bookCounts`,`detail`)VALUES
                                                                  (1,'Java',1,'从入门到放弃'),
                                                                  (2,'MySQL',10,'从删库到跑路'),
                                                                  (3,'Linux',5,'从进门到进牢');
```

下一步当然是导入依赖

```xml
<dependencies>
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.13.2</version>
        <scope>test</scope>
    </dependency>
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>8.0.26</version>
    </dependency>
    <dependency>
        <groupId>com.zaxxer</groupId>
        <artifactId>HikariCP</artifactId>
        <version>5.0.0</version>
    </dependency>
    <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>servlet-api</artifactId>
        <version>2.5</version>
    </dependency>
    <dependency>
        <groupId>javax.servlet.jsp</groupId>
        <artifactId>javax.servlet.jsp-api</artifactId>
        <version>2.3.3</version>
    </dependency>
    <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>jstl</artifactId>
        <version>1.2</version>
    </dependency>
    <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis</artifactId>
        <version>3.5.7</version>
    </dependency>
    <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis-spring</artifactId>
        <version>2.0.6</version>
    </dependency>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-webmvc</artifactId>
        <version>5.3.10</version>
    </dependency>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-jdbc</artifactId>
        <version>5.3.10</version>
    </dependency>

</dependencies>
```

然后连接数据库，建立层级包，创建配置文件，最终效果如图

![image-20211003203335687](https://s2.loli.net/2021/12/06/My5VxO4ziwBhAtg.png)

#### Mybatis层

Mybatis要做的内容是十分简单，即创建实体类，mapper内容，mybatis配置文件及业务层调用

- 实体类

  ```java
  @Data
  @AllArgsConstructor
  @NoArgsConstructor
  public class Books {
      private int bookID;
      private String bookName;
      private int bookCounts;
      private String detail;
  }
  ```

- Mapper接口及sql实现

  ```java
  public interface BookMapper {
      int addBook(Books books);
      int delBookByID(int id);
      int updBook(Books books);
      Books queBookByID(int id);
      List<Books> queBooks();
  }
  
  ```
  
  ```xml
  <?xml version="1.0" encoding="GBK" ?>
  <!DOCTYPE mapper
          PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
          "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
  <mapper namespace="com.test.mapper.BookMapper">
      <insert id="addBook" parameterType="books">
          insert into ssmbuild.books (bookID, bookName, bookCounts, detail)
          values (#{bookID},#{bookName},#{bookCounts},#{detail});
      </insert>
      <delete id="delBookByID" parameterType="_int">
          delete
          from ssmbuild.books
          where bookID = #{id};
      </delete>
      <update id="updBook" parameterType="books">
          update ssmbuild.books
          set bookName = #{bookName},bookCounts=#{bookCounts},detail=#{detail}
          where bookID=#{b};
      </update>
      <select id="queBookByID" resultType="books">
          select *
          from ssmbuild.books where bookID=#{id};
      </select>
      <select id="queBooks" resultType="books">
          select *
          from ssmbuild.books;
      </select>
  </mapper>
  ```
  
- 业务层接口及实现

  ```java
  public interface BookService {
      int addBook(Books books);
      int delBookByID(int id);
      int updBook(Books books);
      Books queBookByID(int id);
      List<Books> queBooks();
  }
  ```

  ```java
  @Data
  public class BookServiceImpl implements BookService{
  
      // 业务层就需要调用dao层，目的就是组合dao
      private BookMapper bookMapper;
  
      @Override
      public int addBook(Books books) {
          return bookMapper.addBook(books);
      }
  
      @Override
      public int delBookByID(int id) {
          return bookMapper.delBookByID(id);
      }
  
      @Override
      public int updBook(Books books) {
          return bookMapper.updBook(books);
      }
  
      @Override
      public Books queBookByID(int id) {
          return bookMapper.queBookByID(id);
      }
  
      @Override
      public List<Books> queBooks() {
          return bookMapper.queBooks();
      }
  }
  ```

  看似似乎业务层和dao层没有什么区别，实际上业务层将会连接Spring并通过Spring注入来传参，而dao层只由业务层调用并传参，既保证安全，有避免耦合

- 配置文件

  ```xml
  <?xml version="1.0" encoding="GBK" ?>
  <!DOCTYPE configuration
          PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
          "http://mybatis.org/dtd/mybatis-3-config.dtd">
          
  <configuration>
  
      <properties resource="db.properties"/>
  
      <settings>
          <setting name="logImpl" value="STDOUT_LOGGING"/>
          <setting name="mapUnderscoreToCamelCase" value="true"/>
      </settings>
      
      <typeAliases>
          <package name="com.test.pojo"/>
      </typeAliases>
      
      <mappers>
          <package name="com.test.mapper"/>
      </mappers>
  </configuration>
  ```
  
  当然还有资源类，此处省略

#### Spring层

Spring层的重点就是整合项目中的各层内容，即对各种内容编写配置文件，在我们的项目中即配置Dao层（连接数据库）和Service层（被web项目调用）

由于我们要对不同的层配置不同的文件，因此为了分工明确且解耦，我们需要创建多个Spring配置文件，并且将它们添加到同一个上下文当中，保证各个配置文件能够相互引用beanid，如图所示，一般来说创建Spring配置文件之后会自动提示配置上下文

![image-20211004154102035](https://s2.loli.net/2021/12/06/M4DcI98gzplaACW.png)

当然也可以通过`import`标签在一个配置文件中引入另一个，但是配置在同一个上下文既安全又高效

- Dao层配置文件（`spring-dao.xml`）

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xmlns:context="http://www.springframework.org/schema/context"
         xmlns:aop="http://www.springframework.org/schema/aop"
         xsi:schemaLocation="http://www.springframework.org/schema/beans
          https://www.springframework.org/schema/beans/spring-beans.xsd
          http://www.springframework.org/schema/context
          https://www.springframework.org/schema/context/spring-context.xsd
          http://www.springframework.org/schema/aop 
          https://www.springframework.org/schema/aop/spring-aop.xsd">
  
      <!--关联数据库配置文件-->
      <context:property-placeholder location="classpath:db.properties"/>
      <!--连接池-->
      <bean id="dataSource" class="com.zaxxer.hikari.HikariDataSource">
          <property name="driverClassName" value="${jdbc.driver}"/>
          <property name="jdbcUrl" value="${jdbc.url}"/>
          <property name="username" value="${jdbc.username}"/>
          <property name="password" value="${jdbc.password}"/>
      </bean>
      <!--SqlSessionFactory-->
      <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
          <property name="dataSource" ref="dataSource"/>
          <!--绑定Mybatis配置文件-->
          <property name="configLocation" value="classpath:mybatis-config.xml"/>
      </bean>
      <!--配置dao接口扫描包，动态实现Dao接口可以注入到Spring容器中-->
      <!--通俗来讲就是省去了原先的创建SqlSession类的过程
          现在由Spring自动根据Mapper生成SqlSession，变得更加简单！-->
      <bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">
          <property name="sqlSessionFactoryBeanName" value="sqlSessionFactory"/>
          <property name="basePackage" value="com.test.mapper"/>
      </bean>
  
  </beans>
  ```

  注意到在获取SqlSession方面采用了更加简便的自动生成的方法，避免了创建多个实现类的繁琐

- Service层（`spring-service.xml`）

  ```xml
  <!--Service层内容，头部内容省去-->
  <!--扫包-->
  <context:component-scan base-package="com.test.service"/>
  <!--将所有业务类注入到Spring，此处使用注解形式-->
  <!--声明式事务配置-->
  <bean class="org.springframework.jdbc.datasource.DataSourceTransactionManager" id="transactionManager">
      <property name="dataSource" ref="dataSource"/>
  </bean>
  
  <!--AOP事务支持，这个项目中用不到-->
  ```

#### SpringMVC层

SpringMVC的功能就是操作web项目，在前面搞了那么多配置文件之后，我们发现实际上我们的项目还不是一个web项目，所以第一步我们就要添加web框架支持（右击项目->添加框架支持->web应用程序）

- 首先要先配置`web.xml`

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <web-app xmlns="https://jakarta.ee/xml/ns/jakartaee"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="https://jakarta.ee/xml/ns/jakartaee https://jakarta.ee/xml/ns/jakartaee/web-app_5_0.xsd"
           version="5.0">
  
      <!--DispatchServlet-->
      <servlet>
          <servlet-name>springmvc</servlet-name>
          <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
          <init-param>
              <param-name>contextConfigLocation</param-name>
              <!--注意注意，此处引用的是总的配置文件而并不是spring-mvc.xml，因为我们是在Service层配置文件中注册的bean，到时候Controller调用的是Service层的bean-->
              <param-value>classpath:ApplicationContext.xml</param-value>
          </init-param>
          <load-on-startup>1</load-on-startup>
      </servlet>
      <servlet-mapping>
          <servlet-name>springmvc</servlet-name>
          <url-pattern>/</url-pattern>
      </servlet-mapping>
  
      <filter-mapping>
          <filter-name>encoding</filter-name>
          <url-pattern>/*</url-pattern>
      </filter-mapping>
      <filter>
          <filter-name>encoding</filter-name>
          <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
          <init-param>
              <param-name>encoding</param-name>
              <param-value>utf-8</param-value>
          </init-param>
      </filter>
  
      <session-config>
          <session-timeout>15</session-timeout>
      </session-config>
  
  </web-app>
  ```

- 下一步是配置创建并配置`spring-mvc.xml`，同样要记得把它添加到上下文

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xmlns:context="http://www.springframework.org/schema/context"
         xmlns:aop="http://www.springframework.org/schema/aop" xmlns:mvc="http://www.springframework.org/schema/mvc"
         xsi:schemaLocation="http://www.springframework.org/schema/beans
          https://www.springframework.org/schema/beans/spring-beans.xsd
          http://www.springframework.org/schema/context
          https://www.springframework.org/schema/context/spring-context.xsd
          http://www.springframework.org/schema/aop 
          https://www.springframework.org/schema/aop/spring-aop.xsd http://www.springframework.org/schema/cache http://www.springframework.org/schema/cache/spring-cache.xsd">
  
      <!--注解驱动-->
      <mvc:annotation-driven/>
      <!--静态资源过滤-->
      <mvc:default-servlet-handler/>
      <!--扫描包-->
      <context:component-scan base-package="com.test.controller"/>
      <!--视图解析器-->
      <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
          <property name="prefix" value="/WEB-INF/jsp/"/>
          <property name="suffix" value=".jsp"/>
      </bean>
  
  </beans>
  ```

最后，为了稳妥起见，在总的`ApplicationContext.xml`中导入需要使用所有的xml文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd
        http://www.springframework.org/schema/aop 
        https://www.springframework.org/schema/aop/spring-aop.xsd">

    <import resource="spring-dao.xml"/>
    <import resource="spring-service.xml"/>
    <import resource="spring-mvc.xml"/>
    
</beans>
```

至此，所有的配置工作就完成啦！可以看出来总的来说还是比较繁琐的。。。

下面是项目完成以后的总项目结构图

![image-20211004162620447](https://s2.loli.net/2021/12/06/sSeTEtUcWu52i1F.png)

如果感觉摸不着头脑，不如看看下面这个图，详细说明了各个配置文件及功能体系连接

![查看源图像](https://pic4.zhimg.com/v2-55b2dac916e70e9bb9a4452868220983_r.jpg)

#### 测试方法

接下来我们要做的就是连接Controller层和jsp目录，同时通过Controller层调用Service层实现内容跳转展示

在这之前不如让我们先写一个最简单的小程序来测试一下我们上面的一大堆配置到底有没有问题

```java
@Controller
@RequestMapping("/book")
public class BookController {
    // Controller层调用Service层
    @Autowired
    private BookService bookService;

    // 查询全部数据并返回到页面
    @GetMapping("/all")
    public String list(Model model){
        List<Books> books = bookService.queBooks();
        model.addAttribute("list",books);
        return "all";
    }
}
```

相对应我们要建立一个jsp文件，并且在`index.jsp`中实现跳转

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
  <head>
    <title>$Title$</title>
  </head>
  <body>
    <h3>
      <a href="${pageContext.request.contextPath}/book/all">所有书籍</a>
    </h3>
  </body>
</html>
```

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>所有书</title>
</head>
<body>
    进入成功
</body>
</html>
```

如果出现问题，我们可以进行Junit单元测试，例如

```java
public class TestM {
    @Test
    public void test(){
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("ApplicationContext.xml");
        BookService bookServiceImpl = context.getBean("BookServiceImpl", BookService.class);
        for (Books queBook : bookServiceImpl.queBooks()) {
            System.out.println(queBook);
        }

    }
}
```

以此来检查dao层及service层有没有问题

最终成功结果如下，点击所有书籍之后跳转成功

![image-20211004172010887](https://s2.loli.net/2021/12/06/dLPO8Qarvuym4EA.png)

#### CRUD操作

前面我们已经测试到让查询页面跳转成功，我们现在来完善它

我们已经将书籍列表传给了这个页面，如今我们只需要将其取出并展示即可

此处我们使用BootStrap样式来展示页面，可以百度一个cdn导入

```jsp
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>所有书</title>
    <link href="https://cdn.staticfile.org/twitter-bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet">
</head>
<body>
    <%--BootStrap栅格系统--%>
    <div class="container">
        <div class="row clearfix">
            <div class="col-md-12 column">
                <div class="page-header">
                    <h1>
                        <small>书籍列表--显示书籍</small>
                    </h1>
                </div>
            </div>
        </div>
        <div class="row clearfix">
            <div class="col-md-12 column">
                <table class="table table-hover table-striped">
                    <thead>
                    <tr>
                        <th>书籍编号</th>
                        <th>书籍名称</th>
                        <th>书籍数量</th>
                        <th>书记详情</th>
                    </tr>
                    </thead>
                    <tbody>
                    <c:forEach var="book" items="${list}">
                        <tr>
                            <td>${book.bookID}</td>
                            <td>${book.bookName}</td>
                            <td>${book.bookCounts}</td>
                            <td>${book.detail}</td>
                        </tr>
                    </c:forEach>
                    </tbody>
                </table>
            </div>
        </div>
    </div>

</body>
</html>
```

查询效果，确实好看不少了

![image-20211004174455640](https://s2.loli.net/2021/12/06/AcurFRCE1nhtL8I.png)

接下来的操作即都是照猫画虎，十分简单，我们简单的贴上源码

- Controller层，为所有资源统一定向和提供Servlet

  ```java
  @Controller
  @RequestMapping("/book")
  public class BookController {
      // Controller层调用Service层
      @Autowired
      private BookService bookService;
  
      // 查询全部数据并返回到页面
      @GetMapping("/all")
      public String list(Model model){
          List<Books> books = bookService.queBooks();
          model.addAttribute("list",books);
          return "all";
      }
  
      @GetMapping("/pageShow/add")
      public String addShow(){
          return "add";
      }
      @GetMapping("/pageShow/update/{id}")
      public String updateShow(@PathVariable int id, Model model){
          Books books = bookService.queBookByID(id);
          model.addAttribute("RBook",books);
          System.out.println(model.getAttribute("RBook"));
          return "update";
      }
  
      @PostMapping("/add")
      public String add(Books books){
          System.out.println("BookController.add");
          bookService.addBook(books);
          return "redirect:/book/all";
      }
      @PostMapping("/update")
      public String update(Books books){
          bookService.updBook(books);
          return "redirect:/book/all";
      }
      @GetMapping("/delete/{id}")
      public String delete(@PathVariable int id){
          bookService.delBookByID(id);
          return "redirect:/book/all";
      }
  }
  ```

- View层接收Servlet传输数据内容并展示

  - `all.jsp`

    ```jsp
    <%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
    <%@ page contentType="text/html;charset=UTF-8" language="java" %>
    <html>
    <head>
        <title>所有书</title>
        <link href="https://cdn.staticfile.org/twitter-bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet">
    </head>
    <body>
        <%--BootStrap栅格系统--%>
        <div class="container">
            <div class="row clearfix">
                <div class="col-md-12 column">
                    <div class="page-header">
                        <h1>
                            <small>书籍列表--显示书籍</small>
                        </h1>
                    </div>
                </div>
    
                <div class="row">
                    <div class="col-md-4 column">
                        <a type="button" class="btn btn-default" href="${pageContext.request.contextPath}/book/pageShow/add">新增书籍</a>
                    </div>
                </div>
    
            </div>
            <div class="row clearfix">
                <div class="col-md-12 column">
                    <table class="table table-hover table-striped">
                        <thead>
                        <tr>
                            <th>书籍编号</th>
                            <th>书籍名称</th>
                            <th>书籍数量</th>
                            <th>书籍详情</th>
                        </tr>
                        </thead>
                        <tbody>
                        <c:forEach var="book" items="${list}">
                            <tr>
                                <td>${book.bookID}</td>
                                <td>${book.bookName}</td>
                                <td>${book.bookCounts}</td>
                                <td>${book.detail}</td>
                                <th>
                                    <a href="${pageContext.request.contextPath}/book/pageShow/update/${book.bookID}">修改</a>
                                    &nbsp; | &nbsp;
                                    <a href="${pageContext.request.contextPath}/book/delete/${book.bookID}">删除</a>
                                </th>
                            </tr>
                        </c:forEach>
                        </tbody>
                    </table>
                </div>
            </div>
        </div>
    
    </body>
    </html>
    ```

  - `add.jsp`

    ```jsp
    <%@ page contentType="text/html;charset=UTF-8" language="java" %>
    <html>
    <head>
        <title>Title</title>
        <link href="https://cdn.staticfile.org/twitter-bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet">
    </head>
    <body>
    <div class="container">
        <div class="row clearfix">
            <div class="col-md-12 column">
                <div class="page-header">
                    <h1>
                        <small>书籍列表--新增书籍</small>
                    </h1>
                </div>
            </div>
        </div>
    
        <form action="${pageContext.request.contextPath}/book/add" method="post">
            <div class="form-group">
                <label>
                    <p>书名</p>
                    <input type="text" class="form-control" name="bookName" required>
                </label>
                <label>
                    <p>数量</p>
                    <input type="text" class="form-control" name="bookCounts" required>
                </label>
                <label>
                    <p>备注</p>
                    <input type="text" class="form-control" name="detail" required>
                </label>
            </div>
            <button type="submit" class="btn btn-default">Submit</button>
        </form>
    </div>
    
    </body>
    </html>
    ```

  - `update.jsp`

    ```jsp
    <%@ page contentType="text/html;charset=UTF-8" language="java" %>
    <html>
    <head>
        <title>Title</title>
        <link href="https://cdn.staticfile.org/twitter-bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet">
    </head>
    <body>
    <div class="container">
        <div class="row clearfix">
            <div class="col-md-12 column">
                <div class="page-header">
                    <h1>
                        <small>书籍列表--修改书籍</small>
                    </h1>
                </div>
            </div>
        </div>
    
        <form action="${pageContext.request.contextPath}/book/update" method="post">
            <div class="form-group">
                <input type="hidden" name="bookID" value="${RBook.bookID}">
                <label>
                    <p>书名</p>
                    <input type="text" class="form-control" name="bookName" value="${RBook.bookName}" required>
                </label>
                <label>
                    <p>数量</p>
                    <input type="text" class="form-control" name="bookCounts" value="${RBook.bookCounts}" required>
                </label>
                <label>
                    <p>备注</p>
                    <input type="text" class="form-control" name="detail" value="${RBook.detail}" required>
                </label>
            </div>
            <button type="submit" class="btn btn-default">Submit</button>
        </form>
    </div>
    
    </body>
    </html>
    ```

会发现比起配置，内容的实现要简单的多，在拥有了框架搭建后的基础上，功能的实现显得是那么简单

接下来贴上耗费了我一个下午时间总结的这个项目中整个SSM框架的[运行流程图](http://assets.processon.com/chart_image/614c05b7f346fb69b168b1ca.png)（看不清就点这个链接）

<img src="https://s2.loli.net/2021/12/06/rJfAEv2wsIzhmeR.png" alt="未命名文件 (1)"  />

## SpringBoot

SpringBoot框架的目的就是简化Spring的开发，是一个Spring的顶级项目，在目前以微服务为潮流的当下，SpringBoot能够大大降低开发成本，增加开发速度，成为了大多数人的首选

> 其中**微服务**就是将一个系统按业务划分成多个子系统，每个子系统都是完整的，可独立运行的，子系统间的交互可通过HTTP协议进行通信（也可以采用消息队列来通信，如RoocketMQ，Kafaka等）。

Spring最大的缺点就是配置繁琐，包括了Spring里的xml里面的配置和Maven项目中的pom文件配置，既要保证导入依赖的版本相同，又要保证创建的bean的正确性，一来二去，形成了代码轻量但配置重量的一种头重脚轻的感觉

SpringBoot解决了Spring的缺点，它在运行时**自动配置**了各种原本需要一个个在`ApplicationContext.xml`中所需要需要配置的内容，同时采用了**起步依赖**的思想，它打包了更多的具有相同功能的不同包，使得我们不需要再依靠Maven来管理我们的jar包，更进一步的是，SpringBoot还提供了许多**辅助功能**，如嵌入式服务器，安全配置等，我们再也不用再配置Tomcat环境了

因此SpringBoot提供了一种快速开发Spring项目的方式，而不是对Spring功能上的增强

### 简单的项目

1. 首先我们还是要先创建一个Maven项目，并在pom.xml中导入依赖

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
       <modelVersion>4.0.0</modelVersion>
   
       <groupId>com.example</groupId>
       <artifactId>myproject</artifactId>
       <version>0.0.1-SNAPSHOT</version>
   
       <!--springboot工程需要继承的父工程-->
       <parent>
           <groupId>org.springframework.boot</groupId>
           <artifactId>spring-boot-starter-parent</artifactId>
           <version>2.5.5</version>
       </parent>
   
       <dependencies>
           <!--web开发的起步依赖-->
           <dependency>
               <groupId>org.springframework.boot</groupId>
               <artifactId>spring-boot-starter-web</artifactId>
           </dependency>
       </dependencies>
   
       <build>
           <plugins>
               <plugin>
                   <groupId>org.springframework.boot</groupId>
                   <artifactId>spring-boot-maven-plugin</artifactId>
               </plugin>
           </plugins>
       </build>
   
   </project>
   ```

   注意到导入的方式与之前有所不同，继承了SpringBoot的父工程之后，我们仅仅需要导入一个依赖即可

2. 定义Controller类

   ```java
   @RestController
   public class Hello {
       @RequestMapping("/")
       public String hello(){
           return "hello Spring";
       }
   }
   ```

3. 编写引导类（注意在必须在根目录下创建引导类）

   ```java
   @SpringBootApplication
   public class HelloApplication {
       public static void main(String[] args) {
           SpringApplication.run(HelloApplication.class,args);
       }
   }
   ```

4. 启动测试

   直接按下main方法旁边的启动按钮即可直接启动项目，接着控制台会弹出一段启动成功的提示

   ![image-20211010154907059](https://s2.loli.net/2021/12/06/gUiRn9Fsjeqh1ML.png)

   看到这里，我们会发现SpringBoot内置的Tomcat服务器已经启动，当我们打开浏览器访问8080端口时，就可以访问到我们自定义的界面了

   ![image-20211010155115311](https://s2.loli.net/2021/12/06/yk1dRcseIiBFz7X.png)

最终项目结构如下

![image-20211010155154318](https://s2.loli.net/2021/12/06/b67crGFLO1NzKtS.png)

> 注意引导类位置，绝对不能放在任何别的目录下（涉及到Spring扫包机制）

可以说是已经简单到批爆了，而这就是SpringBoot项目的最简化方式！真的爽！

经过代码的编写，现在我们总结一下，可以发现几个特点

1. SpringBoot不再使用以前的war打包方式，由于通过main方法启动项目，因此创建项目时使用jar打包
2. SpringBoot引导类时项目的入口，运行main方法就可以启动项目
3. 使用SpringBoot和Spring构建的项目业务代码编写方式完全一样

这时候就有人要问了，万一还是觉得这种方法麻烦那怎么办呢？事实上，IDEA提供了一整套的SpringBoot项目构建方案，一步到位，谁用谁知道

![image-20211010160103550](https://s2.loli.net/2021/12/06/xNjbCvcgu4iGwnL.png)

接着直接用鼠标点击想要导入的依赖即可，经典的面向鼠标编程！

![image-20211010160525254](https://s2.loli.net/2021/12/06/jJKE2V8XSdNWhDn.png)

再看看生成出来的项目结构，哇塞，该创建的不该创建的都给我们创建出来了，可谓是懒人一步到位

![image-20211010160648854](https://s2.loli.net/2021/12/06/pzLAsdJ5yrRfH7c.png)

请记住这个项目结构，接下来的学习中会不断的用到其中的内容！

### 运行原理

我们肯定会好奇，到底是什么操作可以让我们只需要简单的开始一个main方法就能够执行程序，接下来让我们从依赖和主程序方面来初步认识SpringBoot

#### 起步依赖

起步依赖，即在最简单的pom文件中引入的一个父工程和一个依赖，这些依赖的功能需要我们一个个分析

- `spring-boot-starter-parent`父工程

  我们点进这个父工程，发现它又继承了`spring-boot-dependencies`父工程，我们再往里面点，发现了密密麻麻一大堆的配置信息，通过标签锁定，我们看到了整体上来看分为两大类

  - `<properties>`标签下定义的一大堆版本号
  - `<dependencies>`标签下定义的一大堆依赖位置及引用前文版本号
  - `<dependencyManagement>`通过这个标签锁定所有版本号，使得子项目配置时**不需要再引入版本号**

  ![image-20211010162518589](https://s2.loli.net/2021/12/06/IwB8DkYaECfVspU.png)

  可以看到我们之后引入的依赖也可以在里面找到，但是我们在引入时并没有指定版本信息

  综上我们可以得出结论，`spring-boot-starter-parent`父工程为我们贴心的配置了它认为我们会用到的各种依赖的版本信息，同时这些版本都是经过精挑细选使得任意两两之间都能够完美适配，免去了我们在创建Spring项目时不知道导入什么版本的依赖的问题

- `spring-boot-starter-web`依赖

  点进这个依赖，抛开头部信息不谈，我们看到了许多熟悉的身影

  ```xml
  <dependencies>
    <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter</artifactId>
      <version>2.5.5</version>
      <scope>compile</scope>
    </dependency>
    <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-json</artifactId>
      <version>2.5.5</version>
      <scope>compile</scope>
    </dependency>
    <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-tomcat</artifactId>
      <version>2.5.5</version>
      <scope>compile</scope>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-web</artifactId>
      <version>5.3.10</version>
      <scope>compile</scope>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-webmvc</artifactId>
      <version>5.3.10</version>
      <scope>compile</scope>
    </dependency>
  </dependencies>
  ```

  可以说都是老熟人了，其中就非常简洁的集合了我们web开发需要用到的几个框架，同时注意在SpringBoot中凡是带有`starter`的包都代表着一个开发场景，里面包含了所需启动该功能的所有依赖
  
  现在我们只需要依赖这个包，就可以间接的依赖上其中依赖的所有内容，注意

#### 自动配置

在探究自动配置之前，我们需要了解到其实引导类中`SpringApplication.run`这个方法是会返回当前IoC容器的（就是Spring中学习过的通过配置文件创建出来的[应用程序上下文](#应用程序上下文)），其中包含了当前项目中自动或我们手动注册的所有组件（即bean）

```java
public static void main(String[] args) {
    ConfigurableApplicationContext run = SpringApplication.run(Demo01Application.class, args);
    String[] beanDefinitionNames = run.getBeanDefinitionNames();
    for (String beanDefinitionName : beanDefinitionNames) {
        System.out.println(beanDefinitionName);
    }
}
```

可以在打印出来的组件中搜索定义下来的beanid

![image-20211012150348730](https://s2.loli.net/2021/12/06/jIUE4zZevCOVSFP.png)

如图可以轻松搜索到我们之前尝试运行时注册的bean

> 注意到其中还有很多名称为全类名的bean，这些bean实际上是通过@import注解导入的

通过打印下来这个容器，我们可以在里面找到很多熟悉的面孔，例如`DispatcherServlet`（SpringMVC核心前端控制器）、`CharacterEncodingFilter`（乱码过滤器）等等，正是SprignBoot自动帮助我们配置好了这些web开发的场景，才使得我们能够正常、简便的使用其中的各种功能

包括自动配置中还为我们配置了默认的自动扫描包机制，会自动扫描和引导类同级的所有包内容里面的组件

这些所有的配置功能，都在`spring-boot-autoconfigure`这个依赖中

![image-20211012152710735](https://s2.loli.net/2021/12/06/hG7oO6SFigQ2WXb.png)

其实就是相同名称的这个包

![image-20211012153040715](https://s2.loli.net/2021/12/06/ivat59fp8h7Mnyw.png)

除了web场景，里面配置了所有的SpringBoot支持的场景自动配置信息，只不过我们只导入了web应用场景，别的内容将不会生效（体现了自动配置的按需加载）

#### @SpringBootApplication

只需要为引导类添加上这个标签，即可以通过执行main方法来启动SpringBoot，显而易见，整个SpringBoot最核心的部分就是这个注解了，而理解了这个注解，等于理解了SpringBoot的运行模式

点进去，发现它是一个合成注解，内含了一些我们认识或者不认识的注解

- `@SpringBootConfiguration`即SpringBoot的配置，里面包含了`@Configuration`，表明它修饰的这个引导类从根本来说也是一个Spring组件（Bean）
- `@EnableAutoConfiguration`使该组件能够自动配置，也是其中最重要的一个注解
  
  - 内含了一个`@AutoConfigurationPackage`自动配置包注解，这个注解里面又导入了一个注册选择器（`Registrar.class`），选择器代表一个类，这个类里面有一个核心方法
  
    ```java
    public void registerBeanDefinitions(AnnotationMetadata metadata, BeanDefinitionRegistry registry) {
        AutoConfigurationPackages.register(registry, (String[])(new AutoConfigurationPackages.PackageImports(metadata)).getPackageNames().toArray(new String[0]));
    )
    ```
  
    方法通过传入的`metadata`参数获取到自动配置包注解注解到的类（即我们的引导类）的详细信息，并通过调用`(new AutoConfigurationPackages.PackageImports(metadata)).getPackageNames().toArray(new String[0])`获取到引导类所属包名，并把这个包底下的所有组件注册到容器中来
  
  - 同时也导入了一个配置自动导入选择器（`AutoConfigurationImportSelector.class`）这个类里面也有一个核心方法
  
    ```java
    public String[] selectImports(AnnotationMetadata annotationMetadata) {
        if (!this.isEnabled(annotationMetadata)) {
            return NO_IMPORTS;
        } else {
            AutoConfigurationImportSelector.AutoConfigurationEntry autoConfigurationEntry = this.getAutoConfigurationEntry(annotationMetadata);
            return StringUtils.toStringArray(autoConfigurationEntry.getConfigurations());
        }
    }
    ```
  
    这个方法的返回值同样也就是我们需要导入的包名构成的字符串数组，而这个数组怎么来的，我们就要去看`getAutoConfigurationEntry`这个方法
  
    ```java
    protected AutoConfigurationImportSelector.AutoConfigurationEntry getAutoConfigurationEntry(AnnotationMetadata annotationMetadata) {
        if (!this.isEnabled(annotationMetadata)) {
            return EMPTY_ENTRY;
        } else {
            AnnotationAttributes attributes = this.getAttributes(annotationMetadata);
            List<String> configurations = this.getCandidateConfigurations(annotationMetadata, attributes);
            configurations = this.removeDuplicates(configurations);
            Set<String> exclusions = this.getExclusions(annotationMetadata, attributes);
            this.checkExcludedClasses(configurations, exclusions);
            configurations.removeAll(exclusions);
            configurations = this.getConfigurationClassFilter().filter(configurations);
            this.fireAutoConfigurationImportEvents(configurations, exclusions);
            return new AutoConfigurationImportSelector.AutoConfigurationEntry(configurations, exclusions);
        }
    }
    ```
  
    - 可以看出这个方法通过两个方法获得了`configurations`和`exclusions`两个字符串集合，并对其做了一些元素筛选操作，然后返回，我们想知道这两个集合里面到底有什么，就需要进入这个方法里面看看
    
    ```java
    protected List<String> getCandidateConfigurations(AnnotationMetadata metadata, AnnotationAttributes attributes) {
        List<String> configurations = SpringFactoriesLoader.loadFactoryNames(this.getSpringFactoriesLoaderFactoryClass(), this.getBeanClassLoader());
        Assert.notEmpty(configurations, "No auto configuration classes found in META-INF/spring.factories. If you are using a custom packaging, make sure that file is correct.");
        return configurations;
    }
    ```
    
    - 进到`getCandidateConfigurations`这个方法，发现没什么东西，我们得再进一层
    
    - 这时候已经不在上述对象内了，跳到了`SpringFactoriesLoader`这个对象中
    
      ```java
      public static List<String> loadFactoryNames(Class<?> factoryType, @Nullable ClassLoader classLoader) {
          ClassLoader classLoaderToUse = classLoader;
          if (classLoader == null) {
              classLoaderToUse = SpringFactoriesLoader.class.getClassLoader();
          }
      
          String factoryTypeName = factoryType.getName();
          return (List)loadSpringFactories(classLoaderToUse).getOrDefault(factoryTypeName, Collections.emptyList());
      }
      ```
    
      这个方法也没什么东西，只是给返回的调用的方法准备了所需要的参数
    
      ```java
      private static Map<String, List<String>> loadSpringFactories(ClassLoader classLoader) {
          Map<String, List<String>> result = (Map)cache.get(classLoader);
          if (result != null) {
              return result;
          } else {
              HashMap result = new HashMap();
      
              try {
                  Enumeration urls = classLoader.getResources("META-INF/spring.factories");
      
                  while(urls.hasMoreElements()) {
                      URL url = (URL)urls.nextElement();
                      UrlResource resource = new UrlResource(url);
                      Properties properties = PropertiesLoaderUtils.loadProperties(resource);
                      Iterator var6 = properties.entrySet().iterator();
      
                      while(var6.hasNext()) {
                          Entry<?, ?> entry = (Entry)var6.next();
                          String factoryTypeName = ((String)entry.getKey()).trim();
                          String[] factoryImplementationNames = StringUtils.commaDelimitedListToStringArray((String)entry.getValue());
                          String[] var10 = factoryImplementationNames;
                          int var11 = factoryImplementationNames.length;
      
                          for(int var12 = 0; var12 < var11; ++var12) {
                              String factoryImplementationName = var10[var12];
                              ((List)result.computeIfAbsent(factoryTypeName, (key) -> {
                                  return new ArrayList();
                              })).add(factoryImplementationName.trim());
                          }
                      }
                  }
      
                  result.replaceAll((factoryType, implementations) -> {
                      return (List)implementations.stream().distinct().collect(Collectors.collectingAndThen(Collectors.toList(), Collections::unmodifiableList));
                  });
                  cache.put(classLoader, result);
                  return result;
              } catch (IOException var14) {
                  throw new IllegalArgumentException("Unable to load factories from location [META-INF/spring.factories]", var14);
              }
          }
      }
      ```
    
      进到这个方法，我们总算找到了头，让我们细细品味一下，首先它似乎从`"META-INF/spring.factories"`这个工厂里面拿到了什么东西，这个文件在哪呢？实际上哪里都有，他会自动的扫描当前系统中所有这个位置中的文件，比如核心包`spring-boot-autoconfigure-2.5.5.jar`里面就有
    
      ![image-20211013001125706](https://s2.loli.net/2021/12/06/eGFwOM7ZgtykYsN.png)
    
      这里面稍微瞄一眼，密密麻麻全是包名，代表了SpringBoot全环境需要的所有包内容，而这个工厂也就获得了这个里面所有包的名称然后将其返回（默认全部加载）
    
  - 会发现分析到最后，居然是加载了所有的包，但是真的加载了所有的包吗，回到`getAutoConfigurationEntry`这个方法，我们发现之后对`configurations`这个变量做了过滤操作，即`this.getConfigurationClassFilter().filter(configurations);`而这个过滤操作滤除了大多数用不到的配置包，这也就是SpringBoot最重要的按需加载功能
  
  - 什么是按需加载，SpringBoot怎么识别我们是否需要一个配置包，我们不妨在`spring-boot-autoconfigure`里随便点进一个包里面
  
    ![image-20211013164856537](https://s2.loli.net/2021/12/06/zksFLZrhX23NBwO.png)
  
    会发现几乎每一个包里面的类都会由一个`@Conditionxxxx`注解修饰，而这个注解的含义就是能够判断其括号内的条件是否满足，当不满足条件的时候就不会加载它修饰的类内容，因此我们在pom文件中不导入的配置内容当执行到此的时候也判断不到我们需要这个类，也就不加载了
    
    > 我们可以通过在配置文件中添加`debug: true`来在启动时查看日志信息，里面会有生效类和未生效类的列举

到此为止，我们初步的了解了当我们启动main方法的时候发生的一系列事情，也让我们认识到了SpringBoot最重要的两大特性，即自动按需配置和起步依赖的大致工作原理，为之后的学习提供方便

### 配置

SpringBoot虽然尽可能的少配置，但是并不代表着不配置，接下来就要重点讲解一下其中配置文件配置问题

首先由于SpringBoot约定大于配置的要求，很多配置都有默认值，如果我们想用自己的配置替换默认配置的话，就可以使用核心文件`application.properties`或者`application.yml/yaml`进行配置

> 是不是似曾相识？其实就是在自动生成SpringBoot项目时自动创建的配置文件

而归根结底，配置文件的用处就是将一系列数据和一个个Bean绑定在一起

比如我们想要定义Tomcat的启动端口为8081，那么我们可以采用下面两种方式

- `application.properties`

  ```properties
  server.port=8081
  ```

- `application.yml/yaml`

  ```yaml
  server:
    port: 8081
  ```

> 会发现启动测试的时候会出现Spring的一个图标，事实上我们也可以自定义启动时出现的图像，只需要直接在和配置文件的同级的目录下创建`banner.txt`的文件并写入我们自定义内容即可

同时注意`properties>yml>yaml`，其中`properties`会最后加载，在配置了相同属性时，他的优先级最高

`.properties`资源类我们的都很熟悉，采用键值对的形式来配置内容，所以我们重点介绍`.yaml`配置文件形式

#### YAML

YAML 是 "YAML Ain't a Markup Language"（YAML 不是一种标记语言）的递归缩写（还挺好玩？），准确来说它是一种直观的能够被电脑识别的数据序列化格式，并且容易被人类阅读，容易和脚本语言交互，比xml更简洁

YAML比起一般资源文件多了不同配置之间的层级关系，又比起xml文件更加易于编写，因此受到大众欢迎

注意点

- 大小写敏感
- 数据值前边必须有空格（但不限于一个），作为分隔符
- 使用缩进表示层级关系
- 缩进的每一个空格就代表一个层级，相同层级之间元素左侧对齐即可
- 使用`#`进行注释

基本语法

- 对象（Map）

  ```yaml
  person:
  	name: 1  # 层级写法
  person: {name: 1}  # 行内写法
  ```

- 数组

  ```yaml
  address:
  	- 1
  	- 2  # 层级写法
  address: [1,2]  # 行内写法
  ```

- 纯量（常量）

  ```yaml
  msg1: '1/n2'  # 单引号忽略转义字符
  msg2: "1/n2"  # 双引号识别转义字符
  ```

- 参数引用

  ```yaml
  name: 1
  person:
  	name: ${name}  # 引用上面的name值
  ```

#### 读取配置内容

当我们在`application.yaml`配置文件中配置内容之后，我们可以在控制类中通过三种方式取到配置值

假设有这样一个配置文件

```yaml
name: 123

person:
  name: 123
  age: 123
```

在控制类及实体类中，我们可以这样拿到值

```java
@RestController
public class Demo1 {
    @Value("${name}")  // Field注入，不推荐通过这种方式注入
    private String s;

    private final Environment env;  // 将所有的自定义内容注入到一个对象

    private final Person person;

    // @Autowired 当类中仅有一个构造器方法时（无参构造也不行），可以省略Autowired，因此可以搭配Lombok使用
    // Spring4.x中，推荐使用构造器注入方式
    public Demo1(Environment env, Person person) {
        this.env = env;
        this.person = person;
    }

    @RequestMapping("/")
    public String test(){
        System.out.println(s);
        System.out.println(env.getProperty("name"));
        System.out.println(person);
        return "test";
    }
}
```

其中实体类Person内属性名必须保证与配置文件内一致

```java
@Data
@Component
@ConfigurationProperties(prefix = "person")  // 这里指定在配置文件中类名前缀
public class Person {
    private String name;
    private int age;
}
```

> 注意到在添加`@ConfigurationProperties`注解时，系统会提示我们需要配置一下配置文件进程支持
>
> 此时我们在pom文件中添加依赖
>
> ```xml
> <dependency>
>  <groupId>org.springframework.boot</groupId>
>  <artifactId>spring-boot-configuration-processor</artifactId>
>  <optional>true</optional>
> </dependency>
> ```
>
> 之后重新运行一遍SpringBoot进程，会发现当我们在配置文件中输入时会自动提示前缀名对应的属性
>
> ![image-20211010201049781](https://s2.loli.net/2021/12/06/XNq62oUkRS1Gyne.png)
>
> 不过当然我们不导入这个依赖其实也是可以的，只是不会智能提示罢了

除了正常的玩法，yaml配置文件甚至可以做一些正常配置文件想都不敢想的事情

```yaml
name: 123  # 正常赋值
# test: name
person:
  age: ${random.int(10)} # 获得十以内随机数
  name: ${test:null}  # 获取配置文件中test的值，如果没有test这个值就赋值null
```

可以发现比起`.properties`配置文件，`.yaml`更加灵活和方便

除了在`classpath`下直接建立配置文件之外，SpringBoot还支持在其他位置创建配置文件`application.yml`

![image-20211016154812496](https://s2.loli.net/2021/12/06/wYfercdbDHT7m65.png)

之后SpringBoot会根据优先级顺序读取配置内容，优先级高的文件配置会覆盖优先级低的

#### 多环境配置

在SpringBoot中，我们可以根据不同环境配置不同的配置文件，从而方便的切换各种环境

首先我们先创建多个配置文件，注意一定要以`appliacation`开头，不然不会生效

![image-20211016155750250](https://s2.loli.net/2021/12/06/8mrubWnXgHq1D3I.png)

如图，此时我们只需要在主配置文件中配置如下内容即可

```yaml
spring:
  profiles:
    active: dev  # 这里就填短横杠后面内容
```

这样就可以实现多环境配置，同时注意主配置的内容还是会生效的

但是这样可能还是很麻烦，事实上yaml提供了更加强大的多文档模块内容，我们只需要在模块之间加上`---`即可

```yaml
spring:
  profiles:
    active: dev  # 这里就填短横杠后面内容

---
server:
  port: 8082

spring:
  config:
    activate:
      on-profile: test
---
server:
  port: 8083  # 相当于之前的多文件
  
spring:
  config:
    activate:
      on-profile: dev
```

但是这样耦合性高，在配置多的时候还是建议多文件清晰明了

#### AutoConfiguration和Properties文件

。。。

### 添加静态资源

在之前的学习中，我们好像发现SpringBoot好像没有WEB-INF之类的目录，那我们的web开发应该如何进行呢

在SSM框架中，与静态资源交互的是SpringMVC，顺着这个思路，我们去寻找一下在SpringBoot中集成的SpringMVC内容

![image-20211016193743726](https://s2.loli.net/2021/12/06/edLvunzV6KBQSJM.png)

不出所料，我们找到了自动配置静态资源的类，接着我们慢慢看他的方法，发现了一个`addResourceHandlers`方法

```java
public void addResourceHandlers(ResourceHandlerRegistry registry) {
    if (!this.resourceProperties.isAddMappings()) {
        logger.debug("Default resource handling disabled");
    } else {
        this.addResourceHandler(registry, "/webjars/**", "classpath:/META-INF/resources/webjars/");
        this.addResourceHandler(registry, this.mvcProperties.getStaticPathPattern(), (registration) -> {
            registration.addResourceLocations(this.resourceProperties.getStaticLocations());
            if (this.servletContext != null) {
                ServletContextResource resource = new ServletContextResource(this.servletContext, "/");
                registration.addResourceLocations(new Resource[]{resource});
            }

        });
    }
}
```

可以看到里面有一个if语句，判断我们是否在配置文件中指定了文件位置，如果没有指定，就加载他默认的文件位置里的内容

那么它默认的文件位置在哪里呢，这时候我们看到else语句，里面调用了`addResourceHandler`方法两次，明显是从不同的两个地方去读取一些资源文件，第一个地方很明显是某个叫做`/META-INF/resources/webjars/`的目录，我们先不管他，第二条if语句的第三个参数是一个Lambda表达式，里面有一个`getStaticLocations`方法，同时一看调用方法的类，我们一下子懂了，肯定是某一个默认自动配置好的资源内容

为了证明，我们点进去看看，很明显这是一个Getter方法，获得了资源类私有的`staticLocations`属性，翻翻翻，我们看到了这个Resource类里面的构造方法

```java
public static class Resources {
    private static final String[] CLASSPATH_RESOURCE_LOCATIONS = new String[]{"classpath:/META-INF/resources/", "classpath:/resources/", "classpath:/static/", "classpath:/public/"};
    private String[] staticLocations;
    private boolean addMappings;
    private boolean customized;
    private final WebProperties.Resources.Chain chain;
    private final WebProperties.Resources.Cache cache;

    public Resources() {
        this.staticLocations = CLASSPATH_RESOURCE_LOCATIONS;
        this.addMappings = true;
        this.customized = false;
        this.chain = new WebProperties.Resources.Chain();
        this.cache = new WebProperties.Resources.Cache();
    }
```

这下我们知道了，在自动装配阶段，SpringMVC会自动扫描如此代码中`CLASSPATH_RESOURCE_LOCATIONS`内 的内容，也就是说，今后我们的静态资源只需要放在这四个目录下，都可以在项目启动时被扫描到

![image-20211016200852426](https://s2.loli.net/2021/12/06/wXlpvQVDnjU2Guk.png)

同时我们还可以在里面找到一个`welcomePageHandlerMapping`方法

```java
@Bean
public WelcomePageHandlerMapping welcomePageHandlerMapping(ApplicationContext applicationContext, FormattingConversionService mvcConversionService, ResourceUrlProvider mvcResourceUrlProvider) {
    WelcomePageHandlerMapping welcomePageHandlerMapping = new WelcomePageHandlerMapping(new TemplateAvailabilityProviders(applicationContext), applicationContext, this.getWelcomePage(), this.mvcProperties.getStaticPathPattern());
    welcomePageHandlerMapping.setInterceptors(this.getInterceptors(mvcConversionService, mvcResourceUrlProvider));
    welcomePageHandlerMapping.setCorsConfigurations(this.getCorsConfigurations());
    return welcomePageHandlerMapping;
}
```

看第一个方法调用的参数，调用了一个`getStaticPathPattern`方法，我们点点点，发现其中的`staticPathPattern`属性其实就是代表着`/**`，意味着我们只需要访问`/`程序就会自动把我们跳转到欢迎页面

从哪里调用呢，我们再找找找，发现下面有一个`getIndexHtml`方法

```java
private Resource getIndexHtml(Resource location) {
    try {
        Resource resource = location.createRelative("index.html");
        if (resource.exists() && resource.getURL() != null) {
            return resource;
        }
    } catch (Exception var3) {
    }

    return null;
}
```

`Resource`这个类我们很熟啊，不就是存放静态资源的类吗，因此我们只需要在存放静态资源的地方创建一个`index.html`文件，在应用启动的时候就会自动为我们展示欢迎界面

### thymeleaf模板引擎

模板引擎（这里特指用于Web开发的模板引擎）是为了使用户界面与业务数据（内容）分离而产生的，它可以生成特定格式的文档，用于网站的模板引擎就会生成一个标准的html文档，不懂的可以看下图

![image-20211016210337659](https://s2.loli.net/2021/12/06/oPHYFCdW8xT3Azh.png)

可以发现我们把数据和模板丢进模板引擎，他就能造出我们需要的前端文件用于展示，还是挺方便的

#### 准备工作

使用模板引擎第一步还是要导入依赖，当然我们创建项目的话直接点一下就可以了

![image-20211016210702755](https://s2.loli.net/2021/12/06/i9pXanqvKjEc7Ph.png)

当然由于不需要指定版本号，我们完全可以直接在pom文件中手动加上依赖

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-thymeleaf</artifactId>
</dependency>
```

此时我们再启动SpringBoot会发现报了一个WARN问题

```log
2021-10-16 21:12:14.219  WARN 17100 --- [           main] ion$DefaultTemplateResolverConfiguration : Cannot find template location: classpath:/templates/ (please add some templates or check your Thymeleaf configuration)
```

为什么会报这个错误呢，这时候就需要我们去找源码了

![image-20211016212102341](https://s2.loli.net/2021/12/06/STMkaWmiXb8OdBl.png)

又是自动配置的包下面，我们发现了熟悉的身影，我们知道，想要了解他的默认自动配置内容，就得去`Propeties`类里面找

```java
@ConfigurationProperties(
    prefix = "spring.thymeleaf"
)
public class ThymeleafProperties {
    private static final Charset DEFAULT_ENCODING;
    public static final String DEFAULT_PREFIX = "classpath:/templates/";
    public static final String DEFAULT_SUFFIX = ".html";
    private boolean checkTemplate = true;
    private boolean checkTemplateLocation = true;
    private String prefix = "classpath:/templates/";
    private String suffix = ".html";
    private String mode = "HTML";
    private Charset encoding;
    private boolean cache;
    private Integer templateResolverOrder;
    private String[] viewNames;
    private String[] excludedViewNames;
    private boolean enableSpringElCompiler;
    private boolean renderHiddenMarkersBeforeCheckboxes;
    private boolean enabled;
    private final ThymeleafProperties.Servlet servlet;
    private final ThymeleafProperties.Reactive reactive;

    public ThymeleafProperties() {
        this.encoding = DEFAULT_ENCODING;
        this.cache = true;
        this.renderHiddenMarkersBeforeCheckboxes = false;
        this.enabled = true;
        this.servlet = new ThymeleafProperties.Servlet();
        this.reactive = new ThymeleafProperties.Reactive();
    }
```

这可不就来了吗，我们脑补一下就知道在自动配置类里面规定了当我们Controller层调用时，他会去`templates`目录下找到后缀为`.html`的内容，这不就是一个盗版的视图解析器嘛，还是比较好理解的

> SpringBoot的Template目录和我们之前的WEB-INF目录差不多，用户是不能从外部直接访问的，必须在我们内部通过转发得到

当然thymeleaf还是比视图解析器要强大多了，接下来我们看看他到底怎么用

#### 简单语法

```java
@Controller
public class Demo1 {
    @RequestMapping("/")
    public String test(Model model){
        model.addAttribute("msg","<h1>test</h1>");
        model.addAttribute("list", Arrays.asList(1,2));
        return "test";
    }
}
```

Controller和SpringMVC一点都没有区别，由于thymeleaf是请求转发到`.html`页面，因此我们要在Template里面新建一个`test.html`

```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <div th:text="${msg}"></div>
    <div th:utext="${msg}"></div> <!--不转译-->
    <div th:each="var:${list}" th:text="${var}"></div>
    <div th:each="var:${list}">[[${var}]]</div>  <!--行内格式，不推荐-->
</body>
</html>
```

如上代码，想要使用thymeleaf，只需要在头部引用到他的命名空间约束，之后在几乎任何标签属性前加上`th:`即可，然后后面就可以像jsp一样快乐的使用表达式了，下面是显示效果

![image-20211017170406575](https://s2.loli.net/2021/12/06/mfg7oxUl5JZSLKj.png)

实际上thymeleaf就是用一堆标签来代替了jsp的一系列功能，使得我们能在html页面中动态的制定一些内容

接下来的学习中我们会在应用中慢慢的接触其他的语法

### 整合数据库

对于数据访问层，无论是否是关系性数据库，SpringBoot底层都是采用SpringData的方式进行统一管理

其中SpringData也是一个和SpringBoot齐名的知名项目

首先先创建一个项目

![image-20211017194910834](https://s2.loli.net/2021/12/06/m9jYAoF1ElutXPR.png)

之后直接在`application.yml`里面编写数据库连接信息即可

```yml
spring:
  datasource:
    username: root
    password: 123456
    driver-class-name: com.mysql.cj.jdbc.Driver
    url: jdbc:mysql://localhost:3306/mybatis?useUnicode=true&characterEncoding=uft-8
```

然后在测试类里面添加数据源，通过自动装配，就可以自动将数据库的信息注入到该数据源中

```java
@SpringBootTest
class Demo03ApplicationTests {

    @Autowired
    DataSource dataSource;

    @Test
    void contextLoads() {
        System.out.println(dataSource.getClass());
    }

}
```

最后输出结果可以看出SpringBoot默认的数据源是Hikari，之前也介绍过

之后我们就可以通过SpringBoot自动注入好的JDBCTemplate来执行SQL语句进行查找数据内容

```java
@Data
@AllArgsConstructor
@RestController
public class JDBCController {
    private final JdbcTemplate jdbcTemplate;  // 注意这里只有一个有参构造，会自动装配属性

    @GetMapping("/")
    public List<Map<String,Object>> userList(){  // 万能的Map传值，可以不需要实体类了
        String sql = "select * from mybatis.user";
        return jdbcTemplate.queryForList(sql);
    }
}

```

> 注意再次之前要导入web包

### 整合Druid

Druid可以说是功能最强大的数据池了，利用它我们在获取数据的同时还可以非常方便的对数据请求进行监控

首先还是要导入Druid依赖，同样选择`starter`导入，这样在项目启动时会自动配置bean，省去我们的一些配置操作

```xml
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>druid-spring-boot-starter</artifactId>
    <version>1.2.5</version>
</dependency>
```

现在在别的内容不变的情况下，其实我们项目已经在使用druid数据源了，当然我们还需要了解它的强大功能

```yml
spring:
  datasource:
    # 这里不用配在druid下也可以正常使用Druid作为数据源
    username: root
    password: 123456
    driver-class-name: com.mysql.cj.jdbc.Driver
    url: jdbc:mysql://localhost:3306/mybatis?useUnicode=true&characterEncoding=utf-8
    druid:
      # 由于使用了starter，这里的配置内容会默认在项目启动时自动配置
      # druid 数据源专有配置
      # 初始化大小，最小，最大
      initialSize: 5
      minIdle: 5
      maxActive: 200
      # 配置获取连接等待超时的时间
      maxWait: 60000
      # 配置间隔多久才进行一次检测，检测需要关闭的空闲连接，单位是毫秒
      timeBetweenEvictionRunsMillis: 60000
      # 配置一个连接在池中最小生存的时间，单位是毫秒
      minEvictableIdleTimeMillis: 300000
      # 用来检测连接是否有效的sql，要求是一个查询语句
      validationQuery: SELECT 1 FROM DUAL
      # 建议配置为true，不影响性能，并且保证安全性。申请连接的时候检测，如果空闲时间大于timeBetweenEvictionRunsMillis，执行validationQuery检测连接是否有效。
      testWhileIdle: true
      # 申请连接时执行validationQuery检测连接是否有效，做了这个配置会降低性能
      testOnBorrow: false
      # 归还连接时执行validationQuery检测连接是否有效，做了这个配置会降低性能。
      testOnReturn: false
      # 是否缓存preparedStatement，也就是PSCache。PSCache对支持游标的数据库性能提升巨大，比如说oracle。在mysql下建议关闭。
      poolPreparedStatements: true
      # 要启用PSCache，必须配置大于0，当大于0时，poolPreparedStatements自动触发修改为true。
      max-pool-prepared-statement-per-connection-size: 50

      #配置监控统计拦截的filters，stat:监控统计、log4j：日志记录、wall：防御sql注入
      #如果允许时报错  java.lang.ClassNotFoundException: org.apache.log4j.Priority
      #则导入 log4j 依赖即可，Maven 地址：https://mvnrepository.com/artifact/log4j/log4j
      filters: stat,wall
      # 合并多个DruidDataSource的监控数据
      useGlobalDataSourceStat: true
      # 通过connectProperties属性来打开mergeSql功能；慢SQL记录
      connectionProperties: druid.stat.mergeSql=true;druid.stat.slowSqlMillis=500
```

当然上面的这些配置内容其实是个数据源都能做到，现在扩展一些Druid特有内容，比如开启自带的后台监控功能

由于使用了`starter`，我们直接在配置文件后加上开启统计视图的Servlet功能，并配置一些信息即可

```yml
stat-view-servlet:
  enabled: true
  login-username: admin
  login-password: 123456
  allow: 127.0.0.1
  url-pattern: /druid/*
```

这么简单代码感觉都不用解释，完全就是字面意思罢了

同样的通过配置文件中还可以配很多其他的东西，比如说过滤器功能

```yml
web-stat-filter:
  enabled: true
  url-pattern: /*
  # 这些请求不计入统计
  exclusions: /druid/*,*.js,*.gif
```

开启项目，测试，在地址栏输入`http://localhost:8080/druid`，就会自动跳转到Druid配置好的后台中

![image-20211019133905185](https://s2.loli.net/2021/12/06/AsXgD3bx7R8aGlu.png)

使用我们之前配置好的账户（admin）和密码（123456），登陆以后就可以看到内部强大的监控功能

![image-20211019134104245](https://s2.loli.net/2021/12/06/zPnbBj34ec17GCp.png)

还是非常强大的

### 整合Mybatis

跟着SpringBoot的思路，我们需要使用Mybatis，肯定要导入什么什么`-starter`的包才行

![image-20211019140821645](https://s2.loli.net/2021/12/06/FTbdMjwGgStkL5r.png)

直接选中即可

作为一个新项目，首先我们还是要先连接数据库

```yml
spring:
  datasource:
    username: root
    password: 123456
    driver-class-name: com.mysql.cj.jdbc.Driver
    url: jdbc:mysql://localhost:3306/mybatis?useUnicode=true&characterEncoding=utf-8
```

接着创建一个实体类用于存储从数据库接收过来的信息

```java
@Data
public class User {
    private int id;
    private String name;
    private String pwd;
}
```

作为一个Mybatis项目，mapper是必不可少的，所以接下来创建一个mapper接口

```java
@Mapper  // 表示这是一个mybatis的mapper类，里面包含了@Component类注解
public interface UserMapper {
    @Select("select * from mybatis.user")
    List<User> queryUser();
}
```

你可能很惊讶，但是事实上现在已经整合mybatis成功了，接下来我们测一下有没有地方写错

创建一个控制类

```java
@Data
@AllArgsConstructor
@RestController
public class UserController {
    private UserMapper userMapper;
    @GetMapping("/")
    public List<User> test(){
        return userMapper.queryUser();
    }
}
```

会发现只要我们想偷懒，甚至连一个`.xml`文件都不需要创建，直接就可以成功运行

而对于一些复杂sql语句，我们其实也是可以引入`xxxmapper.xml`文件的，只需要在`.yaml`配置文件里配一下即可

比如我们在resource目录下创建了`mapper/userMapper.xml`文件

```xml
<?xml version="1.0" encoding="GBK" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.test.mapper.UserMapper">
    <select id="queryUser" resultType="user">
        select *
        from mybatis.user;
    </select>
</mapper>
```

这时候我们只需要在`.yaml`中配置如下内容即可实现相同功能

```yaml
mybatis:
  mapper-locations: classpath:mapper/*.xml
  type-aliases-package: com.test.pojo
```

同样的，原本我们在`mybatis-config.xml`里写的内容其实都可以直接配置在`.yaml`中，或者通过

```yaml
mybatis:
  config-location:
```

的方式定位到某个配置文件

### 安全防护

之前我们学习了利用过滤器或者拦截器实现对不同特征的请求进行不同的操作分分流，实际上当前有非常多的框架自动为我们实现了这些麻烦的功能，我们只需要引入这些框架内容就可以轻松为自己的项目建立安全防护

这些框架共同的特点就是认证和授权功能，给每个用户分配不同的权限

其中最著名的就是**Shiro**和**SpringSecurity**

#### SpringSecurity

SpringSecurity也是Spring全家桶里面的一个项目，特点是和Spring的契合度极高，但是使用稍微复杂

- 首先还是要先创建一个新项目，导入这些依赖

  ![image-20211020134447315](https://s2.loli.net/2021/12/06/FilkSHeOr1GLpCd.png)

- 环境准备，在开始测试之前，我们需要进行现实环境的简单模拟

  ![image-20211020134053792](https://s2.loli.net/2021/12/06/riTmvkwdfIFM4AW.png)

- 接下来的第一步就是创建控制类，利用thymeleaf模板引擎，使得我们能够访问到`.html`文件

  ```java
  @Controller
  public class Router {
      @RequestMapping("/lv/{a1}")
      public String lv(@PathVariable("a1")int a1){
          return "views/lv"+a1 +"/1";
      }
  }
  ```

  > 这时候我们可以选择在pom文件中将SpringSecurity相关依赖给注掉然后测试一下基础环境的搭建情况，当然如果没有注掉Security的依赖的话，无论我们访问什么内容都会给跳转到Security自带的登录页面，看上去我们似乎没有办法通过控制类访问`.html`资源
  >
  > <img src="https://s2.loli.net/2021/12/06/mWRs3lndX2qLFyJ.png" alt="image-20211020135124296" style="zoom:50%;" />

- 上面发生的情况实际上是由于SpringSecurity的默认配置自动的拦截了所有请求，使得没有人拥有权限能够访问到我们设置好的内容，这意味着想要自定义不同用户的不同权限，我们只需要重写它提供的默认方法即可，

  因此我们创建一个控制类，继承SpringSecurity提供的`WebSecurityConfigurerAdapter`方法

  ```java
  // AOP
  @EnableWebSecurity
  // 链式编程，只需要一直.就完了
  public class SecurityConfig extends WebSecurityConfigurerAdapter {
  
      // 定制授权功能
      @Override
      protected void configure(HttpSecurity http) throws Exception {
          // 首页所有人可以访问，功能页只有有权限的人可以访问
          http.authorizeRequests()
                  .antMatchers("/").permitAll()
                  .antMatchers("/lv/1/**").hasRole("lv1")
                  .antMatchers("/lv/2/**").hasRole("lv2");
          // 没有权限默认会跳转到登录页（/login)，需要开启登录页面
          http.formLogin();
          // 可以通过.loginPage("/tologin").loginProcessingUrl("/login");定制登录页，一旦指定了它提供的页面就没用了
          // 其中第一个/tologin指的是Controller里面对应的请求转发页面，后一个/login指的是登录页html页面中表单的转发请求
          // 注销，开启注销页面（/logout）
          http.logout().logoutSuccessUrl("/");  // 注销成功跳到首页
          // 开启记住我功能，保存在cookie中，关闭浏览器依旧可以保存登陆状态
          http.rememberMe();  // 默认保存两周
      }
  
      // 定制认证功能
      @Override
      protected void configure(AuthenticationManagerBuilder auth) throws Exception {
          // 实际开发中一般从数据库中获取认证，这里先用从内存获取认证来演示
          auth.inMemoryAuthentication().passwordEncoder(new BCryptPasswordEncoder())
                  .withUser("admin1").password(new BCryptPasswordEncoder().encode("123456")).roles("lv1").and()
                  .withUser("admin2").password(new BCryptPasswordEncoder().encode("123456")).roles("lv2");
          // 注意密码必须要编码格式，不然不仅会报错而且很容易被别人破译，不安全
      }
  }
  ```

- 接着我们就可以通过我们设定的认证方式访问到不同的页面了，同时这个认证的内容是保存在session中的，意味着在一次会话中我们都可以用这一身份进行浏览内容

可以看出这个SpringSecurity的核心方法都是一种新奇的链式编程的方式，同时采用了AOP的思想，相当于一个智能化的过滤器，对客户端发起的各种请求都进行拦截和判断，只用符合设定的条件的内容才给予放行

#### Shiro

Shiro是Apache的一个强大且易于使用的Java安全框架，可以执行认证、授权、密码学和会话管理。利用Shiro简单易懂的API，你可以快速、轻松地保护任何应用程序--从最小的移动应用程序到最大的网络和企业应用程序。

这意味着不仅是JavaEE项目，甚至是JavaSE项目也可以使用Shiro作为安全验证

想要在SpringBoot中集成Shiro，由于不是Spring官方的框架，没办法一键导入，我们只能在创建好的项目中添加Shiro启动器依赖

首先我们要了解到Shiro的核心是三层核心组件，分别是Subject, SecurityManager 和 Realms.

- Subject：即“当前操作用户”。但是，在Shiro中，Subject这一概念并不仅仅指人，也可以是第三方进程、后台帐户（Daemon Account）或其他类似事物。它仅仅意味着“当前跟软件交互的东西”。Subject代表了当前用户的安全操作，SecurityManager则管理所有用户的安全操作。
- SecurityManager：它是Shiro框架的核心，Shiro通过SecurityManager来管理内部组件实例，并通过它来提供安全管理的各种服务。
- Realm： Realm充当了Shiro与应用安全数据间的“桥梁”或者“连接器”。也就是说，当对用户执行认证（登录）和授权（访问控制）验证时，Shiro会从应用配置的Realm中查找用户及其权限信息。

多说无益，还是之前同样的项目，相同的味道，让我们再次尝试对不同的用户进行拦截

这次我们采用从数据库中取出用户名和密码，所以还需要[整合Mybatis](#整合Mybatis)

- Mapper

  ```java
  @Mapper
  public interface UserMapper {
      @Select("select * from mybatis.user where name=#{name}")
      public User queryUserByName(String name);
  }
  ```

- 接下来创建我们自己的Realm类，实现对不同用户的认证和授权

  ```java
  @Configuration
  @Scope("prototype")  // 不知道是否是要加多例的注解。。。因为正常代码中这个类时使用时临时new出来的
  @RequiredArgsConstructor
  public class UserRealm extends AuthorizingRealm {
  
      // 通过连接数据库查找账号密码信息
      final UserMapper userMapper;
  
      @Override
      // 当我们的login界面一点提交，就会被这个方法劫持内容，它默认就规定了第一项是用户名第二项是密码
      // 用户名可以通过getPrincipal获得，但是传入的密码我们也获取不到，所以必须通过返回值来交给shiro判断
      protected AuthenticationInfo doGetAuthenticationInfo(AuthenticationToken token) throws AuthenticationException {
          System.out.println("认证");
          User user = userMapper.queryUserByName((String) token.getPrincipal());  // 获取用户登录名
          if (user==null) {
              return null;
          }
          // 这样就可以在完全不知道密码的情况下完成登录，但是还是可以加密（MD5盐值加密）
          // 这个方法实际上就是将认证到的详细内容（也就是登录页面被封装好的token）包装好传给认证信息类，其中第二个参数会与传进来的pwd比对，不一致会抛出异常
          return new SimpleAuthenticationInfo(user.getName(),user.getPwd(),getName());
      }
  
      @Override
      // 当我们想要访问某个在配置文件中经perm修饰的路径时（此项目为/lv/2），会被此方法拦截并获取到该用户的信息（该信息应由认证方法返回传入）
      // PrincipalCollection即为信息的载体，它安全的接收了Object中的有关用户信息的内容（即上个方法中返回的第一个参数）
      protected AuthorizationInfo doGetAuthorizationInfo(PrincipalCollection principalCollection) {
          System.out.println("授权");
          SimpleAuthorizationInfo info = new SimpleAuthorizationInfo();
          // 给指定用户添加2权限
          // getPrimaryPrincipal获取到的实际上就是认证信息类里面第一个参数的内容
          if (principalCollection.getPrimaryPrincipal().equals("用户1")) {
              info.addStringPermission("2");  // 一般来说数据库中会有一个权限表，用来判断哪个用户有哪个权限
          }
          return info;
      }
  
  }
  ```

- 然后我们创建Shiro的配置组件，集成有关权限控制的所有信息

  ```java
  @Configuration
  @RequiredArgsConstructor
  public class ShiroConfig {
  
      // 从IoC池中获取我们配置的realm对象
      private final UserRealm realm;
  
      @Bean
      public ShiroFilterFactoryBean getShiroFilterFactoryBean(){
          // 将realm传入defaultWebSecurityManager
          DefaultWebSecurityManager securityManager = new DefaultWebSecurityManager();
          securityManager.setRealm(realm);
          // ShiroFilterFactoryBean，整合SecurityManager，同时包含了对于权限的控制信息（即过滤条件）
          ShiroFilterFactoryBean bean = new ShiroFilterFactoryBean();
          bean.setSecurityManager(securityManager);
          // 为指定页面设定权限
          Map<String,String> map = new LinkedHashMap<>();
          map.put("/lv/1","authc");  // authc：需要认证才可访问
          map.put("/lv/2","perms[2]");  // perms：必须是认证了并拥有2这个权限的用户才能访问
          bean.setFilterChainDefinitionMap(map);
          // 自定义登录页面，不过Shiro没有内置的登录页面，所以我们必须指定页面
          bean.setLoginUrl("/toLogin");
          return bean;
      }
  }
  
  ```

之后启动项目，我们就可以实现和之前几乎相同的效果了

### Swagger

Swagger是比较流行的API框架，也就是一个RestFulAPI文档在线自动生成工具，可以保证API文档与API定义同步更新，同时支持多种语言（Java，PHP等）

#### 简单环境

我们需要在项目中使用Swagger，千篇一律的要从导入jar包开始

Swagger在3.0之后变得更加简单，现在我们只需要导入这个依赖

```xml
<dependency>
    <groupId>io.springfox</groupId>
    <artifactId>springfox-boot-starter</artifactId>
    <version>3.0.0</version>
</dependency>
```

然后启动项目，访问`http://localhost:8080/swagger-ui/`，接着最简单的Swagger页面就展示出来了

![image-20211025000652190](https://s2.loli.net/2021/12/06/5pmkY67Z39bWiAB.png)

这也就是SpringBoot的好处，其实，所有的事情都是在AutoConfig文件里做的，就像其他starter做的事情一样。从源码中，我们发现swagger和ui组件默认都是开启的

当然只有这么一个简单的页面显然是不够的，所以我们需要对其进行配置

#### API内容配置

我们访问的上面这个页面究竟会显示什么东西实际上是由一个叫做`Docket`的对象bean控制的，如果我们需要自定义显示内容，只需要自己创建一个Docket的bean即可

创建一个bean，在SpringBoot中，仅有`@Configuration`加`@Bean`的模式了

```java
@Configuration
public class SwaggerConf{
    @Bean
    // 配置了Swagger的bean实例（即这里的Docket），我们所有的对Swagger的配置都可以往这个Docket里面丢
    public Docket createRestApi() {
        // OAS_30代表我们使用的是Swagger3.0+版本，如果用2.0+就是SWAGGER_2
        // 同样是链式编程，想要配置什么值直接一直.就可以了
        return new Docket(DocumentationType.OAS_30)
            	.pathMapping("/")  // 给
                .enable(true)  // 是否启动swagger，可以通过外部开发环境传值
                .apiInfo(new ApiInfo("Swagger标题",  // 配置在API页面上显示信息的内容（没啥用）
                        "Swagger描述",
                        "版本号",
                        "服务网站",
                        new Contact("作者信息","作者网站url","作者邮箱email"),
                        "证书",
                        "许可证网站",
                        new ArrayList<>()))
                // 选择哪些接口作为swagger的doc发布（从select开始到build结束）
                .select()
                .apis(RequestHandlerSelectors.basePackage("com.test.controller"))  // 配置要扫描接口的方式
                // any()表示扫描全部，none()表示都不扫描，basePackage()指定包扫描，还有两个是扫描特定的注解
                .paths(PathSelectors.any())  // 过滤什么路径
                .build()  // 工厂模式
                .groupName("group1");  // 给每一个Docket分组，需要另一个组就在这里再加一个即可
    }
}
```

这么一通操作，最后我们显示的页面是这样的

![image-20211026152546778](https://s2.loli.net/2021/12/06/h3OVcluCv4U7ipZ.png)

会发现这个route（即controller类名）里面已经将我们的`/test`路径内容识别进来了，如果之前在参数中的`.RequestHandlerSelectors`配的是any，则还会出现`model`和`error`的内容（虽然里面没东西）

#### 输出注解&调试

比如我们存在一个用户的实体类，此时我们如果在实体类中加一些注释

```java
@Data
@ApiModel("用户")
public class User {
    @ApiModelProperty("用户名")
    private String username;
    @ApiModelProperty("密码")
    private String password;
}
```

然后我们重新创建一个控制路径，同样也添加一些注释，而且尝试返回到User值

```java
@PostMapping("/user/{username}/{password}")
@ApiOperation("user请求")
public User user(@ApiParam("输入用户名")@PathVariable("username")String username,
                 @ApiParam("输入密码")@PathVariable("password") String password){
    User user = new User();
    user.setUsername(username);
    user.setPassword(password);
    return user;
}
```

此时我们再次启动项目，打开route内部的内容，就可以发现自己写的注释显示在特定的位置中

![image-20211026162620991](https://s2.loli.net/2021/12/06/eyLbE8ofMrgJ63K.png)

从这就能看出，swagger可以对每一个人编写的接口（控制类）进行调试，同时输出调试信息，在团队开发中及最后调试中用处非常大

### 任务管理

#### 异步任务

当我们的某个服务操作需要耗费一定时间时，为了不让用户等待太久，我们可以选择先提前响应内容，将耗时任务放到另一个线程中慢慢执行，从而提升用户体验

比如有这么一个服务类和控制类

```java
@Service
public class DelayService {
    public void delay(){
        System.out.println("数据正在处理...");
        try {
            Thread.sleep(3000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```

```java
@Controller
public class AsyncController {

    @Autowired
    DelayService delayService;

    @ResponseBody
    @GetMapping("/")
    public String test(){
        delayService.delay();
        return "OK";
    }
}
```

正常情况下，由于控制类需要等待三秒才能给出响应，因此在执行return之前浏览器就会转三秒的圈圈，用户看着圈圈只能干跺脚，因此我们可以在服务类的耗时方法上加上`@Async`标签，并在main方法内开启异步功能

```java
@Service
public class DelayService {
    @Async
    public void delay(){
        System.out.println("数据正在处理...");
        try {
            Thread.sleep(3000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```

```java
@EnableAsync
@SpringBootApplication
public class Demo08Application {

    public static void main(String[] args) {
        SpringApplication.run(Demo08Application.class, args);
    }

}
```

即可直接秒加载

#### 邮件任务

想要发邮件也很简单，我们直接先导一个包

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-mail</artifactId>
</dependency>
```

之后进行邮箱的配置，告诉它我们要用什么邮箱进行发送

当然在此之前我们得先获取到我们邮箱的账号密码信息，其中的密码并不是我们登陆密码，一般的邮箱页面会给我们一个专用密码供我们使用（比如qq就可以通过设置里打开smtp服务获取专用密码）

以下是配置文件

```yaml
spring:
  mail:
    username: qys.chillyblaze@gmail.com
    password: # 这里要填的是通过设置的专用密码，一般邮箱会进行两步验证之类
    host: smtp.gmail.com
    properties:
      mail.smtp.ssl.enable: true
```

之后我们就可以直接发送邮件了，比如我们可以在测试类中试一下

```java
@SpringBootTest
class Demo08ApplicationTests {

    @Autowired
    JavaMailSenderImpl mailSender;

    @Test
    void contextLoads() {
        final SimpleMailMessage message = new SimpleMailMessage();
        message.setSubject("主题测试");
        message.setText("文本测试");
        message.setTo("qys.chillyblaze@gmail.com");  // smtp发送
        message.setFrom("qys.chillyblaze@gmail.com");  // pop接收
        mailSender.send(message);
    }

}
```

SpringBoot好就好在提供了一系列的配置工具，我们不费吹灰之力就可以直接实现邮件发送

当然还有复杂邮件发送，此处不提

#### 定时任务

比如有时候会设定几点钟更新，几点钟日志输出，这些都需要利用定时任务功能

SpringBoot的Spring框架为我们提供了函数式接口来进行定时任务操作，我们不需要导包就可以直接使用

它和异步任务很类似，我们也是要在启动类上开启服务并且在方法上注解即可

```java
@SpringBootApplication
@EnableScheduling
public class Demo08Application {

    public static void main(String[] args) {
        SpringApplication.run(Demo08Application.class, args);
    }

}
```

```java
@Service
public class ScheduledService {
    // 秒 分 时 日 月 周几，*表示任意，?表示不确定
    // 异步执行，不需要管他，同时注意这里代表的是每分钟的第二秒执行，而不是每两秒执行一次
    @Scheduled(cron = "2 * * * * *")
    public void hello(){
        // 希望在特定的时候执行
        System.out.println("ScheduledService.hello");
    }
}
```

可以发现这里使用了cron表达式，如果不会写的话网上也有生成器可以使用

![image-20211026181101571](https://s2.loli.net/2021/12/06/GKNgRDL5xU1oZFu.png)

可以看出语法还是比较强大的，只需要这样简单的配置，当我们启动项目的时候就能够定时执行了

# Git

Git是一个**开源的分布式版本控制系统**，可以有效、高速地处理从很小到非常大的项目版本管理。

> 版本控制就是某个可以保存老版本并且实时更新新版本的控制系统

## 对比SVN

SVN也是一个版本控制的工具，但是利用的是集中式的版本控制，会将所有的更新代码保存在统一的服务器上，多人协作进行开发时，每个开发者从统一的资源路径下取得最新的版本进行修改和提交

但是这种方案有一个问题，由于每个用户都得去中央服务器中取得版本内容，一旦中央服务器崩了，每个开发者就不能实时获取到最新的内容

这也就诞生了Git，也就是分布式版本控制，所有版本信息仓库全部司步到本地的每个用户，这样就可以在本地查看所有版本历史，可以离线在本地提交，只需在连网时push（同步）到相应的服务器或其他用户那里。由于每个用户那里保存的都是所有的版本数据，只要有一个用户的设备没有问题就可以恢复所有的数据。这样就不会因为服务器损坏或者网络问题，造成不能工作的情况！

**分布式版本控制的特点就是用户之间可以互相从别人那里更新所有版本内容**

## Git安装

先从官网下载最新版本，然后安装的时候实在不行一直点下一步就可以了

安装完成后菜单里会多出来几个东西（如果勾选了添加到菜单的话）

- Git Bash：是Linux风格的命令行，使用最多
- Git CMD：Windows风格的命令行，和上面那个就只有命令代码之间的区别，配置到环境变量之后直接可以在cmd里面使用
- Git GUI：图形化界面，不建议使用

## Git基本原理

Git本地有四个工作区域：

- 工作区（Workspace）：即我们开发中各种的项目文件，
- 暂存区（IndexStage）：是一个`index`文件，里面跟踪了我们曾经`add`进去的文件快照（`add`可以理解为文件保存），使得当内容被放入暂存区之后，即使我们更改了工作区内的内容，暂存区中仍存放着我们上一次`add`的内容，但是与资源库不同的是每一次`add`的记录本身将不会被保存
- 资源库（Repository）：本地的代码库，由一个个分支（HEAD指向的即为当前分支）组成，我们在暂存区的内容通过`commit`提交到某一个分支中，添加了提交信息之后这一次提交记录和当前的项目快照将会被永久保存
- 远程库（Remote）：代码托管的服务器，即GitHub

其实我们需要打交道的就是工作区和远程库，暂存区和资源库一般理解里都在项目的`.git`目录中

文件在这四个区域之间的转换关系如下，每一个关系就是一条命令

![image-20211111094931370](https://s2.loli.net/2021/12/05/p5lqMBG9cL2XhRH.png)

## 本地bash指令

git里面的命令都以git命令开头，下面的命令都省略git代码

- 使用git第一步是对其进行必要的配置，可以通过`config..`进行配置操作

  - `-l`列出配置清单

  - `--system --list`列出系统配置的内容

  - `--global --list`列出用户配置的信息

    > 注意系统的配置内容在`git/etc/gitconfig`文件内
    >
    > <img src="https://s2.loli.net/2021/12/05/5a1r83iUsAcmI4S.png" alt="image-20211027210917502" style="zoom: 37%;" />
    >
    > 而用户的配置则都在`user/.gitconfig`文件中
    >
    > <img src="https://s2.loli.net/2021/12/05/nMoTQwiBhCYcO3g.png" alt="image-20211027211043285" style="zoom:50%;" />
    >
    > > 这里其实是我在安装的时候勾选了默认采用VSCode编辑器的缘故，也算是安装的时候自动配的文件

  - `--global user.name [用户名]`配置用户名，除此之外还需要配置`user.email`，如果想要之后提交到远程仓库时能够被远程仓库识别为你，就需要设置远程仓库的用户名和邮箱

    ![image-20211114000258025](https://s2.loli.net/2021/12/05/oTuaMF1LgtN4d67.png)

    设定完毕后可以通过`–list`查看正确性，之后也可以去之前的文件里看看是否添加成功

    ![image-20211027211919124](https://s2.loli.net/2021/12/05/h7KqmYzGC1tlrn8.png)

- 配置完成后我们就要创建一个仓库，我们可以选择创建本地仓库和克隆远程仓库

  - 创建本地仓库，就在将要创建仓库的地方打开bash，`git init`自动创建出最关键的`.git`目录

    ![image-20211028150906704](https://s2.loli.net/2021/12/05/E37AKGNWR4apZHY.png)

  - 克隆远程仓库，我们就先去GitHub上面随便选择一个项目，点击醒目的code按钮

    ![image-20211028151623795](https://s2.loli.net/2021/12/05/GqW7n6vVc2BTZUj.png)

    复制下这段链接，我们在仓库文件夹中同样打开bash，`git clone [url]`即可克隆远程仓库

    > 可能会遇到无法连接的情况，这时候就需要万能的代理出手
    >
    > ```bash
    > git config --global http.proxy "http://127.0.0.1:7890"
    > git config --global https.proxy "https://127.0.0.1:7890“
    > ```
    >
    > 记得在clash里面打开允许局域网连接，同时这里设置的值前缀还可以改成`socks5`，注意端口一定要写对，同时注意就算代理了流量也是ping不通的（因为ping操作走的不是http协议）

- 完成本地仓库的设置之后，我们就可以对其中的文件进行文件操作

  - `status`查看当前git目录下的各个文件状态，`untracked`代表的就是只在工作目录下未添加到暂存区，同时还可以在后面跟上文件名对某一文件的状态进行特定显示

    ![image-20211029103548701](https://s2.loli.net/2021/12/05/8c4slAn6I3kWmOM.png)

  - 这时候如果我们想添加到暂存区，只需要`add .`即可提交所有文件到暂存区

    ![image-20211029103905818](https://s2.loli.net/2021/12/05/BFpP6k5Da17tUqd.png)

  - `commit -m`将暂存区中的文件提交到本地仓库，并添加备注信息（必需）

    ![image-20211113102259458](https://s2.loli.net/2021/12/05/Wlr36y1HFbIq8do.png)

    > 这里变化了git项目位置，但是不要紧，之前的操作都没变，仅为之后的联动远程仓库做准备

  - 同时还可以通过`status --short`简短但是有效的显示当前目录下的所有内容状态信息

    假设当前突然修改了已提交的1.txt文件的内容，再次查看时会变成这样

    ![image-20211113104111510](https://s2.loli.net/2021/12/05/2mh7YUCHqzrcaPO.png)

    红字表示该文件已被跟踪，但是把**当前工作区的文件内容**（下层区）和**之前暂存的文件**（上层区）进行比对并不一致，因此提示`modified`（文件被修改但未暂存`add`），这时候通过`status --short`展示如下

    ![image-20211113104429000](https://s2.loli.net/2021/12/05/k2nuXwz7csErA9F.png)

    发现文件前面第二位出现了红色的M，接下来我们对修改后的文件进行重新add，再次查看

    ![image-20211113104551374](https://s2.loli.net/2021/12/05/6OhcFvuCreRt2xS.png)

    发现M变成了第一位而且变绿了，这其实表示的是git将**当前暂存的文件**（下层区）和**资源库内之前提交的文件**（上层区）进行比对发现不一致，因此同样是提示`modified`但是含义不同（文件被修改但未提交`commit`）

    自此，我们了解了`--short`两位状态码XY（分别对应上面的绿M位和红M位）的位置含义，即代表暂存区和另外两个区哪个区比对之后的结果展示，除了M之外其实面对文件发生状态的不同还会有另外的字母，以下是官方的介绍

    - ' ' = unmodified
    - *M* = modified
    - *A* = added，下层区出现新的文件但是上层区没有这个文件（仅出现在第一位）
    - *D* = deleted，下层区把文件删掉了但是上层区还留有上次提交的副本
    - *R* = renamed，下层区文件被改名了
    - *C* = copied，不是很重要
    - *U* = updated but unmerged，未合并（合并和分支有关，详见后边）
    - *??* = 未被跟踪的文件
    - *!!* = 被忽略的文件

  - `log [文件名]`当我们已经提交一个文件之后就无法通过`status`定位文件的状态，这时候就需要通过`log`指令展示所有的提交记录和其他提交信息（提交用户，邮箱等），当然也可以通过加文件名的方式查看某一个文件的提交记录

    ![image-20211113102930064](https://s2.loli.net/2021/12/05/9SPwFo4dTZMXNUI.png)

    > 还可以用`shortlog`查看简短的提交信息

这样最简单的git指令就已经差不多搞定了，但是我们会发现上面的add和commit命令其实会提交所有文件，但是有些文件我们不想要提交，这时候就需要通过添加忽略文件（`.gitignore`）

> 我们会发现之前建立SpringBoot项目的时候会自动生成这个文件

随便在网上搜一个`.gitignore`文件配置就可以了，里面可以排除相关的文件，不将其add到暂存区，也就不会被commit全部提交上去

## 分支，合并和冲突

*几乎每一种版本控制系统都以某种形式支持分支。使用分支意味着你可以从开发主线上分离开来，然后在不影响主线的同时继续工作。*

*有人把 Git 的分支模型称为**必杀技特性**，而正是因为它，将 **Git** 从版本控制系统家族里区分出来*。

<p align="right"><i>——菜鸟教程</i></p>

当我们了解完如何提交自己的代码到远程之后，实际上这只是一个开始，也是一个不成熟的提交操作，在实际的开发中，我们必须运用分支+合并的方式对一个项目进行维护和添加功能，即当我们需要给项目添加某个功能但是并不清楚是否会发生错误导致整个项目崩溃时，就可以在主分支下创建一个新的分支，新的分支创建时默认会拥有当前分支的所有信息，在新分支中添加完新功能并测试成功之后再将其安全的合并到原有项目中

不仅安全方面有保障，在我们给新分支中添加新东西时，原本的主分支仍旧在以旧版本正常运行，直到我们将内容合并到主分支中，一定程度上也实现了主分支版本的更替

- `branch`可以查看当前分支信息，加上`-v`则可以看到详细信息，后面加上分支名则可以创建一个新的分支，`checkout [分支名]`可以切换到指定分支

  ![image-20211113145506631](https://s2.loli.net/2021/12/05/cfCa7iVgXTmydv8.png)

  > 这里省略了上面的修改后的commit操作

- 之后比如说我们修改了1.txt文件，并把修改后的1.txt提交到`feature_test`分支的资源库下，再次查看分支信息

  ![image-20211113150336201](https://s2.loli.net/2021/12/05/6AWUcfvz5VFJm9d.png)

- 这时候如果`feature_test`的功能已经开发完毕，则我们需要将其合并到主分支master当中

  注意，想合并到哪个分支，比如现在想合并到主分支，就应该切换到主分支下操作合并动作

  ![image-20211113151124473](https://s2.loli.net/2021/12/05/MCV2zyDtf1l69WP.png)

- 但是分支的合并一般也不是一帆风顺的，比如现在两个分支中分别有不一样的内容且无法合并时

  ![image-20211113152135303](https://s2.loli.net/2021/12/05/qL9OnIo8JdHmZ7k.png)

  很明显能看出，1234和1235两个内容是没有办法一下子合并的，这时候就会出现冲突警告

  ![image-20211113152410494](https://s2.loli.net/2021/12/05/lF5bAHN6mG3yEhc.png)

  这时候我们打开`1.txt`会发现内容已经变成了奇怪的样子

  ![image-20211113152808107](https://s2.loli.net/2021/12/05/7qE8TaSbVtzPfhJ.png)

- 这时候我们应该对内容进行人工审核并保存最终审核内容（比如此处保存123)，重新提交一次即可解决冲突问题

  ![image-20211113155133877](https://s2.loli.net/2021/12/05/7BZsnQrCv5gUwY9.png)

同时当我们合并完一个分支之后，一般来说我们会删去合并来的分支达到项目的足够精简，同时git也建议我们能够删去已经被合并到其他分支的冗余分支

![image-20211113203644908](https://s2.loli.net/2021/12/05/gUyRLzcjCZ52TqD.png)

上图可以发现，在删除分支前git会自动帮助我们比对同一目录下的其他分支，看看这个被删除的分支是否真的已经合并到了别的分支中，如果没有完全被合并，则会提醒我们

## ssh连接远程仓库

由于我们平时工作在本地仓库，想要提交到远程仓库就要和其建立连接，所以我们要设置本机绑定SSH公钥，实现免密码登录Github

由于之前连接虚拟机的时候使用过ssh，因此我已经创建过公钥了，直接在`C:\Users\Lenovo\.ssh\id_rsa.pub`拿来用即可，复制好之后进入github设置里面添加新的SSHKey，标题随便写，下面的Key复制进我们之前复制的公钥，点击保存

![image-20211029123841638](https://s2.loli.net/2021/12/05/XVTkNx5HvyhsCPK.png)

连接好之后打开Bash，`ssh -T git@github.com`测试连接状况

![image-20211029124047930](https://s2.loli.net/2021/12/05/tiRr5YOAEK1pTsJ.png)

## 本地&远程仓库协同运作

上面介绍了本地如何创建一个git仓库并提交到本地的资源库，同时也成功连接了远程的仓库，这时候如何能够使本地和远程仓库相配合，从而对我们的项目进行完整的版本控制就是一个问题

### 推送本地内容至远程

1. 首先确定当前的本地和远程仓库情况，并做一些初始准备

   - 本地仓库已提交了一个`1.txt`文件到资源库
   - 本地仓库已连接到远程仓库，并且测试连接成功

2. 创建一个空白的远程仓库（以GitHub为例）

   ![image-20211113112220762](https://s2.loli.net/2021/12/05/KivMAa2N4koxPIj.png)

   

3. 从本地创建一个远程库别名，这样我们不需要记一长串地址就能够直接提交到远程库

   ![image-20211113140820028](https://s2.loli.net/2021/12/05/5goMsQUVmWIxnbc.png)

   > 其中的地址就是之前我们clone的时候复制的地址

4. 本地直接`push [目标远程仓库别名] [本地分支]`到该仓库即可将资源库里面的内容全部上传到远程

   ![image-20211113161715515](https://s2.loli.net/2021/12/05/oTBrbHQ3Kzy5Fiq.png)

   之后我们打开GitHub刷新仓库内容，即可发现我们的文件已经被推送到远程了，包括我们所有的commit记录

   ![image-20211113162014245](https://s2.loli.net/2021/12/05/6AuckLeZaSOw9Wo.png)

这时候，暂存区，资源库，远程仓库分别是三个独立的运作系统，正常情况下每一个区当中都保有一份当前的项目内容，无论哪个部分出现故障，都能保证整体内容不出差错

有人可能会想，在这种情景下如果我们又回到了`feature_test`分支推送内容到GitHub，会发生什么事情呢

![image-20211113164331008](https://s2.loli.net/2021/12/05/LnrD3TVMgRtjpqu.png)

![image-20211113164549506](https://s2.loli.net/2021/12/05/Hym4XzE6nMsTIJR.png)

远程也确实增加了一个分支，但由于本身我们推送的master分支就是由这个分支合并而来的，因此master分支拥有`feature_test`分支所有的commit和内容改动，即为`feature_test`的超集，因此这两个分支相安无事

GitHub也在线上提供了一个给予我们合并两个类似分支的方式，假设现在我们的两个分支存在相似和可合并之处，我们就可以人为的通过上方的`Pull requests - New pull request`来合并两个分支

![image-20211113165045827](https://s2.loli.net/2021/12/05/VewAzg5IhPci7kn.png)

![image-20211113165320939](https://s2.loli.net/2021/12/05/OehYaz6dbiprH9j.png)

至于真的出现了冲突需要修改，实际上和之前的分支合并操作是完全一样的，此处略

### 抓取远程内容并合并

学习了如何推送本地资源库内容至远程仓库，还有一个很重要的就是如何从远程仓库中拉取别人更新的内容并合并到本地，这在实际开发中也是不可或缺的，不可能所有人在一条流水线上工作，当我们花了很多时间做好一个更新内容的时候，可能在这期间别的人做好了别的新功能，已经推送到远程并更新了远程仓库，这时候就需要我们重新下载远程仓库的更新内容，与自己更新的内容进行合并，之后将整合好的所有内容再一次推送到远程

这非常符合逻辑，但是之前提到的`clone`是可以拷贝远程内容到本地，但是好像并不能做到和我们本地当前内容进行比较，这时候就需要`fetch+merge`出手

![image-20211113190849311](https://s2.loli.net/2021/12/05/1tPURv8VbgMDAQ4.png)

![image-20211113190558402](https://s2.loli.net/2021/12/05/VDnv6L2osr4GSdY.png)

可以看出`fetch`即是相当于将远程仓库中的内容以分支的形式克隆了下来，相关内容保存在`origin/[远程分支名]`这个虚拟分支中，我们可以查看其内的代码变化，修改到没有问题之后再切换回本地分支进行合并

![image-20211113191953164](https://s2.loli.net/2021/12/05/qz2iFPopVtOh8E6.png)

> 其中switch和checkout在此处功能相同，只是新版本git的新特性

同时执行了`fetch`命令之后会发现`.git/refs`目录下出现了一个`remotes`的目录，这个目录和上面的`heads`目录功能类似，都是用来记录和跟踪某个分支的，这里跟踪的即是远程仓库中的分支信息，便于我们进行合并

同时通过`branch -a`可以查看目前目录下所有分支（`-r`可以仅看远程`fetch`来的分支）

![image-20211113193150189](https://s2.loli.net/2021/12/05/RfLdzrpj9Oi1PSX.png)

-----

这样对Git也算有了一个大概的了解，事实上，Git除开介绍的正向提交内容并更新之外，更为强大的是其基本不会导致历史记录丢失的回滚能力，Git发明的目的就是保证在项目启动之后任何一个阶段的内容都不会真正意义上的消失，只要需要无论什么时候都可以方便的找到历史中的任意一个切片时间上的内容

当我们对Git有整体的印象之后，如果遇到了上述情况，如急需找到某一时期的提交内容，我们就可以运用自己的检索能力快速定位到所需要的指令内容，从而实现对任何数据的修补工作

## 项目管理

项目管理有几个不同的工作模式，分别如下

- **直接提交模式**

  clone之后本地直接在main分支上进行操作，并提交和推送，其中可能会出现push失败的情况但是没有关系，通过pull对冲突内容进行合并和修改，之后在本地对内容进行commit，然后再push即可

  如果开启原基模式，则会进入到rebasing模式，在此状态下同样也是对冲突文件进行修改并add，但是此时不再是commit。而是选择`git rebase --continue`退出原基模式，之后会让你输入提交信息一类的内容，输入完之后即可正常push

- **合并分支模式**

  在clone了某个仓库之后，立刻在本地创建一个dev分支，并保留clone之后别人的main主分支，所有的更新操作在dev分支上进行，当完成任务之后，切换到main分支进行pull（由于从来没有更改过主分支，因此此时主分支一定可以成功pull），接着再通过merge操作合并dev分支到主分支，删除dev分支，并push主分支

- **Fork+PR模式**

  除了在本地可以进行合并操作之外，如果仓库并不属于你个人，此时就需要在github上管理合并冲突内容，我们需要先fork一下别人的仓库，或者在github上创建一个新的分支，接着我们所有的操作都在这个fork出来的仓库或者新的分支上进行，同时注意push同样也是push到这个新的内容中，紧接着在网页中点击`Pull requests`新建一个PR请求，在上面选择好自己的仓库或者是分支，点击`Create pull request`即可



# Docker

## 概述

*Docker 是一个开源的应用容器引擎，让开发者可以打包他们的应用以及依赖包到一个可移植的镜像中，然后发布到任何流行的 Linux或Windows操作系统的机器上，也可以实现虚拟化。容器是完全使用沙箱机制，相互之间不会有任何接口。*

<p align="right"><i>——百度百科</i></p>

看上去并不好理解，事实上以后当我们开发一个项目时，除了代码部分的内容（即jar包下内容），我们可能还需要配置很多的环境，比如mybatis简单的数据库连接项目你就必须下载mysql和maven等环境，我们这边跑起来没问题，一上线服务器或交给别人来运行，所有的内容又需要重新部署一边，更有可能出现不能跨平台等问题，费时费力，这时候就需要Docker帮忙了

Docker可以将我们用Java开发的项目包括所有环境直接打包，其中的环境部分就叫做镜像，Docker会提供一个仓库，相当于手机上的应用商店，将打包好的所有环境全部放进仓库中，当另一个下载者运行代码时需要某个环境，直接从仓库中下载即可

Docker还有一个特性就是环境隔离，在Docker仓库中，每一套环境都是相互不会影响的，这意味着如果将一个项目部署到服务器中，不同的环境相互不影响，可以进一步将服务器资源运用到极致

## 容器化/虚拟机技术

我们可能会发现Docker的运行原理似乎和虚拟机比较像，事实上也的确如此，都是提供了一个似乎虚拟的环境供我们使用，但是Docker强就强在它的轻量级

![image-20211114211121151.png](https://s2.loli.net/2021/12/06/nF1tf87EqmNXT2e.png)

其中库文件实际上就是各种环境，可能会有很多种环境相互之间互相混杂，所有的应用都要跑在这个环境上， 免不了会发生环境之间的冲突，同时虚拟机还可以类比于你自己的电脑，每一次的启动都需要花费大把时间，明明你可能只是想开电脑写一个日记，电脑不知道你的需求还是会勤勤恳恳的加载完所有可能需要运行的环境内容

![image-20211115102823673](https://s2.loli.net/2021/12/06/b4aIugeQ9mhAORl.png)

可以看出容器化之后每个应用程序都带着自己少量的环境运行，同时Docker本身不带内核（用的是宿主机的内核）的特性更加避免了启动内

z核时的繁琐，这样我们通过Docker打开某一个应用程序，只需要启动少量但必需的环境即可运行程序，再也不需要进行启动虚拟机或者打开电脑动辄就是几分钟的加载环境过程

同时还有一点就是容器化的技术可以避免像虚拟机一样一堆环境耦合在一起，万一某两个环境冲突了找问题都要找半天，容器化之后，就算你两个容器中都下载了同一个环境，由于容器之间的隔离性，也永远不用担心环境崩溃

## 安装

首先我们要了解到Docker支持的只有Linux系统，如果我们想要在Windows内装Docker还需要装WSL（虚拟机环境），显得得不偿失了，因此我们需要一台虚拟机或者是服务器供我们测试Docker的使用

> 此处使用的是termius连接甲骨文云英国VPS内置的CentOS8系统，Docker[官方文档](https://docs.docker.com/)中也指明了支持的系统类型
>
> ![image-20211115183439983](https://s2.loli.net/2021/12/06/uxKY5WbMeyjv1qP.png)

同时在安装之前我们还是需要通过`cat /etc/os-release`来确定一下自己系统的一些内核即其他环境的配置信息

*To install Docker Engine, you need a maintained version of CentOS 7 or 8. Archived versions aren’t supported or tested.*官方文档中也明确了不会支持CentOS7以下的系统

![image-20211115184748147](https://s2.loli.net/2021/12/06/ALKeFI13oHYzv8R.png)

接着我们就可以开始愉快的安装了，其中官方文档写的非常详细，跟着他一步步来即可

1. 删除原有旧版Docker

   ```shell
   yum remove docker \
                     docker-client \
                     docker-client-latest \
                     docker-common \
                     docker-latest \
                     docker-latest-logrotate \
                     docker-logrotate \
                     docker-engine
   ```

2. 下载`yum-utils`工具包（用于维护yum软件包）及添加固定的Docker镜像仓库（此处可以选用国内镜像源）

   ```shell
   yum install -y yum-utils
   
   yum-config-manager \
       --add-repo \
       https://download.docker.com/linux/centos/docker-ce.repo
   ```

   

   ```shell
   yum erase podman buildah
   ```

3. 安装Docker引擎

   ```shell
   yum install docker
   ```

   >注意，CentOS8默认使用的是podman容器化技术，因此我们这里如果输成了`yum install docker`则会下到一堆不认识的东西，后面的内容也直接无法进行，如果手贱的话我们就执行`sudo yum erase podman buildah`卸载相关内容
   >
   ><img src="https://s2.loli.net/2021/12/06/F8xySnC69fg3NdR.png" alt="image-20211115192201173" style="zoom: 33%;" />

4. 启动Docker并测试是否安装成功

   ```shell
   systemctl start docker
   docker version
   ```

   ![image-20211115192748059](https://s2.loli.net/2021/12/06/7L38yYQHRPjfu4g.png)

   ```bash
   systemctl enable docker.service  # 开机自启
   ```

5. 测试运行`hello-world`

   ![image-20211115194442185](https://s2.loli.net/2021/12/06/myLS3ZwWrNuGdM8.png)

   这时候我们看着这个详细的四步解释运行原理，我们能够更加深刻的认识到Docker的运行原理

   ![731fc8043e0f71aab7851ad87427bdd6](https://s2.loli.net/2021/12/07/Nhi2vKtQYq7kxRu.png)

   我们输入命令的工具称之为客户端 Client，当我们在客户端输入命令时，命令会发送到 docker 所在主机的 daemon 进程，由该进程执行命令。当执行的是创建容器的命令时，如果对应的镜像不存在于本地，那么 daemon 会向远程 docker 仓库请求下载镜像，等镜像下载到本地后在创建容器。

   > 注意容器和镜像的关系就像是对象和类，镜像创建一个个容器就像是类实例化一个个对象

6. 为了验证我们的判断，我们可以查看刚刚下载到的hello-world镜像

   ![image-20211115202451021](https://s2.loli.net/2021/12/06/Kx4bnmJT8UsRCoE.png)

这样我们的一个最简单的Docker项目流程就完成了

## 镜像/容器控制常用命令

和git一样，所有的Docker命令都是`docker`开头的，下面的命令也都省略了前置的`docker`

同时所有的命令都可以在[文档](https://docs.docker.com/engine/reference/commandline/docker/)中找到，下面只列举常用指令的部分信息，同时下面是看帮助文档的方法

![image-20211115223820122](https://s2.loli.net/2021/12/06/qBMDzdgThE5rKxj.png)

- `[命令] --help`帮助命令，什么不会就查什么

- `info`比`version`更详细的Docker信息

- `search [镜像名称]`搜索某个镜像（类比于Github搜索仓库）

- `pull [镜像名称]`下载镜像，同时可以通过后面`:[版本号]`来指定下载版本（默认是最新版）

  > 当然版本也不能乱定，所有镜像的详细信息都可以在[DockerHub](https://hub.docker.com/)里面找到

- `rmi [镜像名称/ID]`删除下载到本地的镜像

上面的是有关镜像的命令，接下来通过在centos内再下一个ubuntu镜像来演示容器命令

![image-20211115214629480](https://s2.loli.net/2021/12/06/ldSGpkeqjhN25TM.png)

- `run`创建容器，上面提到过，容器和镜像就类比对象和类，本地的一个镜像并不能发生什么，想要让他起作用就必须把他run起来

  - `--name`容器名称（类比对象变量名）

  - `-d`后台方式运行

    > 注意到后台启动时如果前台没有应用需要它提供服务，Docker就会自动把他关闭掉

  - `-it`使用交互方式运行，进入容器查看内容

  - `-p [主机映射端口]:[容器端口]`指定容器的端口，也可以仅指定容器端口

    > 比如我们启动了一个Nginx服务，那么此时如果我们设定参数`81:80`意味着宿主机映射端口是81，在容器外部我们访问`localhost:81`可以访问到容器内部开启的Nginx服务，而在容器内部我们访问80，也可以访问到相同的Nginx服务

  - `-P`随机指定端口

    ![image-20211115215338581](https://s2.loli.net/2021/12/06/yMu4vHp5Sm3FVNW.png)

    > 由于`-it`是交互方式运行，因此必须指定相互方式，这里指定的是bash方式

  - `-e [参数名]=[参数数值]`配置一些环境信息，比如说MySQL启动时我们可能要设定用户名密码，ES启动时可能需要限制它能够占用内存大小，而它详细的参数还是需要在Dockerhub中看镜像的相关说明

    ![image-20211117210604713](https://s2.loli.net/2021/12/06/yOn3dSVaQvXMfZi.png)

  内部的环境和外部看上去是没有区别的，甚至你在里面`ls`也能看到根目录下的内容，但是毕竟是镜像，很多东西还是不完善的

- `exit`退出容器（由于现在可以当作运行在Ubuntu环境下，因此命令前面不需要加`docker`），同时一旦退出容器就停止运行，但并不是销毁容器

- `ps`当前在运行的容器，`-a`可以查看曾经运行过的容器

  ![image-20211115220435121](https://s2.loli.net/2021/12/06/xCRh9NWDmzLwtIS.png)

- `Ctrl + p + q`在容器内不停止容器退出，容器依旧在运行

- `rm [容器id]`删除曾经运行过的仍存在的容器，但是不能删除正在运行的容器，`-f`强制删除不管你在不再运行

- `start [容器id]`和Linux一样，开启一个被停止的容器，与此类似的还有`restart`、`stop`、`kill`等，像操作一个进程一样操作容器

- `logs [容器id]`查看目标容器运行时的日志记录

  ![image-20211115223150512](https://s2.loli.net/2021/12/06/7fbT6pEuvRJaixB.png)

- `top [容器id]`查看容器内部的进程信息（容器近似看作一个虚拟机，看的就是虚拟机内部的进程）

- `inspect [容器id]`查看容器的所有信息，会蹦出来一大堆JSON信息，先不着急看懂

- `exec`进入一个正在运行的容器，同样`-it`可以用交互方式运行

- `attach`也是进入一个容器，但是它一般不加参数，进入后如果容器内有某个终端正在执行就直接进入那个终端，而`exec`会重新开启一个终端

- `cp [容器id]:[容器内路径] [当前宿主机目标路径]`不管容器是否开启，都可以在容器外拷贝容器内的文件到容器外（宿主机上），当然交换一下参数内容也可以反向拷贝

## 联合文件系统（UnionFS）

比如当我们下载一个Mysql镜像时，会发现下载内容是呈现层级关系的

![image-20211117162053016](https://s2.loli.net/2021/12/06/ytEZ2aMQfqBnhTm.png)

看上去好像是一层一层逐级下载的，其实这就是Docker巧妙地利用了UnionFS联合文件系统办到的

联合文件系统事实上就是将一个镜像再次分成多个镜像小部件（比如nginx镜像可能就需要centos镜像的支持），如果两个镜像存在多个相同的小部件，只需要下载一次相同的部分，而对不同的部分再区分下载即可

上面的每一个哈希码就代表着目标镜像的子镜像，在下载之前Docker会自动检测当前本地是否存在相同的名称镜像，如果有就不需要额外下载，这样可以进一步的降低Docker的占用和提升运行性能

而且这种联合文件系统还可以使得比如我们需要在这个下载过来的nginx进行修改时，可以重新在这个nginx上面再加一层（容器层），而不是直接对原本的文件进行修改，当我们完成我们的配置之后把我们创建的层和原本的层一起打包成镜像，再传给别人的话，别人就可以拥有我们修改过的已经配置好所需项目环境的nginx内容了

![20160819173838](https://s2.loli.net/2021/12/06/sUQZ6E18rpae57I.png)

## 创建个性化镜像

了解了联合文件系统，接下来自然的我们就可以自己创建一个镜像

`docker commit -m=[提交信息] -a=[作者] [容器id] [目标镜像名]:[版本号] `提交容器成为一个自定义的镜像，和Github很像

之后通过`images`就可以看到提交上去的镜像信息

![image-20211117192308567](https://s2.loli.net/2021/12/06/nmWG3T8ONoPMsdA.png)

## 目录挂载

之前的操作还有一个问题，我们好像并不放心能够在这么一个开启后的容器中持久化存储数据，由于容器本身就是不完整的镜像启动的，难免我们不会手贱删除了某个容器，或是环境配着配着就崩了，导致环境中的数据根本不方便取出，Docker甚至不提供回收站的功能，容器没了就是没了，数据也直接丢失，等于删库跑路，为了避免这种情况的发生，我们需要一种方式在容器中调用本地的数据进行操作，容器只用装配环境，既解耦了数据和环境，又为我们的开发提供了更加安全的方式

这时候就需要用到容器数据卷这个概念，它可以把Docker容器中产生的数据同步到本地

卷技术的目标就是将容器中的目录**挂载**到LInux上面，是一种同步机制，不止是容器和宿主机的交互，甚至能做到隔离的容器间的数据同步，这也给我们的不同环境配置时环境的隔离和数据的统一提供了方案

想要采用容器数据卷技术，就需要在`run`时带上`-v [宿主机目录]:[容器内目录]`可选项，则可以将宿主机的某个目录能够同步容器内某个目录

![image-20211117200440548](https://s2.loli.net/2021/12/06/v1AhD5f2nH9drpB.png)

同时挂载并不是单向连接，除了图中的在容器内部修改会影响到宿主机，同样的宿主机test目录下修改内容也会让容器内相应目录变化，同时这样也意味着我们也可以在本地快捷的修改容器内的目录，实现了不用进容器就能够快速修改例如配置文件

但是注意如果我们删除了容器内的文件，外部文件也会消失，但是如果我们删除容器，外部目录的文件并不会消失

![image-20211117204904612](https://s2.loli.net/2021/12/06/LnAsC3fvBzH1JT6.png)

> 我们可能注意到，当我们已经启动了一个容器之后，好像就不能挂载目录了，事实上也是这样的，如果我们真的要一个已经创建过的容器里面的数据，可以采用`docker cp`指令拷出容器内的文件再删除容器

除了上面这样的挂载方式，我们可以不指定宿主机的目录路径，或者是用一个名称代替目录路径（即最前面不加`/`），这样就叫做匿名/具名挂载，挂载出来的内容会默认挂载到本地docker的目录下

通过匿名/具名挂载出来的内容可以通过`docker volume ls `看到

![image-20211117213342965](https://s2.loli.net/2021/12/06/FauCUbQYMD4v5ck.png)

同时我们也可以通过`docker volume inspect [挂载名称]`来查看详细信息，通过`rm`来删除某个不被容器使用着的挂载卷，其他更多操作指令详见`–help`

更进一步的我们还可以在挂载目录后加`:ro`，这样的话容器内部挂载出来的目录就只能够在宿主机内修改，我们进入容器就修改不了内容了

![image-20211117214737924](https://s2.loli.net/2021/12/06/byx9TiEUCvnmIOw.png)

利用这种机制，虽然各个容器间是隔离的，但是我们可以通过将两个容器挂载到宿主机下的同一目录来实现容器间的数据互通

## Docker配置文件

Docker配置文件（DockerFile）是用来构建docker镜像的文件，也就是说我们可以预先配置一个统一的Docker配置文件，然后不需要通过之前说过的`run+修改+commit`的操作来生成一个自己的镜像，现在我们只需要通过一个`build`命令构建一个新的镜像时引用一个Docker配置文件，Docker就可以自动读取文件内容并且直接对某一个目标镜像进行修改，并且创建一个新的自定义镜像，这个镜像就包含我们在Docker配置文件中写入的自定义内容

事实上，几乎我们能够找到的所有官方镜像都是通过这种方式来构建出来的（一般官方引用的模板镜像叫做`scratch`），只不过相较于我们改动较少的内容，他们需要在Docker配置文件中配置更多的内容

接下来我们详细了解一下Docker配置文件有怎样的常用指令

- `FROM [引用镜像]`我们自定义出来的镜像引用什么镜像为模板，即如果Docker配置文件里面只有这一句话，我们所创建出来的镜像将会和引用镜像一模一样

- `MAINTAINER [作者信息]` 没什么好讲的，标注一下这个镜像是我制作的

- `RUN`也就是当我们通常`run`起来的时候在bash里面将会输入命令，但是他会创建一个新的镜像层（联合文件系统），因此常用作安装某些软件包

- `CMD`和`RUN`类似，但是不会创建新的镜像层，同时它的命令会被用户创建容器`run`时如果输入的命令所覆盖

- `ENTRYPOINT`和上面两个都很类似，比起`CMD`不会创建新镜像层之外，也不会被用户`run`的时候输入的指令覆盖，而是会追加在用户命令之后，即它所修饰的指令一定会被执行

- `ADD/COPY`两个指令功能类似，用于添加镜像需要的一些内容，例如一个环境的集成压缩包

  > 但是`ADD`除了能够完成所有`COPY`的工作，还可以解压压缩文件并拷入镜像和通过URL拷贝文件到镜像（但是官方不建议），功能更加强大

- `WORKDIR`设置运行时的工作目录，即我们第一次进入容器后bash所指向的目录

- `VOLUME`自动设置一个容器卷，自动将镜像下的某个目录挂载到宿主机（匿名挂载）

- `EXPOSE`对外提供的端口，免去了创建容器时的手动暴露端口

- `ENV`设置环境变量，比如一个ES环境需要一大堆的内存空间，然而我们的空间远远不够，可以设置环境变量来控制ES运行时最大可占用内存的大小

常用指令就是这样，非常好理解，等于说是我们写了一个脚本，自动将某一个镜像创建成容器后执行一大堆我们的命令之后再`commit`回一个镜像还给我们

比如我们现在有一个这样的DockerFile

![image-20211122235856270](https://s2.loli.net/2021/12/06/9Dt82TNwpOobnBF.png)

> 这里写错了，ubuntu不能用yum下载文件，同时由于新创建的ubuntu镜像不包含最新源的`apt-get`，所以还需要`apt-get update`一下
>
> 最终代码为
>
> ```bash
> MAINTAINER chillyblaze
> 
> ENV MYPATH /home  # 注意这里环境变量一定不要手贱设个叫PATH的，直接覆盖了原有的环境变量，后果很严重!
> WORKDIR $MYPATH
> 
> RUN apt-get update
> RUN apt-get install vim
> 
> EXPOSE 1111
> 
> CMD echo $MYPATH
> CMD /bin/bash
> ```
>
> > 这个环境变量就可以看作是windows里面设置的path，之后我们可以通过这个环境变量快速访问到相关内容
> >
> > 事实上我们在linux内输入的所有指令都是以环境变量存在着的

我们要将其构建出来

![20211124232558.png](https://s2.loli.net/2021/12/06/ahgpIKeqyb89O2B.png)

如果不出问题的话最后会提示我们构建成功的字样，此时我们可以检查一下镜像

![20211124233300.png](https://s2.loli.net/2021/12/06/aRxVSCwNIyczH5W.png)

如果还不放心可以构建容器`run`看看是否和我们预想当中一致

![image-20211124234018255](https://s2.loli.net/2021/12/06/tMLve7B6WxTgrRO.png)

> 还可以通过`vim -version`查看当前vim版本（忘截了）

如果还是好奇，则可以通过`docker history [容器id]`来查看构建这个容器之中的所有历史内容

![image-20211128202430053](https://s2.loli.net/2021/12/06/8UeRPradQu6SOcl.png)

可以看出来就是我们在文件中编写的每一条内容，他都完整的执行了

## 发布自己的镜像到DockerHub

和GitHub非常像，首先我们也要在Dockerhub上面创建一个账号

![image-20211128210706788](https://s2.loli.net/2021/12/06/1k7bQo4hADglCX8.png)

接着我们在本地登录上我们的这个账号

![image-20211128214051838](https://s2.loli.net/2021/12/06/mwhg3AFCbZaR4Mc.png)

接着就可以通过`push`命令提交镜像

当然为了使我们提交的镜像到指定的仓库，我们必须通过tag命令修改原本的镜像名

> 其实会发现所谓的镜像名其实就是镜像存放的仓库名，所谓的镜像名其实不存在，有名字存在的只是我们的容器名

![image-20211128212514837](https://s2.loli.net/2021/12/06/sqPY8NdE4GOCjtX.png)

![image-20211128212710510](https://s2.loli.net/2021/12/06/j7ZqHPAKXJaER9C.png)

> 反转了，其实不是重名问题，由于我们登录的是chillyblaze这个账号，因此必须指定前缀仓库为我们的用户名才可以（类比于GitHub我们建的仓库名路径），上面解释错了

接着打开DockerHub进入我们的仓库中就可以发现我们推送上去的内容了

![image-20211128213755149](https://s2.loli.net/2021/12/06/gI3mlG6xzydfwEN.png)

## Docker网络

Docker为我们提供了专属于自己的内部Docker网络，相关的容器可以通过内部的网络进行连接

我们可以通过`ip addr`来查看当前的网卡信息

![image-20211130181237933](https://s2.loli.net/2021/12/06/okZnJAEQiqNXGms.png)

为了验证我们的猜想，比如我们先开启一个Tomcat

```bash
docker run -d -P --name tomcatTest tomcat
```

接着我们可以通过交互模式执行`ipconfig`或者是`ip addr`指令来查看容器在Docker网络内的IP地址

![image-20211130220818893](https://s2.loli.net/2021/12/06/PWURhAHVYkXendg.png)

> 如果报错了的话就进到tomcat里面下一个`iproute2`，注意容器内可能是`Debian`系统，得用`apt`来下载内容

这就像是我们在电脑上启动了一个虚拟机，理所当然的我们在本机可以通过虚拟机上的ip地址来访问到虚拟机

![image-20211130183612006](https://s2.loli.net/2021/12/06/lC8RyXEULjGPHK9.png)

如上图ping通也一点问题没有，事实上不仅如此，容器相互之间也可以通过这个ip地址互相ping通，此时我们本机就相当于家中的一个路由器，每一个容器就是家里的各种设备，各个设备之间可以ping通也一点都不奇怪

### veth pair

在上边的测试中我们发现，每开启一个Docker容器，本机上就会多了一对网卡，分别位于容器内和本机上，正由于这两个网卡之间的相互连接，使得我们可以无障碍ping通容器，这个技术就是所谓的veth pair技术

veth pair提供了一对虚拟网卡，像是一对对讲机一样，连接相互隔离的两个网络协议栈（也就是我们此处的Docker容器和本机）

![image-20211130224235081](https://s2.loli.net/2021/12/06/KB7hpWV1PU4IJDg.png)

通过这幅图的辅助，我们就能理解，当每创建一个Docker容器，Docker就会生成一对虚拟网卡（也叫虚拟网络接口），分别放置到容器内和本机上，同时在容器内给这个网卡分配一个IP地址（127.0.0.2），而在本机将这个虚拟网卡连接到`docker0`网络地址（127.0.0.1），这样我们就可以通过这一对网卡实现点对点的连接

如果有多个容器存在，虽然容器之间相互隔离，但是此时本机（也就是`docker0`网卡）就相当于一个路由器（也就是Docker网络的网关），容器内的请求首先被转发到`docker0`上，再由`docker0`寻找转发的IP地址将请求转发到另一个容器内，也正是这样实现了容器相互之间的通信

而`docker0`除了作为网关以外还兼具网桥的功能，这个在本机上建立的小小的Docker网络与我们外界通信的入口就是`docker0`，从这个意义上来说，当我们在本机中ping一个容器时，其实也是先经过了`docker0`的转发，才得以传输到目标容器中

> *网桥也叫桥接器，是连接两个局域网的一种存储/转发设备，它能将一个大的LAN分割为多个网段，或将两个以上的LAN互联为一个逻辑LAN，使LAN上的所有用户都可访问服务器。*
>
> 通俗来说，就是整合两个局域网的一个中间件，在此处，Docker网络和我们本机物理网卡上的网络就可以看作两个局域网

### 自定义docker网络

在了解了`docker0`的运作规律之后，我们就可以尝试自己构建一个docker网络，事实上，在实际开发中，我们更多的使用我们自定义的网络进行容器间通信，相较于通过默认的`docker0`进行通信具有一定的优越性

首先我们可以通过`docker network ls`来列出Docker默认的可选网络

![image-20211201153135620](https://s2.loli.net/2021/12/06/sbdmQF5Rxevw7St.png)

其中的`DRIVER`就是建立的网络模式，每一个条目可以看作一个局域网，当我们启动一个容器时，我们可以通过`–net [NAME]`来指定当前创建容器将其置于哪个网络下，如果不指定，默认就走`bridge`这个网络，也就是`docker0`

了解了这些之后，我们就可以通过`network create`来创建一个自己的网络

![image-20211201153936033](https://s2.loli.net/2021/12/06/qPsHJiQBegc9Utj.png)

创建完成后，我们可以再次创建一个tomcat容器，指定其网络组名称，并查看其网卡情况

![image-20211201155116387](https://s2.loli.net/2021/12/06/WefiZjxvqRY6mNn.png)

![image-20211201155121116](https://s2.loli.net/2021/12/06/dJPyNMvamtHr8kw.png)

这样我们的容器就成功的被放入了我们自定义的网络中，这个网络和docker网络别无二致，此外如果我们为创建的容器指定了名字，这个网络下的容器还可以通过名字当作一个域名一样直接解析成相应IP进行访问

同时拥有了自己的docker网络，就可以在不同的网络中创建不同的集群，降低了相互集群之间的耦合性，便于维护

### 网络间连通

此时我们可能会想，假设我们创建了多个网络，相互网络之间如何进行通信呢？

事实上，Docker也提供了一种容器连通不同网络的办法，只需要通过`connect`连接即可

![image-20211201160628857](https://s2.loli.net/2021/12/06/n27DGQV5A93TpvE.png)

如此可以发现实现的方式十分简单，只需要在现有的容器上再加一个veth接口，并让目标网络给他再分配一个IP地址即可，使得容器在不同的网络中有着不同的IP，由于网段的不同，也不存在出现矛盾的情况，真正实现了容器打通各个网络

## 容器外连接

我们可能会发现，其实容器内什么指令几乎都没有，要运行控制台调试显得特别麻烦，甚至还需要额外下载内容，原本精简的容器莫名其妙就变得臃肿了，显然十分不方便，那么我们可不可以从容器外的指令控制容器内的显示呢

别说还真可以，我们首先要了解到命名空间的概念

***Linux 命名空间对全局操作系统资源进行了抽象，对于命名空间内的进程来说，他们拥有独立的资源实例，在命名空间内部的进程可以实现资源可见。对于命名空间外部的进程，则不可见，实现了资源的隔离。这种技术广泛的应用于容器技术里。***

资源隔离的技术十分常见，同时还可以细分为UTS，IPC，PID，Network，Mount，User等，而Docker所采用的即是基于网络栈的资源隔离（Network）

Docker内的进程隔离也是同理，当启动一个容器时，在主机上看其实只是起了一个进程，因此在容器内部，也就只能看到自己内部的进程了

我们可以通过`docker inspect --format "{{ .State.Pid }}" [name]`来查看容器在宿主机上的进程号，其中两个花括号代笔监视之后显示的json中的某个键，其中键名以`.`开头，后面注意第一个字母大写即可

找到了容器启动时的进程号，我们就可以通过`nsenter`指令来执行容器内的某指令，比如这样`sudo nsenter -n -t 4314 ip addr `就可以查案容器内的端口号，但实际上容器内并没有`ip addr`这个指令

但注意这样的执行方式只能适用于网络命令，如果使用比如`ps -ef`之类的读取目录指令实际上显示的内容还是宿主机中的内容

借助这个命令我们可以对容器内比如mysql进行抓包操作

```shell
sudo nsenter -n -t 4341 ip addr
tcpdump -i lo port 3306 -w mysql.pcap
```

即可

# Nginx

## 背景

Nginx （engine x）是一个开源、高性能的 HTTP 和反向代理 Web 服务器，同时也提供了 IMAP/POP3/SMTP 服务

> 正向代理：我们知道我们要请求的服务器内容，接着我们带着我们知道的请求服务器信息先给代理服务器，代理服务器根据我们传给他的内容代理我们发送请求
>
> 反向代理：我们不知道服务器的详细信息，但是我们知道某个代理服务器的地址，我们直接将请求发送给代理服务器，由代理服务器读取请求并选择他管理下的合适服务器执行我们的要求，从而达到负载均衡的目的

1. 速度更快，并发更高(epoll函数解决高并发)

2. 配置简单，扩展性强

3. 高可靠性

4. 热部署

5. 成本低，BSD许可证（我们可以免费商用并盈利，更可以直接对其源码进行修改并成为自己的项目）

   > 各种开源许可证一览：
   >
   > ![See the source image](https://tse1-mm.cn.bing.net/th/id/R-C.c06456a0fe2f8e911401cd66d0096a2c?rik=8De0vQ8YPiObSw&riu=http%3a%2f%2fwww.vip1993.com%2fuploads%2fallimg%2f200628%2f1-20062Q34453R1.jpg&ehk=LRjjO31gtVjjUCEEK8%2bhrAPzdumv8%2f4YJRsUmommrKs%3d&risl=&pid=ImgRaw&r=0)

   由于这个特性，衍生出了许多拓展nginx版本，比如OpenRestry（Nginx+Lua）等

下面的演示内容均在Docker中的Centos系统进行演示执行，其它系统类似

## 安装/卸载

### 通过源码安装

1. 环境准备

   - 由于Nginx是由C语言编写的，因此我们需要先安装一个GCC编译器
   - Nginx编译过程中需要用到PCRE（正则表达式）库，也得安装这个库
   - 除此之外还需要压缩算法库zlib和安全通信包OpenSSL
   - `yum install -y gcc pcre pcre-devel zlib zlib-devel openssl openssl-devel`安装
   - 安装检查可以通过`rpm -qa [包名]`来查看

2. 下载源码，我们可以通过`https://nginx.org/en/download.html`复制源码链接，接着在终端中`wget https://nginx.org/download/nginx-1.20.2.tar.gz`即可

   ![image-20220130132357064](https://s2.loli.net/2022/01/30/xoNyLhSQl9fWJqt.png)

3. 解压内容，执行内部的configure文件

   	![image-20220130133319457](https://s2.loli.net/2022/01/30/HUGiJKIedxWCaB6.png)

4. 编译内容`make && make install`即可

5. 完成之后我们进入`/usr/local/nginx/sbin`里面执行一下`./nginx`即可直接启动nginx

6. 接着通过`ip addr`查看一下docker内部的ip地址，在外部直接访问ip即可

   ![image-20220130134453566](https://s2.loli.net/2022/01/30/etA43hOgTlfPC7H.png)

### yum安装

上述的方法显然十分不方便，所以我们可以直接通过yum一步到位

1. 先查看`https://nginx.org/en/linux_packages.html`内部提供的用于安装的方式（通过Document一项进入），跟着步骤一步步来即可

   ![image-20220130135311713](https://s2.loli.net/2022/01/30/NJdX7TliMbjrSIG.png)

   > 上面的步骤事实上就是引入了一个yum库，不然直接`yum install nginx`可能会找不到内容

2. 通过`whereis nginx`找到安装到哪里去了

3. 选择一个在`sbin`目录下的文件，执行即可（或者直接nginx也可以执行）

![image-20220130140343549](https://s2.loli.net/2022/01/30/tLHI1siC9M4Rqjv.png)

> 发现和之前的界面不太一样了哦

我们可以比对一下两种方式安装之后的版本信息（`nginx -V`）可以发现两种安装方式的区别是很大的

- 源码安装

  ![image-20220130141610198](https://s2.loli.net/2022/01/30/HDdeBTs3noUqv6Y.png)

- yum安装

  ![image-20220130141705013](https://s2.loli.net/2022/01/30/drlsaL7TFEUZPt6.png)

可以明显发现，肯定是我们源码安装的过程中比起直接安装还是漏了许多东西的

### 编译参数

首先我们先了解一下源码安装的时候各个目录之间的关系

![image-20220130162509183](https://s2.loli.net/2022/01/30/nxRgqKGLWHjZlNE.png)

我们发现在通过源码进行安装的时候，我们似乎只运行了一下`configure`这个文件，这就说明，如果我们需要像如同yum安装那样多那么多参数，那么势必需要在执行`configure`的时候告诉电脑我的想法才行

我们可以通过`--help`来查看如何添加参数

![image-20220130181039452](https://s2.loli.net/2022/01/30/YIf6A2bkhtRBpOE.png)

在yum安装中冒出来的每一个参数/属性，我们都可以跟上面的对应起来，也就是说，我们进行编译时，只需要添加上这些参数，就可以手动模拟通过yum安装的效果了

当然要自己加参数，首先我们还是要了解一些这些参数的作用

- `--with`开头的往往是为Nginx添加某个模块，相反`--without`就是编译时排除某些模块
- `--prefix=PATH`Nginx安装路径。如果没有指定，默认为 `/usr/local/nginx`
- `--sbin-path=PATH`Nginx可执行文件安装路径。只能安装时指定，如果没有指定，默认为`<prefix>/sbin/nginx`（这的prefix就是指上边指定的）
- `--conf-path=PATH `，配置文件，默认为`<prefix>/conf/nginx.conf`
- `--error-log-path=<path>`在nginx.conf中没有指定error_log指令的情况下，默认的错误日志的路径，默认为 `<prefix>/logs/error.log`
- `--http-log-path=<path>`在nginx.conf中没有指定access_log指令的情况下，默认的访问日志的路径，默认为 `<prefix>/logs/access.log`
- 其他都于此类似，`--help`指令之后也有详细说明

综上，我们可以发现比起无脑yum安装，还是手动指定参数更加让人放心，当然这也意味着学习成本的扩大

### 卸载

想要自己通过参数方式编译，我们就需要对上一次安装的程序进行卸载

1. 停止nginx服务（`./nginx -s stop`）
2. 删除nginx主文件夹（`rm -rf nginx/`）
3. 清理编译内容（`make clean`）

![image-20220130184057422](https://s2.loli.net/2022/01/30/BEC1X4V3kcvxMNT.png)

## 目录结构

![image-20220130185810929](https://s2.loli.net/2022/01/30/tDpOAfi1FT6G4Sr.png)

## 服务器起停

### 信号控制

Nginx默认是采用多进程的方式来工作的，当Nginx启动之后，后台进程中会包含一个master进程和若干个worker进程

其中master进程用于管理worker进程，包含接收外界的信息，并将接收到的信号发送给各个worker进程，监控worker进程的状态，当worker进程出现异常退出时，会自动重新启动新的worker进程

而worker进程专门处理用户请求，各个worker进程平等且独立

我们可以通过`ps -ef | grep nginx`查看nginx启动的进程相关情况

![image-20220205184757887](https://s2.loli.net/2022/02/05/CKnlTMkovQDYsFI.png)

其中master进程和worker进程的关系如下

![img](https://www.baiyp.ren/images/nginx/nginx13.png)

因此，我们想要停止Nginx进程，只需要告诉master进程即可

1. 获取master进程pid

   - `ps -ef | grep nginx`查看
   - `cat /usr/local/nginx/logs/nginx.pid`查看

2. 关闭进程`kill -signal PID`，给出指令的同时我我们也要指定信号signal

   - `TERM/INT`立即关闭整个服务

   - `QUIT`所有请求结束之后关闭整个服务

   - `HUP`重读配置文件并使用服务对新配置项生效

   - `USR1`重新打开日志文件，用于日志切割

   - `USR2`平滑升级到最新版Nginx

     > 升级之后会在目录下生成`nginx.pid.oldbin`文件，当确认新Nginx正确启动之后，我们还需要`kill -QUIT pid.old`，关闭旧的服务

   - `WINCH`所有子进程不再接收处理新连接，相当于给worker进程发送`QUIT`

   ![image-20220205214535041](https://s2.loli.net/2022/02/05/PJnEXZ61SaGut4f.png)

### 二进制文件控制

除了上述通过手动删除进程停止Nginx服务，我们还可以通过启动文件来停止

转到`/usr/local/nginx/sbin`下，通过`./nginx -h`查看帮助内容

- `-t`检查当前配置文件语法信息（`/usr/local/nginx/conf/nginx.conf`）是否符合规范
- `-s`信号控制
  - `stop`相当于`TERM/INT`
  - `quit`相当于`QUIT`
  - `reopen`相当于`USR1`
  - `reload`相当于`HUP`
- `-c`指定配置文件的位置

### 版本迭代

当新的Nginx版本发布之后，我们如果想平滑升级服务器，或者是我们如果想要在原有的服务中添加其他模块，由于Nginx的可热部署性，我们可以在改动少量文件的基础上进行快速的平滑升级

1. 同样`wget`下载最新的压缩包，以同样的参数运行`./configure`和`make`，注意不需要进行`make install`

2. 备份`/usr/local/nginx/sbin`下的二进制文件

3. 将安装目录下的`objs`内的`nginx`二进制文件拷贝到`/usr/local/nginx/sbin`，并在原目录下直接运行`make upgrade`即可

   > 如果不想用`make upgrade`，那么就需要通过`USR2`重启服务，并通过`QUIT`平滑删除原进程

### 配置系统服务

通过源码安装程序时，我们都需要在目录下通过手动执行二进制文件来开启Nginx，事实上我们可以通过将其配置为系统服务从而在任意地方一键开启服务

1. 在`/usr/lib/systemd/system/nginx.service`目录下添加`nginx.service`并添加内容

   ```
   [Unit]
   Description=nginx web service
   Documentation=http://nginx.org/en/docs/
   After=network.target
   
   [Service]
   Type=forking
   PIDfile=/usr/local/nginx/logs/nginx.pid
   ExecStartPre=/usr/local/nginx/sbin/nginx -t -c /usr/local/nginx/conf/nginx.conf
   ExecStart=/usr/local/nginx/sbin/nginx
   ExecReload=/usr/local/nginx/sbin/nginx -s reload
   ExecStop=/usr/local/nginx/sbin/nginx -s stop
   PrivateTmp=true
   
   [Install]
   WantedBy=default.target
   ```

2. 修改权限为`755`

3. 测试是否成功（`systemctl start nginx`）

   > 注意到docker内无法使用systemctl这个指令

## 配置文件概述

![image-20220205223344953](https://s2.loli.net/2022/02/05/cK18MZu3lLJ64TW.png)

### 全局块

#### user指令

通过`user user [usergroup]`来指定**worker进程**的用户和用户组，如果不指定`usergroup`则默认使用user名作为组名称，如果不设置用户名则默认使用`nobody`

注意添加的用户应该是本机中存在的用户，如果乱输入用户名会使得`./nginx -t`检查失败

将`user`修改为root后：

![image-20220205224141497](https://s2.loli.net/2022/02/05/kjbLTlnfMv4OhuD.png)

更改`user`信息之后，指定的worker进程就无法访问不属于他权限之内的内容，从而可以避免服务器被入侵

#### work process指令

其中包含两条指令：

1. `master_process [on/off]`控制是否开启worker进程，默认`on`，如果设成`off`再启动会发现进程中的worker进程不见了
2. `worker_processes [num]`用于控制Nginx服务器实现并发处理的量，默认为1，建议和服务器CPU内核数保持一致

注意以上两个命令的修改之后我们都不能直接使用`reload`来重启Nginx服务，必须`stop`之后重新启动才能生效

#### 其他指令

- `deamon [on/off]`使用守护进程启动，默认为`on`，改成`off`之后我们启动Nginx之后当前启动控制台就不能关闭，一关闭Nginx也跟着关掉了
- `pid [path]`配置pid的存储路径
- `error_log [path] [level]`错误日志存放路径，其中的`[level]`项可以设置日志级别，从低到高分别是`debug|info|notice|warn|error|crit|alert|emerg`，设置太低的话会影响磁盘性能，它也不止只能配置在全局块中，默认为`crit`
- `include [path]`用于引入其他配置文件

### events块

这个块是用来设定Nginx服务器与用户之间的网络连接

- `accept_mutex [on/off]`主要用来设置Nginx网络连接序列化，默认为`on`，当Nginx没有收到用户请求时，默认所有的worker进程都是休眠状态，当某一个用户请求到来时，如果把这个值设为`off`，那么所有的worker进程就会被同时唤醒竞争这个请求的所有权，造成惊群效应，而如果设置为`on`那么每次都会只激活一个worker进程处理请求，增强了Nginx的整体性能，然而如果用户请求过于频繁（网站一下子接收大量请求），一个个激活worker进程反而会影响连接速度，因此需根据自身服务器或网站情况进行设置
- `multi_accept [on/off]`改成`on`之后一个worker进程就只能接收一个用户请求了（默认`off`，建议不修改）
- `aorker_connections [num]`用来配置单个worker进程的最大用户连接数
- `use [method]`用于指定Nginx服务器选择哪种事件驱动来处理网络消息，其中`method`有`select/poll/epoll/kqueue`等，建议设为`epoll`采用io多路复用的方式，后面也会涉及

### Http块

#### 定义MIME-Type

这个MIME-Type定义了用户请求的网络资源的媒体类型，作为web服务器必须识别前端请求的资源类型，来做出相应的MIME-Type响应

> 浏览器通常使用MIME类型（而不是文件扩展名）来确定如何处理URL，因此Web服务器在响应头中添加正确的MIME类型非常重要。如果配置不正确，浏览器可能会曲解文件内容，网站将无法正常工作，并且下载的文件也会被错误处理。

Nginx配置文件中默认有这两行配置

```
include mime-types;
default_type application/octet_stream
```

它代表着我们通过Nginx直接返回的内容如果没有指定返回类型那么默认采用文件的方式传输内容，即访问某个内容时返回在用户本机下载目标文件内容（注意`.html`结尾的文件会自动返回`text/html`），但比如`.html.swp`就变成一个文件自动被我们下载而不是浏览器进行解析展示

#### 自定义服务日志

之前我们已经了解到，Nginx中的`access.log`用来记录用户所有的访问请求，而`error.log`则记录Nginx本身运行时的错误信息，事实上我们也可以通过自定义的方式来设置日志的记录方式

我们想要自定义日志，第一步就是要设置我们的日志记录格式，我们通过`log_format [format] [rule]`来设置格式，在默认的Nginx配置文件中也已经给出了样例，其中在`rule`中可以通过指定Nginx内部提供的变量名（之后会提及）来指定用户访问时需要展示的请求信息

我们通过`access_log [path] [format]`指定日志存储位置和日志格式名，这样在该自定义文件下我们就可以查看到用户的访问信息了



#### 其他指令

- `sendfile [on/off]`设置Nginx服务是否使用`sendfile()`传输文件，该属性打开后可以大大提高Nginx处理静态资源的性能

- `keepalive_timeout [time]`用来设定长连接的超时时间，当用户短时间请求结束之后时不会立即关闭该用户的上一次连接内容，使得当用户短时间多次请求时不会频繁创建连接，但是时间设置太长如果请求过多，大量连接没有断开，导致服务器性能下降，默认为`75s`

- `keepalive_requests [num]`设定一个长连接的使用次数，在满足上面一条的情况下，长连接在使用设定的次数之后也会强制断开

- `error_page [status code] [uri]`遇到错误代码指定访问某个页面

  > 此外还可以通过比如`error_page 404 @flag;`来跳转到某个具有`@`标识的location上`location @flag{}`

- `tcp_nopush [on/off]`在服务器开辟一个缓存区存放将要交友用户的数据，等到数据装满缓存区之后再进行发送，与之对应的`tcp_nodelay [on/off]`则指定服务器一接收到数据就将其发送出去，不等待，这两个指令同时开启的话优先使用`nopush`，当最后数据结束后不足以填满缓存，Nginx会自动再调用`nodelay`强制发送剩余数据

#### 子块元素

一个http块内还需要有别的块级元素，它中间可以放多个server块，一个server块又可以放多个location块，其中可以通过`return`来返回页面的响应内容（用于简单页面的返回内容）

用户在访问服务器资源时，默认就是通过`server_name:port/location`访问

![image-20220217123800122](https://s2.loli.net/2022/02/17/dQsRHb7NGUEgLAn.png)

同时大多数在http块中的指令也可以被指定在server和location块，同时指定时采用就近原则

在之后还会大量涉及到这两个块中的内容，此处仅简单介绍

#### listen和server_name

我们可能会疑问，明明一个服务器只有一个ip地址，为什么可以有多个server存在，因为我们可以发现，不同的server都会有`listen`和`server_name`两个字段存在，而我们只知道`listen`会决定浏览器访问时的端口信息，但是`server_name`又是干什么的呢

其实，用户在访问服务器时，一般来说我们会在地址栏输入该服务器绑定的域名，同时一个服务器ip可以绑定多个域名，而当web服务器接受到请求的时候，同时还会接收到服务器是通过哪一个域名访问的自己，而这个域名，就成为了与`server_name`匹配的条件，我们可以通过为同一个ip绑定多个域名，并在服务器内部对不同的访问请求进行筛选，来伪装拥有多个服务器的表象

同时，`server_name`除了上述所说的ip和完整域名匹配，还支持通配符（`*`）和正则表达式（以`~`开始一个正则表达式）域名匹配，同时注意可以通过在正则表达式中加`()`来框定某个变量在之后通过`return $1`来返回值（精确匹配>前通配符>后通配符>正则表达式）

注意，如果任一一个server都无法匹配接收到的请求，同时请求又确确实实发送到了服务器某个正在监听的端口上，那么默认会走第一条server处理请求（或者走存在`default_server`的server）

#### location块

除了server块中可以存在location块，location自身还可以进行嵌套使用

一般来说我们看到的如上面一样都是`location /xxx{}`直接进行匹配的，但是实际上这样匹配是不安全的，因为所有前缀为`xxx`的请求都会走这一条location，如果想要严格匹配，就需要用`=/`来进行匹配，此外还可以通过`~`和`~*`来指定使用正则表达式（不区分大小写）

在location之内可以包含root和alias指令，两者看上去差不多，但是也会有细微的差别

```
location /images{
	root /usr/local/nginx/html  # 会在root+location的位置去寻找资源
	alias /usr/local/nginx/html # 会替换location位置，直接使用alias里面的路径
}
# 第一个只能访问到html/images里面的内容，第二个只能访问到html里面的内容
```

location还可以配置index指令，是用来设置网站的默认首页，如果指定多个首页，就从左往右找到哪个就停，还是十分简单的

## 静态资源

### 压缩

众所周知，传输内容大小决定着传输效率，但是传输内容的多少同样影响着传输效率，此时就需要通过压缩让传输包尽可能的小的同时装载更多的数据

#### ngx_http_gzip_module

Nginx默认会加载模块`ngx_http_gzip_module`，之后我们可以通过在http块中添加`gzip on`来开启传输时的数据压缩

当没有开启时，我们在`html`目录下放入了一个大文件，此时会发现文件的大小和我们用户接收到的包大小是基本一致的

![image-20220219112633181](https://s2.loli.net/2022/02/19/hPCM5zLZ8sDanxf.png)

![image-20220219112757681](https://s2.loli.net/2022/02/19/slI8Wj4JBqxUYg5.png)

此时我们通过检查工具检查接收该文件的MIME并在配置文件中开启传输文件的压缩功能，我们就可以对指定类型的文件进行压缩了

![image-20220219113042059](https://s2.loli.net/2022/02/19/rYS4OtKpvN6sEZl.png)

![image-20220219113004983](https://s2.loli.net/2022/02/19/IvunUc5k8mS3wEM.png)

记得重启服务器

![image-20220219113245367](https://s2.loli.net/2022/02/19/Ln4AkWhazdGVo1v.png)

可以发现比起之前有了明显的压缩了，而其中`gzip_types [MIME]`指定了对何种返回内容的压缩（默认为`text/html`），`gzip on`则代表打开压缩功能，而其中`gzip`默认是不打开的，我们如果想要对所有的返回结果进行压缩，则可以`gzip_types *`来指定，但是不建议这么做，因为某些比如图片和视频默认情况下已经是高度压缩了，服务器进行二度压缩反而会浪费资源降低效率

除了这两个指令之外，还可以使用`gzip_comp_level [num]`来指定压缩等级，其中9压缩程度最高但是耗时也最长，1反之，默认为1，一般设置为6即可

同时还有`gzip_vary [on/off]`指令用于设置使用发送`Vary:Accept-Encoding`头部来告诉用户我们使用了gzip压缩，还有`gzip_disable [regex]`可以通过对正则表达式的设置来设置是否对某些用户的请求头，响应时不进行压缩，一般用来过滤某些低版本或特殊服务端的请求（`MSIE [1-6]\.`来过滤IE6以下版本的请求（可能不支持gzip从而出现乱码）

由于gzip的配置比较复杂，建议配置在单独的文件中，再在初始配置文件中通过`include`包含

#### ngx_http_gzip_static_module

除了上面的内置加载模块，我们还可以为我们的服务器添加其他额外的模块，比如`ngx_http_gzip_static_module`，它只提供了一个指令，即`gzip_static [on/off/always]`，开启之后服务器收到用户请求时，会寻找根目录下存在`[资源名].gz`的文件将其发送给用户，而不是直接现场压缩之后再发给客户端

注意开启这个模块之后需要关闭之前的`gzip on`指令，因为一个是传输时压缩，一个是读取本地压缩文件

而对于在现有的Nginx上额外添加模块，其实并没有什么简便的方法，我们只能对初始Nginx重新编译

1. 查看Nginx当前参数信息

   ```shell
   nginx -V
   ```

   之后复制保存所有的参数内容

2. 对原有的二进制文件进行更名

   ```shell
   cd /usr/local/nginx/sbin
   mv nginx nginxold
   ```

3. 进入Nginx安装目录，重新编译，并进行更新

   ```shell
   cd /root/nginx/core/nginx-xxxxx
   make clean
   ./configure --with-http-gzip-static-module [其他参数内容]
   make
   cp /objs/nginx /usr/local/nginx/sbin
   make upgrade
   ```

### 浏览器缓存

当用户多次访问服务器上同一个资源时，我们显然不希望用户总是频繁的对服务器进行请求，此时就需要了解用户浏览器的本地缓存机制，以便将返回信息内容保存在用户本地，便于缓解服务器的压力

最重要的过程如下图所示：

![img](https://loulanyijian.github.io/images/cache.png)

简单来说，就是当服务器设置了浏览器缓存之后，用户首次访问页面时，服务器会对浏览器返回一个标记，在第二次访问时根据标签的一致来确定两次访问之间服务端是否改动内容，未改动内容则返回304，不请求服务器直接调用本地缓存展示内容则返回200正常，其中也涉及到强缓存和协商缓存，后面内容将会细说

#### 强缓存

在浏览器缓存中，强缓存涉及到两个响应头信息`Expires`和`Cache-Control`，其中前者比较古老，只是在响应头中设置了一个目标时间，只要没到这个目标时间都直接走强缓存，也就是调用本地的页面缓存内容直接显示，返回200

但是这可能涉及到服务端与本地时间不一致的问题，此时如果浏览器版本`HTTP1.1`则直接忽略`Expires`采用`Cache-Control`，后者不设定目标时间，而是设定某个时间段，当浏览器再次请求时，会先读取上一次请求时的200请求，比对当前时间和上一次请求中的`Cache-Control`做差和请求时间比较判断是否过期

注意只要资源没有过期，也就是走强缓存，那么浏览器就不会与服务器进任何的交互，只需要本地调用内容即可，同时虽然调用本地内容，但是页面在监视器中同样返回200

同时还需要注意同一页面刷新并不会走强缓存，必须重新打开一个页面并访问相同地址才能使强缓存生效

对于Nginx配置来说，其中集成了两个内容的同一指令`expires [time]`来直接对`Cache-Control`进行设置，同时也对低于`HTTP 1.0`版本的浏览器仅设置`Expires`

![image-20220222093759895](https://s2.loli.net/2022/02/22/dTSzVU8OWDgrotp.png)

![image-20220222093533133](https://s2.loli.net/2022/02/22/xo1hWEgV3pLtTb7.png)

除了直接设定时间之外，我们还可以直接设定一些选项，比如`no-cache`表示不进行强缓存，`max`直接设定十年缓存等，我们还可以不通过`expires`指令而是直接`add_header [key] [value]`来指定设置响应头信息，因为`Cache-Control`还支持很多不同的值信息

#### 协商缓存

协商缓存不需要指令对他进行控制，但是也是需要了解的一个现象

当资源过期或者强缓存设置为`no-cache`时，浏览器就需要与服务器进行一次通信，但是由于缓存的存在，当服务器上内容未改变时，服务器可以直接通知用户采用缓存内容，这样同样可以节省大量流量资源

具体的操作流程是这样的，首次访问时，服务器会在响应头信息中添加`Etag`和`Last-Modified`两个键值，分别存储了发送信息的一段内容加密验证和在服务器上该内容的最后修改时间，浏览器接收到这两个内容就保存在自己的请求信息`If-Modified-Since`和`If-None-Match`两个键值中，下次与服务端通信时直接与下一次服务器传来的值进行比对，如果一致浏览器就可以直接调用缓存内容进行展示

![image-20220222095843543](https://s2.loli.net/2022/02/22/meHyAZjf1rwJ8Fn.png)

![image-20220222095933728](https://s2.loli.net/2022/02/22/qPzMi7E3X9LB4Fw.png)

### 安全

#### 跨域问题

*前端调用的后端接口不属于同一个域（域名或端口不同），就会产生跨域问题，也就是说你的应用访问了该应用域名或端口之外的域名或端口（来自网络）*

对于我们来说，我们想理解跨域问题，就需要逐步剖析其产生原因

首先我们需要先了解一下同源策略，浏览器的同源策略就是一种约定，是浏览器最核心也是最基本的安全功能，内容即是仅当协议，ip和端口相同时才符合同源策略（同电脑下的不同资源不满足跨域问题）

而当两台服务器不满足同源策略，就会出现跨域问题

比如我现在有两台服务器，或者同一台服务器监听多个端口，此时我通过一个端口获取用户提交的请求，并将其转发到另一个端口上，此时就会触发跨域问题，即目标服务器不允许你这台服务器对其进行转发数据，浏览器的console内会报一个错，提醒我们出现了跨域问题，而原本需要转发的数据也没有办法正常转发

此时我们只需要在接收服务器上添加头信息`add_header Acess-Control-Allow-Origin [转发服务器地址，允许*]`和`add_header Acess-Control-Allow-Methods [请求方式，如GET]`

#### 防盗链

我们可能发现，当我们希望在我们自己的网页中显示别的网站上的图片时，似乎十分靠运气，有些网站的图片直接复制url就可以通过img标签显示在我们的网站中，但是相反也存在很多网站无论我们怎么复制图片地址，都没有办法在页面中显示，那些不能显示的图片实际上就是为图片添加了防盗链

首先我们需要了解到`Referer`头信息，因为我们知道所有的图片也好实际上就是服务器上的静态资源，事实上我们在网页中访问图片时也会携带来源的`Referer`信息，而显然我们通过自己服务器引用时也会携带我们自己服务器的`Referer`信息，而显然我们只需要在服务器中限制引用的服务器地址即可实现防盗链

在Nginx里面，只需要添加以下代码即可

```
location / {
	valid_referers none blocked [allow ip];  # none表示为空时允许访问，blocked表示被防火墙伪装后的东西允许访问（用于判断访问者是否为服务器），最后一项则是指定域名允许访问，不符合该规则的话就会设置invalid_referer这个变量为1
	if ($invalid_referer){
		return 403;
	}  # if也是Nginx的一个块级结构
	return 200 "yes";
}
```

但是这个技术太垃圾了，毕竟referer头信息是可以随便改的，这时候就需要我们用第三方模块进行再次防盗，此处暂时不表

## rewrite模块

从上面的内容我们可以看到，似乎Nginx配置文件内部还可以写一些逻辑判断语句？事实也的确如此，除了上述提到的`if`语句之外，Nginx配置文件内也可以进行简单的变量赋值，判断，跳出等操作

而这些操作的指令都在Nginx默认加载的rewrite模块中

### set

比如有如下代码

```
location /server{
	set $name test;
	set $age 10;
	default_type text/plain;
	return 200 $name=$age;
}
```

即可在屏幕上显示`test=10`，可以发现Nginx里面语法的随意性，赋值变量甚至不需要`=`，而输出更加不分类型（也就是只能存储字符串，不能进行运算等操作），这也说明了在配置文件中编写程序的局限性

同时还要注意就算实在需要设置变量，也避免和Nginx全局变量同名，下面是部分常用的全局变量

```
$remote_addr		    // 获取客户端ip
$binary_remote_addr	    // 客户端ip（二进制)
$remote_port		    // 客户端port，如：50472
$remote_user		    // 已经经过Auth Basic Module验证的用户名
$host			        // 请求主机头字段，否则为服务器名称，如:blog.sakmon.com
$request		        // 用户请求信息，如：GET ?a=1&b=2 HTTP/1.1
$request_filename   	// 当前请求的文件的路径名，由root或alias和URI request组合而成，如：/2013/81.html
$status			        // 请求的响应状态码,如:200
$body_bytes_sent        // 响应时送出的body字节数数量。即使连接中断，这个数据也是精确的,如：40
$content_length	        // 等于请求行的“Content_Length”的值
$content_type	        // 等于请求行的“Content_Type”的值
$http_referer	        // 引用地址
$http_user_agent        // 客户端agent信息,如：Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.76 Safari/537.36
$args		            // 与$query_string相同 等于当中URL的参数(GET)，如a=1&b=2
$document_uri	        // 与$uri相同  这个变量指当前的请求URI，不包括任何参数(见$args) 如:/2013/81.html
$document_root	        // 针对当前请求的根路径设置值
$hostname	            // 如：centos53.localdomain
$http_cookie	        // 客户端cookie信息
$cookie_COOKIE	        // cookie COOKIE变量的值
$is_args	            // 如果有$args参数，这个变量等于”?”，否则等于”"，空值，如?
$limit_rate	            // 这个变量可以限制连接速率，0表示不限速
$query_string	        // 与$args相同 等于当中URL的参数(GET)，如a=1&b=2
$request_body	        // 记录POST过来的数据信息
$request_body_file	    // 客户端请求主体信息的临时文件名
$request_method	        // 客户端请求的动作，通常为GET或POST,如：GET
$request_uri	        // 包含请求参数的原始URI，不包含主机名，如：/2013/81.html?a=1&b=2
$scheme		            // HTTP方法（如http，https）,如：http
$uri			        // 这个变量指当前的请求URI，不包括任何参数(见$args) 如:/2013/81.html
$request_completion	    // 如果请求结束，设置为OK. 当请求未结束或如果该请求不是请求链串的最后一个时，为空(Empty)，如：OK
$server_protocol	    // 请求使用的协议，通常是HTTP/1.0或HTTP/1.1，如：HTTP/1.1
$server_addr		    // 服务器IP地址，在完成一次系统调用后可以确定这个值
$server_name		    // 服务器名称，如：blog.sakmon.com
$server_port		    // 请求到达服务器的端口号,如：80
```

一般来说，全局变量同时包括我们自己定义的变量常常可以通过在日志中[进行输出](#自定义服务日志)来便于我们进行服务器的调试

### if

Nginx里面每一个语法能做的事情都非常有限，比如`if`语句的判断括号内只允许出项七种判断方式

- 直接是一个变量名，此时如果这个变量是`0`或为空，判断不成立，其他情况判断成立（判断请求是否包含变量）
- 比较两个字符串，中间用`=`或`!=`相连，只比较两个字符串是否完全一致（判断请求方式是否为`POST`）
- 通过添加`~`或`~*`进行正则表达式判断，如`$arg ~ [regex]`，其中`~`也可以用`!~`表示取反
- `-f/!-f`判断文件是否存在，如`-f [文件路径]`，注意资源会在`locaiton`指定的目录下寻找，与此类似的还有`-d`判断目录是否存在，`-e`判断目录或文件是否存在，`-x`判断文件是否可执行

### break

`break`可以直接退出一个location内容，并且将请求重定向到根目录下的location指定的请求资源上，如果资源不存在就报404

```
location /test {
	if ($args){
		break;
	}
}
```

则如果存在参数的话直接退出在根目录下寻找`test/index.html`或者是`test`资源进行展示

### return

`return`之前我们都有了解过，它会直接返回给客户一个状态码和响应内容，但它实际上还有别的用法，比如可以直接返回一个URL地址，从而实现重定向的效果

### rewrite

既然都叫做rewirte模块了，那么最重要的指令也就肯定是这个`rewrite [regex] [url] {flag}`指令了

如何使用呢，其实也非常简单，如上面所示，我们可以通过正则表达式匹配访问的内容，同时重定向到相应的页面

```
location /rewrite {
	rewrite ^/rewrite/(test).*$ /$1;
	rewrite ^/rewrite/baidu$ https://www.baidu.com;
}
```

此时注意当我们不添加flag时，我们如果输入`ip:port/rewirte/test1111`则默认状态会被**重写**为`/test`页面（url栏不变），而访问百度则是被**重定向**到百度（返回302）

其中的`flag`为可选项，有以下几个选择

- `last`寻找其他location处理本次请求并重写页面，没有的话就去寻找本地资源重定向，和默认状态下基本一致，如果访问的是外部链接则同样是重定向
- `break`不寻找其他location内容，直接去寻找本地资源重定向，不影响外部链接访问
- `redirect`对寻找到的location内容也进行重定向，其他不变
- `permanent`和`redirect`类似，但是返回的是301表示永久重定向

同时`rewrite`指令也不止只能用在location块中， 当它用在server块中的时候就可以实现域名跳转

```
server {
	listen 80;
	server_name www.test1.com www.test2.com;
	rewrite ^(.*) http://www.test.com$1;
}
```

如上代码所示

### rewrite_log

可以通过`rewrite_log on`打开URL重写日志的输出功能，通过了`rewrite`指令的请求会以notice的形式打印在错误日志上，注意要设置错误日志的等级为`notice`不然不可见

## 反向代理

事实上Nginx还可以进行正向代理但这不是我们学习的重点，我们需要学习其中的反向代理功能

Nginx反向代理模块的指令由`ngx_http_proxy_module`模块进行解析，该模块也是默认安装模块，我们需要了解的就是这个模块中的一些主要指令内容

### proxy_pass

这个指令用于把我们的请求代理转发到固定的服务器，并展示请求之后的内容，比如有如下代码

```
location /test {
	proxy_pass http://ip:port;
	proxy_pass http://ip:port/;
}
```

那么此时我们如果访问这台服务器的任何内容，都会被分发到指定的`ip:port`

同时对于第一条指令，请求会被分发到`http://ip:port/test/index.html`或在被代理服务器上寻找`test`资源，而第二条指令则不会拼接location中的内容，而是直接分发到`http://ip:port/`去寻找内容，但如果是`location / {}`的话就无所谓了

> 注意这里代理和之前rewrite的不同，我们之前说过，当我们使用rewrite请求跨域资源时，无论加什么参数都会被**重定向**到新的URI上去，也就是会变化地址栏中的请求信息，但是我们通过proxy_pass进行代理时虽然被代理服务器收到的还是代理服务器的请求需求，但是地址栏内容不会发生变化，是一个彻底的**重写**操作
>
> 往更深层次来说，rewrite指令让用户连续发了两条请求给不同的服务器（因为第一条请求返回了另一个服务器的ip），而proxy_pass用户始终只发一条请求给代理服务器，被代理服务器始终不对用户可见

### proxy_set_header

有些时候我们在接收到用户的请求时需要在其请求头中添加一些别的信息之后在转发给被代理服务器，此时就需要用到`proxy_set_header [header_name] [value]`指令给请求内容添加指定头信息

我们可以通过构造内容进行演示

![image-20220223150949617](https://s2.loli.net/2022/02/23/M4IpwRDQoknjZx9.png)

![image-20220223151210852](https://s2.loli.net/2022/02/23/eQ1blM9pImC48Zs.png)

可以看到是的确满足了我们的要求，其中82端口就是以后我们被代理服务器，而81端口则是我们的反向代理服务器

有了这个功能，我们就可以给被代理服务器发送用户的真实ip和端口，实现了服务器知道我们的情况但是我们永远不知道被代理服务器信息的功能

### proxy_redirect

为了能够彻底隐藏被代理服务器的所有信息，不给黑客有机可乘，上面的内容显然是不够的，比如在被代理服务器下有如下代码

```
location / {
	if (!-f $request_filename) {
		return 302 http://172.17.0.2:82;
	}
}
```

当访问的资源不存在时，此处显然做了一个重定向处理，且重定向到了自己身上，对用户来讲，会发现地址栏突然就变成被代理服务器的地址，这显然是我们不想看到的，这意味着被代理服务器的地址暴露在了用户面前

究其原因，实际上是代理服务器收到了被代理服务器发来的一个包含`Location`键的响应头的响应信息，该键的值即为被代理服务器的ip地址，在不处理的情况下，代理服务器忠实的将这个响应内容交给用户，用户的浏览器一发现其中的`Location`信息，即立刻就去访问其中指定的ip内容了，这也符合重定向的定义，但我们必须解决这种情况

如果说`proxy_set_header`是修改用户的请求头信息，那么`proxy_redirect`就是修改被代理服务器的响应头信息，它会判断`Location`中的内容是否与指定内容一致，如果一致的话就把他替换为我们希望的地址，比如我们可以在代理服务器上设置

```
location / {
	proxy_pass http://172.17.0.2:82;
	proxy_redirect http://172.17.0.2:82 http://172.17.0.2:81;
}
```

此时我们就可以发现，原本的重定向内容还是被替换成了代理服务器的ip，且再次请求时会跳转到被代理服务器的首页

> 新版Nginx似乎默认这个选项就是开启状态，如果需要测试则应先`proxy_redirect off`

## HTTPS

默认Nginx是不提供HTTPS支持的，如果我们想使用HTTPS，就需要[重新编译文件](#版本迭代)，并添加上`--with-http_ssl_module`模块

重新安装完成之后，可以通过`nginx -V`查看当前模块配置情况

### 通过openssl创建证书

执行以下指令即可，之后会在该目录下生成四个文件

```
openssl genrsa -des3 -out server.key 2048
openssl req -new -key server.key -out server.csr
cp server.key server.key.org
openssl rsa -in server.key.org -out server.key
openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.crt
```

![image-20220223171024898](https://s2.loli.net/2022/02/23/QAkBMPUzXgjEWGC.png)

这样准备工作就完成了

### 开启ssl支持

默认的Nginx文件内的最后就有开启https的配置的范例，我们只需要去掉其中的注释并修改部分内容即可使用，最后内容如下

```
# HTTPS server
    server {
        listen       443 ssl;
        server_name  localhost;

        ssl_certificate      /root/cert/server.crt;
        ssl_certificate_key  /root/cert/server.key;

        ssl_session_cache    shared:SSL:1m;  # 所有内容共享缓存
        ssl_session_timeout  5m;

        ssl_ciphers  HIGH:!aNULL:!MD5;  # 允许的密码格式
        ssl_prefer_server_ciphers  on;

        location / {
            root   html;
            index  index.html index.htm;
        }
    }
```

此时我们可以尝试通过浏览器访问`https://172.17.0.2`，会发现浏览器能够访问了，但是报了一个不安全的错误，因为我们用的是没有经过认证的证书，不用管他，点击继续前往即可正确访问我们的网站

## 负载均衡

实现负载均衡有很多种很多种方式，最原始的就像是用户手动选择自己需要的服务连接，不止如此，我们还可以通过在DNS服务中为同一个域名添加多个IP地址，从而利用DNS轮询的方式选择IP访问，但是这两个方式都不是合理的选择，比如第一种方式并不能保证所有的人都平均的选择各个连接，而DNS轮询结果将会较长时间保存在本地缓存，如果发生对应IP的服务器宕机，同样也影响我们的访问

### 四层/七层负载均衡

被大众所认可的负载均衡器实际上包括四层负载均衡和七层负载均衡，这里的四层和七层指的是OSI参考模型中的第四层（传输层）和第七层（应用层）

四层负载均衡一般以硬件的负载均衡器（F5，BIG-IP等）为主，在数据包还未解析的底层就进行了分发，性能很高，但是硬件的成本也很高，动辄就是几十万，对于我们这种穷苦开发者肯定是用不起了，当然四层负载均衡也有软件方式实现，但相对来说性能也不如硬件设备了

幕墙常见的组合是四层负载（LVS软件）+七层负载（Nginx）实现负载均衡

### Nginx简单轮询负载

Nginx实现负载均衡的原理是在反向代理的基础上把用户的请求根据指定的算法分发到不同的服务器上

由于我们拥有多个服务器，肯定不能一个个去配`proxy_pass`，因此我们需要借用一个负载均衡池（upstream）来将所有的被代理IP地址放到这个池子里，由算法帮助我们选择访问的IP

```
    upstream backend {
        server 172.17.0.2:84;
        server 172.17.0.2:85;
        server 172.17.0.2:86;
    }
    server {
        listen 83;
        server_name localhost;
        location / {
            proxy_pass http://backend;
        }
    }
    server {
        listen 84;
        server_name localhost;
        default_type text/html;
        location / {
            return 200 "<h1>port 84</h1>";
        }
    }
    server {
        listen 85;
        server_name localhost;
        default_type text/html;
        location / {
            return 200 "<h1>port 85</h1>";
        }
    }
    server {
        listen 86;
        server_name localhost;
        default_type text/html;
        location / {
            return 200 "<h1>port 86</h1>";
        }
    }
```

这样就实现了最简单的负载均衡的配置，反向代理服务器会以轮询的方式逐个访问三台被代理服务器，在我们自己的浏览器也可以通过刷新看到访问的服务器周期性变化

### upstream池负载标记

事实上，我们可以在定义的`upstream`池中对每一个IP进行标注，以优化负载均衡的效率

- `down`此IP永久不可用，用于个别服务器维护时使用
- `backup`标记该IP为备用服务器，当别的服务器无法处理请求时再用这台服务器
- `max_fails=[num]`设置允许请求代理服务器失败的次数，默认为1
- `fail_timeout=[num]`表示设置经过`max_fail`失败之后，该服务器暂停的时间，默认为10秒

比如我可以这样设置上面的三个服务器

```
upstream backend {
    server 172.17.0.2:84 down;
    server 172.17.0.2:85 backup;
    server 172.17.0.2:86 max_fails=3 fail_timeout=15;
}
```

### 负载均衡策略

在实际应用中，不同服务器的性能情况不相同，任一时刻所接收到的用户请求数也不同，默认的普通轮询不能满足我们的实际访问需求，这时候就需要为负载均衡添加一些规则

- 加权轮询，我们可以在默认情况下在每一个IP后加上`weight=[num]`设置服务器权重，默认为1，权重越大，被分配到的概率越大

- `ip_hash`负载均衡算法，一般用于不同服务器session不共享的问题，它会计算用户的IP信息进行某种hash算法，将这个用户IP固定到唯一一台被代理服务器上，从而实现用户访问内容的session一致性，使用方法就是在`upstream`块的最上方指定`ip_hash;`即可

  但是这种方式也有局限性，由于它配置的全局性，会导致一切加权内容都失效，最终可能无法实现真正的负载均衡，同时对于session不一致问题也可以通过redis解决，因此这种方式不建议使用

- `least_conn`这种负载均衡算法可以将用户的请求分发到请求连接最少的服务器上，适合处理请求处理 长短不一致造成的服务器过载情况，相对还是比较智能的，使用方式也是全局方式

- `url_hash`按照用户url的内容进行分发，也就是用一台服务器响应用户访问的相同的文件内容，一般用于避免不同服务器多次调用同一文件系统内的同一文件的状况，保证当前用户访问的每一个文件都只存在于一台被代理服务器上，用法是在头部加上`hash $request_uri`

- `fair`这个负载均衡策略相较于其他几种都更为智能，会根据访问的页面大小，加载时间长短智能的进行负载均衡，但是这个智能所付出的代价就是原生的Nginx是不支持`fair`策略的，我们需要自己手动添加第三方模块

  > 如何添加第三方模块，就拿这个案例来说，我们需要以下几步
  >
  > 1. 下载模块，`https://github.com/gnosek/nginx-upstream-fair`
  > 2. 解压缩之后将其命名为`fair`
  > 3. 编译时添加参数`--add-module=[fair路径]`即可
  > 4. 在`src/http/ngx_http_upstream.h`找到结构体`ngx_http_upstream_srv_conf_s`添加`in_port_t  default_port`再执行make即可

## 缓存集成

Nginx还可以作为web缓存服务器使用，具体流程是当用户 多次请求同一内容时，第一次请求的页面会被暂时保存在Nginx服务器某个文件夹内，再次访问时通过比对直接从服务器中取出缓存内容进行响应，这样一方面降低了被代理服务器的负载，另一方面也更快提供给用户页面返回

缓存相关的配置指令在默认安装的`ngx_http_proxy_module`模块中，接下来也只介绍常用指令

### proxy_cache_path

这个指令用于指定缓存在Nginx上存储的目录位置，同时由于将所有缓存都存放在同一目录下当缓存变多时同样会影响性能，因此可以通过参数的方式对请求进行特殊加密后创建多级文件夹存放缓存

指令的完整形态是`proxy_cache_path [path] [keys_zone=] [levels=] [inactive=] [max_size=]`，其中level即指定目录层级，假设此时我们需要一个key用于加密，比如`key=test`，则`MD5(test)=098f...7b4f6`，假设`levels=1:2`，那么我们就会在`path/6/4f`这个目录下保存这个key的所有缓存内容，缓存最多指定三层目录

其他参数比如`keys_zone`是为这个缓存区设置大小和名称，用于存放各种keys，1M大概可以存放8000个keys，而`inactive`则指定缓存数据在多少时间内未被访问则自动删除，`max_size`设定最大的缓存空间，当单个key缓存存满之后会覆盖缓存时间最长的资源

由于除了`path`后面参数不分前后，因此指定时必须说明参数名，如`proxy_cache_path /usr/local/nginx_cache levels=2:1 keys_zone=test:100m inactive=1d max_size=2g`

### 其他指令

- `proxy_cache [zone_name/off]`用于开启缓存，如果开启的话则自定义使用哪一个缓存区进行缓存（上面指定的`keys_zone`）
- `proxy_cache_key [key]`用于设置key值，一般通过全局变量获得请求信息设置key，默认为`$scheme$proxy_host$request_uri`
- `proxy_cache_valid [status] [time]`对不同的返回状态码设置缓存时间，不然默认用`inactive`，设置多个会从上往下找，注意`status`可以设置为`any`
- `proxy_cache_min_uses [num]`，设置资源被访问多少次之后开始被缓存
- `proxy_cache_methods [method]`设置缓存哪些HTTP方法（`GET`等）

### 检测缓存是否生效

一般来说我们的缓存设置在`location`块下，往往和`proxy_pass`呆在一起，我们如果想知道我们的缓存设置有没有生效，最好的办法就是在请求之后去指定的缓存目录下查看是否存在一串md5值的文件，但是如果嫌麻烦，我们也可以在缓存块之下设置`add_header nginx-cache $upstream_cache_status`，然后在访问资源时进行抓包，查看头信息中`nginx-cache`的值，如果是`HIT`则说明用到了Nginx的缓存

## 服务端集群

Nginx在处理高并发请求和静态资源的方面十分强大，但是对于后台业务代码模块相对薄弱，因此我们可以将到后台业务部署在Tomcat，接着用Nginx反向代理到后台服务器即可，这也是今后大项目开发的基本基础

### Tomcat部署

1. 直接去[官网](https://tomcat.apache.org/download-10.cgi)下载Tomcat版本，在本地目录进行解压
2. 之后将打包好的项目`.war`包拷入`webapps`目录下
3. 进入`bin/startup.sh`执行即可
4. 可以在浏览器访问`:8080`端口看看是否启动成功

### Nginx开发环境

更改配置文件

```
upstream webservice{
	server 127.0.0.1:8080;
}
server {
	listen 80;
	server_name localhost;
	location /demo{
		proxy_pass http://webservice;
	}
}
```

即可

但是这样似乎和直接访问Tomcat也没什么不同，为什么突然要在中间加一层呢，此时就需要利用Nginx的特性对被代理服务器实现动静分离和集群搭建，这才能完全体现Nginx的优势

### 动静分离

其中的动静就是只动态资源和静态资源，正如之前所讲，Nginx处理静态资源的能力是非常高的，而相反对于连接动态资源cgi显得有些疲软和复杂，因此我们正好取长补短，用Tomcat处理后端请求数据，而Nginx负责展示静态的数据即可

同时动静分离还可以降低动态资源和静态资源的耦合度，就算是后端Tomcat宕机了，也不影响静态资源的展示

### 高可用解决方案

之前我们提到过，当某台被代理服务器宕机之后，由于Nginx的负载均衡和反向代理的特性，我们可以将请求分发到其他正常的代理服务器上从而不影响用户访问，但是万一Nginx宕机了那该怎么办呢

此时我们可以介绍一种Keepalived软件来解决

#### VRRP协议

Keepalived主要使通过VRRP协议实现高可用的功能，而这个协议的核心就是将几台不同的服务器虚拟成一台设备，对外提供虚拟路由器的IP，而在这服务器组内，分为时刻接收用户请求的Master服务器，和若干台用于监听Master服务器的Backup服务器，Master服务器会每隔一段固定时间向Backup服务器发送一个心跳检测， 如果在指定时间内Backup没有接收到这个通知内容，那么Backup就会替代Master成为新的接收用户请求的Master服务器

接下来，我们只需要在两台Nginx服务器上安装Keepalived支持即可

#### 下载安装

下载[Keepalived](https://keepalived.org/download.html)，解压之后`./configure --sysconf=/etc --prefix=/usr/local`，接着`make && make install`即可安装

进入`/etc/keepalived/keepalived.conf.sample`，我们可以分析一下其中的配置内容

![image-20220225185340622](https://s2.loli.net/2022/02/25/syGUW31eRcMrgXD.png)

修改完成后，执行`/usr/local/sbin/keepalived`即可开启功能，此时我们在Master主机上通过`ip addr`可以看到新的对外虚拟ip，此时我们可以通过这个虚拟ip访问Master主机

此时如果两台服务器分别安装Keepalived，并设定虚拟主机ip相同，此时如果一台主机Keepalive服务掉线了，那么另一台主机就能够及时补充为Master进程，直到掉线主机恢复

#### 优化

但是我们发现这种情况时仅当Keepalived自己进程被切断之后才会切换节点，显然没有和服务器上的Nginx建立联系，就算Nginx服务断了也和你Keepalived没有任何关系，因此我们需要将两个内容进行绑定

这时我们就需要在配置文件中加入`VRRP`脚本，首先编写一个bash脚本，放在keepalived文件夹下

```shell
#! /bin/bash
num=`ps -C nginx --no-header | wc -l`
if [$num -eq 0];then
	killall keepalived
fi
```

之后在配置文件中加上`vrrp_script`

```
vrrp_script nginx{
	script "/etc/keepalived/nginx.sh"
	intercal 2  # 脚本执行周期
	weight -20  # 权重减20
}
```

即可

## 制作下载站点

我们有时会在某些镜像站上看到下载列表之类，点一点就可以飞速下载内容，事实上大多就是利用Nginx做到的，我们也可以尝试一下

为了实现该功能需要使用默认加载模块`ngx_http_autoindex_module`

- `autoindex [on/off]`开启目录列表输出
- `autoindex_exact_size [on/off]`指定是否展示文件的详细大小，如果off的话会显示`kB/MB`之类
- `autoindex_format [html|xml|json|jsonp]`设置目录列表格式
- `autoindex_localtime [on/off]`在目录列表上显示文件修改时服务器的时间，`off`的话显示GMT时间

```
location /download {
	    root html;
	    autoindex on;
}
```

这样就会在`html/download`下寻找下载内容，此时我们只需要在目录下创建download目录，放一些下载文件即可

![image-20220225194235249](https://s2.loli.net/2022/02/25/FAry7wenG64kxXL.png)

### 用户认证模块

每个人都可以下载 服务器内容显然是危险的，因此我们需要对访问的用户进行筛选，只有输入正确的用户名密码才能够下载内容，Nginx也提供了这样的模块，只需要在其中加上`auth_basic [string]`即可设定验证，其中`[string]`为提示信息，然后我们再指定`auth_basic_user_file [file]`文件来确认用户输入内容是否符合要求来指定是否通过请求

但是为了这个功能能够实现，我们还需要安装一下`yum install -y httpd-tools`，之后使用命令

![image-20220225203306484](https://s2.loli.net/2022/02/25/kU5YGy3nIC4bqJT.png)

然后我们在浏览器再次访问内容，就会出现输入用户名和密码的提示框

![image-20220225203431469](https://s2.loli.net/2022/02/25/sc2VZHbhijuxBkP.png)

## Lua

Nginx是可扩展的，我们可以使用Lua来扩展Nginx的功能，Lua是一个脚本语言，随意程度可以和Javascript媲美

### 安装

1. `wget http://www.lua.org/ftp/lua-5.4.4.tar.gz`，接着解压
2. 来到安装目录，`make linux test`测试是否可以在本地安装，如果报错了的话就安装它报错的安装包
3. `make install`安装
4. `lua -v`检测是否安装成功

### Lua程序

Lua有可以通过交互式或者是脚本式来运行文件，首先先介绍一下交互式运行程序

1. `lua`调出命令行
2. `print("hello word")`即可打印结果
3. `Ctrl+c`退出

脚本式也很简单，只需要创建一个`.lua`文件，接着在里面输入lua语法接着`lua [文件名]`即可

> lua和javascript差不多，语句加不加分号其实无所谓

### 语法

- `--`单行注释，`--[[  ]]--`多行注释，`---[[ ]]--`取消多行注释
- 区分大小写，不等于是`~=`，逻辑运算符是`and or`之类，变量不用声明类型
- `..`连接两个字符串，`#[变量名]`计算变量字符串长度，数字型变量会报错
- `local`声明局部变量，不声明就是全局变量，`nil`是无效值，用`{}`包起来的叫table类型，比较重要，可以通过`type([变量名])`来查看变量类型，只有`false/nil`是False，其他包括`0`都是True
- 可以通过`[变量名]=[[`的方式声明长字符串，最后记得`]]`闭合
- 数组（table 表）索引默认从1开始，但我们可以先声明`a={}`接着通过`a["key"]=value`或`a.key=value`指定索引和值，这样的话`a[1]=nil`，还可以`a={"test",key=value}`直接指定一个表
- 函数`function name(params)`开始，以`end`结束，可以返回多个返回值，名字相同会覆盖函数并不会重载，可以乱传参数，多的丢弃，少的赋值`nil`，多个参数`...`，赋值直接`local a,b,c = ...`即可，返回值也是`return`
- 判断和循环不用加括号，语法是`if [条件] then`和`while [条件] do`和`for i=exp1,exp2,exp3 do`，这仨都以`end`结尾，同时`exp1`之类的和C里面的两个`;`隔开的东西完全一致，另外还有`repeat [循环体] until [条件]`和`for i,j in ipairs(a) do`其中ipairs会返回a的索引和值
- `require [库]`引入第三方库，`[类]:new()`创建一个对象，`[对象]:[方法]`调用方法

### nginx_lua

这是一个淘宝开发的`ngx_lua`模块，将lua解释器集成进Nginx，可以使用lua脚本实现业务逻辑，降低了业务逻辑的实现成本

正常安装比较麻烦，因此我们采用安装OpenResty直接一步到位

> OpenResty是淘宝工程师开发的，集成了大量的精良lua库，第三方模块和大多数依赖项

#### 安装方式

1. OpenResty已经内置了Nginx，因此我们需要先将之前Nginx关掉`nginx -s stop`
2. 进官网查看[安装方法](https://openresty.org/cn/linux-packages.html#centos)，当然我们也可以下载源码安装`wget https://openresty.org/download/openresty-1.19.9.1.tar.gz`
3. 接着解压，进入目录`./configure`和`make && make install`
4. 进入`/usr/local/openresty/nginx`目录，会发现和我们通过二进制安装的Nginx十分类似，我们也可以在`conf/nginx.conf`更改相关配置文件，以及通过`sbin/nginx`启动服务

#### 简单程序

先让我们在配置文件中指定一个location熟悉一下openresty的基本语法

```
location /lua {
    default_type text/html;
    content_by_lua ngx.say("<h1>Hello</h1>");
}
```

![image-20220226090449325](https://s2.loli.net/2022/02/26/f6jws18vPQcBKeC.png)

我们会发现想要网页上输出指定内容，我们就需要一个`content_by_lua`的指令，而在`ngx_lua`里面还有各种各样的`xxx_by_lua`指令，这些指令的含义就是应该在这些指令后面跟上一个lua语句



#### 常用语法

下面用一段代码展示常用指令操作

```
location /test {
	default_type text/html;
	set_by_lua $param "
		local uri_args = ngx.req.get_uri_args()
		local name = uri_args.name
		local gender = uri_args.gender
		if gender=='1' then
			return name.."先生"
		return name.."女士"
	"
	charset utf-8;
	return 200 $param;
}
```

可以发现我们嵌入了一段类似lua函数的内容，赋值给了nginx的一个变量，从而实现了指令的多种变化，避免使用Nginx内置的危险`if`语句

同时官方建议我们替换`by_lua`而使用`by_block`，用法差不多一致，只是把后面的双引号改为`{}`即可，里面还是若干lua代码

其他内容库我们可以访问[官网](http://openresty.org/cn/components.html)查看各个模块里面究竟如何使用

# Vue2

Vue就是一套构建用户界面的渐进式JavaScript框架，就是根据获得的数据，利用小巧的核心库+插件的层次结构组成的库来设计用户响应界面的框架

同时Vue还有以下特点

- 采用组件化模式，将页面中每一个模块（HTML、CSS、JS）打包成一个个组件（.vue），提高代码复用率，更好进行维护
- 声明式编码，与之相对的是命令式编码，声明式只需要通过简单的声明框架会自动帮助我们写好声明的内容，且嵌入在HTML页面中，益于开发和阅读
- 虚拟DOM技术，当页面上的内容发生变化时，Vue框架会先自动将变化后的DOM信息引入虚拟DOM中，比较更新后的内容与原先虚拟DOM内容的区别和更新，并对新内容进行合并，最终在页面中只展示更新之后的内容，而不是将整个页面重新加载

## 嵌入式

### HelloWorld

想要开始学习一门技术，正常的步骤就是从helloworld开始，同样我们可以创建一个html文件，开始制作我们的第一个Vue项目

不过在此之前我们还是需要先[下载](https://cn.vuejs.org/v2/guide/installation.html#%E7%9B%B4%E6%8E%A5%E7%94%A8-lt-script-gt-%E5%BC%95%E5%85%A5)一下Vue的js库（当然也可以使用[CDN](https://cdn.jsdelivr.net/npm/vue@2.6.14/dist/vue.js)，并且导入进我们的项目中

![image-20220311211748796](https://s2.loli.net/2022/03/11/gzyMcrU8mKDIijX.png)

编写如下代码

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>测试html文件</title>
    <script src="../js/vue.js"></script> <!--引入Vue库-->
</head>

<body>
    <div id="root">
        <h1>Hello {{name}}</h1> <!-- {{}}包裹住的内容称为容器模版，其中的代码依然符合HTML规范 -->
    </div>
    <script>
        // 阻止Vue启动时生成的生产提示
        Vue.config.productionTip = false
        // 创建Vue实例，想要使用Vue就一定需要创建实例
        new Vue({
            el: '#root',  // 建立Vue实例和页面容器的关系，现在就是为上面的div服务
            // 当然上面也可以document.getElementById('root')
            data: {  // data中存储数据，数据供el所指定的容器使用，它的值可以像这样写成对象
                name: 'World'
            }
        })
    </script>
</body>

</html>
```

接着就可以在页面上显示内容了

然而上面的代码虽然简单，但是还是需要有一些注意点

- 一个Vue实例和容器之间是严格的一对一关系，比如如果存在两个容器`class`都为`root`，那么Vue中的`.root`仅会匹配DOM中从上往下的第一个`.root`容器，或者如果创建了两个Vue实例匹配`#root`，那么第二个Vue实例也会失效
- `{{}}`之内的内容看上去是在Vue实例中定义的data值，但是实际上也是js表达式，可以在其中添加任意的js表达式，但只是不建议这么写js

### 数据绑定

#### 单向数据绑定

除了上面展示的直接通过`{{}}`包含`data`对象中的内容实现包含信息之外，Vue还提供了指令语法内容，用它我们可以根据需要绑定`data`内的属性

```html
<body>
    <div id="root">
        <h1>插值语法</h1>
        <h2>Hello {{name}}</h2>
        <hr>
        <h1>指令语法</h1>
        <h2>
            <!--其中v-bind可以运用在所有标签属性之上，会把后面的引号内内容自动识别成js语句-->
            <a v-bind:href="url">v-bind进百度<br></a>
            <a :href="url">:简写直接进百度</a>
        </h2>
    </div>
    <script>
        Vue.config.productionTip = false
        new Vue({
            el: '#root',
            data: {
                name: 'World',
                url: "https://www.baidu.com"
            }
        })
    </script>
</body>
```

指令语法可以解析标签（包括标签体内容和绑定事件，以v-开头的指令），功能非常强大

同时注意当需要动态变化的属性值比较多的时候，我们可以通过在data中添加比如`contain:{name:'123'}`之后在容器中添加`{{contain.name}}`即可

`v-bind`可以绑定所有的标签属性，包括class指定的CSS样式等，使目标可以根据我们的需要动态调整

#### 双向数据绑定

除了`v-bind`可以进行数据绑定，但是他是单向数据绑定，意思就是虽然我们在Vue实例中修改值时页面上的内容也会发生改变，但是比如页面上有一个输入框，将其中的`value`属性通过`v-bind`绑定，那么我们如果在输入框中改变页面上`value`的值，并不会影响到实际Vue实例中data下的属性，此时如果我们想要两个内容同步变化，那么我们就需要`v-model`绑定输入框中的value值

不过注意`v-model`只能绑定表单类型的标签属性，也就是应该满足Vue实例属性和页面内容可以双向更改的情况下（存在`value`属性）才能使用，不然会报错

同时由于`v-model`只能绑定表单元素的`value`使用，因此我们可以直接省去`value`值，直接`v-model:`绑定表单内容

```html
<body>
    <deng degndiv id="root">
        <h1>Hello {{name}}</h1>
        <input type="text" v-model:value="user"><br>
        <input v-model="user" type="text" />
    </div>
    <script>
        Vue.config.productionTip = false
        nshu ju jie chiew Vue({
            el: '#root',
            data: {
                name: 'World',
                user: 'root'
            }
        })
    </script>
</body>
```

其中注意别的表单属性与这种直接输入内容的表单属性的操作有所区别，不过第一要义还是盯着value看，比如单选/多选框无论选没选都没有value值，我们就需要自己添加

在绑定监视多个值时（比如页面上的多选框）data中的默认属性应该是`[]`而不是`''`，不然数据没有办法正常添加

同时对输入的内容有要求的时候（比如必须用户输入数字），此时我们可以`v-model.number`来控制输入，否则默认在保存时默认会使用字符串，在与后端交互之中可能会出错

除此之外还有`v-model.lazy`可以当输入框失去焦点时才更新Vue实例内容，`v-model.trim`可以过滤输入前后空格

### Vue实例对象

除了之前我们在前面编写的那样定义Vue实例对象内容进行页面展示，我们可能会发现好像我们创建出来的这个实例似乎并没有用一个变量来接收，也就是因为我们在创建的时候已经设定好了它的所有属性，因此创建之后我们也不需要它了

但是显然照常理来说我们也可以在创建实例之后通过某个调用方法对实例中的属性进行操作

```html
<body>
    <div id="root">
        <h1>Hello {{name}}</h1>
    </div>
    <script>
        Vue.config.productionTip = false
        const v = new Vue({
            data() {
                return {
                    name: 'World',
                    user: 'root'
                }
            }
        })
        v.$mount('#root')
    </script>
</body>
```

其中`$mount`是Vue实例父类的一个属性，我们可以通过修改它来实现Vue的el初始化

![image-20220312115511557](https://s2.loli.net/2022/03/12/xyPutHclAYkv2Vo.png)

同时data除了可以通过创建对象来指定，还可以如上面一样直接写一个函数，返回一个map表即可

#### MVVM模型

MVVM是一种软件架构模式，Vue也参考了这个模型，代表了三个东西，分别是模型（Model），视图（View），视图模型（ViewModel），在我们上面的代码中，分别对应着JavaScript对象（data中存储的所有数据），DOM页面和Vue实例，其中Vue实例作为视图模型，连接着页面内容和JavaScript对象，将JavaScript中的数据封装展示在页面中

> 因此我们常常使用变量名vm接收Vue实例对象

同时我们还可以发现，当我们在data中添加了属性之后，当我们输出Vue实例时，它的属性正包含了我们data中的属性，因此我们可以大胆猜测，是不是我们在`{{}}`中嵌入的数据，实际上就是生成Vue实例中的属性名呢？

显然这是正确的，因此我们可以在页面代码中嵌入任何Vue实例中的属性内容，且不需要在之前添加比如`vm.[属性名]`，Vue会自动帮助我们解析内容

#### Object.defineProperty

在进行进一步学习之前，我们要先复习一下这个方法，它的作用是为某个对象添加属性，但是还是有一些注意点

```html
<body>
    <script>
        let person = {
            name: "ZS",
            sex: "man"
        }
        Object.defineProperty(person, 'age', {
            value: 18,
            // enumerable:true,  // 控制添加的属性可以被枚举，默认false
            // writable:true,  // 控制属性是否可以被修改
            // configurable:true  // 控制属性是否可以被删除
        })
        console.log(person)
        console.log(Object.keys(person))  // 枚举
    </script>
</body>
```

我们可以在控制台验证一下

![image-20220312122531485](https://s2.loli.net/2022/03/12/akOHAxRmJcKIY9n.png)

可以发现通过这个方法直接添加的属性，在不指定其他内容的情况下，默认是不可枚举，不可修改，不可删除的

同时如果直接在定义对象的时候指定死了某一个属性的值，就等于在构造方法中传入了一个值，因此无论传入的值是不是一个变量，比如（`let person = {age:num}`，然而我们如果之后改变了num变量的值，person的属性并不会跟着变化，如果想要实现两者的同步变化，`defineProperty`也可以做到

```javascript
let num = 18
Object.defineProperty(person, 'age', {
    // 当有人读取person的age属性的时候，get方法就会被调用，实时更改属性的值
    get: function () {
        return num
    }
})
```

此时我们可能在控制台中没有明确显示age的属性，但是一点开就会发现其实age属性是在的，只是需要我们点一点三个点才能显示

![image-20220312123557072](https://s2.loli.net/2022/03/12/SYkfCGMQWmbjBwP.png)

这时候如果我们修改num的值，person中的内容也就会跟着变了

![image-20220312123912690](https://s2.loli.net/2022/03/12/lZQJMhuBHDpqnCR.png)

与此同理的是set方法，在修改属性的时候会被调用，此处不举例了

#### 数据代理

数据代理就是通过对一个对象属性的修改，来达到对另一个对象属性修改的效果，而实现这个效果的底层原理其实就是上面讲过的`defineProperty`来定义属性的

此时我们看一下上面原始程序的控制台信息

![image-20220312130233461](https://s2.loli.net/2022/03/12/QVvmR6BbGgOLXuE.png)

在了解了defineProperty方法之后，我们对为什么在页面代码中直接使用`{{name}}`就能展示数据也有了更深层次的了解

明白了这个道理，我们可以尝试在页面中直接添加`{{_data.name}}`，页面中也可以正常显示

> 但是我们如果在控制台直接打开`_data`属性，可能会惊讶的发现里面的数据好像还经过了一次get，也就是核心数据仍然是使用三个点实时获取的，实际上这并不是get效果，而是Vue在其中做了数据劫持的操作，为的是能让页面显示的内容和实时修改内容相匹配，为了每当我们修改了（set）data中的属性时，页面能实时显示修改后的内容

### data数据处理

#### 事件处理（methods）

除了能够调用数据之外，JavaScript还有一个功能就是对于页面的各种事件（点击，键盘），能够进行捕捉并处理，为了能够在页面中响应用户的操作，Vue也贴心地提供了以`v-on`开头的指令（可简写为`@`），使得容器事件可以被Vue实例捕获并处理

同时为了相应按钮能够正确执行内容，我们理应为我们创建的实例添加某些方法，Vue提供了`methods`供我们编写执行函数

##### 点击事件

```html
<body>
    <!-- 
        prevent:阻止跳转
        stop:阻止冒泡事件
        once:只执行一次
		同时也可以写在一起比如.prevent.stop
    -->
    <div id="root">
        <h2>Hello {{name}}</h2>
        <button @click="showinfo()">show Tips</button>
        <a href="http://www.baidu.com" @click.prevent="showinfo()">阻止跳转</a>
        <div @click="showinfo()">
            <button @click.stop="showinfo()">事件冒泡测试</button>
        </div>
        <button @click.once="showinfo()">只执行一次</button>
    </div>
</body>
<script>
    Vue.config.productionTip = false
    const vm = new Vue({
        el: '#root',yu fa
        data: {
            name: 'World'
        },
        methods: {
            showinfo() {
                alert('Tips')
            }
        },
    })
</script>
```

> 注意为指令添加比如`.prevent`细节时并没有提示信息，应该牢记语法

与`data`类似，`methods`定义之后我们也可以在Vue实例中看到它作为一个方法显示在属性中，这意味着如果我们定义了一个比如`show()`的函数，我们除了在标签属性中使用，还可以在页面中利用`{{show()}}`调用

但是注意`methods`定义的内容并不会像`data`一样生成代理数据属性，因为方法中的内容是不常修改的，因此不需要时刻检查是否发生变动，同时也节省了资源和时间

> 除了click之外，form表单的submit属性也可以设置事件处理（比如前端监测内容输错了可以不提交后台`@submit.prevent`等等）

##### 键盘指令

除了能够捕获点击指令之外，我们还可以捕获键盘的输入

```html
    <!-- 
        Vue提供了常见按键的别名，比如enter,delete,esc,space,tab等
        如果我们需要检测别的按键的情况可以通过e.key查看某按键的名字，接着@keyup.[按键名即可]
        如果涉及到多单词，比如CapsLock需要改为caps-lock，不过不是很方便就是了
        同时注意tab只能绑定在keydown上，因为默认会切走光标
		系统修饰键也可以比如@keyup.ctrl.e来绑定快捷键
    -->

    <body>
        <div id="root">
            <input type="text" placeholder="按下回车提示输入" @keyup.enter="showInfo">
        </div>
    </body>
    <script>
        Vue.config.productionTip = false
        new Vue({
            el: '#root',
            methods: {
                showInfo(e) {
                    // if (e.keyCode !== 13) return 与这条语句相等
                    alert(e.target.value)
                }
            },
        })
    </script>
```

#### 计算属性（computed）

当我们需要在页面上显示比如两个`data`中属性的拼接值，我们当然可以通过页面中直接拼接或增加`methods`方法来实现，但是用起来总是感觉怪怪的，这时候就需要使用计算属性了

和前面讲过的`data`和`methods`一样，计算属性`computed`我们也需要将其添加到Vue实例中

```html
<body>
    <div id="root">
        <input v-model="first" type="text" />
        <input v-model="second" type="text" /> <br>
        <span>{{merge}}</span>
    </div>
</body>
<script>
    Vue.config.productionTip = false
    new Vue({
        el: '#root',
        data: {
            first: '1',
            second: '2'
        },
        computed: {
            merge: {
                // 当有人读取这个方法时，get就会被调用
                get() {
                    // 同时如果返回值没有被改变，那么会放进缓存里，再次在页面中调用时get方法不会被重复调用
                    return this.first + this.second
                }
            }
        }
    })
</script>
```

同理只要有get，那么按道理计算属性也有set方法，用法也和上面的内容相同，当merge被修改的时候就会被调用，不过总之就是不太好用，不如直接修改被计算属性调用的data或其他内容比较好

> 需要特别注意，虽然我们是按函数的样子去写的merge，但是它返回的是一个确定的计算出来的值，同时它的名字就叫做计算**属性**，因此他在Vue实例内部实际上是一个属性，因此我们在页面中调用这个计算属性的时候千万不要变成比如`merge()`这样的函数调用写法

同时计算属性还可以通过简写，但是必须只有get而没有set方法才可以使用，可以直接把比如上面的merge当做一个函数使用，返回get所需要的值即可

```javascript
merge() {
    return this.first + this.second
}
```

#### 监视属性（watch）

监视属性就是监视某一个值的变化，直接上案例，在上一个文件的基础上只需要添加

```
watch: {
    merge: {
        handler(newV, oldV) {
        console.log("新:" + newV + "老" + oldV)
        }
    }
}
```

即可实现监视merge函数，在我们输入内容使之发生改变时在控制台提示我们改变内容

![image-20220312215605586](https://s2.loli.net/2022/03/12/rO5zsqhivt26mTo.png)

当我们监视的属性中存在多级结构时（比如`data:{a{b:{c:1}}}`），想要监视其中的子结构（`watch:{a:{...}}`）改变情况，可以在watch监视属性中开启`deep=true`，实现深度检测

> 如果只监测多级结构中的某一个子属性，也可以通过`watch:{'a.b.c':{...}}`进行监视（注意单引号）

同时上面的监视属性同样可以进行简写，同样和计算属性一样，当监视属性内部只需要handler的时候，也可以直接把监视属性定义成一个函数即可

#### 对比计算属性

学了监视属性之后，我们可能发现监视属性似乎和计算属性差不太多，好像上面的案例中的merge也可以在watch中进行更新，只需要在data下再定义一个merge属性即可

但实际上两者还是有差别的，比如watch不依靠返回值来确定属性内容，而是直接在watch内更改属性内容，没有返回结果，但是computed计算属性却要靠返回值确定属性内容，我们还是需要择机使用，不过当两者都可以实现的情况下，我们优先还是使用计算属性

#### 函数管理

假设有这么一个情况，我们在watch监视属性内部调用了一个`setTimeout()`函数，此时应该如何编写内容？

```
watch: {
    merge(newV, oldV) {
        setTimeout(() => {
        	console.log("新:" + newV + "老" + this.second)
        }, 1000)
    }
}
```

此时看上去十分自然，但实际上其中却学问不小，假设我们将函数改为`setTimeout(function(){...})`你会很惊讶的发现this的地方报了一个错，事实上是因为如果是`function`定义函数，那么它的this就在setTimeout函数上，显然这时Window底下的函数，但是如果是箭头函数定义，那么this默认没有，就会去它的外边寻找this，显然就找到了merge所对应的受Vue实例控制的this了

这也同时说明了为什么我们不能将merge定义为一个箭头函数，因为它的外部是window对象，因此其中的this也就变成了window对象了

因此我们总结出两个规律

- 所有被Vue管理的函数，应该写成普通函数，这样其中的this才是vm对象
- 所有不能被Vue所管理的函数，应该写成箭头函数，这样才能使内部的this为vm对象

#### 过滤器（filters）

当我们页面上存在某些简单的数据处理需求时（比如`1000->1,000`或日期格式的转换），且该要求需要被多个内容数据复用（比如界面上多个位置都有`1000`需要处理），当然使用methods或者是computed都能够处理，但是我们还可以使用过滤器这个方案

比如以下场景

```vue
<body>
    <div id="root">
        <span>{{msg | dotF}}</span>
    </div>
</body>
<script>
    Vue.config.productionTip = false
    new Vue({
        el: '#root',
        data: {
            msg: 1000
        },
        filters: {
            dotF(msg) {
                return '1,000'
            }
        }
    })
</script>
```

可以发现在页面中调用时使用管道符将data属性传给过滤器，而且过滤器支持多层传递，可以比如再将`dotF`的返回值作为参数传递给下一个过滤器，进一步的是我们可以在过滤器中指定多个参数，除了第一个参数默认由外部传入，其他参数都可以直接在调用过滤器时添加，比如`msg | dotF('111')`这样

由于过滤器存在不同数据的复用性，因此我们还可以为全局所有的Vue实例添加全局过滤器，只需要使用`Vue.filter('[名称]',function(value){..return ...})`来指定即可，不可避免的增大了

### 渲染

#### 控制标签显示

当我们需要隐藏页面上的某些容器时，我们可以用两个指令实现

- `v-show:[bool]`，自动将容器的`display: none`，这样的隐藏效果可以在页面检查中看到
- `v-if:[bool]`，直接将容器的结构移除，在页面中哪都找不到了，除此之外还有`v-else-if`和`else`，不过控制的容器需要紧紧写在if控制的容器后面才可以生效

其中`v-if`可以与template连用，在不影响原本结构的前提下批量为连续的容器添加样式

#### 枚举列表

与之相类似的是`v-for`标签属性，它可以遍历指定数组的内容，并创建多个与数组元素个数相同数量的容器用以列表展示列表内不同属性

其结构需要了解一下，常规的结构如下

```vue
<body>
    <div id="root">
        <ul>
            <li v-for="(item, index) in items" :key="index">
                {{item.id}}-{{item.name}}-{{item.age}}
            </li>
        </ul>
    </div>
</body>
<script>
    Vue.config.productionTip = false
    new Vue({
        el: '#root',
        data: {
            items: [
                { id: 1, name: 2, age: 3 },
                { id: 2, name: 2, age: 3 },
                { id: 3, name: 2, age: 3 },
            ]
        }
    })
</script>
```

对于其中的内容，有`v-for:"([列表遍历出每一项存放的变量名],[索引变量名]) in [列表]" :key="[遍历出的每一个容器的唯一标识位]"`

当然`v-for`也可以遍历对象，这样的话上面小括号内的第一项就是属性值，第二项就是属性名

#### Key详细探讨

其实我们会发现，上面的`:key`似乎我们不写内容也可以正常显示，我们可能会疑惑这个key到底有什么卵用zhe yzhe yzhe y呢，更重要的是，我们会发现好像这个`key`属性并不存在在页面上，同时如果我们设置了两个相同的key，页面还会报错，这就好玩了，既然不写也没事，在真实页面中也不作为标签内属性展示，写了还有可能错，那我干嘛要写它呢？

其实它虽然名为标签标识位，但是它只在Vue生成的虚拟DOM中使用，其中最重要的一点，就是如开篇所说的，对比更换的内容并进行有选择的修改真实DOM而不是浪费大量时间直接重新生成DOM

教程中展示了一个案例，当我们将遍历的`<li>`标签中的内容进行变化，并改变顺序重新加载DOM之后，在虚拟DOM中发生的变化

![image-20220313174023242](https://s2.loli.net/2022/03/13/HlVczSu9hGqIvem.png)

之后又在`<li>`标签中添加了一个输入框

![image-20220313174155944](https://s2.loli.net/2022/03/13/P2MAkanTdz6eDyH.png)

点击按钮之前和之后

![image-20220313174254051](https://s2.loli.net/2022/03/13/tY5fKQ24HPdM3Z8.png)

![image-20220313174310943](https://s2.loli.net/2022/03/13/a1UkfHw5rcL28WY.png)

这就是典型的如果无脑采用`:key=index`之后会出现的问题，下面是解释图

![image-20220313175149768](https://s2.loli.net/2022/03/13/wfniY2bNXW8kCOQ.png)

可以发现不止是显示的错误操作，同时也使得更换效率极其低下，虚拟DOM的优越性没有被体现，这也就说明了为什么数据库中的记录一般都有一个`id`属性，为前端的页面显示提供了方便

但是这种问题一般不会出现，只有当真实DOM上的显示内容顺序发生改变的时候才会出现（逆序增加，逆序删除等）

同时当我们没有写key的时候，Vue也会自动把`index`作为默认的key

#### 列表过滤案例

学习了上面的内容之后，我们应该可以编写一个在前端筛选数据并实时展示的案例了 

就沿用上一个案例内容，稍作修改，形成了这样的代码

```vue
<body>
    <div id="root">
        <input v-model="searchKey" type="text" />
        <button @click="sortType=-1">升</button>
        <button @click="sortType=1">降</button>
        <button @click="sortType=0">不操作</button>
        <ul>
            <li v-for="selItem in selItems">
                {{selItem.id}}-{{selItem.name}}-{{selItem.age}}
            </li>
        </ul>
    </div>
</body>
<script>
    Vue.config.productionTip = false
    new Vue({
        el: '#root',
        data: {
            items: [
                { id: 1, name: '123', age: 2 },
                { id: 2, name: '145', age: 1 },
                { id: 3, name: '647', age: 3 },
            ],
            searchKey: '',
            sortType: 0
        },
        computed: {
            selItems() {
                const arr = this.items.filter((p) => {
                    return p.name.indexOf(this.searchKey) !== -1
                })
                if (this.sortType !== 0) {
                    arr.sort((p1, p2) => {
                        return (p2.age - p1.age) * this.sortType
                    })
                }
                return arr
            }
        }
    })
</script>
```

注意其中JavaScript对数组排序和筛选条件的使用

形成效果

![image-20220313223952710](https://s2.loli.net/2022/03/13/swDnVQaUruNGg9E.png)

当然联系我们前一节讲过的内容，上面这个代码key值不是数据的id，且在执行排序之后对数据的顺序进行了改变，因此在排序上其实效率并不是很高

### 内部数据监视

我们会发现我们虽然学习了watch检测属性，但是当我们对data中的某一个属性在页面上进行绑定的时候，会发现data中的内容一旦变化，页面内容即跟着改变了，这显然也存在着一个Vue内部的监视机制，会帮助用户检测Vue中的内容并在页面上给出改变

#### 产生问题

比如有以下这样的代码

```vue	
<body>
    <div id="root">
        <button @click="updateD">更新数据</button>
        <span v-for="(item, index) in items" :key="index">{{item.id}}-{{item.name}}-{{item.age}}</span>
    </div>
</body>
<script>
    Vue.config.productionTip = false
    new Vue({
        el: '#root',
        data: {
            items: [{
                id: 1,
                name: '1',
                age: 1
            }]
        },
        methods: {
            updateD() {
                // this.items[0].id = 2
                this.items[0] = { id: 2, name: '2', age: 2 }
            }
        }
    })
</script>
```

看上去似乎十分正常，页面的展示也没有存在问题

![image-20220314203452319](https://s2.loli.net/2022/03/14/8AQ9qkz3tvMaghT.png)

但是如果当我们点击一下按钮之后，想象当中的页面上出现`2-2-2`的情况并没有出现，而只有当我们把上面注释解除掉之后页面上的id值才会被修改，这显然是不符合我们的常理的，而更加不符合常理的事情是当我们点击按钮之后打开f12的，会发现Vue开发者工具中又出现了我们修改的内容，这也太诡异了

![image-20220314203926179](https://s2.loli.net/2022/03/14/yZgBIMDrvJSA21b.png)

而这种情况一旦不注意在实际开发中就会造成十分大的困扰，究其原因还是没有理解Vue自带的监视对象

#### 模拟对象监视

如何才能实现我们修改一个data中的内容之后立刻提醒用户哪个内容被修改了呢？在不看Vue提供的源代码的基础上，我们可能会写出以下代码

```javascript
let data = {
    id: 1
}
let tmp = data.id
setInterval(() => {
    if (data.id !== tmp) {
        tmp = data.id
        console.log('被更改了')
    }
}, 100);
```

这确实能够实现效果，但是这样一个个设置定时器，data一多直接报废了，这时候就需要效仿一下别人的结构了

![image-20220314205414693](https://s2.loli.net/2022/03/14/EbfVcOxCkhqnKFB.png)

在Vue实例中我们找到了`_datad`属性，这个属性我们之前也提到过，就是用来存储在实例化的时候指定的data数据的，但是明明直接将data内容放进去就可以万事大吉，为什么Vue要设定一个get和set方法来控制name项呢？

相信经过上面的示例我们已经知道这个get和set方法是为了能够时刻监视`_data`中的属性变动，但是其中到底是如何实现的呢，我们不妨自己模拟一下，由前面所提到的内容可以知道，`Object.defineProperty`似乎满足了我们的需求

```javascript
Object.defineProperty(data,'id',{
    get(){
        return data.id
    },
    set(val){
        data.id = val
    }
})
```

这样子写吗，显然是不对的，虽然设定了只要想查看id就调用get方法，但是get方法内却又调用了id属性，从而形成爆栈，而`set`方法也与此类似，都不能完成目标操作，这时候就需要我们对其中的内容稍稍改动一下

```javascript
let data = {
    id: 1
}
const obs = new Observer(data)
let vm = {}
vm._data = data = obs
console.log(vm._data)
function Observer(obj) {
    const keys = Object.keys(obj)
    keys.forEach((k) => {
        Object.defineProperty(this, k, {
            get() {
                return obj[k]
            },d
            set(val) {
                obj[k] = val
            }
        })
    })
}
```

看到这个代码的第一眼我们一定是懵逼的，这也正是这个代码能够实现实时监控变量变化的巧妙之处，接下来是对这个代码的解释

1. 页面进行第一次渲染，data初始赋值，新建实例`obs`和`Observer`对象内的内容

2. 注意此时data作为行参传入了`obs`对象（注意此时行参已经和data分开了），同时新创建了一个`obs.k`局部属性，值为传入的局部变量data内的内容

3. 同时在`obs`内部为这个`obs`实例的局部属性`k`新建了一个监听方法（`k=id`，外部可以通过`obs.id`访问到`k`），直到检测到`k`被修改或者在页面上被访问

4. 比如当`k`被修改的时候（比如`obs.id=2`），此时立即调用`set()`方法，虽然`obs.id`的值已经被改变了，但是`set()`的第一个参数就是带着这个修改之后的参数进入方法内，接着我们让`obs的行参obj.id=2`，注意，这里总的来说就是`obs的obj.id=obs.id`，这样就直接避免了像之前一样爆栈的问题

   > 注意到监听属性的`get`方法是在调用想查看监听属性值时被调用，而`set`方法是属性已经被改变之后才被调用

5. 这样就实现了巧妙的属性监听，同时由于最巧妙的是`obj`是`obs`的一个形参，同时还巧妙的利用了JavaScript的特性，即函数内的非`this.[属性]`在实例化之后都只作为构造函数内的局部变量出现，而不作为实例内的属性出现，因此我们在外部是不能通过`obs.obj`或`obs.keys`访问到其中的内容的

6. 当我们打开`Console`的时候可以惊讶的发现`obs`实例的内容似乎与data如出一辙

   ![image-20220314231154351](https://s2.loli.net/2022/03/14/K7y1JogzksYRXC4.png)

   甚至我们可以通过`obs==data`来确定他们俩的内容其实是一样的，这就很好玩了，结合之前我们创建Vue实例之后`Vue._data==[传入data]`判断也是true来看，我们似乎已经复现了Vue中的内容了

这种把原本数据遍历并添加监视方法的行为就称为数据劫持

#### 数组监视

上面所模拟的案例显然并不能解释为什么会产生第一节中的问题，因此我们还需要了解一下Vue的数组监视原理

回到[第一个案例](#产生问题)，我们打开控制台看一看Vue实例的结构

![image-20220315090256503](https://s2.loli.net/2022/03/15/o1dHKADMEWiyFGR.png)

我们会很惊讶的发现，即使`items[0]`里面存在相对应的比如`id.get`方法，然而外层的`items[0]`本身却没有相对应的`get/set`方法，通过上一节的分析，我们就非常好理解为什么我们单独`items[0]=...`的时候不能即时更新页面了，因为它根本没有`set`去监测修改！

所以这是Vue的一个bug吗，显然可能性比较小，真实的情况是，Vue故意避免了我们使用直接赋值的方法为Vue的data内管理的数组进行改动，假如我们需要改动，就需要对这个数组调用Vue为我们写好的七种函数

他们分别是`push/pop/shift/unshift/splice/sort/reverse`，一般来说，这几种函数可以满足我们的所有数组改动需要

你可能注意到了，为什么说是Vue为我们写好的函数呢，这些数组操作函数难道不是本身数组就有吗？当然是的，但是为了调用此方法后实现数据的实时监测，Vue就必须要重写这些方法，我们可以通过控制台验证

![image-20220315091137773](https://s2.loli.net/2022/03/15/WOHmITBXGawenJi.png)

说清楚了数组监测，我们就正式理解了Vue对实例中数据改动的监测原理

> 想要修改数组中的某一项也可以`Vue.set(vm.items,1,{...})`实现实时数据监测
>
> 同时如果使用filter过滤数组并赋值给原数组，事实上是替换掉了整个数组而不是其中的一个下标，因此是会被Vue监测到的

### 其他指令

常见的指令在之前都已经介绍过了，因此接下来的指令可能在开发中不常见，但是部分场景中还是可能会遇到，纯当增长见识了

#### v-text

直接对标`{{}}`，可以在标签属性中直接指定该标签下显示的内容（如`<span v-text="msg"></span>==<span>{{msg}}</span>`不解析，纯文本显示），没什么用

#### v-html

在上面`v-text`的基础上，Vue会将传入的内容经过html解析之后传到页面上，不过注意如果作为用户输入可能会造成XSS攻击

#### v-cloak

不带任何参数`<span v-cloak>{{...}}</span>`当内容存在解析模版时使用，当比如模版还没被加载的时候（此时如果什么都没做会显示`{{...}}`而不是`...`的值）存在`v-cloak`属性，而当模版被加载完毕之后这个属性就会消失，我们可以通过配置`style`样式定位这个属性，当这个属性存在的时候比如不显示内容（`display: none`），直到模版加载成功，`v-cloak`消失，也就显示出来了

#### v-once

同样不带任何参数，在初次动态渲染之后就被视为静态元素，无论data或其他指令中的内容怎么修改这个标签内的这个内容都不会实时更新

#### v-pre

比起`v-once`更狠，直接将其中的内容直接强行不经过Vue渲染直接输出，`{{}}`该咋样就咋样，不仅可以节省Vue加载速度，这也可以防止一些奇怪的注入获取我们创建的Vue实例（当然不知道有没有用）

#### 自定义指令

我们如果发现Vue内置的指令并不能满足我们的需求，此时就需要自定义指令了

我们可以直接在Vue实例创建时添加上配置项`directives`，之后直接写上自定义指令的名称（`v-[指令名]`）定义的函数，并在函数中指定内容即可，下面是简单的案例

```vue
<body>
    <div id="root">
        <span v-test="msg"></span>
    </div>
</body>
<script>
    Vue.config.productionTip = false
    new Vue({
        el: '#root',
        data: {
            msg: 1000
        },
        directives: {
            test(element, binding) {
                // 其中element是使用这个指令的标签信息，binding是传入data属性的各种属性
                // 自定义指令中，不得不涉及DOM操作指令
                console.log(element, binding)
                element.innerText = binding.value * 10
            }
        }
    })
</script>
```

控制台显示

![image-20220315122725531](https://s2.loli.net/2022/03/15/n2kGCcBeMEvdJqI.png)

综上，指令的自定义就需要拿着指令返回给我们的真实DOM元素进行修改，并且我们还需要注意每一次当模版发生解析的时候（不一定是指令控制的数据发生改变），所有的指令都会被调用一次，确保界面展示的正确性

除此之外，上面这个函数其实和计算属性中的内容一样也是简写形式，完整的写法每一个自定义指令其实都是一个对象，结构如下

```
directives:{
	test:{
		bind(){}
		inserted(){}
		updated(){}
	}
}
```

其中我们知道其实我们页面上的标签只要打上了Vue的某个指令，实际上在页面展示这个标签之前都会前经过一次Vue解析，然后才在DOM中添加解析之后的内容，但是细分开来其实还有不少细节，而这三个函数第一个`bind`就是将页面标签交由Vue解析的时候执行的，`inserted`就是在解析之后将要插入页面的时候执行的（比如可以在`isnerted`里获取到该标签的父标签，而`bind`里就获取不到），`update`则是在模版被重新解析的时候执行的（第一次展示时不执行）

这三个函数都有上面所说的两个参数，我们可以对其修改DOM并根据需求进行自定义

而简写方式就是将我们写的DOM操作内容复制到`bind`和`update`两个函数中

> 注意指令名多个单词的时候，单词之间用`-`分隔，同时在定义时要在整个单词外加引号，同时自定义指令也和过滤器一样，可以在全局配置`Vue.directive`，用法大差不差

### 生命周期

学习一项技术最重要的内容就是了解这个框架或应用的生命周期，它何时产生，何时运行，何时终止，我们在自定义指令的时候已经关注到了指令执行时所在阶段的重要性，在创建Vue实例的时候，Vue实例也为我们提供了标识Vue工作不同阶段开始或结束时的函数供我们使用，默认函数都不存在内容，但是我们可以根据我们自己的需求，在不同时间点执行不同的操作

这么多的时间点函数就是Vue的生命周期回调函数（生命周期钩子）

所有的函数我们可以在官网看到，但我们放一张网上的中文的解析图

![img](https://www.icode9.com/i/ll/?i=20200709180519923.png?,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0Nhb19NYXJ5,size_16,color_FFFFFF,t_70)

其中红框白底的内容就是Vue为我们提供的生命周期函数

看着似乎不太好理解，我们可以做个案例试验一下

```vue
<body>
    <div id="root">
        <h2>{{n}}</h2>
        <button @click="addN">n++</button>
        <button @click="destroyV">destory</button>
    </div>
</body>
<script>
    Vue.config.productionTip = false
    new Vue({
        el: '#root',
        data: {
            n: 1
        },
        methods: {
            addN() {
                this.n++
            },
            destroyV() {
                this.$destroy()
            }
        },
        beforeCreate() {
            // 此时只有一个Vue实例，里面的_data和method属性等我们指定的初始化属性都还没出来，数据代理未开始
            console.log('beforeCreate:', this._data)
        },
        created() {
            // 开启数据监测和数据代理，Vue实例的内容终于完整了
            console.log('create:', this._data)
        },
        beforeMount() {
            // 虚拟DOM已经生成了，但是还没来得及将其放到页面上
            console.log('beforeMount:页面显示{{n}}而不是1')
        },
        mounted() {
            // 初始化结束，页面正常显示，也就是我们不做任何操作时页面展示的内容，其中当前页面的DOM信息存在vm.$el中
            console.log('mounted')
        },
        beforeUpdate() {
            // data被修改了，但是页面上的真实DOM还没更新
            console.log('beforeUpdate:页面显示n=1但是实例中n=', this.n)
        },
        updated() {
            // 更新完成
            console.log('updated')
        },
        beforeDestroy() {
            // vm.$destroy被调用的时候调用，一般会清空一下一生加载或订阅的内容，料理后事
            console.log('beforeDestroy:', this)
        },
        destroyed() {
            // 已经死完了，但是注意给比如某个按钮绑定的事件还在（但是自定义事件不在了），addN会执行，但是页面上内容不更新
            console.log('destroyed:', this)  // 好像也能输出实例，但是实际上已经不作用了
        },
    })
</script>
```

![image-20220315185623768](https://s2.loli.net/2022/03/15/zApDrxXFtQ17JBH.png)

可以发现，生命周期都是成对出现的，每一个时刻都分为进行之前和之后，其中某些函数是之后常用的，之后也会介绍到

## 组件化编程

组件化编程就是将完整的页面进行拆分，拆分成不同的几大块，之后先把每一大块进行封装，再将其中更细分的内容进行进一步拆分并封装，其中封装内容包括但不限于CSS/html/js/ttf等资源，保证每一块无论是大块还是小块都可以在下一页面中被完全的复用

### 非单文件组件

#### 简单的组件添加和使用

创建一个组件和我们之前`new Vue()`的操作十分类似，此时只需要调用`Vue.extend()`即可创建一个组件，不过需要注意的是我们不应该在组件中为其添加`el`属性，因为这个组件到底是给谁用的是由之后创建的Vue实例指定

同时data属性不能再和之前一样写成对象了，必须写成一个函数形式，因为对象被多变量引用时并不会创建多个不同实例，而函数的返回值永远是全新的新的对象，不用担心耦合的问题

而由于我们的组件没有指定`el`，因此我们肯定不能直接拿来用，此时第二步我们就需要将其添加到我们创建的Vue实例中，在创建实例的过程中，只需要添加`components`指令即可

```Vue
new Vue({
	el:...,
	components:{
		[组件名(随便取)]:[接收了Vue.extend的对象名],
		...
	}
})
```

第三步就是添加组件标签，直接在界面上添加组件名所指定的标签即可，比如以下这样的案例

```html
<body>
    <div id="root">
        <comp1></comp1>
        <br> <!-- 普通标签结构不用修改 -->
        <comp2></comp2>
    </div>
</body>
<script>
    Vue.config.productionTip = false
    const comp1 = Vue.extend({
        template: `
            <h2>{{name}}</h2>
        `,
        data() {
            return {
                name: '组件1'
            }
        },
    })
    const comp2 = Vue.extend({
        template: `
            <h2>{{name}}</h2>
        `,
        data() {
            return {
                name: '组件2'
            }
        },
    })
    new Vue({
        el: '#root',
        components: {
            comp1,  // 等于comp1: comp1
            comp2
        }
    })
</script>
```

> 其中`template`可以代替`el`属性，组件会直接像解析原本`div#root`一样解析`template`里面的标签

在开发者调试工具中，我们也可以看到组件的身影

![image-20220316182103596](https://s2.loli.net/2022/03/16/CWxEuzPfRjiBsH7.png)

同时即使我们在页面上添加了多个组件标签，各个组件之间也是隔离的关系，数据的改变并不会互相造成影响，即实现了复用，又简洁美观使用性强

但是这个文件还是存在很多问题，比如我们在单文件中创建了多个组件，但是在实际开发中实际上一个文件内仅有一个组件，同时我们还要将创建的Vue实例扩展到全局，这些内容在接下来的学习中都会涉及

#### 一些注意点

- 组件名（即在Vue实例中注册的名），当为单个单词时，Vue推荐我们当使用大写开头的单词，多个单词则使用小写字母开头+`-`连接，比如`my-name`等，要注意的是大驼峰命名法会让Vue无法识别内容报错，不过之后学习脚手架环境之后会对这种错误进行修正
- 组件名也不能和html原有的标签名重名，不然也会报错
- 页面上的组件标签支持自闭合，但是最好是在脚手架环境下，不然会出奇怪问题
- 可以省略`Vue.extend`，直接`const [名] = {}`之后在实例中注册即可
- 除此之外组件之间也可以嵌套，也只需要在组件内添加`components`即可，不过这样需要在父组件的`template`属性里编写`<[子组件]>`标签
- 在非单文件组件的编写中，需要将子组件定义在父组件之前
- 在一般的开发中我们一般会开发一个`app`组件，由它而不是Vue实例管理所有组件，而这样Vue实例（root组件）就只需要管理`app`一个组件了

### VueComponent

如果我们在上面通过`console.log(comp1)`那么我们会看到在控制台输出了一个名叫`VueComponent`对象，那这个东西到底是什么呢？我们好像也没有通过`new`创建这个函数啊？

实际上当我们在页面中添加组件的标签时，Vue就会调用`new`一次这个对象，也就是说，页面上引用了多少次组件标签，就会生成多少个`VueComponent`对象

而我们的`extend`方法实际上是调用了一下这个对象的构造函数`this._init`之后就返回给变量`comp1`了，而不是直接new出来给变量

因此在调用`extend`的时候其中的`this`也就是`VueComponent`对象了，只不过这个对象如果我们通过控制台输出会发现它和`new Vue`出来的内部结构长得基本一模一样

> 之后就把`VueComponent`创建的**组件实例**称为vc了，我们创建的Vue**根实例**则理所当然叫做vm了，我们发现对于vc我们往往会对其命名，但是vm我们一般就不拿变量去接收它了，这也是组件所必须的

#### 构造方法和原型对象

我们首先得弥补一下之前欠下的JavaScript的债，好好讲一讲函数这个东西和类这个东西在其中的区别和联系

我们之前只是提了一下原型和原型链的概念，但是如果不巧碰到了以下代码

```javascript
function Test(name) {
    this.name = name
    console.log("构造方法")
}
let test = new Test("123")
```

常识来说，Test应该是一个函数，而常识又告诉我们，函数是不可能被`new`出来一个对象的，更不可能在函数内存在什么`this`之类的，但是JavaScript显然不信这个邪，就是要反其道而行之

于是我们打算换一种角度思考，盯着它看了一会儿，我们发现这个函数的内容怎么这么像一个构造函数，这么一想好像突然有点道理，但是执行这个构造函数的类跑到哪里去了呢

这时候`prototype`属性隆重登场，如果我们在控制台输出这个函数的信息（注意要用`console.dir`），那么我们会发现这个函数像一个类一样拥有好多属性

![image-20220317230340960](https://s2.loli.net/2022/03/17/v5YNVoZTtEXngxS.png)

这个函数居然真的像一个类一样被我们输出出来了，同时它的`prototype`正指向他所服务的那个类，为了验证这个假设，我们输出我们`new`出来的实例

![image-20220317231222449](https://s2.loli.net/2022/03/17/x5HqQoXrCJNGyuh.png)

这下我们明白了，这个函数的的确确是某个类的构造函数，于是我们就把定义函数时自动那个创建的这个类叫做原型对象，而这个函数即为构造函数，`new`出来的内容叫做实例

当然我们会发现每一个输出的类都有一个`[[prototype]]`的方法，看似和之前的`prototype`很像，但是它的功能唯一且任何对象上都有（`prototype`只有定义构造函数的时候会出现），就是指向其原型对象，无论是实例还是构造函数都一样，而如果本身就是原型对象那就指向更高层次的原型对象，直到最终的`Object`

![img](https://pic2.zhimg.com/80/v2-c4fad77a39802a292c71792559d7ea99_720w.jpg)

#### 内置关系

介绍完了这些知识，我们再回过头来看看`VueComponent`和`Vue`的关系就一目了然了

接下来我只需要给出一张图，估计就能领会其中的意思

![image-20220317232421156](https://s2.loli.net/2022/03/17/FWLK7owQZXjyksp.png)

这样我们就搞清了这vm和vc之间到底是什么牛马关系，进一步为我们巩固了构造函数，原型对象，实例之间的关系

### 单文件组件

接下来我们就需要写一些`.vue`文件了，但是显然浏览器并不会自动帮我们解析这种类型的文件，这时候就需要我们借助别人提供的工具对`.vue`进行编译组装成浏览器看的懂的内容（HTML、CSS、JS等）

而这工具就叫做脚手架

不过在此之前我们先要了解一下`.vue`文件中应该怎么写代码

#### 目录结构

首先我们需要创建几个`[组件].vue`，文件名称就应该就是你组件注册的名字，采用大驼峰命名法，这么一来就和Java类的创建和命名方式非常类似

```vue
// Demo.vue
<template>
	<!-- 组件的html结构写在这 -->
	<div class=".demo">
		<h1>{{name}}</h1>
	</div>
</template>

<script>
	// 组件交互相关方法比如data和method方法
	// export default是默认暴露
	export default { // 简略形式，简略了const vc = Vue.extend{...}，和最后的export default vc
		name: 'Demo1',  //最好写一下组件的名字
		data() {
			return {
				name: '单组件测试'
			}
		}
		// .methods等等
	};
</script>

<style>
	/* CSS样式 */
	.demo {
		background-color: orange;
	}
</style>
```

创建好了一个组件，下一步就是创建所有组件的管理者，`App.vue`

```vue
// App.vue
<template>
	<div>
		<Demo1 />
	</div>
</template>

<script>
	// 汇总所有的组件
	// 引入
	import Demo1 from "./Demo1.vue";
	export default {
		name: "App",
		// 注册
		components: {
			Demo1,
		},
	};
</script>

<style>
</style>
```

仅有组件肯定是不行的，还有个老大哥没有定义，他就是vm，因此下一步就是创建一个`main.js`文件，来创建一个vm

```js
// main.js
import App from './App.vue';

new Vue({
	template: '<App></App>',
	components: { App }
})
```

当然这样我们仅有组件和vm并不能使页面进行运行，更不能通过浏览器访问，因为没有结构网页可不管那么多，他只会执行`.html`文件，因此下一步就是创建一个html文件

```html
<!--index.html-->
<!DOCTYPE html>
<html lang="en">

<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>单文件组件</title>
</head>

<body>
	<script src="../js/vue.js"></script>
	<script src="./main.js"></script>
</body>

</html>
```

这样我们Vue项目的基础就完成了，当然由于没有脚手架，因此这么四个文件还是不能运行的，这时候就需要我们先安装一下脚手架再说了！

## 脚手架

脚手架到底是什么牛马，其实他是Vue提供的标准化开发工具，我们需要通过npm安装它

### 安装

1. 先下载一个npm，可以网上搜一搜先安装一个Node.js（最好，指不定直接装npm就和我一样乱报错），要确认npm可以使用
2. `npm config set registry https://registry.npm.taobao.org`，设置国内镜像源
3. `sudo npm install -g @vue/cli`，如果是Windows下可能要开管理员模式
4. 跑到桌面上，确定需要在此处生成一个Vue文件，则运行`sudo vue create [项目名]`，接着选择Vue版本构建项目即可
5. 之后会在指定位置生成一个项目名的文件夹，我们先不急打开它，接下来注意我们现在创建的文件夹所有者好象是root，我们把它改成我们自己`sudo chown chillyblaze:chillyblaze vue_test/**`
6. 接着进入文件夹，执行`npm run serve`即可开启Vue项目
7. 打开网站查看效果

> 如果你像我一样发现不知道为什么下载内容跑不动或者报了什么错，这时候我们就需要检查是否已经正确设置镜像库，检查是否设置了代理，检查缓存是否清空等等，可以用如下指令`npm config get registry proxy`查看仓库和代理，接着`npm cache clean --force `清理缓存，这还不行就重启电脑，我反正是重启之后就好了

### 内部结构

看完了网站效果，这时候我们就需要通过代码编辑器打开这个文件夹，我们首先了解一下其中的项目结构

![image-20220318223943885](https://s2.loli.net/2022/03/18/nzTmJOb7HsKVAUi.png)

我们扫一扫src下面的组件内容，好像和我们之前自己写的东西都差不多，但是我们还是发现了一个我们不熟悉的东西

```js
import Vue from 'vue'
import App from './App.vue'

Vue.config.productionTip = false

new Vue({
	render: h => h(App),
}).$mount('#app')

```

这个render是什么东西啊，这个东西我们之后会详细说明，此处我们只需要了解到这个指令让我们的App组件被放入到了vm中即可，可以暂时约等于`component`的效果

### 运行项目

接下来我们只需要把之前写完的组件**（仅`.vue`组件！）**直接拷到相应的src目录下即可运行，且在修改之后只需要保存一下Vue就会帮我们自动重新构建项目展示

接下来的项目结构是这样的

![image-20220318225928605](https://s2.loli.net/2022/03/18/6o7lw9SLpKIgrkv.png)

同时注意要在`App.vue`里面修改一下组件的路径，注意到`App.vue`组件在components文件夹之外

> 但是如果像上面那样做之后你重启服务，可能就会被报一个错了
>
> ![image-20220318230135768](https://s2.loli.net/2022/03/18/shcgjz3LKQvSZ7I.png)
>
> 这牛马东西居然不认我们的Demo单个单词组成的组件！简直是无法无天，我们需要直接在`vue.config.js`里面把这个垃圾语法判定给他关了
>
> ![image-20220318230329454](https://s2.loli.net/2022/03/18/yIuqPLWFSaT4CXl.png)
>
> 之后再次执行即可成功运行，除非你之前代码写错了

### render配置项

上面已经提过，render配置项让我们看不太懂，而且我们发现我们自己写的`main.js`好像也就和他给出的差了一个这个render，那么我们不妨就将我们自己的`main.js`拷进来执行看看到底会发生什么

![image-20220319211348031](https://s2.loli.net/2022/03/19/m52uvgZqbTXia9y.png)

很可惜，启动的时候报了一个错误，这个错误好像说的是我们什么导入的Vue包不包含叫什么`compiler`的编译器，所以没有办法解析模版`template`，这时候我们如果打开点进头部包含的vue包里面，会发现这个包深藏在一大堆`node_module`里面，而我们如果看到`vue`目录下的`package.json`我们会发现有一条`  "module": "dist/vue.runtime.esm.js"`语句，而它指定了当我们仅引入vue包的时候它默认引用的就是这个`runtime`包，而这个包中正巧没有我们解析`template`所用的解析器

终于知道了原来不能在创建vm的时候使用`el`或者和`template`有关的属性，而这时候允许我们使用的就是这个render函数了，它的原本样子长得是这个样子

```vue
render(h){
	return h(App)
}
```

经过简化就变成了我们所见到的这个模样，其中`h`参数原本的名字叫做`createElement`，这个函数的作用就是给我们创建一个页面标签元素，比如我们`h('h1','test')`就可以创建一个`<h1>test</h1>`

render函数还是比较简单的，之后我们除了在`main.js`里面用一下之外一般也不会在别的地方用到了

### 默认配置

我们可以通过`vue inspect > [输出文件].js`来将vue的所有配置内容输出到文件中

我们可以看到很多乱七八糟的属性，如果真的要改配置，我们就需要在目录下的`vue.config.js`里面修改所需要修改的默认属性，而什么东西可以修改，我们可以在[官网上](https://cli.vuejs.org/zh/config/)查找

但是默认的配置也挺好的，尽量不要改吧。。

## 各种特性

接下来我们介绍一些当前阶段常用的杂项内容，涉及到了各个方面的重要的新知识

### ref属性

当我们想要拿到某个标签时，我们往往会给他打上一个id，之后我们在其他地方通过`document.getElementById()`来获得DOM内容，但是手动操作DOM显然是不理想的，Vue提供了`ref`代替频繁设置`id`供我们使用，同时其中的标签内容都会存在当前vc下的`$refs`属性中

还有一个优点就是当我们把`ref`属性打在组件标签上时，我们还得到这个组件标签的vc实例内容，在之后的组件通信中有大用

```vue
<template>
	<div>
		<h1 ref="title">测试ref</h1>
		<Demo ref="demo" />
		<button @click="showref">点我展示ref</button>
	</div>
</template>

<script>
	import Demo from "./components/Demo.vue";
	export default {
		name: "App",
		components: {
			Demo,
		},
		methods: {
			showref() {
				console.log(this.$refs);
			},
		},
	};
</script>

<style>
</style>
```

![image-20220319220342671](https://s2.loli.net/2022/03/19/6LzgpAWUfT8tFKc.png)

### props配置

我们可能发现了，当我们在比如App组件当中引入多个子组件的时候，好像子组件的内容都是一样的？既然内容都一样那我们引入多个的意义是什么呢？假如某两个组件之间仅有数据不一致，难道我们还需要重新写一遍组件吗？那Vue高复用性的优点又如何体现呢？

这时候就需要`props`属性隆重登场，我们只需要通过在组件标签中传入我们需要的内容，之后在子组件内引入`props`属性，最后即可正常展示内容了

- `Demo.vue`

  ```vue
  <template>
  	<div class="demo">
  		<h1>{{ name }}</h1>
  		<h2>{{ age }}</h2>
  		<h2>{{ sex }}</h2>
  	</div>
  </template>
  
  <script>
  	export default {
  		name: "Demo",
  		data() {
  			return {
  				name: "张三",
  			};
  		},
  		props: ["age", "sex"], // 最简单写法
  		// props:{
  		// 	age:Number,  // 指定传入类型，不然控制台会报错
  		// 	sex:String
  		// },  // 稍微复杂一点写法
  		// props:{
  		// 	age:{
  		// 		type:Number,
  		// 		required:true  // 这个参数是必须的，不然控制台会报错
  		// 	},
  		// 	sex:{
  		// 		type:String,
  		// 		default:"男"  // 不传入的话默认值
  		// 	}
  		// }  // 最完整写法
  	};
  </script>
  ```

- `App.vue`

  ```VUE
  <template>
  	<div>
  		<Demo :age="10" :sex="'男'" />
  	</div>
  </template>
  
  <script>
  	import Demo from "./components/Demo.vue";
  	export default {
  		name: "App",
  		components: {
  			Demo,
  		}
  	};
  </script>
  ```

> 注意其中传入的标签属性最好在之前加上比如上述这样的`:age`，根据`v-bind`的特性，这样后面引号内的内容就会被当作js表达式执行，之后如果我们传入为数字就可以在子组件中被正常识别为数字，如果单`age="18"`子组件只会认为是字符串18

当然这其中还有一些底层的注意点

- 传入的参数在子组件的vc实例中只作为属性存在，并不会跑到`_data`里面去，这也意味着传入的这个参数和data中指定的组件属性还是有一定的区别的
- 传入组件的属性不允许在组件内部再进行修改了，虽然我们在组件内通过`this.[参数名]`访问，但是Vue并不推荐我们去修改它，如果我们真的需要修改，请在`data`中指定一个属性`[属性名]:this.[传入参数名]`这样将传入的参数交给`data`处理，就可以正常通过比如`methods`修改了
- 如果在`data`中存在和`props`指定的参数同名，`props`的优先级更高，`data`是什么牛马
- 注意在传值的时候我们不能使用Vue自带的标记了，比如`key`、`ref`等等

同时注意`props`不仅解决的是多数据在不同组件之间的重用问题，更重要的是它还能解决父子组件之间的通信问题，它不仅可以父组件给子组件传数据，甚至可以在父组件中定义一个方法传给子组件，之后子组件通过调用父组件传给它的方法，来调用父组件的方法，控制父组件的数据内容发生改变，特别注意无论是传值还是方法，都像是在子组件里面打开了一个快捷方式，最终的数据和方法存储位置还是父组件，因此这也进一步说明了为什么不建议在子组件中改变父组件传过来的参数内容了

### mixin混入配置

如果说上面的`props`是在高复用的前提下添加个性化，那么`mixin`就是在本就高组件话的基础上进一步提高复用效率，比如你的`Worker`组件和`Student`组件都有一段代码叫做

```vue
methods:{
	showName(){
		alert(this.name);
	}
}
```

难道我们需要在两个组件中都写一遍吗，这时候就可以使用mixin，我们可以先在Vue项目中创建一个`mixin.js`，里面写上如下内容

```js
export const mixin1 = {
    methods:{
        showName(){
			alert(this.name);
		}
    }
}  // 分别暴露
```

这时候我们就可以在Student组件中添加

```vue
<script>
	import { mixin1 } from "./mixin";
	export default {
		name: "Student",
		data() {
			console.log(this);
			return {
				name: "张三",
			};
		},
		mixins: [mixin1],
	};
</script>
```

当然使用的过程中同样有一些注意点

- 当混入内容`mixin`与原本定义的属性存在重复时，会进行合并（比如在已有`data`段的时候`mixin`内还存在`data`段），而当`data`内的属性存在重复时，优先忽略`mixin`内的
- 当遇到重复的生命周期钩子函数时，内部的内容都会执行，同时以`mixin`内的先执行
- 同时我们还可以在`main.js`中通过`Vue.mixin({...})`定义全局混入

### 插件

解决完了复用性，我们还需要解决耦合性，回顾我们之前学习过的某些指令，比如`Vue.mixin`、`Vue.filter`、`Vue.directive`等等全局的方法，这些方法往往都需要占用不少的代码空间，而且由于我们的Vue实例对象仅在`main.js`里面创建，因此我们这些代码难道只能一大堆放在`main.js`里面吗？

不，这时候我们就需要使用插件技术，我们只需要创建一个`plugin.js`，像是这么一写

```js
export default {
    install(Vue){
        Vue.directive...,
        Vue.filter...,
    }
}
```

紧接着我们只需要在`main.js`里面引入内容`import plugin from './plugin'`，之后在后面轻轻的引入一个`Vue.use(plugin)`即可完成所有配置的导入

比如我们在`Vue.prototype`上添加了一个方法，那么我们在全局的vm和vc上都能使用了，对于某些效果来说简直不要太方便

这同样便利了第三方插件的提供商，我们只需要简单的`use`一下，被人配置好的所有的插件内容都可以即时使用了

同时我们在`main.js`里面调用插件的时候，我们甚至能够往插件内再传入参数，之后插件内对我们传入的参数进行接收，从而做出相应的个性化反应

### scoped样式

当我们在不同组件内写了名字一样的样式时，如果我们在页面中引入了这个样式，我们可能会发现所有的样式都变成了某一个组件中定义的样式了（按照`main.js`中加载的顺序），这显然不是我们想要看到的，假如我们团队中有一大堆人开发组件，难道每一个样式还需要先统一注册避免冲突吗？

此时我们就需要在样式标签中添加`scoped`属性，这样里面写的样式就只属于这一个组件了

![image-20220319233721368](https://s2.loli.net/2022/03/19/xW6igbtfoeFG7Yw.png)

![image-20220319233745047](https://s2.loli.net/2022/03/19/LhPQk7NeTXVsbxE.png)

这样我们就可以愉快的在里面写代码了

### $nextTick

我们都知道，当想让页面上的input输入框获取焦点，页面上必须要有一个输入框才行，也就是说如果我们在`methods`某个函数内直接比如`this.$refs.inputT.focus()`是没用的，因为此时页面内容还在虚拟DOM里，自然没办法获取焦点，此时我们就可以在前面加一个`this.$nextTick(()=>{this.$refs.inputT.focus()})`即可让Vue在将虚拟DOM放到页面上之后再执行内部的代码

### 过度与动画

除了我们自己在CSS上写一些动画效果，Vue还内置提供了使用动画效果的方式

#### 动画组成

一般的动画都分为入场动画和离开动画，于是Vue内置了自动调用这两个动画效果的`transition`标签，只需要将其包裹所要执行动画效果的标签即可

同时Vue也内置了三种调用动画效果的方式，请看下面范例

```vue
<template>
	<div class="demo">
		<button @click="isShow = !isShow">animate</button>
		<!-- name指定需要调用哪一个样式，如果不指定就会去找v-enter/v-leave -->
		<!-- appear指定在第一次加载标签时便执行动画效果 -->
		<transition name="test" appear>
			<h1 v-show="isShow">这是一个动画</h1>
		</transition>
	</div>
</template>

<script>
	export default {
		name: "Demo",
		data() {
			return {
				isShow: true,
			};
		},
	};
</script>

<style scoped>
	/* 第一种方式:动画实现 对整个过程直接调用进场动画*/
	/* h1 {
				background-color: skyblue;
			}
			.test-enter-active {
				animation: anim 0.5s cubic-bezier(0.075, 0.82, 0.165, 1);
			}
			.test-leave-active {
				animation: anim 0.5s cubic-bezier(0.075, 0.82, 0.165, 1) reverse;
			}
			@keyframes anim {
				from {
					transform: translateX(-100%);
				}
				to {
					transform: translateX(0);
				}
			} */
	/* 第二种方式:过度实现 对起末位置进行指定并额外指定动画过程*/
	h1 {
		background-color: skyblue;
		transition: 0.5s cubic-bezier(0.075, 0.82, 0.165, 1);
	}
	/* 上方也可改成 */
	/* .test-enter-active,.test-leave-active{
			transition: 0.5s cubic-bezier(0.075, 0.82, 0.165, 1);
		} */
	.test-enter,
	.test-leave-to {
		transform: translateX(-100%);
	}
	.test-enter-to,
	.test-leave {
		transform: translateX(0);
	}
</style>
```

> 同时如果像一下子让一堆标签都共用一个动画样式，则可以通过`<transition-group>`包裹，不过注意内部元素必须包含`key`值，或者通过`v-for`枚举

而第三种方式便是直接在标签中指定动画样式的类名，不过一般用于引入第三方动画库 的动画效果时使用

#### 集成第三方

当然我们自己写的肯定没有别人写的动画效果好，我们可以直接下载别人写好的动画库进行引用使用

首先选择一个第三方动画库，这里以`animate.css`做范例

1. `npm install animate.css`

2. 进入[官网](https://animate.style/)找一个自己喜欢的样式

3. 在上面案例的`transition`标签中写入

   ```html
   		<transition
   			name="animate__animated animate__bounce"
   			enter-active-class="animate__bounceIn"
   			leave-active-class="animate__bounceOut"
   			appear
   		>
   			<h1 v-show="isShow">这是一个动画</h1>
   		</transition>
   ```

   即可

### Ajax请求

在前端的开发中，常常会遇到需要通过Ajax的方式请求其他服务器的资源并返回显示在页面上，Vue自身并不拥有模拟发送请求的功能，因此我们需要借助第三方库帮助我们发送请求获取数据

#### 简单获取请求

我们可以借助`axios`库来实现请求功能，直接`sudo npm i axios`即可

让我们借助github的开放api实现一个查询用户的案例

```vue
<template>
	<div>
		<input
			type="text"
			v-model="keyWord"
			placeholder="请输入需要翻译的词语"
			@keydown.enter="sendInfo"
		/>
	</div>
</template>

<script>
	import axios from "axios";
	export default {
		name: "Translate",
		data() {
			return {
				keyWord: "",
			};
		},
		methods: {
			sendInfo() {
				axios
					.get(
						`https://api.github.com/search/users?q=${this.keyWord}`
					)
					.then(
						(Response) => {
							console.log(Response.data);
						},
						(Error) => {
							console.log(Error.message);
						}
					);
			},
		},
	};
</script>
```

还是十分简单的，但是现实当中的情况并不如此顺利，可能你会遇到这样的报错

![image-20220322203028265](https://s2.loli.net/2022/03/22/ShMw1sYvXpBlGcF.png)

总之就是会出现`CORS policy`的错误，这其实就是因为Ajax请求的资源必须满足同源关系，当外来的内容与本机并不同源并且还在响应头中没有包含`cors`的头信息，那么浏览器会拒收返回的内容，自然也不能被我们获取到了

当然这仅限于Ajax，如果我们可以找一个代理服务器，帮助我们通过正常的http请求到我们所需要的资源，并返回给我们，那我们岂不是就可以获取到本获取不到的内容了吗

#### Vue设置代理

虽然Vue没有内置请求模块，但是却为我们提供了代理服务

我们只需要在`vue.config.js`中设置一下代理即可

```js
module.exports = defineConfig({
	transpileDependencies: true,
	lintOnSave: false,
	devServer: {
		proxy: {
			'/test': {
				target: 'http://translate.google.cn',
				pathRewrite: { '^/test': '' }
			}
		}
	}
})

```

其中通过pathRewirte来重写请求路径并将剩下结果拼接到目标路径后，请求之后再返回结果给我们的组件内容

之后我们只需要在组件内修改前缀`http://localhost:8080/translate_a/single?client=at&sl=en&tl=zh-CN&dt=t&q=${this.keyWord}`即可

### 组件事件

#### 浏览器本地存储

我们可以通过`localStorage.setItem('[key]','[value]')`来设置本地存储值，接着接着我们可以在浏览器的检查元素中的`Application`中看到我们设定的键值对

> 注意我们设定的`value`和`key`都必须是字符串，如果不是字符串类型那么它就会给你调用`tostring`方法，因此如果我们需要在用户本地存一个对象，就需要调用`JSON.stringify()`方法

除此之外，`localStorage`的`getItem`和`removeItem`和`clear`可以对存储的内容进行读取，删除，清空操作，同时如果读取到的是一个对象记得调用`JSON.parse`方法

除此之外我们还可以将`localStorage`改成`sessionStorage`，此时设定的就是当前会话临时创建的本地缓存，当浏览器关闭的时候会自动消失

> 当然这两个对象都是在`Window`里面的，但是由于ES6的特性可以省略`Window.`

#### 自定义事件

之前我们说到的自定义指令是与标签相关的，涉及到DOM元素的操作，而现在我们需要学习自定义事件，也就是`v-on`绑定的标签属性，我们可以直接在**子组件标签**上通过`@[自定义事件名]`来绑定自定义事件

注意，当我们为一个子组件添加自定义事件时，这个自定义事件就会被添加到子组件实例的vc身上，此时我们可以在**子组件内**通过`this.$emit('[自定义事件名]',[参数])`的方式触发这个事件

比如我们想要实现一个一点击按钮，就让子组件将自己的信息传给父组件，当然我们可以通过`props`将父组件的一个方法传给子组件，但是我们也可以通过自定义事件实现

```vue
// 父组件
<template>
	<div>
		<Demo @eventN="getDemoName" />
	</div>
</template>

<script>
	import Demo from "./components/Demo.vue";
	export default {
		name: "App",
		components: {
			Demo,
		},
		methods: {
			getDemoName(name) {
				console.log(name);
			},
		},
	};
</script>
```

```vue
// 子组件
<template>
	<div class="demo">
		<h1>{{ name }}</h1>
		<button @click="sendName()">click me and send name to App component</button>
	</div>
</template>

<script>
	export default {
		name: "Demo",
		data() {
			return {
				name: "张三",
			};
		},
		methods: {
			sendName() {
				this.$emit("eventN", this.name);
			},
		},
	};
</script>
```

同时当事件不使用之后我们还可以通过`this.$off()`，解绑所有事件，如果只想解绑某一个事件，可以通过数组`[自定义事件1,自定义事件2]`并传入`off`函数指定解绑

> 同时补充一个生命周期的知识，当一个组件实例或者是vm实例被销毁的时候，实例身上的所有自定义事件会被销毁，但是普通交互标签身上的固定比如`@click`事件不受影响

当然我们如果真的想在子组件上使用预先定义好的事件比如`@click`那么也不是不能用，我们只需要通过加上`@click.native`即可正常使用原生事件

以后对于子组件给父组件传递信息最好还是使用自定义事件，通过`props`让父组件给子组件传递一个方法之后子组件再调用实在是有点膈应了

#### 全局事件总线

上面我们已经将父子之间的通信关系介绍清楚了，那么两个兄弟之间通信用什么办法呢？这时候就需要使用全局事件总线的知识了，它理论上可以让任意的两个组件进行通信

此时我们已经学习过了自定义事件的创建，这时我们可以设想一个场景，由于我们知道我们自定义的事件是绑定在vc实例身上的，同时我们可以通过在实例内启动这个事件来让带有这个标签的父组件接收到事件被启动的信息

那么我们有没有一种方法，可以创建一个所有vc实例都可以访问到的组件，然后在一个组件内往这个组件上绑定自定义事件，再由另外一个组件调用这个事件并传递一些信息，接着绑定这个事件的组件通过接收这个事件是否启用并且使用时携带的信息，达到组件之间通信的要求呢？

我们之前介绍过，所有组件的原型都是vm，也就是所有vc实例都可以访问到vm原型对象，更巧的是，当我们输出vm原型对象的属性时（`Vue.prototype`），我们惊讶的发现这个对象上居然有`$emit`属性，也就是说咱们上一回说到的事件触发函数并不是在vc身上的，而是在vm身上的

那么根据上面的猜想，我们只需要在vm身上绑一个事件，就可以在任何一个vc身上查询并触发这个事件了！

##### $on

当然我们现有的方法是通过直接在标签上设定`@[事件名]`来开启一个事件，然而这种方法显然是对vm不奏效的，因为它根本不是一个组件，更不要说通过什么牛马标签来实例化它，面对我们遇上的难题，这里介绍另一种不在组件实例化时的标签内绑定事件的方法

我们可以在某个组件内的`mounted`生命周期中调用`this.$on('[自定义事件名]',([触发事件时接收的参数])=>{[触发事件时做的内容]})`，来开启一个自定义事件，而相对应的，这个`$on`函数同样是在Vue原型对象上的，之所以要将这个函数调用放在`mounted`中，还是因为这个函数在vc的生命周期中仅调用一次，且所有内容都加载完毕，正是绑定事件的好时机

而我们要认清的是，组件的自定义事件，从来都是绑定一次，触发多次的原则，而`mounted`钩子完全符合了我们的要求罢了

除此之外，我们也不用在组件标签中写什么`@`事件了，只不过比起那样绑定事件的方便，这种方式更加底层也更加不便罢了

##### 解决问题

就算我们知道了如何在组件内绑定自己的事件，但是问题依旧很多，我们不妨梳理一下某些可能性

1. 无论哪种方式绑定事件，都是在vc**实例化时**调用**Vue原型对象上的`$on`**方法在**自己身上**绑上一个事件，也就是说虽然调的是别人的方法，但是产生的结果却在自己身上，同理，在触发事件时调用**Vue原型对象上的**某个方法`$emit`**为自己**开启事件
2. 既然谁调用的方法自定义事件就在谁身上，那么我们直接找到Vue原型对象给他绑一个事件不就完了？但显然这又是理解不够透彻，任何原型对象我们都是无法直接拿到的，况且以往绑事件都是在创建实例时调用的`$on`方法，那能够直接原型对象调用自己的方法给自己绑事件？
3. 就算我们拿到了Vue原型对象，同样还有问题，Vue早就已经实例化完了，我们根本找不到任何一个函数或者是方法能让其唯一的绑定一个事件，而就算给Vue实例绑定了一个事件，但是他是实例啊，我们在别的组件中又怎么调用这个**实例**的方法？

综上，整理一下我们当前所掌握的信息

- 无论在哪个组件中，我们都可以调用到Vue**原型对象**上的方法，且是毫无阻碍的
- 除了在自己组件内，我们无法在任何地方访问到任何组件的**实例化内容**
- 事件是绑定在**实例化后的内容**上的，如果存在某个公共的绑定事件的位置，那么它必须是**实例对象**
- 事件只能在一个实例化对象上绑定一次（意味着必须通过`mounted`），但是能够被多次调用

现在揭晓答案，你会发现这个解决方案完美的符合了上述所有要求，直接贴代码

```js
new Vue({
	el: '#app',
	render: h => h(App),
	beforeCreate() {
		Vue.prototype.$bus = this  // 安装全局事件总线
	},
})
```

我们在Vue的原型对象上增加了一个`$bus`属性，而这个属性又刚好是刚实例化到一半的Vue实例化对象的拷贝，这样，我们就可以在任意组件内，通过`this.$bus`时时刻刻都访问到这个实例化对象（因为本地没有`$bus`属性，就会往外找），同时，我们只需要在组件内的`mounted`函数内，使用`this.$bus.$on`绑定事件即可建立一个全局的自定义事件，在其他组件中`this.$bus.$emit`就可以随时调用这个事件了！

#### 消息订阅和发布

除此之外我们还可以通过第三方库实现组件内的通信，我们只需要在组件内订阅某一个消息，在另一个组件中发布被订阅的某条消息并提供消息内容，订阅消息的组件就可以获得消息的内容了

1. 安装`sudo npm i pubsub-js`
1. 在组件内引用`import pubsub from 'pubsub-js'`
1. 在`mounted`中订阅某条消息`pubsub.subscribe('[消息名]',([消息参数])=>{[接收到消息时执行]})`，注意第一个参数是消息名，因此发布者携带的参数放在第二个接收，同时请设置一个比如`this.pubId`接收`subscribe`函数的返回值id，之后要利用它取消订阅
1. 在其他组件发布消息`pubsub.publish('[消息名]',[携带消息参数])`即可
1. 组件被销毁时记得`pubsub.unsubscribe(this.pubId)`

但是还是使用全局事件总线比较香，毕竟是Vue自带的

### 插槽

当我们需要在不同的容器中添加不同的内容，但是大体上不变时，我们当然可以通过`props`配置通过标签属性传参的方式引入内容，但是如果不同组件实例内的标签结构有所不同呢？我们目前的方法就是在组件内通过比如`v-show`并判断`props`接收到的内容比较并选择性的展示结构内容，但是这种方式一旦组件实例一多就要写一大堆判断，而且毕竟是整个标签结构整个标签结构的置换，全部塞在组件里显然显得不太合适

此时我们就可以借助插槽的功能了

#### 默认插槽

我们之前从没在组件使用标签内添加过别的内容，但是如果想要使用插槽，我们就需要在标签中添加自定义内容

```vue
// 父组件
<template>
	<div>
		<slot-test>
			<span>自定义的插槽功能</span>
		</slot-test>
		<slot-test />
	</div>
</template>

<script>
	import SlotTest from "./components/SlotTest.vue";
	export default {
		name: "App",
		components: {
			SlotTest,
		},
	};
</script>
```

```vue
// 子组件
<template>
	<div>
		<h1>测试插槽功能</h1>
		<slot>默认值</slot>
	</div>
</template>

<script>
	export default {};
</script>

<style>
</style>
```

这样外层的父组件就会自动将内部属性添加到子组件的`slot`标签中了

![image-20220322214546640](https://s2.loli.net/2022/03/22/Sdq4Uky76VMLlwK.png)

#### 具名插槽

非常简单，直接在上面的基础上在子组件中的slot标签中添加`name`属性，并在父组件的标签中添加`slot='[子组件name名]'`即可，这样就可以在子组件中定义多个插槽，在父组件中根据不同插槽的位置添加不同内容

> 注意，Vue推荐我们在使用具名插槽时，在父组件中的不同插值标签外包裹上`<template>`标签，并且支持我们在使用`<template v-slot:[子组件name]>...</template>`（注意不需要加引号，同时前面是冒号）的方式同样实现绑定子组件内的具名插槽，当然也支持简写`#[子组件name]`快速绑定

#### 作用域插槽

现在我们要明确一个概念，插槽就是子组件提供了一个接口，然后给父组件使用，而父组件使用时可以往这个接口里丢不一样的东西，实现个性化

但是！说到底还是父组件在使用这个插入的标签，这个标签的渲染也是在父组件中执行的，但是由于这个标签是给子组件使用的，难免会出现标签内的数据来自于子组件而不是父组件，假设现在子组件中有一个`msg`属性要显示在个别组件实例中的插槽里，这时候就会报错了

```vue
<slot-test>
    <span>自定义的插槽功能,{{ msg }}</span>
</slot-test>
```

![image-20220322220555357](https://s2.loli.net/2022/03/22/NBIqnSiveL1Eabr.png)

这时候就需要用到作用域插槽，我们必须在子组件中将`msg`属性传给父组件，之后才能让父组件使用这个数据

```vue
// 子组件
<template>
	<div>
		<h1>测试插槽功能</h1>
		<slot :msg="msg">默认值</slot>
	</div>
</template>

<script>
	export default {
		name: "SlotTest",
		data() {
			return {
				msg: "hello",
			};
		},
	};
</script>
```

```vue
// 父组件
<template>
	<div>
		<slot-test>
            <!-- 特别注意这里是等于号+引号的v-slot！ -->
            <!-- 传到父组件里被v-slot接收的是一个对象！里面有msg这个属性，这里使用的是ES5的解构赋值-->
			<template v-slot="{ msg }">
				<span>作用域插槽功能,{{ msg }}</span>
			</template>
		</slot-test>
	</div>
</template>
```

在这个案例中我们也了解到`v-slot`在不同形式下的两种用法，它通过冒号指定插槽名称，通过等号指定作用域传来的数据内容，所以正式的`v-slot`用法即为`#[子组件插槽name]='{[子组件传出数据]}'`

```vue
<template #test="{ msg }">
	<span>{{ msg }}</span>
</template>
// 其中子组件
<slot :msg="msg" name="test">默认值</slot>
```

作用域插槽一般用于父组件指定标签结构，子组件提供数据的情况

## Vuex

它是专门在Vue中实现集中式状态管理的一个插件，它可以对Vue应用中多个组件的共享状态进行集中式的管理，同时也是一种组件间通信的方式

假设我们还是使用全局事件总线进行一大堆组件的通信，比如A组件中的某个值其他一大堆组件都需要使用，因此在我们目前看来只能在每一个要使用这个数据的组件内`$on`一个事件，再由A组件`$emit`一下才能实现，但这显然比较麻烦，虽然确实`$bus`谁都能用，但是似乎并没有什么工具对其进行管理，频繁的调用事件效率十分低下，如果我们有另一个类似全局变量池的地方既能帮助我们管理数据，对于每一个独立的组件都能访问这个全局变量池，同时可以实时对其上的数据进行修改等等操作，岂不美哉

这时候，Vuex就出现了

### 原理图

Vuex有三个重要的组成部分，分别是`Actions`、`Mutations`和`State`，我们需要保管的数据交由`State`对象进行保管，而我们需要对保管的数据进行操作时（`dispatch`）我们会先将指令交给`Actions`去检查和整理，接着我们将被`Actions`整理好的数据进行`commit`，然后`Mutations`就会将数据进行操作并更新到`State`中，并对我们页面上的数据重新进行渲染，于是我们只需要在组件内调用Vuex提供给我们的几个api，就可以对Vuex中保管的数据进行操作

![vuex](https://vuex.vuejs.org/vuex.png)

这么一讲好像`Actions`比较多余，确实当我们已知操作的所有内容时直接可以`commit`跳过`Actions`，但是如果我们对数据操作的某个步骤不清楚，需要请求后端时，`Actions`就会自动帮助我们请求后端内容

这样好像组件是用户，`Actions`是服务员，`Mutations`是厨师，`State`是菜，我们当然可以直接叫厨师给我们做饭，但是服务员可以将我们点的菜进行分析并给出建议，同时将我们的菜记录到菜单中，这些都是只会做菜的厨师没办法做到的

同时Vuex的三个组件都是在store大的对象的领导之下的，因此我们在使用api的过程中调用的都是`store.xxx`，这在图中没有体现，需要注意

### 基础使用

首先我们还是先要安装Vuex，`npm install vuex@3.6.2`，因为我们目前还没用到Vue3，因此需要指定版本号，用最新的四点多的版本会出问题

接着在`main.js`里面引入一下，顺便尝试在`store`里面存个值试试

```js
import Vue from 'vue'
import App from './App.vue'
import Vuex from 'vuex';

Vue.config.productionTip = false
Vue.use(Vuex)

new Vue({
	el: '#app',
	render: h => h(App),
	store: 'hello',
})
```

接着我们可以在所有的vc和vm上看到存在一个`$store`属性，并且内部有一个`hello`值

但是这样显然和前面讲过的组成部分一点关系没有，因此我们需要真正创建一个store

### 简单案例

Vuex由于是和Vue同一个团队开发的，因此我们如果需要使用Vuex，正确的做法就是和创建vm一样创建一个Vuex实例

当然Vuex要求我们在创建实例的时候应该提前导入Vuex插件，同时官方也建议我们在创建实例时应该额外创建一个`store/index.js`用以存储Vuex实例

于是我们在根目录下创建一个`store/index.js`，接着在里面写上上面所示的三个内容

```js
// index.js
import Vuex from 'vuex';
import Vue from 'vue';

Vue.use(Vuex)

const actions = {
	// 业务逻辑写在这，写完之后调用commit
	handle(context, value) {
		// 我们在这里还可以通过context.dispatch调用其他处理逻辑
        // 当然我们
		value += "!"
		context.commit('EXEC', value)
	}
}
const mutations = {
	// 对state的操作写在这里，注意函数名最好大写
	EXEC(context, value) {
		// 注意这里不是context.state.x，Vuex直接把整个x都给你了
		context.x.push(value)
	}
}
const state = {
	// 所有全局数据都保存在这，之后在页面中通过this.$store.state.x访问
	x: []
}

export default new Vuex.Store({
	actions,
	mutations,
	state
})
```

```js
// main.js
import Vue from 'vue'
import App from './App.vue'
import store from './store';

Vue.config.productionTip = false

new Vue({
	el: '#app',
	render: h => h(App),
	store,
	beforeCreate() {
		Vue.prototype.$bus = this  // 安装全局事件总线
	},
})
```

```vue
// 父组件,App.vue
<template>
	<div>
		<vuex-test />
	</div>
</template>

<script>
	import VuexTest from "./components/VuexTest.vue";
	export default {
		name: "App",
		components: { VuexTest },
	};
</script>
```

```vue
// 子组件
<template>
	<div>
		<ul>
			<li v-for="(item, index) in $store.state.x" :key="index">{{ item }}</li>
		</ul>
		<input type="text" v-model="x" />
		<button @click="dispatchV(true)">添加一个元素</button>
		<button @click="dispatchV()">添加一个元素并加感叹号</button>
	</div>
</template>

<script>
	export default {
		name: "VuexTest",
		data() {
			return {
				x: "",
			};
		},
		methods: {
			dispatchV(f = false) {
                // 如果不需要数据处理可以直接调用commit
				if (f) this.$store.commit("EXEC", this.x);
				else this.$store.dispatch("handle", this.x);
			},
		},
	};
</script>
```

这样就实现了一个简单的添加内容的业务逻辑

![image-20220323224855030](https://s2.loli.net/2022/03/23/aoN52FEHiYwUJkK.png)

### Getters

Vuex还有一些不必需配置项，当我们需要的时候也可以在其中进行配置

其中有一个`getters`配置项和组件内的`computed`计算属性非常类似，只不过是全局版的，我们只需要在其中编写函数对`state`数据源中数据进行操作，之后在页面中调用`{{$store.getters.[函数名]}}`即可使用Vuex内置的计算属性

```js
const getters = {
	xNew(state) {
		return state.x[0] + "!!"
	}
}

export default new Vuex.Store({
	actions,
	mutations,
	state,
	getters
})
```

### mapState/mapGetters

我们会发现上面的代码中在页面里我们频繁的使用`$store.state.xxx`调用，一旦Vuex管理的数据越来越多，我们可能在页面中写的同样的代码也越来越长，这样显然不符合代码的简洁原则，因此Vuex提供了map方法帮助我们批量的生成简便形式的参数名

我们只需要在前引入`mapState`和`mapGetters`即可

可以将之前的代码改为

```vue
<template>
	<div>
		<ul>
			<li v-for="(item, index) in x" :key="index">{{ item }}</li>
		</ul>
		<div>{{ xNew }}</div>
		<input type="text" v-model="x1" />
		<button @click="dispatchV(true)">添加一个元素</button>
		<button @click="dispatchV()">添加一个元素并加感叹号</button>
	</div>
</template>

<script>
	import { mapState, mapGetters } from "vuex";
	export default {
		name: "VuexTest",
		data() {
			return {
				x1: "",
			};
		},
		computed: {
			// 下面代码等价于
			// x(){
			// 	return this.$store.state.x
			// }
			...mapState({ x: "x" }), // 不能简写为｛x},因为属性值不是变量
			// 当存在属性名和字符串内容一致时，可以写为数组形式...mapState(['x'])
			...mapGetters(["xNew"]), // 同上
		},
		methods: {
			dispatchV(f = false) {
				if (f) this.$store.commit("EXEC", this.x1);
				else this.$store.dispatch("handle", this.x1);
			},
		},
	};
</script>
```

### mapActions/mapMutations

当然我们也可以对`methods`里面的内容进行简写

同上引入`mapActions`和`mapMutations`之后，我们只需要在methods内仿照上面的样子写即可

但是注意在调用方法的时候注意要手动传入value值，对于上述的案例只需要修改dispatchV即可

```vue
		methods: {
			...mapActions(["handle"]),
			...mapMutations(["EXEC"]),
			dispatchV(f = false) {
				// 注意调用生成的方法时传入给Mutation的value值this.x1
				if (f) this.EXEC(this.x1);
				else this.handle(this.x1);
			},
		},
```

### 模块化设计

当我们的Mutations和Actions里面的内容越来越多的时候，我们的Vuex也需要进行模块化拆分，将部分包括`Actions`、`Mutations`、`State`等等内容拆分再重新打包，那么我们只需要对每一个模块进行命名，接着在创建`Vuex.Store`的时候添加`modules`属性即可

```js
const moduleA = {
	actions:{},
	mutations:{},
	state:{},
	getters:{}
}
const moduleB = {
	actions:{},
	mutations:{},
	state:{},
	getters:{}
}
export default new Vuex.Store({
	modules:{
		moduleA,
		moduleB
	}
})
```

接着在页面中引入时只需要比如`...mapState(['moduleA',moduleB])`，接着在页面中引用时需要`{{moduleA.x}}`即可

当然可能会觉得每一个属性都要`moduleA.`很不爽，那么我们就需要在定义`moduleA`的时候添加一个属性`namespaced:true`，接着在mapState中多传一个参数`...mapState(moduleA,['x'])`，这样我们在页面中就可以直接`{{x}}`引用了，如果还需要引用`moduleB`的，那么必须得在加一个`mapState`了，其他的map都类似

当然如果不知道map这个东西，我就要硬用`$store`取值，那么我就要这样写`$store.state.moduleA.x`，而如果要调用方法，则`$store.commit('moduleA/EXEC',this.x1)`这么写，注意要`/`斜杠分开，而且如果调用getters会发现更加复杂，直接不演示了

这么一对比简写方式就很香了

## router

路由就是一个对应关系，将某一个key与另一个value进行配对，同时所有的路由都需要有一个路由器进行管理才有意义

Vue里的路由效果与之十分类似，通过它，我们可以实现炫酷的单页面应用（SPA）

经典的实际案例就是当我们点击某个网站的导航栏时页面中的内容可以在页面中显示不同内容，但是导航和页脚都是不变的

这个Vue中的路由器会监测浏览器的地址变化，与预置的内容进行比对，只要比对上了，就会响应预先配置好的组件进行展示，而同样这个请求也会通过AJAX的方式被发送到后端，后端通过地址的信息去处理返回给我们要显示的组件的必要数据，从而实现完整的页面展示

### 简单的使用

同样它也是一个插件库，我们如果需要在vue2中使用也和vuex差不多，`npm i vue-router@3`即可

同样的，由于这两个插件都是Vue团队开发的，因此我们依葫芦画瓢，同样要在根目录下创建一个`router`目录，同时在里面创建`index.js`文件，里面的内容是这样的

```js
// 该文件专门用于创建整个应用的路由器
import Router from 'vue-router';
import RouterF from '../pages/RouterF.vue';
import RouterS from '../pages/RouterS.vue';

// 创建一个路由器
export default new Router({
	routes: [
		{
			path: '/demo1',
			component: RouterF
		},
		{
			path: '/demo2',
			component: RouterS
		}
	]
})
```

可以看出来，在这里我创建了一个路由器，并且让路由器给两个组件绑定了两个路径，这样我们路由器的配置项就写完了

接下来同样学着Vuex的样子，修改`main.js`的内容，使用路由插件内容

```js
import Vue from 'vue'
import App from './App.vue'
import router from './router';
import VueRouter from 'vue-router';

Vue.config.productionTip = false
Vue.use(VueRouter)

new Vue({
	el: '#app',
	render: h => h(App),
	router
})
```

之后我们会发现页面的地址栏中的最后出现了`/#/`的标识，意味着我们的路由器已经在正常运行了

然后我们需要在引用被路由代理的组件的组件里写上`<router-link>`标签和`<router-view>`标签，用于为用户实现交互和展示预定组件，此时在页面中我们只需要点击`<router-link>`标签内容（相当于一个`<a>`标签），那么在`<router-view>`标签中就会显示当前路由到的组件内容`/demo1->RouterF...`（等于是将`<router-view>`标签替换为了`<RouterF/>`）

正因为路由代理组件不再需要在父组件中编写组件标签的方式引入组件内容，因此我们常常对被路由管理的组件单独拎出来放在`pages`目录中（范例中的`RouterF`和`RouterS`），而普通的组件内容则放在components目录里

```vue
// 父组件,App.vue
<template>
	<div>
		<!-- 这个router-link和a标签完全一致，只需要修改href到to属性即可 -->
        <!-- 内部active-class可以指定被选中时展示的样式 -->
		<router-link to="/demo1" active-class="">查看第一个测试页面</router-link>
		<router-link to="/demo2">查看第二个测试页面</router-link>
		<!-- 在这里展示个性化内容 -->
		<router-view>内容</router-view>
	</div>
</template>

<script>
	import RouterF from "./pages/RouterF.vue";
	import RouterS from "./pages/RouterS.vue";
	export default {
		name: "App",
		components: { RouterF, RouterS },
	};
</script>
```

```vue
// pages/RouterF.vue
<template>
	<h2>这是第一个测试文件</h2>
</template>

<script>
	export default {
		name: "RouterF",
	};
</script>
// RouterS与此类似
```

接着我们就可以在页面中看到完整效果了

![image-20220326124154938](https://s2.loli.net/2022/03/26/gJPkbixLQv6eulK.png)

> 如果我们查看被路由管理的组件内容，我们会发现里面的vc实例中出现了`$route`和`$router`两个属性，这两个属性分别代表了我们在路由`index.js`配置的路由信息（即数组中的每一项）和这些组件的路由器信息（即new的Router），其中路由信息每一个组件不同，但是路由器是组件间共用的，其中的方法使用之后会提到

### 嵌套

当我们在一个路由到的组件中想要继续配置路由结构，即继续配置子路由，那么我们就需要在`index.js`中给需要配置路由的配置项添加`children`属性，比如下面这样

```js
{
    routes:[
        {
            path:'/father',
            component:Father
            children:[
            	{
					path:'son',  // 注意不要加横杠
            		component:Son,
        		}
            ]
        }
    ]
}
```

接下来我们就可以通过在组件内的`<router-link>`标签中添加路径`/father/son`即可

### query传参

上面的案例有一些问题，因为界面中的内容变化不大，即仅变化了一个字，但是我们为了展示变化不大的内容却用到了两个组件，没有满足组件间的复用要求，有没有一种办法，我们仅用一个组件，同时告诉路由往该组件中传入不同的参数，实现页面内容的变化呢？

此时我们就需要用到get请求的知识，假装发了一个请求，实际上每一个子组件内将会收到地址栏中传入的参数，根据这个参数调整显示内容即可

```vue
// 父组件,App.vue
<template>
	<div>
		<!-- 直接将to写成对象模式，推荐 -->
		<router-link
			:to="{
				path: 'demo1',
				query: {
					id: 1,
				},
			}"
			active-class=""
		>查看第一个测试页面</router-link>
		<!-- 模版字符串，里面可以加变量的引用 -->
		<router-link :to="`/demo1?id=2`">查看第二个测试页面</router-link>

		<router-view>内容</router-view>
	</div>
</template>

<script>
	import RouterF from "./pages/RouterF.vue";
	import RouterS from "./pages/RouterS.vue";
	export default {
		name: "App",
		components: { RouterF, RouterS },
	};
</script>
```

```vue
<template>
	<h2>这是第{{ $route.query.id }}个测试文件</h2>
</template>

<script>
	export default {
		name: "RouterF",
	};
</script>
```

### params传参

#### 命名

当我们的路由嵌套层级越来越多的时候，我们每一次在页面中引用都显得很麻烦，因此我们可能需要一个简写形式，这时候就可以在路由器的配置中给指定的路由结构增加一个name属性，紧接着在页面中引用时直接`:to="{name:'[name名]'}"`，即可快速访问指定路由，但是必须写成对象形式

#### params

但是可能会觉得这种方式定义name还是有点反人类，不知道为什么要这么做，直接写路径不香吗？其实是因为给通过params传参提供方便，这是除了query之外另一种传递参数的方式

在之前的学习中我们知道了地址通过Restful传参的方式，实际上params传参就是利用Restful进行的，我们只需要如此配置

```js
// 该文件专门用于创建整个应用的路由器
import Router from 'vue-router';
import RouterF from '../pages/RouterF.vue';
import RouterS from '../pages/RouterS.vue';

// 创建一个路由器
export default new Router({
    routes: [{
            name: 'demo1',
            path: '/demo1/:id',
            component: RouterF
        },
        {
            path: '/demo2',
            component: RouterS
        }
    ]
})
```

```vue
// 父组件,App.vue
<template>
	<div>
		<!-- 对象式传参，注意必须是name属性，如果还是path会报错 -->
		<router-link
			:to="{
				name: 'demo1',
				params: {
					id: 1,
				},
			}"
			active-class=""
		>查看第一个测试页面</router-link>
		<!-- Restful风格传参 -->
		<router-link :to="`/demo1/2`">查看第二个测试页面</router-link>

		<router-view>内容</router-view>
	</div>
</template>

<script>
	import RouterF from "./pages/RouterF.vue";
	import RouterS from "./pages/RouterS.vue";
	export default {
		name: "App",
		components: { RouterF, RouterS },
	};
</script>

```

```vue
<template>
	<h2>这是第{{ $route.params.id }}个测试文件</h2>
</template>

<script>
	export default {
		name: "RouterF",
	};
</script>
```

可以发现在params传参的过程中，如果涉及到参数传递的对象写法，那么就必须通过指定name的方式进行传递，但是总体上来说和query的取得参数区别不大，具体怎么选择就看个人习惯了

#### props

除此之外，我们可能会发现在子组件内调用父组件传过来的参数时，似乎也不是那么方便，我们每次都要写一个`$route.params/query.xx`的方式调用参数，一旦传过来的参数变多了，写一大堆内容显得十分繁琐，此时我们就需要借助路由器的props属性，它可以帮助我们简化组件内代码

```js
export default new Router({
    routes: [{
            name: 'demo1',
            path: '/demo1/:id',
            component: RouterF,
            // 第一种写法，将参数写死
            // props:{id:1}
            // 第二种写法，直接打开，router默认会将params里面携带的参数变成props的内容传给子组件
            // props:true
            // 第三种写法，函数方式返回值，可以指定接收参数，参数为将要传给子组件的route对象
            props(route) {
                return { id: route.params.id }
            }
        },
        {
            path: '/demo2',
            component: RouterS
        }
    ]
})
```

这三种方式的效果都是一样的，会给子组件内通过props传入一个id属性，当然指定props参数之后我们还需要在组件内接收

```vue
<template>
	<h2>这是第{{ id }}个测试文件</h2>
</template>

<script>
	export default {
		name: "RouterF",
		props: ["id"],
	};
</script>
```

### 编程式导航

我们发现我们现在进行跳转的时候必须将跳转内容设置在`<router-link>`也就是最后显示的`<a>`标签上，但是实际开发中我们肯定不止会在`<a>`标签上添加跳转需求，比如目标是一个按钮，那目前我们就一筹莫展了

此时就需要进行编程式导航了，而实现这个方法的基础，就是每个路由组件身上的`$router`属性

```vue
// 父组件,App.vue
<template>
	<div>
		<button @click="showD()">按钮实现查看第一个页面</button>
		<router-view>内容</router-view>
	</div>
</template>

<script>
	import RouterF from "./pages/RouterF.vue";
	import RouterS from "./pages/RouterS.vue";
	export default {
		name: "App",
		components: { RouterF, RouterS },
		methods: {
			showD() {
				this.$router.replace({
					name: "demo1",
					params: {
						id: 1,
					},
				});
			},
		},
	};
</script>
```

> 其中`$router.replace`可以替换为`$router.push`，其他都一样，他们的区别是路由之后可不可以回退到上一次的操作界面，如果设置为`replace`那么按下本次操作之后浏览器上的后退按钮就无法回退到按下按钮前的页面
>
> 另外`$router`还有`back()/forward()/go()`，他们的效果和浏览器的后退和前进按钮差不多

### 新生命周期钩子

#### 缓存路由组件

我们如果为两个路由组件添加了`beforeDestroy`钩子，那么我们会发现当展示的组件进行切换的时候，上一个展示的组件立即被销毁了，意味着每一次点击后产生的页面vc实例都是不一样的，路由器帮助我们对不需要使用的实例内容进行销毁

但是有时候比如当页面上存在表单的时候用户输了一大堆内容结果不小心将界面切走了，切回来的时候由于产生了一个新的实例，因此表单内的数据都不存在了，这时候我们就需要将填写表单的页面进行缓存，以便下一次回到页面的时候能够重新展示内容

此时我们只需要在`<router-view>`标签外包一个`<keep-alive>`标签就可以了

```html
<keep-alive include="RouterF">
    <router-view>内容</router-view>
</keep-alive>
```

注意include里面一定是**组件名**，就是组件内的name属性

#### activated/deactiveted

但是虽然我们知道了可以避免组件销毁，但是比如我们在缓存组件中开了一个定时器，那么在组件切换的过程中我们后台的定时器依旧在运作，一旦类似组件越来越多也会极大的占用资源，因此我们需要一个钩子来对我们是否切换出组件做一个判断

这时就引入了两个新的生命周期钩子，他们分别代表组件被启动和组件被切走（无论是否配置`keep-alive`，比起直接在`beforeDestroy`钩子里写内容，用这两个钩子能够更方便的对路由组件进行管理

### 路由守卫

路由守卫就是保护路由的权限，用于保护用户的信息安全，比如用户的用户中心，当然需要当用户登录时判断用户信息才决定究竟是否能够查看，这时候就需要配置路由守卫

#### 全局

```js
const router = new VueRouter({
    routes: [{
            name: 'demo1',
            path: '/demo1/:id',
            component: RouterF,
            props(route) {
                return { id: route.params.id }
            },
            meta: { a: 123 }
        },
        {
            path: '/demo2',
            component: RouterS
        }
    ]
})

// 前置路由守卫，在每次页面初始化和路由切换的时候进行调用（即页面交互引起地址栏路径变化时）
router.beforeEach((to, from, next) => {
    // to和from可以查看当前路由组件和跳转到的路由组件内的$route属性信息，包括路径名称参数等信息
    // 同时我们还可以对每一个路由的meta属性进行编辑，使得我们可以在守卫里面拿到路由信息
    console.log(to, from, meta.a);
    // 在这判断是否对其放行，对放行的请求使用next函数
    next()
})

// 后置路由守卫，用的不多，在路由切换之后调用，可以配置一些页面标题之类的信息，没有next参数
router.afterEach((to, from) => {
    console.log(to, from);
})
export default router
```

![image-20220326195816873](https://s2.loli.net/2022/03/26/SegyQvjLTq7Z9Rh.png)

#### 独享

原理同上，在每一个路由之前添加`beforeEnter`属性即可

```js
const router = new VueRouter({
    routes: [{
            name: 'demo1',
            path: '/demo1/:id',
            component: RouterF,
            props(route) {
                return { id: route.params.id }
            },
            meta: { a: 123 },
            beforeEnter: (to, from, next) => {
                console.log(to, from)
                next()
            }
        }]
}
```

注意独享路由守卫没有后置守卫

#### 组件内

在组件内添加`beforeRouteEnter`和`beforeRouteLeave`属性即可，在从路由器进入组件的时候和从组件中离开的时候调用

```vue
<template>
	<h2>这是第{{ id }}个测试文件</h2>
</template>

<script>
	export default {
		name: "RouterF",
		props: ["id"],
		beforeRouteEnter(to, from, next) {
			console.log(to, from);
			next();
		},
		beforeRouteLeave(to, from, next) {
			console.log(to, from);
			next();
		},
	};
</script>
```

注意两个方法都有next参数

### 项目上线

当前我们会发现我们的所有地址前面都有一个`#`号，十分的不美观，导致的原因其实是路由默认使用了hash模式，我们只需要在定义路由器时指定为`mode:history`即可

```js
const router = new VueRouter({
    mode: 'history',
    routes: [
        ...
    ]
})
```

接着我们在浏览器中路由到指定内容就会在地址栏显示仅以`/`分隔的地址了

![image-20220326210813514](https://s2.loli.net/2022/03/26/oeFBvLpItwqu8DJ.png)

但是当项目正式上线的时候，这种history风格的地址名很可能会给后端带来困扰，因为前端路由是不发送请求的，因此我们很可能在点了半天之后一按刷新，于是给后端发了一个不存在的请求，从而产生404错误，当然为了好看我们可以解决一切问题，其中如果用Nginx作为代理服务器，仅一行代码就可以[解决问题](https://router.vuejs.org/zh/guide/essentials/history-mode.html#nginx)

但是做好的前端项目如何上线呢，我们就需要通过`npm run build`来打包项目，接着会在当前目录下生成一个dist文件，里面有我们写的纯html和css，js文件，当然直接打开`index.html`是行不通的，模块化处理需要我们搭建一个服务器管理项目，比如直接将里面内容拷贝粘贴到在本机的Nginx上默认目录下即可

## ElementUI

Vue最好的UI库还得是饿了么UI，当然也有别的各种不同的UI库可以用，但是一通俱通，我们就拿ElementUI作为例子

官网在这，直接按照里面的内容依葫芦画瓢即可，但是其中有些内容可能过时了，因此我们需要进行一下修改

最后的文件修改内容如下

- `main.js`

  ```js
  import Vue from 'vue'
  import App from './App.vue'
  
  Vue.config.productionTip = false
  
  // 所有的组件都被注册了，发的包会很大
  // import ElementUI from 'element-ui' 
  // import 'element-ui/lib/theme-chalk/index.css';
  // Vue.use(ElementUI)
  
  // 按需引入
  import { Button, Row } from 'element-ui';
  Vue.component(Button.name, Button)
  Vue.component(Row.name, Row)
  
  new Vue({
      el: '#app',
      render: h => h(App),
  })
  ```

- `babel.config.js`

  ```js
  module.exports = {
      presets: [
          '@vue/cli-plugin-babel/preset', ["@babel/preset-env", { "modules": false }]
      ],
      "plugins": [
          [
              "component",
              {
                  "libraryName": "element-ui",
                  "styleLibraryName": "theme-chalk"
              }
          ]
      ]
  }
  ```

- `App.vue`

  ```vue
  <template>
  	<div>
  		<el-row>
  			<el-button>Default</el-button>
  			<el-button type="primary">Primary</el-button>
  			<el-button type="success">Success</el-button>
  			<el-button type="info">Info</el-button>
  			<el-button type="warning">Warning</el-button>
  			<el-button type="danger">Danger</el-button>
  		</el-row>
  	</div>
  </template>
  
  <script>
  	export default {
  		name: 'App',
  	}
  </script>
  ```

即可运行

# Vue3

终于进入了Vue3的学习，从上面对于Vue2的学习，我们还是发现了Vue2的某些缺陷，于是Vue3应运而生，它

- 打包大小减少41%
- 初次渲染快55%，更新渲染快133%
- 内存减少54%

还有更多乱七八糟的更新，牛逼就完了

## 简单使用

1. 为了避免和之前的内容相重复出现问题，因此我们先直接卸载所有模块

   `npm uninstall * && npm rm -rf node_module package.json package-lock.json`，如果不知道`node_module`在哪，可以通过`npm root`查看，并通过`npm ls`看看是不是真的卸载成功

2. 安装vue，同时我选择不安装脚手架，直接梭哈另一个Vue团队开发的前端构建工具vite

3. 在想要的目录下部署vite项目文件`npm create vite@latest`然后跟着选项一路选下来即可

4. vite并没有预先帮助我们下载好依赖包，因此我们需要`cd vite-project && npm install`来安装内容

5. `npm run dev`启动项目，接着可以在`localhost:3000`看到部署的项目

## 文件结构

进入项目目录，我们发现大体上的文件结构和Vue2十分类似

![image-20220327100533896](https://s2.loli.net/2022/03/27/KhYbvEiatZdRxpF.png)

因此我们还是从入口文件`main.js`开始分析，众所周知这里应该就是原本我们创建vm的地方

```js
// 引入的不是Vue构造函数了，引入的是名为createApp的工厂函数
import { createApp } from 'vue'
import App from './App.vue'

// 可以直接调用这个函数
const app = createApp(App) // 页面容器的id
app.mount('#app') // 挂载
console.log(app); // 这个app比起下面之前写的vm显得非常的轻量
// app.unmount('#app')  // 我们也可以直接通过unmount解除挂载，页面上的东西直接没了

// const vm new Vue({
// 	render:h=>h(App)
// })
// vm.$mount('#app')
```

 可以发现初始的代码就三行，明显比之前简单了许多，而进行逐行分析我们还是可以发现与Vue2的`main.js`一对比相似程度还是很高的，但是Vue3更加精简了我们需要编写代码的内容，仅需要一行，就达到了我们之前`new Vue...`一大堆的配置内容

接着我们看一看预先给我们配置好的`App.vue`组件内容

```vue
<script setup>
	// This starter template is using Vue 3 <script setup> SFCs
	// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
	import HelloWorld from './components/HelloWorld.vue'
</script>

// Vue3可以没有根标签
<template>
	<img
		alt="Vue logo"
		src="./assets/logo.png"
	/>
	<HelloWorld msg="Hello Vue 3 + Vite" />
</template>

<style>
	#app {
		font-family: Avenir, Helvetica, Arial, sans-serif;
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
		text-align: center;
		color: #2c3e50;
		margin-top: 60px;
	}
</style>
```

总的结构和之前大差不差，只是多了一个setup标签属性和在template内的多个标签内容，不过还是可以勉强进行阅读的

稍微对目录结构有了一个大致的印象，接下来就可以开始Vue的学习了

## Composition API

一看这标题名字是什么鬼啊，暂且将其理解为组合式API，这是Vue3运行的基础，而接下来所有的学习内容都是组合式API的一部分，我们会发现在使用这些函数的时候我们都需要在顶部加上`import ... from 'vue'`来引入这些API，不然在页面运行时会报错，而这些API都需要写在setup中才能被使用，如果还是不理解，我们在接下来的学习中一定会不断的接触这个概念

### setup

它是所有Compositon API表演的舞台也是接下来内容中唯一不需要引入的配置项，是Vue3新的配置项，是一个函数，组件中所用到的所有的数据方法都要配置在这

```vue
<script>
	export default {
		name: 'App',
		setup() {
			let name = '123'
			function sayHi() {
				alert(`${name},hi!`)
			}
			return {
				name,
				sayHi
			}
		}
	}
</script>

<template>
	<h2>{{name}}</h2>
	<button @click="sayHi">欢迎</button>
</template>
```

除了setup函数之外，几乎没有别的任何不同，同时setup返回的对象属性和方法可以直接在页面模版对象中使用，相当于在之前配置了data和methods项

借助提供的`script setup`标签，我们还可以进一步简化代码

```vue
<script setup>
	let name = '123'
	function sayHi() {
		alert(`${name},hi!`)
	}
</script>
```

> 要注意的是setup函数执行的时机比beforeCreate还要早，同时它的this是undefined

### ref

此时上面这个案例是没有存在响应式的，就算我们在函数内`name='234'`但是反映到页面中并不会修改页面内容，因为Vue3没有对里面的这个参数进行跟踪，如果我们想要让他真的变成原本Vue2中的`data`属性，我们就要借助ref对setup内的参数进行包装，使得在内部函数修改之后能够正确响应到页面上

```vue
<script setup>
    // 引入ref函数
	import { ref } from 'vue'
	// 因为ref产生一个代理对象，因此使用const来接收内容
	const name = ref('123')
    // 定义对象类型的响应数据
	const person = ref({
		name: '123',
		age: '456',
	})
	function sayHi() {
		// 这样就可以修改数据了
		name.value = '234'
		person.value.name = '345' // 只需要一个value
	}
</script>

<template>
	<h2>{{ name }}</h2>
	<button @click="sayHi()">欢迎</button>
</template>
```

至于为什么修改数据时需要调用`value`属性，其实是由于ref默认帮我们给数据打包成了一个`RefImpl`对象，我们可以通过控制台输出来确认，而我们的数据，正是存在这个对象中的`value`属性中

### reactive

reactive专门用以定义对象类型的响应数据，当然ref也可以定义对象类型，但是reactive作为管理响应对象的专家，显然有它的优势

```vue
<script setup>
	import { reactive } from 'vue'
	const reac = reactive({
		name: '234',
	})
	function test() {
        // 不需要加value，直接修改即可
		reac.name = '456'
	}
</script>

<template>
	<h2>{{ reac.name }}</h2>
	<button @click="test()">改名</button>
</template>

```

如果我们输出reac变量和上面通过ref定义的person对象，我们会发现两个对象的内容其实都是一个Proxy响应对象，意味着Vue3为了达到响应式的对象内容将我们定义的对象变成了一个个Proxy实例

```js
console.log(person)
console.log(reac)
```

![image-20220327171006923](https://s2.loli.net/2022/03/27/1Eu4TyUDt7Xsoip.png)

这也说明了为什么我们使用ref的时候修改对象内属性不是`person.value.name.value`，因为有比起Vue2更强大的Proxy类型帮我们对对象进行响应式操作

Proxy更强大的地方在于，只要把需要监测的对象丢给它，无论对象里面是怎么复杂的结构，不管到底里面还包了几层对象，只要其中某个对象的某个值被修改了，就一定会被Proxy监测到，不仅是对象，Proxy还支持数组的监测，对我们而言，也就只需要将数组内容抛给`reactive`方法就行了

也就是说Proxy除了不能处理，已经是全面碾压ref了（因为ref还是使用的是Vue2的`$getter`和`$setter`实现响应式），既然Proxy这么强大，因此不到万不得已，我们一般都不会使用ref了（甚至可以自创一些对象为了不使用ref）

### 响应式原理

Vue2要修改数组内容，必须使用给定的五个数组修改方法，或者直接换一个数组，或者使用`this.$set`方法，但是Vue3有了Proxy，可以直接通过下标来修改数组内容，一样会被监测到，不仅如此，反正只要setup方法把其中定义的对象交出去了，不管你在里面函数里怎么调教定义的属性，Vue3都能监测到对被Proxy管理的属性

那为什么这个Proxy那么给力呢，这时候就需要介绍Vue3的响应式原理了，为了形成对比，我们可以先复习一下Vue2的[响应式原理](#Object.defineProperty)

强大的Proxy实现主要还是靠`window.Proxy`这个内置对象和`Reflect`反射对象的内容操作，我们不妨对Vue3中的响应式数据操作进行简单的模拟，先看案例

```html
<body>
    <script>
        const person = {
            name: '测试',
            age: 12
        }
        const p = new Proxy(person, {
            // 查
            get(target, propsData) {
                console.log(`检测到你读取了${propsData}`)
                return Reflect.get(target, propsData)
            },
            // 增和改
            set(target, propsData, value) {
                console.log(`检测到将${target[propsData]}修改为${value}`)
                Reflect.set(target, propsData, value)
            },
            // 删
            deleteProperty(target, propsData) {
                console.log(`检测到删除${propsData}`)
                return Reflect.deleteProperty(target, propsData)
            }
        })
    </script>
</body>
```

![image-20220327183551590](https://s2.loli.net/2022/03/27/hTHKmpdrsC3ENOv.png)

可以发现创建的这个Proxy代理实例p，不仅能对所有他自己身上属性的修改并对person进行镜像操作，同时对于自己身上的每一次修改都能够被内置的方法所监测到，而这个比起Vue2中单纯的只有get和set方法的`defineProperty`阉割版数据代理不知道强到哪里去了

同时顺便提一下Reflect反射对象，其中内置了很多正常使用也完全没问题的镜像方法，比如说上面的代码可以直接用我们常用的形式替换，比如`Reflect.get(target, propsData)`完全等价于`target[propsData]`，但是优点是通过反射对象所进行操作无论成不成功都不会以报错的方式展示（一旦报错程序立即终止，整个项目就瘫痪了），而是在返回值中确定操作是否被完成，这样对于大型框架的开发有着举足轻重的作用，完全可以通过返回值人为设置一些友好的报错信息，不然就得在代码中写满`try...catch`了

### 传参/事件/插槽

作为父组件给子组件传递的三个内容，由于Vue3中不再有methods属性了，因此也需要提一下，直接给一个样例就过

```vue
// 父组件
<template>
	<div>
		<Demo02 @event="showEvent" :msg="msg">
			<template #test="{ msg1 }">
				<h2>这是一个插槽内容,从子组件传来的参数为{{ msg1 }}</h2>
			</template>
		</Demo02>
	</div>
</template>
<script>
	import Demo02 from './components/Demo02.vue'
	export default {
		name: 'App',
		components: { Demo02 },
		setup() {
			const msg = 'test'
			function showEvent(value) {
				console.log(`触发了event事件，收到了${value}参数`)
			}
			return {
				showEvent,
				msg,
			}
		},
	}
</script>
```

```vue
// 子组件
<template>
	<h1>从父组件中获得的参数为{{ data.para }}</h1>
	<button @click="execEvent">按下触发事件</button>
	<span v-show="data.flag">事件被触发了</span>
	<slot name="test" :msg1="data.msg1">默认值</slot>
</template>

<script>
	// 当然如果组件内需要配置多个属性项，自然是不适合用setup的语法糖效果的
	import { reactive } from 'vue'
	export default {
		name: 'Demo2',
		props: ['msg'],
		emits: ['event'],
		// setup可以收到两个参数，分别是父组件里传过来的参数内容(props)和调用开启事件的上下文(context)
		// 当然context的用处不仅是开启事件
		// 如果前面没有声明props属性，那么父组件传过来的参数就会被放在context.attr中
		// 而父组件传入的插槽信息也会存在context.slot里
		setup(props, context) {
			// 一定要记得写reactive内容，不然所有的修改都会失效
			const data = reactive({
				msg1: 123,
				// 将父组件的传参通过行参的方式传给子组件，避免了父组件的参数被直接调用修改，子组件要在页面上使用就必须重新赋一个变量
				para: props.msg,
				flag: false,
			})
			function execEvent() {
				data.flag = true
				context.emit('event', 123)
			}
			return {
				execEvent,
				data,
			}
		},
	}
</script>
```

![image-20220327202006594](https://s2.loli.net/2022/03/27/QCMtfOHNoPzxLR8.png)

注意当子组件与父组件有信息交互的时候，不能用setup语法糖

### computed

Vue3同样支持计算属性，具体代码如下

```vue
<template>
	<input type="text" v-model="data.name" />
	<input type="text" v-model="data.age" />
	<br />
	<span>{{ merge }}</span>
</template>

<script setup>
	import { reactive, computed } from 'vue'
	const data = reactive({
		name: 'test',
		age: 12,
	})
	const merge = computed(() => {
		return data.name + '-' + data.age
	})
</script>
```

其中`computed`也是简写形式，具体的形式可以使用`get`和`set`方法，和Vue2差不太多

### watch

Vue3里面的watch就比较奇葩了，一共会分为六种情况，需要分别掌握

```vue
<template>
	<button @click="name += '1'">修改ref属性name</button>
	<button @click="data.name += '1'">修改reactive属性data.name</button>
	<button @click="data.obj.a.b++">修改reactive属性obj.a.b</button>
</template>

<script setup>
	import { ref, reactive, watch } from 'vue'
	let name = ref('test1')
	let age = ref(12)
	const data = reactive({
		name: 'test',
		age: 12,
		obj: {
			a: {
				b: 1,
			},
		},
	})
	watch(name, (newValue, oldValue) => {
		console.log('第一种情况，监视单个ref属性', newValue, oldValue)
	})
	watch([name, age], ([newname, newage], [prevname, prevage]) => {
		console.log('第二种情况，监视多个ref属性', newname, newage)
	})
	watch(data, (newValue, oldValue) => {
		console.log('第三种情况，监视单个reactive对象，则oldValue无效，无法知道谁被修改了', newValue, oldValue)
	})
	watch(
		() => data.name,
		(newValue, oldValue) => {
			console.log('第四种情况，监视单个reactive对象的某个属性', newValue, oldValue)
		},
	)
	watch([() => data.name, () => data.age], ([newname, newage], [prevname, prevage]) => {
		console.log('第五种情况，监视多个reactive对象的多个属性', newname, newage)
	})
	watch(
		() => data.obj,
		(newValue, oldValue) => {
			console.log('第六种情况，监视reactive对象里的深度属性', newValue, oldValue)
		},
		{ deep: true, immediate: true },
	) // 在这里可以配置Vue2里面提到过的参数内容
</script>

```

![image-20220327212538758](https://s2.loli.net/2022/03/27/fUdjECZaiQ7PAch.png)

同时还需要注意监视ref的时候不应该加`.value`，因为我们监视的必须是一个结构而不是单单的一个值

#### watchEffect

Vue3还提供了一个过程监视的方法， 有点类似计算属性，但是不返回计算结果给某个变量，调用这个方法时会自动检测在此代码块中的参数内容，一旦发生改变便会自动调用这个函数

```vue
<template>
	<button @click="data.name += '1'">修改reactive属性data.name</button>
</template>

<script setup>
	import { reactive, watchEffect } from 'vue'
	const data = reactive({
		name: 'test',
		age: 12,
	})
	watchEffect(() => {
		// 一些包含了参数内容的业务逻辑，只需要当里面参数的内容被修改就会调用
		console.log('当前的data.name被修改了', data.name)
		// 上面代码调用了data.name，因此我们不需要指定去监视它
		// 由于注重过程内容，因此不需要返回值
	})
</script>
```

### Vue3生命周期

Vue3取消了Vue2中的`beforeDestroy`和`Destroy`两个生命周期，代替的是`BeforeUnmount`和`Unmounted`，代表着的是组件的卸载，在Vue2中组件不使用的时候会销毁，而在Vue3中销毁就是将其不再挂载在父组件上了，也不算难理解

同时Vue3为大多数生命周期钩子配置了组合式API，我们可以在setup属性中直接调用

```vue
// 子组件
<template>
	<div>
		<button @click="num++">num++</button>
	</div>
</template>

<script>
	import { ref, onBeforeMount, onMounted, onBeforeUpdate, onUpdated, onBeforeUnmount, onUnmounted } from 'vue'
	export default {
		setup() {
			console.log('----setup')
			let num = ref(1)
			onBeforeMount(() => {
				console.log('----BeforeMount')
			})
			onMounted(() => {
				console.log('----Mounted')
			})
			onBeforeUpdate(() => {
				console.log('----BeforeUpdate')
			})
			onUpdated(() => {
				console.log('----Updated')
			})
			onBeforeUnmount(() => {
				console.log('----BeforeUnmount')
			})
			onUnmounted(() => {
				console.log('----Unmounted')
			})
			return {
				num,
			}
		},
		beforeCreate() {
			console.log('----beforeCreate')
		},
		created() {
			console.log('----create')
		},
	}
</script>
```

```vue
// 父组件
<template>
	<button @click="isShow = !isShow">是否显示</button>
	<Demo05Vue v-if="isShow" />
</template>

<script>
	import Demo05Vue from './components/Demo05.vue'
	import { ref } from 'vue'
	export default {
		name: 'App',
		components: { Demo05Vue },
		setup(props) {
			let isShow = ref(true)
			return { isShow }
		},
	}
</script>
```



![image-20220327221213469](https://s2.loli.net/2022/03/27/xBq5mgWVsufaZ4Y.png)

### Hook函数

当我们的项目中可能会产生某些可以复用的小功能，比如获取鼠标在屏幕上的位置并显示，这些功能和组件本身是没什么关系的，而且往往需要在多个组件内灵活使用，这时候我们就可以把他们封装成一个个Hook函数，Hook的本质就像是一个钩子，当我们需要的时候随时把他勾过来使用就行

一般来说，我们会在src目录下建立一个`hooks`目录，在其中以`usexxxx.js`定义钩子的名字，接着在里面写上全套的可以被`setup`使用的函数内容，接着提供一个返回值，保证`setup`函数每一次钩到这个钩子都能够获取到一个返回值

尤其是当这个功能内存在对生命周期钩子函数的使用，那么将其封装为一个钩子还可以减少在setup中引入的过量API

```js
import { reactive, onMounted, onBeforeUnmount } from "vue";
export default function() {
    let point = reactive({
        x: 0,
        y: 0
    })

    function savePoint(event) {
        point.x = event.pageX
        point.y = event.pageY
        console.log(event.pageX, event.pageY);
    }
    onMounted(() => {
        window.addEventListener('click', savePoint)
    })
    onBeforeUnmount(() => {
        window.removeEventListener('click', savePoint)
    })
    return point
}
```

同时由于传出来的天然是reactive对象，因此在组件内直接`let`接收即可

```vue
<template>
	<div>
		<h2>当前点击{{ p.x }},{{ p.y }}</h2>
	</div>
</template>

<script setup>
	import usePoint from '../hooks/usePoint.js'
	let p = usePoint()
</script>
```

### toRef

我们都知道我们推荐使用Vue3新增的reactive作为响应式数据，但是它也有缺点，就是我们把一般数据都包裹在一个对象中，在页面上引用的时候免不了要先引用`[对象名].[属性]`来引用数据，一旦数据比较多就需要写一大堆对象名，可不可以直接在返回时将对象内属性拆解，使得在页面中只使用属性名来显示属性内容呢

我们可以先思考一下用仅有的API可不可以做到

- 直接`return{a.b}`显然不行，因为a是Proxy对象而里面的属性b不是，因此返回的是一个干巴巴的数据，根本没有办法进行响应
- `return{ref(a.b)}`也是不行的，虽然好像在页面上进行了代理，但是实际上返回出去的根本就是一个新的数据，Vue将`a.b`这个reactive代理的数据重新包装成了ref数据，如果在setup中有修改a的方法一下子就会发现并不能做到响应式

这时候就需要请出我们的`toRef(s)`了，它可以在拆分reactive属性的基础上仅引用其中的属性内容，形成一个二次代理，从而使所有的数据修改都保持一致性

```vue
<script>
	import { reactive, toRefs } from 'vue'
	export default {
		setup() {
			const data = reactive({
				a: 1,
				b: {
					c: 2,
				},
			})
			return {
				// 等于toRef(data,'a')和toRef(data.b,'c')
				// 如果单用ref(data.a)会使页面上的响应式数据与setup中的reactive数据脱离关系，toRef是引用数据并不是无脑复制
				...toRefs(data),  // 返回的若干对象的对象集合，需要使用解构赋值
			}
		},
	}
</script>
```

但是toRef有一个局限，就是当其中被拆解的对象中又新添了一个新的属性时，我们并不能在页面上捕获到新增的属性信息，遇到这种情况就不得不直接传出整个data对象了

### 其他API

- Vue3还提供了能够让祖先给他的后代所有组件传数据的方式，只需要在父组件中添加`privide([变量共享名字],[变量名])`，接着在任意层级子组件中添加`inject([变量共享名字])`即可直接使用数据，但是注意这个数据和父组件里面共用的一个响应式，修改的时候应该注意对父组件的影响，同时这个API比较适用于祖孙之间传递数据，父子之间还是使用`props`比较好
- 当我们从别人手上拿到一个响应式数据（比如父组件），但是要提醒自己不要修改它时，我们可以使用`readonly([变量名])`，会让这个变量还是响应式数据，但是我们已经无法修改了，真的要修改就会控制台报错提醒我们

### 优势

通过对各种组合式API的学习，我们发现了我们所有的内容都写在setup方法里，写程序更加畅快了，这就是它的最大优势，原本我们在Vue2的时候，假设要增加一个响应式数据，我们得从`data`配置项开始改，一路改`computed`、`methods`、`watch`里面的配置项，一个数据的流程都被拆散了，当然拆散也有拆散的好处，在查找时可以方便的查到内容，但是如果我们需要跟踪一个数据就麻烦了，我们得每个配置项一个个找，才能理出一条数据的操作流程，而使用组合式API，所有数据的定义和操作流程是流畅的，我们可以方便的找到我们需要的内容，下面是几张动图

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/568b0ced69f241d282cf2c512e4e5f33~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp)

![See the source image](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/d05799744a6341fd908ec03e5916d7b6~tplv-k3u1fbpfcp-watermark.image)

![img](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/4146605abc9c4b638863e9a3f2f1b001~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp)

同时我们注意到第三张gif，当所有的数据内容高度集中化之后，我们就可以将每一个数据的操作流程进行一个打包，成为一个个Hook，既提高了复用效率，更加提高了代码的精简程度，方便维护者进行修改维护，这么一想也有点面向对象的意思了

## 特殊功能标签

讲完了setup里面的各种API，接下来我们就需要学习一些写在默认`<template>`里面的一些具有特殊功能的标签，他们都是Vue3不可缺少的组成成分

### Fragment

我们会发现在Vue3项目中，它不要求我们每一个组件内部最外层必须仅套一个标签了，我们可以在`<template>`标签下写任意个数的标签，其实是Vue3在渲染的时候默认会贴心的给我们所有标签加了一层`Fragment`标签，同时在显示在页面上的时候再将其去掉，我们可以从开发者工具中看到端倪

![image-20220328225644915](https://s2.loli.net/2022/03/28/LhoASFCZVpKMIR5.png)

### Teleport

我们可以在任意组件中用这个标签包裹其他标签，并在标签属性中指定需要将其中内容摆放的位置，这时候我们在观察程序结构的时候会惊讶的发现我们的组件已经不再遵循父子关系了

```html
<template>
	<h2>{{ a }}--{{ b.c }}</h2>
	<teleport to="body">
		<h2>你好</h2>
	</teleport>
</template>
```

![image-20220328225404935](https://s2.loli.net/2022/03/28/phkY52AvdGTFq4P.png)

当然我们也可以在`to`属性中写比如`#app`，实现组件内的部分结构到处乱飞的效果，还是十分有用的，尤其适合各种弹窗效果

