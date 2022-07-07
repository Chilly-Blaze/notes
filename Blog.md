# Windows下搭建Nginx+PHP环境

虽然服务器上一键装好了Nginx+PHP环境，但是我完全不懂它到底干了什么，虽然还没学Nginx，但并不妨碍我利用搭建一个运行PHP服务的环境

主要还是手贱把XAMPP删掉了，同时既然服务器都不推荐使用Apache的WebServer了，我凭什么还要用它运行PHP，实在是掉我身价

然后就花了一个晚上搭建这个神秘的环境

## 搭建步骤

1. 下载[Nginx](https://nginx.org/en/download.html)和[PHP](https://www.php.net/downloads.php)最新版，解压，最好放在同一目录下

   ![image-20211112215335265](https://s2.loli.net/2021/12/05/DAQKGLm12fZ8Sas.png)

   效果图如下

2. 配置`nginx.conf`，进入`".\nginx-1.20.1\conf\nginx.conf"`，可以通过行号查找并修改以下内容

   ![image-20211112220423802](https://s2.loli.net/2021/12/05/PXsTZoybGKdighM.png)

3. 配置`php.ini`，进入`.\php-8.0.12-Win32-vs16-x64`，刚下好的内容没有`php.ini`我们要复制一份`php.ini-development`然后改名即可

   ![image-20211112220758237](https://s2.loli.net/2021/12/05/NxVofUnz2tPrsAO.png)

   打开`php.ini`修改以下内容

   ```ini
   enable_dl = On
   cgi.force_redirect = 0　
   cgi.fix_pathinfo=1
   fastcgi.impersonate = 1
   cgi.rfc2616_headers = 1
   extension_dir = "./ext"
   doc_root = "../nginx-1.20.1/html"
   ;大概900多行有一大堆extension的看着开就行，真的不行就全开，按理说不影响
   ```

   里面东西实在太多了，差不多两千行，直接`Ctrl+F`查找指定内容就行，这些参数大多默认都是被注释掉的，可能有些参数不用配，反正这东西也玄学，我配了这些东西就可行

4. 测试`Nginx`是否运行正常，我也不知道为什么环境变量生效不了，所以我们需要跑到`nginx`文件目录下启动`nginx`

   ![image-20211112222214148](https://s2.loli.net/2021/12/05/gjGzeB1Ps5Oyurf.png)

   启动之后去任务管理器里面查看一下是否有这个进程

   ![image-20211112222336910](https://s2.loli.net/2021/12/05/SC5oatlYZge7fEi.png)

   如果没有的话尝试`.\nginx.exe -s reload`，尝试重启服务，系统会抛出错误的异常信息

5. 启动`PHP FastCGI`（这是什么？后面会讲到），并测试

   同样跑到PHP文件目录下打开控制台，输入`.\php-cgi.exe -b 127.0.0.1:9000`

   ![image-20211112223056457](https://s2.loli.net/2021/12/05/DO6UHltRIeESkYv.png)

   同样打开任务管理器确认是否存在`php-cgi.exe`进程

   ![image-20211112223157820](https://s2.loli.net/2021/12/05/9ntMEl8uKQgH7Lb.png)

6. 之后我们可以在`nginx`的`html`目录下放上我们的`.php`文件，之后就可以通过浏览器访问`localhost:80`端口并`/xx.php`直接访问到我们的php文件

   ![20211112224257.png](https://s2.loli.net/2021/12/05/4mahNT1xt5DcVfd.png)

## 原理概要

这样这个复杂的Nginx+PHP的环境就搭建好了，接下来简单介绍一下它的原理，实际上就是Nginx这个服务端本身自己并不能解释php文件，这时候他必须借助我们下载过来的php服务来解释，而FastCGI提供了两者交互信息的通道，当Nginx遇到一个php文件时，他就借助FastCGI将它交给php解释器， 而php解释器又将解释好的html文件通过FastCGI返回给Nginx，从而可以在页面上显示正确的html内容

而我们上面配的这么一大堆东西，都是为了建立起Nginx和PHP之间的联系，从而达到数据互通的效果

![image-20211112225333268](https://s2.loli.net/2021/12/05/ErB9puIJVRG4K8M.png)

大体就是这么个情况

## .bat快速启动/停止服务

美中不足的是凭什么我们打开php-cgi之后页面就停在那不动了？而且难道每次我们启动服务都得打开一遍相关目录吗？显然又费时又费力，不如创建一个`.bat`批处理文件，辅助我们快速启动/停止nginx服务和php-cgi

代码如下：

```bash
@echo off
echo Starting nginx...
D:
cd D:\PROGRAM\EXE\Environment\nginx-1.20.1
start .\nginx.exe
cd ..
cd .\php-8.0.12-Win32-vs16-x64\
echo Starting PHP FastCGI...
RunHiddenConsole .\php-cgi.exe -b 127.0.0.1:9000
echo 按任意键终止 Nginx 和 PHP 进程
pause>nul
echo Stopping nginx...  
taskkill /F /IM nginx.exe > nul
echo Stopping PHP FastCGI...
taskkill /F /IM php-cgi.exe > nul
echo 成功! 按任意键退出
pause>nul
```

> 由于之前没学过批处理文件的语法，这里对里面的内容进行解释
>
> - `echo [内容]`表示将要求内容显示在控制台上
> - `@ [内容]`表示所执行的内容代码不会显示在控制台上（但是该停还是会停）
> - `pause`暂停，并在控制台显示`请按任意键继续`字样，按下任意键后继续执行代码
> - `RunHiddenConsole`是一个插件（[下载][1]之后放进`C:\Windows`（或者其他环境变量下的路径下）即可），等于说重新打开了一个隐藏的控制台来执行后面的内容，在这里可以保证我们的php-cgi进程不会卡住不动并且关闭控制台后导致的进程强行被关闭，但导致的结果就是我们必须手动关闭进程，而不是通过关闭控制台关闭进程
> - `>nul`是前面的指令返回值为空，给`pause`就可以保证返回一个空值从而使我们自定义输出内容、
> - 注意其中的文件路径要改成自己的

![image-20211112230716294](https://s2.loli.net/2021/12/05/ZRqst9UiwaHNemB.png)

最终效果就是这样，如果乱码的话可以考虑改一下编码形式

## Docker环境下搭建

有关Docker下Nginx+PHP的环境搭建可以[参考](https://www.cnblogs.com/xingxia/p/docker_php.html)，其中我的终端代码如下

> 注意在此之前应该先裸启动一次nginx和php，将里面相应位置的配置文件先通过cp到本机，因为挂载操作本机文件的优先级大于容器内文件，当本机不存在指定文件/文件夹时默认也将容器内的文件夹删除

```shell
$ sudo docker run --name nginx -p 80:80 -v /home/chillyblaze/Documents/Development/Docker/Nginx/conf:/etc/nginx/conf.d -v /home/chillyblaze/Documents/Development/Docker/Nginx/html:/usr/share/nginx/html -v /home/chillyblaze/Documents/Development/Docker/Nginx/log:/var/log/nginx -d nginx
$ sudo docker run --name php -v /home/chillyblaze/Documents/Development/Docker/Nginx/html:/var/www/html -v /home/chillyblaze/Documents/Development/Docker/PHP/conf/www.conf:/usr/local/etc/php/www.conf -v /home/chillyblaze/Documents/Development/Docker/PHP/conf/php.ini:/usr/local/etc/php/php.ini -p 9000:9000 -d php:fpm
```

Nginx配置文件如下：

```conf
server {
        listen       80;
        server_name  localhost;
        root /var/www/html;
        charset utf-8;

        access_log  /var/log/nginx/access.log  main;
        error_log  /var/log/nginx/error.log;

        location / {
            index  index.html index.htm index.php;
            try_files $uri $uri/ /index.php?$query_string;
        }
        #error_page  404              /404.html;
        # redirect server error pages to the static page /50x.html
        #
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }

        location ~ \.php$ {
            fastcgi_index index.php;
            fastcgi_pass   172.17.0.3:9000;  # 根据自己情况填写
            fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
            include       fastcgi_params;
        }

        location ~ /\.ht {
            deny  all;
        }
}
```

同时注意配置文件中的内容比如和Docker网络中的ip对应，意味着第一次的启动顺序在之后的启动中都不能变化（启动一次容器会重新分配一次ip地址）

如上述的操作的话，之后`docker start`的时候就必须是先启动Nginx之后再启动PHP否则在Nginx中的配置文件将会失效

总之由于fpm版本的PHP的存在，使得我们不需要像Windows一样连接Fastcgi，方便了很多

[1]: https://blog.chillyblaze.xyz/usr/uploads/RunHiddenConsole.exe

# Win11快速安装WSA

进入[微软安装包抓包网址](https://store.rg-adguard.net/)，输入地址`https://www.microsoft.com/store/productId/9P3395VX91NR`，选择Slow通道

![image-20211112160822555](https://s2.loli.net/2021/12/05/8OLZUnQpuVERvaW.png)

找到如下的安装包点击下载，如果下载不了就直接右键复制地址之后地址栏粘贴打开

下载好之后**以管理员方式**运行powershell，输入`add-AppxPackage [文件位置]`即可安装

![image-20211112161120949](https://s2.loli.net/2021/12/05/5hUSds1J4Zim2Oy.png)

等待安装完成搜索栏直接搜索打开WSA系统设置

![image-20211112161223206](https://s2.loli.net/2021/12/05/e4lBa21ZtMCSY9m.png)

打开开发者模式进入管理开发人员设置就可以启动安卓模拟机，可以通过显示的端口进行adb连接

![image-20211112161353298](https://s2.loli.net/2021/12/05/SgXVl6D8BbfmvMn.png)

- 下载[图形化APK安装界面](https://github.com/Paving-Base/APK-Installer/releases/tag/v0.0.3)，之后在保证上面显示IP地址的情况下下载APK安装包点击即可安装

  安装完成后直接在搜索框内搜索应用名打开即可

  ![image-20211112162721536](https://s2.loli.net/2021/12/05/7Hu6VAmhaTQOCpj.png)

除了这种自动化安装方式之外，我们也可以通过adb连接手动安装

1. 下载[开发者调试工具](https://developer.android.google.cn/studio/releases/platform-tools?hl=zh-cn)

2. 在下载工具目录下打开终端，adb连接上面所示的端口，显示完成后`adb install [apk文件位置]` 即可

   ![image-20211112163358158](https://s2.loli.net/2021/12/05/dOzjFcberSWZmGH.png)

3. 除了这些指令之外，只要连接上了WSA，就可以像调试正常安卓手机一样调试它



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

## IDEA集成Git

由于正常的开发中我们并不会天天使用命令行进行git的操作，因此我们借用IDEA平台进行git的集成，同时顺便巩固和记忆git的运行模式

1. 首先随便先创建一个项目，这里以SpringBoot项目为例

   ![image-20211029174845927](https://s2.loli.net/2021/12/05/n6kVTFacixMj3Lb.png)

   看起来多正常，这时候我们就要给他添加git的依赖

# Typecho一些奇怪的小问题

## 无法上传.exe

不知道为什么设置里面无论怎么设置文件上传类型为exe都通过不了，大概是什么神秘过滤器把包含exe的请求给截断了，一气之下直接去文件目录改

![image-20211113213742546](https://s2.loli.net/2021/12/05/2Wta1QMYZUgGyL7.png)

之后在编辑文章界面搞个链接链过来就行了

![image-20211113213908766](https://s2.loli.net/2021/12/05/C5gavLJ9M4lhOpQ.png)

## 更改DNS域名解析问题

由于bk的前缀太难看了就在CloudFlare里面改成了blog二级域名

然后就要去宝塔面板里面改一下访问域名

![image-20211114001503841](https://s2.loli.net/2021/12/05/vyaDWnUMd54STzE.png)

![image-20211114001720307](https://s2.loli.net/2021/12/05/wVSb9f1Je7YEiIL.png)

然而改完发现网站名并没有修改掉，看着很不爽，于是要去`/www/server/panel/data`把`default.db`拷出来拿Navicat打开，找到sites表把name一栏改掉就行了

![20211114002627.png](https://s2.loli.net/2021/12/05/NJpCbv8TEWHncQz.png)

这样我们打开博客发现电脑似乎没什么问题，但是一到手机上就一张图片都显示不出来，这就需要去Typecho后台寻找问题

![image-20211114002435536](https://s2.loli.net/2021/12/05/BqsUKv16EXFjlG5.png)

修改正确了即可，当然还有问题就得去外观的后台里面找之前设定过的url了

# V2ray搭建相关

## 基础：V2ray+TLS+tcp

这是CentOS版的，下面可能变成Debian，在大体上都是一样的

首先是下载和配置V2ray

1. 首先要配置一下我们的时区，不然V2ray坑爹的特性会让我们使用的设备无法连接

   ```bash
   date -R
   timedatectl set-local-rtc 1
   timedatectl set-timezone Asia/Shanghai
   ```

2. 接着我们要关闭防火墙/开放之后我们需要连接的端口（此处为443）

   - 关闭防火墙

     ```bash
     systemctl stop firewalld
     systemctl disable firewalld  # 开机不启动
     ```

   - 开放特定端口

     ```bash
     firewall-cmd --zone=public --add-port=443/tcp --permanent
     systemctl restart firewalld.service
     ```

   - 查看防火墙信息/端口开放信息

     ```bash
     systemctl status firewalld.service
     firewall-cmd --list-ports
     ```

3. 安装一些依赖包

   ```bash
   yum install curl
   yum install socat
   yum install git
   ```

4. 安装和更新V2ray

   ```bash
   curl -O https://raw.githubusercontent.com/v2fly/fhs-install-v2ray/master/install-release.sh
   curl -O https://raw.githubusercontent.com/v2fly/fhs-install-v2ray/master/install-dat-release.sh  # 下载V2ray内容
   bash install-release.sh  # 安装V2ray
   bash install-dat-release.sh  # 确定来访者时区用的
   ```

5. 创建和配置V2ray配置文件

   ```bash
   cd /usr/local/etc/v2ray/
   vi config.json
   ```

   ```json
   {
    "inbounds": [
       {
         "port": 443, // 建议使用 443 端口
         "protocol": "vmess",    
         "settings": {
           "clients": [
             {
               "id": "e480fd2b-c733-485e-8d18-f0ed4ca4a430",  //UUID
               "alterId": 16 //额外id
             }
           ]
         },
         "streamSettings": {
           "network": "tcp", //协议自己替换比如WS
           "security": "tls", // security 要设置为 tls 才会启用 TLS
           "tlsSettings": {
             "certificates": [
               {
                 "certificateFile": "/etc/v2ray/v2ray.crt", // 证书文件
                 "keyFile": "/etc/v2ray/v2ray.key" // 密钥文件
               }
             ]
           }
         }
       }
     ],
     "outbounds": [
       {
         "protocol": "freedom",
         "settings": {}
       }
     ]
   }
   ```

现在我们的V2ray就已经安装好了，但是由于我们在配置文件里启用了TLS，所以接下里开始注册和创建我们的TLS证书和密钥

1. 克隆远程`acme`仓库，这是一个免费构建证书的工具，并验证自己的身份，用于下载远程的内容

   ```bash
   git clone https://github.com/acmesh-official/acme.sh.git
   
   cd ./acme.sh  # 进入工作目录
   ./acme.sh --install -m qys.chillyblaze@gmail.com  # 输入自己的邮箱用于验证（必需）
   ```

2. 接下来更新一下内容，并且指定一下创建证书的服务类型

   ```bash
   ./acme.sh --upgrade
   .acme.sh  --set-default-ca  --server  letsencrypt  # letsencrypt是一个免费TLS证书颁发机构
   ```

3. 找到我们当时在`config.json`里面指定的证书存放路径，在其内申请证书

   ```bash
   cd /etc
   mkdir v2ray
   sudo ~/.acme.sh/acme.sh --issue -d [申请域名] --alpn -k ec-256  # 向远程发起一个为目标域名申请一个ECC证书的请求，并且通过告诉他通过本机的80端口接收证书（默认）
   ~/.acme.sh/acme.sh --installcert -d [申请域名] --fullchainpath /etc/v2ray/v2ray.crt --keypath /etc/v2ray/v2ray.key --ecc  # 从远程把申请到的证书下载过来，放到指定位置下的指定文件内
   ```

4. 然后我们就会发现目标目录下出现了`v2ray.crt`（证书文件）和`v2ray.key`（密钥文件），由于下过来的密钥文件默认是不允许访问修改的，我们还得改一下他的权限，接着重启V2ray服务即可，顺便还可以设置一下开机自启

   ```bash
   cd v2ray
   chmod 644 v2ray.key
   service v2ray restart
   service v2ray status  # 查看运行状态
   systemctl enable v2ray
   ```

最终效果如下，我们可以通过[检测网站](https://www.ssllabs.com/ssltest/)来看一下我们的TLS是否部署成功（输入域名即可）

![image-20211201175910420](https://s2.loli.net/2021/12/05/eXKuFIlDk8pGbRV.png)

## docker容器内部署

1. 下载和安装docker（详见docker教程）

   > 注意不是直接yum install docker，详见[docker官方网站](https://docs.docker.com/engine/install/centos/)！

2. 拉取镜像`docker pull teddysun/v2ray `

3. 准备好上面的内容，包括`config.json`，`v2ray.key`和`v2ray.crt`

4. 将上面的文件一起放到一个自己喜欢的目录下，记住这个目录的路径

5. 启动镜像`docker run -d -p [配置文件里填的端口]:[配置文件里填的端口] --name [生成容器名字] --restart=always -v [本机存放配置文件路径]:/etc/v2ray teddysun/v2ray `

6. 然后就成功了，就是这么简单

# 配置主机名

> 甲骨文云的`CentOS 7`在使用`hostnamectl set-hostname`命令修改主机名时,重启服务器后依旧会恢复为 Web 端创建实例时所设置的名字.网上查找了各种方法都无效,最终找到了解决方案.

编辑修改`oci-hostname.conf`文件

```shell
vi /etc/oci-hostname.conf
```

将`PRESERVE_HOSTINFO=0`中的的值`0`修改为`1`

```
# This configuration file controls the hostname persistence behavior for Oracle Linux
# compute instance on Oracle Cloud Infrastructure (formerly Baremetal Cloud Services)
# Set PRESERVE_HOSTINFO to one of the following values
#   0 -- default behavior to update hostname, /etc/hosts and /etc/resolv.conf to 
#        reflect the hostname set during instance creation from the metadata service
#   1 -- preserve user configured hostname across reboots; update /etc/hosts and 
#           /etc/resolv.conf from the metadata service  
#   2 -- preserve user configured hostname across instance reboots; no custom  
#        changes to /etc/hosts and /etc/resolv.conf from the metadata service,
#        but dhclient will still overwrite /etc/resolv.conf
#   3 -- preserve hostname and /etc/hosts entries across instance reboots; 
#        update /etc/resolv.conf from instance metadata service
PRESERVE_HOSTINFO=0
```

使用`hostnamectl set-hostname`命令修改主机名即可.重启也不会失效.

```shell
hostnamectl set-hostname xxxxxx
```

# Zsh

bash指令只是图一乐，真要用终端还得靠我Zsh，通过特定框架，主题和插件的辅助，你的终端不仅能脱离干瘪的外观，更能拥有更加畅快的终端命令体验

## Oh My Zsh

说到Zsh，就不得不提传说中的神级框架Oh My Zsh，正是由于它的出现，Zsh逐渐变成了最受大众欢迎的终端之一，最主要这还得归功于其强大的主题和插件功能

1. 下载Zsh，并启动Zsh作为默认shell

   ```shell
   yum install zsh
   chsh -s /bin/zsh
   ```

   > 如果遇到PAM: Authentication failure报错，就改变`/etc/pam.d/chsh:`
   >
   > ```
   > auth       sufficient   pam_shells.so
   > ```
   >
   > 即可

   之后为了使生效，重启终端即可

2. 一键安装Oh My Zsh

   ```shell
   wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | sh
   ```

3. 安装完Oh My Zsh之后，我们会在家目录下发现一个`.zshrc`文件，这就是Oh My Zsh为我们配的Zsh初始核心配置文件（如果没有装Oh My Zsh，我们第一次启动Zsh的时候也会根据我们的简单选择创建这个文件），也是我们玩转Zsh的开始，我们可以先粗略看一下里面的内容

   ```shell
   # Enable Powerlevel10k instant prompt. Should stay close to the top of ~/.zshrc.
   # Initialization code that may require console input (password prompts, [y/n]
   # confirmations, etc.) must go above this block; everything else may go below.
   
   # If you come from bash you might have to change your $PATH.
   # export PATH=$HOME/bin:/usr/local/bin:$PATH
   
   # Path to your oh-my-zsh installation.
   export ZSH="/root/.oh-my-zsh"
   
   # Set name of the theme to load --- if set to "random", it will
   # load a random theme each time oh-my-zsh is loaded, in which case,
   # to know which specific one was loaded, run: echo $RANDOM_THEME
   # See https://github.com/ohmyzsh/ohmyzsh/wiki/Themes
   ZSH_THEME="robbyrussell"
   
   # Set list of themes to pick from when loading at random
   # Setting this variable when ZSH_THEME=random will cause zsh to load
   # a theme from this variable instead of looking in $ZSH/themes/
   # If set to an empty array, this variable will have no effect.
   # ZSH_THEME_RANDOM_CANDIDATES=( "robbyrussell" "agnoster" )
   
   # Uncomment the following line to use case-sensitive completion.
   # CASE_SENSITIVE="true"
   
   # Uncomment the following line to use hyphen-insensitive completion.
   # Case-sensitive completion must be off. _ and - will be interchangeable.
   # HYPHEN_INSENSITIVE="true"
   
   # Uncomment one of the following lines to change the auto-update behavior
   # zstyle ':omz:update' mode disabled  # disable automatic updates
   # zstyle ':omz:update' mode auto      # update automatically without asking
   # zstyle ':omz:update' mode reminder  # just remind me to update when it's time
   
   # Uncomment the following line to change how often to auto-update (in days).
   # zstyle ':omz:update' frequency 13
   
   # Uncomment the following line if pasting URLs and other text is messed up.
   # DISABLE_MAGIC_FUNCTIONS="true"
   
   # Uncomment the following line to disable colors in ls.
   # DISABLE_LS_COLORS="true"
   
   # Uncomment the following line to disable auto-setting terminal title.
   # DISABLE_AUTO_TITLE="true"
   
   # Uncomment the following line to enable command auto-correction.
   # ENABLE_CORRECTION="true"
   
   # Uncomment the following line to display red dots whilst waiting for completion.
   # You can also set it to another string to have that shown instead of the default red dots.
   # e.g. COMPLETION_WAITING_DOTS="%F{yellow}waiting...%f"
   # Caution: this setting can cause issues with multiline prompts in zsh < 5.7.1 (see #5765)
   # COMPLETION_WAITING_DOTS="true"
   
   # Uncomment the following line if you want to disable marking untracked files
   # under VCS as dirty. This makes repository status check for large repositories
   # much, much faster.
   # DISABLE_UNTRACKED_FILES_DIRTY="true"
   
   # Uncomment the following line if you want to change the command execution time
   # stamp shown in the history command output.
   # You can set one of the optional three formats:
   # "mm/dd/yyyy"|"dd.mm.yyyy"|"yyyy-mm-dd"
   # or set a custom format using the strftime function format specifications,
   # see 'man strftime' for details.
   # HIST_STAMPS="mm/dd/yyyy"
   
   # Would you like to use another custom folder than $ZSH/custom?
   # ZSH_CUSTOM=/path/to/new-custom-folder
   
   # Which plugins would you like to load?
   # Standard plugins can be found in $ZSH/plugins/
   # Custom plugins may be added to $ZSH_CUSTOM/plugins/
   # Example format: plugins=(rails git textmate ruby lighthouse)
   # Add wisely, as too many plugins slow down shell startup.
   plugins=(git zsh-autosuggestions)
   
   source $ZSH/oh-my-zsh.sh
   
   # User configuration
   
   # export MANPATH="/usr/local/man:$MANPATH"
   
   # You may need to manually set your language environment
   # export LANG=en_US.UTF-8
   
   # Preferred editor for local and remote sessions
   # if [[ -n $SSH_CONNECTION ]]; then
   #   export EDITOR='vim'
   # else
   #   export EDITOR='mvim'
   # fi
   
   # Compilation flags
   # export ARCHFLAGS="-arch x86_64"
   
   # Set personal aliases, overriding those provided by oh-my-zsh libs,
   # plugins, and themes. Aliases can be placed here, though oh-my-zsh
   # users are encouraged to define aliases within the ZSH_CUSTOM folder.
   # For a full list of active aliases, run `alias`.
   #
   # Example aliases
   alias zshconfig="vi ~/.zshrc"
   alias ohmyzsh="vi ~/.oh-my-zsh"
   ```

   可以发现，最重要的就是Oh My Zsh在Zsh的初始配置中加上了`source $ZSH/oh-my-zsh.sh`这一句话，使得我们可以在这个文件中通过关键字清晰的配置我们想要的所有内容

当然，为了入门Zsh，我们需要这样强大的框架的辅助，而当我们通过框架慢慢熟悉Zsh的工作原理，运行流程之后，我们就可以尝试删去`.zshrc`文件和`.oh-my-zsh`文件，通过自己自定义配置来重新配置Zsh内容，毕竟框架就像一个巨大的集成库，繁琐而又复杂，远没有我们自定义配置后的小巧简洁

## Powerlevel10k主题

重启终端，我们可以看到我们的终端样式已经变了，事实上这就是在配置文件中`THEME`一栏中填的`robbyrussell`主题，不过大多数的框架都是内置的不如外设的，在[全世界最喜欢的Zsh主题](https://www.slant.co/topics/7553/~theme-for-oh-my-zsh)中，Powerlevel10k高居榜首，事实上也证明它傻瓜式的自定义步骤也极度满足了我们所有的要求和xp，让我们有了不得不入手的理由

1. 配置主题

   ```shell
   git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
   ```


2. 然后`vi ~/.zshrc`修改oh my zsh配置文件，找到`ZSH_THEME="powerlevel10k/powerlevel10k" `修改即可
3. 先别着急重启终端，让我们先进入下一步，之后再开始慢慢享受Powerlevel10k带给我们的极致观感

## Nerd Font字体

如果就这样认为一切都完备之后高兴的进入了Powerlevel10k的配置，那估计你只能拥有一个相对失败的体验，因为你进去之后会发现自己的终端似乎突然拉跨了，面对Powerlevel10k提供的各种有意思的小图标（Awesome Font），然而我们只能看着屏幕上出现的大块乱码独自流泪

![image-20211202150232197](https://s2.loli.net/2021/12/05/rxzj2QnZHLT36Uc.png)

这时候就需要NerdFont字体的帮助，这款字体提供了几乎所有格式的符号及字体内容，涵盖量可谓是 应有尽有，十分好用，注意终端显示问题是终端的问题而不是服务器的问题，因此我们需要调整的是终端字体内容，比如我用的Windows的SSH登录的远程服务器，那么我就需要改Windows终端的字体

1. 进入[NerdFont官网](https://www.nerdfonts.com/font-downloads)选择一款自己喜欢的字体（我这里挑选的是Hack Nerd，当然我感觉Cousine也很不错），点击下载

2. 下载完成之后是一个压缩包，里面有这种字体的各个形式版本（斜体/粗体等），我选择的是斜粗体，之后直接点击安装即可

3. 然后在终端中配置字体内容，我用的是Tabby终端，因此在设置里找到字体选项填入我们的字体名字即可

   ![image-20211202151116052](https://s2.loli.net/2021/12/05/8pSaf2ELcUxKjWC.png)

   > 如果比如是Windows终端，也是去寻找一下其中设置的选项，比如这样的，Ubuntu等具有图形化界面的终端也是类似，反正要么右击，要么菜单设置，实在不行就百度即可
   >
   > ![image-20211202151910396](https://s2.loli.net/2021/12/05/qZvdczEV71fjg9M.png)

4. 之后我们只需要重启终端，注意现在会进入Powerlevel10k的设置界面，跟着引导一路下来，最后你也可以生成一个好看的终端样式

![image-20211202151252831](https://s2.loli.net/2021/12/05/fHsrbp1OzdumExe.png)

> ~~当然我的为了好玩搞得好像稍微有点花哨了~~

## Autojump插件

终端美化完成了，是时候介绍更为强大的Autojump插件了，这个插件可以帮你快速的跳转到曾经使用过的目录，甚至你可以不需要知道目录的全名

1. 克隆仓库`git clone git://github.com/joelthelion/autojump.git`

2. 无脑安装

   ```shell
   cd autojump
   ./install.py
   ```

3. 将以下代码复制到`.zshrc`文件中即可，保证每次启动zsh时都能加载这个插件

   ```.zshrc
   [[ -s ~/.autojump/etc/profile.d/autojump.sh ]] && . ~/.autojump/etc/profile.d/autojump.sh
   ```

4. 重启终端，或者直接`source ~/.zshrc`即可

然而，上面这些都是你没有装Oh My Zsh的情况，现在你有了这个完美的框架，你要做的可能只是直接在配置文件里面的`plugins`后面的括号里轻松的打上`autojump`（两个插件之间用空格隔开），重启即可

## zsh-syntax-highlighting插件

而当Oh My Zsh的疏忽忘记把插件放进来时，我们也可以通过将插件仓库克隆到本地`/root/.oh-my-zsh/custom/plugins`，之后也只需要在配置文件中添加上插件名称即可

1. 克隆远程仓库

   ```shell
   git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
   ```

2. 在配置文件中找到插件一栏直接添加即可

   ![image-20211202154955052](https://s2.loli.net/2021/12/05/cXql6eCKbDpr9YV.png)

3. 重启或`source ~/.zshrc`

# Manjaro

听闻Linux是办公写代码的神器，又听闻高端人士身边常备系统盘若干枚，又恰巧收到了来自母亲大人的2TB SSD一个，不将其用起来简直是暴殄天物，于是便萌生了在这个固态上装个Linux，从而使得能够拥有一个可即插即用的装逼随身系统的想法

选择什么Linux系统可以说是一个比较头疼的问题，一开始使用还是保守的选择了比较熟悉的Ubuntu，但是又不够保守的选择了非长期支持版体验（21.10），然而没搞几下不知道是系统bug还是我操作不当，出现大大小小的问题，折腾半天网络中还搜索不到相关解决办法，这下一下让我认清了我就不适合这种保守的，可能只用LTS系统才能保证使用的系统，况且本身Ubuntu某一方面来说还就只是给服务器添加一个图形化界面的缝合产物，在我看来本身就不是为了日常使用而开发的系统

参考了一下[Linux的排行网站](https://distrowatch.com/dwres.php?resource=popularity)，结合网络上的各种评论，最终选择了应该是最受人们欢迎，且社区成熟的Manjaro系统，下一步就是将其安装到我的SSD上了！

## 准备工作

1. 一个Windows环境
2. 一个8G以上U盘（安装盘）
3. SSD（系统盘）

## 安装

1. **下载Manjaro镜像文件(.iso)**，我们会惊奇的发现[官网](https://manjaro.org/)居然有三个版本的Manjaro，其实这代表的都是Manjaro，只是用的不同的桌面系统而已，事实上，Manjaro可以看作一个配置整合包，建立在Arch Linux的基础上，由于原本的ArchLinux是没有图形化界面的，因此Manjaro理所应当给予用户自主选择图形化系统的权利

   > 注意如果官网下载速度太慢可以尝试[SourceForce](https://sourceforge.net/projects/manjarolinux/files/)，据我查找了差不多一个下午的经验来说，似乎是也只有这两个平台可以下载到官方版本镜像了。。。~~（什么清华大学镜像站都是骗人的）~~
   >
   > ![image-20220124170414390](https://s2.loli.net/2022/01/24/ijB9deIhn4NDuPl.png)

   我选择的是Gnome版本，这也就是Ubuntu默认的桌面系统，完美的体现了Linux的独特性和极简风格，不知道为什么网络上那么多不看好它的，神秘

2. 下载一个创建USB启动盘工具，这里极度推荐开箱即用的[rufus](https://rufus.ie/en/)

   ![img](https://upload-images.jianshu.io/upload_images/10887067-07513e8ea6ff6520.png?imageMogr2/auto-orient/strip|imageView2/2/format/webp "做的时候忘记截图这里用网图代替")

   最上方选择自己的U盘，下面选择下载到的镜像，rufus会自动帮你选择DD镜像模式写入，点击开始即可

   > 注意到安装盘制作完毕之后可能会出现比如电脑找不到你的U盘了，甚至通过比如`DiskGenius`也搜索不到你的安装盘内部信息，请不要着急，Rufus说制作成功就是成功了，直接下一步即可

3. 关闭secure boot，关闭电脑，再次开机的时候疯狂按f2，进入bios，之后根据每个电脑的不同，找到其中的Security->secure boot选项，调成disable即可

4. 确保SSD里面什么都没有并且连接妥当，在电脑开机状态下按住`shift`然后点击重启键，即可进入Windows的安全模式，在这里可以选择通过U盘启动（正常的话就是选择其他设备启动->U盘启动），接着选择你的U盘名即可

5. 不出意外的话在稍等片刻之后你就会进入manjaro的安装界面，唯一需要注意的就是在第四步分区的时候选择手动分区（最后一个选项），接着在上面选择你的SSD，分区规则选择GPT，并且之后根据自己的SSD容量和电脑配置选择自己的分区方案，下面是我的分区详细

   ![image-20220124180440741](https://s2.loli.net/2022/01/24/bQltr5d6m4GDNKS.png)

   除此之外还有一个交换分区，为了避免在其他电脑上发生冲突，我设置成了10G，但是一般来说应该8G足以

   > 要注意这个分区策略和ubuntu还是有区别的，尤其要设定`/boot/efi`这个分区（不然无法启动），并且像是`/`、`swap`、`boot/efi`分区都要在最后打上相应的标记，不然很可能无法安装成功或成功启动

6. 完成之后重启时同样疯狂按f2进入bios，在boot选项中找到刚刚安装好的Manjaro系统，将其调至顶部，接着保存->启动即可进入Manjaro的默认grub

   > GNU GRUB（GRand Unified Bootloader简称“GRUB”）是一个来自GNU项目的多操作系统启动程序。GRUB是多启动规范的实现，它允许用户可以在计算机内同时拥有多个操作系统，并在计算机启动时选择希望运行的操作系统。GRUB可用于选择操作系统分区上的不同内核，也可用于向这些内核传递启动参数。

7. 安装完成，享受Manjaro带给你的极致享受

